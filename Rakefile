task :default => [:server]

task :generate do
    system "jekyll"
end

task :server do
    system "jekyll --server --auto"
end

task :deploy => [:generate] do
    sh "rsync -av --rsh='ssh -p 22' _site/ root@192.168.1.121:/var/www/"
end

task :deploy_to_test => [:generate] do
    sh "rsync -av --rsh='ssh -p 22' _site/ root@192.168.1.121:var/www/"
end

desc 'Begin a new post'
task :post do
  ROOT_DIR = File.dirname(__FILE__)

  title = ARGV[1]
  tags = ARGV[2 ]

  unless title
    puts %{Usage: rake post "The Post Title"}
    exit(-1)
  end

  datetime = Time.now.strftime('%Y-%m-%d')  # 30 minutes from now.
  slug = title.strip.downcase.gsub(/ /, '-')

  # E.g. 2006-07-16_11-41-batch-open-urls-from-clipboard.markdown
  path = "#{ROOT_DIR}/_posts/#{datetime}-#{slug}.markdown"

  header = <<-END
---
layout: post
title: #{title}
description:
categories:
---

END

  File.open(path, 'w') {|f| f << header }
  system("mate", path)
end

task :default => :server

def jekyll(opts = '')
  sh 'time jekyll ' + opts
end
