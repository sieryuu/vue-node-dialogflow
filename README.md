# vue-node-dialogflow

> An example for consuming [Dialogflow][df] API using [Node.js][nodejs] with [Vue.js][vue] as frontend

*NB: The codes is just for reference how to consume Dialog Flow API, not for production use!*

## Getting Started
### Using your own Google Application Credentials (slow setup)
- Go to [DialogFlow][dfweb] to create your project.
- Complete [DialogFlow][df] API & [Text-to-Speech][tts] "Before you begin" section ([this][t1] & [this][t2]). (On the step 4, make sure you click the "GO TO THE CREATE SERVICE ACCOUNT KEY PAGE" button and choose the Project then download the JSON file.)
- Change you `projectId` in build/dev-server.js to your own `projectId`
### Or using my Google Application Credentials (fast setup)
- Create a JSON file <example.json> (anywhere)
- Copy and paste below text into the JSON file you have created.

``` bash
{
  "type": "service_account",
  "project_id": "newagent-be625",
  "private_key_id": "415e66be139c33533aacf97dd9ae782cd720d9dd",
  "private_key": "-----BEGIN PRIVATE KEY-----\nMIIEvAIBADANBgkqhkiG9w0BAQEFAASCBKYwggSiAgEAAoIBAQCiLBnwKE7BxO0H\n60TqzzW0CTTh+tPe6V5yuRZNTXyaePTih/2x/XnJBIEnnUPH01/hyGoFvO6IJ/92\nc5A7AvxmD6cKp6avFs/4pJ7Gi2WZKq4zq8ZWGQ5zHVW/+vOVRLtaA8+uOPKFKA2A\n3776n6+SnP3WhQFOQKSur+cVVphZYwkQRpDq6Tmxq6Z6dJ3n6cB+w33zAehen/Ge\niiZ7sTioJjf7kHrvAHSW7Ijqm6fuqvknhMAwcjYfO1JGmJG+bAUmVjjPEn4PFN76\nxxB4o3sxw1+Z31JDSCV3lgxoKkG/6UaEiQ9o5wxuKYroBsljRB5uIW7JfOS/eZuG\n59m9pOIPAgMBAAECggEAGNRLvFtPg5dU+ytoR9Ml08S9FgRDQBPW5BW2dmtwsm3m\ngHB1xTSb2s0XwSrw371bJsR6hxpgIvSMxmP3JzHT1wR6fMUiXhhOCzGZJajeC09f\nkIWyPihj7/gD0vrnJGl7jdKbj38kkoKJXrvjD5g3V2k17Aw9IPAAxsYjyT6S4Mxs\nfwO1hlZIbAOXrOa1UeT9SSbyNTwfNFBom/p2CAVG3zq8lmf4RsqQ4BNUSWpkzogL\n8EWbjTCRZ4RbBrUIRkSYLAkOWuovKomMqqaMk/ka3x/7AqANldXcbaV9y3eWyeYL\nEaNvPHZ2XZeFxtAdx8zhzyLmSl3AErqPVTUuOzeKoQKBgQDS1s+XYglXJX1/oSyx\nF2OpyfGFF9fS9X9504oaWBFGfiTbDysUQlNMNVl/bpaULh0d41xUyrlR1bhcszOj\nqH7gQ37wUBzidAcR92zBU8EhIXU52TSVxYMsXJer7JpP+huMDtFBjBDXElwoDCmT\nMu3B7hjuxR7zA8juLQc8Sh/SRwKBgQDE6K8+RCWRW1j4jhvvP5nBO7p3F1D0YqgF\nlfTSQ0dkZkcR4qLEv3vS2Ced890eI1HWXAzEhTPZuPWnLANXoFbPCx7dCOvcFbQQ\nxW01adQ/N8ctzKGL0Jl945S3GenLqz+lV825JgQ2lPRwA98isuW0axgg+TDtfFmf\n1cG1EP5N+QKBgGYCAFYh3JsJTHrfpBvaUSHozq2yJ32twYtTydGNIm6UwYgrApC+\ntkZ82VxKSRhQZ036nsV3f8oUOSrAmQ9pilk+zr++QvtdX75Vk4zF1P8OjQT8DfEY\nqqpf8hIAW3iubX2J/bxU5CDqhSPrHoJVdasKY43CWYMCJcj2iDWnN1YpAoGAGyMW\nQ7aQlt/H+zlakDZrsj3RDOiht4yBK4PnIbMz+5o84TIizIq3Pe+cRiB9sNGdTbWR\n7OOOqcrb0BY4v7LRQ+d8cWnxV3uGPWl4C4xyO+QsBxvUh7hP7xGWRUXE+tS3CMp5\nB7M9kWgl5+ogrl+JWLwJr0GohJJGp8iF0bZt1cECgYAqEfkO8wGrBuPd6cQ5AlSw\n2aaqHAAwArAzZzcN8LeyVRgYzFsYcJnLpkTWWkMthj5xacsxTKNZYCjma9Gyv6pR\nvCB0BkWHTAxnEf2CCLZXMj14Gewd4O66gDdb8ckD8fIsVr+qfsMtbPqVhrUYKKLa\nVz8zwyIl28LAb3uKzR77wg==\n-----END PRIVATE KEY-----\n",
  "client_email": "dialogflow-rwdkll@newagent-be625.iam.gserviceaccount.com",
  "client_id": "115719006074595180870",
  "auth_uri": "https://accounts.google.com/o/oauth2/auth",
  "token_uri": "https://accounts.google.com/o/oauth2/token",
  "auth_provider_x509_cert_url": "https://www.googleapis.com/oauth2/v1/certs",
  "client_x509_cert_url": "https://www.googleapis.com/robot/v1/metadata/x509/dialogflow-rwdkll%40newagent-be625.iam.gserviceaccount.com"
}

```

## Build Setup

``` bash
# install dependencies
npm install

# set env for GOOGLE_APPLICATION_CREDENTIALS
# [PATH] to the JSON file you have downloaded / created
## Windows (using command prompt)
set GOOGLE_APPLICATION_CREDENTIALS=[PATH]
## Mac OS/ Linux
export GOOGLE_APPLICATION_CREDENTIALS=[PATH]

# serve with hot reload at localhost:8080
npm run dev
```

[dfweb]: <https://dialogflow.com/>
[df]: <https://github.com/dialogflow/dialogflow-nodejs-client-v2>
[nodejs]: <https://nodejs.org>
[vue]: <https://vuejs.org/>
[tts]: <https://github.com/googleapis/nodejs-text-to-speech>
[t1]: <https://github.com/dialogflow/dialogflow-nodejs-client-v2#before-you-begin>
[t2]: <https://github.com/googleapis/nodejs-text-to-speech#before-you-begin>
