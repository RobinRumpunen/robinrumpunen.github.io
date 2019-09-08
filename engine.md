---
layout: page
menus: header
title: Engine
permalink: /engine
---

# Echo Engine
This is a brief overview of my ongoing personal engine, dubbed “Echo Engine”.
Down below you will see the current achievements of the project.

Try it out for yourself!
Download binaries here:
	[Win64](/download/win64)
	[Win32](/download/win32)
	[OSX](/download/OSX)
	[Linux](/download/linux)

#### Echo engine is a personal engine created from scratch* by me.
It was started as a way for me to better understand what is truly going on
under the hood of a modern mid sized game engine.
- Development is still a work in progress.
 * Everything used except Assimp is written by me, more details further down.

Vulkan renderer.
Fully written renderer backend with Vulkan.
No extensions part from Khrono’s “swapchains” has been enabled.
Allowing any platform supporting Vulkan to be compatible.

Dynamic soft shadows.
Variable soft shadow mapping has been implemented based on three passes*.
1. Light-space pass storing depth (D).
2. X-direction filter storing a two component texture (D-filtered, D2-filtered).
3. Y-direction filtering based on the previous texture.
 * Currently only supporting one light, however work has started on supporting
   multiple lights.

Physically based shading model.
PBS based on Epic Games’ approach.
Utilizing “Image Based Lighting” provided via cubemap textures used to generate
radiance and irradiance textures.











Image importing library.
Fully written image importing library supporting KTX v1.1 and TGA file formats.
The KTX file format allows for storing mips, meta data (e.g. internal formats),
cubemaps, texture arrays, and beyond 8 bit/channel data. Also included are
image manipulation tools such as mirroring and image orientation.

Math library
The engine uses a custom math library written from scratch.
Starting of as a way for me to exercise and read up on my mathematical knowledge
this has become the foundation of this journey. It has been a great learning
experience but also streamlining the code without introducing 3rd party overhead.

Window & input handling. 
Input handling has been configured to consists of states, keys and ‘actions’.
On startup the system registers key-codes to actions*.
Each frame the Window might trigger an input update, the input handler then
goes through the registered keys and updates their state;
Pressed, Released (max one frame), or Inactive.
Any system can then query the input handler and create logic based on an action
and a state.

 * Work has started on an XML-style key configuration file, mapping actions to
   key-codes enabling user customization.
Currently only supported platform is windows, but work has been put through to
change between system configurations when alternatives have been implemented.

Model loading.
Currently provided via 3rd party Assimp file loading library.
Used to import model data, but the plan is to create a custom system.
https://github.com/assimp/assimp

Contribution?
Feel free to take a look inside the source code
Issue requests are open, contribute via Github!














This guide assumes that you already have created your blog and tested locally. If not please follow this tutorial : [Create a Blog using devlopr jekyll](https://devlopr.netlify.com/guides/2017/11/19/build-a-blog-using-devlopr-jekyll). Then come back and proceed with the deployment process.

In this Guide, we are using Github Pages and Travis CI for deploying our blog. Sometimes Github Pages does not support external third party plugins. In that case we deploy our blog using Travis CI, it automatically builds our website and pushes the static files of the site to a deployment branch. Which then Github Pages uses to render the site. Hope you get it :P !

We might need to instruct Travis CI to follow deployment instructions. Copy the below content in `.travis.yml` file:

```yml
language: ruby
cache: bundler

# Travis will build the site from gh-pages branch 
# and deploy the content to master branch 
# use gh-pages branch to serve for github pages
# master branch will be used for deployment

branches:
  only:
  - gh-pages
script: 
  - JEKYLL_ENV=production bundle exec jekyll build --destination site

# You need to generate a Personal Access Token 
# https://github.com/settings/tokens
# Add this token in environment variable GITHUB_TOKEN in Travis CI repo settings

deploy:
  provider: pages
  local-dir: ./site
  target-branch: master
  email: deploy@travis-ci.org
  name: Deployment Bot
  skip-cleanup: true
  github-token: $GITHUB_TOKEN
  keep-history: true
  on:
    branch: gh-pages

# Generate your secure token with the travis gem:
# get Github token from your Travis CI profile page
  gem install travis
  travis encrypt 'GIT_NAME="YOUR_USERNAME" GIT_EMAIL="YOUR_EMAIL" GH_TOKEN=YOUR_TOKEN' --add env.global --com

# env:
#   global:
#     secure: Example
```

All we are doing is telling Travis to pick up files from our **gh-pages** branch and push the build files to **master** branch.

##### Generate a New Github Personal Access Token 

We need this token as a Environment Variable in Travis. For Travis can automatically login as you, and finish its job of building your site and pushing it to your repo's master branch.

Go to [Github Generate a New Token](https://github.com/settings/tokens) Page.

![deploy using travis](/assets/img/posts/d1.png){:class="img-fluid"}

Create a new Access Token 

![deploy using travis](/assets/img/posts/d2.png){:class="img-fluid"}


##### Configure Travis 

Go to [Travis](https://travis.org) and Toggle the repository access to use Travis 

![deploy using travis](/assets/img/posts/d3.png){:class="img-fluid"}

Go to the repository settings page and Add Environment Variable 'GITHUB_TOKEN' 
![deploy using travis](/assets/img/posts/d4.png){:class="img-fluid"}

##### Push your changes to Github 

Commit your local changes in gh-pages branch 

`git add .`
`git commit -m "added new post"`
`git push origin gh-pages`

After push, Travis will automatically run a build process and deploy your blog.

![deploy using travis](/assets/img/posts/d5.png){:class="img-fluid"}

You can visit your site at https://yourusername.github.io

![deploy using travis](/assets/img/posts/d6.png){:class="img-fluid"}

Done ! Enjoy your brand new devlopr-jekyll blog. You can visit the site at https://yourusername.github.io