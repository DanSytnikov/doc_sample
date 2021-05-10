# ExampleProject

## Installation

ExampleProject requires [Node.js](https://nodejs.org/) v10+ to run.

### Windows

###### (failed. Steps to reproduce)

```sh
cd example
npm i
npm run server
```
Open the second therminal:
```sh
npm run watch -t 3000
```
Open `localhost:3000`.

For production environments (before starting server) ...

```sh
NODE_ENV=production
```

##### Blocker/error:

```
Error: graphql error
    at /home/andrewpltnv/job/webapp-website/dist/server/index.js:276081:21
    at processTicksAndRejections (node:internal/process/task_queues:96:5) {
  errors: [
    Error: Request failed with status code 404
        at createError (/home/andrewpltnv/job/webapp-website/dist/server/index.js:115663:15)
        at settle (/home/andrewpltnv/job/webapp-website/dist/server/index.js:115884:12)
        at IncomingMessage.handleStreamEnd (/home/andrewpltnv/job/webapp-website/dist/server/index.js:115024:11)
        at IncomingMessage.emit (node:events:377:35)
        at IncomingMessage.emit (node:domain:532:15)
        at endReadableNT (node:internal/streams/readable:1312:12)
        at processTicksAndRejections (node:internal/process/task_queues:83:21) {
      config: [Object],
      request: [ClientRequest],
      response: [Object],
      isAxiosError: true,
      toJSON: [Function (anonymous)]
    }
  ]
```


## Docker

###### (failed. Steps to reproduce)

```sh
cd example
docker build -t example:dev .
docker run -p 3000:80 example:dev
```

##### Blocker/error:
```
Not Found - GET https://npm.pkg.github.com/@hireflix%2futils-constants - npm package "utils-constants" does not exist under owner "hireflix"
npm ERR! 404
npm ERR! 404  '@hireflix/utils-constants@1.0.0' is not in the npm registry.
npm ERR! 404 You should bug the author to publish it (or use the name yourself!)
npm ERR! 404 It was specified as a dependency of 'webapp-website'
```

Assumptions how to fix here (if you have).

```sh
docker run -d -p 8000:8080 --restart=always --cap-add=SYS_ADMIN --name=dillinger <youruser>/dillinger:${package.json.version}
```



```sh
127.0.0.1:8000
```

## Linux/WSL

```
cd example
npm i
npm run server-watch
```
Open `localhost:3000`

No blockers.

