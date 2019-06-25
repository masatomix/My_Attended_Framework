
# My Attended Framework

UiPath Go! で公開されている、Attended Framework というテンプレート:

https://go.uipath.com/component/attended-framework

にいくつか改修を加えたテンプレートです。

もともとの Attended Framework は

- 変数を設定ファイルから読み込む機能
- 変数をOrchestratorのAssetから読み込む機能
- ワークフロー全体をtry/catchすることで、システム例外(Application Exception)発生にスクリーンキャプチャを取得してくれる機能

という機能を持った便利なフレームワーク(のテンプレート)です。

ただ、設定ファイルの読み込み場所が"Data¥Config.xlsx" と固定的だったので、下記の対応を入れることにしました。

今回公開したテンプレートは、デフォルトでは

- configPath = カラ : 本番用設定ファイルを置く場所
- devConfigPath = "C:\Temp\Config.xlsx" : 開発用設定ファイルを置く場所

を指定してあります。以下の仕様でファイルを探しに行くので、値を適宜変更して設定ファイルを開発・本番で切り替えて使ってください

devConfigPath で指定したパスが存在すれば、その設定ファイルを使用します。開発時はココに設定ファイルを置けばよいでしょう。もしくは適宜パスを修正してしまってください。

devConfigPath が空か、もしくはその場所に該当ファイルが存在しない場合は、configPathを参照します。

configPathは、空の場合は「ワークフローのパス + "Data/Config.xlsx"」を参照する。指定した場合は、そのパスの絶対パスにある設定ファイルを参照します。


従って、開発時は C:\Temp\Config.xlsx に設定ファイルを置いておき、publish後の本番運用時は、ワークフローと共にアーカイブされたData/Config.xlsxを使うか、明示的にどこかにおいたConfig.xlsxを使用する事が出来るようになります。


## 使い方

https://github.com/masatomix/My_Attended_Framework/releases より、最新版のソースコードをzip形式でダウンロードするか、もしくはGitのコマンドでソースコードを取得してください。

```bash
$ git clone https://github.com/masatomix/My_Attended_Framework.git
```

取得したコード(zipなどの場合は解凍してください) は UiPath Studioのプロジェクトになっているので、そのまま UiPath Studio で開いてご利用ください。

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/73777/0dfae90c-472a-829b-d4ee-9e3fe3a2d07d.png)


## テンプレートとして保存しておくと便利

UiPath Studioで開いた後「テンプレートとして保存」をクリックすると
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/73777/ab218267-c7f0-c177-d860-357835a0647b.png)


テンプレート作成画面が表示されます。適当に名前を入力後「作成」をクリックしてテンプレートを作成すると、、、
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/73777/6e76a223-5a9f-dcd9-3d5e-93693423fea4.png)

プロジェクトの新規作成画面に、自分が作成したテンプレートが表示されるようになりました！
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/73777/000491ec-96fa-b142-1d51-91a61bab27e9.png)


他のテンプレートと同様、今後はココからプロジェクトを作成すれば、まさにテンプレートとして使用することが可能です。

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/73777/b7714a70-5e8b-e5ca-94be-815a94a2b654.png)





## 依存するカスタムアクティビティ

このプロジェクトは [nuget.org](https://www.nuget.org/packages/kino.UiPath.MyAttendedFramework/) で公開されている kino.UiPath.MyAttendedFramework というアクティビティパッケージに依存しています。

ソースコードは、
https://github.com/masatomix/kino.UiPath.MyAttendedFramework
です。

もともとの Attended Framework はただのテンプレートだったので、テンプレート部のコードを修正したばあいは、再度テンプレートを配布し保存し、いま作成中のワークフローたちを新テンプレートに載せ替える必要がありました。

今回作成したテンプレートは初期処理と終了処理を、上記のアクティビティパッケージ内のカスタムアクティビティで実施しています。したがって、kino.UiPath.MyAttendedFramework のバージョンを更新することで、ロジックの改修が可能となり、保守性が向上すると思います。

