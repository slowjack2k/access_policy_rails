# AccessPolicyRails 

Rails extension for AccessPolicy. Stores the policy_check_user (default current_user)
in a RequestLocalStorage. So it is not needed to pass the user around.

Further more some macros are provided to query permissions and protect actions.

## Installation

Add this line to your application's Gemfile:

    gem 'access_policy_rails'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install access_policy_rails

## Usage

```ruby

  class DummyController < ActionController::Base
    attr_accessor :current_user

    guarded_action :create do

    end

    guarded_action :show do

    end
  end


  DummyControllerPolicy = Struct.new(:current_user, :controller) do
      def create?
        !! (current_user && current_user.create_allowed?)
      end

      def show?
        !! (current_user && current_user.show_allowed?)
      end
   end

  # Query permissions in controller or view

  policy_for(an_object).allow?(:create)

```



## Contributing

1. Fork it ( http://github.com/slowjack2k/access_policy_rails/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
