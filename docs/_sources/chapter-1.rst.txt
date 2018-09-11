Flask + Flask-SQLAlchemy のチュートリアルを日本語で (Hello World! 編)
=======================================================================

はじめに
----------

Python で Web サービスを開発したいとき、皆さんは何のフレームワークを使いますか？？

Django?

Flask?

Pyramid?

とりあえず、私は Flask が大好きです！ Django も趣味程度で触ってましたが、やはり Flask のあの良い感じに軽い感じが、とても好きです。(ものすごく非論理的。)

さて、そんな Flask で Web サービスを開発する場合、データベースアクセスの部分は Flask-SQLAlchemy を利用することが多いと思いますが、それらをまとめたチュートリアルで日本語で書かれているものってかなり少ないんですよね・・・。英語が全く抵抗なく読める方は問題ないんですが、英語を見ただけでブラウザをそっ閉じするようなタイプの方には、なかなかハードルが高い感じになっています。

そこで！ 新たに Flask + Flask-SQLAlchemy を学びたいと考えている方に向けて、日本語でチュートリアル的な何かを書いてみようと思います。コレをきっかけに、1人でも Flask 好きが増えてくれたら嬉しい限りです。

当記事では、なるべくファイル数やモジュール数を減らし、全体像の理解を最優先に考えています。分かり難い箇所などありましたら、お気軽にコメントいただければと思います。

なお、以下の公式ドキュメントをかなり参考にしています。

Tutorial — Flask Documentation (0.12)

Quickstart — Flask-SQLAlchemy Documentation (2.3)

環境、主要なバージョン情報
----------------------------

* Python : 3.6.2

* Flask : 0.12.2

* Flask-SQLAlchemy : 2.3.2

OS は Windows でも Mac でも問題ないはずです。当記事では Mac を利用しています。

各種インストール
------------------

Python をインストールします。

Download Python | Python.org

Flask をインストールします。

pip install flask

Flask-SQLAlchemy をインストールします。

pip install flask-sqlalchemy

Flask で Hello World!
-----------------------

作業用に flask-tutorial ディレクトリを作成します。以後、同ディレクトリ内で作業します。

以下のコードを hello.py として作成します。

.. code-block:: python

   from flask import Flask
   
   app = Flask(__name__)
   
   @app.route('/')
   def hello():
       return 'Hello World!'
   
   if __name__ == '__main__':
       app.run(debug=True)

以下のコマンドを実行します。

python hello.py

ブラウザから http://127.0.0.1:5000/ にアクセスし、以下の表示になっていることを確認します。

Hello World! ワクワクしてきました。

Jinja2 テンプレートでページの見た目を整える
---------------------------------------------

機能を追加していく前に、Jinja2 テンプレートを用いてページの見た目を整えます。見た目がキレイだと、テンション上がりますよね？ テンション上がると、プログラミングが更に面白くなりますよね？？(押し付け。)

templates ディレクトリを作成し、その中に hello.html を作成します。

.. code-block:: html

   <!DOCTYPE html>
   <html>
   <head>
     <meta charset="utf-8">
     <title>Hello World!</title>
     <link rel=stylesheet type=text/css href="{{ url_for('static', filename='style.css') }}">
   </head>
   <body>
     <div class="page">
       <h1>Hello World!</h1>
     </div>
   </body>
   </html>

style.css を読み込む箇所で利用している url_for は、URL を生成するメソッドです。今回の場合は /static/style.css になります。アプリケーションやディレクトリの構成にあわせて適切に生成してくれるので、有効活用しない手はないです。

static ディレクトリを作成し、その中に style.css を作成します。

.. code-block:: css

   body {
     font-family: sans-serif;
     background: #eee;
   }
   
   h1 {
     color: #377ba8;
     font-family: 'Georgia', serif;
     margin: 0;
     border-bottom: 2px solid #eee;
   }
   
   .page {
     margin: 2em auto;
     width: 35em;
     border: 5px solid #ccc;
     padding: 0.8em;
     background: white;
   }

hello.py を以下のように修正します。

.. code-block:: python

   # render_template を追加
   from flask import Flask, render_template
   
   app = Flask(__name__)
   
   @app.route('/')
   def hello():
       # render_template を使って hello.html を表示
       return render_template('hello.html')
   
   if __name__ == '__main__':
       app.run(debug=True)

テンプレートファイルは templates ディレクトリから見つけてきてくれます。

ブラウザから http://127.0.0.1:5000/ にアクセスし、以下の表示になっていることを確認します。

Hello World! が少しキレイになりました。ワクワクしてきました。

おわりに
----------

今回は、Hello World! を少しキレイに表示するところまで進めました。

次回からは、少しずつ機能を追加していきたいと思います。
