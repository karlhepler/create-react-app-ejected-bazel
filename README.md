# create-react-app-ejected-bazel

The purpose of this repo is to demonstrate an issue I'm having with Bazel and an **ejected** `create-react-app` project.

## Baseline Context

When a `create-react-app` project is ejected, `config/` and `scripts/` directories are created and filled with files. You will notice that the `build` script in `package.json` looks like this: `node scripts/build.js`. If you run `yarn build`, then you will see that a `build/` directory is created in the source root and that it is filled with output files.

## Integrating Bazel

1. I added `WORKSPACE` and `BUILD.bazel` files and set everything up to build correctly with Bazel.

2. If you run `git checkout 5517901ab51bf4110aa1c50049b358fd6957048e && yarn bazelisk clean && yarn bazelisk run //:build`, you will notice that the `scripts/build.js` is executed by Bazel. However, instead of outputting a `build/` directory in the source root, it outputs a `build/` directory here: `bazel-bin/build.sh.runfiles/create-react-app-ejected-bazel/build`.

3. If you run `git checkout 217ff3953df9ee09929717ef0ee8e30713671c37 && yarn bazelisk clean && yarn bazelisk build //:bundle`, you will notice that everything builds correctly and outputs to `bazel-bin/bundle/` as expected.

## Problem

If you run `git checkout c6a4e62053d3d4fd3c294752e3a19d2be7556484 && yarn bazelisk clean && yarn bazelisk build //project:bundle`, you will notice that it doesn't build. I can't figure it out. I've tried to get this working for days.

I expect it to output `bazel-bin/project/bundle/` full of output files.
