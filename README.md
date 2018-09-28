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
Exit
```

