# koatty
Koa2 + Typescript = koatty. 

Use Typescript's decorator implement auto injection just like SpringBoot.

[![Version npm](https://img.shields.io/npm/v/koatty.svg?style=flat-square)](https://www.npmjs.com/package/koatty)[![npm Downloads](https://img.shields.io/npm/dm/koatty.svg?style=flat-square)](https://npmcharts.com/compare/koatty?minimal=true)

## Installation

```shell
npm i -g koatty_cli
```

## Quick Start

Check out the [quick start example][quick-example].

[quick-example]: https://github.com/thinkkoa/koatty_demo/

## Usage

### 1.Create Project

```shell
koatty new projectName

cd ./projectName

yarn install

npm start
```

### 2.Create a Controller
```shell
koatty controller test

```

### 3.Create a Service

```shell
koatty service test

```

### 3.Create a Middleware

```shell
koatty middleware test

```

### 4.Define TestController

```javascript
import { Controller, BaseController, Autowired, GetMaping, RequestBody, PathVariable, PostMaping, BaseApp, RequestMapping, RequestMethod } from "koatty";
import { TestService } from "../service/TestService";

interface App extends BaseApp {
    cache: any;
}

@Controller()
export class IndexController extends BaseController {
    app: App;

    @Autowired()
    private testService: TestService;

    init() {
        //...
        this.app.cache = {};
        console.log('IndexController.init()', this.app.cache);
    }

    @RequestMapping("/", RequestMethod.ALL)
    async default(@PathVariable("test") test: string) {
        const info = await this.testService.sayHello();
        return this.ok(test, info);
    }

    @PostMaping("/test")
    test(@RequestBody() body: any) {
        // return this.default('aaa');
        return this.ok("test", body);
    }
}
```



## How to debug

if you use vscode , edit the `.vscode/launch.json` , like this: 
```
{
    "version": "0.2.0",
    "configurations": [
        {
            "type": "node",
            "request": "launch",
            "name": "TS Program",
            "args": [
                "${workspaceRoot}/src/App.ts" 
            ],
            "runtimeArgs": [
                "--nolazy",
                "-r",
                "ts-node/register"
            ],
            "sourceMaps": true,
            "cwd": "${workspaceRoot}",
            "protocol": "inspector",
            "internalConsoleOptions": "neverOpen"
        }
    ]
}
```
Select `TS Program` to debug run. Try to call `http://localhost:3000/` .