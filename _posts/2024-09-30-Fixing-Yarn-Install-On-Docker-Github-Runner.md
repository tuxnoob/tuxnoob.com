---
title: "Fixing Yarn Install On Github Runner Using Docker"
author: arief
date: 2024-09-30 20:00:00 +07:00
categories: [Infrastructure]
tags: [Docker, Github, Yarn, Ubuntu, Linux, Github Actions, Github Runner, Node.js]
---

![yarninstall](/assets/images/yarn-install.png){: width="1250" height="300"}

_Image by [Arief JR](https://linkedin.com/in/arief-jr)_


A few weeks ago, I was using a Docker container on a GitHub Actions runner to build and test my project. In case the developer team has built a new library project that needs to be installed in the main project, I used the `yarn install` to call the library project inside package.json on private github repository.
However, I encountered an issue when trying to install Yarn using the `yarn install` command i got error on above image. Here is the error message:

```plaintext
#16 ERROR: process "/bin/sh -c yarn install" did not complete successfully: exit code: 1
------
 > [builder 8/9] RUN yarn install:
60.57 [1/4] Resolving packages...
60.59 [2/4] Fetching packages...
62.74 [1/4] Resolving packages...
62.76 [2/4] Fetching packages...
62.83 error https://registry.yarnpkg.com/@typescript-eslint/eslint-plugin/-/eslint-plugin-6.0.0.tgz: Extracting tar content of undefined failed, the file appears to be corrupt: "ENOENT: no such file or directory, chmod '/usr/local/share/.cache/yarn/v6/npm-@typescript-eslint-eslint-plugin-6.0.0-19ff4f1cab8d6f8c2c1825150f7a840bc5d9bdc4-integrity/node_modules/@typescript-eslint/eslint-plugin/README.md'"
62.83 info Visit https://yarnpkg.com/en/docs/cli/install for documentation about this command.
```

```plaintext
#16 ERROR: process "/bin/sh -c yarn install" did not complete successfully: exit code: 1
------
 > [builder 8/9] RUN yarn install:
51.24 [1/4] Resolving packages...
51.27 [2/4] Fetching packages...
52.05 error https://registry.yarnpkg.com/@nodelib/fs.walk/-/fs.walk-1.2.8.tgz: Extracting tar content of undefined failed, the file appears to be corrupt: "ENOENT: no such file or directory, chmod '/usr/local/share/.cache/yarn/v6/npm-@nodelib-fs-walk-1.2.8-e95737e8bb6746ddedf69c556953494f196fe69a-integrity/node_modules/@nodelib/fs.walk/out/providers/index.js'"
52.05 info Visit https://yarnpkg.com/en/docs/cli/install for documentation about this command.
```

```plaintext
49.66 [3/4] Linking dependencies...
49.82 error An unexpected error occurred: "ENOENT: no such file or directory, lstat '/usr/local/share/.cache/yarn/v6/npm-libphonenumber-js-1.11.4-e63fe553f45661b30bb10bb8c82c9cf2b22ec32a-integrity/node_modules/libphonenumber-js/.gitlab-ci.yml'".
49.82 info If you think this is a bug, please open a bug report with the information provided in "/app/yarn-error.log".
49.82 info Visit https://yarnpkg.com/en/docs/cli/install for documentation about this command.
50.62 [3/4] Linking dependencies...
```

and many more error message if i re-run the pipeline job.

So i tried to find a solution to fix this issue, and i found a solution that i can use on my project. Then i found a solution that i can use on my project. here is the solution:

You should running or add command inside your dockerfile with:

```bash
yarn cache clean --all
```

If in dockerfile will be:

```bash
RUN yarn cache clean --all
```

And add this one command inside your dockerfile:

![Docker](/assets/images/Dockerfile.png)

add command `--network-concurrency 1`

So it will fixed the issue. Have a nice day!
