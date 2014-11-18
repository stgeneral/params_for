# ParamsValidator

Use service objects and the power of `ActiveSupport::Validations` to easy validate params in controller.

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'params_validator'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install params_validator

## Usage

In your controller:

```Ruby
# app/controllers/fancy_controller.rb
 
class Fancycontroller < ApplicationController
  include ParamsFor
  
  # Creates a Fancy object by checking and validating params 
  # before that
  #
  def create
    ...
    @fancy = Fancy.new(fancy_params)
    ...
  end
  
  protected
  
  # Strong params delegated to ParamValidator::Fancy
  # and memoized in @fancy_params var returned by this method
  #
  # @return [HashwithIndifferentAccess]
  def fancy_params
    params_for :fancy
  end
end
```

Some place in your application ( suggested `app/validators/params_validator/` )

```Ruby
  # app/validators/param_validator/fancy.rb
 
  class ParamValidator::Fancy < ParamValidator::Base
    attr_accessor :user_id, :fancy_name, :fancy_description
    
    validates :user_id, :fancy_name, presence: true
    validates :user_id, integer: true
  end
```

## Contributing

1. Fork it ( https://github.com/[my-github-username]/params_validator/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request