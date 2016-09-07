#!/usr/bin/env ruby

# Invisible Tasks

objects = Rake::FileList.new "titan-*.markdown", "titan-*.md"
rule ".7" => ".markdown" do |t|
  sh "pandoc -s -t man #{t.source} -o #{t.name}"
end

task :copy => objects.ext(".7") do |t|
  sh "cp #{t.source} /usr/local/share/man/man7/#{t.source}"
end

# Visible Tasks

desc "Overwrite benner.net. Sudo required"
task :banner do
  sh "cp banner.net /usr/local/banner.net"
end

desc "Install generated manfile in /usr/local/man directory. Sudo required."
task :install => [:copy, :banner] do
  sh "mandb"
end

desc "Compile manfile from markdown. Check with: man -l FILE"
task :default => objects.ext(".7")
