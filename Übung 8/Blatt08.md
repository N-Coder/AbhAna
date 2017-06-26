Blatt 08 (Schnelltests)
=======================

13a) (GCD- und Extreme Value Test)
----------------------------------

Reihenfolge:

1. Einfacher GCD
2. Extreme Value Test
3. Erweriterter GCD

Drei Arrays: A, B, C

Für A, Einfacher GCD

    j = j'          j-j' = 0            =>  gcd(1, -1) | 0
    2i = 2i+1       2i-2i' = 1          =>  gcd(2, -2) | 1
                                        =>           2 | 1
    Nicht lösbar

Für B, einfacher GCD

    i = i' + 1      i - i' = 1          =>  i-i' = 1
    i = i'          i - i' = 0          =>  gcd(1, -1) | 0

    Keine Ahnung

Für B, Extreme Value Test

    0 <= i <= n
    0 <= j <= i

    lower  |  upper  |  elim
    -------+---------+--------
    i - i' | i - i'  | i
    -i'    | n-1-i'  | i'
    -n+1   | n-1     | n
    -inf   | inf     |

    Keine Ahnung

Für B, erweiterter GCD

             /  1  1 \ 
    (i i') * \ -1 -1 / = (1 0)

    /  1  1 \      / 1 1 \
    \ -1 -1 /  ~>  \ 0 0 / = (1 0)

             / ..........

    t1 = 1
    t1 = 0      => Keine Abhängigkeiten

Für C: Einfacher GCD

    i+j = j'-i'     =>  i+j+i'+j' = 0   =>  gcd(1,1,1,-1) | 0

    Keine Ahnung

Für C: Extreme Value Test

    0 <= i <= n
    0 <= j <= i

    lower       | upper         | elim
    ------------+---------------+----------
    i+j+i'-j'   | i+j+i-j'      | j, j'
    i+i'-(i-1)  | i+j-1+i'      | i, i'
    1           | 2(n-1)+n-1-1  |
    1           | 3n-4          | n
    1           | inf           |

    0 in [1,inf)?  =>  Nein, keine Abh.


14) Preprocessing
-----------------

    void foo(int n, int m, double B[n]) {
        const int nm = n*m;
        for (int i=0; i < n; ++i) {
            double s = 0.0;
            double A[nm];
            A[0] = rand();
            for (int j=0; j<nm; ++j) {
                A[j+1] = exp(i*j*3.141) + A[j];
                s += A[j+1] + (j+2)%2;
            }
            B[i] = s;
        }
    }

Abhängigkeiten nur über der inneren Schleife!

