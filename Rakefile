# Adapted from Scott Kyle's Rakefile
# http://github.com/appden/appden.github.com/blob/master/Rakefile

def jekyll(opts = "", path = "~/dev/jekyll/bin/")
  sh "rm -Rf _site/*"
  sh path + "jekyll " + opts
end
 
desc "Build site using Jekyll"
task :build do
  jekyll
end
 
desc "Serve at localhost:4000"
task :default do
  jekyll("--server --auto")
end

desc "Serve at localhost:4000 sans autogeneration"
task :hack do
  jekyll("--server")
end
 
desc "Deploy to dev"
task :deploy => :"deploy:dev"
 
namespace :deploy do
  desc "Deploy to dev"
  task :dev => :build do
    rsync "/Library/WebServer/www/AndrewHeiss/jekyll/"
  end
  
  desc "Deploy to live"
  task :live => :build do
    rsync "appden.com" # Fix this. This is the wrong live server.
  end
  
  desc "Deploy to dev and live"
  task :all => [:dev, :live]
  
  def rsync(location)
    sh "rsync -rtz --delete _site/ #{location}"
  end
end