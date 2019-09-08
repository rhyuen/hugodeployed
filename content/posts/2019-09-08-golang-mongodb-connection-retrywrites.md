---
layout: blog
title: Golang MongoDB Connection RetryWrites
date: 2019-09-08T23:31:36.191Z
thumbnail: /images/uploads/firstsprite.png
rating: 2
---
I tried using the new-ish MongoDB Golang Controller/Driver.

An issue I had with using it was that the MongoDB Deployment I was using didn't support retryable writes and the error message stated that it wanted me to add `retryWrites=false` to my connection string.  The thing is the tutorial/blog post I was following [here](https://www.mongodb.com/blog/post/mongodb-go-driver-tutorial) didn't mention anything regarding that.

The error message was as follows: 
```bash
$ 2019/09/08 23:21:04 this MongoDB deployment does not support retryable writes. Please add retryWrites=false to your connection string
```

What I ended up doing to make the issue go away was as follows: 

```go
url := os.Getenv("name_of_mongo_db_env_var")
clientOptions := options.Client().ApplyURI(url).SetRetryWrites(false)
client, err := mongo.Connect(context.TODO(), clientOptions)
```

The key are is the `.SetRetryWrites(false)` at the end of `line 2`.  The source of which was found [here](https://godoc.org/go.mongodb.org/mongo-driver/mongo/options#ClientOptions.SetRetryWrites) on the `godoc` website.  

This only got a blog post because I made this error twice...


