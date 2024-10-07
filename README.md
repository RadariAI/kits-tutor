# Docs - Data Collection Chatbot
**Developed by Radari AI Limited**
This repository contains the readme file for the hosted chatbot service.


_Last Updated: 07/10/2024_

---

## API Routes

**Base URL:**  
`https://kits-tutor-bot.up.railway.app`

### `/bot-invoke` (POST)

- **URL format:**  
  `https://kits-tutor-bot.up.railway.app/bot-invoke/{phone_number}`

- **Example:**  
  `https://kits-tutor-bot.up.railway.app/bot-invoke/67604087`

#### JSON input format:
```json
{
    "latest_user_message": "你好，想找一個有經驗的老師專補小三"
}
```

# Full Example (python)
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
