# Sinatra::ParamChecker

Sinatra::ParamChecker is an extension of Sinatra.
The extension add a before filter for your api to do the param
validation.
It supports many kinds of type checking, like Integer's range,
String's regexp, and delimiter of Array, Hash.


## Installation

Add this line to your application's Gemfile:

```ruby
gem 'sinatra_param_checker'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install sinatra_param_checker

## Usage

``` ruby
require 'sinatra/base'
class Example < Sinatra::Base
  register Sinatra::ParamChecker

  api = '/example'
  params api, methods: [:post] do
    required :name, type: String
    optional :gender, type: Boolean, default: false
  end
  post api do
    name = params[:name]
    gender = params[:gender]
    # Do your logic
    'OK'
  end
end
```

## Supported Options

``` ruby
OPTIONS = [:type, :default, :values, :min, :max, :range, :regexp, :delimiter, :separator]
```

- every param validation should contain a `:type` option.
- `:default` option can only be used with `optional`.
- `:values` cannot be used with `[Array, Hash, File]`.
- `:min, :max` can only be used with `[Integer, Float]`.
- `:range` can only be used with `Integer`.
- `:regexp` can only be used with `String`.
- `:delimiter` can only be used with `[Array, Hash]`.
- `:separator` can only be used with `Hash`.

Supported Types:

- TrueClass, FalseClass, ParamChecker::Boolean
- Integer, Float
- String ,ParamChecker::UUID(32)
- Date, Time, DateTime
- File
- Array, Hash

If you has more demands, ping me by issues or pull requests!


## Development

After checking out the repo, run `bin/setup` to install dependencies. Then, run `rake test` to run the tests. You can also run `bin/console` for an interactive prompt that will allow you to experiment.

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/lerencao/sinatra_param_checker. This project is intended to be a safe, welcoming space for collaboration, and contributors are expected to adhere to the [Contributor Covenant](http://contributor-covenant.org) code of conduct.


## License

The gem is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).

