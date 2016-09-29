source ENV['GEM_SOURCE'] || 'https://rubygems.org'

def location_for(place, fake_version = nil)
  if place =~ /^(git[:@][^#]*)#(.*)/
    [fake_version, { :git => $1, :branch => $2, :require => false }].compact
  elsif place =~ /^file:\/\/(.*)/
    ['>= 0', { :path => File.expand_path($1), :require => false }]
  else
    [place, { :require => false }]
  end
end

group :test do
  gem 'metadata-json-lint'
  gem 'puppet_facts'
  gem 'puppet-blacksmith', '>= 3.4.0'
  gem 'puppetlabs_spec_helper', '>= 1.2.1'
  gem 'rspec-puppet', '>= 2.3.2'
  gem 'rspec-puppet-facts'
  gem 'simplecov'
  gem 'parallel_tests'
  gem 'rubocop', '0.41.2' if RUBY_VERSION < '2.0.0'
  gem 'rubocop' if RUBY_VERSION >= '2.0.0'
  gem 'rubocop-rspec', '~> 1.6' if RUBY_VERSION >= '2.3.0'
  gem 'json_pure', '<= 2.0.1' if RUBY_VERSION < '2.0.0'
  gem 'puppet-lint',                                               :require => false, :git => 'https://github.com/rodjek/puppet-lint.git'
  gem 'puppet-lint-absolute_classname-check',                      :require => false
  gem 'puppet-lint-classes_and_types_beginning_with_digits-check', :require => false
  gem 'puppet-lint-leading_zero-check',                            :require => false
  gem 'puppet-lint-trailing_comma-check',                          :require => false
  gem 'puppet-lint-unquoted_string-check',                         :require => false
  gem 'puppet-lint-variable_contains_upcase',                      :require => false
  gem 'puppet-lint-version_comparison-check',                      :require => false
  gem 'rake',                                                      :require => false
  gem 'rspec',                                                     :require => false
  gem 'rspec-puppet-utils',                                        :require => false
end

group :development do
  gem 'guard-rake',  :require => false
  gem 'travis',      :require => false
  gem 'travis-lint', :require => false
end

group :system_tests do
  gem 'beaker', *location_from_env('BEAKER_VERSION', []) if RUBY_VERSION >= '2.3.0'
  gem 'beaker', *location_from_env('BEAKER_VERSION', ['< 3']) if RUBY_VERSION < '2.3.0'
  gem 'beaker-rspec', *location_from_env('BEAKER_RSPEC_VERSION', ['>= 3.4'])
  gem 'serverspec'
  gem 'beaker-puppet_install_helper'
  gem 'master_manipulator'
  gem 'beaker-hostgenerator', *location_from_env('BEAKER_HOSTGENERATOR_VERSION', [])
end

if facterversion = ENV['FACTER_GEM_VERSION']
  gem 'facter', facterversion.to_s, :require => false, :groups => [:test]
else
  gem 'facter', :require => false, :groups => [:test]
end

ENV['PUPPET_VERSION'].nil? ? puppetversion = '3.8.5' : puppetversion = ENV['PUPPET_VERSION'].to_s
gem 'puppet', puppetversion, :require => false, :groups => [:test]

# vim:ft=ruby
