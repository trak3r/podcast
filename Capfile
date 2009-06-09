role :site, 'podcast.anachromystic.com'

desc "Push the git repository"
task :push, :roles => :site do
  system "git push"
end

desc "Copy the index.html file to the server."
task :scp, :roles => :site do
  destination = '~/podcast.anachromystic.com'
  upload 'index.html', destination, :via => :scp
  upload 'styles.css', destination, :via => :scp
  upload 'blueprint', destination, :via => :scp, :recursive => true
  upload 'images', destination, :via => :scp, :recursive => true
end

task :deploy do
  push
  scp
end

[ 'scp' ].each do |task| 
  before "#{task}" do 
    set :user, 'teflonted'
  end 
end
