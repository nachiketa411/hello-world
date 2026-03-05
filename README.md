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
