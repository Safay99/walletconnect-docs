# Dapp Authentication

Push API requires Dapp developers to host a did:web document to expose public keys for two specific purposes:

    * key agreement - public key used to subscribe to the chosen cast server
    * authentication - public key used to sign message published by the chosen cast server

This should be available under the `.well-known` path for the Dapp Domain or alternatively it can be made available through a specific path for this did:web document.

Here is an example for the two public keys being exposed:

```jsonc
did:web:example.com -> https://example.com/.well-known/did.json
# OR
did:web:example.com:wc:push -> https://example.com/wc/push/did.json

// did.json
{
  "@context": [
    "https://www.w3.org/ns/did/v1",
    "https://w3id.org/security/suites/jws-2020/v1"
  ],
  "id": "did:web:example.com",
  "verificationMethod": [
    {
      "id": "did:web:example.com#key-0",
      "type": "JsonWebKey2020",
      "controller": "did:web:example.com",
      "publicKeyJwk": {
        "kty": "OKP",
        "crv": "X25519",
        "x": "9GXjPGGvmRq9F6Ng5dQQ_s31mfhxrcNZxRGONrmH30k"
      }
    },
    {
      "id": "did:web:example.com#key-1",
      "type": "JsonWebKey2020",
      "controller": "did:web:example.com",
      "publicKeyJwk": {
        "kty": "OKP",
        "crv": "Ed25519",
        "x": "0-e2i2_Ua1S5HbTYnVB0lj2Z2ytXu2-tYmDFf8f5NjU"
      }
    },

  ],
  "keyAgreement": [
    "did:web:example.com#key-0"
  ],
  "authentication": [
    "did:web:example.com#key-1"
  ],
}
```