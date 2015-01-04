[![Gem Version](https://badge.fury.io/rb/databound.svg)](http://badge.fury.io/rb/databound)
[![Bower version](https://badge.fury.io/bo/databound.svg)](http://badge.fury.io/bo/databound)
[![NPM version](https://badge.fury.io/js/databound.svg)](http://badge.fury.io/js/databound)
[![Code Climate](https://codeclimate.com/github/Nedomas/databound/badges/gpa.svg)](https://codeclimate.com/github/Nedomas/databound)
[![Build Status](https://travis-ci.org/Nedomas/databound.svg)](https://travis-ci.org/Nedomas/databound)

![Databound](https://cloud.githubusercontent.com/assets/1877286/4743542/df89dcec-5a28-11e4-9114-6f383fe269cb.png)

Provides Javascript a simple CRUD API to the Ruby on Rails backend.

**Check out live examples on the Databound website** [databound.me](http://databound.me).

**Backend gem repo** [github.com/Nedomas/databound-rails](http://github.com/Nedomas/databound-rails).

## Usage

```js
  User = new Databound('/users')

  User.where({ name: 'John' }).then(function(users) {
    alert('Users called John');
  });

  User.find(15).then(function(user) {
   print('User no. 15: ' + user.name);
  });

  User.create({ name: 'Peter' }).then(function(user) {
   print('I am ' + user.name + ' from database');
  });
```

[More API docs](http://nedomas.github.io/databound/src/databound.html)

## Version support and dependencies

Works with:
- Ruby on Rails **3+**
- Ruby **2.0+**
- It can work with **Angular** as a better **ngResource** alternative
- ActiveRecord or Mongoid
- Works with [Active Model Serializers](https://github.com/rails-api/active_model_serializers)
- Chrome **any**, Firefox **any**, Opera **any**, IE **8+**

Depends on:
- Lodash (should work with any version)

## Installation

**1 - Gemfile**
```ruby
gem 'databound', '2.0.1'
```

**2.1 - With asset pipeline (sprockets)**

Run generator to add Databound to application.js
```sh
rails g databound:install
```

**2.2 - Without asset pipeline**

Download the [databound-standalone.js](https://raw.githubusercontent.com/Nedomas/databound/master/dist/databound-standalone.js) and load it up
```html
<script src='assets/databound-standalone.js'></script>
```

**2.3 - With require.js**

Download Javascript part with [npm](http://npmjs.com) or [bower](bower.io)

```sh
npm install databound
```

OR

```sh
bower install databound
```

Require it Javascript with:
```javascript
var Databound = require('databound');
```

**3 - Add a route to config/routes.rb**
```ruby
Rails.application.routes.draw do
  databound :users, permitted_columns: [:name, :city]
end
```

**4 - *(optional)* Controller is autogenerated from route**

But if you already have a controller, you can include Databound and specify the model yourself.
```ruby
class UsersController < ApplicationController
  include Databound

  private

  def model
    User
  end

  def permitted_columns
    [:name, :city]
  end
end
```

**5 - Use it in the Javascript**
```javascript
var User = new Databound('/users');
```

## Security

**Which parts can Javascript modify?**

Specify ``permitted_columns``. No columns are modifiable by default.

**How to secure the relation values?**

You can use ``dsl(:your_column, :expected_value)`` to only allow certain dsl values and convert them to relation ids in the backend.

**How to protect the scope of the modifiable records?**

Use ``permit_update_destroy?`` to check permissions.

**Which parts can Javascript show?**

Use [Active Model Serializers](https://github.com/rails-api/active_model_serializers) to serialize the record.

## Changelog

**2.0.1** - 2015-01-03

* Add support for specifying ``permitted_columns`` in ``routes.rb``. No columns are modifiable by default.

**1.1.0** - 2015-01-03

* You can specify ``permit_update_destroy?`` on a controller to manage the scope of the records that can be modified from the Javascript.

**1.0.0** - 2015-01-03

* Destroy now accepts ``id`` instead of ``{ id: someid }``.
* ``extra_find_scopes`` renamed to ``extra_where_scopes``

## Used and sponsored by

[![SameSystem](https://cloud.githubusercontent.com/assets/1877286/5602104/d8e44986-933f-11e4-8e64-b0c8e83a94d1.jpg)](http://samesystem.com) [![picnic-right](https://cloud.githubusercontent.com/assets/1877286/5602105/dab01272-933f-11e4-9aab-624ba81825d9.png)](http://spacepicnic.net)
