---
layout: post
title: "Getting Started with Ruby on Rails"
date: 2013-09-21 00:35
comments: true
categories: [ruby, rails, ruby on rails, linux, web development]
author: Junerey Casuga
---
I've introduced to you already what Ruby on Rails is and I've also given you the very basic knowledge on the Ruby language itself. So it's now time to develop something with Rails.

<!--more-->

###Installation
Let's assume that you've already installed Ruby. If not, you can refer to my previous blog. To install rails, just fire up your terminal and run this command:

{% codeblock %}
gem install rails
{% endcodeblock %}

Alright! We already have Rails so let's move on!

###Creating a WebApp
Now that we already have Rails, we can now create a very simple CRUD web application using Rails. To initialize your project, enter this command to your terminal:

{% codeblock %}
rails new testApp
{% endcodeblock %}

As we can see, initializing a new appliction with Rails is very easy. We just told Rails to create a new application called <b><i>'testApp'</i></b>. Upon telling Rails to create new application, it also creates the files and directories that you will need for development. After Rails has created your files, it also automatically runs the `bundle install` command to get your app dependencies.

###The Rails directory structure
Before we proceed with some coding, we must first know what's inside our Rails app directory.

{% img /images/ruby_on_rails/rails_dir.png %}

On the Rails directory, you can see there is the <i>/public</i> folder. This folder contains all static files you need like your <i>404</i> page, <i>robots.txt</i>, and your favicon.

Another folder which is very important in your Rails directory is the <i>/app</i> folder. This is where you will consume almost 97% of your development. This folder contains:

*	<b><i>app/assets</i></b>

	- The /assets folder contains your images, css, and javascripts.
*	<b><i>app/controllers</i></b>

	- This  is where Rails will find all of your controller classes.
*	<b><i>app/helpers</i></b>

	- This folder contains the helper classes used to assist the model, view, and controller classes.
*	<b><i>app/models</i></b>

	- This contains the model classes for your Rails app.
*	<b><i>app/views</i></b>

	- This contains the view templates which is basically what the user sees on their screen.

In the directory, we also have this `Gemfile`. The Gemfile is where you put all the dependencies you need for your app.

###Runing your Rails app
We've already created our rails app a while ago. So let's try to make it work. First of all, you must know how to run your Rails server. To run your server just run `rails server` or simply `rails s`. Upon raining your Rails server, you can now check your rails app on your browser usng `localhost:3000` as the address. If it runs properly, you should see something like this:

{% img /images/ruby_on_rails/rails_welcome.png %}


###Creating our first Rails app
Alright! We have our Rails app running on our browser. Now what? So let's make our Rails app working. Hmm. Let's make something that works with CRUD. How about an inventory of products? Alright, let's do it!

####Generating our model
As Rails suggested on our app, we must create a model and controller to get this rolling. I'll assume that you already know the concept of MVC pattern so we can move on to development.

To create a model, use this syntax: `rails g model NAME [field[:type]]`. Let's now create the model for our app. So a product can have its name, description, price, and category. Let us now generate them.

{% codeblock %}
rails g model product title:string description:text price:float
{% endcodeblock %}

{% img /images/ruby_on_rails/rails_model.png %}

Now Rails created a model class for us. Not just that, it also made us a migration file. Now let's migrate our database:

{% codeblock %}
rake db:migrate
{% endcodeblock %}

<small>*By default, Rails is using SQLite3 for database.</small>

####Generating our controller

Alright! We already have our model so let us now create our controller. To create a controller on Rails, just run `rails g controller controller_name [controller_actions]`. So let's make a controller named as <b>products</b>. We're creating a CRUD application so let us make actions for it. Let us run `rails g controller products index new show edit` on your terminal.

{% img /images/ruby_on_rails/rails_controller.png %}

What we just did? When we told Rails to generate a controller named as <b>products</b>, it created the controller class itself at `app/controllers/products_controller.rb`. It also created the view files for our controller and the routes for the actions we defined. And it also created test units, helpers, a coffeescript and scss file for the specific controller.

####Routes
Okay! We already have our controller, so let's go to `localhost:3000/products`. I bet you got an error :P It's because we did not define the <b>products</b> controller on the resource in our routes yet. So let's configure our routes by inserting the below code under `config/routes.rb` file:

{% codeblock Routes - routes.rb %}
resources :products
{% endcodeblock %}

If you want to make the products controller to be the root page, just add this to `routes.rb` file:

{% codeblock Routes - routes.rb %}
root 'products#index'
{% endcodeblock %}

So from now on when we access `localhost:3000`, it automatically uses the products controller and its index action. 

####CRUD
Alright! We now have our controller and our model. Let's move on to get it working.

Let's say we want to display all data from our database on our <i>index</i> action. To do that, let's edit our index action:

{% codeblock Products Controller - products_controller.rb %}
...
	def index
		@products = Product.all
	end
...
{% endcodeblock %}

What we did here is we defined our index controller and inside of it, we declared a variable that can be accessed by our views which is the `@products`. Then our `@products` controller is getting all the data from `Product` model. After telling our index controller what to do, let us now edit the `index.html.erb` file from our `views/products` directory.

{% codeblock index.html.erb %}
<h1>All Products</h1>

