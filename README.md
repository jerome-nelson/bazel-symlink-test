## Issue
Yarn workspaces symlink dependencies. There is a boundary conflict when using `yarn_install`/`npm_install` as 
Bazel files are renamed _BUILD, due to being detected as external dependencies.

As a result any local builds will not run as BUILD files will be renamed to _BUILD

* To replicate:
    - Setup yarn bazel WORKSPACE i.e `yarn create @bazel [foldername] --packageManager yarn --typescript`
    - Create sub package i.e `packages/subpackage` and add as [yarn workspace](https://yarnpkg.com/en/docs/workspaces)
    - Create BUILD target in `subpackage` (I used `ts_library` as ) and setup package.json
    - run `yarn bazel build //...`
    - Watch file rename so BUILD isn't run 