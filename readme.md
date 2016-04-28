# npm-publish-index-test

> npm publish test repository

Issue: https://github.com/npm/npm/issues/12498

## Problem

When I upgraded to Node 6, it came shipped with `npm@3.8.6`. I released new versions from some packages and after using those packages, my `index.js`
file was not published. At first I thought that it only affected me, "I must have done something wrong!". But it appeared that
[Sindre Sorhus](https://github.com/sindresorhus) released his [array-differ](https://github.com/sindresorhus/array-differ) package after installing
Node 6 and suffered from the same bug.

After testing things out, it seems that something is going wrong when specifying the [files](https://github.com/SamVerschueren/npm-publish-index-test/blob/v0.2.0/package.json#L15-L18)
property in your `package.json` file. If that property is used, the `index.js` file is not being published when using `npm@3.8.6`.

### Test

Go to your module directory and run the following command

```
$ npm pack
```

This will generate a tarball just like the one that will be published. So extract the contents and take a look if some files are missing.


## Solution

Downgrade `npm` to `npm@2` and republish your package!

