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

### Test 6

- Testing to see if i see the changed files list and the logs with additions and deletions if any in the given file.

### New Change

- The webhook endpoint is publicly accessible. Anyone who is able to find my NGROK url, can send fake requests to it.
- We need to verify the identify of the sender and the integrity of the payload.
- It needs to verify that Github is the sender.
- Github computes an HMAC-SHA256 signature of request body using our generated secret and puts it in the `X-Hub-Signature=256` header.
- If we receive a fake request, the sender cannot reproduce our generated secret, and thus the signatures wont match.

### Test 7

- On opening a new PR, the API should trigger a comment on the recently opened PR.

### Test 8

- I dont see inline comments, I see the PR comments.
- Debugging it right now.

### Test 9

- The DiffCalculator is returning `-1` due to which inline comments are being skipped.
- Printing the patch string itself, to see where the problem is.

### Test 10

- Updated the diff calculator logic.
- Currently, it should add a comment on `lineNumber` that we are passing through `getFirstAddedLineNumber()`, but with the integration of AI service, it is expected that the AI will return the exact line number to add the comments to and we will pass that.
- Github only accepts the relative position to add the comments to, not absolute line numbers.
- Example: If the AI service tells that the issue is line 50, then we need to parse to line 50 and find the position in respect to the file diff, which would be 10 lines for example. So if we pass line 50 to github, it will result in an error saying that line 50 does not exist in terms of the file diff.
