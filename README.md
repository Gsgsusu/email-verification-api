# Email Verification API

REST API to verify any email address for deliverability and get owner details like name and gender. Detects disposable emails, free providers, and invalid addresses in real time.

## Features

- Verify email deliverability with syntax, MX record, and SMTP checks
- Detect disposable/temporary email addresses (Guerrilla Mail, Mailinator, etc.)
- Identify free email providers (Gmail, Yahoo, Outlook)
- Get owner details — first name, last name, and gender
- 5,000 requests/month on free tier
- Example Response:
```json
{
  "is_valid": true,
  "status": "valid",
  "is_free_email": false,
  "first_name": null,
  "last_name": null,
  "gender": null
}
```

## Get API Key

Create an account at [omkar.cloud](https://www.omkar.cloud/auth/sign-up?redirect=/api-key) to get your API key, and use it in requests. 5000 requests are free every month.

## Quick Start

```bash
curl -X GET "https://email-verification-api.omkar.cloud/verify?email=happy.to.help%40omkar.cloud" \
  -H "API-Key: YOUR_API_KEY"
```

```json
{
  "is_valid": true,
  "status": "valid",
  "is_free_email": false,
  "first_name": null,
  "last_name": null,
  "gender": null
}
```

## Installation

### Python

```bash
pip install requests
```

```python
import requests

response = requests.get(
    "https://email-verification-api.omkar.cloud/verify",
    params={"email": "happy.to.help@omkar.cloud"},
    headers={"API-Key": "YOUR_API_KEY"}
)

result = response.json()
print(f"Valid: {result['is_valid']}, Status: {result['status']}")
```

### Node.js

```bash
npm install axios
```

```javascript
import axios from "axios";

const response = await axios.get("https://email-verification-api.omkar.cloud/verify", {
    params: { email: "happy.to.help@omkar.cloud" },
    headers: { "API-Key": "YOUR_API_KEY" }
});

console.log(`Valid: ${response.data.is_valid}, Status: ${response.data.status}`);
```

## API Reference

### Endpoint

```
GET https://email-verification-api.omkar.cloud/verify
```

### Headers

| Header | Required | Description |
|--------|----------|-------------|
| `API-Key` | Yes | API key from [omkar.cloud/api-key](https://www.omkar.cloud/api-key) |

### Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `email` | Yes | Email address to verify (e.g., `happy.to.help@omkar.cloud`) |

### Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `is_valid` | boolean | Whether the email address is deliverable |
| `status` | string | Verification status (`"valid"`, `"invalid"`) |
| `is_free_email` | boolean | Whether the email is from a free provider like Gmail, Yahoo, or Outlook |
| `first_name` | string \| null | Owner's first name (when available) |
| `last_name` | string \| null | Owner's last name (when available) |
| `gender` | string \| null | Owner's gender (when available) |

## Examples

### Verify a business email

```python
response = requests.get(
    "https://email-verification-api.omkar.cloud/verify",
    params={"email": "info@company.com"},
    headers={"API-Key": "YOUR_API_KEY"}
)

result = response.json()
if result["is_valid"]:
    print("Email is deliverable")
else:
    print("Email is invalid — skip sending")
```

### Block disposable emails on signup

```python
response = requests.get(
    "https://email-verification-api.omkar.cloud/verify",
    params={"email": user_email},
    headers={"API-Key": "YOUR_API_KEY"}
)

result = response.json()
if not result["is_valid"]:
    print("Blocked: disposable or invalid email")
```

### Enrich CRM contacts with owner details

```python
response = requests.get(
    "https://email-verification-api.omkar.cloud/verify",
    params={"email": "john@example.com"},
    headers={"API-Key": "YOUR_API_KEY"}
)

result = response.json()
if result["first_name"]:
    print(f"Contact: {result['first_name']} {result['last_name']}")
```

## Error Handling

```python
response = requests.get(
    "https://email-verification-api.omkar.cloud/verify",
    params={"email": "test@example.com"},
    headers={"API-Key": "YOUR_API_KEY"}
)

if response.status_code == 200:
    data = response.json()
elif response.status_code == 401:
    # Invalid API key
    pass
elif response.status_code == 429:
    # Rate limit exceeded
    pass
```

## Rate Limits

| Plan | Price | Requests/Month |
|------|-------|----------------|
| Free | $0 | 5,000 |
| Starter | $25 | 100,000 |
| Grow | $75 | 1,000,000 |
| Scale | $150 | 10,000,000 |

## Questions? We have answers.

Reach out anytime. We will solve your query within 1 working day.

[![Contact Us on WhatsApp about Email Verification API](https://raw.githubusercontent.com/omkarcloud/assets/master/images/whatsapp-us.png)](https://api.whatsapp.com/send?phone=918178804274&text=I%20have%20a%20question%20about%20the%20Email%20Verification%20API.)

[![Contact Us on Email about Email Verification API](https://raw.githubusercontent.com/omkarcloud/assets/master/images/ask-on-email.png)](mailto:happy.to.help@omkar.cloud?subject=Email%20Verification%20API%20Question)
