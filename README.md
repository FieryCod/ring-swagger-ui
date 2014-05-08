# Ring-Swagger-UI

Jar-packaged version of [Swagger-UI](https://github.com/wordnik/swagger-ui) for ring-based clojure web-apps (and other JVM apps).

## Usage

Add the following dependency to your `project.clj` file:

```clojure
[metosin/ring-swagger-ui "2.0.16"]
```

and you have full Swagger-UI ready in `/swagger-ui` on classpath.
The `ring.swagger.ui` namespace includes a function which can be used to create ring handler to serve the Swagger-ui.
The default URI for the api-docs is `/api/api-docs` but this can be changed by copying `resources/swagger-ui/conf.js`
to your own project or using provided function to create handler which will dynamically create proper file based
on given options.
 You can override the `index.html`-page by putting a new page into your local `resources/swagger-ui`-directory.

You might also be intrested in [Ring-Swagger](https://github.com/metosin/ring-swagger).

## Usage

Example using [Compojure-api](https://github.com/metosin/compojure-api) and setting custom urls for swagger-docs and swagger-ui.
```Clojure
(defapi app
  (ring.swagger.ui/swagger-ui
    "/swagger-ui"
    :api-url "/swagger-docs")
  (compojure.api.swagger/swagger-docs
    "/swagger-docs"
    :title "Sample Api"
    :description "Compojure Api sample application")
  ...)
```

## Packaging

### Initialize the submodules
```Shell
git submodule init
git submodule update
```

### New swagger-ui version
```Shell
pushd ext/swagger-ui
git fetch
git checkout <new tag>
popd
git add ext/swagger-ui # Update submodule to point into new swagger-ui
vim project.clj README.md # Edit version
git add project.clj README.md
git commit -m "New version"
git tag -m "v2.y.z"
git push --tags origin master # Push new tags and master
lein do clean, install
```

## TODO

- Automate updates
  - Update index.html automatically
  - Daily builds (Travis?)

## License

### Swagger-UI

Copyright 2011-2013 Wordnik, Inc.

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.

### These scripts

Copyright © 2014 Metosin Oy

Distributed under the Eclipse Public License, the same as Clojure.
