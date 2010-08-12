!SLIDE
# parallel #

!SLIDE full-page
![multitasking](multitasking.jpg)

!SLIDE
# typhoeus #

!SLIDE code small
    @@@ ruby
    require 'typhoeus'

    Typhoeus::Request.get "http://example.com/posts"

!SLIDE code
    @@@ ruby
    require 'typhoeus'

    url = "http://example.com/posts"
    request = Typhoeus::Request.new(url)

    # only makes the request when
    # we ask for the response
    puts request.response.body

!SLIDE code small
    @@@ ruby
    require 'typhoeus'
    require 'json'

    request = Typhoeus::Request.new(
      "http://example.com/posts",
      :body          => "this is a request body",
      :method        => :post,
      :headers       => {:Accepts => "text/html"},
      :timeout       => 100, # milliseconds
      :cache_timeout => 60, # seconds
      :params        => {:title => "first post"})

    resp = request.response
    puts "got #{resp.code} in #{resp.time}"
    puts response.headers.inspect
    puts response.body

!SLIDE
.notes BTW: if you're accessing your own service with any of these, stop. HTTP has a ton of overhead and you'd likely be better served with either more granular requests (batched index, patch method) or a lower-overhead encapsulation protocol


    @@@ Ruby
    hydra = Typhoeus::Hydra.new
    requests = urls.map do |url|
      t = Typhoeus::Request.new(url)
      hydra.queue(t)
      t
    end
    hydra.disable_memoization
    hydra.run # this is a blocking call
    
    # we can handle them once the
    # entire queue has returned
    requests.each do |r|
      r.handled_response.body
    end

!SLIDE bullets

# Why Typhoeus? #

* can't switch off http
* ntlm auth
* parallel
* lazy
* caching
* memoization

!SLIDE
## http://github.com/pauldix/typhoeus ##