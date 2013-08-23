Rails method csrf_meta_tags, which prevents cross-site request forgery (CSRF), a type of malicious web attack.

Note that, in contrast to the plural convention for controller names, model names are singular: a Users controller, but a User model.) 

he table name is plural (users) even though the model name is singular (User), which reflects a linguistic convention followed by Rails:

Starting in Rails 4.0, the preferred method to find by attribute is to use the find_by method instead, passing the attribute as a hash:

>> User.find_by(email: "mhartl@example.com")

The update_attributes method accepts a hash of attributes, and on success performs both the update and the save in one step (returning true to indicate that the save went through). Note that if any of the validations fail, such as when a password is required to save a record (as implemented in Section 6.3), the call to update_attributes will fail. If we only need to update a single attribute, using the singular update_attribute bypasses this restriction:


This is the first time we’ve seen the command to create a test database with the correct structure:

$ bundle exec rake test:prepare

This just ensures that the data model from the development database, db/development.sqlite3, is reflected in the test database, db/test.sqlite3.9 (Failure to run this Rake task after a migration is a common source of confusion. In addition, sometimes the test database gets corrupted and needs to be reset. If your test suite is mysteriously breaking, be sure to try running rake test:prepare to see if that fixes the problem.)


Because we have already properly prepared the test database with rake test:prepare, the tests should pass:

>> user.errors.full_messages
=> ["Name can't be blank"]
(The error message is a hint that Rails validates the presence of an attribute using the blank? method,

Here the regex VALID_EMAIL_REGEX is a constant, indicated in Ruby by a name starting with a capital letter.

nother example of the RSpec boolean convention we saw in Section 6.2.1: whenever an object responds to a boolean method foo?, there is a corresponding test method called be_foo. 

FORM_FOR

Let’s break this down into pieces. The presence of the do keyword indicates that form_for takes a block with one variable, which we’ve called f for “form”:

<%= form_for(@user) do |f| %>
  .
  .
  .
<% end %>
As is usually the case with Rails helpers, we don’t need to know any details about the implementation, but what we do need to know is what the f object does: when called with a method corresponding to an HTML form element—such as a text field, radio button, or password field—it returns code for that element specifically designed to set an attribute of the @user object. In other words,

<%= f.label :name %>
<%= f.text_field :name %>
creates the HTML needed to make a labeled text field element appropriate for setting the name attribute of a User model.

<<<<<<< HEAD
========================

Rails 4 has secure form submission Hoooray!!!!!

====================

This hash gets passed to the Users controller as params, and we saw starting in Section 7.1.2 that the params hash contains information about each request. In the case of a URL like /users/1, the value of params[:id] is the id of the corresponding user (1 in this example). In the case of posting to the signup form, params instead contains a hash of hashes, a construction we first saw in Section 4.3.3, which introduced the strategically named params variable in a console session. The debug information above shows that submitting the form results in a user hash with attributes corresponding to the submitted values, where the keys come from the name attributes of the input tags.

 this is not the final implementation. The reason is that initializing the entire params hash is extremely dangerous—it arranges to pass to User.new all data submitted by a user. In particular, suppose that, in addition to the current attributes, the User model included an admin attribute used to identify administrative users of the site. (We will implement just such an attribute in Section 9.4.1.) The way to set such an attribute to true is to pass the value admin=’1’ as part of params[:user], a task that is easy to accomplish using a command-line HTTP client such as curl. The result would be that, by passing in the entire params hash to User.new, we would allow any user of the site to gain administrative access by including admin=’1’ in the web request.

Previous versions of Rails used a method called attr_accessible in the model layer to solve this problem, but as of Rails 4.0 the preferred technique is to use so-called strong parameters in the controller layer. This allows us to specify which parameters are required and which ones are permitted. In addition, passing in a raw params hash as above will cause an error to be raised, so that Rails applications are now immune to mass assignment vulnerabilities by default.
=======



===================

Rails console test
rails console production

As with the console, development is the default environment for the local Rails server, but you can also run it in a different environment:

  $ rails server --environment production


If you view your app running in production, it won’t work without a production database, which we can create by running rake db:migrate in production:

  $ bundle exec rake db:migrate RAILS_ENV=production

(I find it confusing that the console, server, and migrate commands specify non-default environments in three mutually incompatible ways, which is why I bothered showing all three.)
>>>>>>> user-signup


the authenticity token, which Rails automatically includes to thwart a particular kind of attack called a cross-site request forgery (CSRF).

As we’ll see in Section 7.4, the key to creating a user is the special name attribute in each input:

<input id="user_name" name="user[name]" - - - />
.
.
.
<input id="user_password" name="user[password]" - - - />
These name values allow Rails to construct an initialization hash (via the params v

Initializing the entire params hash is extremely dangerous—it arranges to pass to User.new all data submitted by a user. In particular, suppose that, in addition to the current attributes, the User model included an admin attribute used to identify administrative users of the site. (We will implement just such an attribute in Section 9.4.1.) The way to set such an attribute to true is to pass the value admin=’1’ as part of params[:user], a task that is easy to accomplish using a command-line HTTP client such as curl. The result would be that, by passing in the entire params hash to User.new, we would allow any user of the site to gain administrative access by including admin=’1’ in the web request.

Previous versions of Rails used a method called attr_accessible in the model layer to solve this problem, but as of Rails 4.0 the preferred technique is to use so-called strong parameters in the controller layer. This allows us to specify which parameters are required and which ones are permitted. In addition, passing in a raw params hash as above will cause an error to be raised, so that Rails applications are now immune to mass assignment vulnerabilities by default.

params.require(:user).permit(:name, :email, :password, :password_confirmation) :password_confirmation)
    end

By the way, all of these methods—count, empty?, and any?—work on Ruby arrays as well. 

config.force_ssl = true