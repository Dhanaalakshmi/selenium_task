## Selenium_task:
## Name: DHANA LAKSHMI A
## Reg no: 212223040033
## Task 01: Actor check:
## Code:
```
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
import time
driver = webdriver.Chrome()
driver.get("https://www.google.com")
time.sleep(2)
search_box = driver.find_element(By.NAME, "q")
search_box.send_keys("Actor Suriya")
search_box.send_keys(Keys.ENTER)
time.sleep(5)
print("Search completed")
input("Press Enter to close the browser...")
driver.quit()
```
## Output:
<img width="1816" height="1005" alt="image" src="https://github.com/user-attachments/assets/91112c31-d12b-48b7-a81d-18a4a7185433" />

## Task 02: Product list check:
## Code:
```
import time
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

driver = webdriver.Chrome()

try:
    # Open SauceDemo login page
    driver.get("https://www.saucedemo.com/")

    # Locate login inputs and log in
    username = driver.find_element(By.ID, "user-name")
    password = driver.find_element(By.NAME, "password")
    login_btn = driver.find_element(By.ID, "login-button")

    username.send_keys("standard_user")
    password.send_keys("secret_sauce")
    login_btn.click()

    # Wait until inventory page loads
    WebDriverWait(driver, 10).until(
        EC.presence_of_element_located((By.CLASS_NAME, "inventory_item"))
    )

    # Locate all product cards
    products = driver.find_elements(By.CLASS_NAME, "inventory_item")
    print(f"Total products found: {len(products)}")

    visible_products = 0
    for index, product in enumerate(products, start=1):
        # Scroll product into view
        driver.execute_script("arguments[0].scrollIntoView(true);", product)
        time.sleep(0.3)  # brief pause for rendering

        title = product.find_element(By.CLASS_NAME, "inventory_item_name").text
        price = product.find_element(By.CLASS_NAME, "inventory_item_price").text
        img = product.find_element(By.TAG_NAME, "img")

        # Check if the image source loaded and element is displayed
        img_loaded = driver.execute_script(
            "return arguments[0].complete && typeof arguments[0].naturalWidth != 'undefined' && arguments[0].naturalWidth > 0", 
            img
        )

        if product.is_displayed() and img_loaded:
            visible_products += 1
            print(f"[{index}] Product Visible: '{title}' | Price: {price}")
        else:
            print(f"[{index}] Product Hidden/Not Visible: '{title}'")

    print(f"\nSummary: {visible_products}/{len(products)} products are fully visible.")

finally:
    time.sleep(3)
    driver.quit()
```
## Output:
<img width="1822" height="907" alt="Screenshot 2026-10-05 111448" src="https://github.com/user-attachments/assets/fdee90bd-ea89-4287-b2b1-26cb0809b643" />

## Task 03: Login to Flipkart:
## Code:
```
import time
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

driver = webdriver.Chrome()
wait = WebDriverWait(driver, 20)

try:
    print("1. Opening Flipkart...")
    driver.get("https://www.flipkart.com/")
    driver.maximize_window()

    print("2. Waiting for Login...")
    login = wait.until(
        EC.presence_of_element_located(
            (By.XPATH, "//span[normalize-space()='Login']")
        )
    )

    print("3. Clicking Login...")
    driver.execute_script("arguments[0].click();", login)

    time.sleep(2)

    print("4. Finding mobile number field...")

    mobile = wait.until(
        EC.visibility_of_element_located(
            (By.CSS_SELECTOR, "input[type='number']")
        )
    )

    print("5. Mobile field found!")

    mobile.click()
    mobile.clear()
    mobile.send_keys("7358452031")

    print("6. Mobile number entered successfully!")

    time.sleep(2)

    print("7. Finding Continue button...")

    continue_button = wait.until(
        EC.element_to_be_clickable(
            (By.XPATH, "//button[normalize-space()='Continue']")
        )
    )

    print("8. Continue button found!")

    driver.execute_script("arguments[0].click();", continue_button)

    print("9. Continue button clicked!")

    wait.until(
        EC.url_contains("/login/verify")
    )

    print("10. OTP page opened!")
    print("Enter the OTP manually in the browser.")

    input("After entering OTP and clicking Verify, press Enter here...")

    print("Login completed!")

    input("Press Enter to close the browser...")

except Exception as e:
    print("\nERROR:")
    print(type(e).__name__)
    print(e)

    input("\nBrowser is still open. Press Enter to close it...")

finally:
    driver.quit()
```
## Output:
<img width="1913" height="1015" alt="image" src="https://github.com/user-attachments/assets/84ba97f3-7134-4875-a44d-5d5dd8c565a4" />
