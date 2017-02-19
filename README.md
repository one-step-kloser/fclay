# Fclay

Welcome to your new gem! In this directory, you'll find the files you need to be able to package up your Ruby library into a gem. Put your Ruby code in the file `lib/fclay`. To experiment with that code, run `bin/console` for an interactive prompt.

TODO: Delete this and the text above, and describe your gem

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'fclay'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install fclay

## Usage

Create migration for model:

    $ rails g fclay User

Add `has_fclay_attachment` to model file:

```ruby
class User < ActiveRecord::Base
  has_fclay_attachment without: [:process, :upload, :delete], content_type: "application/json", extension: 'png', styles: [:thumb,:original]
end
```

Now `User` model has `file_url` method

```ruby
  User.last.file_url
```

## Configuration

Configuring with `config\initializers\fclay.rb`:

```ruby
  
  require 'fclay'
  Fclay.configure do |config|
    config.local_storage_host = "http://mysite.com"
    config.storage_policy = "s3"
    config.remote_storages = {
      "s3" => {
        kind: 'aws',
        storage_policy: "storage_policy_name",
      }
    }
  end
```



## Development

After checking out the repo, run `bin/setup` to install dependencies. Then, run `rake spec` to run the tests. You can also run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release`, which will create a git tag for the version, push git commits and tags, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/[USERNAME]/fclay.


## License

The gem is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).

