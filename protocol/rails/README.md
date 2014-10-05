Rails Protocol
==============

A guide for writing great web apps.

Set Up Laptop
-------------

To set up your laptop you can use the thoughtbot laptop script:
[thoughtbot/laptop](https://github.com/thoughtbot/laptop)

It is also highly recommended to version your dotfiles. Here are some
interesting sources:
* https://dotfiles.github.io/
* https://github.com/thoughtbot/dotfiles
* https://github.com/thoughtbot/rcm
* https://github.com/holman/dotfiles


## !!! The following content has not been tested yet and should be revised once we create a new app !!!

Create App
----------

Get Suspenders.

    gem install suspenders

Create the app.

    suspenders app --heroku true --github organization/app

Set Up App
----------

Get the code.

    git clone git@github.com:organization/app.git

Set up the app's dependencies.

    cd project
    ./bin/setup

Use [Heroku config](https://github.com/ddollar/heroku-config) to get `ENV`
variables.

    heroku config:pull --remote staging

Delete extra lines in `.env`, leaving only those needed for app to function
properly. For example: `BRAINTREE_MERCHANT_ID` and `S3_SECRET`.

Use [Foreman](https://github.com/ddollar/foreman) to run the app locally.

    foreman start

It uses your `.env` file and `Procfile` to run processes just like Heroku's
[Cedar](https://devcenter.heroku.com/articles/cedar/) stack.

Git Protocol
------------

Follow the normal [Git Protocol](/protocol/git).

Code Review
-----------

Follow the normal [Code Review guidelines](/code-review). When reviewing others'
Rails work, look in particular for:

* Review data integrity closely, such as migrations that make irreversible
  changes to the data, and whether there is a related todo to make a database
  backup during the staging and production deploys.
* Review SQL queries for potential SQL injection.
* Review whether dependency upgrades include a reason in the commit message,
  such as a link to the dependency's `ChangeLog` or `NEWS` file.
* Review whether new database indexes are necessary if new columns or SQL
  queries were added.
* Review whether new scheduler (`cron`) tasks have been added and whether there
  is a related todo in the project management system to add it during the
  staging and production deploys.

Deploy
------

View a list of new commits. View changed files.

    git fetch staging
    git log staging/master..master
    git diff --stat staging/master

If necessary, add new environment variables.

    heroku config:add NEW_VARIABLE=value --remote staging
