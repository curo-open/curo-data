# NCZI xml patches

folder `ciselnik-patches` moze obsahovat subory nazvane codeSchemaId.(xml|str)

- `.str` znamena ze je to kompletny overwrite ciselnika (e.g. msluzba)
    - v pripade str sa pouzije vzdy len posledny item (sorted)
        (teda ucel je nazvat ho podla roku:
        1.3.158.00165387.100.10.23-2026.str; *2027*, etc)
- `.xml` su spracovane ako merge alebo insert (podla property `<operation>`,
    vid nizsie)

- sposob ako doplnit/prepisat NCZI XML
    - pre kazdy XML subor moze tu existovat jeho dalsi patch
    - jednotlive polozky budu merged (podla `codeValue`, alebo `Skratka`;
        case-insensitive).
        to
        znamena ze vlastnosti z patch-suboru prepisu hodnoty uz existujucej
        NCZI-polozky
    - pokial ma byt polozka **len pridana**,
        potom musi XML polozka obsahovat `<operation>insert</operation>`
        (vid priklad: `1.3.158.00165387.100.10.26-union-lowercase.xml`):

```xml

<PolozkaCiselnika>
    <operation>insert</operation>
    ...
```

- `*.(xml|str)` subor sa musi volat tak isto ako codesystem-id,
    ale moze mat dodatocny `som musel-suffix`, ktory sluzi len ako poznamka,
    aky bol dovod na prepisanie polozky

## zoznam codesystemId:

```yaml
- codesystemId: 1.3.158.00165387.100.10.25  #  diagnoza
- codesystemId: 1.3.158.00165387.100.10.26  #  vykon
- codesystemId: 1.3.158.00165387.100.10.51  #  stat
- codesystemId: 1.3.158.00165387.100.10.52  #  labvys
- codesystemId: 1.3.158.00165387.100.10.90  #  sposob-podania
- codesystemId: 1.3.158.00165387.100.10.13  #  liekova-forma
- codesystemId: 1.3.158.00165387.100.10.206 #  typ-davkovania
- codesystemId: 1.3.158.00165387.100.10.83  #  atc
- codesystemId: 1.3.158.00165387.100.10.37  #  cinnost
- codesystemId: 1.3.158.00165387.100.10.39  #  zameranie
- codesystemId: 1.3.158.00165387.100.10.34  #  odbornost
- codesystemId: 1.3.158.00165387.100.10.35  #  ockovanie
- codesystemId: 1.3.158.00165387.100.10.36  #  octyp
- codesystemId: 1.3.158.00165387.100.10.116 #  oczrusenie
- codesystemId: 1.3.158.00165387.100.10.158 #  alergen
- codesystemId: 1.3.158.00165387.100.10.58  #  reakcia
- codesystemId: 1.3.158.00165387.100.10.159 #  prejav
- codesystemId: 1.3.158.00165387.100.10.87  #  merjednotka
```

## ukrajina
- ciselnik-patches/1.3.158.00165387.100.10.26-UA.xml
