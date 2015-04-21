# DodontofSakuraRental
さくらのレンタルサーバにRuby 2.1をインストールしてどどんとふを動かす

スタンダードプラン以上が必要、Ruby 2.2 系は rbenv でのインストールに失敗する。
gitのインストール
cd
wget --no-check-certificate https://git-core.googlecode.com/files/git-1.9.0.tar.gz
tar zxvf git-1.9.0.tar.gz
cd git-1.9.0
./configure --prefix=$HOME --enable-pthreads=-pthread --with-curl=/usr/local
gmake && gmake install

rbenvのインストール
cd
git clone https://github.com/sstephenson/rbenv.git ~/.rbenv
mkdir ~/.rbenv/plugins
git clone https://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build

Rubyのインストール（rbenv使用）
※ 2.1.5 の部分は現在の最新版に読み替えてください。
cd
cd .rbenv/bin
setenv TMPDIR $HOME/tmp
setenv MAKE gmake
./rbenv install 2.1.5

Rubyのバージョン確認
※ 2.1.5 の部分は現在の最新版に読み替えてください。
$HOME/.rbenv/versions/2.1.5/bin/ruby -v
->ruby 2.1.5p273 (2014-11-13 revision 48405) [x86_64-freebsd9.1]

msgpackインストール
※ 2.1.5 の部分は現在の最新版に読み替えてください。
$HOME/.rbenv/versions/2.1.5/bin/gem install msgpack

DodontoFServer.rbのシェバン行の変更
※ 2.1.5 の部分は現在の最新版に読み替えてください。
一行目を
#!/home/あなたのユーザ名/.rbenv/versions/2.1.5/bin/ruby
に変更。

config_local.rbに以下を追記してmsgpackを有効に
$isMessagePackInstalled = true

追記（bashを使う）
bashが使えるので .bashrc に

echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc
echo 'export TMPDIR=$HOME/tmp' >> ~/.bashrc
echo 'export MAKE=gmake' >> ~/.bashrc

して

bash

必要なら

source ./.bashrc

で bash に切り替えるほうがラク。

rbenv の更新（bashでやった）
git clone https://github.com/rkh/rbenv-update.git ~/.rbenv/plugins/rbenv-update

でプラグインをインストール。

rbenv update

で rbenv をアップデート。




参考
https://gist.github.com/saronpasu/10796448
http://http://www.machu.jp/diary/20130622.html
http://aics-app.sakura.ne.jp/blog/2015/01/17/ruby-rails%E3%82%92%E3%83%AC%E3%83%B3%E3%82%BF%E3%83%AB%E3%82%B5%E3%83%BC%E3%83%90%E3%83%BC%E3%81%AB%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB/

