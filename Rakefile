require "json"
namespace :vendor do
  desc "copy to vendor/assets/javascripts from bower, npm managed assets"
  task :install do
    vendor = JSON.load(open("vendor.json"))
    javascripts = vendor["javascripts"]
    stylesheets = vendor["stylesheets"]

    javascripts.each do |name, src|
      src_path = expand_bower_npm src
      cp src_path, "vendor/assets/javascripts/#{name}.js"
    end

    stylesheets.each do |_name, src|
      src_path = expand_bower_npm src
      map_path = "#{src_path}.map"
      cp src_path, "vendor/assets/stylesheets/"
      cp map_path, "vendor/assets/stylesheets/" if File.exist? map_path
    end

    # puts help message
    puts_message "Add below to app/assets/javascripts/application.js"
    javascripts.keys.each { |name| puts "//=require #{name}" }
    puts_message "Add below to app/assets/stylesheets/application.css"
    stylesheets.keys.each { |name| puts "*=require #{name}" }
    puts_message "or import in the sass"
    stylesheets.keys.each { |name| puts "@import \"#{name}\";" }
  end

  def puts_message(message)
    puts
    puts "============================================================"
    puts message
    puts "============================================================"
  end

  # Add node_modules or bower_components to the path
  def expand_bower_npm(path)
    bower_path = "bower_components/#{path}"
    npm_path = "node_modules/#{path}"
    if File.exist?(bower_path) && File.exist?(npm_path)
      fail "#{path} exists in both node and bower, don't do that"
    elsif File.exist?(npm_path)
      npm_path
    elsif File.exist?(bower_path)
      bower_path
    else
      fail "#{path} does not exit in both #{npm_path} and #{bower_path}"
    end
  end
end
