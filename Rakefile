KEYWORDS = %w(technology dot-com java ruby rails iphone linux)

def url_for(suffix)
  require 'cgi'
  "http://podcast.softcraft.ca/anachromystic/audio/#{CGI.escape(suffix).gsub('+','%20')}"
end

desc "Generate the RSS feed"
task :default do
  require 'rss/itunes'
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
  channel.image.url = url_for('logo.jpg')
  channel.image.title = 'Anachromystic Podcast Logo'
  channel.image.link = channel.link

  channel.itunes_author = 'Ted Davis'
  channel.itunes_owner = RSS::ITunesChannelModel::ITunesOwner.new
  channel.itunes_owner.itunes_name = channel.itunes_author
  channel.itunes_owner.itunes_email = 'podcast@anachromystic.com'

  channel.itunes_keywords = KEYWORDS

  channel.itunes_subtitle = channel.description
  channel.itunes_summary = channel.description

  # below is what iTunes uses for your "album art", different from RSS standard
  channel.itunes_image = RSS::ITunesChannelModel::ITunesImage.new(channel.image.url)
  # channel.itunes_image.href = channel.link
  channel.itunes_explicit = 'Yes'

  episodes = YAML.load(File.open('episodes.yml'))
  episodes.keys.each do |episode_key|
    episode = episodes[episode_key]
    item = RSS::Rss::Channel::Item.new
    item.title = episode['title']
    item.link = url_for(episode['media_url'])
    item.itunes_keywords = KEYWORDS
    item.guid = RSS::Rss::Channel::Item::Guid.new # is this used!?
    item.guid.content = episode['image_url']
    item.guid.isPermaLink = true
    puts episode.inspect
    item.pubDate = Date.parse(episode['pub_date']).strftime("%a, %d %b %Y %H:%M:%S %z")
    item.description = episode['description']
    #        item.itunes_summary = "<img src=\""+episode['image_url+"\" />"
    # I use guid to save image url instead.
    #        item.itunes_summary = episode['image_url
    # item.itunes_subtitle = "audio.nice_title"
    # item.itunes_explicit = '' #episode['itunes_explicit
    #item.image = episode['image_url
    item.itunes_author = channel.itunes_author
    item.enclosure = RSS::Rss::Channel::Item::Enclosure.new(
              item.link, 
              episode['media_file_size'].to_f * 1024.0 * 1024.0, 
              'audio/mpeg')
    channel.items << item
  end

  feed = RSS::Rss.new("2.0")
  feed.encoding = 'utf-8'
  feed.channel = channel
  # puts feed.to_s
  File.open('episodes.rss', 'w') do |file|
    file.puts feed.to_s
  end
end
          