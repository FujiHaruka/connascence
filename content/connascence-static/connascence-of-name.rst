名前のコナーセンス
###################

:strength: 0
:slug: name
:summary: 名前のコナーセンスは複数のコンポーネントがエンティティの名前に関して一致しなければならないときに発生します。

.. Connascence of name is when multiple components must agree on the name of an entity. Method names are an example of this form of connascence: if the name of a method changes, callers of that method must be changed to use the new name.

名前のコナーセンスは複数のコンポーネントがエンティティの名前に関して一致しなければならないときに発生します。メソッド名がこの種のコナーセンスの例です。メソッド名が変更されると、メソッドを呼び出す側が新しいメソッド名を使うよう変更する必要があります。

.. Almost any code example involves connascence of name. Consider the following class declaration taken from the Python standard library (method implementation has been omitted for clarity):

ほどんどありとあらゆるコード例に名前のコナーセンスがあります。以下の Python 標準ライブラリから取ったクラス宣言を考えてみてください（わかりやすさのためにメソッドの実装は省略しました）。

.. code-block:: python

    class Request:

        def __init__(self, url, data=None, headers={},
                     origin_req_host=None, unverifiable=False,
                     method=None):
            pass

        def set_proxy(self, host, type):
            pass

.. Changing the name of any part of this code will cause code that uses this class to break, including:

このコードのどの部分で名前を変更してもこのクラスを使っているコードは壊れてしまいます。たとえば以下の変更です。

.. * Changing the class name from ``Request``.
.. * Changing any of the method names (such as ``set_proxy``).
.. * Changing the name of any of the parameters to either ``__init__`` or ``set_proxy``.

* クラス名 ``Request`` を変更する
* メソッド名（``set_proxy`` など）を変更する
* ``__init__`` や ``set_proxy`` に与えるパラメータ名を変更する

.. Connascence of name is unavoidable, since we refer to entities using labels. If we change the name of an entity when we declare it, we must also change all code that refers to that entity. For this reason, connascence of name is the *weakest* connascence. However, it also illustrates how important it is to name entities in code well.

名前のコナーセンスは、私たちがエンティティを参照するためにラベルを使う以上は避けられません。エンティティを宣言する際にエンティティ名を変更すれば、そのエンティティを参照するすべてのコードも変更しなければなりません。このため、名前のコナーセンスは*最も弱い*コナーセンスです。しかし、このことはコードの中でエンティティを適切に命名することがいかに大切かを示してもいます。
