# npm-publish-index-test

> npm publish test repository

## Problem?

When I upgraded to Node 6, it came shipped with `npm@3.8.6`. I released new versions from some packages and after using those packages, all my
JavaScript files where vanished. At first I thought that it only affected me, "I must have done something wrong!". But it appeared that
[Sindre Sorhus](https://github.com/sindresorhus) released his [array-differ](https://github.com/sindresorhus/array-differ) package after installing
Node 6 and suffered from the same bug.

After testing things out, it seems that something is going wrong when specifying the [files](https://github.com/SamVerschueren/npm-publish-index-test/blob/v0.2.0/package.json#L15-L18)
property in your `package.json` file. The files listed in that array are not being published when using `npm@3.8.6`.

## Solution

Downgrade `npm` to `npm@2` and republish your package!
