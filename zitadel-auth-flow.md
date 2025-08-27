# Complete Code Flow Diagram - Easy to Understand

## 🚀 What This App Does:
This is a **"User Management System"** where people can:
- Login with their ZITADEL account
- Get different roles (like being a customer, seller, or service provider)
- Access different types of information based on their role

---

## 🌐 STEP 1: User Opens the App

```
┌─────────────────────────────────────────────────────────────────┐
│                    User Opens Browser                          │
│                    Goes to: http://localhost:3000             │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    App.jsx Loads                               │
│                    (Main Page)                                 │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Check: Is User Logged In?                   │
│                                                                 │
│  ┌─────────────────┐    ┌─────────────────┐                   │
│  │   NO TOKEN      │    │   HAS TOKEN     │                   │
│  │   FOUND        │    │   FOUND         │                   │
│  └─────────────────┘    └─────────────────┘                   │
│           │                       │                           │
│           ▼                       ▼                           │
│  ┌─────────────────┐    ┌─────────────────┐                   │
│  │ Show:           │    │ Show:           │                   │
│  │ "Login Button"  │    │ "Go to         │                   │
│  │                 │    │  Protected"     │                   │
│  └─────────────────┘    └─────────────────┘                   │
└─────────────────────────────────────────────────────────────────┘
```

**🔍 What Happens in Code:**
- `App.jsx` runs `getTokenForAPI()` to check for saved login information
- If no token: shows login button
- If has token: shows link to protected area

---

## 🔐 STEP 2: User Clicks Login Button

```
┌─────────────────────────────────────────────────────────────────┐
│                    User Clicks "Login" Button                  │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    auth.js - startLogin() Function             │
│                                                                 │
│  1. Generate Secret Code (PKCE)                                │
│     - Create random secret: "abc123xyz"                        │
│     - Create challenge: "def456uvw"                            │
│                                                                 │
│  2. Save Secret in Browser Memory                              │
│     - Store: "abc123xyz"                                       │
│                                                                 │
│  3. Create Login URL                                           │
│     - Add: User ID, Challenge, Website Address                 │
│     - URL: https://zitadel.com/login?challenge=def456uvw       │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Browser Redirects to ZITADEL                │
│                    (Like going to a different website)         │
└─────────────────────────────────────────────────────────────────┘
```

**🔍 What Happens in Code:**
- `generatePKCE()` creates two secret codes
- `sessionStorage.setItem()` saves the secret code
- `window.location.href` sends user to ZITADEL login page

---

## 👤 STEP 3: User Logs into ZITADEL

```
┌─────────────────────────────────────────────────────────────────┐
│                    User is on ZITADEL Website                  │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                    ZITADEL Login Page                   │   │
│  │                                                         │   │
│  │  Email: [user@example.com]                             │   │
│  │  Password: [••••••••]                                  │   │
│  │                                                         │   │
│  │  [Login Button]                                         │   │
│  └─────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    User Types Email & Password                 │
│                    Clicks Login                               │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    ZITADEL Checks Credentials                  │
│                    (Like a bouncer checking ID)                │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    If Login Successful:                        │
│                    ZITADEL Creates Special Code                │
│                    (Like a temporary pass)                     │
└─────────────────────────────────────────────────────────────────┘
```

**🔍 What Happens:**
- User enters their ZITADEL account details
- ZITADEL verifies the information
- ZITADEL creates a temporary "authorization code"

---

## 🔄 STEP 4: ZITADEL Sends User Back with Code

```
┌─────────────────────────────────────────────────────────────────┐
│                    ZITADEL Redirects User Back                 │
│                    To: http://localhost:3000/callback          │
│                    With Code: ?code=ABC123XYZ                  │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Callback.jsx Loads                          │
│                    (Receives the Code)                         │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Frontend Gets the Code                      │
│                    Code: "ABC123XYZ"                           │
│                    (Like receiving a ticket)                   │
└─────────────────────────────────────────────────────────────────┘
```

**🔍 What Happens in Code:**
- `Callback.jsx` reads the code from the URL
- Code looks like: `?code=ABC123XYZ`
- This code is temporary and can only be used once

---

## 💱 STEP 5: Frontend Exchanges Code for Real Tokens

