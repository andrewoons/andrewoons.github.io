---
layout: post
title:  "How to define Sequelize assocations using migrations"
date:   2017-11-23 19:21:00 +0100
categories: sequelize
---
The Sequelize CLI is pretty great at generating model and migration files, but not at adding associations with other models.

Unfortunately there is not much (clear) documentation about adding associations in migration files — so whilst figuring this out myself I decided to write down to basic examples for the 4 types of associations to save others the time.

### Creating models
I suggest creating all models first, and then adding associations in a separate migration file. This prevents errors surrounding models that do not exist yet. For me, this has proven to be the easiest way to get the database up to an initial state.

Example order of files:

- create-tags.js
- create-products.js
- create-orders.js
- create-customers.js
- create-payments.js
- add-associations.js

Create all the models and their migrations using `sequelize model:generate`.

To check if the models are created correctly I suggest running `sequelize db:migrate` and seeing if there any errors.

**Note:** if you get an error saying the ‘Dialect needs to be explicitly supplied as of v4.0.0’, export the NODE_ENV of your configuration first, e.g. `export NODE_ENV="local"`.

If there are no errors, we can move on to the next step.

### Adding associations
Depending on the size of your project you can split up the associations for each model, or have all of them in one file. When starting a project, I like to do them all in one file, but it’s up to personal preference and how many associations each model has.

First, let’s create the migration file where we will be doing all the associations: `sequelize migration:generate --name add-associations`.

#### belongsTo
According to the [documentation](https://sequelize.readthedocs.io/en/latest/api/associations/) a belongsTo relation *‘adds a foreign key and singular association mixins to the source’*.

In our example an `Order` belongs to a `Customer`. In this case, the source is `Order` so we will need to add a `CustomerId` key to the `Order` table.

{% gist 363393782d412720a29938f983645bce order.js %}

**Note**: I’m using UUID’s for my ids. If you use the standard integers change the type to `DataTypes.INTEGER`, remove the `defaultValue` line and change `autoIncrement` to `true`.

In our migration file we will need to add a column called `CustomerId`. This can be done using the `queryInterface.addColumn` method. We also need to provide a `down` function that will return the database to the state before the migration.

{% gist b01404bbb5550ec7ae21e0daf7ea27b9 add-associations.js %}

A couple of things to notice here:

- Table names are plural and the reference key is exactly like the key used when defining the models (most of the time it will be `id`).
- The foreign key is capitalized.
- We’re also defining `onUpdate` and `onDelete`. The default is `CASCADE` for update and `SET NULL` for delete for belongsTo, hasOne and hasMany. BelongsToMany associations will have `CASCADE` as default for both update and delete.

**Note**: if you’re using integers instead of UUID’s use `type: Sequelize.INTEGER`.

Save and run `sequelize db:migrate`. If all is well, let’s run `sequelize db:migrate:undo` to check if the undo function works too.

#### hasOne
When defining a hasOne relation ‘the foreign key is added on the target’.

In our example `Payment` has `oneOrder`. `Order` is the target so we will need to add a `PaymentId` key to the `Order` model.

{% gist 8622782c4ba28e17d31a83b2ff8b2b8d payment.js %}

Let’s add our migration of the hasOne key. We’re appending that migration to add-associations.js so the complete file will look like this:

{% gist e13ecddce48016b0184478cebe4d7fe3 add-associations.js %}

Notice that we are chaining the `queryInterface` methods because they return Promises.

Let’s run `sequelize db:migrate` again. If there are no errors run `sequelize db:migrate:undo` to check if our down function also works.

#### hasMany
A hasMany association *“creates a 1:m association between the source and the provided target.* The foreign key is added on the target.”

In our example an `Order` has many `Products`. Let’s update our `order.js` model file.

{% gist 90d19fb1beec62f4e9449a32c85dfa83 order.js %}

We just added line 16 where we define the hasMany relation.

Now we need to add the `OrderId` column to the `Products` table in the migration file:

{% gist bc8f938dcd119f4d6c0d03a9f1b223ba add-associations.js %}

Pretty straight-forward :)

#### belongsToMany
This is where it gets slightly more complicated. *A belongsToMany relation creates a n:m association through a join table.*

In our example a `Product` belongs to many `Tag`s and vice versa. Here are the model definitions:

{% gist a8df7fb9016840f2214cf9164a15fb18 product.js %}

{% gist a8df7fb9016840f2214cf9164a15fb18 tag.js %}

Notice the following:

- we are defining `through: 'ProductTags'`. This defines that we are storing the n:m association in the `ProductTags` table.
- we are defining the belongsToMany association in **both** models using the same through.

To keep things more concise I’ll create a new migration file for this association by running `sequelize migration:generate --name associate-product-tag`.

Instead of `queryInterface.addColumn` we now need to use `queryInterface.createTable`.

{% gist dae22a780224e1d888c11110add36f42 associate-product-tag.js %}

This table doesn’t need an `id` key. Please note that `ProductId` and `TagId` are both primary keys. For the `down` function we’re just dropping the table again.

Run `sequelize db:migrate` again and see if it works. Don’t forget to test the down function by running `sequelize db:migrate:undo`.

### Done
That’s it! I hope these basic examples help and save you some time. If you have any questions don’t hesitate to ask.

