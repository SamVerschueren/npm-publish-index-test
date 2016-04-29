# npm-publish-index-test

> npm publish test repository

Issue: [npm#12498](https://github.com/npm/npm/issues/12498) → [npm#5082](https://github.com/npm/npm/issues/5082)<br>
Status: Identified

## Problem

When I upgraded to Node 6, it came shipped with `npm@3.8.6`. I released new versions from some packages and after using those packages, my `index.js`
file was not published. At first I thought that it only affected me, "I must have done something wrong!". But it appeared that
[Sindre Sorhus](https://github.com/sindresorhus) released his [array-differ](https://github.com/sindresorhus/array-differ) package after installing
Node 6 and suffered from the same bug.

In the following case, the bug always occurs.

- Add `index.js` to the [files](https://github.com/SamVerschueren/npm-publish-index-test/blob/v0.2.0/package.json#L15-L18) property in `package.json`
- Have `node_modules` directory with your dependencies
- Have a `.gitignore` file which ignores the `node_modules` directory


### Why

> The improved performance of `fs.realpath` has changed the timing and order of operations enough that it greatly exacerbates the race condition.

So probably something goes wrong because Node 6 improved the performance of `fs.realpath`.


### Test

Go to your module directory and run the following command

```
$ npm pack
```

This will generate a tarball just like the one that will be published. So extract the contents and take a look if some files are missing.


## Solution

You have two options

1. Downgrade `npm` to `npm@2` and republish your package!
2. Remove the `node_modules` directory first before publishing

I can't say 100% for sure that option 2 always works. You can always test with `npm pack` before publishing.

