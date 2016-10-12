# Building My Own Resposive Blog using Rails 5

This is written for Rails beginners  with a walkthrough of building a blog web application.

If you include 'bootstrap' gem in your Gemfile, you can implement easily responsive web pages.



## Development Environment

This project was tested on the following development environment :

- Ruby v2.3.1
- Ruby on Rails v5.0.0.1
- UI : Bootstrap  v4.0.0-alpha.4 (as of Sep 9, 2016)
- Deployment : Heroku
- Terminal tool : iTerm2
- Code editor : Atom (http://atom.io)
- SCM : Git
- Remote Repository : http://github.com




## Getting Started

Let's get started from creating a Rails project named as `"rorla-blog"`.

```sh
$ rails new rorla-blog
```

At this time, without addtional command line option `-d`, sqlite is set up implicitly as a default database adapter. But, if you want to change the default database adapter to the other one, you could create `.railsrc` file on your account home directory and add the following lines:

```shell
$ cat ~/.railsrc
-d postgresql
```

From now, all Rails projects will be created with `PostgreSQL` database adapter by default.

Using the following command, you should create database for development and test environments before starting rails server.

```sh
$ rake db:create
```



## Composition of Gemfile

Let's open Gemfile on the project root directory and add the following gems:

```ruby
gem 'bootstrap', '~> 4.0.0.alpha3.1'
gem "bootstrap_flash_messages", "~> 1.0.1"
gem 'simple_form'
gem 'devise'

gem "letter_opener", :group => :development

# Tooltips and popovers depend on tether for positioning. If you use them, add tether to the Gemfile:
source 'https://rails-assets.org' do
  gem 'rails-assets-tether', '>= 1.1.0'
end
```

### 1. bootstrap

Bootstrap will be used as a front-end styling framework. Recently it is being developed for its new version 4 and, as of, it is included v4.0.0.alpha3.1 in this gem. After bundle installing for the first time, application.css file on `assets/stylesheets/` folder should be renamed to `application.scss`, a SCSS file(sassy CSS) and delete its all contents. And then`bootstrap` file need to be imported as follows:

```ruby
@import "bootstrap";
```

In the `application.js` file on the`assets/javascripts/` folder, you should require `tether` and `bootstrap` as follow:

```js
//= require jquery
//= require tether
//= require bootstrap
//= require jquery_ujs
//= require turbolinks
//= require_tree .
```

### 2. boostrap_flash_messages

This gem is for flash message presentation. After bundle-installing, the following `erb` snippet should be inserted at the appropriate location in the application layout file(`views/layouts/appliction.html.erb`).

```erb
<div id="flash_messages"><%= flash_messages(:close) %></div>
```

### 3. simple_form

If you use simple_form gem, you can reduce the amount of codes for form tag composition and simplify them. More over, if you want to apply Bootstrap styling framework to form_form helper, you had better use simple_form gem with `—bootstrap`  option. Suppose you had already bundle-installed this gem, you should run the following commands as follows:

```sh
$ rails generate simple_form:install --bootstrap
```

### 4. devise

This is a very famous gem for authenticating users in Rails world. If you manage the membership for your application, it is definitely included in your Gemfile. To apply this gem after bundle-installing, run the following commands in terminal:

```sh
$ rails generate devise:install    # apply devise gem in your project
$ rails generate devise User       # generate User model for device gem
$ rails generate devise:views      # customize devise views
```

You should not forget to update 'config/initializers/devise.rb' (line number #223 ) as follows:

```ruby
config.scoped_views = true    # uncomment this line and change its value to true.
```

### 5. letter_opener

When you apply `:confirmable` devise module to `User` model, users will get the confirm email from your application server. In development mode, it is so inconvenient to send real emails. In this context, you can use `letter_opener` gem and immediately check the email received in simulated situation. For this, you should insert the following code line in  `config/environments/development.rb` file:

```ruby
config.action_mailer.delivery_method = :letter_opener
```

### 6. rails-assets-tether

In fact, this is an accessory gem for **tooltips and popovers** function of Bootstrap 4.



## Booting Rails Server

To confirm that there is no errors in the above coding works, let's start rails local server and open it on the web browser.



## Setting Up Heroku Deployment (PaaS)

It's time to deploy this blog project to Heroku if we can't find any errors on booting rails server.

Conventionally, we deploy rails projects to the remote web server (Nginx or Apache) using `Capistrano` gem. But, It is a very cumbersome and difficult to deploy Rails projects for Rails beginners.

In this lecture, to lessen deployment burden, Heroku service will be introduced. Heroku is a Platform as a Service for deployment of various framework projects. And so, you can easily deploy your Rails project, just doing `git push heroku master` command in command line of terminal.

If you don't have any accounts for Heroku, first of all, you should sign up at [Heroku site](https://www.heroku.com).

Sign in at Heroku website and you can see `New` > `Create new app` menu.

I will name the app name `rorla-blog`.

>  Reference : [Getting Started with Rails 5.x on Heroku](https://devcenter.heroku.com/articles/getting-started-with-rails5)


At this point, if you didn't initialize Git, please walk through as follows:

```sh
git init
git add .
git commit -m 'initial commit'
```

Well, you can deploy `rorla-blog` project to Heroku like as if you do "git push" to remote repository.

```sh
heroku git:remote -a rorla-blog
git push heroku master
```

It's so simple. What a easy way to deploy Rails projects!



## Gem Update

During the screencast production, `bootstrap` gem was upgraded from alpha3.1 to alpha4 version, as of September 10, 2016. And so, if you need to upgrade the specific gem only, you could run the command as follows:

```sh
$ bundle update bootstrap
$ bundle list | grep "bootstrap\s"
```



## Working Steps

- Chapter 1. Application Layout
  - Layout design
  - Flash message
- Chapter 2. Membership
  - Registration, Profile, Withdrawal
  - Sign in / Sign out
- Chapter 3. Posting
  1. CRUD
  2. Email notification to subscribers on creating a post
  3. Subscribe / Unsubscribe
- Chapter 4. Commenting
  1. CRUD
  2. Email notification to post-writer on creating a comment
- Chapter 5. Image Upload
- Chapter 6. Tagging
  1. Create tags on a post
  2. Tag cloud
  3. Search tags
- Chapter 7. Categorizing Posts
  1. CRUD
- Chapter 8. Sidebar Widgets
  1. List of recent 5 posts
  2. List of post counts by year-month
  3. List of posts by categories




## Bootstrap 4 Responsive Layout and Grid System

http://v4-alpha.getbootstrap.com/layout/overview/



![](http://i683.photobucket.com/albums/vv193/luciuschoi/building_my_blog/2016-10-12_18-19-05_zpso7qtufme.png)



![](http://i683.photobucket.com/albums/vv193/luciuschoi/building_my_blog/2016-10-12_18-17-55_zpsdhbyzt1w.png)

http://v4-alpha.getbootstrap.com/layout/grid/#customizing-the-grid



## Application Layout Design

This project's application layout will be composed of 3 sections: `header`, `trunk`, and `footer`. Especially, `trunk` section has two columns: `main` and `aside`.

In HTML5, various sectionaing elements were introduced: `header`, `nav`, `main`, `article`, `section`, `aside`, `footer`, and `address`.

These are very intuitive and helpful on exploring whole structure of application layout and also some programs, e.g. screen reader, can easily detect the structure of web page.

In this project, we will use `header`, `main`, `aside`, and `footer` tags and make the application layout as follows:

![](http://i683.photobucket.com/albums/vv193/luciuschoi/building_my_blog/2016-10-12_18-27-57_zpsxnbyscog.png)

It's HTML codes are like this:

```erb
<body>
  <div class='container'>
    <header>
      <div id="logo">RORLA Blog</div>
    </header>
    <div id='trunk'>
      <main role='main'>
        <div id="flash_messages"><%= flash_messages(:close) %></div>
        <%= yield %>
      </main>
      <aside>
        <p>사이드바</p>
      </aside>
    </div>
    <footer>
      RORLA Blog<sup>&reg;</sup> since 2016. RORLAB | All Rights Reserved.
    </footer>
  </div>
</body>
```

Also, you need some CSS styles for this layout.

So you should create `app/assets/stylesheets/layouts.scss` file and fill it with the following:

```scss
header, #trunk, footer { @extend .row; }

header {
  color: white;
  background-color: #3f4c6b;
  padding: 2em 0;
  text-align:center;
  margin-bottom: 1.5em;
  h1 {
    font-weight: bold;
  }
}

#trunk {
  main { @extend .col-lg-9; }
  aside { @extend .col-lg-3; }
}

footer {
  text-align: center;
  margin-top: 1em;
  padding: 1em 0;
  border-top: 1px solid #ccc;
}
```

> _*Reference*_ : [http://sass-lang.com/guide/inheritance](http://sass-lang.com/guide#topic-7)

This CSS file also should be imported in the `app/assets/stylesheets/application.scss` file.

```scss
@import "bootstrap";
@import "layouts";
```

In the responsive design, you should not forget including the viewport meta information between `head` tags as follows:

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0, minimum-scale=1.0, maximum-scale=1.0">
```

>  *Reference* : [Understanding the viewport meta tag, CSS @viewport and making an automatic link to your app](https://benfrain.com/understanding-the-viewport-meta-tag-and-css-viewport/)



## Flash Messaging

Flash is a hash object(`ActionDispatch::Flash::FlashHash`) which contain temporarily some messages occurring during action running, and can be accessed at the very next action view template file. After that, it disappears.

Symbolic keys, e.g. `:notice`, `:alert`, are used and its usage is as follow:

```ruby
flash[:notice] = "Successfully saved."
flash[:alert] = "Failed to save."
```

`:notice` and `:alert`  keys are mostly commonly used and they have individual dedicated methods:

```ruby
flash.notice = "Successfully saved."
flash.alert = "Failed to save."
```

Flash `now` method returns `FlashNow` class object and can be used when flash message can be accessed just in the current action and it usage is as follow:

```ruby
flash.now[:notice] = "Successfully save."
flash.now[:alert] = "Failed to save."
```

They have also their convenient accessors:

```ruby
flash.now.notice = "Successfully save."
flash.now.alert = "Failed to save."
```

This `now` method is very useful on the system messaging of application.

In addition to `now` method,  `keep` method postpones `flash` object to next action.

``` ruby
flash.keep            # keeps the entire flash
flash.keep(:notice)   # keeps only the "notice" entry, the rest of the flash is discarded
```

If you are using Bootstrap, you can easily insert flash messages in application layout.

For this, you need add `bootstrap_flash_messages` gem into Gemfile and bundle install.

```ruby
gem "bootstrap_flash_messages", "~> 1.0.1"
```

And you just insert the `ERB` code at the proper position in application layout as follows:

```erb
<div id="flash_messages"><%= flash_messages(:close) %></div>
```



## User registration & authentication

A `log_status`  partial template is inserted in `aside` section in application layout file.

```erb
<!-- app/views/layouts/application.html.erb -->
<%= render "shared/log_status" %>
```

For this purpose, `views/shared/_log_status.html.erb`  file need to be filled as follows:

```erb
<div class="log_status">
  <% if user_signed_in?  %>
    <% if devise_controller? %>
      <%= link_to "Home", root_path, class: "btn btn-outline-primary d-block m-b-1" %>
    <% end %>
    <%= link_to "Sign out #{current_user.name}", destroy_user_session_path, method: :delete, data: { confirm: 'Are you sure?' }, class: "btn btn-outline-primary d-block d-block m-b-1" %>
    <%= link_to "Account", edit_user_registration_path, class: "btn btn-outline-primary d-block" %>
  <% else %>
    <% if devise_controller? %>
      <%= link_to "Home", root_path, class: "btn btn-outline-primary d-block" %>
    <% else %>
      <%= link_to "Sign In", new_user_session_path, class: "btn btn-outline-primary d-block m-b-1" %>
      <%= link_to "Sign Up", new_user_registration_path, class: "btn btn-outline-primary d-block" %>
    <% end %>
  <% end %>
</div>
```



You should include additional `:name` attribute in stong params hash. For this, insert the following code lines in `app/controllers/application_controller.rb`.

```ruby
class ApplicationController < ActionController::Base
  before_action :configure_permitted_parameters, if: :devise_controller?

  protected

  def configure_permitted_parameters
    devise_parameter_sanitizer.permit(:sign_up, keys: [:name])
    devise_parameter_sanitizer.permit(:account_update, keys: [:name])
  end
end
```

But, unfortunately, we could find out 2 path errors in devise view template files.

URL path is wrong in `views/devise/confirmations/new.html.erb`.

```erb
<%= simple_form_for(resource, as: resource_name, url: confirmation_path(resource_name), html: { method: :post }) do |f| %>
```

To fix this error, `confirmation_path(resource_name)` should be changed to `user_confirmation_path` as follows:

```erb
<%= simple_form_for(resource, as: resource_name, url: user_confirmation_path, html: { method: :post }) do |f| %>
```

Another URL path error was found at code line #14 in `views/devise/shared/_links.html.erb` as follows:

```erb
<%= link_to "Didn't receive confirmation instructions?", new_confirmation_path(resource_name) %><br />
```

To fix this error, `new_confirmation_path(resource_name)` should be corrected to `new_user_confirmation_path` as follows:

```erb
<%= link_to "Didn't receive confirmation instructions?", new_user_confirmation_path %><br />
```

> *Reference* : [Devise Strong Parameters](https://github.com/plataformatec/devise#strong-parameters)



## Creating Post Resource

```sh
$ rails g scaffold Post title content:text user:references
```

```ruby
Running via Spring preloader in process 69391
      invoke  active_record
      create    db/migrate/20161010210648_create_posts.rb
      create    app/models/post.rb
      invoke    test_unit
      create      test/models/post_test.rb
      create      test/fixtures/posts.yml
      invoke  resource_route
       route    resources :posts
      invoke  scaffold_controller
      create    app/controllers/posts_controller.rb
      invoke    erb
      create      app/views/posts
      create      app/views/posts/index.html.erb
      create      app/views/posts/edit.html.erb
      create      app/views/posts/show.html.erb
      create      app/views/posts/new.html.erb
      create      app/views/posts/_form.html.erb
      invoke    test_unit
      create      test/controllers/posts_controller_test.rb
      invoke    helper
      create      app/helpers/posts_helper.rb
      invoke      test_unit
      invoke    jbuilder
      create      app/views/posts/index.json.jbuilder
      create      app/views/posts/show.json.jbuilder
      create      app/views/posts/_post.json.jbuilder
      invoke  assets
      invoke    coffee
      create      app/assets/javascripts/posts.coffee
      invoke    scss
      create      app/assets/stylesheets/posts.scss
      invoke  scss
      create    app/assets/stylesheets/scaffolds.scss
```

To customize the `db/migrate/[your_timestamp]_create_posts.rb` migration file

```ruby
class CreatePosts < ActiveRecord::Migration[5.0]
  def change
    create_table :posts do |t|
      t.string :title
      t.text :content, null: false
      t.references :user, foreign_key: true

      t.timestamps
    end
  end
end
```

In here, you could add `null: false` option to code line No. 5 to set content column to be required.

Don't forget to rake db:migrate to create physical tables in database.

```sh
$ rake db:migrate
```

```ruby
Running via Spring preloader in process 69944
== 20161010210648 CreatePosts: migrating ======================================
-- create_table(:posts)
   -> 0.0328s
== 20161010210648 CreatePosts: migrated (0.0329s) =============================
```

You need to confirm the routing info on posts resource. Run the commands as follows:

```sh
rails routes -c posts
```

```ruby
   Prefix Verb   URI Pattern               Controller#Action
    posts GET    /posts(.:format)          posts#index
          POST   /posts(.:format)          posts#create
 new_post GET    /posts/new(.:format)      posts#new
edit_post GET    /posts/:id/edit(.:format) posts#edit
     post GET    /posts/:id(.:format)      posts#show
          PATCH  /posts/:id(.:format)      posts#update
          PUT    /posts/:id(.:format)      posts#update
          DELETE /posts/:id(.:format)      posts#destroy
```

You can easily find out the URI pattern on the index page of posts resource. So lets' put that URI on the browse and go.

![](http://i683.photobucket.com/albums/vv193/luciuschoi/building_my_blog/2016-10-11_06-35-00_zps3brbluer.png)

Before you proceed further, you should insert `has_many` association declaration in `User` class as follows:

```ruby
class User < ApplicationRecord
  ...
  has_many :posts, dependent: :destroy
  ...
end
```

And so you can use like this: e.g. `@user.posts`.

Let's customize the index page of posts. For this, open the index.html.erb file in the views/posts/ folder in your favorite code editor.

```erb
<!-- original code -->
<p id="notice"><%= notice %></p>

<h1>Posts</h1>

<table>
  <thead>
    <tr>
      <th>Title</th>
      <th>Content</th>
      <th>User</th>
      <th colspan="3"></th>
    </tr>
  </thead>

  <tbody>
    <% @posts.each do |post| %>
      <tr>
        <td><%= post.title %></td>
        <td><%= post.content %></td>
        <td><%= post.user %></td>
        <td><%= link_to 'Show', post %></td>
        <td><%= link_to 'Edit', edit_post_path(post) %></td>
        <td><%= link_to 'Destroy', post, method: :delete, data: { confirm: 'Are you sure?' } %></td>
      </tr>
    <% end %>
  </tbody>
</table>

<br>

<%= link_to 'New Post', new_post_path %>
```

To remove duplicated messaging functionality, delete code line No. 2.

And some CSS classes are inserted into <table> tag as follows:

`assets/stylesheets/posts.scss`

```scss
.card {
  table:last-child {
    margin-bottom: 0;
  }
}
```

`assets/stylesheets/application.scss`

```scss
@import "bootstrap";
@import "layouts";
@import "posts";
```

and finally this page looks like this:

```erb
<h1>Posts</h1>

<div class='card'>
  <table class='table'>
    <thead class='thead thead-default'>
      <tr>
        <th>Title</th>
        <th>Content</th>
        <th>User</th>
        <th colspan="3"></th>
      </tr>
    </thead>

    <tbody>
      <% @posts.each do |post| %>
        <tr>
          <td><%= post.title %></td>
          <td><%= post.content %></td>
          <td><%= post.user %></td>
          <td><%= link_to 'Show', post %></td>
          <td><%= link_to 'Edit', edit_post_path(post) %></td>
          <td><%= link_to 'Destroy', post, method: :delete, data: { confirm: 'Are you sure?' } %></td>
        </tr>
      <% end %>
    </tbody>
  </table>
</div>

<div class='form-actions'>
  <%= link_to 'New Post', new_post_path, class: 'btn btn-outline-primary' %>
</div>
```

![](http://i683.photobucket.com/albums/vv193/luciuschoi/building_my_blog/2016-10-11_06-49-08_zpseqowl6l3.png)

It looks ugly if no posts exists.

So you might modify source codes to show guide message as follows:

```erb
<tbody>
  <% if @posts.any? %>
    <% @posts.each do |post| %>
      <tr>
        <td><%= post.title %></td>
        <td><%= post.content %></td>
        <td><%= post.user %></td>
        <td><%= link_to 'Show', post %></td>
        <td><%= link_to 'Edit', edit_post_path(post) %></td>
        <td><%= link_to 'Destroy', post, method: :delete, data: { confirm: 'Are you sure?' } %></td>
      </tr>
    <% end %>
  <% else %>
    <tr>
      <td colspan="6">
        <p class='text-xs-center p-y-3'>No posts were published.</p>
      </td>
    </tr>
  <% end %>
</tbody>
```

![](http://i683.photobucket.com/albums/vv193/luciuschoi/building_my_blog/2016-10-11_06-59-39_zpsrudabnn1.png)

Yes, it looks more reasonable.

Let's click `New Post` button to access the new post form page.

![](http://i683.photobucket.com/albums/vv193/luciuschoi/building_my_blog/2016-10-11_08-56-54_zps68ulbpcv.png)

You need customize form partial template file (views/posts/_form.html.erb).

1. Change row count of content textarea to 5
2. Delete user select element. `user_id` attribute will be assigned to `current_user` in `create` action of posts controller
3. Within `.form-action` div tag, add `show` and `back` links

As a result, it looks as follow:

```erb
<%= simple_form_for(@post) do |f| %>
  <%= f.error_notification %>

  <div class="form-inputs">
    <%= f.input :title %>
    <%= f.input :content, input_html: { rows: 10 } %>
  </div>

  <div class="form-actions">
    <%= f.button :submit, class: 'btn btn-outline-primary' %>
    <%= link_to 'Show', @post, class: 'btn btn-outline-primary' if @post.persisted? %>
    <%= link_to 'Back', posts_path, class: 'btn btn-outline-primary' %>
  </div>
<% end %>
```

In code line No. 11, it will be more reasonable if `if @post.persisted?` condition is appended in the same code line.

Now, in the `create` action of posts controller, as mentioned before, `@post.user` is assigned current_user.

```ruby
def create
  @post = Post.new(post_params)
  @post.user = current_user       # added like this

  respond_to do |format|
    if @post.save
      format.html { redirect_to @post, notice: 'Post was successfully created.' }
      format.json { render :show, status: :created, location: @post }
    else
      format.html { render :new }
      format.json { render json: @post.errors, status: :unprocessable_entity }
    end
  end
end
```

```ruby
Started POST "/posts" for ::1 at 2016-10-11 18:24:50 +0900
Processing by PostsController#create as HTML
  Parameters: {"utf8"=>"✓", "authenticity_token"=>"UHPpB+BK5Mn+P1RiRrt3SsftQ0nSUDxl1vBurukLFLqaufSuUED8tyfj4geUeA2dzAD4l4kA+24ToK8WrD1a9Q==", "post"=>{"title"=>"Test Title", "content"=>"Compellingly promote best-of-breed e-services whereas professional applications. Uniquely deliver customized ideas rather than competitive scenarios. Seamlessly engage state of the art imperatives and just in time relationships. Assertively syndicate premier channels and granular deliverables. Dynamically develop wireless testing procedures and pandemic architectures.\r\n\r\nRapidiously maximize economically sound infrastructures for sticky total linkage. Assertively disseminate equity invested e-markets before multifunctional information. Authoritatively productivate future-proof processes through maintainable technologies. Conveniently whiteboard wireless internal or \"organic\" sources vis-a-vis adaptive value. Interactively orchestrate strategic platforms vis-a-vis equity invested functionalities.\r\n\r\nCompellingly extend 2.0 e-commerce with bleeding-edge technologies. Continually disintermediate alternative leadership skills via backward-compatible strategic theme areas. Enthusiastically reinvent multifunctional e-tailers via prospective potentialities. Authoritatively enable enterprise opportunities before effective services. Interactively leverage other's one-to-one catalysts for change before cost effective action items.\r\n\r\nAuthoritatively extend cost effective initiatives vis-a-vis top-line supply chains. Progressively fashion inexpensive meta-services through technically sound networks. Distinctively harness reliable value before timely niche markets. Collaboratively transition mission-critical resources before inexpensive niches. Progressively deliver bricks-and-clicks human capital with installed base networks.\r\n\r\nCredibly envisioneer interdependent users whereas multidisciplinary internal or \"organic\" sources. Authoritatively empower strategic networks whereas B2B architectures. Completely negotiate.", "user_id"=>""}, "commit"=>"Create Post"}
   (0.2ms)  BEGIN
   (0.1ms)  ROLLBACK
  Rendering posts/new.html.erb within layouts/application
  User Load (152.1ms)  SELECT "users".* FROM "users"
  Rendered posts/_form.html.erb (158.1ms)
  Rendered posts/new.html.erb within layouts/application (159.2ms)
  Rendered shared/_log_status.html.erb (0.7ms)
Completed 200 OK in 188ms (Views: 33.3ms | ActiveRecord: 152.4ms)
```

You will get the following error message if you submit the form filled with title and content data.

The reason is that `current_user` is not yet assigned because you are not yet signed in.

![](http://i683.photobucket.com/albums/vv193/luciuschoi/building_my_blog/2016-10-11_18-25-06_zpswgrnah6f.png)

To solve this problem, you should add `before_action :authenticate_user!` in the top of `posts` controller class.

```ruby
class PostsController < ApplicationController
  before_action :authenticate_user!
  before_action :set_post, only: [:show, :edit, :update, :destroy]

  ...
```

Now, if you refresh the post form page, it will redirect to the `Log in` page as follows:

![](http://i683.photobucket.com/albums/vv193/luciuschoi/building_my_blog/2016-10-11_18-41-38_zpseehmtahb.png)

But we need user authentication just for `new`, `create`, `edit`, `update`, and `destroy` actions except `index` and `show` actions.

So, if you want to, you can add `:only` option to `before_action` as follows:

```ruby
class PostsController < ApplicationController
  before_action :authenticate_user!, only: [ :new, :create, :edit, :update, :destroy]
  before_action :set_post, only: [:show, :edit, :update, :destroy]
```

Post resource was created and so we could change root path to "posts#index" in routes.rb file.

```ruby
Rails.application.routes.draw do
  root 'posts#index'
  resources :posts
  devise_for :users

end
```

Now that you solved this user authentication problem, let's try to log in again.

At this time, after logging in, you might see the `post` index page on root route.

![](http://i683.photobucket.com/albums/vv193/luciuschoi/building_my_blog/2016-10-11_19-23-08_zpshwy890yt.png)

In user-signed-in state, let's add a new post.

You will get the `show` action view page as follows:

![](http://i683.photobucket.com/albums/vv193/luciuschoi/building_my_blog/2016-10-11_19-29-28_zpscjczfahs.png)

As you can see, flash messages are show duplicated.

Let's customize `show` action view template as follows:

```erb
<h2><%= @post.title %></h2>
<small class='text-muted'>
  <%= @post.user.username %>,
  <%=l @post.created_at, format: :long %>
</small>

<p>
  <%= simple_format @post.content %>
</p>

<div class="form-actions">
  <%= link_to 'Edit', edit_post_path(@post) , class: 'btn btn-outline-primary'%>
  <%= link_to 'Back', posts_path, class: 'btn btn-outline-primary' %>
</div>
```

Yeah, it looks so smart.

![](http://i683.photobucket.com/albums/vv193/luciuschoi/building_my_blog/2016-10-11_19-52-59_zpsklkwtxtf.png)

At this point, we need update the `views/shared/_log_status.html.erb` file as follows:

```erb
<% if devise_controller? or action_name != 'index' %>
  <%= link_to "Home", root_path, class: 'btn btn-outline-primary d-block m-b-1' %>
<% end %>

<% if user_signed_in? %>
  <%= link_to "New Post", new_post_path, class: 'btn btn-outline-primary d-block m-b-1' %>
  <%= link_to "My Profile", edit_user_registration_path, class: 'btn btn-outline-primary d-block m-b-1' %>
  <%= link_to "Sign Out", destroy_user_session_path, method: :delete, class: 'btn btn-outline-primary d-block' %>
  <%= link_to "New Post", new_post_path, class: 'btn btn-outline-primary d-block' %>
<% else %>
  <%= link_to "Sign In", new_user_session_path, class: 'btn btn-outline-primary d-block m-b-1' %>
  <%= link_to "Sign Up", new_user_registration_path, class: 'btn btn-outline-primary d-block' %>
<% end %>
```

Let's modify the index view template file as follows:

```erb
<div class="posts">
  <%= render @posts %>
</div>
```

And you should create a partial template, so called `_post.html.erb`, as follows:

```erb
<article class="post">
  <div class='title'>
    <%= post.title %>
  </div>
  <div class="status text-xs-right">
    <small>
      <%= post.user.name %>,
      <%= localize post.created_at, format: :long %>
      <% if user_signed_in? && current_user == post.user %>
      	·
        <%= link_to "Edit", edit_post_path(post)  %>
      <% end %>
    </small>
  </div>
  <div class='content'>
    <p><%= simple_format truncate(post.content, length: 300) %></p>
    <p><%= link_to "Read more", post, class: "btn btn-primary btn-sm" if post.content.length > 300 %></p>
  </div>
</article>

```

You need create some styles in the `assets/stylesheets/posts.scss` file as follows:

```scss
.posts {
  article.post {
    margin-bottom: 1.5em;
    div.title {
      font-size: 2em;
      font-weight: bold;
      color: rgb(161, 161, 161)
    }
    div.content {
      padding-bottom: 1em;
    }
    div.status {
      border-top: 1px dashed #ccc;
      color: #ababab;
      margin-bottom: .5em;
    }
  }
}
```

And finally, the `index` page will look like this:

![](http://i683.photobucket.com/albums/vv193/luciuschoi/building_my_blog/2016-10-11_21-06-46_zpsmlgyd71o.png)

If the length of post content is more than 300 characters, `Read more` link will be shown at the bottom of each post.

![](http://i683.photobucket.com/albums/vv193/luciuschoi/building_my_blog/2016-10-11_21-11-26_zpsghmanivm.png)













---

References :

1. [How to Use The HTML5 Sectioning Elements](http://blog.teamtreehouse.com/use-html5-sectioning-elements)
2. [ARIA and Progressive Enhancement](http://alistapart.com/article/aria-and-progressive-enhancement/)
3. [Devise Strong Parameters](https://github.com/plataformatec/devise#strong-parameters)
