# builder-test-app

> @dinocarl I think you'll love this

Based on Formidable's **Builder**: http://formidable.com/open-source/builder/

## Setup

1. Create a sandbox directory.
2. Clone this repository, https://github.com/code-for-coffee/builder-archetype-example-dev, and https://github.com/code-for-coffee/builder-archetype-example into that folder.
3. `cd` into `builder-test-app` (this project)
4. `npm i` to install everything. You'll notice that your `node_modules` contains many dependencies that *are not* in our package.json. They are instead hosted in two central locations.

> Script for the lazy:

```bash
cd 
mkdir sandbox && cd sandbox
git clone https://github.com/code-for-coffee/builder-archetype-example-dev.git
git clone https://github.com/code-for-coffee/builder-archetype-example.git
git clone https://github.com/code-for-coffee/builder-test-app.git
cd builder-test-app
npm i
```

## Holy crap! how the fuck does this work!?

Two archetypes are created: one for dependencies and one for devDependencies. Those repos contain dependencies to be installed in each project. We specify the set via an **Archetype** file in the `.builderrc` file:

```yaml
---
archetypes:
  - builder-archetype-example
```

Looks directly in our package.json for two dependencies (specified via file system OR npm modules; Git *does not work* per https://github.com/FormidableLabs/builder/issues/98): 

- builder-archetype-example (in our example this contains the modules: *semver* & *structz*)
- builder-archetype-example-dev (in our example this contains the mdoules: *webpack*)

From there, builder then installs the depencies directly into node_modules. 

From there we can have webpack directly reference the node_modules folder as needed. There is a direct integration for this too: http://formidable.com/open-source/builder/#webpack-and-module-pattern

## In Conclusion

Builder provides us a single source of truth for package dependencies and devDepencies on large scale enterprise projects.
