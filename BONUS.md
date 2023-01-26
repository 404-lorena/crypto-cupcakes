# BONUS ROUND: GET /me Route
Let's create and send back a token


## JWT
- [ ] Install `jsonwebtoken` 
```
npm install jsonwebtoken
```

- [ ] Be sure to `require` it at the top of `index.js`
```
const jwt = require("jsonwebtoken");
```

- [ ] Destructure `JWT_SECRET` from `process.env`

- [ ] Create a secret and add it to your `.env` file
```
JWT='somethingHonestlyItCanBeAnySecretYouWant'
```


## GET /me Route
- [ ] Create /me route
```
app.get("/me, async(req,res,next)=>{
    // Logic to find user goes here
})
```

- [ ] Find the user
* Use `User.findOne` to search for a User whose `username` matches the `req.oidc.user.nickname` from Auth0.
```
app.get("/me, async(req,res,next)=>{
    const user = await User.findOne({
        where: {
            username: req.oidc.user.nickname
        }
    })
})

```





