require 'rake/clean'
require 'date'
#require 'metric_fu'

CLEAN.include("pkg")
CLEAN.include("doc")


task :default => [:buildgem]

desc "Build the gem without a version change"
task :buildgem => :clean do
  system "gem build viewpoint.gemspec"
end

task :release => :build do
  ver = File.open('VERSION', 'r').readline.chomp
  system "gem push viewpoint-#{ver}"
end

desc "Build the gem, but increment the version first"
task :newrelease => [:versionup, :clean, :repackage]


desc "Increment the version by 1 minor release"
task :versionup do
	ver = up_min_version
	puts "New version: #{ver}"
end


def up_min_version
	f = File.open('VERSION', 'r+')
	ver = f.readline.chomp
	v_arr = ver.split(/\./).map do |v|
		v.to_i
	end
	v_arr[2] += 1
	ver = v_arr.join('.')
	f.rewind
	f.write(ver)
	ver
end

#MetricFu::Configuration.run do |config|
  #define which metrics you want to use
#  config.metrics  = [:churn, :saikuro, :stats, :flog, :flay]
#  config.metrics  = [:flog, :flay]
#  config.graphs   = [:flog, :flay]
#end

