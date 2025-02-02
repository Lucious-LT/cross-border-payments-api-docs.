##### 📌 Overview  
The `/api/v1/payments` endpoint allows users to initiate a cross-border payment between a sender and recipient. The request includes payment details such as amount, currency, sender info, and recipient banking details.  

##### 📌 Request Details  
**Method:** `POST`  
**Endpoint:** `/api/v1/payments`  
**Headers:**  

| Header         | Description                     | Required | Example Value           |
|---------------|---------------------------------|----------|-------------------------|
| Authorization | Bearer token for authentication | ✅ Yes   | Bearer your_api_key     |
| Content-Type  | Data format type               | ✅ Yes   | application/json        |

###### 📌 Request Body (JSON Format)

Explain required parameters and their data types:

```json
{
  "amount": 100.00,
  "currency": "USD",
  "sender": {
    "name": "John Doe",
    "email": "john.doe@x.com"
  },
  "recipient": {
    "name": "Jane Smith",
    "accountNumber": "0987654321",
    "bankCode": "XYZ456",
    "country": "USA"
  },
  "reference": "INV-12345"
}


📌 4. Error Handling
Common error responses with explanations:
HTTP Status	Error Code	Message	Cause
400 Bad Request	INVALID_REQUEST	"Invalid bank code for the recipient."	Bank code does not match a valid entry.
400 Bad Request	MISSING_PARAMETERS	"Amount, currency, and recipient details are required."	Missing required fields in the request body.
401 Unauthorized	INVALID_API_KEY	"Authentication failed. Invalid API key."	API key is missing or incorrect.
500 Internal Server Error	SERVER_ERROR	"Unexpected server error. Please try again later."	Generic server-side error.

📌 5. Example Requests & Responses
Valid Request using cURL

curl -X POST https://api.example.com/api/v1/payments \
     -H "Authorization: Bearer your_api_key" 
     -H "Content-Type: application/json" 
     -d '{
           "amount": 100.00,
           "currency": "USD",
           "sender": {
             "name": "John Doe",
             "email": "john.doe@x.com"
           },
           "recipient": {
             "name": "Jane Smith",
             "accountNumber": "0987654321",
             "bankCode": "XYZ456",
             "country": "USA"
           },
           "reference": "INV-12345"
         }'

Example Response (Success)
json

{
  "transactionId": "TXN789456123",
  "status": "SUCCESS",
  "createdAt": "2025-01-12T10:15:30Z",
  "amount": 100.00,
  "currency": "USD",
  "recipient": {
    "name": "Jane Smith",
    "country": "USA"
  }
}

Example Response (Error - Invalid Bank Code)
json

{
  "error": "INVALID_REQUEST",
  "message": "Invalid bank code for the recipient."
}
