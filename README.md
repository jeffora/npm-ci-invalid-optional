# Invalid `npm ci` install

## Description

When a project has an optional dependency on a git url (e.g. a fork of an existing npm module that has been modified)
`npm ci` will install the module from `npm`, not from `git`, resulting in an invalid install where the code a project is
using is not the code expected.

Running `npm install` does not suffer from the same behaviour.

This project includes an optionalDependency on a fork of `left-pad`. This fork simply adds one line: `console.log('custom left-pad');`.

When running the steps below, the incorrect (npm registry version) of `left-pad` is installed instead of the `git` version.

**Steps**:
1. Run `npm install`
2. Run `grep "custom" node_modules/left-pad/index.js`
  - this will output `console.log('custom left-pad');`
3. Run `npm ci`
4. Rerun `grep "custom" node_modules/left-pad/index.js`
  - there will be no results found
