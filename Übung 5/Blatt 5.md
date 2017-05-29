Aufgabe 9
=========

Für die Konfliktanalyse interessant sind die Zugriffe auf `A`. `B` könnnte potentiell Konflikte
beim Schreibzugriff verursachen, das ist aber trivial zu widerlegen.

Für `A` (Schreibzugriff in `S`, Lesezugriff in `T`)
---------------------------------------------------

    2i + 2j = 2i' - 4j' + 500
    i + 4j = -i - 5j + 600

Umformen um Matrixdarstellung zu ermöglichen (Variablen nach links, Konstanten nach rechts):

    2i + 2j = 2i' - 4j' + 500  <=>  2i + 2j + 2i' + 4j' = 500
     i + 4j = -i - 5j + 600    <=>    i + 4j + i' + 5j' = 600

Überprüfung der Lösbarkeit: Wenn der ggT der Koffizienten auf der linken die rechte Seite teilt,
existiert eine reelle, ganzzahlige Lösung der Gleichung. Dies gilt also für beide Gleichungen
separat, ob das GS insgesamt lösbar ist, ist damit noch unklar.

Händisches Lösen des GS:

    A * x = u

                  / 2 1 \
    (i j i' j') * | 2 4 | = ( 500 600 )
                  | 2 1 |
                  \ 4 5 /

    / 2 1 | 1 0 0 0 \      / 2 1 |  1 0 0 0 \      / 1 1 |  1  0 0 0 \ (*)
    | 2 4 | 0 1 0 0 |  ~>  | 0 3 | -1 1 0 0 |  ~>  | 0 3 | -1  1 0 0 |
    | 2 1 | 0 0 1 0 |      | 0 0 | -1 0 1 0 |      | 0 0 | -1  0 1 0 |
    \ 4 5 | 0 0 0 1 /      \ 0 3 | -2 0 0 1 /      \ 0 0 | -1 -1 0 1 /

                    / 2 1 \
    (t1 t2 t3 t4) * | 2 4 | = (500 600)
                    | 2 1 |
                    \ 4 5 /

           t1 = 250
    1t1 + 3t2 = 600  =>  250 + 3t2 = 600  =>  3t2 = 350  =>  t2 = 350/3  =>  Nicht ganzzahlig!

Das LGS `Ax=u` hat keine ganzzahligen Lösungen! Was tun um die ganzzahligen Lösungen des
ursprünglichen GS zu bestimmen?

Die Matrix `(*)` ist unimodular, kann das Ergebnis also nicht so "strecken", dass die Lösung
ganzzahlig wird - das ursprüngliche GS hat also ebenfalls keine ganzzahligen Lösungen. Damit
gibt es keine Zugriffskonflikte zwischen den Lesezugriffen auf `A` in `T` und den Schreibzugriffen
auf `A` in `S`.

Für `A` (Schreibzugriffe in `S` untereinander, *output dependency*)
-------------------------------------------------------------------

    2i + 2j = 2i' + 2j'  <=>  2i + 2j - 2i' - 2j' = 0
     i + 4j = i' + 4j'   <=>    i + 4j - i' - 4j' = 0

Das ggT-Kriterium hilft auch hier nicht.

    /  2  1 | 1 0 0 0 \      / 2 1 |  1 0 0 0 \
    |  2  4 | 0 1 0 0 |  ~>  | 0 3 | -1 1 0 0 |
    | -2 -1 | 0 0 1 0 |      | 0 0 |  1 0 1 0 |
    \ -2 -4 | 0 0 0 1 /      \ 0 0 |  0 1 0 1 /

                    / 2 1 \
    (t1 t2 t3 t4) * | 0 3 | = (0 0)
                    | 0 0 |
                    \ 0 0 /

           t1 = 0
    1t1 + 3t2 = 0  =>  0 + 3t2 = 0  =>  3t2 = 0  =>  t2 = 0

Im ursprünglichen GS:

                  /  1 0 0 0 \
    (0 0 t3 t4) * | -1 1 0 0 | = (t3 t4 t3 t4)
                  |  1 0 1 0 |
                  \  0 1 0 1 /

Also gibt es nur einen "Konflikt" für `i=i'` und `j=j*`, d.h. die Schreiboperation steht nur in
Konflikt mit sich selbst, was vernachlässigt werden kann.


Aufgabe 10
==========

Die Indizes `i` und `j` in `S[i,j]` zählen die Iterationen und haben *nichts* mit den Indizes der
Arrayzugriffe zu tun!

Aufgabe 10a)
------------

### Für `A` (zwei Möglichkeiten)

    S[i,j] -> T[i+1,j]
    T[i,j] -> S[i+1,j]

Der Pfeil geht "in der Zeit vorwärts", d.h. welches Statement kommt zuerst?
Exemplarisch auf `A[1,1]` greifen `T[1,1]` und `S[0,1]` zu. Deshalb ist die Abhängigkeit korrekt

    S[i,j] -> T[i+1,j]

Es handelt sich um eine anti (write after read) dependency.

### Für `B`

    T[i,j] -> S[i+3, j]

Es handelt sich um eine input (read after read) dependency.

### Für `C`

    S[i,j] -> T[i,j]

Es handelt sich um eine true/flow (read after write) dependency.

    S[i,j] -> S[i,j+1]

Exemplarisch auf `C[0,0]` wird in `S[0,1]` gelesen und in `S[0,0]` gelesen. Deshalb kommt der
Schreibzugriff zuerst und es handelt sich um eine true/flow (read after write) dependency.

Aufgabe 10b)
------------

Für `A`:

    Distanzvektor:              (1, 0)
    Richtungsvektor (Signum):   (+, 0)
    Level:                           1      weil der erste Eintrag != 0 ist

Für `B`:

    Distanzvektor:              (3, 0)
    Richtungsvektor (Signum):   (+, 0)
    Level:                           1

Für `C`:

    Distanzvektor:              (0, 0)
    Richtungsvektor (Signum):   (0, 0)
    Level:                         "3"     Textuelle, nicht schleifengetragene Abhängigkeit

    Distanzvektor:              (0, 1)
    Richtungsvektor (Signum):   (0, +)
    Level:                           2     zweite Komponente != 0

Aufgabe 10c)
------------

Relevant:

- Flow/True: Unbedingt, nicht wegrationalisierbar
- Anti/Output: Umgehbar, indem Speicher dupliziert und nicht mehr als einmal geschrieben wird
- Input: Auf gewöhnlichen Plattformen irrelevant

Aufgabe 10d)
------------

Möglichkeiten zur Parallelisierung (Siehe PDF):

- Zuerst alle `S` nach `j` aufteigend, dann alle `T`
- Zuerst `S[*,0]`, dann jeweils parallel `S[*,j]` und `T[*,j-1]`, dann `T[*,n]

