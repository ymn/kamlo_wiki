* * * * *

Findlib -
[http://projects.camlcity.org/projects/findlib.html/](http://projects.camlcity.org/projects/findlib.html/)
-- менеджер библиотек для Ocaml.

Библиотека, с точки зрения findlib, -- это набор файлов, реализующих
функционал библиотеки и файл META, определенного формата, в котором
записана информация о библиотеке: название, версия, описание,
зависимости, состав и др.

После установки создайте в `site-lib` каталог `stublibs` и добавьте путь к нему в 
`$(ocaml -where)/ld.conf`.

Кстати, RTFM, там подробно и доступно всё описано.

ocamlfind
---------

С помощью утилиты ocamlfind, входящей в состав findlib, можно
устанавливать, удалять и использовать во время компиляции библиотеки,
поддерживающие findlib.

Типичное использование:

```
ocamlfind install -patch-version $version $packagename META x.mli x.cma x.cmi -optional x.a x.lib x.so x.dll x.cmx x.cmxa
```

Использование в top-level
-------------------------

Скрипт "topfind" предоставляет удобное средство работы с библиотеками из
топлевела.

Команды:

-   \#use "topfind" загружает findlib
-   \#list отображает список установленных в системе библиотек
-   \#require <имя библиотеки\> добавляет в load path необходимые для
    загрузки библиотеки пути и загружает библиотеку
-   \#camlp4o;; загружает camlp4 (стандартный синтаксис)
-   \#camlp4r;; загружает camlp4 (revised syntax)
-   Topfind.reset();; перезагружает библиотеки
-   \#thread;; включает нити(threads)

Инфраструктура
--------------

Подпакеты - средство организации пространств имён для библиотек.
Синтаксические расширения принято держать в подпакете `.syntax`.

Пример (компиляция с использованием синтаксического расширения):

```
ocamlfind ocamlc -linkpkg -syntax camlp4o -package deriving.syntax q.ml -o q
```

Пример (использование синтаксического расширения в интерпретаторе):

```
       Objective Caml version 3.11.2

# #use "topfind";;
- : unit = ()
# #camlp4o;;
	Camlp4 Parsing version 3.11.2

# #require "deriving.syntax";;
# type t = A | B deriving (Show);;
type t = A | B
```

See also
--------

- [Q: Using “ocamlfind” to make the OCaml compiler and toplevel find (project specific) libraries](http://stackoverflow.com/questions/2023173/using-ocamlfind-to-make-the-ocaml-compiler-and-toplevel-find-project-specific/2056896#2056896)
- [Q: OCaml toplevel with syntax extensions](http://stackoverflow.com/questions/7438373/ocaml-toplevel-with-syntax-extensions)
- [Q: Which .cma file corresponds with which module in OCaml?](http://stackoverflow.com/a/9717348/118799)
- [Q: How can the ocamlfind/ocamlbuild toolchain be used with project-local copies of packages?](http://stackoverflow.com/questions/7274960/how-can-the-ocamlfind-ocamlbuild-toolchain-be-used-with-project-local-copies-of)

TODO
----

- ocamlfind ocamlc -package name1,name2 -linkpkg
- написание META
- установка библиотек
