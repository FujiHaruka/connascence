局所性
########

:name: 局所性
:slug: locality
:strength: 10
:summary: コナーセンスの局所性は２つのエンティティが互いにどれだけ近くにあるかです。

.. The *locality* of an instance of connascence is how close the two entities are to each other. Code that is close together (in the same module, class, or function) should typically have more, and higher forms of connascence than code that is far apart (in separate modules, or even codebases). Many of the stronger forms of connascence that can be devastating to the readability and maintainability of a codebase when they appear far apart are innocuous when close together.

コナーセンスの *局所性* は２つのエンティティが互いにどれだけ近くにあるかです。互いに近くにあるコード（同じモジュール、クラス、関数内など）には通常、遠くにあるコード（別のモジュールや別のコードベースなど）よりも大きく高い形のコナーセンスがあるべきです。強い形のコナーセンスが互いに離れた場所にあるとコードベースの可読性と保守性に壊滅的な影響を与えることがありますが、互いに近くにあれば無害です。

.. image:: {filename}/images/locality.svg
	:class: center-block

.. Locality matters! Stronger connascences are more acceptible within a module. Weaker connascences should be used between entities that are far apart (in separate modules or even codebases).

局所性が重要です！　強いコナーセンスでも同じモジュール内にあれば許容できます。離れた場所（別のモジュールや別のコードベースなど）にあるエンティティ間ではより弱いコナーセンスが使用されるべきです。
