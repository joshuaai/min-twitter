# Command Help

## Create Rails project
`rails new min_twitter`

Add pg to the production group and sqlite to the development test group.
`bundle install --without production`

## Deploy to Heroku
It is never too early to deploy, so that you start testing features modularly in production.

* Add a hello action `def hello end` to the application_controller.rb file. And a text: `render html: "hello world"`.
* Make it the root route to the routes.rb file. `root application#hello`.
* `heroku create` 
* `git push heroku master` || [Heroku App](https://min-twitter.herokuapp.com/).
* `heroku apps:rename min-twitter`

## Models Logic (High-level)
```
rails generate scaffold User name:string email:string
rails generate scaffold Micropost content:text user_id:integer
rails db:migrate
```

* A user has an `id`, a `name` and an `email`.
* A micropost has an `id`, a `content` of type text and a `user_id`. A psot belongs to a user and a user has many posts.

## Model Validation and Associations
In the Micropost model, add:
```
belongs_to :user
validates :content, length: { maximum: 140 }
```

In User model, add:
```
has_many :microposts
rails db:migrate
heroku run rails db:migrate
```

This is possible because of the user_id column in the microposts table.

