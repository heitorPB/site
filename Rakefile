# default to help message
task :default => ["help"]

# Show help message
task :help do
  puts "\n"
  puts "List of all available tasks"
  puts "---------------------------"
  puts "\n"
  system("rake -sT")
  puts "\n"
end

# Install dependecies
namespace 'install' do
  

  desc "Install all gems globally"
  task :global do
    puts "Installing Jekyll and all dependencies..."
    system("bundle install")
  end
  
  desc "Install all gems in vendor/bundle directory"
  task :local do
    puts "Installing Jekyll and all dependencies in vendor/bundle directory..."
    system("bundle install --path 'vendor/bundle'")
  end

end

task :install do
  Rake::Task['install:global'].invoke
end

# Choose the mode in which you want to serve Jekyll
namespace 'serve' do

  desc "Run Jekyll in development mode"
  task :dev do
    puts "Starting Jekyll in development mode..."
    system("bundle exec jekyll serve --watch --config _config.yml,_config_dev.yml")
  end
  
  desc "Run Jekyll in production mode"
  task :prod do
    puts "Starting Jekyll in production mode..."
    system("bundle exec jekyll serve --watch --config _config.yml")
  end

end

task :serve do
  Rake::Task['serve:prod'].invoke
end
