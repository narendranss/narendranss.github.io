Following are the commands to work with this repo,
1. install
2. serve-production
3. serve
4. new-post
5. generate-category
6. generate-tag

install
  - Installs jekyll and the dependencies required by personal-jekyll-theme

serve-production
  - Builds and serves your website in 127.0.0.1:4000

serve
  - Builds and serves your website without generating the Disqus comments and the Google Analytics code

new-post <title>
  - Creates a new post under \_posts

generate-category
  - Generate all the categories that are used in the \_posts

generate-tag
  - Generate all the tags that are used in the \_posts

integrate-personal
  - Integrates the latest bug fixes and new features from personal-jekyll-theme repository.
  Make sure to read [this](https://github.com/PanosSakkos/personal-jekyll-theme/wiki/Integrating-latest-bug-fixes-and-features-into-your-past-fork) before using it.

# Sample commands
```
ruby ./scripts/install
ruby ./scripts/serve
ruby ./scripts/serve-production
ruby ./scripts/new-post "My New Post"
ruby ./scripts/generate-category
ruby ./scripts/generate-tag
ruby ./scripts/integrate-personal
```