<ul>
	<% @products.each do |p| %>
	<li>
		<h3><%= p.title %></h3>
		<small><%= number_to_currency(p.price) %></small>
		<p><%= p.description %></p>
	</li>
	<% end %>
</ul>
{% endcodeblock %}

By default, Rails is using erb as its template engine. That's why that our `index.html` has a `.erb` extension. There are other template engines for Rails like HAML. On our `index.html.erb` file, we looped through each data from the model and displayed it into a list. The `number_to_currency` function converts a number to a currency format.

After editing our index action an our index view, let us refresh our page. It shows nothing right? Because we don't have any data from our database yet. So let's make a function on the products controller for creating data on our database.

{% codeblock products_controller.rb %}
...
	def new
		@product = Product.new
	end
...

...
	def create
		@prodct = Product.new(params[:product].permit(:title, :price, :description))
		@product.save
		redirect_to products_path
	end
...
{% endcodeblock %}

As you see, we defined two different actions. The <i>new </i> action and the <i>create</i> action. The <i>new</i> action is responsible for returning the HTML form for creating a product. And the <i>create</i> action does the saving of the data and redirects us to the producs_path (products/index) after saving the data. We now have our function, let's create our form on the `new.html.erb` file from the views.

{% codeblock new.html.erb %}
<h1>Create Product</h1>

<%= form_for @product, url: products_path do |f| %>
	<p>
		<%= f.label :title %>
		<%= f.text_field :title %>
	</p>
	<p>
		<%= f.label :price %>
		<%= f.text_field :price %>
	</p>
	<p>
		<%= f.label :description %>
		<%= f.text_field :description %>
	</p>
	<p><%= f.submit %></p>
<% end %>
{% endcodeblock %}

Okay! We now have our view. So let's try to create a product:

{% img /images/ruby_on_rails/rails_create.png %}

After creating a product, it should redirect you to the products page showing something like this:

{% img /images/ruby_on_rails/rails_index.png %}

Okay! It worked! We can now add products as much as we want. Let's try adding a link in our `index.html.erb` for viewing a specific product and a link for adding a product.

{% codeblock index.html.erb %}
<h1>All Products</h1>

<%= link_to "Add Prodct", new_product_path %>
<ul>
	<% @products.each do |p| %>
	<li>
		<h3><%= link_to p.title, product_path(p) %></h3>
		<small><%= number_to_currency(p.price) %></small>
		<p><%= p.description %></p>
	</li>
	<% end %>
</ul>
{% endcodeblock %}

Alright, we now have a link for creating a new product and a link for viewing a specific product. Let us now edit our controller and the `show.html.erb` file for displaying the details of a specific product. We should edit the <i>show</i> action on our controller first:

{% codeblock products_controller.rb %}
...
	def show
		@product = Product.find(params[:id])
	end
...
{% endcodeblock %}

Next is the view:

{% codeblock show.controller.rb %}
<h1>Product ID #<%= @product.id %></h1>
<%= link_to "Back to Products", @product_path %>

<h3><%= @product.title %></h3>
<small><%= number_to_currency(@product.price %></small>
<p><%= product.description %></p>
<p><%= link_to "Edit", edit_product_path(@product)</p>
{% endcodeblock %}

Now if we click the title of the product, it should bring you to a page like this: 

{% img /images/ruby_on_rails/rails_show.png %}

As you can see, we also added a link for editing this specific product. Let's now move on for the editing of specific product. Let us again edit our products controller.

{% codeblock products_controller.rb %}
...
	def edit
		@product = Product.find(params[:id])
	end
...

...
	def update
		if @product = Product.find(params[:id])
			@product.update_attributes(params[:product].permit(:title, :price, :description))
		end
		redirect_to products_path
	end
...
{% endcodeblock %}

We now have the function, let's make the view for editing:

{% codeblock edit.html.erb %}
<h1>Edit Product ID #<%= @prouct.id %></h1>
<%= link_to "Back to Products", product_path %>

<%= form_for @product do |f| %>
	<p>
		<%= f.label :title %>
		<%= f.text_field :title %>
	</p>
	<p>
		<%= f.label :price %>
		<%= f.text_field :price %>
	</p>
	<p>
		<%= f.label :description %>
		<%= f.text_field :description %>
	</p>
	<p>
		<%= f.submit %>
		<%= link_to "Delete", product_path(@product), :method=>:delete %>
	</p>
<% end %>
{% endcodeblock %}

Yeap! It does look like with our `new.html.erb`. We just removed the `url: products_path` from the form. So if we clicked the <i>Edit</i> link from the show page, it should bring you to the edit page showing the form and you should be able to edit it.

{% img /images/ruby_on_rails/rails_edit.png %}

As you can see, we've also added a link for deleting the product. It won't work yet because we haven't added the function for it yet. So let us add it now. Let us edit again our product controller.

{% codeblock products_controller.rb %}
...
	def destroy
		if @product = Product.find(params[:id])
			@product.delete
		end
		redirect_to products_path
	end
...
{% endcodeblock %}

###Conclusion
On this article, we've learned how to create a new Rails app and how to do CRUD using Rails. It's now your turn to do some more experimentation on Rails. Thanks for reading my post.
