Adderall
========

[![Build Status](https://travis-ci.org/algernon/adderall.png?branch=master)](https://travis-ci.org/algernon/adderall)

This library contains a (work in progress) implementation of
[miniKanren][mk] in [Hy][hylang]. It is a naive implementation, speed
isn't the primary concern.

 [mk]: http://minikanren.org/
 [hylang]: http://hylang.org/

Example
-------

```clojure
(import [adderall.dsl [*]])
(require adderall.dsl)

(run* [q] (condᵉ [(≡ q :tea)]
                 [(≡ q :coffee) succeed]))
;; => [:tea :coffee]

(run* [q] (condᵉ [(≡ q :tea)]
                 [(≡ q :coffee) fail]))
;; => [:tea]

(import [getpass [getuser]])

(defreader h [_] "#hy")
(defn lovesᵒ [u v] (≡ v #hy))
(run* [who what] (lovesᵒ who what)
                 (≡ who (getuser))
                 (≡ what #hy))
;; => [['algernon' '#hy']]
```

More examples can be found in the [test suite][t:generic], and in
particular, the tests [adapted][t:trs] from
[The Reasoned Schemer][trs].

 [t:generic]: https://github.com/algernon/adderall/blob/master/tests/adderall_test.hy
 [t:trs]: https://github.com/algernon/adderall/blob/master/tests/schemer/
 [trs]: http://mitpress.mit.edu/books/reasoned-schemer

Adderall also comes with a set of extra functions, which are there
mostly to show the power of the system, or for fun:

```clojure
(import [adderall.dsl [*]]
        [adderall.extra.zebra [*]])
(require adderall.dsl)
(require adderall.extra.zebra)

(run* [water-drinker horse-owner] (zebraᵖ water-drinker horse-owner))
;; => [['norvegian 'japanese]]
```

License
-------

All the code is licensed under the GNU Lesser General Public License
(v3+).
