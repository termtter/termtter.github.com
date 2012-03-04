---
layout: default
title: Termtter -Plugin-
---

# Writing Plugins

自分で作ったプラグインをロードするには ~/.termtter/plugins ディレクトリにファイルを配置し、
設定ファイル ~/.termtter/config に以下のような設定を追加します。

    ...
    Termtter::Client.init do |t|
      ...
      t.plug 'my_plugin'
      ...
    end
    ...

## Command

fib コマンドの例:

コマンドの登録には Termtter::Client.register_command メソッドを使います。

    Termtter::Client.register_command(
      :name => :fib,
      :exec => lambda {|arg|
        n = arg.to_i
        text = "fib(#{n}) = #{fib n}"
        Termtter::API.twitter.update(text)
        puts "=> " << text
      }
    )

## Hook

update コマンドで ERB を使えるようにするためのフックの例:

フックの登録には Termtter::Client.register_hook メソッドを使います。

    require 'erb'
    
    Termtter::Client.register_hook(
      :name => :erb,
      :point => :modify_arg_for_update,
      :exec => lambda {|cmd, arg|
        ERB.new(arg).result(binding)
      }
    )


## Filter

protected にしているユーザーを非表示にするためのフィルタの例:

フィルタはフックの一種です。普通のフックと同じように Termtter::Client.register_hook メソッドで登録します。

    Termtter::Client.register_hook(
      :name => :protected_filter,
      :point => :filter_for_output,
      :exec => lambda { |statuses, event|
        statuses.select { |s| !s.user.protected }
      }
    )

