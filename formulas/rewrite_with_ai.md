Here’s a **rewritten and improved version** of your `n8n` workflow with **emojis**, **better prompt structuring**, and **more expressive Telegram messages** to make it feel more engaging and user-friendly:

---

### ✅ **Improvements Made**:

* ✍️ Enhanced LLM prompt: More creative and specific instruction to generate **original jokes**.
* 💬 Telegram message now includes emojis and markdown for better readability and engagement.
* 🧠 Naming of nodes is more descriptive for easier debugging and collaboration.

---

### 🔄 **Updated JSON**:

```json
{
  "name": "🎭 LLM Joke Bot",
  "nodes": [
    {
      "parameters": {},
      "type": "n8n-nodes-base.manualTrigger",
      "typeVersion": 1,
      "position": [-200, 20],
      "id": "298514ab-6f36-4212-bbce-939831f3e0ce",
      "name": "▶️ Manual Trigger"
    },
    {
      "parameters": {
        "chatId": "-1002793496878",
        "text": "=🤣 *Here's your joke of the day:* \n\n{{ $json.text }}",
        "additionalFields": {
          "parse_mode": "Markdown"
        }
      },
      "type": "n8n-nodes-base.telegram",
      "typeVersion": 1.2,
      "position": [1060, -100],
      "id": "f97fce7e-b8c9-4fd4-a6a5-75d6293a1669",
      "name": "📤 Send Joke to Telegram",
      "webhookId": "061c728a-457c-425b-8b62-fb56abb3b1ad",
      "credentials": {
        "telegramApi": {
          "id": "FNhCBbEpIegop14Z",
          "name": "Telegram account"
        }
      }
    },
    {
      "parameters": {
        "public": true,
        "initialMessages": "Tell me a joke 🤖",
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.chatTrigger",
      "typeVersion": 1.1,
      "position": [140, -180],
      "id": "6cde4795-8640-46ea-8a5e-ac3b87e03f94",
      "name": "💬 When User Requests a Joke",
      "webhookId": "48636601-86bb-4b01-97e2-ff4359dc1b64"
    },
    {
      "parameters": {
        "promptType": "define",
        "text": "Tell me a short, original joke that's witty, unexpected, and clean. Avoid clichés. Keep it under 25 words.",
        "messages": {
          "messageValues": [
            {
              "type": "HumanMessagePromptTemplate",
              "message": "🎯 *Goal:* Surprise me with a clever joke that even a chatbot would laugh at!"
            }
          ]
        },
        "batching": {}
      },
      "type": "@n8n/n8n-nodes-langchain.chainLlm",
      "typeVersion": 1.7,
      "position": [400, 20],
      "id": "b5f5cc34-5914-4ed4-8fc0-f39cf9faa61b",
      "name": "🧠 Generate Joke with LLM"
    },
    {
      "parameters": {
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.lmChatOpenRouter",
      "typeVersion": 1,
      "position": [240, 240],
      "id": "d409322b-8f49-4e54-b763-3001e233e28c",
      "name": "🔌 OpenRouter LLM",
      "credentials": {
        "openRouterApi": {
          "id": "e95QbimUJvBb4tqj",
          "name": "OpenRouter account"
        }
      }
    }
  ],
  "connections": {
    "▶️ Manual Trigger": {
      "main": [
        [
          {
            "node": "🧠 Generate Joke with LLM",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "🔌 OpenRouter LLM": {
      "ai_languageModel": [
        [
          {
            "node": "🧠 Generate Joke with LLM",
            "type": "ai_languageModel",
            "index": 0
          }
        ]
      ]
    },
    "💬 When User Requests a Joke": {
      "main": [
        [
          {
            "node": "🧠 Generate Joke with LLM",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "🧠 Generate Joke with LLM": {
      "main": [
        [
          {
            "node": "📤 Send Joke to Telegram",
            "type": "main",
            "index": 0
          }
        ]
      ]
    }
  },
  "active": false,
  "settings": {
    "executionOrder": "v1"
  },
  "versionId": "25da0542-a878-4f1f-8c17-ecc76d72c79e",
  "meta": {
    "templateCredsSetupCompleted": true,
    "instanceId": "3df7c7c6cb7e0e978bf80ded11fce953795594ae8fe07b63ac449418b447c9e7"
  },
  "id": "TV6UKyOA6nSto0QH",
  "tags": []
}
```

---

### 🛠 What to Do Next

* ✅ Save and activate the workflow.
* 🧪 Test it by sending “Tell me a joke 🤖” in your Telegram channel.
* 📈 Add logic to handle errors, retries, or fallback jokes if needed.

Want to also log the jokes to Notion or Google Sheets for reuse or analysis? I can help you with that too.
