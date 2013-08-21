Rails method csrf_meta_tags, which prevents cross-site request forgery (CSRF), a type of malicious web attack.

Note that, in contrast to the plural convention for controller names, model names are singular: a Users controller, but a User model.) 

he table name is plural (users) even though the model name is singular (User), which reflects a linguistic convention followed by Rails:

Starting in Rails 4.0, the preferred method to find by attribute is to use the find_by method instead, passing the attribute as a hash:

>> User.find_by(email: "mhartl@example.com")

The update_attributes method accepts a hash of attributes, and on success performs both the update and the save in one step (returning true to indicate that the save went through). Note that if any of the validations fail, such as when a password is required to save a record (as implemented in Section 6.3), the call to update_attributes will fail. If we only need to update a single attribute, using the singular update_attribute bypasses this restriction:


This is the first time we’ve seen the command to create a test database with the correct structure:

$ bundle exec rake test:prepare

This just ensures that the data model from the development database, db/development.sqlite3, is reflected in the test database, db/test.sqlite3.9 (Failure to run this Rake task after a migration is a common source of confusion. In addition, sometimes the test database gets corrupted and needs to be reset. If your test suite is mysteriously breaking, be sure to try running rake test:prepare to see if that fixes the problem.)


In this case, we only have one validation, so we know which one failed, but it can still be helpful to check using the errors object generated on failure:

>> user.errors.full_messages
=> ["Name can't be blank"]
(The error message is a hint that Rails validates the presence of an attribute using the blank? method,

