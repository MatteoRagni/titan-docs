#!/usr/bin/env ruby

objects = Rake::FileList.new "*.markdown", "*.md"

#task :object => objects.ext(".1")
rule ".1" => ".markdown" do |t|
  sh "pandoc -s -t man #{t.source} -o #{t.name}"
end

task :copy => objects.ext(".1") do |t|
  puts "cp #{t.source} /usr/local/share/man/man1/#{t.source}"
  sh "cp #{t.source} /usr/local/share/man/man1/#{t.source}"
end

desc "Install generated manfile in /usr/local/man directory"
task :install => :copy do
  sh "mand"
end

desc "Compile manfile from markdown. Check with: man -l FILE"
task :default => :man
