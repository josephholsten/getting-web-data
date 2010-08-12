!SLIDE
# services #

!SLIDE full-page
![rest seal](rest_seal.jpg)

!SLIDE
# restclient #

!SLIDE
    @@@ Ruby
    require 'rest_client'

    RestClient.get 'http://localhost:4567/posts'

!SLIDE
    @@@ Ruby
    require 'rest_client'

    RestClient.post 'http://localhost:4567/posts',
        :author => 'Me', :title => 'First Post'

!SLIDE commandline
    $ restclient "http://example.com"
    >> post '/resource', :value => 42
    => "result"

!SLIDE commandline
    $ restclient get "http://host.com/posts" > posts.xml
    $ restclient post "http://host.com/posts" < post.xml
    $ restclient put "http://host.com/posts/1" < post.xml
    $ restclient delete "http://host.com/posts/1"

!SLIDE
    @@@ Ruby
    $ RESTCLIENT_LOG=stdout ./myscript.rb

    RestClient.get "http://example.com/posts"
    # => 200 OK | text/html 3781 bytes

    RestClient.post "http://example.com/posts",
    	"title=First+post"
    # => 200 OK | text/html 40 bytes

!SLIDE small code
    @@@ Ruby
    require 'rest_client'

    client = RestClient::Resource.new("http://example")
    client['/asides'].get
    client['/asides'].post(:body => text)
    client["/asides/1.json"].get
    client["/asides/1"].delete

!SLIDE bullets

# Why Rest Client? #

* urls
* verbs
* headers
* simple

!SLIDE
## http://github.com/archiloque/rest-client ##