## Chitter Challenge ##

In which I created a working twitter clone named Chitter. Based of the cockatoos that I grew up with Chitter will take all tweets given by multiple users and then return them as capitals.

Chitter will store the information of the peeps (tweets) in a local database and it is possible in a SQL interface to list all avilable tweets by a certain user.

You can also sign up to Chitter, store you own peeps and even create some to be posted to the database.

This was all created using an MVC model and has been built on the front-end using HTML, controller side using Sinatra and Ruby and finally the database's are built using SQL and interfaced with via the rubygem 'pg'

To run Chitter you need to create the databases stored below (I will leave the details for the SQL code below) and rund bundle within the terminal. Finally launch the app either through the command 'rackup' or 'ruby app.rb'.

AND ENJOY!

## Database Creation SQL Commands ##

- Please note if run in test mode then the rspec/Capybara tests will look for a test database named 'chitter_test'

- users - In which all users are stored
CREATE TABLE "public"."users" (
    "id" int4 NOT NULL DEFAULT nextval('users_id_seq'::regclass),
    "email" varchar(60),
    "username" varchar(255),
    "realname" varchar(255),
    "passwrd" varchar(255),
    PRIMARY KEY ("id")
);

- peeps - In which all peep information is stored
CREATE TABLE "public"."peeps" (
    "id" int4 NOT NULL DEFAULT nextval('peeps_id_seq'::regclass),
    "created_at" timestamp DEFAULT CURRENT_TIMESTAMP,
    "user_id" int4,
    "peep" varchar(255) NOT NULL,
    CONSTRAINT "peeps_user_id_fkey" FOREIGN KEY ("user_id") REFERENCES "public"."users"("id"),
    PRIMARY KEY ("id")
    
## Notes on Progress ##
Created database tables user & peeps

Contain in user are 5 columns
- id- autoincrements to show user id - PRIMARY KEY
- email- stored as VARCHAR(255)
- passwrd - stored as VARCHAR(255)
- name - stored as VARCHAR(255)
- username - stored as VARCHAR(255)

Contained in peep table are 5 columns
- id- autoincramates to show peep id (might be an issue with test autoupdate)
- user_id - foreign key stored at int4 and references users::id - FOREIGN KEY
- created_at - should at initilization of peep autocreate a time stamp in TIMESTAMP format ie YYYY-MM-DD HH:MM:SS
- peep - The content of the peep itself stored in VARCHAR(255)

- ALSO added filepath requirements and named classes. Everything is required and bundled.

## Notes on Features ##

- Can add and access users by clicking the Sign Up button on the chitter homepage.
  - When a user is created all information is stored in user column and when returning to the page will be welcomed on the homepage.
- Can post peeps (tweets) and see them appear on the views page

Chitter Challenge
=================

* Challenge time: rest of the day and weekend, until Monday 9am
* Feel free to use Google, your notes, books, etc. but work on your own
* If you refer to the solution of another coach or student, please put a link to that in your README
* If you have a partial solution, **still check in a partial solution**
* You must submit a pull request to this repo with your code by 9am Monday morning

Challenge:
-------

As usual please start by forking this repo.

We are going to write a small Twitter clone that will allow the users to post messages to a public stream.

Features:
-------

```
STRAIGHT UP

As a Maker
So that I can let people know what I am doing  
I want to post a message (peep) to chitter

As a maker
So that I can see what others are saying  
I want to see all peeps in reverse chronological order

As a Maker
So that I can better appreciate the context of a peep
I want to see the time at which it was made

As a Maker
So that I can post messages on Chitter as me
I want to sign up for Chitter

HARDER

As a Maker
So that only I can post messages on Chitter as me
I want to log in to Chitter

As a Maker
So that I can avoid others posting messages on Chitter as me
I want to log out of Chitter

ADVANCED

As a Maker
So that I can stay constantly tapped in to the shouty box of Chitter
I want to receive an email if I am tagged in a Peep
```

Technical Approach:
-----

This week you integrated a database into Bookmark Manager using the `PG` gem and `SQL` queries. You can continue to use this approach when building Chitter Challenge.

If you'd like more technical challenge this weekend, try using an [Object Relational Mapper](https://en.wikipedia.org/wiki/Object-relational_mapping) as the database interface.

Some useful resources:
**DataMapper**
- [DataMapper ORM](https://datamapper.org/)
- [Sinatra, PostgreSQL & DataMapper recipe](http://recipes.sinatrarb.com/p/databases/postgresql-datamapper)

**ActiveRecord**
- [ActiveRecord ORM](https://guides.rubyonrails.org/active_record_basics.html)
- [Sinatra, PostgreSQL & ActiveRecord recipe](http://recipes.sinatrarb.com/p/databases/postgresql-activerecord?#article)

Notes on functionality:
------

* You don't have to be logged in to see the peeps.
* Makers sign up to chitter with their email, password, name and a username (e.g. samm@makersacademy.com, password123, Sam Morgan, sjmog).
* The username and email are unique.
* Peeps (posts to chitter) have the name of the maker and their user handle.
* Your README should indicate the technologies used, and give instructions on how to install and run the tests.

Bonus:
-----

If you have time you can implement the following:

* In order to start a conversation as a maker I want to reply to a peep from another maker.

And/Or:

* Work on the CSS to make it look good.

Good luck and let the chitter begin!

Code Review
-----------

In code review we'll be hoping to see:

* All tests passing
* High [Test coverage](https://github.com/makersacademy/course/blob/master/pills/test_coverage.md) (>95% is good)
* The code is elegant: every class has a clear responsibility, methods are short etc.

Reviewers will potentially be using this [code review rubric](docs/review.md).  Referring to this rubric in advance may make the challenge somewhat easier.  You should be the judge of how much challenge you want this weekend.

Automated Tests:
-----

Opening a pull request against this repository will will trigger Travis CI to perform a build of your application and run your full suite of RSpec tests. If any of your tests rely on a connection with your database - and they should - this is likely to cause a problem. The build of your application created by has no connection to the local database you will have created on your machine, so when your tests try to interact with it they'll be unable to do so and will fail.

If you want a green tick against your pull request you'll need to configure Travis' build process by adding the necessary steps for creating your database to the `.travis.yml` file.

- [Travis Basics](https://docs.travis-ci.com/user/tutorial/)
- [Travis - Setting up Databases](https://docs.travis-ci.com/user/database-setup/)

Notes on test coverage
----------------------

Please ensure you have the following **AT THE TOP** of your spec_helper.rb in order to have test coverage stats generated
on your pull request:

```ruby
require 'simplecov'
require 'simplecov-console'

SimpleCov.formatter = SimpleCov::Formatter::MultiFormatter.new([
  SimpleCov::Formatter::Console,
  # Want a nice code coverage website? Uncomment this next line!
  # SimpleCov::Formatter::HTMLFormatter
])
SimpleCov.start
```

You can see your test coverage when you run your tests. If you want this in a graphical form, uncomment the `HTMLFormatter` line and see what happens!
