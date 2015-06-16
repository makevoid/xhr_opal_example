# task :default => [:hello]
task :default => [:setup_and_run]

# task :hello do
#   puts "hello world"
# end

task :run do
  puts `python -m SimpleHTTPServer 3000`
  # puts `rackup`
end

task :setup do
  puts `bundle install`
end

task :setup_and_run do
  setup
  run
end

# task :run