!SLIDE
# scraping #

!SLIDE full-page
![paro](paro_seal.jpg)

!SLIDE
# mechanize #

!SLIDE
.notes just get a page
    @@@ Ruby
    require 'mechanize'

    page = Mechanize.new.get 'http://google.com/'
    page.links # all the links in the page
    page.forms # all the forms

!SLIDE
.notes fill out a form
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
.notes follow links
    @@@ Ruby
    require 'mechanize'
    agent = Mechanize.new
    agent.get('http://http_clients.tadalist.com/session/new')
    agent.page
    form = agent.page.forms.first
    form.password = 'secret'
    form.sumbit
    
    # now logged in
    agent.page.link_with(
      :text => 'Wish List').click

    # now on wish list page
    items = agent.page.search('.edit_item')
    puts items.map(&:text).map(&:strip)

!SLIDE code smaller
.notes upload files
    @@@ ruby
    a = Mechanize.new
    a.get('http://flickr.com/') do |home_page|
      # click sign in at the home page
      signin_page = a.click(home_page.link_with(
        :text => /Sign In/))

      # fill and submit the sign in page
      page = signin_page.form_with(
        :name => 'login_form') do |form|
          form.login  = 'josephholsten'
          form.passwd = 'secret'
      end.submit

      # Click the upload link
      page = a.click(page.link_with(
        :text => /Upload/))

      # We want the basic upload page
      page = a.click(upload_page.link_with(
        :text => /basic Uploader/))

      # Upload the file
      page.form_with(:method => 'POST') do |form|
        form.file_uploads.first.file_name = 'cute_seal.jpg'
      end.submit
    end

!SLIDE
    @@@ ruby
    require 'mechanize'

    agent = Mechanize.new
    agent.set_proxy('localhost', '8000')
    page = agent.get(ARGV[0])
    puts page.body

!SLIDE bullets

# Why Mechanize? #

* links, forms & redirects
* store & send cookies
* proxies
* digest auth
* tls client certs

!SLIDE
## http://mechanize.rubyforge.org ##