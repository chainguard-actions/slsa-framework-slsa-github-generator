# setup-token

The token has the following format:

```text
token := B64_BUNDLE.B64_TOKEN
```

where

```text
B64_TOKEN := base64(JSON_RAW_TOKEN)
B64_BUNDLE := base64(Sign(B64_TOKEN))
```

## Privacy

This Action contacts Chainguard's licensing server to verify authorization. Connection metadata (IP address, GitHub repository identifier, timestamp, and any metadata encoded in the auth token) is transmitted to Chainguard, Inc. even if authorization is denied in accordance with our [Privacy Notice](https://www.chainguard.dev/legal/privacy-notice)
