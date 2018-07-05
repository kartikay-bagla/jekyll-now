---
layout: post
title: Getting Started With Jekyll Now
---

So far, due to the excellent tutorials and documentation provided by Barry Clack, setting up jekyll and getting this website up and running has been a breeze.

The steps I followed so far:
1.  Fork Barry Clark's **Jekyll Now repo** - [located here](https://github.com/barryclark/jekyll-now)
2.  Rename the forked repo to **username.github.io**
3.  Edit the **_config.yml** and wait for a minute or two to let the site go live.
4.  Go to **_posts** and create new posts with the format **year-month-day-title.md**

Now to **build the site locally** i.e. view the changes locally without pushing them to GitHub everytime, you need to set up Jekyll locally, to do that you need to:
1.  [Download and install Ruby](https://rubyinstaller.org/downloads/) (select the **Ruby+Devkit**)
2.  After installation of Ruby, go to **Command Prompt** and type in **gem install github-pages**
3.  Check the installation of Jekyll by typing in **jekyll -v** and you'll get the version if everything went perfectly.

For **viewing the site locally** when adding changes:
1.  Navigate to the directory of your site
2.  Type in **jekyll serve --watch**

And that's a wrap! Now you know how to build a basic GitHub pages Blog.

Also here are the links to the pages that helped me get set up nicely, a huge thanks to all the authors of these pages:
*   [Markdown Cheatsheet by Adam Pritchard](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
*   [Barry Clark's Post at Smashing Magazine](https://www.smashingmagazine.com/2014/08/build-blog-jekyll-github-pages/)