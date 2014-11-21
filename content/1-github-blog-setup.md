Title: Github Blog Setup
Date: 2014-11-20 22:09
Category: Python
Tags: blog, python
Slug: github-blog-setup
Author: chtangwin
Summary: github is super cool.
comments: true


Now I have decided to use github + pelican for personal blog. The plan is to 
integrate with ipython notebook so all the math and stats notes can be displayed 
easily. 

Setup Steps
-----------

1. Follow the instructions from [How to setup Github User Page with Pelican](http://ntanjerome.org/blog/how-to-setup-github-user-page-with-pelican/), up to
the point where first post is done and local devserver is up. The only difference
is that I am using main branch ("master") for all edits. The other **very good** references are:
    
    - [Migrating to GitHub Pages using Pelican](http://mathamy.com/migrating-to-github-pages-using-pelican.html)
    
    - [Createing your blog with Pelican](http://chdoig.github.io/create-pelican-blog.html)
    
    In fact, they use pretty themes. I plan to read through carefully later
    and see if can use some of their settings.
    
2. For now, use the same theme as in [python4oceanographers](http://nbviewer.ipython.org/url/ocefpaf.github.com/python4oceanographers/downloads/notebooks/2013-12-23-blogging.ipynb), mainly download *theme* and *plugin* from github, then edit *pelicanconf.py* and *publishconf.py* scripts.

        :::bash
        $ git clone https://github.com/jakevdp/pelican-octopress-theme.git
        $ git clone https://github.com/getpelican/pelican-plugins.git

3. Write markdown files in `conten` folder, then run `make devserver` to generate HTML 
for the site, and serves is up locally at [http://localhost:8000](http://localhost:8000).
Note that `make devserver` will also automatically regenerate the whole site, i.e. run `pelican` on `content` every time one save a change to a content, configuration, or theme file. Just refresh the page in your browser, and you should immediately see the changes. To shutdown the webserver, use `make stopserver`.

4. Now we have two repos, one is for `blog-source`, the other is actual site under `output` directory. See [Posting to GitHub](http://mathamy.com/migrating-to-github-pages-using-pelican.html) 
for how to publish to username.github.io site. In short summary, use the following commands:

        :::bash
        $ cd blog
        $ pelican content   # or "make html"
        $ cd output
        $ git add --all
        $ git commit -m "commit message"
        $ git push origin master

5. The disadvantage of previous step is that two checkins are needed for update, one
for `blog-source`, the other for actual site. One can use *git hooks* to push changes
to both repos at the same time, as shown 
[here](http://mavant.com/blog/2014/03/10/pelican-git-hooks-github-dot-io/).
Now one can do the following:

        :::bash
        $ vim content/your-message.md
        $ git commit -am "commit message"
        $ git push origin master

        
Workflow
--------
I use `conda` to manage virtualenv. The normal workflow is going to be like below:

    :::bash
    $ activate myblog
    $ vim content/blog-post-file.md  # add/edit entries
    $ ... # test locally till all is good
    $ git commit -am "commit message"
    $ git push origin master
    $ deactivate myblog # or just exit once all done

As to ipython notebook integration and how to use markdown, the blog post from Jake
[Migrating from Octopress to Pelican](https://jakevdp.github.io/blog/2013/05/07/migrating-from-octopress-to-pelican/)
gives very detailed instructions. Check it out.

Resources
---------
1. [Creating your blog with Pelican](http://chdoig.github.io/create-pelican-blog.html)
2. [Migrating to GitHub Pages using Pelican](http://mathamy.com/migrating-to-github-pages-using-pelican.html)

TODO
----
- disqus setup
- ipython notebook integration
- update .bashrc for deactive() call
- starting writing real contents
