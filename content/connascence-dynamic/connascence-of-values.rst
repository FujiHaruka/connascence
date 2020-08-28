値のコナーセンス
########################

:strength: 70
:slug: value
:summary: 値のコナーセンスはいくつかの値を一緒に変更しなければならないときに生じます。

.. Connascence of value is when several values must change together. This frequently occurs between production code and test code. For example, consider an ``Article`` class, which represents a blog article. When it is instantiated, it is given some text contents, and its initial 'state' is 'draft':

値のコナーセンスはいくつかの値を一緒に変更しなければならないときに生じます。これはプロダクションコードとテストコードの間でよく発生します。たとえば、ブログ記事を表す ``Article`` クラスを考えてみましょう。これはインスタンス化されるときにテキストコンテンツが与えられ、最初の 'state' は 'draft' です。

.. code-block:: python

    class ArticleState(Enum):
        Draft = 1
        Published = 2


    class Article(object):

        def __init__(self, contents):
            self.contents = contents
            self.state = ArticleState.Draft

        def publish(self):
            # do whatever is required to publish the article.
            self.state = ArticleState.Published

.. Now imagine a hypothetical test that ensures that the ``publish`` method works:

今、``publish`` メソッドが正しく機能していることを保証する仮のテストを想像してみます。

.. code-block:: python

    article = Article("Test Contents")
    assert article.state == ArticleState.Draft
    article.publish()
    assert article.state == ArticleState.Published

.. The problem here is that the test requires knowledge of the initial state of the ``Article`` class: if the Article's initial state is ever changed, this test will break (this is arguably a bad test, since the first assertion has little to do with the intent of the test, but it's a common mistake). This code can be improved by adding an ``InitialState`` label to ``ArticleClass``, and changing both the ``Article`` class and the test to refer to that label instead:

ここで問題になるのは、テストが ``Article`` クラスの初期状態に関する知識を要求しているということです。もし Article の初期状態が変更されると、このテストは失敗します（このテストは最初のアサーションがテストの意図とほとんど関係がないためおそらく悪いテストですが、よくあるミスです）。``ArticleClass`` に ``InitialState`` ラベルを加えて ``Article`` クラスとテストが同じラベルを参照するようにすれば、このコードは改善されます。

.. code-block:: python

    class ArticleState(Enum):
        Draft = 1
        Published = 2
        InitialState = Draft

        
    class Article(object):

        def __init__(self, contents):
            self.contents = contents
            self.state = ArticleState.InitialState


.. The test now becomes:

テストは以下のようになります。

.. code-block:: python

    article = Article("Test Contents")
    assert article.state == ArticleState.InitialState
    article.publish()
    assert article.state == ArticleState.Published

.. Should we need to change the state machine of the ``Article`` class, we can do so by changing the ``ArticleState`` enumeration:

万が一 ``Article`` クラスに状態マシンを変更する必要が生じたら、``ArticleState`` enum を変更することで対応できます。

.. code-block:: python

    class ArticleState(Enum):
        Preproduction = 1
        Draft = 2
        Published = 3
        InitialState = Preproduction

.. We have effectively introduced a level of indirection between the ``Article`` class and its initial state value.

以上が、``Article`` クラスとその初期値の間にある迂回のレベルについての説明でした。
