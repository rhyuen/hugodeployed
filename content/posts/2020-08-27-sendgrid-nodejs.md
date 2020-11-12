---
title: "sendgrid nodejs tutorial"
date: 2020-8-26T07:02:21-08:00
draft: false
---

I attempted the Sendgrid NodeJS 'Send an Email' tutorial [here](<https://app.sendgrid.com/guide/integrate/langs/nodejs>).

I'm pretty sure I've done this before but its been a while.  Unfortunately, I had problems with it.  I am assuming again.  Since the sample code they provided didn't work.  

```javascript
const sgMail = require('@sendgrid/mail');
sgMail.setApiKey(process.env.SENDGRID_API_KEY);
const msg = {
  to: 'test@example.com',
  from: 'test@example.com',
  subject: 'Sending with Twilio SendGrid is Fun',
  text: 'and easy to do anywhere, even with Node.js',
  html: '<strong>and easy to do anywhere, even with Node.js</strong>',
};
sgMail.send(msg);
```
Got this error:
![console error](/images/uploads/sendgrid-promise-rejection.png)

Then I had to revise the code so the 'catch' handler for the promise is caught.  I ended up using an 'IIFE' (Immediately invoked function expression).

```javascript
require("dotenv").config();
const mail = require("@sendgrid/mail");


const msg = {
    to: "someonethatisntverified@emailaddr.ca",
    from: "singlesenderverificationemailaddress@emailaddress.com",
    subject: "Some subject.",
    text: "Some text.",
    html: '<strong> why not have xss in the tutorial.</strong>'
};

(async function () {
    try {
        mail.setApiKey(process.env.SENDGRID_API_KEY);
        await mail.send(msg);
        console.log(process.env.SENDGRID_API_KEY);
    } catch (e) {
        console.error(e.response.body.errors);
    }
})()
```

![Single Sender Verification console error message](/images/uploads/sendgrid-ssv-errormessage.png)

I followed the link to [here](https://sendgrid.com/docs/ui/sending-email/sender-verification) and followed the directions.

![screenshot of sendgrid documentation page for single sender verification](/images/uploads/send-grid-ssvdocspage).

Then it works, finally.

