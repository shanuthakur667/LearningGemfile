## Welcome 
Let's have a look about some basic understanding of gemfile and gems 
### 1> source
Its a global source. we can use multiple flobal source. If gem found in multiple souce, then bundler will print warning message (after intsalling the gem) to tell from which souce , gem get install and also listing the other source available.
### 2> Ruby
Use option paremeter
- Version
  The version ruby your application requres
  eg - ruby '2.5.5'
- Engine and Engine Version
  Engine is implementaion of ruby language in app, MRI( Matz's Ruby Interpreter) is commonly used engine(also known as cruby as it written in c laguage).
  other engine example is Rubinius, and JRuby
  NOTE- if engine is specifed then engine version should also be specifed and vice versa
  eg - ruby "1.8.7", :engine => "jruby", :engine_version => "1.6.7"
- Patchlevel
  Ruby patchlevel.
  eg - ruby "2.0.0", :patchlevel => "247"
  
### 3> Gems
Optional Paremeter
- Version
  If you don’t set a gem version, bundler will set it for you. You can avoide it by usings operators (=, !=, >, <, >=, <=, ~> i.e Pessimistically Greater Than or Equal To)
  NOTE- ~> ensures app will work safly with future version
  gem 'gem_name', '~> 1.0' is the same as: gem 'gem_name', '>= 1.0', '< 2.0'
- Require
  gem 'gem_name', require: false
  You can prevent bundler from requiring the gem with require: false, but it will still install and maintain the gem. You need to call requre 'gem_name' in file where you use that gem explicitly.
  These three line are same in functioning
  gem "nokogiri"
  gem "nokogiri", :require => "nokogiri"
  gem "nokogiri", :require => true
- Source
  gem 'gem_name', source: 'https://gem_site.com'
  You can add source of gem so it will override global source for that specific gem, it can be a git or system path as well

### 4> Gem grouping
  Gem can belongs to one or more group
  By default if there is no group assign then it will belongs to 'Default' group.
  eg -  group :development, :test do
          gem 'gem_name'
          gem 'gem_another_name'
        end
  You can install gem without specifically excluding a group by-
  bundle install --without development test

-> Bundler stores the flag in APP_ROOT/.bundle/config, see setting of bundler by running 'bundle config'
  By default, a Rails generated app calls Bundler.require(:default, Rails.env) in your application.rb
  You can leave groups of gems out of Bundler.require and then require them manually using Ruby's require(require 'gem_name') at the appropriate place in your app. You might do this because requiring a certain gem takes some time and you don't need it every time you boot your application.

