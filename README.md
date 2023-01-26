# Server build crash without output

[Angular CLI issue #24612](https://github.com/angular/angular-cli/issues/24612)

This repo content is based on the Angular Universal example, it removes all extra files
to only expose server rendering.

The file `server.ts` has a syntax error on line 10 which causes a build failure. Angular
crashes with exit code 1 **without printing any diagnostic**.

Commands:

```
npm install
npm run build
```

Output on my machine:

```
$ uname -a
Linux red 6.1.7-arch1-1 #1 SMP PREEMPT_DYNAMIC Wed, 18 Jan 2023 19:54:38 +0000 x86_64 GNU/Linux
$ node --version
v18.13.0
$ npm run build

> angular.io-example@0.0.0 build
> ng run angular.io-example:server

✔ Server application bundle generation complete.
$ echo $?
1
$ ls dist/
ls: cannot access 'dist/': No such file or directory
```

Expected behavior: The TypeScript syntax error should be reported in the console.

This is a regression in Angular 15 compared to Angular 14.

The `ng14` branch is configured to use Angular 14.2. Here's th output with Angular 14:

```
$ npm run build

> angular.io-example@0.0.0 build
> ng run angular.io-example:server

✔ Server application bundle generation complete.

Initial Chunk Files | Names         | Raw Size
main.js             | main          |  5.68 MB | 

                    | Initial Total |  5.68 MB

Build at: 2023-01-26T07:36:35.761Z - Hash: 2ce5cd4dbb2aca9e - Time: 6918ms

Error: server.ts:10:39 - error TS1005: 'from' expected.

10 import { AppServerModule } /* from */ './src/main.server';
                                         ~~~~~~~~~~~~~~~~~~~


Error: Optimization error [main.js]: SyntaxError: Unexpected token: punc ({)

$ echo $?
1
```
