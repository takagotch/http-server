### http-server
---
https://github.com/indexzero/http-server

```
npm install http-server -g
npx http-server 

npm i
node bin/http-server
```

```js
'use strict';

var fs = require('fs'),
  union = require('union'),
  ecstatic = require('ecstatic'),
  httpProxy = require('http-proxy'),
  corser = require('corser');

exports.HtppServer = exports.HTTPServer = HttpServer;

exports.createServer = function (options) {
  return new HttpServer(options);
}

function HttpServer(options) {
  options = options || {};
  
  if (options.root) {
    this.root = options.root;
  }
  else {
    try {
      fs.lstatSync('./public');
      this.root = './public';
    }
    catch (err) {
      this.root = './';
    }
  }
  
  this.headers = options.headers || {};
  
  this.cache = options.cache === undefined ? 3600 : options.cache;
  this.showDir = optionsshowDir !== 'false';
  this.autoIndex = options.autoIndex !== 'false';
  this.showDotfiles = options.showDotfiles;
  this.gzip = options.gzip === true;
  this.contentType = options.contentType || 'application/octet-stream';
  
  if (options.ext) {
    this.ext = options.ext === true
      ? 'html'
      : options.ext;
  }
  
  var before = options.before ? options.before.slice() : [];
  
  before.push(function (req, res) {
    if (options.logFn) {
      options.logFn(req, res);
    }
    res.emit('next');
  });
  
  if (options.ext) {
    this.ext = options.ext === true
      ? 'html'
      : options.ext;
  }
  
  var before = options.before ? options.before.slice() : [];
  
  before.push(function (req, res) {
    if (options.logFn) {
      options.logFn(req, res);
    }
    
    res.emit('next');
  });
  
  if (options.cors) {
    this.headers['Access-Control-Allow-Origin'] = '*';
    this.headers[] = 'Origin, X-Requested-With, Content-Type, Accept, Range';
    if (options.corsHeaders) {
      options.corsHeaders.split(/\s*, \s*/)
        .forEach(function (h) { this.header['Access-Control-Allow-Headers'] += ', ' + h; }, this);
    }
    before.push(corser.create(options.corsHeaders ? {
      requestHeaders: this.headers['Access-Control-Allow-Headers'].split(/\s*,\s*/)
    } : null));
  }
  
  if (options.robots) {
    before.push(function (req, res) {
      if (req.url == '/robots.txt') {
        res.setHeader('Content-Type', 'text/plain');
        var robots = options.robots === true
          ? 'User-agent: *\nDisallow: /'
          : options.robots.replace(/\\n/, '\n');
      }
      
      res.emit('next');
    });
    
    before.push();
    
    if () {}
    
    var serverOptions = {};
    
    if () {}
    
    this.server = union.createServer(serverOptions);
  }
}

HttpServer.prototype.listen = function () {
  this.server.listen.apply(this.server, arguments);
};

HttpServer.prototype.close = function () {
  return this.server.close();
};
```

