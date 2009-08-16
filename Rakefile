require 'rss/itunes'  

desc "Generate the RSS feed"
task :default do
  channel = RSS::Rss::Channel.new  
  category = RSS::ITunesChannelModel::ITunesCategory.new("Technology")  
  channel.itunes_categories << category  

  channel.title = 'Anachromystic Podcast'
  channel.description = 'Two grizzled veterans of the first dot-com bubble discuss technology.'
  channel.link = 'http://podcast.anachromystic.com'
  channel.language = 'en'
  channel.copyright = '2009'
  channel.lastBuildDate = Time.now  

  # below is your "album art"  
  channel.image = RSS::Rss::Channel::Image.new  
  channel.image.url = 'http://podcast.softcraft.ca/anachromystic/audio/logo.jpg'
  channel.image.title = 'Anachromystic Podcast Logo'
  channel.image.link = channel.image.url

  channel.itunes_author = 'Ted Davis'
  channel.itunes_owner = RSS::ITunesChannelModel::ITunesOwner.new  
  channel.itunes_owner.itunes_name = channel.itunes_author
  channel.itunes_owner.itunes_email = 'podcast@anachromystic.com'

  channel.itunes_keywords = %w(technology dot-com java ruby rails iphone linux)  

  channel.itunes_subtitle = 'Technology Triage'
  channel.itunes_summary = channel.description

   # below is what iTunes uses for your "album art", different from RSS standard  
   channel.itunes_image = channel.image.url
   channel.itunes_explicit = 'Explicit'

  # collection.audio_items.each do |r|  
    item = RSS::Rss::Channel::Item.new  
  #   item.title = r.title  
  #   item.link = r.mp3_url  
  #   #~ item.link =  r.image_url  
  #   # item.itunes_keywords = %w(Keywords For This Particular Audio Clip)  
  #   item.guid = RSS::Rss::Channel::Item::Guid.new  
  #   item.guid.content = r.image_url  
  #   item.guid.isPermaLink = true  
  #   item.pubDate = r.pub_date.strftime("%a, %d %b %Y %H:%M:%S %z")  
  #   #        item.pubDate = r.pub_date.rfc822   
  # 
  #   item.description = r.description  
  #   #        item.itunes_summary = "<img src=\""+r.image_url+"\" />"  
  #   # I use guid to save image url instead.  
  #   #        item.itunes_summary = r.image_url  
  #   # item.itunes_subtitle = "audio.nice_title"  
  #   # item.itunes_explicit = '' #r.itunes_explicit  
  #   #item.image = r.image_url  
  #   item.itunes_author = r.author  
  # 
  #   # TODO can add duration once we can compute that somehow  
  # 
  #   item.enclosure = \  
  #   RSS::Rss::Channel::Item::Enclosure.new(item.link, r.mp3_file_size, 'audio/mpeg')  
    channel.items << item  
  # end
    
  feed = RSS::Rss.new("2.0")  
  feed.encoding = 'utf-8'
  feed.channel = channel  
  File.open('episodes.rss', 'w') do |file|
    file.puts feed  
  end
end
          