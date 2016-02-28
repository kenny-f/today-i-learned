# Deploying node app to Azure

## [Using a custom web.config for Node apps](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps)

## iisnode
- your nodejs server must listen on the `process.env.PORT` variable passed from iisnode.

## Webpack output breaks on Azure

TURNS OUT `    new webpack.DefinePlugin({"process.env": {NODE_ENV: '"production"'}})` IN THE WEBPACK CONFIRGURATION WAS CAUSING THIS!!! DUH. BLINDLY COPYING CODE. NAUGHTY!

After a webpack server build,  webpack turns

```
server.connection({
   	  host: process.env.HOST || 'localhost',
   	  port: process.env.PORT || 3000
   	});
```
TO
```
server.connection({
   	  host: ({"NODE_ENV":"production"}).HOST || 'localhost',
   	  port: ({"NODE_ENV":"production"}).PORT || 3000
   	});
```

Whhy locally the app was working on `localhost:3000` but after deployment to Azure it was not.

As mentioned above Azure sets the process.env.PORT value on startup so that must be passed in as a named piped for the hapi server.
