---
layout: default
title: Termtter -Plugin-
---

# Writing Plugins

Put your own plugin file under ~/.termtter/plugins and add the following lines
to load it.

    ...
    Termtter::Client.init do |t|
      ...
      t.plug 'my_plugin'
      ...
    end
    ...

## Command

An example with fib plugin:

Use Termtter::Client.register\_command method to add a new command.

    Termtter::Client.register_command(
      name: :fib,
      exec: lambda {|arg|
        n = arg.to_i
        text = "fib(#{n}) = #{fib n}"
        Termtter::API.twitter.update(text)
        puts "=> " << text
      })

## Hook

An example of a hook to make ERB available in update command:

Use Termtter::Client.register\_hook method to add a hook.

    require 'erb'
    
    Termtter::Client.register_hook(
      name: :erb,
      point: :modify_arg_for_update,
      exec: lambda {|cmd, arg|
        ERB.new(arg).result(binding)
      })


## Filter

An example of a filter for hiding protected users:

A filter is a kind of a hook; use Termtter::Client.register\_hook just like adding a hook.

    Termtter::Client.register_hook(
      name: :protected_filter,
      point: :filter_for_output,
      exec: lambda {|statuses, event|
        statuses.reject {|s| s.user.protected }
      })

