# gmail-send
Minimalistic module to send email using GMail 

Basically it's a wrapper around `nodemailer` package to simplify its usage for GMail even more.

# Install

````
npm install --save gmail-send
````

# Usage

To send emails using GMail you need to add application-specific password to access GMail:
[My Account](https://myaccount.google.com/) -> [Sign-in & security](https://myaccount.google.com/security) -> [Signing in to Google](https://myaccount.google.com/security#signin) -> [App passwords](https://security.google.com/settings/security/apppasswords?utm_source=OGB&pli=1)

Select 'Other (Custom name)' in 'Select app'/'Select device' drop-downs, enter descriptive name for your application and pc and press 'GENERATE'.
Copy provided password.

````
'use strict';

// file credentials.json looks like following:
// {
//   "user": "user@gmail.com",
//   "pass": "abcdefghijklmnop"
// }
var credentials = require('./credentials.json');

// Require'ing module and setting default options

var send = require('gmail-send')({  
  user: credentials.user,           // Your GMail account used to send emails
  pass: credentials.pass,           // Application-specific password
  to:   credentials.user,           // Send to yourself
  // from:    credentials.user         // from: by default equals to user
  // replyTo: credentials.user         // replyTo: by default undefined
  subject: 'test subject',          // subject:
  text:    'test text'              // plain text
});

var file = './package.json';

// Override any default option and send email

send({ // Overriding default parameters
  subject: 'attached file',         // new subject:
  files: [file]                     // file names to attach
}, function (err, res) {
  console.log('send(): err:', err, '; res:', res);
});
````
