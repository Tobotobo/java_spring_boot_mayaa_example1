# java_spring_boot_mayaa_example1

## 概要
- Spring Boot で テンプレートエンジンに Mayaa を使用するサンプルプログラム
- 出力は war ファイル
- 実行は Spring Boot 内臓の Tomcat は使わず Community Server Connector を使用

## 参考
- Mayaa  
  http://mayaa.seasar.org/index.html

- Mayaa - チュートリアル  
  http://mayaa.seasar.org/documentation/hello.html

- Mayaa - 4-1. Mayaa core プロセッサ リファレンス　※タグの説明
  http://mayaa.seasar.org/documentation/processor_reference.html

- Mayaa - 4-2. 定義済みオブジェクト  
  http://mayaa.seasar.org/documentation/implicit_object.html

## 実行方法
1. VSCode の拡張機能で Community Server Connector をインストール
1. apache-tomcat-9.0.41 を作成
1. build_war.bat を実行(Ctrl+Shift+B)し target フォルダ内に demo.war を作成
1. demo.war を右クリックし Run on Server で apache-tomcat-9.0.41 にデプロイ

次回以降、既にデプロイが済んでいれば、apache-tomcat-9.0.41 を起動して build_war.bat を実行するだけで反映される。  
ただし、たまに反映されなくなることがあるので、その時は SERVERS から demo.war を Remove Deployment し再度 Run on Server する。  
また、demo.war のビルド時にエラーがあった場合に、Community Server Connector がバグってフォーカスを奪い続ける状態になることがある。  
その際は、SERVERS の apache-tomcat-9.0.41 を右クリックし Stop Server で一度停止させてやれば元に戻る。  
(フォーカスを奪われることで、すぐに右クリックメニューが消えるので、消える前に気合でクリックすること)

## Tomcat が demo.war の更新をチェックする間隔を変更する
demo.war を更新すると自動的に Tomcat に反映されるが、チェック間隔が 15 秒なので、反映されるまでに少し待たされることがある。  
Community Server Connector で管理されている Tomcat の server.xml の設定を変更することでチェック間隔を短くすることができる。
```
code "%userprofile%\.rsp\redhat-community-server-connector\runtimes\installations\tomcat-9.0.41\apache-tomcat-9.0.41\conf\server.xml"
```
server.xml - 152行目付近  
backgroundProcessorDelay を追加する。(単位は秒)
```xml
<Host name="localhost"  appBase="webapps"
    unpackWARs="true" autoDeploy="true"
    backgroundProcessorDelay="1">
```

## 構成
- example1  
  Mayaa - 2-6. HTML 部品 (動的)  - コンポーネントで親ページの変数を使う
  http://mayaa.seasar.org/documentation/component2.html

## メモ
- コンテキストルートに default.mayaa を作成することでページ共通の設定ができる  
  Mayaa - 3-1. ページ共通の設定  
  http://mayaa.seasar.org/documentation/default.html
