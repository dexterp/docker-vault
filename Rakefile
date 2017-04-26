require 'dotenv'
require 'rake'

ROOT = File.dirname(File.expand_path(__FILE__))
VERSION = File.read(File.join(ROOT, 'VERSION')).chomp
IMAGE = File.read(File.join(ROOT, 'IMAGE')).chomp

Dotenv.load File.join(ROOT, '.env')
PUSH = ENV.fetch('PUSH', 'false').to_s.downcase.eql? 'true'
REGESTRY = ENV.fetch('REGESTRY', '')


desc 'Build'
task :build do
  sh "docker build . -t #{IMAGE}:#{VERSION}-snapshot"
end

desc 'Release - Tag/push docker image. Git tag/push source'
task :release do
  sh "docker tag #{IMAGE}:#{VERSION}-snapshot #{REGESTRY}#{IMAGE}:#{VERSION}"
  sh "docker push #{REGESTRY}#{IMAGE}:#{VERSION}" if PUSH
  sh "git tag #{VERSION}"
  sh "git push --tags" if PUSH
end
