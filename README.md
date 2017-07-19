# sincity

Sincity is a bash script that sets up a skeleton development environment for a ruby/sinatra project.

## Usage

Output from ```sincity --help```

```shell
Generates a skeleton directory structure for a Sinatra project
Usage:
sincity -p|--project theprojectname
        -s|--structure microservices|webapp
        -v|--verbose
        -f|--force
        -h|--help
           --version
```

The --verbose, --version, and --help options do what you probably expect them to do.

The --force option will overwrite directory _theprojectname_ if it exists.

Run ```sincity``` from the directory under which you would like the _theprojectname_ directory to be created.

The value of _theprojectname_ is used to generate some filenames and comments.

The default project structure is _microservices_. You can also specify _webapp_ (not implemented yet).

### microservices project

A _microservices_ project structure is simpler than a _webapp_ project structure. It uses the "classic" Sinatra style, with a non-class ruby script as the starting point of the application. The expectation is a _microservices_ app will expose a RESTful API over HTTP.

The project is set up to use git, rack, rackup, bundler, rake, rspec, and cucumber. Various helpful but tedious files are created for you, with (hopefully) useful content. These include some of the usual ancillary things like .gitignore, spec_helper.rb, Rakefile, Gemfile, environent.rb, and so forth.

If everything installs as expected, you should be able to start the app on localhost;9292 with

```shell
rackup
```
Then run

 ```shell
bundle exec cucumber
```

and see two passing scenarios with four passing steps, no failures, and no pending steps.

Cucumber features are set up to verify the default responses from routes that return plain text and JSON; namely,

```shell
http://localhost:9292/
http://localhost:9292/json
```

You can check those routes with cURL from a command-line, as well:

```shell
curl -I http://localhost:9292           displays the returned HTTP headers for the text/html response
curl -s http://localhost:9292           displays the text 'Welcome to Sinatra'
curl -I http://localhost:9292/json      displays the returned HTTP headers for the JSON response
curl -s http://localhost:9292/json      displays a JSON document containing the welcome message
```

You can also run

```shell
bundle exec rake
```

but the _microservices_ setup doesn't include any rspec specs, so you'll see "0 examples, 0 failures." It's still useful to run this because it will complain if anything wasn't installed correctly.

### webapp project

The _webapp_ project setup assumes you want a model-2 (quasi-MVC) architecture with separate folders for controllers, views, and models and with ActiveRecord support. It sets up a "modular" Sinatra app and generates just enough of a database and ruby files to verify the configuration is as expected.
