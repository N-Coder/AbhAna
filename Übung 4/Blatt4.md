Aufgabe 7b: Gleichungssystem mit der isl lösen
----------------------------------------------

Eingabe:

    s = Set("{ [x1,x2,x3,x4] : \
        -2x1 + x2 + x4 = 1 and \
        -2x1 + 4x2 + 2x3 + 2x4 = -4 and \
        -8x1 + 10x2 + 4x3 + 6x4 = -6 }"

Vereinfacht:

    { [ x1, x2, x3 = -3 - x1 - x2, x4 = 1 + 2x1 - x2 ] }


Aufgabe 8b: Fourier-Motzkin mit der isl
---------------------------------------

Eingabe:

    domain = Set("[n] -> { [i,j] : \
        2i >= n and \
        n-2 >= j and \
        n-i-j >= 0 and \
        j+6-3i >= 0 }")
    codegen(domain

Ausgabe:

    for (int c0 = floord(n + 1, 2); c0 <= floord(n + 1, 3); c0 += 1)
        for (int c1 = 3 * c0 - 6; c1 <= min(n - 2, n - c0); c1 + 1) 
            (c0, c1);

Dabei ist `floord` ein Makro zur floor-Division (Integer-Division in C rundet zur 0 hin,
was für negative Zahlen fälschlicherweise auf- statt abrundet).

