# Docs - Data Collection Chatbot
**Developed by Radari AI Limited**

This repository contains the readme file for the hosted chatbot service.


_Last Updated: 07/10/2024_

---

## API Routes

**Base URL:**  
`https://kits-tutor-bot.up.railway.app`

**[Endpoint]** `/bot-invoke` (POST): Invoke chatbot to extract user data and return bot response, with full data if the collection is complete.

- **URL format:**  
  `https://kits-tutor-bot.up.railway.app/bot-invoke/{phone_number}`

- **Example:**  
  `https://kits-tutor-bot.up.railway.app/bot-invoke/67604087`

Returns 200 if the invoke is successful, 400 otherwise. 

#### JSON input format:
```json
{
    "latest_user_message": "你好，想找一個有經驗的老師專補小三"
}
```

#### JSON output format:
Incomplete collection:
```json
{
    "message": "請提供您的姓名、就讀學校以及有沒有特別要求。"
}
```
Complete collection:
```json
{
    "data": {
        "name": "陳小明",
        "phone_number": "67604087",
        "requirement": "要一個有經驗的老師專補小三",
        "school": "國際中學",
        "subjects": [
            "數學"
        ]
    },
    "message": "已收集到您的資料，將為您尋找合適的數學補習老師。稍後會有導師聯繫您。"
}
```

## Scope of service
- Accepted message format is text only. Images, videos or voice messages are not processed, and the bot is expected to give generic responses.
- Conversation is unique for each phone number, hence the bot is capable of handling multiple conversations at once.
- After the data collection is completed, the conversation will be marked as ended. Bot should repeat the same message and staff members should start another conversation.

## Full Example (python)
```python
import requests
import json

base_url = 'https://kits-tutor-bot.up.railway.app'

phone_number = 67604087

# Define the search route URL
invoke_url = f'{base_url}/bot-invoke/{phone_number}'

# Define your query
query = {
    "latest_user_message": "你好，想找一個有經驗的老師專補小三"
}

# Set headers for the request (Content-Type is necessary for sending JSON)
headers = {
    'Content-Type': 'application/json'
}

# Send POST request to the search route
response = requests.post(invoke_url, headers=headers, json=query)

# Check if the request was successful
if response.status_code == 200:
    # Parse the response JSON
    result = response.json()
    print("Message:", json.dumps(result, indent=4, ensure_ascii=False))
else:
    print(f"Failed to invoke bot. Status code: {response.status_code}")
    print(f"Response content: {response.text}")

```
