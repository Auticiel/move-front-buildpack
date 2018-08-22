Add as a first buildpack in the chain. Set `FRONT_PATH` environment variable to point to front root. It will be moved to project root, and overwrite files if there is a conflict. Following buildpack (e.g. nodejs) will finish slug compilation.

The intent is to support having your front-end in a git submodule and copy it to the root at compile time so that heroku/nodejs buildpack properly detects the package.json

Based on https://github.com/timanovsky/subdir-heroku-buildpack

**Disclaimer:** I may change the code without notice, so always pin to specific github version. Provided as is.

# How to use:
1. `heroku buildpacks:clear` if necessary
2. `heroku buildpacks:set https://github.com/Auticiel/move-front-buildpack`
3. `heroku buildpacks:add heroku/nodejs` or whatever buildpack you need for your application
4. `heroku config:set FRONT_PATH=projects/nodejs/frontend` pointing to your front root
5. Deploy your project to Heroku.

# How it works
The buildpack takes subdirectory you configured and copies that subdirectory to project root, overwriting any file that conflicts. Then normal Heroku slug compilation proceeds.
