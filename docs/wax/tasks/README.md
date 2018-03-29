# Wax Tasks

Wax Tasks is a gem-packaged set of [Rake](https://ruby.github.io/rake/) tasks for creating minimal exhibitions with [Jekyll](https://jekyllrb.com/), [IIIF](http://iiif.io), and [ElasticLunr.js](http://elasticlunr.com/). These tasks are the muscle behind [Wax](/wax/)—building search indexes, generating pages, running tests and more behind the scenes.


## Getting Started

### Prerequisites

You'll need `Ruby >= 2.2` with `bundler` installed. Check your versions with:
```bash
$ ruby -v
  ruby 2.4.2p198 (2017-09-14 revision 59899) [x86_64-darwin15]

$ bundler -v
  Bundler version 1.16.1
```

To use the IIIF task, you will also need to have ImageMagick installed and functional. You can check to see if you have ImageMagick by running:
```bash
$ convert -version
  Version: ImageMagick 6.9.9-20 Q16 x86_64 2017-10-15 http://www.imagemagick.org
  Copyright: © 1999-2017 ImageMagick Studio LLC
  License: http://www.imagemagick.org/script/license.php
  Features: Cipher DPC Modules
  Delegates (built-in): bzlib freetype jng jpeg ltdl lzma png tiff xml zlib
```

You can learn more about installing ImageMagick (e.g., for [mac](http://macappstore.org/imagemagick/) or [ubuntu](https://www.tutorialspoint.com/articles/how-to-install-imagemagick-on-ubuntu)) or ignore this completely if you do not plan to generate IIIF derivatives.

### Installing

Add `wax_tasks` to your Jekyll site's Gemfile:

```ruby
gem 'wax_tasks'
```

... and install with bundler:

```bash
$ bundle install
```

Create a `Rakefile` with the following:
```ruby
spec = Gem::Specification.find_by_name 'wax_tasks'
Dir.glob("#{spec.gem_dir}/lib/tasks/*.rake").each {|r| load r}
```

## Running the Tasks

After following the installation instructions above, you will have access to the rake tasks in your shell by running `$ bundle exec rake wax:taskname` in the root directory of your Jekyll site.


### wax:pagemaster

Takes a CSV or JSON file of collection metadata and generates a Markdown page for each record to a directory using a specified layout. [Read More](/wax/tasks/pagemaster).

`$ bundle exec rake wax:pagemaster collection-name`

### wax:lunr

Generates a client-side JSON search index of your site for use with [ElasticLunr.js](http://elasticlunr.com/). [Read More](/wax/tasks/lunr).

`$ bundle exec rake wax:lunr`

### wax:iiif

Takes a local directory of images and generates tiles and data that work with a IIIF compliant image viewer like [OpenSeaDragon](https://openseadragon.github.io/), [Mirador](http://projectmirador.org/), or [Leaflet IIIF](https://github.com/mejackreed/Leaflet-IIIF). [Read More](/wax/tasks/iiif).

`$ bundle exec rake wax:iiif collection-name`

### wax:test

Runs [`htmlproofer`](https://github.com/gjtorikian/html-proofer) on your compiled site to look for broken links, HTML errors, and accessibility concerns. Runs [Rspec](http://rspec.info/) tests if a `.rspec` file is present. [Read More](/wax/tasks/test).

`$ bundle exec rake wax:test`


### wax:push

There are two tasks within the namespace `wax:push`: `gh` and `s3`, which push the compiled exhibition site to the `gh-pages` and `s3` branches of your repository respectively for deployment. [Read More](/wax/tasks/push)

`$ bundle exec rake wax:push:gh` and `$ bundle exec rake wax:push:s3`