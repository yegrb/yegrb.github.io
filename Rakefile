pages_dir = "_github_pages"

jekyll_render_opts = "--pygments"
jekyll_server_opts = "--server --auto"

directory pages_dir
 
file "#{pages_dir}/.git/config" => pages_dir do
  sh "git clone git@github.com:yegrb/yegrb.github.com.git #{pages_dir}"
end

namespace :github_pages do

  desc "Clone the YEGRB GitHub Pages repo so we can commit the pre-rendered site into it"
  task :setup => "#{pages_dir}/.git/config" do
  end

  desc "Clear away old files from the site. Fresh copies are regenerated to replace them."
  task :purge => :setup do
    # TODO
  end

  desc "Publish this site to GitHub pages"
  task :publish => [:setup, :"jekyll:render"]

end

namespace :jekyll do
  desc "Render the site with Jekyll"
  task :render do
    sh "jekyll #{jekyll_render_opts}"
  end

  desc "Run a local jekyll server, which will automatically regenerate pages as you change them"
  task :server do
    sh "jekyll #{jekyll_render_opts} #{jekyll_server_opts}"
  end
end
