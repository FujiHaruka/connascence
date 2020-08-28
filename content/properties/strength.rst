強度
########

:slug: strength
:strength: 0
:summary: コナーセンスの形の強度は結合度の種類をリファクタリングする容易さによって決定されます。

.. The *strength* of a form of connascence is determined by the ease with which that type of coupling can be refactored. For example, `connascence of name <{filename}/connascence-static/connascence-of-name.rst>`_ is a weak form of connascence because renaming entities across a codebase is usually reasonably trivial. However, `connascence of meaning <{filename}/connascence-static/connascence-of-meaning.rst>`_ is considered a stronger form of connascence since semantic meaning is harder to find across an entire codebase.

コナーセンスの *強度* は結合度の種類をリファクタリングする容易さによって決定されます。たとえば、`名前のコナーセンス <{filename}/connascence-static/connascence-of-name.rst>`_ はコードベース全体にわたってエンティティの名前を変更するのは通常トリビアルな変更といえるので、弱い形のコナーセンスです。しかし、`意味のコナーセンス <{filename}/connascence-static/connascence-of-meaning.rst>`_ はセマンティックな意味をコードベース全体にわたって発見するのが難しいため、より弱い形のコナーセンスと考えられます。

.. Static connascences are considered to be weaker than dynamic connascences, since static connascences can be determined simply by examining the source code. Dynamic connascences require knowledge of run-time behavior, and thus are harder to reason about.

静的なコナーセンスは動的なコナーセンスと比べると単にソースコードを調べることで決定できるため、弱いと考えられます。動的なコナーセンスは実行時のふるまいに関する知識を必要とするため、推測がより難しくなります。

.. Strength and `locality <{filename}/properties/locality.rst>`_ should be considered together. Stronger forms of connascence are often found within the same function, class, or module where their impact can be more easily observed.

強度と `局所性 <{filename}/properties/locality.rst>`_ は一緒に考えるべきです。より強い形のコナーセンスは同じ関数、クラス、モジュールの中でよく発見されますが、その場合は影響範囲が容易に観察できます。
