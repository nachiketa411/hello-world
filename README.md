# -hello-world

## Testing events

Lets see if my api picks this event up.

### Test 2

- Previous test resulted in private key loading error.
- I think it was due to the key being in the wrong format.
- Converting the current private key to PKCS8 format.
- Hopefully it works.

### Test 3

- The Auth Service was generating the wrong url to trigger.
- My error. I forgot to add the preceding `/`

### Test 4

- Added a log in the response body to see the full error message from Github.

### Test 5

- The error message: `java.lang.RuntimeException: Failed to fetch installation token: 401 - {"message":"'Expiration time' claim ('exp') is too far in the future","documentation_url":"https://docs.github.com/rest","status":"401"}`

- GitHub's maximum is 10 minutes
- Changing the time from 540 -> 480
