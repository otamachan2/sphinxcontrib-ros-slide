sphinxcontrib-ros紹介
======================

第7回ROS勉強会＠ドワンゴ

by otamachan

自己紹介
--------

* ID: otamachan (Twitter: otamasan)
* 愛知県在住サラリーマン
* 3児のお父さん
* ROSは今年の1月から使い始めました
* 勉強会発表初めて枠

  - Tシャツにつられてしまいました・・・
  - Tシャツ駆動開発
  - Tシャツ怖い

ところで
----------

* みなさんはドキュメント書いてますか？
* ドキュメント書くの好きですか？

私は好きではありません
----------------------

ドキュメント書いていたはずなのに、気づいたら、

  * 音声認識で文書生成するプログラム書いてる
  * Texのマクロいじってる
  * Sphinxの拡張書いてる

ことが多々・・・

そんな私ですが、今日はROSのドキュメンテーションツールを紹介します。

目次
----

#. Sphinxの紹介
#. sphinxcontrib-rosの紹介
#. まとめ

というわけでまずはSphinxの紹介
----------------------------------

`Sphinx <http://sphinx-users.jp/>`_ とは
  * Pythonで書かれたドキュメンテーションツール
  * reStructuredText(マークアップ言語)でドキュメントを記述
  * HTML, PDF, ePub等出力フォーマットが豊富
  * HTMLのテーマも豊富
  * 多言語対応のドキュメントも書ける
  * `Python <http://docs.python.jp/3/>`_ のドキュメントに使用されている
  * `ReadTheDoc <https://readthedocs.org/>`_ といったホスティングサービスも

こんな感じで書くと
------------------

.. rst-class:: small

.. literalinclude:: _sample/sample.rst
   :language: rst

こんな風にかっこよく出力してくれる
----------------------------------

.. raw:: html

    <div>
      <iframe style="height:520px" src="sample/sample.html" frameborder="0"></iframe>
    </div>

良い点(個人的な感想)
---------------------

* 簡単にかっこ良く書ける
* Gitとかで管理しやすい
* Pythonで拡張が書ける!

使いづらい点(個人的な感想)
--------------------------

* 細かい表現がしづらい(表とか)
* WYSIWYGでない(ビルドのタイムラグがある)
* ソフト屋さんでないと敷居が少し高い

ロボット界でもちらほらSphinxが
------------------------------

NAOqi(Pepper)
-------------

.. raw:: html

    <div>
      <iframe style="height:520px" src="http://doc.aldebaran.com/2-1/naoqi/index.html" frameborder="0"></iframe>
    </div>

fetch robotics
---------------

.. raw:: html

    <div>
      <iframe style="height:520px" src="http://docs.fetchrobotics.com/" frameborder="0"></iframe>
    </div>

Choreonoid
-----------

.. raw:: html

    <div>
      <iframe style="height:520px" src="http://choreonoid.org/en/" frameborder="0"></iframe>
    </div>

ROSのドキュメントといえばROS wiki
---------------------------------

.. raw:: html

    <div>
      <iframe style="height:520px" src="http://wiki.ros.org/Documentation" frameborder="0"></iframe>
    </div>

Wiki拡張で書けて
------------------

.. raw:: html

    <div>
      <iframe style="height:520px" src="http://wiki.ros.org/amcl?action=raw" frameborder="0"></iframe>
    </div>

パッケージ
-----------

.. raw:: html

    <div>
      <iframe style="height:520px" src="http://wiki.ros.org/amcl#line-2" frameborder="0"></iframe>
    </div>

API(Pub/Sub/パラメータ/型)
--------------------------

.. raw:: html

    <div>
      <iframe style="height:520px" src="http://wiki.ros.org/amcl#line-23" frameborder="0"></iframe>
    </div>

かっこいい
-----------

.. rst-class:: build

* かも

SphinxでもROSのドキュメントかっこよく書きたい
---------------------------------------------

sphinxcontrib-rosの紹介
------------------------

sphinxcontrib-ros
  SphinxでROSのドキュメンテーションをするための拡張

  #. シンタックスハイライト
  #. パッケージ概要
  #. メッセージ定義
  #. インタフェース

  が書ける。

インストール
------------

#. パッケージインストール

   .. code-block:: bash

      $ pip install sphinxcontrib-ros

#. 設定ファイル(``conf.py``)に追加

   .. code-block:: python

      # 拡張の追加
      extenstions += ['sphinxcontrib.ros']
      # パッケージパスを指定
      ros_package_path = ['../src']

(2)シンタックスハイライト
-------------------------

.. rst-class:: small

.. literalinclude:: _sample/syntax.rst
   :language: rst

出力
----

(1)パッケージ概要
------------------

.. literalinclude:: _sample/package.rst
   :language: rst

出力
----


オプションとか
---------------


(2)メッセージ定義
-----------------

出力
----

(2)メッセージ定義(ファイル指定)
-------------------------------

出力
----

オプションとか
---------------


(3)インターフェース定義
------------------------

出力例
--------

オプションとか
---------------

サンプル
---------

Indigoの

* 全パッケージ
* 全メッセージ(2015/09現在)

を出力してみました。

* TravisCI + Docker (Ubuntu14.04/Indigo !!)

自プロジェクトで使う時
----------------------

* 一から全部メッセージ定義しないといけないの？

大丈夫
-------

* そんな時の `sphinx.ext.intersphinx <http://sphinx-doc.org/latest/ext/intersphinx.html>`_ !

  ``conf.py`` に

  .. code-block:: python

     extensions += ['sphinx.ext.intersphinx']
     intersphinx_mapping = {'ros': ('https://docs.python.org/3.4', None)}

  って書いておけば

  .. code-block:: rst

     .. ros:message:: my_greate_package/NewMessage

  だけで

参照できちゃう
---------------

まとめ
-------

* Tシャツにつられてsphinxcontrib-rosを公開しました
* conf.pyに以下を追加するだけ

  .. code-block:: python

     extensions += ['sphinxconrib.ros', 'sphinx.ext.intersphinx']
     ros_package_path = ['../src']
     intersphinx_mapping = {'ros': ('https://docs.python.org/3.4', None)}

* かっこよくROSのドキュメントが書けちゃうかも

ありがとうございました
----------------------

* **Hope your happy ROS documentation life with Sphinx!**

* ちなみにこのスライドもSphinxで記載しています

  * 拡張: `hieroglyph <https://github.com/nyergler/hieroglyph>`_
  * Source: `github.com <https://github.com/otamachan2/sphinxcontrib-ros-slide/blob/master/index.rst>`_
  * Build: `travis-ci.com <https://travis-ci.org/otamachan2/sphinxcontrib-ros-slide/>`_
  * Slide: `gitbub.io <http://otamachan2.github.io/sphinxcontrib-ros-slide/>`_
