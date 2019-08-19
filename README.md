# florian-schoppmann.net

This repository contains the source of [florian-schoppmann.net](https://florian-schoppmann.net). It is built using [Jekyll](https://jekyllrb.com) and designed with [Bootstrap](https://getbootstrap.com).

In order to preview the site locally, follow the instructions on GitHub, titled [“Setting up your GitHub Pages site locally with Jekyll”](https://help.github.com/articles/setting-up-your-pages-site-locally-with-jekyll/). Basically, what it comes down to is installing [Bundler](https://bundler.io) once with

```sh
gem install bundler
```

and use

```sh
bundle exec jekyll serve
```

to start a local webserver that automatically refreshes as you update the local files. It uses the same versions as GitHub Pages in order to compile the site (this is configured in file `Gemfile`). Initially, and whenever versions used by GitHub Pages are updated, run:

```sh
bundle install
```

## Publishing

As one-time setup, define the git alias `prepare-website` and define the remote repository `website`:
```sh
git config alias.prepare-website \
  '!git branch -f website $(git commit-tree HEAD^{tree} -m "Website as of commit $(git rev-parse HEAD)")'
git remote add website https://github.com/fschopp/florian-schoppmann.net.git
git config remote.website.push '+website:master'
```

Publishing happens by pushing to the `master` branch of the `website` remote repository. This is accomplished with the following commands:

```sh
git prepare-website
git push website
```

The first command recreates the local `website` branch as an identical copy of `HEAD`, but with no history. The second command force-pushes the `website` branch (as configured above).
