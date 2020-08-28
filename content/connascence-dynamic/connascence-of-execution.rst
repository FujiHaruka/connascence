実行のコナーセンス
########################

:name: 実行
:strength: 50
:slug: execution
:summary: 実行のコナーセンスは複数のコンポーネントの実行する順序が重要なときに生じます。

.. Connascence of execution is when the order of execution of multiple components is important. Common examples include locking and unlocking resources, where locks must be acquired and released in the same order everywhere in the entire codebase. 

実行のコナーセンスは複数のコンポーネントの実行する順序が重要なときに生じます。よくある例はリソースのロックとアンロックで、コードベース全体のいたるところでロックの確保と解放が同じ順序で実行される必要があります。

.. Connascence of execution can also occur when using objects that encapsulate a state machine, and that state machine only allows certain operations in certain states. For example, consider a hypothetical ``EmailSender`` class that allows a caller to generate and send an email:

実行のコナーセンスは状態マシンをカプセル化するオブジェクトを使う場合にも生じます。状態マシンは特定の状態にあるときに特定の操作だけを許可します。たとえば、Eメールを生成して送信する仮の ``EmailSender`` クラスを考えてみましょう。

.. code-block:: python

    email = Email()
    email.setRecipient("foo@example.comp")
    email.setSender("me@mydomain.com")
    email.send()
    email.setSubject("Hello World")

.. The last two lines show a trivial example of connascence of execution. The ``setSubject`` method cannot be called after the ``send`` method (at best it will do nothing). In this example the `locality <{filename}/properties/locality.rst>`_ of the coupling is very low, but cases where the locality is very high can be much harder to find and fix (consider, for example a scenario where the last two lines are called on separate threads).

末尾２行が実行のコナーセンスに当たるトリビアルな例です。``setSubject`` メソッドを  ``send`` メソッドの後に呼び出すことはできません（エラーにならないとしても何もしません）。この例では結合度の `局所性 <{filename}/properties/locality.rst>`_ は非常に小さいですが、局所性が非常に大きいと発見と修正がずっと難しくなります（たとえば末尾２行が別のスレッドで呼ばれるというシナリオを考えてみてください）。
