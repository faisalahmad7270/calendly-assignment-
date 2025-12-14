1. Update Calendly Access Token
1.1 Generate New Token

Login to Calendly

Navigate to
Account → Integrations → API & Webhooks

Click Create New Token

Copy the generated Personal Access Token

1.2 Update Token in Database

Execute the following SQL query:

UPDATE API_CONFIG
SET auth_token = '<NEW_CALENDLY_ACCESS_TOKEN>'
WHERE system_name = 'CALENDLY';


-> No code change required
-> No application redeployment required



2. Execute External API Call
2.1 Trigger Application API

Use Postman or browser to call:

POST http://localhost:8080/users/fetch/calendly

2.2 Expected API Response
Users fetched from calendly


-> Indicates successful external API invocation
-> Generic API service executed

3. Verify External API Execution (Logs)

Check application logs for:

HTTP 200 response from Calendly

No authentication or resource errors

External API URL loaded from DB

Example log:

Calling external API: https://api.calendly.com/users/me

4. Verify User Data in Temporary Table
4.1 Execute Verification Query
SELECT * FROM TEMP_USERS
WHERE source_system = 'CALENDLY'
ORDER BY fetched_at DESC;

4.2 Expected Result
id	name	email	source_system	fetched_at
10	John Doe	john@gmail.com
	CALENDLY	2025-xx-xx
