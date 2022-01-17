## Specify a URL with a port

If you are running Piwigo on a non-standard port in docker, you can specify the port when connecting:

```ruby
require 'piwigo/session'
require 'piwigo/images'


session = Piwigo::Session.login('localhost', 'root', 'piwigo', port: 8083, https: false)
unless session.nil?
  require 'piwigo/session'
  require 'piwigo/albums'

  album = Piwigo::Albums::Album.new
  album.name = "Chippy"
  album = Piwigo::Albums.add(session, album)

  filename = 'C:\Photos\chippy.jpg'
  if Piwigo::Images.lookup(session, filename).nil?
    Piwigo::Images.upload(session, filename, album, 'apple-pie-bars')
  end
end
```

Example output:
~~~
$ ruby main.rb
I, [2022-01-16T20:40:27.437987 #13428]  INFO -- : Login succeeded: {"stat":"ok","result":true}
I, [2022-01-16T20:40:27.471733 #13428]  INFO -- : Status succeeded
I, [2022-01-16T20:40:27.475731 #13428]  INFO -- : Encoding: Chippy - UTF-8
I, [2022-01-16T20:40:27.534389 #13428]  INFO -- : Album Add succeeded: Chippy(1) created.
I, [2022-01-16T20:40:27.589282 #13428]  INFO -- : Image lookup succeeded: {"e49804192ae97cd09460e09fddb8187a"=>nil}
I, [2022-01-16T20:40:27.702908 #13428]  INFO -- : Image AddChunk #0 succeeded: {"stat"=>"ok", "result"=>nil}
I, [2022-01-16T20:40:27.817544 #13428]  INFO -- : Image AddChunk #1 succeeded: {"stat"=>"ok", "result"=>nil}
I, [2022-01-16T20:40:27.901301 #13428]  INFO -- : Image AddChunk #2 succeeded: {"stat"=>"ok", "result"=>nil}
I, [2022-01-16T20:40:27.902947 #13428]  INFO -- : --> GPS: 45.33110277777778, -75.79546111111111
I, [2022-01-16T20:40:27.903224 #13428]  INFO -- : {:date_creation=>"2022-01-16", :categories=>1}
{"stat"=>"ok", "result"=>{"image_id"=>1, "url"=>"http://localhost:8083:8000/picture.php?/1/category/1"}}
I, [2022-01-16T20:40:27.980021 #13428]  INFO -- : Image Add succeeded.

~~~
