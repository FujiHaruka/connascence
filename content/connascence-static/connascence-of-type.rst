型のコナーセンス
###################

:strength: 10
:slug: type
:summary: 型のコナーセンスは複数のコンポーネントがエンティティの型において一致しなければならないときに生じます。


.. Connascence of type is when multiple components must agree on the type of an entity. In a statically typed language, these issues are often (but not always) caught by the compiler. Consider the following trivial C++ code:

型のコナーセンスは複数のコンポーネントがエンティティの型において一致しなければならないときに生じます。静的型付け言語では、この問題は（常にではないものの）ほとんどの場合、コンパイラが捕捉します。以下の単純な C++ コードを考えてみてください。

.. code-block:: c++

    std::string cost;

    cost = 10.95; // OOPS!

.. Dynamically typed languages typically suffer from less obvious instances of connascence of type. Consider a function that calculates your age, given your day, month, and year of birth:

動的型付け言語では型のコナーセンスが明らかでないため苦しめられる場合が多くあります。以下のような誕生年月日から年齢を計算する関数を考えてみてください。

.. code-block:: python

    def calculate_age(birth_day, birth_month, birth_year):
        # do the calculation here:

.. How is this function supposed to be called? Here are a few different options:

この関数はどのように呼ばれるでしょうか。いくつか選択肢があります。

.. code-block:: python

    calculate_age(1, 9, 1984)
    calculate_age(1, 9, 84)
    calculate_age('1', '9', '1984')
    calculate_age('1', 'September', '1984')

.. TODO - need an example of how to fix this.