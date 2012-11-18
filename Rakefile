pages_dir = "_github_pages"
site_dir = "_site"

jekyll_render_opts = "--pygments"
jekyll_server_opts = "--server --auto"

directory pages_dir
 
file "#{pages_dir}/.git/config" => pages_dir do
  sh "git clone git@github.com:yegrb/yegrb.github.com.git #{pages_dir}"
end

namespace :gh do

  desc "Clone the YEGRB GitHub Pages repo so we can commit the pre-rendered site into it"
  task :setup => "#{pages_dir}/.git/config" do
  end

  desc "Clear away old files from the site. Fresh copies are regenerated to replace them."
  task :purge => :setup do
  end

  desc "Copy rendered files ready to publishing"
  task :copy_rendered => [:"jekyll:render", :purge] do
    sh "cp -r #{site_dir}/* #{pages_dir}"
  end

  desc "Commit changes to GitHub pages"
  task :commit_changes => :copy_rendered do
    Dir.chdir(pages_dir) do
      sh "git add ."
      sh 'git commit -m "Automatically published"'
    end
  end

  desc "Publish this site to GitHub pages"
  task :publish => :commit_changes do
    Dir.chdir(pages_dir) do
      sh 'git push origin master'
    end
  end

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