```
┌─────────────────────────────────────────────────────────────────┐
│                    Frontend Sends to Backend:                  │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                    Request to Backend                    │   │
│  │                                                         │   │
│  │  Code: "ABC123XYZ"                                      │   │
│  │  Secret: "abc123xyz" (from Step 2)                      │   │
│  │  Website: "http://localhost:3000"                       │   │
│  └─────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Backend (server.js) Receives Request        │
│                    /exchange-token endpoint                    │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Backend Sends to ZITADEL:                   │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                    Request to ZITADEL                    │   │
│  │                                                         │   │
│  │  "Hi ZITADEL, I have code ABC123XYZ                     │   │
│  │   and secret abc123xyz. Can I have                      │   │
│  │   the real access tokens?"                               │   │
│  └─────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    ZITADEL Checks and Responds                 │
│                    "Yes, here are your tokens:"                │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                    ZITADEL Response                     │   │
│  │                                                         │   │
│  │  access_token: "w0Ajn6bill3iqHIdssXfz6Uu19D430pw..."   │
│  │  id_token: "eyJhbGciOiJSUzI1NiIsImtpZCI6IjMzNTI1..."   │
│  │  expires_in: 43199 (12 hours)                           │   │
│  └─────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
```

**🔍 What Happens in Code:**
- `exchangeCodeForTokens()` sends POST to backend
- Backend `app.post("/exchange-token")` receives request
- Backend sends request to ZITADEL with code + verifier
- ZITADEL returns real access tokens

---

## 💾 STEP 6: Frontend Saves the Tokens

```
┌─────────────────────────────────────────────────────────────────┐
│                    Backend Sends Tokens to Frontend            │
│                    (Like passing a package)                    │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Frontend Receives Tokens                    │
│                    (auth.js - exchangeCodeForTokens)           │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Frontend Saves Tokens in Browser            │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                    Browser Memory (sessionStorage)      │   │
│  │                                                         │   │
│  │  access_token: "w0Ajn6bill3iqHIdssXfz6Uu19D430pw..."   │
│  │  id_token: "eyJhbGciOiJSUzI1NiIsImtpZCI6IjMzNTI1..."   │
│  │  (Like putting keys in a safe)                          │   │
│  └─────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    User is Now Logged In!                      │
│                    Can Access Protected Areas                  │
└─────────────────────────────────────────────────────────────────┘
```

**🔍 What Happens in Code:**
- `sessionStorage.setItem("access_token", json.access_token)`
- `sessionStorage.setItem("id_token", json.id_token)`
- Tokens are stored in browser memory for later use

---

## 🛡️ STEP 7: User Visits Protected Page

```
┌─────────────────────────────────────────────────────────────────┐
│                    User Clicks "Go to Protected"               │
│                    Goes to: http://localhost:3000/protected    │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Protected.jsx Loads                         │
│                    (Protected Component)                       │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Component Gets Token                        │
│                    getTokenForAPI() Function                   │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                    Token Selection Logic                 │   │
│  │                                                         │   │
│  │  Check: Do we have id_token?                            │   │
│  │  If YES: Use id_token (JWT format)                      │   │
│  │  If NO: Use access_token (opaque format)                 │   │
│  └─────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Frontend Sends Request to Backend           │
│                    GET /api/me with Token                     │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                    Request Headers                       │   │
│  │                                                         │   │
│  │  Authorization: Bearer eyJhbGciOiJSUzI1NiIsImtpZCI6... │   │
│  │  (Like showing your ID card)                            │   │
│  └─────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
```

**🔍 What Happens in Code:**
- `Protected.jsx` uses `useEffect` to run when page loads
- `getTokenForAPI()` gets the best available token
- `axios.get()` sends request with Authorization header

---

## 🔍 STEP 8: Backend Verifies the Token

```
┌─────────────────────────────────────────────────────────────────┐
│                    Backend Receives Request                    │
│                    /api/me endpoint                           │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    verifyAccessToken Middleware Runs            │
│                    (Like a security guard)                     │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Token Analysis                              │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                    Token Check                          │   │
│  │                                                         │   │
│  │  Question: Does token contain dots (.)?                │   │
│  │                                                         │   │
│  │  ┌─────────────────┐    ┌─────────────────┐             │   │
│  │  │   YES (JWT)     │    │   NO (Opaque)   │             │   │
│  │  │   Contains .    │    │   No dots       │             │   │
│  │  └─────────────────┘    └─────────────────┘             │   │
│  │           │                       │                     │   │
│  │           ▼                       ▼                     │   │
│  │  ┌─────────────────┐    ┌─────────────────┐             │   │
│  │  │   JWT Verify    │    │   Introspection │             │   │
│  │  │   (Local)       │    │   (Ask ZITADEL) │             │   │
│  │  └─────────────────┘    └─────────────────┘             │   │
│  └─────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
```

**🔍 What Happens in Code:**
- `if (token.includes('.'))` checks if token is JWT format
- JWT tokens use `jwtVerify()` with JWKS (public keys)
- Opaque tokens use `introspectToken()` (ask ZITADEL)

---

## 🔐 STEP 9: JWT Token Verification (Most Common)

