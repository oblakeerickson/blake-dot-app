---
layout: post
title:  "Ember CLI - TodoMVC Tutorial - Adding a Rails Back End"
date:   2014-07-07 01:00:00 -0600
---

Now that we have our ember application working, let's add in a data persistance layer so that not only when we refresh the browser we don't lose any data, but you will also still have all your Todo items if you were to visit this page from another computer. To add this data persistance layer we are going to use Ruby on Rails.

Our current directory structure for our Ember app should look something like this: `~/code/todos`, but want to put our Rails and Ember app in separate directories, but under the same parent directory. So, let's work on that now by renaming the current ember application directory, creating a new project directory, moving our ember directory into the project directory, and then creating our rails project:

```
    cd ~/code/
    mv todos ember
    mkdir todos
    mv ember todos/
    cd todos
    rails new todos
    mv todos rails
    cd rails
```

Now our directory structure should like like: `~/code/todos/ember` and `~/code/todos/rails`.

## Working on our Rails API

Now that we are inside of our Rails directory lets edit the `Gemfile` and get rid of some Javascript dependencies and add some tools that we will need for our API. The new `Gemfile` should look like this:

```
source 'https://rubygems.org'

gem 'rails', '4.1.1'
gem 'sdoc', '~> 0.4.0',          group: :doc
gem 'spring',        group: :development
gem 'active_model_serializers'
gem 'rack-cors', :require => 'rack/cors'

group :development, :test do
  gem 'sqlite3'
end

group :production do
  gem 'pg'
end
```

Now run `bundle install`.

Now let's edit our `config/application.rb` file. We are going to comment out the line with `sprockets` in it and add some stuff to take care of CORS. Your new file should like like the following:

```
require File.expand_path('../boot', __FILE__)

# Pick the frameworks you want:
require "active_model/railtie"
require "active_record/railtie"
require "action_controller/railtie"
require "action_mailer/railtie"
require "action_view/railtie"
# require "sprockets/railtie"
require "rails/test_unit/railtie"

# Require the gems listed in Gemfile, including any gems
# you've limited to :test, :development, or :production.
Bundler.require(*Rails.groups)

module Todoemberrails
  class Application < Rails::Application
    config.assets.enabled = false

    config.middleware.use Rack::Cors do
      allow do
        origins '*'
        resource '*', headers: :any, methods: [:get, :post, :put, :delete, :options]
      end
    end
  end
end

```

## Creating our Todos Model

We need to setup our database to store our todo items and their completed status. To do this type in this command:

    rails generate model todo title:string is_completed:boolean

This will create a migration file for you inside of `db/migrate/` with the current timestamp called `create_todos.rb`. To run this migration file type:

    rake db:migrate

## Creating our Serializer

The next thing that we need to do is create a serializer. Create a new directory inside of the `app` directory called: `serializer`:

    mkdir app/serializer

And then create a new file inside of that folder called: `todo_serializer.rb`:

    touch app/serializer/todo_serializer.rb

Inside of this file type:

```
    class TodoSerializer < ActiveModel::Serializer
      attributes :id, :title, :is_completed
    end
```

## Creating our Controller

We are going to place our controller inside of an api folder so before we create our controller file lets make that directory:

    mkdir app/controllers/api

Now let's make our todos controller file:

    touch app/controllers/api/todos_controller.rb

Now edit this file to look like the following:

```
class Api::TodosController < ApplicationController
  skip_before_action :verify_authenticity_token
  def index
    render json: Todo.all
  end

  def show
    render json: Todo.find(params[:id])
  end

  def create
    todo = Todo.new(todo_params)

    if todo.save
      render json: todo, status: :created
    else
      render json: todo.errors, status: :unprocessable_entity
    end
  end

  def update
    todo = Todo.find(params[:id])

    if todo.update_attributes(todo_params)
      render json: todo
    else
      render json: todo.errors, status: :unprocessable_entity
    end
  end

  def destroy
    todo = Todo.find(params[:id])
    todo.destroy
    head :no_content
  end

  private

  def todo_params
    params.require(:todo).permit(:title, :is_completed)
  end
end
```

## Creating our Routes

Now we need to do setup our `config/routes.rb` file to talk to our controller. It should like like:

```
Rails.application.routes.draw do
  namespace :api do
    resources :todos
  end
end
```

## Starting our Server

Now that we have everything configured let's start our Rails Server with the `rails s` command. It should start on http://localhost:3000. We then need to configure this as the host inside of our ember app.

## Configuring Ember to talk to our Rails API

Now inside of our `ember` directory open up `app/adapters/application.js`. And edit the file to look like the following:

```
import DS from 'ember-data';

export default DS.ActiveModelAdapter.extend({
  host: 'http://localhost:3000/api'
});
```

This tells are Ember app where it can reach our Rails API.

## Starting our Ember Server

From inside of a different terminal windows let's start our ember server with `ember s`. Which should start running at http://localhost:4200. There shouldn't be any todos yet in our list since our database is empty. So go ahead and create some, and then refresh the page to see that they are no longer being cleared out like they were before we setup our Rails API for data persistance.
