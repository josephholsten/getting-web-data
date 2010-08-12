!SLIDE
# Standard Lib #

!SLIDE
    @@@ Ruby
    require 'openuri'
    open('http://user:pass@flickr.com/')

!SLIDE full-page
![cute seal](cute_seal.jpg)

!SLIDE
    @@@ Ruby
    require 'net/http'
    require 'uri'

    url = URI.parse('http://example.com/todo')
    req = Net::HTTP::Post.new(url.path)
    req.basic_auth 'jack', 'pass'
    params = {
      'from'=>'2005-01-01',
      'to'=>'2005-03-31'
    }
    req.set_form_data(params, ';')
    client = Net::HTTP.new(url.host, url.port)
    res = client.start do |http|
      http.request(req)
    end

!SLIDE full-page
![club seal](club_seal.jpg)