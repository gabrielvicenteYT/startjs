---
description: In this tutorial we will make a basic video downloader for youtube.
---

# Building a Basic Youtube Video Downloader \(Part. 1\)

## Getting Started

First Off, Create a New Folder called DownloadYT

Next, follow our Setting up a Folder from our [Yarn](../../npm/yarn.md#how-to-initialize-a-folder-using-yarn) Tutorial.

Then, run the following in the Visual Studio Code Terminal \(in your new folder\)

```bash
yarn add ytdl-core
yarn add express
yarn add open
```

Next, create a new file called index.js and add the following to it:

```javascript

// Add all the libraries
const fs = require("fs");
const open = require("open");
const ytdl = require("ytdl-core");
// init project
const express = require("express");
const app = express();
let os = require('os')
// we've started you off with Express,
// but feel free to use whatever libs or frameworks you'd like through `package.json`.
ytdl("https://www.youtube.com/watch?v=Yp-VBg3LFqY", { filter: format => format.container === 'mp4' }).pipe(fs.createWriteStream("video.mp4"));
var dir = os.userInfo().homedir + "/videos/downloadYT";

if (!fs.existsSync(dir)) {
  fs.mkdirSync(dir);
  console.log("madedir")

}
// http://expressjs.com/en/starter/basic-routing.html
app.get("/:id", function(req, res) {
  
  console.log("readytogo")
  var stream = ytdl("https://www.youtube.com/watch?v=" + req.params.id, {
    filter: format => format.container === "mp4"
  }).pipe(fs.createWriteStream(os.userInfo().homedir + "/videos/downloadYT/" + req.params.id+ ".mp4"));
  stream.on('finish', function () {
     open(
       os.userInfo().homedir + "/videos/downloadYT/" + req.params.id + ".mp4"
     );
     res.send(os.userInfo().homedir + "/videos/downloadYT/" + req.params.id + ".mp4");
     console.log("done")
  });
});

// listen for requests :)
const listener = app.listen(18080, function() {
  console.log("Your app is listening on port " + listener.address().port);
});
listener.setTimeout(99999999999999999999);
```

### Creating the Package

We need to add a new package to achieve this called pkg. For a good tutorial on this, use [this](https://dev.to/jochemstoel/bundle-your-node-app-to-a-single-executable-for-windows-linux-and-osx-2c89). Run the following in the VS code Terminal.

```javascript
yarn global add pkg
```

This installed the JavaScript compiler onto your computer.  To compile an application, run the following in the Visual Studio Code terminal:

```javascript
pkg .
```

Voila. We now have 3 files, one for each OS. Simply open the file like an app you wanted to install. This will start up the application ready to use in Part 2. 

### Code Explainer

```javascript
const fs = require("fs");
const open = require("open");
const ytdl = require("ytdl-core");
// init project
const express = require("express");
const app = express();
let os = require('os')
```

This adds all the required NPM Packages to your app.

```javascript
ytdl("https://www.youtube.com/watch?v=Yp-VBg3LFqY", { filter: format => format.container === 'mp4' }).pipe(fs.createWriteStream("video.mp4"));
var dir = os.userInfo().homedir + "/videos/downloadYT";
```

This makes sure the app is working by downloading a sample video.

```javascript
if (!fs.existsSync(dir)) {
  fs.mkdirSync(dir);
  console.log("madedir")
}
```

This makes sure the youtube download folder has been created. If it has not, it creates it.

```javascript
app.get("/:id", function(req, res) {
  console.log("readytogo")
```

This triggers when part 2 tells the app download a video.

```javascript
var stream = ytdl("https://www.youtube.com/watch?v=" + req.params.id, {
    filter: format => format.container === "mp4"
  }).pipe(fs.createWriteStream(os.userInfo().homedir + "/videos/downloadYT/" + req.params.id+ ".mp4"));
```

This downloads the youtube video.

```javascript
  stream.on('finish', function () {
     open(
       os.userInfo().homedir + "/videos/downloadYT/" + req.params.id + ".mp4"
     );
     res.send(os.userInfo().homedir + "/videos/downloadYT/" + req.params.id + ".mp4");
     console.log("done")
  });
});
```

This tells Part 2 that the download is done.

```javascript
const listener = app.listen(18080, function() {
  console.log("Your app is listening on port " + listener.address().port);
});
```

This starts the app

```javascript
listener.setTimeout(99999999999999999999);
```

This prevents the downloads from timing out.

