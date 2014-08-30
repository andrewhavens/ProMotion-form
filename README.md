# ProMotion-form

[![Gem Version](https://badge.fury.io/rb/ProMotion-form.svg)](http://badge.fury.io/rb/ProMotion-form) [![Build Status](https://travis-ci.org/clearsightstudio/ProMotion-form.svg)](https://travis-ci.org/clearsightstudio/ProMotion-form) [![Code Climate](https://codeclimate.com/github/clearsightstudio/ProMotion-form.png)](https://codeclimate.com/github/clearsightstudio/ProMotion-form)

ProMotion-form provides a PM::FormScreen for the
popular RubyMotion gem [ProMotion](https://github.com/clearsightstudio/ProMotion).

![form](http://clrsight.co/jh/Screen_Shot_2014-08-29_at_4.03.13_PM.png?+)

## Installation

```ruby
gem 'ProMotion-form'
```

Then:

```sh-session
$ bundle
$ rake pod:install
```

## Usage

Easily create a form screen. Powered by the CocoaPod [FXForms](https://github.com/nicklockwood/FXForms).

*Has all the methods of PM::Screen*

```ruby
class MyFormScreen < PM::FormScreen
  title "My Form"

  def form_data
    [{
      title: "Account Information",
      cells: [{
        name: "email",
        title: "ID",
        type: :email,
        value: current_user.email,
      }, {
        name: "password",
        title: "Password",
        type: :password,
        value: ""
      }]
    }]
  end

end
```

### Why not Formotion?

We've used and like Formotion for some form-heavy apps, but it's a rather bulky gem. ProMotion-form works better with ProMotion and is a lot lighter.

---

### Methods

#### form_data

Method that is called to build the form.

```ruby
class AccountScreen < PM::FormScreen
  title "Account Info"

  def form_data
    [{
      title: "Account Information",
      cells: [{
        name: "email",
        title: "ID",
        type: :email,
        value: current_user.email,
      }, {
        name: "password",
        title: "Password",
        type: :password,
        value: ""
      }, {
        name: :submit,
        title: "Submit",
        action: "my_action:"
      }]
    }]
  end

  def my_action(cell)
    # cell is the calling cell, in this case the Submit cell
    render_form # use to save the data
  end
end
```

All possible properties:

```ruby
{
  label: "Name", # or title:
  name: :name, # required
  type: :string, # :default is default...
  options: [ "Water", "Fire", "Wind" ], # for :option type
  placeholder: "Your name",
  default: "Jamon",
  value: "Jamon Holmgren",
  action: :"my_action:" # use symbol literal with trailing colon
}
```

##### Types of fields:

* `:default`
* `:label`
* `:text`
* `:longtext`
* `:url`
* `:email`
* `:phone`
* `:password`
* `:number`
* `:integer`
* `:unsigned`
* `:float`
* `:bitfield`
* `:boolean`
* `:option`
* `:date`
* `:time`
* `:datetime`
* `:image`


#### update_form_data

Forces a reload of the form.

#### render_form

Returns a hash of the fields and values.

```ruby
render_form # => {:email=>"jkdflsljkdsfad", :password=>"asdfadsfadsf", :submit=>""}
```

#### dismiss_keyboard

Dismisses the keyboard. Note that you may need to call this before `render_form` to ensure that you capture the input from the currently focused form element.

---

### Class Methods

None yet.

---

### Accessors

#### form_object (read only)

This is a Struct with a `#fields` method (what is used to build the form in FXForms) and writeable properties for each field.

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Make some specs pass
5. Push to the branch (`git push origin my-new-feature`)
6. Create new Pull Request
