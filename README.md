### Connect server via ssh:
```
ssh gokhan@159.89.102.25
```

### Tunnel Forwarding
_Because Google-Chrome only accepts requests from localhost_
```
ssh -L 0.0.0.0:9223:localhost:9222 localhost -N
```

### Run headless browser (should be other than 'root' user)
```
google-chrome --headless --remote-debugging-port=9222
```

### Web Socket Information and String for the puppeteer.connect() can be found
```
http://159.89.102.25:9223/json/version

Look for "webSocketDebuggerUrl" property
```

### Connection code for the robot
```js
const wsChrome= "ws://ws://159.89.102.25:9223/devtools/browser/7c59e4eb-d442-4ad6-8df3-94488a0bfe9b";

(async () => {
    const browser = await puppeteer.connect({
        browserWSEndpoint: wsChrome,
    }).catch(e => console.log(e));
})();
```

### Chrome Run Flags
http://codefodder.github.io/chrome-chromium-startup-flags/
