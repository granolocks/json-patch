# JSON::Patch
[![Build Status](https://travis-ci.org/guillec/json-patch.png)](https://travis-ci.org/guillec/json-patch)
[![Code Climate](https://codeclimate.com/github/guillec/json-patch.png)](https://codeclimate.com/github/guillec/json-patch)
[![Coverage Status](https://coveralls.io/repos/guillec/json-patch/badge.png)](https://coveralls.io/r/guillec/json-patch)

Inspired by: 
- Steve Klabnik: https://github.com/steveklabnik/json-merge_patch
- Tenderlove: https://github.com/tenderlove/hana

This gem augments Ruby's built-in JSON library to support JSON Patch
(identified by the json-patch+json media type). http://tools.ietf.org/html/rfc6902

## Installation

Add this line to your application's Gemfile:

    gem 'json-patch'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install json-patch

## Usage

Then, use it:

```ruby
# The example from http://tools.ietf.org/html/rfc6902#appendix-A

# Add Object Member
target_document = <<-JSON
  { "foo": "bar"}
JSON

operations_document = <<-JSON
[
  { "op": "add", "path": "/baz", "value": "qux" }
]
JSON

JSON.patch(target_document, operations_document)
# => 
{ "baz": "qux", "foo": "bar" }


# Add Array Element
target_document = <<-JSON
  { "foo": [ "bar", "baz" ] }
JSON

operations_document = <<-JSON
[
  { "op": "add", "path": "/foo/1", "value": "qux" }
]
JSON

JSON.patch(target_document, operations_document)
# => 
{ "foo": [ "bar", "qux", "baz" ] }
```

If you'd prefer to operate on pure Ruby objects rather than JSON
strings, you can construct a JSON::Patch object instead.

```ruby
target_document = { "foo" => [ "bar", "baz" ] }
operations_document = [{ "op" => "add", "path" => "/foo/1", "value" => "qux" }]

JSON::Patch.new(target_document, operations_document).call
# => 
{ "foo" => [ "bar", "qux", "baz" ] }
```


## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
