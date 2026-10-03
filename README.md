# jwt-jku-test

## JWT JKU Injection Lab - ATTACKER CONTROLLED EXPLOIT SERVER PUBLIC RSA KEY

This repository is created for security testing of **JWT authentication vulnerabilities**, specifically **JKU header injection**.

## Purpose

The repository hosts a `jwks.json` file containing a test RSA **public JWK**. It can be used to understand how a vulnerable JWT implementation may retrieve an attacker-controlled public key through the `jku` header.

### Attack Flow

```text
Generate RSA Key Pair
        ↓
Private Key → Sign Modified JWT
        ↓
Public Key → Host in jwks.json
        ↓
Inject jku URL into JWT Header
        ↓
Target fetches JWKS
        ↓
Target uses supplied Public Key
        ↓
JWT Signature Verification
```

## Repository Structure

```text
jwt-jku-test/
└── jwks.json
```

`jwks.json` contains only the **public RSA key** required for signature verification.

The corresponding **private key must never be stored in this repository**.

## Example JWT Header

```json
{
  "alg": "RS256",
  "typ": "JWT",
  "kid": "test-key",
  "jku": "https://<username>.github.io/jwt-jku-test/jwks.json"
}
```