```
┌─────────────────────────────────────────────────────────────────┐
│                    JWT Token Verification                      │
│                    (Like checking a passport)                  │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Backend Gets Public Keys from ZITADEL       │
│                    (JWKS - JSON Web Key Set)                   │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Backend Checks Token:                       │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                    Verification Steps                    │   │
│  │                                                         │   │
│  │  1. Is signature valid? (Using public key)              │   │
│  │  2. Is token expired? (Check time)                      │   │
│  │  3. Is issuer correct? (From ZITADEL?)                  │   │
│  │  4. Is audience correct? (For our app?)                 │   │
│  └─────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    If All Checks Pass:                         │
│                    Extract User Information                    │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                    User Claims (Payload)                │   │
│  │                                                         │   │
│  │  sub: "335192599776231860" (User ID)                    │   │
│  │  email: "user@example.com"                              │   │
│  │  iss: "https://balaji-xd4tvj.us1.zitadel.cloud"        │   │
│  │  exp: 1756371123 (Expiration time)                      │   │
│  └─────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
```

**🔍 What Happens in Code:**
- `jwtVerify(token, JWKS, verifyOptions)` validates the token
- JWKS automatically fetches public keys from ZITADEL
- Backend extracts user information from verified token

---

## 👤 STEP 10: Backend Returns User Data

```
┌─────────────────────────────────────────────────────────────────┐
│                    Backend Has Verified User                   │
│                    (Security check passed)                     │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Backend Checks User's Personas              │
│                    (What roles does this user have?)           │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    personaStore Lookup                         │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                    Memory Storage                       │   │
│  │                                                         │   │
│  │  User ID: "335192599776231860"                          │   │
│  │  Personas: ["consumer", "vendor"]                       │   │
│  │  (Like checking what permissions someone has)            │   │
│  └─────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Backend Sends Response                      │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                    Response Data                         │   │
│  │                                                         │   │
│  │  {                                                      │   │
│  │    claims: {                                            │   │
│  │      sub: "335192599776231860",                         │   │
│  │      email: "user@example.com"                          │   │
│  │    },                                                   │   │
│  │    personas: ["consumer", "vendor"]                     │   │
│  │  }                                                      │   │
│  └─────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
```

**🔍 What Happens in Code:**
- `personaStore.get(sub)` looks up user's roles
- `res.json({ claims: req.user, personas })` sends response
- Frontend receives user information and roles

---

## 📱 STEP 11: Frontend Displays User Information

```
┌─────────────────────────────────────────────────────────────────┐
│                    Frontend Receives Response                  │
│                    (Protected.jsx)                            │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Frontend Updates State                      │
│                    (React State Management)                    │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Frontend Shows User Interface               │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                    User Information Display              │   │
│  │                                                         │   │
│  │  User claims (sub): 335192599776231860                  │   │
│  │  Email: user@example.com                                │   │
│  │                                                         │   │
│  │  Personas on your account: consumer, vendor             │   │
│  │                                                         │   │
│  │  Add persona: [consumer] [vendor] [affiliate] [service] │   │
│  │                                                         │   │
│  │  Fetch persona data: [Get consumer] [Get vendor]        │   │
│  └─────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
```

**🔍 What Happens in Code:**
- `setMe(resp.data.claims)` stores user information
- `setPersonas(resp.data.personas)` stores user roles
- React automatically re-renders the page with new data

---

## ➕ STEP 12: User Adds New Persona

```
┌─────────────────────────────────────────────────────────────────┐
│                    User Clicks "Add affiliate" Button          │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Frontend Sends Request                      │
│                    POST /api/persona                           │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                    Request Data                          │   │
│  │                                                         │   │
│  │  Headers: Authorization: Bearer [token]                 │   │
│  │  Body: { persona: "affiliate" }                         │   │
│  │  (Like asking for a new permission)                     │   │
│  └─────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Backend Receives Request                    │
│                    /api/persona endpoint                      │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Backend Verifies Token Again                │
│                    (Same security check)                      │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Backend Adds Persona to User               │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                    personaStore Update                   │   │
│  │                                                         │   │
│  │  Before: User "335192599776231860" has ["consumer",     │   │
│  │          "vendor"]                                       │   │
│  │                                                         │   │
│  │  After:  User "335192599776231860" has ["consumer",     │   │
│  │          "vendor", "affiliate"]                          │   │
│  └─────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Backend Sends Success Response              │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                    Response                              │   │
│  │                                                         │   │
│  │  {                                                      │   │
│  │    ok: true,                                            │   │
│  │    personas: ["consumer", "vendor", "affiliate"]        │   │
│  │  }                                                      │   │
│  └─────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
```

