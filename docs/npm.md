####
**Package vs Module**
####

A module is a single js file with reusable functionality.

A package is made up of one or more modules.

npm install will install all dependencies

npm test will run npm test script if one is created

**Help**

npm <command> -h to to get help -- for text based help

npm -h <command> to to get help -- for online official help page


npm help-search <command*> - this will regex search for commands that start with that name


**Shortcuts**

https://docs.npmjs.com/misc/config - shorthand for flags

npm install - npm i


Package .json

track depencies
run scripts so you don't grunt
npm init - create it using npm init
$ npm set init-author-name Cesar Aviles
$ npm get init-author-name Cesar Aviles
$ npm config remove init-author-name 

**NPM INSTALL**

npm install -g install package globaly -- for instance to get mocha or gulp from command line
npm install <package> --S or --save -- to save to your dependencies section of package.json
npm install <package> --D or --save-dev -- to save to dev dependencies
npm list - shows dependencies hierarchy
npm list -g -depth 0 -- to view the global packages you've installed


**Semantic versioning**

major.minor.patch

major version means something is not backwards compatible
minor is a simple new feature
patch is a bug fix

npm install <package>@1.8 -- will install the latest 1.8.x version

npm install <package>@1.8.4 -- will install 1.8.4

leave off the @version to install the latest package

npm install <package>@">=1.8.4 <1.9.3" -- get any package between the two versions

npm install <package> -- will install the latest

npm install <package>@">=1.8.4 <1.9.3"

npm install <package>@"^1.8.4" -- will install any version at or newer than this version

npm install <package>@"~1.8.4" -- will install newer version as long as they are 1.8

npm update -- update packages

npm update --dev update dev packages

npm update --prod update prod packages

npm update -g -- will update global libraries

npm install <giturl or other url> -- this is the same as installing with the npm package name

npm i <folder> -- install from a local or network path

via browser

npmjs.com -- here you can search the registry

npm.im/<packagename> -- gives packages details

npm remove <package> -- remove can be used to remove packages from your packages.json file 

npm prune <package> -- remove can be used to remove packages that are extraneous aka not in  packages.json file 

npm list --depth 0 -- list packages we've installed

npm prune --production -- will remove all dev dependencies so your package is ready to go to prod

npm repo <package> -- goes to github page for package

**sudo npm npm@lates -g -- upgrade npm**

--save -- will always add ~

npm install --save-dev @types/mocha -- install type defs to get intellisense in webstorm
npm install @types/node --save-dev -- node typings











