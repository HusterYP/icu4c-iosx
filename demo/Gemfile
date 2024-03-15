# frozen_string_literal: true
# Ensure this file is checked in to source control!

# NOTE: to ensure updated gems only use version from byted, not the newest local or official gems, use a clean dir for resolve dependency
# eg: BUNDLE_PATH=.bundle bundle lock
source 'https://rubygems.byted.org'

cocoapods_version = '1.11.2'

if lark_pipeline_worksapce = ENV['LARK_PIPELINE_WORKSPACE']
  require File.realpath(File.expand_path(File.join(lark_pipeline_worksapce, 'scripts/local_gems.rb')))
  LarkPipeline::Rakefile::ComponentManager.instance.components.each do |com|
    gem com.name, path: com.workspace
  end
  begin
    gem 'pry-byebug'
    require 'pry-byebug'
  rescue LoadError
    # optional require
  end
else
  gem 'EEScaffold', '>= 0.1.0.pre'
  gem 'optimus_ios'
  gem 'brickwork'
end
# gem 'lark-project', path: './bin/lib/lark-project'
# if !ENV['WORKFLOW_JOB_ID'].nil?
  ENV['COCOAPODS_SHARED_CACHE'] ||= 'true'
  ENV['COCOAPODS_SHARED_CACHE_UPLOAD'] ||= 'true'
# else
#   ENV['COCOAPODS_SHARED_CACHE'] ||= 'true'
#   ENV['COCOAPODS_SHARED_CACHE_UPLOAD'] ||= 'true'
# end

gem 'cocoapods-byted-dependency-support', '1.0.0.pre.lark.0' # seer publish
gem 'cocoapods-xcremotecache', '100.0.4' 
gem 'cocoapods-monitor'
gem 'seer-hummer-apm', '~> 0.0.17'
gem 'seer-optimize', '>= 1.0.1.alpha', '< 1.1' # pod install ,remove cocoapods-amicable https://bytedance.feishu.cn/docs/doccnFTUeA1JqmFAf5MhTcPwWob#90AEaL

gem "cocoapods-remote-resolve", ENV['BITS_BITNEST_VERSION'] || '>= 0.1.2'

gem 'cocoapods', cocoapods_version
gem 'rake'
gem 'xcov'

gem 'chef-utils', '16.6.14'
gem 'ffi', '1.14.0'
gem 'json', '2.3.1'
gem 'xcpretty', '0.3.1.1' 

plugins_path = File.join(File.dirname(__FILE__), 'fastlane', 'Pluginfile')
eval_gemfile(plugins_path) if File.exist?(plugins_path)

ENV['CP_CACHE_DIR'] = File.join(Dir.home, 'Library/Caches/CocoaPods', cocoapods_version)
