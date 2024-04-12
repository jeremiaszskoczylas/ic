# ic


import time
from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver.common.keys import Keys


service = Service(executable_path="chromedriver.exe")
driver = webdriver.Chrome(service=service)


wait = WebDriverWait(driver, 10)
driver.get("https://www.intercity.pl/pl/")

departue_date = '2024-04-13'
departue_time = "07:31"

wait.until(EC.element_to_be_clickable((By.XPATH, '//*[@id="CybotCookiebotDialogBodyLevelButtonLevelOptinAllowallSelection"]'))).click()

#selection of starting station
wait.until(EC.element_to_be_clickable((By.ID, 'stname-0')))
clear_stname0 = driver.find_element(By.ID, 'stname-0')
clear_stname0.send_keys(Keys.CONTROL + "a")
clear_stname0.send_keys(Keys.DELETE)
driver.find_element(By.ID, 'stname-0').send_keys("Wrocław Główny")
wait.until(EC.element_to_be_clickable((By.XPATH, '//ul[@class="typeahead dropdown-menu"]'))).click()

#selection of ending station
clear_stname1 = wait.until(EC.element_to_be_clickable((By.ID, 'stname-1')))
clear_stname1.send_keys(Keys.CONTROL + "a")
clear_stname1.send_keys(Keys.DELETE)
driver.find_element(By.ID, 'stname-1').send_keys("Warszawa Centralna")
wait.until(EC.element_to_be_clickable((By.XPATH, '(//a[@href="#"])[2]'))).click()

#choice of departure date
wait.until(EC.element_to_be_clickable((By.XPATH, '//button[@id="date_picker_trigger"]'))).click()
wait.until(EC.element_to_be_clickable((By.XPATH, f'//button[@date="{departue_date}"]'))).click()

#choice of departure time
clearfield = driver.find_element(By.XPATH, '//input[@id="ic-seek-time"]')
clearfield.send_keys(Keys.CONTROL + "a")
clearfield.send_keys(Keys.DELETE)
driver.find_element(By.XPATH, '//input[@id="ic-seek-time"]').send_keys(f'{departue_time}')

#click serach button
wait.until(EC.element_to_be_clickable((By.XPATH, '//button[@name="search"]'))).click()

time.sleep(3)
#selecting a specific call
wait.until(EC.element_to_be_clickable((By.XPATH, '//div[@class="godziny do_prawej" and text()="07:31"]'))).click()












print("spie1")
wait.until(EC.element_to_be_clickable((By.XPATH, '//div[@class="godziny do_prawej" and text()="07:31"]'))).click()
print("spie2")
time.sleep(400)
driver.quit()
