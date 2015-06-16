# task :default => [:hello]
task :default => [:setup_and_run]

# task :hello do
#   puts "hello world"
# end


class Bundle

  class Buildr
    def self.guardfile
      tmpl = gemfile_tmpl

      File.open("Gemfile", "w"){ |f| f.write tmpl } # lol, this is not the final impl...

      # the final impl should have
      #
      # a self.gems method that maps the guardfile gems and does:
      #
      # def self.gem(gem:)
      #   "gem #{name}"
      #
      # appending everything to the gemfile_tmpl

    end

    def self.gemfile_tmpl
      <<-ASD.gsub(/^\s+/, '')
        source "http://rubygems.org"

        gem 'haml'
      ASD
    end
  end

  def self.setup
    app_features = autodetect
    Buildr.guardfile if app_features.include? :guardfile
    # switch ... # when action Build.send action # ...
  end

  def self.autodetect
    type  = []
    type << detect_feature_guardfile
    type << detect_feature_sinatra
    type << detect_feature_roda
    type.compact
  end

  def self.detect_feature_guardfile
    :guardfile if File.exists? "Guardfile"
  end

  def self.detect_feature_sinatra
    :sinatra # if  gem 'sinatra' in Gemfile
  end

  def self.detect_feature_roda
    :roda    # if  gem 'roda'    in Gemfile
  end

  #

  def self.install
    puts `bundle install`
  end
end

class Task
  def self.run
    popen_read "python -m SimpleHTTPServer 3001"
  end

  def self.setup
    Bundle.setup
    Bundle.install
  end

  # private

  def self.popen_read(cmd)
    IO.popen cmd, 'r+' do |f|
      puts f.gets
    end
  end
end

task(:run)   { Task.run   }
task(:setup) { Task.setup }


task :setup_and_run do
  Task.setup
  Task.run
end