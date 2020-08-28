意味のコナーセンス
######################

:strength: 20
:slug: meaning
:summary: 意味のコナーセンスは複数のコンポーネントが特定の値の意味に関して一致しなければならないときに発生します。


.. Connascence of meaning is when multiple components must agree on the meaning of particular values. Consider some code that processes credit card payments. The following function might be used to determine if a given credit card number is valid or not:

意味のコナーセンスは複数のコンポーネントが特定の値の意味に関して一致しなければならないときに発生します。クレジットカード決済を処理するコードを考えてみます。以下の関数はクレジットカード番号が有効かどうかを判定するためのものです。

.. code-block:: python

    def is_credit_card_number_valid(card_number):
        # Check for 'test' credit card numbers:
        if card_number == "9999-9999-9999-9999":
            return True
        # Do normal validation:
        # ...

.. The problem here is that all parts of this system must agree that ``9999-9999-9999-9999`` is the test credit card number. If that value changes in one place, it must also change in another.

ここで問題になるのは、このシステムの全体に渡って ``9999-9999-9999-9999`` がテスト用のカード番号であるという点で一致しなければならないということです。この値が一箇所で変更されれば、他の箇所でも変更する必要があります。

.. Here's another example where user roles are encoded as integers:

他の例を挙げます。ユーザーのロールが以下のように整数でエンコードされているとします。

.. code-block:: python

    def get_user_role(username):
        user = database.get_user_object_for_username(username)
        if user.is_admin:
            return 2
        elif user.is_manager:
            return 1
        else:
            return 0

.. Elsewhere, code might need to check that a given username is an administrator, like so:

別の場所で、与えられたユーザー名が管理者権限を持つかどうかを確認する必要があるかもしれません。

.. code-block:: python

    if get_user_role(username) != 2:
        raise PermissionDenied("You must be an administrator")

.. Connascence of meaning can be improved to connascence of name by moving the "magic values" to named constants, and referring to the constants instead of the values. However in doing so, we have increased the amount of connascence of name (since we now need a third location to store the constant).

「マジックバリュー」を名前付き定数に移動し、値の代わりに定数を参照するようにすれば、意味のコナーセンスは名前のコナーセンスへと改善できます。しかしそうしたとしても、名前のコナーセンスの量は増えます（定数を保存するためにまた別の場所を必要とするからです）。

.. Another common example of connascence of meaning is when ``None`` is used as a return value. This frequently occurs in functions that are tasked with finding an object. If that object isn't found, the function might return ``None``. 

他のよくある例は、``None`` が返り値として使われる場合です。これは何らかのオブジェクトを見つけるタスクを実行する関数でよく起こります。オブジェクトが見つからなければ ``None`` を返すというわけです。

.. code-block:: python

    def find_user_in_database(username):
        return database.find_user(username=username) or None

.. However, the function might also return None in an error condition:

しかし、この関数はエラーが起きたときにも None を返すかもしれません。

.. code-block:: python

    def find_user_in_database(username):
        try:
            return database.find_user(username=username) or None
        except DatabaseError:
            return None

.. The problem in both these cases is that a semantic meaning is being assigned to the ``None`` value. If multiple different meanings are assigned to the same ``None`` value in the same codebase, the programmer must remember which meaning applies to which case. This can be improved to connascence of name by returning an explicit object that represents the case in question:

この両ケースで問題なのは、セマンティックな意味が ``None`` の値に割り当てられていることです。一つのコードベース内で同じ ``None`` が複数の異なる意味を持っていると、プログラマーがどの場合にどの意味になっているかを覚えておかなければならなくなります。これは当該の状態を明示的に表すオブジェクトを返すようにすることで、名前のコナーセンスへと改善できます。

.. code-block:: python

    def find_user_in_database(username):
        try:
            return database.find_user(username=username) or ObjectNotFound
        except DatabaseError:
            return None

.. We still have connascence of meaning in the error case, but at least the ``None`` value is no longer ambigous. The error case could also be improved to connascence of name in a similar way.

エラー発生時の処理に意味のコナーセンスがまだ残っていますが、少なくとも ``None`` の値は曖昧でなくなりました。エラー発生時の処理も同じようなやり方で名前のコナーセンスに改善できます。

.. Another common example of connascence of meaning is when we use primitive numeric types to represent more complex values. Consider this line of code in a codebase that processes payments:

さらに他のよくある例は、プリミティブな数値型で複雑な値を表現しようとする場合です。決済を処理するコードベースの中にあるこんな行を考えてみてください。

.. code-block:: python

    unit_cost = 49.95

.. What currency is that cost expressed in? US dollars? British pounds? How do you ensure that two costs with different currencies are not added together? Similar to the examples above, the problem is that a semantic meaning is being added to the primitive type. It can be improved to connascence of type by creating a 'Cost' type that disallows operations between different currencies:

コストはどの通貨で表現されているのでしょうか。米ドルでしょうか、それとも英ポンドでしょうか。通貨が異なる場合はコストを足し合わせられないことをどのように保証できるでしょうか。今までの例と同じように、問題はセマンティックな意味がプリミティブ型に与えられていることです。'Cost' 型を作成して異なる通貨間の操作をできないようにすれば、これは型のコナーセンスに改善できます。

.. code-block:: python

    unit_cost = Cost(49.95, 'USD')

.. This particular problem is often called "**Primitive Obsession**", and can be generically described as using primitive data types to represent more complex domains. 

特にこの問題は「**プリミティブ型への執着**」と呼ばれることがあり、プリミティブデータ型で複雑なドメインを表現しようとする問題として一般に知られています。
