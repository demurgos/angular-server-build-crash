# Server build crash without output

This repo contains is based on the Angular Universal example, it removes all extra files
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
