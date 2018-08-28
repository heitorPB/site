# ---------------------------------------
# Rakefile
# ---------------------------------------

# inport module
require "benchmark"
require 'sassc'

# Help
# 
# rake      -> Default to rake help
# rake help -> List all tasks with a description
task :help do
  puts "\n"
  puts "List of all available tasks"
  puts "---------------------------"
  puts "\n"
  system("rake -sT")
  puts "\n"
end

# default to help message
task :default => ["help"]
# END Help

# Install
#
# rake install        -> Default to rake install:global
# rake install:global -> Install gems' dependencies system-wide
# rake install:local  -> Install gems' dependencies in vendor/bundle directory"
namespace 'install' do

  # Install all gems globally (default)
  task :global do
    puts "Installing Jekyll and all dependencies..."
    system("bundle install")
  end
  
  desc "Install gems' dependencies in vendor/bundle directory"
  task :local do
    puts "Installing Jekyll and all dependencies in vendor/bundle directory..."
    system("bundle install --path 'vendor/bundle'")
  end

end

desc "Install all gems globally"
task install: ["install:global"]
# END Install

# Serve
#
# rake serve     -> Run Jekyll in production mode
# rake serve:dev -> Run Jekyll in development mode
namespace 'serve' do

  # Run Jekyll in production mode (default)
  task :prod do
    puts "Run Jekyll in production mode..."
    system("bundle exec jekyll serve --watch --config _config.yml")
  end

  desc "Run Jekyll in development mode"
  task :dev do
    puts "Starting Jekyll in development mode..."
    system("bundle exec jekyll serve --watch --config _config.yml,_config_dev.yml")
  end

end

desc "Run Jekyll in production mode"
task serve: ["serve:prod"]
# END serve

# Sass
#
# rake sass
# rake sass:watch
namespace 'sass' do

  desc "Compile Sass files"
  task :compile do
    puts "Sass"
    puts "Compiling..."
    time = Benchmark.realtime { 
      sass_dir = File.dirname(__FILE__) + "/assets/scss/foundation/"
      sass_input = File.read('./assets/scss/app.scss')
      sass_engine = SassC::Engine.new(
        sass_input,
        {
          :load_paths     => [sass_dir],
          :style          => :compressed,
          :cache          => true,
          :cache_location => './.sass-cache',
          :syntax         => :scss,     
        }
      )
      sass_output = sass_engine.render
      File.open("assets/css/app.min.css", 'w') { |file| file.write(sass_output) }
    }
    puts "             done in #{time.round(4)} seconds."
  end

  task :watch do
    puts "Sass"
    puts "Watching..."
    time = Benchmark.realtime { 
      sass_dir = File.dirname(__FILE__) + "/assets/scss/foundation/"
      sass_input = File.read('./assets/scss/app.scss')
      sass_engine = SassC::Engine.new(
        sass_input,
        {
          :always_update  => true,
          :always_check   => true,
          :load_paths     => [sass_dir],
          :style          => :compressed,
          :cache          => true,
          :cache_location => './.sass-cache',
          :syntax         => :scss,     
        }
      )
      sass_output = sass_engine.render
      File.open("assets/css/app.min.css", 'w') { |file| file.write(sass_output) }
    }
    puts "             done in #{time.round(4)} seconds."
  end

end

# Bug: default task doesn't seems to load sass' path...
desc "Compile Sass files"
task sass: ["sass:compile"]
# END sass

