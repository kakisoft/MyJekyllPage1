---
layout: post
title:  LAN環境Android無料通話
date:   2017-07-09 21:23:00 +0900
categories: Android
---

### 　日付：2017/07/07〜2017/07/09

1. (初動)    
構内電話網(IP-PBX)を構築してAndroidで無料通話をやってみよう！  
[http://blog.zamuu.net/2011/0429/ip-pbx-android/](http://blog.zamuu.net/2011/0429/ip-pbx-android/)

1. Pantheon(KLUE 2.0)が入っていたジャンクPCに、Cent OSを入れる

1. せっかくだから最新版のイメージファイルを落とす

1. rufusを使い、USBブートディスク作成。

1. イメージファイルが4GB越えてて、使おうと思っていた、USBメモリ（4G）が使用不可。32Gを用意する。

1. ブートメニューが起動せず。  
イメージファイル作成が失敗したのか？
何度トライしてもうまく行かず。何故だ！？

1. どうやら、このジャンクPCでは32GのUSBメモリを認識できないみたいだ。  
こういう、生々しい状況があるんで、「古いPCでも簡単に、遜色なく利用できますよ。」なんて情報は大してアテにならん。  
渋々、ミニマム版(800M)のイメージファイルで作成する。

1. インストール完了。

1. インストール時に、ネットワーク設定を忘れてた（インストールボタン押したあと、子供を公園に連れて行った）ため、ネットワーク設定。

1. Cent OS 7から、設定方法が結構変わってる。。。。  
（無線LAN内蔵でないのも影響し、少し面倒になってる。）
インストール時に認識させて設定するほうが楽そう。  
再インストール。

1. ついでにGUI環境にしておこう。

1. 完了。  
ログイン時、デフォルトでデスクトップ環境になるようにしておこう。

1. え？このシリーズって、デフォルトランレベル設定できないの？  
ってか、ランレベルの切り替えもうまくいかんぞ。。  
もういいや。ログインしてstartxで。

1. 重い・・・あれ？こんなに動き悪かったっけか？  
Asteriskインスト終わって、設定をチマチマやっていくも、息子の妨害に遭い、PCが床に落下。
TVの放送終了後のような、悲しい画面が目の前に広がる。  
嫁曰く、「シムシティの怪獣みたいな存在だから諦めて。」

1. 不安程度が増してきたし、あのPCはでやるのは、もういいや。  
いっそ、VPCとかでやってる人いないかな。  
参照元記事の日付が５年前なんで、ちょっと不安だったのもあり、少し調べる。

1. 居たよ！やってる人！  
[http://qiita.com/ganezasan/items/05b16a2254f066f6bbdc](http://qiita.com/ganezasan/items/05b16a2254f066f6bbdc)

1. セキュリティグループを作成。EC2インスタンス作成。  
インスタンス名は「Asterisk」としておこう。

1. 特に行き詰る事はなく、インストール完了。

1. 続いて設定。

1. [ec2-user@ip-xxx-xxx-xxx-xxx asterisk-1.8.8.1]$ make sample  
make: *** No rule to make target `sample'.  Stop.  
[ec2-user@ip-xxx-xxx-xxx-xxx asterisk-1.8.8.1]$ make config  
We could not install init scripts for your distribution.  
あれ？サンプル設定ファイルのインストールできねーじゃん。  

1. ディストリが原因なの？取り合えず控えておく。  
cat /etc/system-release  
Amazon Linux AMI release 2017.03

1. 今日はもう遅いから寝よう。
　  
　  

### 　日付：2017/07/11

1. Cent OS は最近 ver 7に上がり、それ以前と大きく変わったみたい。
先日、サンプル設定ファイルがインストールできなかったのは、それも原因の一旦？

1. 別のAMIで試してみようか。  
* Webuzo 2.2.9 Moodle 2.7.2 Application Manager on LAMP Stack centos 6.5 x86_6-52c23e0a-10c2-4d78-ac74-8d438d805435-ami-7005b218.2
* centos-6.8-hardened-x86_64-170117_21-disk1-d07a026a-15d3-4d17-97d4-333edabc2b58-ami-16ed0500.3
* Webuzo 2.2.9 Piwik 2.7.0 Application Manager on LAMP Stack centos 6.5 x86_64-ed0548ae-49e9-4edb-b8d9-36b3910d53e6-ami-c456e7ac.2
* ultraserve-centos-6.8-ami-database-hvm-2017.03.3-2-x86_64-gp2
* Webuzo 2.3.2 ownCloud 7.0.3 Application Manager on LAMP Stack centos 6.6 x86-bcf7a10b-628e-4ccf-9a47-3954db7f650a-ami-3eac3556.2
* 2016-06-Recovery (No-LVM)-ACB-CentOS6-HVM
* ultraserve-centos-6.7-ami-pv-2016.03.2.x86_64-gp2
* spel-minimal-centos-6.8-pvm-2017.01.1.x86_64-gp2
* CentOS Linux 6 x86_64 HVM EBS 1602-74e73035-3435-48d6-88e0-89cc02ad83ee-ami-21e6d54b.3
* ultraserve-centos-6.9-ami-reverse_proxy-hvm-2017.03.2-4-x86_64-gp2 
* ultraserve-centos-6.7-ami-application-hvm-2016.03.2-1-x86_64-gp2 
* CentOS 6.3 hvm bashton3  
* （以下略）  
むちゃくちゃ多い。全部は書ききれん。  
今回、「CentOS 6.3 hvm bashton3」を選択。特に根拠はない。  
　  
1. インスタンス作成。  
cat /etc/redhat-release  
CentOS release 6.3 (Final)

1. Asteriskインストール。

1. このインスタンスタイプだとrootパスワード要求されるのね。。。
パスワード控えてなかったヨ

1. もっかいEC2作り直す。

1. 先日と同じ個所でエラー。  
make sampleは何者だ？調べてみるか。

1. 正しいコマンドは「make sample**s**」では！？  
[https://wiki.asterisk.org/wiki/display/AST/Installing+Sample+Files](https://wiki.asterisk.org/wiki/display/AST/Installing+Sample+Files)

1. OK！起動まで出来たぜ！

1. 次はクライアント側だ！  
が、Android版の X-Liteを探してみたが、見つからん・・・  
試しに別のソフトフォンを落としてみようか。
 * Cloud Softphone
 * CSipSimple
試しにこの２つを。  
　  
1. ・Cloud Softphone  
何だ Cloud ID って…？  
よくわからんから、もう１つのやつを動かしてみよう。

1. ・CSipSimple  
うーん。繋がらない。

1. X-LiteのPC版があるみたいだから、それを使ってみよう。  
WinとMacか・・・。作業端末をWinに変更。

1. ダウンロードはここから。  
[http://www.counterpath.com/x-lite-download/](http://www.counterpath.com/x-lite-download/)

1. インストールには .NET Frameworkの更新が必要とな。  

1. 更新。再起動。

1. X-Liteインストール完了。

1. 参考サイトと全く同じ設定にしておこう。

1. ステータスが「Available」にならないぜ！  
今日はこの辺にしておこう。インスタンスは一旦、消しとく。
　  
　  

### 　日付：2017/07/16

1. 今度は Amazon Linuxでやってみよう。

1. AsteriskインストールまではOK。だが、  
make samplesにて、  
```
build_tools/make_sample_voicemail "//var/lib/asterisk" "//var/spool/asterisk"
Installing file phoneprov/000000000000-directory.xml
/usr/bin/install: 通常ファイル `/var/lib/asterisk/phoneprov/000000000000-directory.xml' を作成できません: そのようなファイルやディレクトリはありません
Installing file phoneprov/000000000000-phone.cfg
/usr/bin/install: 通常ファイル `/var/lib/asterisk/phoneprov/000000000000-phone.cfg' を作成できません: そのようなファイルやディレクトリはありません
Installing file phoneprov/000000000000.cfg
/usr/bin/install: 通常ファイル `/var/lib/asterisk/phoneprov/000000000000.cfg' を作成できません: そのようなファイルやディレクトリはありません
Installing file phoneprov/polycom.xml
/usr/bin/install: 通常ファイル `/var/lib/asterisk/phoneprov/polycom.xml' を作成できません: そのようなファイルやディレクトリはありません
Installing file phoneprov/polycom_line.xml
/usr/bin/install: 通常ファイル `/var/lib/asterisk/phoneprov/polycom_line.xml' を作成できません: そのようなファイルやディレクトリはありません
Installing file phoneprov/snom-mac.xml
/usr/bin/install: 通常ファイル `/var/lib/asterisk/phoneprov/snom-mac.xml' を作成できません: そのようなファイルやディレクトリはありません
make: *** [samples] エラー 1  
```  
とな。

1. make install  
を忘れていたのが原因。

1. make config  
We could not install init scripts for your distribution.  
何故だ。

1. 事前に、
```touch /etc/redhat-release```  
を実行しておくといいらしい。
[http://www.spanky-world.com/asterisk/asterisk-page040.html](http://www.spanky-world.com/asterisk/asterisk-page040.html)

1. sudo asterisk -vvvr  
```
=========================================================================  
  == Parsing '/etc/asterisk/asterisk.conf':   == Found  
  == Parsing '/etc/asterisk/extconfig.conf':   == Found  
Unable to connect to remote asterisk (does /var/run/asterisk/asterisk.ctl exist?)  ```  
だと？ 

1. ldconfig  
でいいのか？

1. ```=========================================================================  
  == Parsing '/etc/asterisk/asterisk.conf':   == Found  
  == Parsing '/etc/asterisk/extconfig.conf':   == Found  
Connected to Asterisk 1.8.8.1 currently running on ip-172-31-2-102 (pid = 31351)  
Verbosity is at least 3  
ip-172-31-2-102*CLI>```   
これでOKだったみたい。
Amazon Linuxでも問題なしという事で。

1. X-Liteを設定。
おお！今度は Aailableになったぞ！
上記の設定例で行くと、パスワードは「pass」となる。  
ポート番号の指定は特に要らない。

1. 続いて、Android側。  
Media5-phoneをインストール。

1. あれ？どう設定するんだ。これ。  
もう遅いから、明日にしよう。


