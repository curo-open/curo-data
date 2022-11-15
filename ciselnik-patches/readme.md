# NCZI xml patches

- sposob ako doplnit/prepisat NCZO XML
- pre kazdy XML subor moze tu existovat jeho dalsi doplnok
- jednotlive polozky budu merged (podla `codeValue`, alebo `Skratka`; case=insensitive)
- pokial ma byt polozka **len pridana**, potom musi XML polozky obsahovat:

```xml

<PolozkaCiselnika>
    <operation>insert</operation>
    ...
```

vid priklad: `1.3.158.00165387.100.10.26-union-lowercase.xml`

- xml subor sa musi volat tak isto ako codesystem-id, ale moze mat dodatocny suffix, ktory sluzi len ako
  poznamka, aky bol dovod na dane polozky.
