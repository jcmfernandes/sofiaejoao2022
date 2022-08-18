require "bundler/setup"
require "rubygems"

require "tmpdir"
require "fileutils"
require "jekyll"

GITHUB_REPONAME = "jcmfernandes/sofiaejoao2022"

desc "Generate site files"
task :generate do
  FileUtils.rm_rf('_site/')
  Jekyll::Site.new(Jekyll.configuration("config" => "_config.yml")).process
end


desc "Generate and publish site to gh-pages"
task :publish => [:generate] do
  Dir.mktmpdir do |tmp|
    cp_r "_site/.", tmp

    old_pwd = Dir.pwd
    Dir.chdir(tmp)

    system "git init"
    system "git checkout -b site"
    system "git add ."
    system "git commit -m 'Site updated at #{Time.now.utc}'"
    system "git remote add origin git@github.com:#{GITHUB_REPONAME}.git"
    system "git push origin site --force"

    Dir.chdir(old_pwd)

    FileUtils.rm_rf('_site/')
  end
end
