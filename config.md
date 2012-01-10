Configuration

~/.termtter/config というファイルが Termtter のデフォルトの設定ファイルになります。
設定ファイルは以下のように記述します。

config.user_name = 'your id'
config.password = 'your password'
config.update_interval = 60

# プロキシ設定
#config.proxy.host = 'proxy host'
#config.proxy.port = '8080'
#config.proxy.user_name = 'proxy user'
#config.proxy.password = 'proxy password'

# 初期化時にここの処理が呼ばれます
Termtter::Client.init do |t|
  # 使用したいプラグインをここでロードします
  t.plug 'growl'
  ... 
end
