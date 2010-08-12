!SLIDE
# parallel #

!SLIDE
![multitasking](multitasking.jpg)

!SLIDE
# typhoeus #

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
    # f = File.open(path, "w")
    requests.each do |r|
      # f << r.handled_response.body
      r.handled_response.body
    end
    # f.close
