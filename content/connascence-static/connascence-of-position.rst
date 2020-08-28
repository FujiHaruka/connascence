位置のコナーセンス
#######################

:name: 位置
:strength: 30
:slug: position
:summary: 位置のコナーセンスは複数のエンティティが値の順序に関して一致しなければならないときに生じます。


.. Connascence of position is when multiple entities must agree on the order of values. 

位置のコナーセンスは複数のエンティティが値の順序に関して一致しなければならないときに生じます。

.. In Data Structures
.. ==================

データ構造
==================

.. For example, consider a function that retrieves a user's details:

たとえば、ユーザーの詳細を取得する関数を考えます。

.. code-block:: python

    def get_user_details():
        # Returns a user's details as a list:
        # first_name, last_name, year_of_birth, is_admin
        return ["Thomas", "Richards", 1984, True]

.. This is a somewhat contrived example, but it's not uncommon to see data returned in lists or tuples. Elsewhere in the code we might need to perform some check on whether the user is an administrator or not:

これは少し不自然な例ですが、リストやタプルでデータを返すのは珍しいことではありません。コードの別の箇所でユーザーが管理者かどうかを確認する必要があるとします。

.. code-block:: python

    def launch_nukes(user):
        if user[3]:
            # actually launch the nukes
        else:
            raise PermissionDeniedError("User is not an administrator!")

.. These two functions are linked by *connascence of position*. If the order of the values in the user list ever changes, both locations must be updated (this example is particularly scary if someone were to update the user list to be ``[first_name, initials, last_name, year_of_birth, is_admin]`` without updating the check inside launch_nukes).

この２つの関数は*位置のコナーセンス*で結びついています。ユーザーの詳細リストにある値の順序が変更されれば、両方の箇所を更新する必要があります（この例で特にあぶなっかしいのは、誰かがユーザーの詳細リストを  ``[first_name, initials, last_name, year_of_birth, is_admin]`` に変更して、launch_nukes の中の確認ロジックを更新せずにいる場合です）。

.. This connascence can be improved to connascence of name by turning the list into a dictionary or class. The following example shows how the above functions might look as a dictionary:

このコナーセンスはリストを辞書やクラスに変えることで名前のコナーセンスに改善できます。以下の例では上の関数を辞書で書き換えています。

.. code-block:: python

    def get_user_details():
        return {
            "first_name": "Thomas",
            "last_name": "Richards",
            "year_of_birth": 1984,
            "is_admin": True,
        }


    def launch_nukes(user):
        if user['is_admin']:
            # actually launch the nukes
        else:
            raise PermissionDeniedError("User is not an administrator!")

.. Note that these two functions are still coupled, but we've turned connascence of position into the weaker connascence of name. This has also increased the readability of the ``get_user_details`` function - the explicit comment is no longer needed to document the order of the keys.

注意点していただきたいのですが、２つの関数はまだ結合しています。けれども、位置のコナーセンスをより弱い名前のコナーセンスに変換しました。この変更によって、``get_user_details`` 関数の可読性も上がりました。キーの順序を注釈するためのコメントはもう必要ありません。

.. A similar solution is to use a class instead of a dictionary, and this can be beneficial if the structure being returned has constraints or operations associated with it.

同じような解決策として、辞書ではなくクラスを使うこともできます。返却するデータ構造が関連する制約や操作をもつ場合にはそのほうが便利でしょう。

.. In Function Arguments
.. =====================

関数の引数
=====================

.. Connascence of position also frequently occurs in function argument lists. Consider the following function declaration from a mythical email-sending utility library:

位置のコナーセンスは関数の引数リストの中にもよく現れます。想像上のEメール送信ライブラリの一部にある以下のような関数宣言を考えてみてください。

.. code-block:: python

    def send_email(firstname, lastname, email, subject, body, attachments=None):

.. Code calling this ``send_email`` function must remember the order of arguments. Should that order ever change, all calling locations must also be updated. This example could also be improved to connascence of name by passing a structured object (a class or dictionary) instead of a number of parameters.

この ``send_email`` 関数を呼び出すコードは引数の順序を覚えておかなければなりません。万が一順序が変更されると、関数を呼び出すコードもすべて変更する必要があります。この例も複数のパラメータを順番に渡す代わりに構造化されたオブジェクト（クラスや辞書）を渡すことによって名前のコナーセンスへと改善することができます。
