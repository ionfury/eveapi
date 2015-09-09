# encoding: utf-8

require 'rubygems'

begin
  require 'bundler/setup'
rescue LoadError => e
  abort e.message
end

require 'rake'

require 'bundler/gem_tasks'

require 'rdoc/task'
RDoc::Task.new
task :doc => :rdoc

require 'rspec/core/rake_task'
RSpec::Core::RakeTask.new

require 'pry'

desc 'Run pry console'
task :console do
  require './lib/eveapi'
  require './lib/eveapi/console'
  Pry.start
end

desc 'Generate method docs'
task :methods do
  Bundler.require
  require 'awesome_print'
  EVEApi::Client.new.working_methods.each do |m|
    p m
    @client = EVEApi::Client.new
    @client.key_id = 2139278
    @client.vcode = "BLG8R4woo0iG9zCnSS6mXzjrjp68DQlQhUbI2TG3J9VBF5Q8XkvNjm4QvrMtEdDJ"
    @client.character_id = 810699209
    out = ""
    begin
      out << @client.api_methods_hash.select { |me| me[:name] == m }.first[:desc]
    rescue
      out << "TODO Description (#{m})"
    end
    out << "\n\n"
    out << "```ruby\n@client = EVEApi::Client.new\n"
    out << "@client.key_id = 4278167\n"
    out << "@client.vcode = '7QJg6p5BZNpDBp2FIz39dGwa7jnN'\n\n"
    out << "@client.#{m}\n\n"
    begin
      out << @client.send(m).pretty_inspect
      out << '```'
      f = File.new("eveapi.wiki/#{m.to_s}.md","w")
      f.puts out
      f.close
    rescue
    end
  end
end


task :c => :console
task :test    => :spec
task :default => :spec
