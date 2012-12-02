require 'rake/clean'
CLEAN.include '*.o', '*.plist', '*.gch'
CLEAN.include 'Mouse'

SRC = FileList['*.c']
OBJ = SRC.ext 'o'

task :default => 'Mouse.o'

rule '.o' => '.c' do |fn|
  sh "clang -o #{fn.name} -c #{fn.source} -Wall -Werror -pedantic"
end

desc 'Build the mouse tests'
file 'MouseTest' => ['MouseTest.o', 'Mouse.o'] do
  sh 'clang -o MouseTest MouseTest.o Mouse.o -framework ApplicationServices'
end

desc 'Run the test for Mouse'
task :test => 'MouseTest' do
  sh './MouseTest'
end

desc 'Run the Clang static analyzer'
task :analyze do
  sh 'clang --analyze Mouse.c'
end

desc 'Startup an IRb console with Mouse loaded'
task :console => [:compile] do
  sh 'irb -Ilib -rmouse'
end

# Gem stuff

require 'rubygems/specification'
MOUSE_SPEC = Gem::Specification.load('mouse.gemspec')

require 'rake/extensiontask'
Rake::ExtensionTask.new('mouse', MOUSE_SPEC)
