
# ExpressJS Web Server Start Guide 

## Getting Started (with Yarn)

{% hint style="warning" %}
Notice: This step requires that you have read our [NPM](npm.md) and [Yarn](npm/yarn.md) Tutorials and have completed the install step of the [Yarn](npm/yarn.md) tutorial.
{% endhint %}

First off, create a new folder called StartJS_Express.
Then, open it in Visual Studio Code and complete the "How to Initialize a Folder using Yarn" section of our [Yarn](npm/yarn.md) guide.
Next, run the following commands in the Terminal Feature of Visual Studio Code:

```bash
yarn add express
```

This has installed the web server module to your folder. Now you can start on creating a basic Node.js Express Web Server:

## Making the Web Server:

In this step we will make the web server. Make sure you have your new folder open in Visual Studio Code.
First off, create a new file called index.js with the following contents:

```javascript
// this line allows us to use the express.js module
var express = require("express");

// Add this line so we can serve files from our local
// directory
var path = require("path");
var app = express();

// Add the ability to serve our static files from the public directory
app.use(express.static("public"));

// Here we serve up our index page
app.get("/", function(req, res) {
  res.sendFile(path.join(__dirname + "/public/index.html"));
});

var server = app.listen(80, function() {
  var host = server.address().address;
  var port = server.address().port;
  console.log("startjs Demo Server listening at http://%s:%s", host, port);
});

```

Next, create a new folder called public and add a new file called index.html inside your "public" folder with the following contents:

```html

<!doctype html>
<html lang="en">
  <head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

    <!-- Bootstrap CSS -->
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/css/bootstrap.min.css" integrity="sha384-Vkoo8x4CGsO3+Hhxv8T/Q5PaXtkKtu6ug5TOeNV6gBiFeWPGFN9MuhOf23Q9Ifjh" crossorigin="anonymous">

    <title>Hello world!</title>
  </head>
  <body>
    <h1>Hello world!</h1>

    <!-- Optional JavaScript -->
    <!-- jQuery first, then Popper.js, then Bootstrap JS -->
    <script src="https://code.jquery.com/jquery-3.4.1.slim.min.js" integrity="sha384-J6qa4849blE2+poT4WnyKhv5vZF5SrPo0iEjwBvKU7imGFAV0wwj1yYfoRSJoZ+n" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.0/dist/umd/popper.min.js" integrity="sha384-Q6E9RHvbIyZFJoft+2mJbHaEWldlvI9IOYy5n3zV9zzTtmI3UksdQRVvoxMfooAo" crossorigin="anonymous"></script>
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/js/bootstrap.min.js" integrity="sha384-wfSDF2E50Y2D1uUdj0O3uMBJnjuUD4Ih7YwaYd1iqfktj0Uod8GCExl3Og8ifwB6" crossorigin="anonymous"></script>
  </body>
</html>

```

Now, type [localhost](http://localhost/) into your web browser. Congrats, you are now serving a website onto your network using Node.JS.

Now, let's review the code that we have just written:

```javascript
var express = require("express");
```

This line allows you to use the Express web server.

```javascript
var path = require("path"); // alllow express to use folders.
var app = express(); // create the server
```

These two lines create the Express web server and allows you to server a file on your Web Server.

```javascript
app.use(express.static("public")); // Tell express to use the Public Folder.
```

This line tells Express to use the Public folder to server your website from.

```javascript
app.get("/", function(req, res) {
  res.sendFile(path.join(__dirname + "/public/index.html"));
}); // Tells Express where the Homepage is.
```

This line (this is one line, expanded into 3 lines for easier readability) tells Express which file to use as the Homepage.

```javascript

var server = app.listen(80, function() {
  var host = server.address().address;
  var port = server.address().port;
  console.log("startjs Demo Server listening at http://%s:%s", host, port);
});
```

This line (this is one line, expanded into 3 lines for easier readability) starts the server.

The HTML file is a standard website. Feel free to change it to any HTML code. Just keep it's name as index.html.
