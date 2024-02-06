# How to send Notification to SeaTalk

# 1. Use notify the package in Python
import requests
from notify import Notifier
import os

# SeaTalk API endpoint
seatalk_api_url = 'https://api.seatalk.com/send_message'

# SeaTalk credentials
seatalk_system_account_id = 'system_account_id_here'
seatalk_access_token = 'your_access_token_here'

# Slack Webhook URL, replace with your own Webhook URL
slack_webhook_url = os.environ.get('SLACK_WEBHOOK_URL')

# Initialize Notifier instance
notifier = Notifier()

# Send message to SeaTalk
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

# Send message to Slack
def send_message_to_slack(text):
    notifier.notify(text, slack_webhook_url=slack_webhook_url)

# Main program logic
def main():
    # Send message to SeaTalk
    send_message_to_seatalk('This is a test message sent to SeaTalk!')

    # Send message to Slack
    send_message_to_slack('This is a test message sent to Slack!')

if __name__ == "__main__":
    main()
