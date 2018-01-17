.. _sphinx-intro:

#################
Intro to MySphinx
#################

I decided to start a new project to document how I use Sphinx.  I also plan to put a repository for the project up on GitHub.  Here is how I do it.

I start with Sphinx.  The home page is here:

http://sphinx-doc.org

A prominent instruction says to do:

.. sourcecode:: bash

    easy_install -U Sphinx

I don't use ``easy_install`` much, but for Sphinx this is how I do it.  I repeat the process now, not expecting much, and I find that it runs.

Just check the version:

.. sourcecode:: bash

    > sphinx --version
    -bash: sphinx: command not found
    > sphinx-
    sphinx-apidoc      sphinx-build       
    sphinx-autogen     sphinx-quickstart  
    > sphinx-
    > sphinx-build --version
    Sphinx (sphinx-build) 1.3b3
    >

Sorry to introduce a complication right at the beginning, but here goes.  Apparently ``Sphinx`` does not have a command line tool named ``sphinx``, so ``sphinx --version`` does nothing.  I discovered the names of the other programs by tabbing:  First I typed in ``sph`` and then tab to obtain ``sphinx-``; at that point a double tab prints out the possible matches:  there are four of them, and the display goes back to ``sphinx-``.  Finally, I type in a ``b`` and tab once again and Terminal gives me ``sphinx-build``.  From there I just add ``--version``.

..note:: 
    I am not actually completely happy with this.  The front page says version ``1.2.3`` is the current one;  here we have ``1.3b3`` which is probably a "development" version and may have some quirks.

To start a new project, I do ``mkdir MySphinx`` and then ``cd MySphinx`` and then we run ``sphinx-quickstart`` from *inside the new project directory*.  The output of some of the choices displayed by ``quickstart`` is messed up, so the new version does seem a little buggy.  

I check the output file ``config.py``, and correct one line:  I don't like the new default theme ``'alabaster'`` and I happen to know that the alternative is ``'classic'``, so I do that substitution.

I add the first line ``.. _sphinx-intro:`` to this file, and move it into the project as ``intro.rst``.  I modify ``index.rst`` (produced by ``quickstart``) as follows:

.. sourcecode:: bash

    .. toctree::
       :maxdepth: 2

      intro.rst

If you want to see what this file looks like, click of Show Source in the sidebar.

Then I ``cd`` into the project directory and do ``make html``.

.. sourcecode:: bash

    Last login: Tue Mar 10 11:46:15 on ttys000
    > cd Desktop
    > cd MySphinx/
    > make html
    sphinx-build -b html -d _build/doctrees   . _build/html
    Running Sphinx v1.3b3
    making output directory...
    loading pickled environment... not yet created
    building [mo]: targets for 0 po files that are out of date
    building [html]: targets for 2 source files that are out of date
    updating environment: 2 added, 0 changed, 0 removed
    reading sources... [100%] intro                             
    /Users/telliott_admin/Desktop/MySphinx/index.rst:11: WARNING: toctree contains reference to nonexisting document u' :maxdepth: 2'
    looking for now-outdated files... none found
    pickling environment... done
    checking consistency... done
    preparing documents... done
    writing output... [100%] intro                              
    /Users/telliott_admin/Desktop/MySphinx/index.rst:11: WARNING: toctree contains reference to document u'intro' that doesn't have a title: no link will be generated
    generating indices... genindex
    writing additional pages... search
    copying static files... done
    copying extra files... done
    dumping search index in English (code: en) ... done
    dumping object inventory... done
    build succeeded, 2 warnings.

    Build finished. The HTML pages are in _build/html.
    > 

I point Safari at the output by doing this in Terminal:

.. sourcecode:: bash

    open -a ~/Desktop/MySpinx/_build/html/index.html
    
I take a screenshot, rename the file, make a directory ``figs`` inside the project, and put this directive into the source for this file:

.. sourcecode:: bash

    .. image:: /figs/sphinx1.png
      :scale: 50 %

Here is the image:

.. image:: /figs/sphinx1.png
  :scale: 50 %

Click on the link to this first chapter and see

.. image:: /figs/sphinx2.png
  :scale: 50 %

We want to set up a "repo" or repository on GitHub.

I don't want to track the files inside the ``_build`` directory so I put this into a file ``.gitignore`` in ``_build``:

.. sourcecode:: bash

    > cp MyUnix/_build/.gitignore MySphinx/_build
    > cat MySphinx/_build/.gitignore 
    # Ignore everything in this directory
    *
    # Except this file
    !.gitignore
    >

Next I need to do ``git init`` and ``git add *``, etc.  But first, before I do the first commit, I go to GitHub, sign in, and set up a repo for this project using the website.  Click on ``+`` and follow the brief instructions.  Two clicks.  Read the instructions for copy-paste to Terminal.

Now back in the project directory I do

.. sourcecode:: bash

    > cd Desktop
    > cd MySphinx/
    > git init
    Initialized empty Git repository in /Users/telliott_admin/Desktop/MySphinx/.git/
    > git add *
    > git remote add origin git@github.com:telliott99/MySphinx.git
    > git remote -v
    origin	git@github.com:telliott99/MySphinx.git (fetch)
    origin	git@github.com:telliott99/MySphinx.git (push)
    > git commit -m "first commit"
    [master (root-commit) 7c2ff23] first commit
     7 files changed, 632 insertions(+)
     create mode 100644 Makefile
     create mode 100755 _build/.gitignore
     create mode 100644 conf.py
     create mode 100644 figs/sphinx1.png
     create mode 100644 figs/sphinx2.png
     create mode 100644 index.rst
     create mode 100644 sphinx-intro.rst
    > git push -u origin master
    Counting objects: 11, done.
    Delta compression using up to 4 threads.
    Compressing objects: 100% (10/10), done.
    Writing objects: 100% (11/11), 251.15 KiB | 0 bytes/s, done.
    Total 11 (delta 0), reused 0 (delta 0)
    To git@github.com:telliott99/MySphinx.git
     * [new branch]      master -> master
    Branch master set up to track remote branch master from origin.
    >

That is all there is to it.  We can even view the page on GitHub.

https://github.com/telliott99/MySphinx/blob/master/sphinx-intro.rst

It looks really good, even though the file is not designed to be read in this manner.  What we are doing is saving the source ``.rst`` files which Sphinx will transform into ``.html`` files suitable for viewing in a browser.  To see that output, again do this from the command line:

.. sourcecode:: bash

    > open -a Safari ~/Desktop/MySphinx/_build/html/index.html

Or navigate there in the Finder and double-click.  I have a short-cut set where I can do ``oh`` from top-level in the project.  But to explain that would be getting ahead of ourselves.





