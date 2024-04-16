import warnings
from flask import Flask
from flask_socketio import SocketIO, emit
from flask_cors import CORS
import threading
import logging
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
import time

logging.basicConfig(level=logging.INFO)
warnings.filterwarnings("ignore", category=UserWarning, module='urllib3')

app = Flask(__name__)
CORS(app)
socketio = SocketIO(app, cors_allowed_origins="*")

driver = None  # Define driver globally but initialize it in a specific context

def setup_selenium_with_mitmproxy():
    chrome_options = webdriver.ChromeOptions()
    chrome_options.add_argument('--ignore-certificate-errors')
    chrome_options.add_argument("user-agent=Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/123.0.0.0 Safari/537.36")
    chrome_options.add_experimental_option("excludeSwitches", ["enable-automation"])
    chrome_options.add_experimental_option('useAutomationExtension', False)
    chrome_options.add_argument("--disable-blink-features=AutomationControlled")

    return webdriver.Chrome(options=chrome_options)

def monitor_content(driver, selector, tracked_contents):
    elements = WebDriverWait(driver, 10).until(
        EC.presence_of_all_elements_located((By.CSS_SELECTOR, selector))
    )
    for element in elements:
        content = element.text.strip()
        if content and content not in tracked_contents:
            tracked_contents.add(content)
    return list(tracked_contents)

@socketio.on('start')
def handle_start():
    global driver
    driver = setup_selenium_with_mitmproxy()
    driver.get("https://you.com/")  # Change to your actual URL
    emit('response', {'message': 'Driver is ready and session started'})

@socketio.on('send_input')
def handle_input(data):
    user_input = data['input']
    if user_input.lower() == 'exit':
        emit('response', {'message': 'Exiting.'})
        return
    textarea = WebDriverWait(driver, 10).until(
        EC.presence_of_element_located((By.ID, "search-input-textarea"))
    )
    textarea.clear()
    textarea.send_keys(user_input + Keys.ENTER)
    time.sleep(3)  # Wait for content to potentially update
    emit('response', {'message': 'Input sent'})

@socketio.on('monitor')
def handle_monitor():
    selector = 'div.sc-410348ef-4.eutDKy'
    tracked_contents = set()
    contents = monitor_content(driver, selector, tracked_contents)
    emit('content_update', {'contents': contents})

@socketio.on('stop')
def handle_stop():
    if driver:
        driver.quit()
    emit('response', {'message': 'Driver has quit and session ended'})

if __name__ == "__main__":
    socketio.run(app, debug=True, port=5000, allow_unsafe_werkzeug=True)
