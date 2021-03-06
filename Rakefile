# -*- mode: ruby; coding: utf-8 -*-
require 'rubygems'
require 'bundler'
require 'rake'
require 'rake/clean'
require 'rubygems/package_task'
require 'rdoc/task'
require 'rspec/core'
require 'rspec/core/rake_task'

# Bundler::GemHelper.install_tasks

RSpec::Core::RakeTask.new(:spec) do |spec|
  spec.rspec_opts = ["-c", "-fs"]
  spec.pattern = FileList['spec/lib/**/*_spec.rb']
end

namespace :spec do
  desc "Run RSpec for main procedure"
  RSpec::Core::RakeTask.new(:sysadmin) do |spec|
    spec.rspec_opts = ["-c", "-fs"]
    spec.pattern = FileList['spec/lib/sysadmin/**/*_spec.rb']
  end
end

if RUBY_VERSION >= '1.9.0'
  desc "Run RSpec code examples with simplecov"
  task :simplecov do
    ENV['COVERAGE'] = "on"
    Rake::Task[:spec].invoke
  end
else
  desc "Run RSpec code examples with rcov"
  RSpec::Core::RakeTask.new(:rcov) do |spec|
    spec.pattern = FileList['spec/**/*_spec.rb']
    exclude_files = [
      "gems",
    ]
    spec.rcov_opts = ['--exclude', exclude_files.join(",")]
    spec.rcov = true
  end
end

task :default => :spec

desc 'Generate documentation for the sysadmin.'
RDoc::Task.new do |rdoc|
  rdoc.rdoc_dir = 'rdoc'
  rdoc.title = "sysadmin"
  rdoc.options << '--line-numbers' << '--inline-source'
  rdoc.rdoc_files.include('README*')
  rdoc.rdoc_files.include('lib/**/*.rb')
end

require 'jeweler'
Jeweler::Tasks.new do |gem|
  # gem is a Gem::Specification... see http://docs.rubygems.org/read/chapter/20 for more options
  gem.name = "stdout"
  gem.homepage = "http://github.com/id774/stdout"
  gem.license = "GPL"
  gem.summary = %Q{Stdout}
  gem.description = %Q{Change stdout to array object}
  gem.email = "idnanashi@gmail.com"
  gem.authors = ["id774"]
  # dependencies defined in Gemfile
end
Jeweler::RubygemsDotOrgTasks.new
