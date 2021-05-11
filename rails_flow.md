### リクエストからレスポンスまでの流れについて(GET編)
***
* Webブラウザから`/members`というURLでHTTPメソッド`GET`のHTTPリクエストが送られる。開発者ツールで見てみると、URLが`/members`、Request Methodが`GET`のリクエストが送られていることが分かる。
[![Image from Gyazo](https://i.gyazo.com/13bab4301c259d6a4913a41e472a0afb.png)](https://gyazo.com/13bab4301c259d6a4913a41e472a0afb)
* HTTPリクエストがWebサーバーを介してRailsアプリケーションへ受け渡される。
* `routes.rb`に記述されているルーティングに沿って、mambersコントローラのindexアクションが呼び出される。
* 一覧機能であるindexアクションでは、全ユーザーデータをMemberオブジェクト群としてMemberクラスから取得する。アクションでは必要に応じてモデルを利用する。
* モデルはコントローラからの命令を元にSQLを発行してレコード操作を行う。今回はデータベースのmemberテーブルから全レコードを読みだすSQLが実行される。
* indexアクションに対応するビューテンプレートを用いてHTMLが生成される。
* コントローラがHTTPレスポンスを作成し、Webサーバを介してクライアントへと返され、その中に含まれるHTMLをWebブラウザが解釈して新規作成ページが表示される。  
(今回はtech-essentialsのスパルタコースのメンバーを例に出したので/usersを/membersにしています)

### リクエストからレスポンスまでの流れについて(POST編)
***
#### 新規作成ページが表示されるまでの流れ
* Webブラウザから`/tasks/new`というURLでHTTPメソッド`GET`のHTTPリクエストが送られる。開発者ツールで見てみると、URLが`/tasks/new`、Request Methodが`GET`のリクエストが送られていることが分かる。
[![Image from Gyazo](https://i.gyazo.com/7d433e6c2383435391a4ac00072eea06.png)](https://gyazo.com/7d433e6c2383435391a4ac00072eea06)
* HTTPリクエストがWebサーバーを介してRailsアプリケーションへ受け渡される。
* `routes.rb`に記述されているルーティングに沿って、tasksコントローラのnewアクションが呼び出される。
* newアクション内ではTaskクラスのオブジェクトが生成され、インスタンス変数`@task`に格納される。
* newアクションに対応するビューテンプレートを用いてHTMLが生成される。
* コントローラがHTTPレスポンスを作成し、Webサーバを介してクライアントへと返され、その中に含まれるHTMLをWebブラウザが解釈して新規作成ページが表示される。

#### タスク名を入力し、作成ボタンを押して一覧画面に遷移するまでの流れ
* タスク名を入力して作成ボタンを押すと、Webブラウザから`/tasks`というURLで`POST`メソッドのHTTPリクエストが送られる。開発者ツールで見てみると、URLが`/tasks`、Request Methodが`POST`のリクエストが送られていることが分かる。
[![Image from Gyazo](https://i.gyazo.com/a41a98410854c847aa0a75c1b2db6560.png)](https://gyazo.com/a41a98410854c847aa0a75c1b2db6560)
* HTTPリクエストがWebサーバーを介してRailsアプリケーションへ受け渡される。
* `routes.rb`に記述されているルーティングに沿って、tasksコントローラのcreateアクションが呼び出される。
* createアクション内では、`form_with`メソッドからリクエストパラメータとして送られてきた情報の中から、`params`を用いて名称(name)と詳しい説明(description)の情報だけが抜き取られ、変数taskに格納された後にデータベースに保存される。開発者ツールのForm Dataを見てみると、`task[name]:会議`、`task[description]:パソコンを持っていく`という情報が渡されていることが分かる。
[![Image from Gyazo](https://i.gyazo.com/71444e012b32e916393c65a047c07ddb.png)](https://gyazo.com/71444e012b32e916393c65a047c07ddb)
* この時モデルはコントローラからの命令を元にSQLを発行してレコード操作を行う。今回は変数`task`内の情報をデータベースのtasksテーブルに保存するSQLが実行される。
* その後`redirect_to`メソッドで２つ目のリクエストが発生し、`/tasks`というURLで`GET`メソッドのHTTPリクエストが送られる。開発者ツールで見てみると、URLが`/tasks`、Request Methodが`GET`のリクエストが送られていることが分かる。
[![Image from Gyazo](https://i.gyazo.com/6b867a85954d929a1203dfa10341e66f.png)](https://gyazo.com/6b867a85954d929a1203dfa10341e66f)
* `routes.rb`に記述されているルーティングに沿ってtasksコントローラ内のindexアクションが呼び出される。
* indexアクションに対応するビューテンプレートを用いてHTMLを生成する。
* コントローラがHTTPレスポンスを作成し、Webサーバを介してクライアントへと返され、その中に含まれるHTMLをWebブラウザが解釈して一覧画面が表示される。

#### 詳細画面に遷移するまでの流れ
一覧画面からタスクを選んでクリックすると詳細画面に遷移する

* タスクがクリックされると、そのタスクに対応したidを持った`/tasks/:id`のような形のURLでHTTPメソッド`GET`のHTTPリクエストが送られる。開発者ツールで見てみると、URLが`/tasks/5`、Request Methodが`GET`のリクエストが送られていることが分かる。
[![Image from Gyazo](https://i.gyazo.com/099466c1c81f9528393d5e9cc6dc129f.png)](https://gyazo.com/099466c1c81f9528393d5e9cc6dc129f)
* HTTPリクエストがWebサーバーを介してRailsアプリケーションへ受け渡される。
* `routes.rb`に記述されているルーティングに沿って、tasksコントローラのshowアクションが呼び出される。
* showアクション内では、`params`を用いてURLからidが取得され、findメソッドによってそのidに対応したレコードがインスタンス変数`@tasks`に格納される。
* この時モデルはコントローラからの命令を元にSQLを発行してレコード操作を行う。今回はデータベースのtasksテーブルからidに対応したレコードを読みだすSQLが実行される。
* showアクションに対応するビューテンプレートを用いてHTMLが生成される。
* コントローラがHTTPレスポンスを作成し、Webサーバを介してクライアントへと返され、その中に含まれるHTMLをWebブラウザが解釈して画面に表示される。
