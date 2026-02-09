# Autosend REST API Reference

## Authentication

All requests require a Bearer token in the Authorization header:

```
Authorization: Bearer YOUR_API_KEY
```

All POST/PUT requests require:

```
Content-Type: application/json
```

## Base URL

```
https://api.autosend.com/v1
```

---

## Endpoints

### Send Email

Send a single transactional email.

**curl**
```bash
curl -X POST https://api.autosend.com/v1/mails/send \
  -H "Authorization: Bearer $AUTOSEND_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "to": "user@example.com",
    "subject": "Welcome!",
    "html": "<h1>Hello</h1><p>Welcome to our service.</p>",
    "from": "hello@yourdomain.com"
  }'
```

**Python**
```python
import requests

response = requests.post(
    "https://api.autosend.com/v1/mails/send",
    headers={
        "Authorization": f"Bearer {api_key}",
        "Content-Type": "application/json"
    },
    json={
        "to": "user@example.com",
        "subject": "Welcome!",
        "html": "<h1>Hello</h1><p>Welcome to our service.</p>",
        "from": "hello@yourdomain.com"
    }
)
```

**Go**
```go
payload := []byte(`{
    "to": "user@example.com",
    "subject": "Welcome!",
    "html": "<h1>Hello</h1><p>Welcome to our service.</p>",
    "from": "hello@yourdomain.com"
}`)

req, _ := http.NewRequest("POST", "https://api.autosend.com/v1/mails/send", bytes.NewBuffer(payload))
req.Header.Set("Authorization", "Bearer "+apiKey)
req.Header.Set("Content-Type", "application/json")

client := &http.Client{}
resp, err := client.Do(req)
```

**Ruby**
```ruby
require 'net/http'
require 'json'

uri = URI("https://api.autosend.com/v1/mails/send")
http = Net::HTTP.new(uri.host, uri.port)
http.use_ssl = true

request = Net::HTTP::Post.new(uri)
request["Authorization"] = "Bearer #{api_key}"
request["Content-Type"] = "application/json"
request.body = {
  to: "user@example.com",
  subject: "Welcome!",
  html: "<h1>Hello</h1><p>Welcome to our service.</p>",
  from: "hello@yourdomain.com"
}.to_json

response = http.request(request)
```

**Rust**
```rust
let client = reqwest::Client::new();
let response = client
    .post("https://api.autosend.com/v1/mails/send")
    .header("Authorization", format!("Bearer {}", api_key))
    .json(&serde_json::json!({
        "to": "user@example.com",
        "subject": "Welcome!",
        "html": "<h1>Hello</h1><p>Welcome to our service.</p>",
        "from": "hello@yourdomain.com"
    }))
    .send()
    .await?;
```

---

### Bulk Send

Send emails to multiple recipients with shared sender and template support.

**curl**
```bash
curl -X POST https://api.autosend.com/v1/mails/bulk \
  -H "Authorization: Bearer $AUTOSEND_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "from": { "email": "hello@yourdomain.com", "name": "Your Company" },
    "subject": "Welcome!",
    "templateId": "tmpl_welcome",
    "dynamicData": { "companyName": "Acme Inc" },
    "recipients": [
      {
        "email": "user1@example.com",
        "name": "User One",
        "dynamicData": { "firstName": "User" }
      },
      {
        "email": "user2@example.com",
        "name": "User Two",
        "dynamicData": { "firstName": "User" }
      }
    ]
  }'
```

---

### Create Contact

Add a new contact to your list.

**curl**
```bash
curl -X POST https://api.autosend.com/v1/contacts \
  -H "Authorization: Bearer $AUTOSEND_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "email": "contact@example.com",
    "firstName": "Jane",
    "lastName": "Doe",
    "listIds": ["list_abc123"],
    "customFields": {
      "company": "Acme Inc",
      "plan": "enterprise"
    }
  }'
```

---

### Get Contact

Retrieve a contact by ID.

**curl**
```bash
curl -X GET https://api.autosend.com/v1/contacts/contact_abc123 \
  -H "Authorization: Bearer $AUTOSEND_API_KEY"
```

---

## Error Responses

Errors return JSON with an `error` object:

```json
{
  "success": false,
  "error": {
    "message": "The 'to' field is required",
    "code": "VALIDATION_FAILED",
    "details": []
  }
}
```

Common HTTP status codes:
- `400` - Bad request (validation error)
- `401` - Unauthorized (invalid API key)
- `402` - Payment required (plan upgrade needed)
- `403` - Forbidden (insufficient permissions)
- `404` - Resource not found
- `429` - Rate limit exceeded
- `500` - Server error

---

## Additional Operations

The following operations use the same patterns shown above:

| Operation | Method | Endpoint |
|-----------|--------|----------|
| Upsert contact | POST | `/v1/contacts/email` |
| Delete contact | DELETE | `/v1/contacts/:id` |

Adapt the curl examples to your language using the patterns from Send Email.
