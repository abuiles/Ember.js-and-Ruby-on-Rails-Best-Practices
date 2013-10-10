# Prelude
A bunch of Rails developers have started to pickup this awesome Ember thing.
Though when we start to work on it, there is always the question on
how to map equivalent functionalities. For example, how can I do a
link_to in Ember? How do I handle relationships? etc.

The Ember-Rails Style guide aims to be a community generated guide,
collecting knowledge from all the Rails developers out there who have
started to work with Ember.

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

# Contributing

Feel free to open tickets or send pull requests with improvements.

# License

![Creative Commons License](http://i.creativecommons.org/l/by/3.0/88x31.png)
This work is licensed under a [Creative Commons Attribution 3.0 Unported License](http://creativecommons.org/licenses/by/3.0/deed.en_US)

Inspired by [https://github.com/bbatsov/ruby-style-guide](https://github.com/bbatsov/ruby-style-guide)
