# anderson

*checks your go dependencies for contraband licenses*

## usage

If you don't have an `.anderson.yml` in your current directory then a listing
of your dependencies and their license types are shown.

![Without Config](media/without-config.png)

If you add a `.anderson.yml` file then your dependencies will be checked for
valid licenses. The syntax of this file can be found below.

![Without Config](media/with-config.png)

Anderson can operate in two different modes. When invoked with input on *STDIN*
it will read the packages that it should scan from there. If no input is given
then it will make a best effort attempt to scan the packages that it should
scan itself. Automatic scanning can sometimes fail if you have transitive
(often test) dependencies that you do not include.

Most of the package and dependency listing code was graciously taken from
[Godep](https://github.com/tools/godep).

## installation

```
go get -u github.com/contraband/anderson
```

## configuration

You can configure *anderson* to be more or less lenient when checking you
dependencies. A file called `.anderson.yml` in the root of your Go package will
be checked when you run it.

``` yml
---
whitelist:
- MIT

blacklist:
- GPL

exceptions:
- github.com/xoebus/greylist
```

The whitelisted section is for licenses that are always allowed. Conversely,
the blacklist section is for licenses that are never allowed and will always
fail a build. Any licenses that are not explicitly mentioned are considered
to be in a "greylist" and will need to be explicitly allowed by adding the
import path to the exceptions.

