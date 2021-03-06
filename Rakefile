# encoding: UTF-8
# -*- mode: ruby -*-
# vi: set ft=ruby :

require 'bundler/setup'

namespace :style do
  require 'rubocop/rake_task'
  desc 'Run Ruby style checks'
  RuboCop::RakeTask.new(:ruby)

  require 'foodcritic'
  desc 'Run Chef style checks'
  FoodCritic::Rake::LintTask.new(:chef)
end

desc 'Run all style checks'
task style: %w(style:chef style:ruby)

task :unit do
  sh "bundle exec 'rspec ./test/unit/spec/ --color --format documentation'"
end

desc 'Run Test Kitchen integration tests'
task :integration do
  require 'kitchen'
  Kitchen.logger = Kitchen.default_file_logger
  Kitchen::Config.new.instances.each do |instance|
    instance.test(:always)
  end
end

desc 'Run all tests'
task test: %w(style unit integration)

desc 'Tasks to run on Travis CI'
namespace :travis do
  desc 'Run tests on Travis'
  task ci: %w(style)
end

task default: %w(style unit integration)
