# Intro
If you are a Ruby on Rails developer who is just getting started with Ember sometimes you would want to map 
equivalent Rails functionalities into Ember (e.g How can I do a `link_to`?)

The Ember-Rails Style guide aims to be a community generated guide to make easier for Rails developers to get started
with Ember.

# Understanding Ember Concepts (WIP)
# Rails Model to Ember Model.
# Rails Controllers
# Rails Views
# Rails Helpers
# Testing


# Routes
* Try to avoid nested routes
* In the Index action for  controllers add support for params[:ids]

        def index
          @comments = Comment.all

          if params[:ids]
            @comments = @comments.where(id: params[:ids])
          end
          respond_with @micro_tags
        end

* Return the ids for you has_many relations with active model serializer you can do

         class MySerializer < ActiveModel::Serializer
             embed :id
             has_many :foo # This will add foo_ids
             has_one :bar  # bar_id
         end

In your Ember Model

       App.Post = DS.Model.extend
         comments: DS.hasMany('comment', async: true) # this will load your association lazily

       App.Comment = DS.Model.extend
         post: DS.belongsTo('post')

When you do `model.get('comments')` it will fire a request to `'/comments?ids=[1,2,3]`

# Embedding Ember.js into an existing Rails app

You can embed Ember.js on a subsection of a page instead of the default `<body>` by specifying the `rootElement` property on your Ember application object:

    var App = Ember.Application.create({
      rootElement: '#ember-app'
    });
    
If this is the case you may not want Ember changing the URL:

    App.Router.reopen({
      location: 'none'
    });

This can be a good starting point for gradually migrating an existing Rails app to Ember.js.

# Read

* [Ember.js Concepts for Rails Developers - Matthew Lehner](http://matthewlehner.net/ember-js-concepts-for-rails-devs)
* [Ember Routing: The When and Why of Nesting - Hashrocket Blog](http://hashrocket.com/blog/posts/ember-routing-the-when-and-why-of-nesting)


# Contributing

Feel free to open tickets or send pull requests with improvements.

# License

![Creative Commons License](http://i.creativecommons.org/l/by/3.0/88x31.png)
This work is licensed under a [Creative Commons Attribution 3.0 Unported License](http://creativecommons.org/licenses/by/3.0/deed.en_US)

Inspired by [https://github.com/bbatsov/ruby-style-guide](https://github.com/bbatsov/ruby-style-guide)
