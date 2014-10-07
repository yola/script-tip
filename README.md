#script-tip

Daily Command Line Tip or Trick



###To use, set up a ruby development environment:

1. Install [rbenv](https://github.com/sstephenson/rbenv) and ruby 2.0.0-p247
1. Install bundler, by running `gem install bundler`
1. Install dependencies, by running `bundle install`


###Run jekyll

1. Start the server with `bundle exec jekyll serve`
1. 0pen your browser at [http://localhost:5000](http://localhost:5000).


###Create a new post


    touch _posts/yyyy-mm-dd-url-friendly-title.markdown

... where yyyy-mm-dd is a date (e.g., 2012-08-31) and url-friendly-title is, well, a URL-friendly title.  

Then inside that post, be sure to add at least the minimal [YAML front matter](https://github.com/mojombo/jekyll/wiki/YAML-Front-Matter):

    ---
    layout: post
    title: "My Awesome Script Tip"
    ---

   	It was the best of greps it was the worst of greps...
