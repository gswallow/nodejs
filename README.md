# nodejs-cookbook [![Build Status](https://travis-ci.org/redguide/nodejs.svg)](https://travis-ci.org/redguide/nodejs)

## DESCRIPTION

Installs Node.js and manage npm

## USAGE

Include the nodejs recipe to install node on your system based on the default installation method:
```chef
include_recipe "nodejs"
```
Installation method can be customize with attribute `node['install_method']`

### Install methods

#### Package

install node from packages:
Note that only apt (Ubuntu, Debian) appears to have up to date packages available.
Centos, RHEL, etc are non-functional. (Try install_from_binary for those)
```chef
node.default!['install_method'] = 'package'
# Or
include_recipe "nodejs::nodejs_from_package"
```

#### Binary

Install node from official prebuilt binaries:
```chef
node.default!['install_method'] = 'binary'
# Or
include_recipe "nodejs::install_from_binary"
```

#### Source

Install node from sources:
```chef
node.default!['install_method'] = 'source'
# Or
include_recipe "nodejs::nodejs_from_source"
```

## NPM

Npm is included in nodejs installs by default.
By default, we are using it and call it `embedded`.
Adding recipe `nodejs::npm` assure you to have npm installed and let you choose install method with `node['npm']['install_method']`
```chef
include_recipe "nodejs::npm"
```

## LWRP

### nodejs_npm

`nodejs_npm` let you install npm packages from various sources:
* npm registry:
 * name: `attribute :package`
 * version: `attribute :version` (optionnal)
* url: `attribute :url`
 * for git use `git://{your_repo}`
* from a json (packages.json by default): `attribute :json`
 * use `true` for default
 * use a `String` to specify json file
 
Packages can be installed globally (by default) or in a directory (by using `attribute :path`)
 
This LWRP try to use npm bare as much as possible (no custom wrapper).

#### [Examples](test/cookbooks/nodejs_test/recipes/npm.rb)

## AUTHORS

* Marius Ducea (marius@promethost.com)
* Nathan L Smith (nlloyds@gmail.com)
* Guilhem Lettron (guilhem@lettron.fr)
* Barthelemy Vessemont (bvessemont@gmail.com)
