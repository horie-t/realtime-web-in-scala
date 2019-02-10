## Scalaによる、リアルタイムWebアプリケーションの構築メモ

Scalaで、チャット・ルームのWebアプリを作りながら、リアルタイムWebアプリケーションを作ってみた例です。

以下の3つを使って、Webアプリを構築していきます。
* [Play Framework](https://www.playframework.com/)
  ScalaおよびJavaのためのWebアプリケーション・フレームワークです。
* [Scala.js](https://www.scala-js.org/)
* [Akka.Js](https://github.com/akka-js/akka.js)

### 前提条件

ここでは、Ubuntu 18.04を使って構築していく方法について記載します。

### 準備

Play Frameworkを利用するには、Javaとsbt(Scala等用のビルドツール)が必要です。よって、Javaとsbtをインストールします。尚、Scala自体は、sbtによってインストールされます。

#### Javaの開発環境(JDK)のインストール

JDKをインストールします。ここでは、[AdoptOpenJDK](https://adoptopenjdk.net/)の[Ubuntu向けのインストーラ・パッケージ](https://github.com/rpardini/adoptopenjdk-deb-installer)を使ってインストールします。

```bash
sudo add-apt-repository --yes ppa:rpardini/adoptopenjdk
sudo apt-get update
sudo apt-get install adoptopenjdk-11-jdk-hotspot-set-default
```

Javaのライセンス価格やサポート期間については色々と騒ぎになりましたが、以下の通りの結論になりそうです。
* Oracle JDK  
  Javaの開発元による開発環境。Java 11からは実運用に使うには、 *Oracleと有償契約* が必要。LTS(長期サポート)版は、5年間のサポートがある。追加のサポートとして、更に3年、無期限のサポートもある。
* OpenJDK  
  Oracleがメインスポンサーとなっていて、 *無償で* 利用できる開発環境。ただし半年毎にリリースがあり、そのリリースを持って旧バージョンのサポートは終了する。実質的に、半年しか利用できない。
* AdoptOpenJDK  
  IBM、Microsoft等がスポンサーとなっている、OpenJDKのビルド済みバイナリの配布プロジェクトによる開発環境。独自に[4年間のLTS](https://adoptopenjdk.net/support.html#roadmap)も設定している。無償でJavaを利用したい場合は、これを利用する事に落ち着きそう。

#### sbtのインストール

sbtをインストールします。

```bash
echo "deb https://dl.bintray.com/sbt/debian /" | sudo tee -a /etc/apt/sources.list.d/sbt.list
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2EE0EA64E40A89B84B2DF73499E82A75642AC823
sudo apt-get update
sudo apt-get install sbt
```

