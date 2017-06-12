# 11
## 11 a)

### Voraussetzungen für Banerjee:

- Perfekt verschachtelt (Unklar ob nötig, Vorlesung?)
- Statisch bekannter Kontrollfluss (Abbruchbedingung muss beim Schleifeneintritt (statisch)
  bekannt sein, keine `while`-Schleifen mit obskuren Bedingungen)
    - Affine Schleifengrenzen aus Strukturparametern
    - Größte Einschränkung im Polyedermodell
- Statisch bekannte Arrayzugriffe (keine Indirektion)
- Nur Skalare und Arrays als Datenstrukturen
- Keine Funktionsaufrufe
- Bedingiungen (`if`) erlaubt, solange affin

### 1. Normalisieren

Done (Stride = 1)

### 2. Potentielle Konflikte finden

- `A` wird sowohl gelesen als auch geschrieben
- `B` offensichtlich konfliktfrei

Zugriffsmatrizen bestimmen:

        As = / 2 4 \    as = (0 0)
            \ 2 4 /

        AT = / 4 4 \    aT = (-20 20)
            \ 4 0 /

Konfliktgleichungssystem für `A` in `S` und `T` (Echelon):

                        /  2  4 \
        (iS, jS, iT, jT) * |  2  4 | = (-20 20)
                        | -4 -4 |
                        \ -4  0 /

        /  2  4 | 1 0 0 0 \      / 2 4 |  1 0 0 0 \      / 2 0 | -1 0 -1 0 \
        |  2  4 | 0 1 0 0 |  ~>  | 0 0 | -1 1 0 0 |  ~>  | 0 4 |  2 0  1 0 |
        | -4 -4 | 0 0 1 0 |      | 0 4 |  2 0 1 0 |      | 0 0 | -1 1  0 0 |
        \ -4  0 | 0 0 0 1 /      \ 0 8 |  2 0 0 1 /      \ 0 0 | -2 0 -2 1 /

                        / 2 0 \
        (t1, t2, t3, t4) * | 0 4 | = (-20 20)
                        | 0 0 |
                        \ 0 0 /

        =>  t1 = -10, t2 = 5, t3 und t4 nicht eingeschränkt

                                            / -1 0 -1 0 \
        (iS, jS, iT, jT) = (-10, 5, t3, t4) * |  2 0  1 0 |
                                            | -1 1  0 0 |
                                            \ -2 0 -2 1 /

        iS  =  10 + 10 - t3 - 2t4  =  -t3 - 2t4 + 20
        jS  =  t3
        iT  =  -2t4 + 15
        jT  =  t4

        S[-t3 - 2t4 + 20, t3] <?-> T[-2t4 + 15, t4]

### 3. Existenz

        1 <= -t3 -2t4 + 20 <0= 100
        1 <= t3 <= 90
            t3 <= -t3 - 2t4 + 20
        1 <= -2t4 + 15 <= 100
        1 <= t4 <= 90
            t4 <= -2t4 + 15
        ---------------------------
        t3 + 2t4  <=  19
            -80  <=  t3 + 2t4
            1  <=  t3
            t3  <=  90
        t3 + t4  <=  10
            t4  <=  7
            -85  <=  2t4
            1  <=  t4
            t4  <=  90
            t4  <= 5

Vereinfachen:

        1 <= t3
        t3 + t4 <= 10
        1 <= t4
        t4 <= 5

Eliminiere t3:

        1 <= t3             \   1 <= t4
            t3 <= 10 - t4  /  t4 <= 5

Eliminiere t4:

        true 

### 4. Ordnung

                    iS  <  iT  ?
        -t3 - 2t4 + 20  <  -2t4 + 15
                    t3  >  5

                    iS  =  iT  ?
                    t3  =  5

                    jS  <=  jT  ?
                    t3  <=  t4

Abhängigkeiten:

        S[...] -> T[...]: t3 > 5 or (t3 = 5 and t3 <= t4)
        T[...] -> S[...]: t3 < 5 or (t3 = 5 and t3 > t4)

        not (t3 > 5 or (t3 - 5 and t3 <= t4))
        t3 <= 5 and (t3 != t5 or t3 = t4)
        t3 < 5 or (t3 <= 5 and t3 > t4)
        t3 < 5 or ((t3 < 5 or t3 = 5) and t3 > t4)
        t3 < 5 or (t3 < 5 and t3 > t1) or (t3 = 5 and t3 > t4)

### 2. Konflikt für A in S:

                      /  2  4 \
        (i j i' j') * |  2  4 | = (0 0)
                      | -2 -4 |
                      \ -2 -4 /

        /  2  4 | 1 0 0 0 \      / 2 4 |  1 0 0 0 \
        |  2  4 | 0 1 0 0 |  ~>  | 0 0 | -1 1 0 0 |
        | -2 -4 | 0 0 1 0 |      | 0 0 |  1 0 1 0 |
        | -2 -4 | 0 0 0 1 /

                        / 2 4 \
        (t1 t2 t3 t4) * | 0 0 | = ( 0 0 )
                        | 0 0 |
                        \ 0 0 /

        t1 = 0

                                       /  1 0 0 0 \
        (i j i' j') = ( 0 t2 t3 t4 ) * | -1 1 0 0 |
                                       |  1 0 1 0 |
                                       \  1 0 0 1 /

        i = -t2 + t3 + t4
        j = t2
        i' = t3
        j' = t4

Konflikt:

        S[-t2 + t3 + t4, t2] <?-> S[t3, t4]

### 3. Existenz:

        1  <=  -t2 + t3 + t4  <=  100
        1  <=  t2  <=  90
               t2  <=  -t2 + t3 + t4
        1  <=  t3  <=  100
        1  <=  t4  <= t3
               t4  <= 90
        -----------------------------
                    1  <=  -t2 + t3 + t4
        -t2 + t3 + t4  <=  100
                    1  <=  t2
                   t2  <=  90
                    0  <=  -2t2 + t3 + t4
                    1  <=  t3
                   t3  <=  100
                    1  <=  t4
                   t4  <=  t3
                   t4  <= 90

Abhängigkeiten:

        S[t2 + t3 + t4, t2] -> T[t3, t4]: t4 < t2
        
        S[...] -> T[...] : t3 > t5 or (t3 = t5 and t3 <= t4)
