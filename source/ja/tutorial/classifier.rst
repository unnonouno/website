Classifier
=================

ここではJubatusの多値分類機能（Classifier）である ``jubaclassifier`` を使用した、Jubatus Client の使い方を説明します。

多値分類機能（Classifier）とは、入力データを複数グループに分類する機能であり、スパムメールの判定などに利用することができます。


-------------------------------------
サンプルプログラムの概要
-------------------------------------

サンプルとして、各時代の将軍は姓（苗字）ごとに名（名前）が似ていることから、将軍の名から姓を当てるというプログラム「 `shogun <https://github.com/jubatus/jubatus-example/tree/master/shogun>`_ 」を用いて説明していきます。

最初に、「"家康"という名は"徳川"という姓である」、「"尊氏"という名は"足利"という姓である」という、歴代将軍の名前を元に作成した一定量以上の姓と名のペアをクライアント側で用意し、 ``jubaclassifier`` に学習させます。
これにより、姓を分類ラベル、名を特徴としたモデルが作成されます。

次に、予測用の入力データとして任意の名を ``jubaclassifier`` に与えます。 ``jubaclassifier`` は先ほど学習したモデルを用い、姓を予測して返却するので、クライアント側では、受け取った結果を出力します。

例えば、予測用の入力データとして"慶喜"を ``jubaclassifier`` に与えると、"徳川"が結果として出力されます。
もちろん、「"慶喜"という名は"徳川"である」というデータは学習データに含まれていません。


--------------------------------
処理の流れ
--------------------------------

Jubatus Client を使ったコーディングは、主に以下の流れになります。

1. ``jubaclassifier`` への接続設定
    ``jubaclassifier`` のホストやポート番号を指定し、接続設定をします。

2. 学習用データの準備
    一定量以上の名に姓を付与した学習データを作成します。

3. データの学習（学習モデルの更新）
    2\. で作成した学習データを ``train`` メソッドで ``jubaclassifier`` に与え、学習を行います。

4. 予測用データの準備
    予測用に ``jubaclassifier`` に投げる、名のデータを作成します。

5. 学習モデルに基づく予測
    4\. で作成した予測用データを入力値とし、 ``classify`` メソッドで 3. の学習に基づいた予測を行います。

6. 結果の出力
    ``classify`` メソッドの戻り値である予測結果を出力します。


--------------------------------
サンプルプログラム
--------------------------------

.. toctree::
   :maxdepth: 2

   classifier_python
   classifier_ruby
   classifier_java
