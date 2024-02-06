
# 1. Use notify the package in Python
import requests
from notify import Notifier
import os

seatalk_api_url = 'https://api.seatalk.com/send_message'

seatalk_system_account_id = 'system_account_id'
seatalk_access_token = 'access_token'

slack_webhook_url = os.environ.get('SLACK_WEBHOOK_URL')

notifier = Notifier()

def send_message_to_seatalk(text):
    message = {
        'text': text,
        'receiver': seatalk_system_account_id
    }
    headers = {
        'Authorization': f'Bearer {seatalk_access_token}',
        'Content-Type': 'application/json'
    }
    response = requests.post(seatalk_api_url, json=message, headers=headers)
    if response.status_code == 200:
        print('Message sent to SeaTalk successfully!')
    else:
        print('Failed to send message to SeaTalk:', response.text)

def send_message_to_slack(text):
    notifier.notify(text, slack_webhook_url=slack_webhook_url)

def main():
    
    send_message_to_seatalk('This is a test message sent to SeaTalk!')

    send_message_to_slack('This is a test message sent to Slack!')

if __name__ == "__main__":
    main()