**🔍 What Happens in Code:**
- `addPersona("affiliate")` sends POST request
- Backend `personaStore.get(sub).add(persona)` adds new role
- Frontend updates persona list automatically

---

## 📊 STEP 13: User Accesses Persona Data

```
┌─────────────────────────────────────────────────────────────────┐
│                    User Clicks "Get affiliate data" Button     │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Frontend Sends Request                      │
│                    GET /api/data/affiliate                     │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                    Request                              │   │
│  │                                                         │   │
│  │  URL: /api/data/affiliate                               │   │
│  │  Headers: Authorization: Bearer [token]                 │   │
│  │  (Like asking for specific information)                  │   │
│  └─────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Backend Receives Request                    │
│                    /api/data/:persona endpoint                │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Backend Checks Permission                  │
│                    (Does user have this persona?)             │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Permission Check                            │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                    Access Control                        │   │
│  │                                                         │   │
│  │  User has: ["consumer", "vendor", "affiliate"]          │   │
│  │  Requesting: "affiliate" data                           │   │
│  │  Question: Is "affiliate" in the list?                  │   │
│  │  Answer: YES ✅                                         │   │
│  │  Result: Access granted                                 │   │
│  └─────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Backend Returns Data                        │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                    Response                              │   │
│  │                                                         │   │
│  │  {                                                      │   │
│  │    persona: "affiliate",                                │   │
│  │    records: [                                           │   │
│  │      { id: "a1", info: "Affiliate stats 1" }            │   │
│  │    ]                                                    │   │
│  │  }                                                      │   │
│  └─────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
```

**🔍 What Happens in Code:**
- `fetchPersonaData("affiliate")` sends GET request
- Backend checks `set.has(persona)` for permission
- If allowed: returns `dataStore[persona]` data
- If denied: returns 403 error

---

## 🚫 STEP 14: Access Denied Example

```
┌─────────────────────────────────────────────────────────────────┐
│                    User Tries to Access "service_provider"     │
│                    (But doesn't have this persona)            │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Backend Checks Permission                  │
│                    (Same process as before)                   │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Permission Check - FAILED                   │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                    Access Control                        │   │
│  │                                                         │   │
│  │  User has: ["consumer", "vendor", "affiliate"]          │   │
│  │  Requesting: "service_provider" data                    │   │
│  │  Question: Is "service_provider" in the list?           │   │
│  │  Answer: NO ❌                                          │   │
│  │  Result: Access denied                                  │   │
│  └─────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Backend Returns Error                       │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                    Error Response                        │   │
│  │                                                         │   │
│  │  Status: 403 Forbidden                                   │   │
│  │  Body: {                                                 │   │
│  │    error: "forbidden_persona",                           │   │
│  │    message: "Your account does not have persona          │   │
│  │              'service_provider'. Use POST /api/persona   │   │
│  │              to add it."                                 │   │
│  │  }                                                       │   │
│  └─────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Frontend Shows Error Message                │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                    Error Display                         │   │
│  │                                                         │   │
│  │  Error / Forbidden:                                      │   │
│  │  Your account does not have persona 'service_provider'.  │   │
│  │  Use POST /api/persona to add it.                       │   │
│  │                                                         │   │
│  │  [Login/Signup as different account] [Add persona]      │   │
│  └─────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
```

**🔍 What Happens in Code:**
- Backend `if (!set.has(persona))` returns 403 error
- Frontend `err.response?.status === 403` catches the error
- Error message shows helpful instructions to user

---

## 🔄 STEP 15: Complete Cycle Summary

```
┌─────────────────────────────────────────────────────────────────┐
│                    Complete User Journey                        │
│                                                                 │
│  1. User opens app → sees login button                        │
│  2. Clicks login → redirected to ZITADEL                      │
│  3. Logs into ZITADEL → gets authorization code               │
│  4. Returns to app → code exchanged for tokens                │
│  5. Tokens saved → user is logged in                          │
│  6. Visits protected page → token verified                    │
│  7. User data loaded → personas displayed                     │
│  8. Adds new persona → role updated                           │
│  9. Accesses persona data → permission checked                │
│  10. Data displayed → user sees information                   │
└─────────────────────────────────────────────────────────────────┘
```

## 🔑 Key Points for Non-Technical People:

1. **Security**: Like having a passport that gets checked at every door
2. **Roles**: Like having different keys for different rooms
3. **Tokens**: Like temporary passes that expire after a certain time
4. **Verification**: Like a security guard checking your ID before letting you in
5. **Permissions**: Like only being able to access areas you're authorized for

This system ensures that:
- Only logged-in users can access protected areas
- Users can only see data they're allowed to see
- Security is maintained at every step
- Everything is logged and traceable