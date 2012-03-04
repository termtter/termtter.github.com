---
layout: default
title: Termtter -Configuration-
---

# Configuration

~/.termtter/config is termtter configuration file.

for example:

    config.user_name = 'your id'
    config.password = 'your password'
    config.update_interval = 60
    
    # Proxy setting
    #config.proxy.host = 'proxy host'
    #config.proxy.port = '8080'
    #config.proxy.user_name = 'proxy user'
    #config.proxy.password = 'proxy password'

    # Call from Initilization.
    Termtter::Client.init do |t|
      # You can need use plugin
      t.plug 'growl'
      ... 
    end
