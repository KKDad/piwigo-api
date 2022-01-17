## Upload a single image

Upload a single image if it doesn't already exist. Image is not associated with any Albums. The image will named apple-pie-bars

```ruby
require 'piwigo/session'
require 'piwigo/images'


session = Piwigo::Session.login('10.100.230.78', 'Adrian', 'mypassword', https: false)
unless session.nil?
  album = Piwigo::Albums::Album.new
  album.name = "Recipes"
  album = Piwigo::Albums.add(session, album)

  filename = 'C:\photos\apple-pie-bars-articleLarge.jpg'
  if Piwigo::Images.lookup(session, filename).nil?
    Piwigo::Images.upload(session, filename, album, 'apple-pie-bars')
  end
end
```

Piwigo will automatically associate the Author of the image as `Adrian` matching the session login id.