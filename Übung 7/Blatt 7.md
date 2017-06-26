Aufgabe 12
==========

Für S-T-(True)-Konflikt:
------------------------

1. `S[i', j'] -> T[i]`
2. Konfliktgleichungssystem
    
    i = 4i' - 2j'

3. Existenzbedingungen

    0 <= 1' <= n
    0 <= j' <= i' -1
    0 <= i <= n (Kontext)

    Der Kontext beinhaltet Bedingungen, die nicht nur für eine Abhängigkeit spezifisch sind, sondern von vornherein gegeben sind.

4. Ordnung

    i' < i or (i' = i and "S vor T")
    `----------.---------´  `---.---´
            i' <= i            true

Zusammenfassung:

    =>  i = 4j' - 2j'
        0 <= j' < i' <= i <= n

    S[i', j'] -> T[4i' - 2j']: 0 <= j' < i' <= i <= n

5. Optimierung

     i' = i
     i' = 4i' - 2j'
      0 = 3i' - 2j'
    2j' = 3i'

    S[i, i-1] -> T[2i+2]: i > 0 and 2i <= n-2

Konflikt für U-T:
-----------------

1. `U[i'] -> T[i]`
2. Konfliktgleichungssystem

    i = i' + 13

3. Existenz

    0 <= i <= n
    0 <= i' <= n

4. Ordnung
    
    i' < i or (i' = i and "U vor T")
                          `---.---´
                            false
           `----------.----------´
                    false

    =>  i = i' + 13        ------. .-----    0 <= i'
        0 <= i' < i <= n         | |
                                 v v

                             0 <= i - 13
                         =>  i >= 13

    U[i - 13] -> T[i]: 13 <= i  <= n

5. Optimierung (keine)

Mit ISL S-T und U-T mischen

Single-Assignment-Form
----------------------




