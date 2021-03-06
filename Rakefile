require './lib/rubycheck'

task :default => 'test'

task :test => ['spec/'] do
  sh 'rspec'
end

task :gem => [:clean, 'rubycheck.gemspec'] do
  sh 'gem build *.gemspec'
  sh "gem install ./*.gem"
end

task :publish => [:gem] do
  sh "gem push ./*.gem"
end

task :ruby => [] do
  begin
    sh 'for f in **/*.rb; do ruby -wc $f 2>&1 | grep -v "Syntax OK" | grep -v openssl | grep -v rubygems; done'
  rescue
  end
end

task :reek => [] do
  sh 'bundle exec reek -q .; true'
end

task :flay => [] do
  sh 'bundle exec flay .'
end

task :roodi => [] do
  sh 'bundle exec roodi -config=roodi.yml *.rb **/*.rb'
end

task :cane => [] do
  sh 'bundle exec cane -f *.rb; bundle exec cane **/*.rb'
end

task :excellent => [] do
  sh 'bundle exec excellent .'
end

task :rubocop => [] do
  sh 'bundle exec rubocop **/*.rb **/*.erb **/Guardfile*'
end

task :tailor => [] do
  sh 'bundle exec tailor'
end

task :lili => [] do
  sh 'bundle exec lili .'
end

task :editorconfig=> [] do
  sh 'find . -type f -name Thumbs.db -prune -o -type f -name .DS_Store -prune -o -type d -name .git -prune -o -type d -name .svn -prune -o -type d -name tmp -prune -o -type d -name bin -prune -o -type d -name target -prune -o -name "*.app*" -prune -o -type d -name node_modules -prune -o -type d -name bower_components -prune -o -type f -name "*[-.]min.js" -prune -o -type d -name "*.dSYM" -prune -o -type f -name "*.scpt" -prune -o -type d -name "*.xcodeproj" -prune -o -type d -name .vagrant -prune -o -type f -name .exe -prune -o -type f -name "*.o" -prune -o -type f -name "*.pyc" -prune -o -type f -name "*.hi" -prune -o -type f -name "*.beam" -prune -o -type f -name "*.png" -prune -o -type f -name "*.gif" -prune -o -type f -name "*.jp*g" -prune -o -type f -name "*.ico" -prune -o -type f -name "*.ttf" -prune -o -type f -name "*.zip" -prune -o -type f -name "*.jar" -prune -o -type f -name "*.dot" -prune -o -type f -name "*.pdf" -prune -o -type f -name "*.wav" -prune -o -type f -name "*.mp[34]" -prune -o -type f -name "*.svg" -prune -o -type f -name "*.flip" -prune -o -type f -name "*.class" -prune -o -type f -name "*.jad" -prune -o -type d -name .idea -prune -o -type f -name "*.iml" -prune -o -type f -name "*.log" -prune -o -type f -name "*" -exec node_modules/.bin/editorconfig-tools check {} \\;'
end

task :lint => [
  :ruby,
  :reek,
  :flay,
  :roodi,
  :cane,
  :excellent,
  :rubocop,
  :tailor,
  :lili,
  :editorconfig
] do
end

task :flog => [] do
  sh 'bundle exec flog .'
end

task :churn => [] do
  sh 'bundle exec churn'
end

task :clean => [] do
  begin
    sh 'rm *.gem'
  rescue
  end

  begin
    sh 'rm -rf tmp'
  rescue
  end

  begin
    sh 'rm -rf doc/'
  rescue
  end
end

task :doc => [:clean] do
  sh 'rdoc lib/'
end
