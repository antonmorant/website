desc "Build and serve jekyll site for local testing"
task :serve do
  `jekyll serve --baseurl=""`
end

desc "Build jekyll site and copy it to /docs for deploying"
task :deploy do
  `jekyll build`
  `mv docs/CNAME CNAME_tmp`
  `rm -rf docs`
  `cp -r _site docs`
  `mv CNAME_tmp docs/CNAME`
  `git commit docs -m "Copying latest version of the website to docs/ for deploying."`
end
