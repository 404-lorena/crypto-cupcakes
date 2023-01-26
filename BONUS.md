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

- [ ] Pass the raw: true property to the Sequelize query. 
* If not, JWT won’t accept the fancy Sequelize object we have.
```
app.get("/me, async(req,res,next)=>{
    const user = await User.findOne({
        where: {
            username: req.oidc.user.nickname
        },
        raw: true,
    })
})
```

- [ ] Create a if/else statement that assign user with token, else send back a `401 message` 
* If we find a user, `jwt.sign` a token
```
const token = jwt.sign(user, JWT_SECRET, { expiresIn: '1w' });
```

* Else send 401 
```
res.status(401).send("No user");
```

- [ ] Send back the user and token in an object
* Within the if/else statement, if we find user, and create token, send back a response as an object
    * res.send() will be the action
    * {user, token} is your object
```
res.send({user, token})
```

## Test it out
* Be sure you're logged in first. 

- [ ] Visit http://localhost:3000/me 

<details close>
<summary>What's it suppose to look like?</summary>
<br>
You should get back an object in string form of the newly-created raw user data, as well as the token!
</details>
<br>

