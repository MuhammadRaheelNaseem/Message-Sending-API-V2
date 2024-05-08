# Message-Sending-API-V

## Introduction
These Python scripts demonstrate how to send SMS messages using the Vonage (formerly Nexmo) SMS API. They provide two different implementations for sending SMS messages, catering to both MicroPython and standard Python environments.

## Prerequisites
Before using these scripts, you need to sign up for a Vonage account and obtain your API key and API secret. Additionally, ensure that you have Python installed on your system. For MicroPython users, you need the `urequests` library, while for standard Python, the `requests` library is required.

## Code 1: Using MicroPython Requests Library (urequests)
```python
import requests as urequests

def send_sms(api_key, api_secret, from_number, to_number, message):
    # Define the Vonage API endpoint and headers
    url = "https://rest.nexmo.com/sms/json"
    headers = {"Content-Type": "application/x-www-form-urlencoded"}
    
    # Prepare data for the POST request
    data = {
        "api_key": api_key,
        "api_secret": api_secret,
        "from": from_number,
        "to": to_number,
        "text": message
    }
    
    # Send the POST request and print the response
    response = urequests.post(url, headers=headers, data=data)
    response_data = response.json()
    print(response_data)
    response.close()

# Replace these variables with your actual Vonage API key, API secret, and phone numbers
API_KEY = "your_api_key"
API_SECRET = "your_api_secret"
FROM_NUMBER = "your_vonage_number"
TO_NUMBER = "recipient_number"
MESSAGE = "Hello from IoT Device"

send_sms(API_KEY, API_SECRET, FROM_NUMBER, TO_NUMBER, MESSAGE)
```
**Explanation:**
- This script utilizes the `urequests` library, suitable for MicroPython environments with limited resources.
- The `send_sms` function constructs a POST request to the Vonage API endpoint with necessary parameters.
- After sending the request, it prints the response received from the API.

## Code 2: Using Requests Library (Python)
```python
import requests
import json

def send_sms(api_key, api_secret, from_number, to_number, message):
    # Define the Vonage API endpoint and headers
    url = "https://rest.nexmo.com/sms/json"
    headers = {"Content-Type": "application/x-www-form-urlencoded"}
    
    # Prepare data for the POST request
    data = {
        "api_key": api_key,
        "api_secret": api_secret,
        "from": from_number,
        "to": to_number,
        "text": message
    }
    
    try:
        # Send the POST request
        response = requests.post(url, headers=headers, data=data)
        response_data = response.json()
        print(response_data)
        response.close()
        
        # Check if the message was sent successfully
        if response_data.get("messages") and response_data["messages"][0].get("status") == "0":
            print("Message sent successfully!")
        else:
            print("Failed to send message. Error:", response_data.get("messages")[0]["error-text"])
    except Exception as e:
        print("Error:", e)

# Replace these variables with your actual Vonage API key, API secret, and phone numbers
API_KEY = "your_api_key"
API_SECRET = "your_api_secret"
FROM_NUMBER = "your_vonage_number"
TO_NUMBER = "recipient_number"
MESSAGE = "Hello from From IoT Device"

send_sms(API_KEY, API_SECRET, FROM_NUMBER, TO_NUMBER, MESSAGE)
```
**Explanation:**
- This script employs the `requests` library, suitable for standard Python environments.
- Similar to the MicroPython script, `send_sms` function constructs a POST request to the Vonage API endpoint.
- Additionally, it includes error handling to manage exceptions and checks the response for successful message delivery.

## Usage
To use these scripts:
1. Replace the placeholder variables with your actual Vonage API key, API secret, and phone numbers.
2. Run the script using Python.

## Conclusion
These scripts provide simple examples of how to send SMS messages using the Vonage SMS API in Python, catering to both MicroPython and standard Python environments. They serve as a foundation for integrating SMS functionality into your projects, such as IoT applications or automated notification systems.
