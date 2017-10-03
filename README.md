Bitmask Help Pages
==================================

This is the repository for the Bitmask help pages at https://bitmask.net.

It is entirely static, but relies on a bunch of apache tricks for things like
language negotiation. Bitmask help uses a static website generator called `amber`
to render the source files into html files.

To submit changes, please fork this repo and issue pull requests on github. If
you don't know how to use git, you can submit changes via the github website.

Simple method - editing on github
--------------------------------------------

Learning to use git can be very difficult. As an alternative, it is possible
to contribute to bitmask_help by directly editing pages through the github
website. This method does not let you preview how the page will render, but it
does allow you to contribute edits without needing to install any software.

First, create your own fork:

1. Go to https://github.com and register for an account
2. Visit https://github.com/leapcode/bitmask_help
3. Click "Fork" in the top right hand corner

Next, edit files:

* **Existing Files:** You can edit an existing file by clicking on the file
  name and then clicking the "Edit" button in the file's toolbar. To save,
  type a commit message and hit the "Commit" button.
* **New Files:** You can add a new page by clicking the "+" button at the
  end of the path breadcrumbs (e.g. "bitmask_help / pages / chat / [+]"
  near the top of the page).

Once you are done with edits:

1. Visit the web page for your fork (e.g. https://github.com/yourname/bitmask_help)
2. Click the "Pull Request" link above the file listing (not the "Pull Requests" link on the side)
3. Review changes, then click "Create Pull Request"
4. Add some description, the click "Send pull request"

Boom, you are done. Someone will review the pull request
and either merge it right away or add comments.

Once your changes are merged, you should destroy your fork. Then, the next time you want to make
changes, create a new fork again. This way, you will be working from the current copy.

Advanced method - using git and amber
--------------------------------------------

Installing amber

In order to preview your edits to the content in `pages` you will need a
program called `amber`.

To install on Debian or Ubuntu (Wheezy or later):

    sudo apt-get install ruby ruby-dev libz-dev
    sudo gem install amber

To install on Mac, see below. Check https://github.com/leapcode/amber for more
information.

Previewing pages

When you are making changes, you can see a preview of these changes
by running the amber server:

    amber server

Then browse to http://localhost:8000. Any page you view this way gets re-
rendered when it is loaded. Because the links and css paths are absolute,
loading the rendered pages directly in the browser will create ugly results.
For this reason, it is best to use the `amber server`.

Putting it all together:

1. Go to https://github.com/leapcode/bitmask_help and click the fork button.
2. Clone your fork locally: `git clone ssh://git@github.com/your-id/bitmask_help`
3. Start the amber server: `cd bitmask_help; amber server`
4. Edit files in `bitmask_help/pages`
5. Preview changes in your browser using http://localhost:8000
6. When satisfied, `git commit`, `git push`
7. Go to https://github.com/your-id/bitmask_help and [issue a pull request](https://help.github.com/articles/using-pull-requests)

One way you can refresh your repo with upstream before pushing:

    git remote add upstream https://github.com/leapcode/bitmask_help
    git fetch upstream
    git rebase upstream/master

You only need to run `git remote add` once. Alternately, you could set origin
to be `leapcode/bitmask_help` and add your fork as a remote.

Directories
--------------------------------------------

    bitmask_help/
      amber/     -- amber configuration, stylesheets, layouts, etc.
      pages/     -- the source text for the website pages.
      public/    -- the rendered output (not committed to git).

The static content files in `bitmask_help/public` are rendered from the content in
`bitmask_help/pages`. You edit pages in the `pages` directory, but never edit
anything in the `public` directory.

Amber file structure
--------------------------------------------

There are two ways to create pages:

A page might be represented by files with different language suffixes:

    email.en.text
    email.pt.text

Alternately, a page might be represented by a folder. This method allows you
to have sub-pages.

    email/
      en.text
      pt.text
      client/
        en.text

In general, it is preferred to use the folder method, even when pages
don't have children.

Modifying locale files
--------------------------------------------

Many of the strings for the website are not in pages but are in special
localization files. These live in the locales directory:

    amber/
      locales/
        en.yml
        es.yml

If you change one of these files or add a file, you will need to restart
the amber server.

Note: these files are only picked up if the locale is enabled in `amber/config.rb`.

Modifying Navigation
--------------------------------------------

If you need to add or remove a top or side nav menu, you'll need to edit

    amber/
      menu.txt

Note that you will need to restart the amber server for changes to take effect.

Notes on markup
--------------------------------------------

You can create pages in three different markup languages:

* textile (suffix .text)
* markdown (suffix .md)
* haml (suffix .haml)

Most of the Bitmask help pages are written using textile. It is best to keep to
textile for consistency.

Here is a brief overview of textile markup:

    h1. heading 1
    h2. heading 2

    this is a paragraph

    * this is a list
    * another item in the list

    "this is a link":http://to-this-url.org

    here is some *bold text*

For a complete reference, see http://redcloth.org/textile/

Amber adds an additional way to make links:

    [[label -> page-name]]
    or
    [[page-name]]
    or
    [[chat/client]]
    or
    [[label => https://bitmask.net]]

By using this double bracket link notation will automatically find the right
path for the page with the specified name. Also, it will warn you if the page
name is missing and it will ensure that the link is created with the correct
language prefix. In haml, you can get the same effect using ruby code
`link 'label' => 'page'`

The standard textile and markdown methods of linking do not work well with
non-latin languages or right-to-left script, so it is recommended that you
always use the amber method of forming links.

The arrows `->` and `=>` can be used interchangeably. For right-to-left script,
the arrow goes the opposite direction (`<-` or `<=`).

Setting page properties
--------------------------------------------

Every file can have a "properties header". It looks like this:

    @title = "A fine page"
    @toc = false

    continue on here with body text.

The properties start with '@' and are stripped out of the source file before
it is rendered. Property header lines are evaluated as ruby. All properties
are optional and they are inherited, including `@title`. To make a property
not get inherited, use `@this.propertyname = 'value'` instead.

The syntax for properties is slightly different for HAML files (so that it
is still valid HAML):

    - @title = "A fine page"
    - @toc = false

    %p continue on here with body text.

Available properties:

* `@title` -- The title for the page, appearing as in an H1 on the top of the
   page and as the HTML title. Also used for navigation title if `@nav_title`
   is not set.
* `@nav_title` -- The title for the navigation to this page, as well as the
   HTML title if @title is not set.
* `@summary` -- Displayed under the title.
* `@toc` -- If set to `false`, don't include a table of contents when rendering
   the file. This only applies to .text and .md files.
* `@layout` -- Manually set the layout template to use for rendering this page.
* `@this.alias` -- An alternate url path (or paths if the value is an array)
   where this page should be available.

Tracking pages that need translating
--------------------------------------------

We do not yet have the capability to automatically identify which translated
pages need to be updated. However, in the future, I plan to add the command
`amber diff [language-code]`, which will automatically spit out a listing that
shows the changes made to the source English pages since the translation for
each page was made.

Installing on Mac
--------------------------------------------

(I haven't tried this myself)

Ruby 1.9 or greater is required to run amber.

Mac OS 10.9 (Mavericks) or later is running ruby 2.0 and can work with amber
out of the box. For earlier Mac OS releases, you need to upgrade the ruby that
comes with the computer. The easiest way to do this is with homebrew. To
install, open a terminal and type:

    ruby -e "$(curl -fsSL https://raw.github.com/Homebrew/homebrew/go/install)"
    brew install ruby

After ruby is at 1.9 or newer, then just run:

    sudo gem install amber

Alternately, if you want different versions of ruby installed, consider:

* https://github.com/sstephenson/rbenv
* http://rvm.io/

Installing on Windows
----------------------------------------

Windows is not yet supported.
