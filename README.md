### Legato
---

https://github.com/tpitale/legato
```
access_token = OAuth2 Access Token 

user = Legato::User.new(access_token)

user.accounts
user.accounts.first.profiles

user.profiles

profile = user.profiles.first

profile.user == user # => true

profile.web_property

class Exit
  extend Legato::Model
  
  metrics :exits, :pageviews
  dimensions :page_path, :operating_system, :browser
end
profile.exit # => return a Legato::Query
profile.exit.each {} # => any enumerable kicks off the request to GA

metrics :exits, :pageviews
dimensions :page_path, :operating_system, :browser

filter(:high_exits){gte(:exits, 2000)}
filter :high_exits, &lambda {gte(:exits, 2000)}
filter(:low_pageviews) {lte(:pageviews, 200)}
filter(:for_browser){|browser| matches(:browser, browser)}

filter(:browsers){|| browsers.map {|browser| matches(:browser, browser)}}

Exit.for_browser("Safari", profile)
Exit.results(profile) == profile.exit
profile.exit.high_exits.low_pageviews.by_pageviews
Exit.high_exits(profile).low_pageviews == Exit.low_pageviews(profile).high_exits
filter(:browsers) {|*browsers| browsers.map {|browser| matches(:browser, browser)}}
Exit.browsers("Firefox", "Safari", profile)


eql => '==',
not_eql => '!=',
gt => '>',
gte => '>=',
lt => '<',
lte => '<='

matches => '==',
does_not_match => '!=',
contains => '=~',
does_not_contain => '!~',
substring => '=@',
not_substring => '!@'


segment :high_exits do
  gte(:exits, 2000)
end

segment :low_pageviews do
  lte(:pageviews, 2000)
end

Exit.high_exits.low_pageviews(profile)
profile.exit.high_exits.low_pageviews

Legato::Management::Account.all(user)
Legato::Management::WebProperty.all(user)
Legato::Management::Profile.all(user)
Legato::Management::Goal.all(user)

Eixt.results(profile).realtime

query = Exit.realtime
query.realtime? # => true
query.tracking_scope # => 'rt'

user = Legato::User.new(access_token)
user.quota_user = 'some_unique_identifier'
user.user_ip = ip_address_from_a_web_user_or_something



```

