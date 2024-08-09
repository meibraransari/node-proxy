---
Created: 2024-08-09T10:44:19+05:30
Updated: 2024-08-09T11:13:55+05:30
Maintainer: Ibrar Ansari
---
# Node-Proxy

##  Install required package
```
npm install http-proxy
```
#### Create https-server.js to use HTTPS
**Generate SSL**
```
openssl req -newkey rsa:2048 -nodes -keyout server.key -x509 -days 365 -out server.cert
```
nano https-server.js
```
const https = require('https');
const fs = require('fs');
const httpProxy = require('http-proxy');
// Create a proxy server
const proxy = httpProxy.createProxyServer({});
// Create an HTTPS server
const server = https.createServer({
    key: fs.readFileSync('path/to/server.key'),
    cert: fs.readFileSync('path/to/server.cert')
}, (req, res) => {
    // Proxy requests to Cube.js running on localhost:4000
    proxy.web(req, res, { target: 'http://localhost:4000' });
});
// Listen on port 443
server.listen(443, () => {
    console.log('HTTPS server listening on port 443');
});
```

#### Create http-server.js to use HTTP
nano http-server.js
```
const http = require('http');
const httpProxy = require('http-proxy');
// Create a proxy server
const proxy = httpProxy.createProxyServer({});
// Create an HTTP server
const server = http.createServer((req, res) => {
    // Proxy requests to Cube.js running on localhost:4000
    proxy.web(req, res, { target: 'http://localhost:4000' });
});
// Listen on port 80
server.listen(80, () => {
    console.log('HTTP server listening on port 80');
});
```

#### Run service from Node or PM2
```
node https-server.js
or 
pm2 start https-server.js
pm2 status
pm2 startup
pm2 save
```

#### Test it
> Open browser and check with HTTP or HTTPS base on above configuration used.

```
http://your_ip
or
https://your_ip
```
---
### 💼 Connect with me 👇👇 😊

- 🔥 [**Youtube**](https://www.youtube.com/@DevOpsinAction?sub_confirmation=1)
- ✍ [**Blog**](https://ibraransari.blogspot.com/)
- 💼 [**LinkedIn**](https://www.linkedin.com/in/ansariibrar/)
- 👨‍💻 [**Github**](https://github.com/meibraransari?tab=repositories)
- 💬 [**Telegram**](https://t.me/DevOpsinActionTelegram)
- 🐳 [**Docker**](https://hub.docker.com/u/ibraransaridocker)
