# Wink

A Ruby wrapper for the [Wink Hub](http://www.winkapp.com/) [API](http://docs.wink.apiary.io/)

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'wink'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install wink

## Usage

```ruby
Wink.configure do |wink|
  wink.client_id     = ENV['WINK_CLIENT_ID']
  wink.client_secret = ENV['WINK_CLIENT_SECRET']
  wink.access_token  = ENV['WINK_ACCESS_TOKEN']
  wink.refresh_token = ENV['WINK_REFRESH_TOKEN']
end
```

Finding your connected devices:

```ruby
client = Wink::Client.new
client.devices
```

Finding a subset of your devices:

```ruby
client.light_bulbs
client.binary_switches
client.garage_doors
```

Controlling binary switch:

```ruby
light_bulb = client.light_bulbs.find(400)
light_bulb.powered?
light_bulb.off
light_bulb.off? # => true
light_bulb.on
light_bulb.on? # => true
light_bulb.toggle
light_bulb.off? # => true
```

Controlling garage doors:

```ruby
light_bulb = client.light_bulbs.find(400)
light_bulb.position # => 0
light_bulb.open
light_bulb.open?
light_bulb.closed?
light_bulb.close
light_bulb.opening?
```

List subscriptions for each device:

```
light_bulb.subscriptions
```

Create subscription for device:

```ruby
light_bulb.subscriptions.create(:secret => "1", :callback => "http://requestb.in/")
```

Parse incoming subscription payload from Wink API:

```
Wink::Subscription.parse(params[:payload])
```

## Contributing

1. Fork it ( https://github.com/dewski/wink/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request
