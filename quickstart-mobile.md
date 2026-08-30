# Swift and mobile apps

A compiled mobile app cannot safely contain a private Stockero key. App Store encryption, obfuscation, or the iOS Keychain do not solve the initial distribution problem: a determined user can extract a bundled credential.

## Correct design

1. The iOS or Android app authenticates to **your backend**.
2. It sends a constrained request such as `{ "zip": "10001" }`.
3. Your backend validates the user and input.
4. Your backend calls Stockero using its server-side key.
5. Your backend returns the permitted data to the mobile app.

Swift should therefore call your service:

```swift
let url = URL(string: "https://api.yourapp.com/stores?zip=10001")!
var request = URLRequest(url: url)
request.setValue("Bearer \(yourUserSession)", forHTTPHeaderField: "Authorization")
let (data, response) = try await URLSession.shared.data(for: request)
```

`yourUserSession` authenticates the user to your own service. It is not a Stockero key. The Stockero key exists only in your backend environment.

Use platform secure storage for your app's own short-lived user session, validate authorization on every backend request, and rate-limit users independently of Stockero's upstream limits.
