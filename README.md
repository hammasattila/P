# 1. Programozás

## 1.1. Változok

| Típus         |    Formázókarakter     | Méret  |        Tartomány         | Megjegyzés                                                                               |
| ------------- | :--------------------: | :----: | :----------------------: | ---------------------------------------------------------------------------------------- |
| char          |         `"%c"`         | 1 byte |        -128...127        | Egy ASCII karakter.                                                                      |
| short         |  `"hd%"` vagy `"hi%"`  | 2 byte |      -32768...32767      | Egy 16 bitten tárol egésszám.                                                            |
| int           |   `"%d"` vagy `"%i"`   | 4 byte | -2147483648...2147483647 | Egy 32 bitten tárol egésszám.                                                            |
| long int      |  `"%ld"` vagy `"%li"`  | 4 byte | -2147483648...2147483647 | Egy 32 bitten tárol egésszám.                                                            |
| long long int | `"%lld"` vagy `"%lli"` | 8 byte | -2147483648...2147483647 | Egy 64 bitten tárol egésszám.                                                            |
| float         |         `"%f"`         | 4 byte |  kb. ±9*10<sup>18</sup>  | Egy 32 bitten tárol lebegőpontos szám.                                                   |
| double        |        `"%lf"`         | 4 byte |  kb. ±10<sup>309</sup>   | Egy 64 bitten tárol lebegőpontos szám.                                                   |
| char [n]      |         `"%s"`         | n byte |            -             | Egy karakterekből álló tömb. Még szokták nevezni **karakterlánc**nak vagy **string**nek. |
| <típus> *     |         `"%p"`         | 4 byte |            -             | Egy memmória cim. Még szokták nevezni **mutató**nak vagy **pointer**nek.                 |

Egy változónak le tudjuk kérni a címét a `&` operátorral.

## 1.2. Példák

```c++
int i;                          // Deklaráció (Nincs adva kezdeti érték.)
int d = 3;                      // Definicó (Van adva kezdeti érték.)
int o = 053;                    // 8-as számrendszerben van megadva.
int x = 0x16;                   // 16-as számrendszerben van megadva.
float f = 123.456;
double lf .6078;
char c = 'A';
char s[5] = "alma";             // A karakterlánc mérete eggyrl nagyobb kell legyen mint a bene levő betük száma.
char str[] = "Hello World!";    // Ha egyből adunk kezdeti értéket akkor nem szükséges megadni a tömb méretét, a fordító ki tudja találni.

int *ptr = &i;                  // Az 'i' változó cime elmentve az int mutató 'ptr' változóba.
```

## 1.3. Írás/Olvasás

### 1.3.1. Képernyőre

A képernyőről való olvasásra és a képernyőre való írásra vanak C függvények: `scanf("<formázósor>", <mutató>, <mutató>, ...);` és `printf("<formázósor>", <változó>, <változó>, ...);`

![Printf használatára példa.](./assets/images/C-IO.png)

```c
int i;
printf("Kérem a számot:\n");
scanf("%i", &i);
printf("A szám: %i\n", i);
```

A képernyőről való olvasásra és a képernyőre való írásra vanak C++ függvények: `cin >> <változó>;` és `cout << <változó>;`

```c++
int i;
std::cout << "Kérem a számot:" << std::endl;
std::cin >> i
std::cout << "A szám: " << i << std::endl;
```

## 1.4. Feltételes utasítások

Párhuzamos forgatókönyvek. Egy feltétel szerint eldöntjük melyik uton haladunk tovább: if (`<feltétel>`) { `<utasítások>` } else { `<utasítások>` }

![If else ábra.](./assets/images/if-else.png)

A feltételben összehasonlító operátorokat éehet használni, mint például: `==`, `!=`, `<`, `<=`, `>`, `>=`, stb.

```c++
/**
 * Írjunk egy programot amely meghatározza egy másodfokú polinom gyökeit: ax^2 + bx + c = 0.
 * Olvassuk be az a, b, c értékeket és száoljuk ki az x1-t és x2-t.
 **/
double a,b,c,delta,x1,x2;
scanf("%lf%lf%lf", &a ,&b, &c);
if (a != 0){
    delta = b*b – 4*a*c;
    if (delta >= 0) {
        x1 = (–b + sqrt(delta)) / (2*a);
        x2 = (–b – sqrt(delta)) / (2*a);
        printf("Gyokok: %.2lf, %.2lf", x1, x2);
    } else {
        printf("Komplex gyokok!");
    }
} else {
    printf("Nem masodfoku!");
}
```

**C89**: minden nem nulla numerikus érték logikai értéke IGAZ, a nulla pedig HAMIS. Lwhwt alkalmazni a boolalgebra alap logikai operátorait: `!` (NEM), `&&` (ÉS), `||` (VAGY).

|   A   |   B   | A && B | A \|\| B |
| :---: | :---: | :----: | :------: |
|   0   |   0   |   0    |    0     |
|   0   |   1   |   0    |    1     |
|   1   |   0   |   0    |    1     |
|   1   |   1   |   1    |    1     |

Egy kevésbé verbális elágazás a kérdőjel operátor: `<kif1>` ? `<kif2>` : `<kif3>`

```c++
int b =1 
printf( b ? "IGAZ\n" : "HAMIS\n" );
/**
 * if-else megfelelője:
 * if (B) {
 *      printf("IGAZ\n");
 * } else {
 *      printf("HAMIS\n");
 * }
```

Ha töbszörös elágazásra van szükség lehet használni a `switch` elágazást.

```c++
/**
 * switch (<kifejezés>){
 * case <konstans_1> : <utasítások>; [break;]
 * ...
 * case <konstans_n> : <utasítások>; [break;]
 * [ default <utasítások> ]
 * }
 **/
int jegy;
scanf(“%i”, &jegy);
switch (jegy){
    case 5 : printf(“jeles”); break;
    case 4 : printf(“jo”); break;
    case 3 : printf(“kozepes”); break;
    case 2 : printf(“elegseges”); break;
    case 1 : printf(“elegtelen”); break;
    default: printf(“nem jegy”);
}
```

## 1.5. Ciklusok

### 1.5.1. While ciklus

while ( `<feltétel>` ) { `<utasítások>` }
