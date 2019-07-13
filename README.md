# Node JS and Express JS

## Node JS version

```
const http = require('http'); // import http module (req, res)
const fs = require('fs'); // import file system module (read html files)

// set up pages
const homePage = fs.readFileSync('index.html');
const aboutPage = fs.readFile('about.html');
const contactPage = fs.readFileSync('contact.html');

// create the server
const server = http.createServer((request, response) => {
  console.log(request.url);

  if (request.url === '/about') {
    return response.end(aboutPage);
  } else if (request.url === '/contact') {
    return response.end(contactPage);
  } else if (request.url === '/') {
    return response.end(homePage);
  } else {
    response.writeHead(404);
    response.end('<h2> 404 Page not found!</h2>');
  }
});

server.listen(3000);
```

### Express JS version

```

const express = require('express');
const path = require('path');

const app = express();
const port = 3000;

// set public folder for static requests
app.use(express.static('public'));

// define routes / serve files
app.get('/', (req, res) => {
  res.sendFile(path.resolve(__dirname, 'index.html'));
});

app.get('/about', (req, res) => {
  res.sendFile(path.resolve(__dirname, 'about.html'));
});

app.get('/contact', (req, res) => {
  res.sendFile(path.resolve(__dirname, 'contact.html'));
});

app.listen(port, () => {
  console.log(`app working on port ${port}`);
});
```

#### Start app

```
node index.js
```
