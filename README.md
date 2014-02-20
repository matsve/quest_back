# QuestBack

Simply Ruby client for QuestBack's SOAP API.

### WARNING

This gem is not complete and may lack many functions provided by QuestBack.
Please feel free to contribute and make pull requests.

It is also very simplistic, only using simple hashes for both sending in arguments to the API and returning responses.
Maybe this will change in the future with real objects sent in to the API.




## Installation

Add this line to your application's Gemfile:

    gem 'quest_back'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install quest_back

## Usage

### Get access - test client in console

1. Go to https://response.questback.com/soapdocs/integration/ and request white listing of the IP you will make requests from.
2. Sign in to QuestBack. Go to your account's page and fill in "Integration username and password".
   If you have no fields under Integration Information you have to contact QuestBack to get access.
3. Copy config.example.yml to config.yml and insert your username and password.
4. `QuestBack.conf!` to load config.yml as default config.
5. `QuestBack::Client.new.test_connection` to make a test connection API call. On successful connection this returns string with current namespace of integration library.


### Example of usage

```ruby
# Read quests
api = QuestBack::Api.new
response = api.get_quests
irb(main):005:0> response.results
=> [
    {
      :quest_id=>"4567668",
      :security_lock=>"m0pI8orKJp",
      :quest_title=>"Skalars spørreundersøkelse",
      ...
    },
    {
      ...
    }
  ]


# Add email invitees
response = api.add_email_invitees(
  quest_info: {quest_id: 4567668, security_lock: 'm0pI8orKJp'},
  emails: ['inviso@skalar.no', 'th@skalar.no'],
  sendduplicate: true
)

response.result
=> "Added 2 invitations to QuestId:4567668"
```



## Contributing

1. Fork it ( http://github.com/<my-github-username>/quest_back/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
