---
title: Netlifyfunctions
date: 2019-06-30T21:27:08.000Z
thumbnail: /images/uploads/scieworld.jpg
rating: 5
---

> Aside: So, my [BuildScript]("https://royu.netlify.com/posts/buildscript/") has already come in handy.  I forgot how to make a new post in `hugo`.  The line that came in handy was as follows:
> ```bash
> $ hugo new posts/name-of-my-new-post.md
> ```

This may or may not be a growing list.  I, as with many things, have not decided yet.

Some things I've learned from using netlify functions:

> You have to remember to disconnect from your data store otherwise your function hands for 10 seconds and then times out.

```javascript

const mongoose = require("mongoose");

exports.handler = async (evt, ctx) => {
    const {dbConnection} = process.env;
    await mongoose.connect(dbConnection, {useNewUrlParser: true});
    //Get or write what you need to the data store
    await mongoose.disconnect();
    return {
        statusCode: 200,
        body: JSON.stringify({
            data: "Done"
        })
    };
}

```

> In the `.toml` file, under the `[build]` category, the `functions = "directory_name_goes_here"` is actually where the compiled/transpiled/not_the_source_code goes and not where your netlify functions source files go.

```json
    "build:lambda": "netlify-lambda build src/lambda"
```

```toml
["build"]
    command = "npm run build:lambda"
    functions = "lambda"
    publish = "site"
```

> If you want the data from the HTTP Request Body you have to call `JSON.parse(evt.body)` before you have access to the payload.

```javascript

exports.handler = async(evt, cts) => {
    const {email} = JSON.parse(evt.body);
    console.log(email);
}

```
