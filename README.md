


# My Attended Framework

UiPath Go! で公開されている、Attended Framework というテンプレート:

https://go.uipath.com/component/attended-framework

にいくつか改修を加えたテンプレートです。

もともとの Attended Framework は

- 変数を設定ファイルから読み込む機能
- 変数をOrchestratorのAssetから読み込む機能
- ワークフロー全体をtry/catchすることで、システム例外(Application Exception)発生にスクリーンキャプチャを取得してくれる機能

という機能を持った便利なフレームワークのテンプレートです。。

設定ファイルの読み込み場所が、"Data¥Config.xlsx" と固定的だったので、下記の対応を入れることにしました。

テンプレートはデフォルトでは

- configPath = カラ : 本番用設定ファイルを置く場所
- devConfigPath = "C:\Temp\Config.xlsx" : 開発用設定ファイルを置く場所

を指定してあります。以下の仕様でファイルを探しに行くので、値を適宜変更して設定ファイルを開発・本番で切り替えて使ってください

devConfigPath で指定したパスが存在すれば、その設定ファイルを使用します。開発時はココに設定ファイルを置けばよいでしょう。もしくは適宜パスを修正してしまってください。

devConfigPath が空か、もしくはその場所に該当ファイルが存在しない場合は、configPathを参照します。

configPathは、空の場合は「ワークフローのパス + "Data/Config.xlsx"」を参照する。指定した場合は、そのパスの絶対パスにある設定ファイルを参照します。


従って、開発時は C:\Temp\Config.xlsx に設定ファイルを置いておき、publish後の本番運用時は、ワークフローと共にアーカイブされたData/Config.xlsxを使うか、明示的にどこかにおいたConfig.xlsxを使用する事が出来るようになります。