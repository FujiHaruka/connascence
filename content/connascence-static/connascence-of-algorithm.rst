アルゴリズムのコナーセンス
#############################

:name: アルゴリズム
:strength: 40
:slug: algorithm
:summary: アルゴリズムのコナーセンスは複数のコンポーネントが特定のアルゴリズムに関して一致しなければならないときに生じます。


.. Connascence of algorithm is when multiple components must agree on a particular algorithm. 

アルゴリズムのコナーセンスは複数のコンポーネントが特定のアルゴリズムに関して一致しなければならないときに生じます。

.. In Data Transmission
.. ====================

データの転送
====================

.. Connascence of algorithm frequently occurs when two entities must manipulate data in the same way. For example, if data is being transmitted from one service to another, some sort of checksum algorithm is commonly used. The sender and receiver must agree on which algorithm is to be used. If the sender changes the algorithm used, the receiver must change as well.

アルゴリズムのコナーセンスは２つのエンティティが同じ方法でデータを操作しなければならない場合によく現れます。たとえば、データが一つのサービスから別のサービスに送信されるとき、ある種のチェックサムアルゴリズムが一般的に使われます。送信側と受信側がどのアルゴリズムを使用するかに関して一致していなければなりません。送信側が使用するアルゴリズムが変更されれば、受信側も更新する必要があります。

.. In Data Validation and Encoding
.. ===============================

データのバリデーションとエンコーディング
===========================================

.. Consider a hypothetical piece of software that required users to provide a valid email address when creating an account. The software must validate that the email address is valid, but this might happen in several places, including:

仮に、アカウントを作成するときに有効なメールアドレスの入力を要求するソフトウェアを考えてみましょう。このソフトウェアはメールアドレスの有効性を検証しますが、検証はいくちかの場所で行われることが想定できます。

.. * In a database model object.
.. * In a webapp 'controller' class method.
.. * In a form field in the front-end UI.

* データベースモデルオブジェクトの中で検証する
* ウェブアプリの「コントローラ」クラスのメソッドで検証する
* フロントエンド UI のフォームフィールドで検証する

.. These pieces of code might well be in different languages, and will almost certainly be far apart from each other. The consequence of these algorithms being different might include users not being able to register, but recieving no feedback as to why.

これらのコードは別々の言語で書かれているかもしれませんし、ほぼ確実に互いに離れた場所にあります。これらのアルゴリズムが異なるとユーザーが登録できず、なぜ登録できないかフィードバックを得られないかもしれません。

.. Another common example of connascence of algorithm is when unicode strings are written to disk. Imagine a hypothetical piece of software that writes a data string to a cache file on disk:

アルゴリズムのコナーセンスに関してまた他の例はユニコード文字列がディスクに書き込まれる場合です。データ文字列をディスク上のキャッシュファイルに書き込む仮のソフトウェアを想像してみましょう。

.. code-block:: python

    def write_data_to_cache(data_string):
        with open('/path/to/cache', 'wb') as cache_file:
            cache_file.write(data_string.encode('utf8'))

.. A matching function is used to retrieve the data from the cache file:

キャッシュファイルからデータを読み取るために使う関数がこれに対応します。

.. code-block:: python

    def read_data_from_cache():
        with open('/path/to/cache', 'rb') as cache_file:
            return cache_file.read().decode('utf8')

.. The connascence of algorithm here is that both functions must agree on the encoding being used. If the ``write_data_to_cache`` function changes to encrypt the data on disk (the data being stored is potentially sensitive), the ``read_data_from_cache`` must also be updated.

ここでアルゴリズムのコナーセンスは２つの関数が同じエンコーディングを使わなければならないということです。もし ``write_data_to_cache`` 関数がディスクに書き込むデータを暗号化するよう変更すれば（保存するデータが潜在的にセンシティブな情報かもしれません）、``read_data_from_cache`` 関数も更新する必要があります。

.. In Test Code
.. ============

テストコード
============

.. Test code often contains connascence of algorithm. Consider this hypothetical test:

テストコードはアルゴリズムのコナーセンスを含む場合がよくあります。次のような仮のテストを考えてみてください。

.. code-block:: python

    def test_user_fingerprint(self):
        user = User.new(name="Thomi Richards")
        actual = user.fingerprint()
        expected = hashlib.md5(user.name).hexdigest()
        self.assertEqual(expected, actual)

.. This test is supposed to be testing that the 'fingerprint' method of the ``User`` class works as expected. However, it contains connascence of algorithm, which limits it's effectiveness. If the ``User`` class ever changes the way fingerprints are calculated, this test will fail.

このテストでは ``User`` クラスの 'fingerprint' メソッドが期待通りに動作することをテストしているとします。しかし、これはアルゴリズムのコナーセンスを含んでいるため、テストの有効性が限定的です。``User`` クラスがフィンガープリントの計算方法を変えるとこのテストは失敗します。
