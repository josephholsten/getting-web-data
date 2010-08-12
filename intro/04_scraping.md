!SLIDE
# scraping #

!SLIDE
# mechanize #

!SLIDE
![paro](paro_seal.jpg)

!SLIDE
    @@@ Ruby
    require 'mechanize'

    page = Mechanize.new.get('http://google.com/')
    page.links # all the links in the page
    page.forms # all the forms

!SLIDE
    @@@ Ruby
    require 'mechanize'

    a = Mechanize.new do |agent|
      agent.user_agent_alias = 'Mac Safari'
    end

    a.get('http://google.com/') do |page|
      form = page.form_with(:name => 'f') do |f|
        f.q = 'Hello world'
      end
      search = form.submit

      search.links.each do |link|
        puts link.text
      end
    end

!SLIDE
    @@@ Ruby
    require 'mechanize'
    agent = WWW::Mechanize.new
    agent.get('http://http_clients.tadalist.com/session/new')
    agent.page
    form = agent.page.forms.first
    form.password = 'secret'
    form.sumbit
    # now logged in
    agent.page.link_with(:text => 'Wish List').click

    # now on wish list page
    agent.page.search('.edit_item').map(&:text).map(&:strip)

!SLIDE
## SSL support
## back button
## Proxies
## file uploading
## cookies
## sessions


!SLIDE
## http://mechanize.rubyforge.org ##