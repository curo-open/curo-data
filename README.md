# curo-data

## vykony.csv

- sluzi na dodatocne doplnenie do uz existujucich vykonov
- kod - bude pouzity na sparovanie s vykonom existujucim v NCZI (case-insensitive)
- body,typ,nazov -> tieto polozky budu potom prepisane

### pridanie pripocitatelnej polozky (PP) k vykonom

typicky ticket: *"do ciselnika vv potrebujeme pridat pripocitatelnu polozku AKUT
k tymto vykonom: 60, 60R, 62, 63, ..."*

PP nie je samostatny zaznam. pre **kazdu** dvojicu vykon+PP vznikne novy
samostatny vykon s kodom `<vykon>+<PP>`. teda 18 vykonov v tickete = 18 novych
riadkov. existujuce vzory: `grep '+' vykony.csv` (`+FOB`, `+EDU`, `+POHOS`, ...)

**postup:**

1. pre kazdy vykon zo zoznamu zisti jeho **aktualny `body`**
    - `body` sa **nedopocitava automaticky** — build ho berie doslovne z CSV,
      takze ho treba vypisat rucne pre kazdy riadok
    - `body` noveho `<vykon>+<PP>` = `body` **povodneho vykonu, nezmenene**
      (PP nie je priplatok navyse)
2. pre kazdy vykon pridaj na koniec `vykony.csv` riadok:

```csv
"60+AKUT","350","","Výkon 60 s pripočítateľnou položkou AKUT"
"3262a+AKUT","1500","SVaLZ","Výkon 3262a s pripočítateľnou položkou AKUT"
```

- `kod` — velkost pismen kopiruj z povodneho riadku (`60r`, `3262a` su v CSV
  male); parovanie je aj tak case-insensitive
- `body` — z kroku 1
- `typ` — **zdedi sa z povodneho vykonu** (napr. `SVaLZ`), inak prazdne
- `nazov` — `Výkon <kod> s pripočítateľnou položkou <PP>` (s diakritikou)

3. over ze `<vykon>+<PP>` este v `vykony.csv` neexistuje (duplicitny kod by kolidoval)

**pozor:** `vykony.csv` je *jediny* subor ktory build cita — nazov je hardcoded
v `ciselnik.js` (`importVykonyOpen`). samostatny subor typu `vykony-akut.csv`
sa **nikdy nenacita**.

**co sa s tym deje v pipeline:**

- novy kod (neexistuje v NCZI) → prida sa ako novy item s `codeValue: curo-<kod>`
  (`impjruz/ciselnik.js`, CR-3434)
- `body` → `payloadSlim.props.body`, zobrazi sa ako `displayCode2` = `"350 b"`
  (`apps/curo-md/lib/sources/vykon.js`, `normalizeData`)
- `typ` → v outpute sa premenuje na `props.type` + `displayProps.typ`
    - `typ` = `!` znamena **ignoruj tento vykon** — item sa do buildu vobec nedostane

vysledok v CS po builde:

```json
{"displayCode1": "63+EDU", "displayCode2": "200 b",
 "displayName": "Výkon 63 s pripočítateľnou položkou EDU",
 "payloadSlim.ids.ezId": "curo-63+EDU@64",
 "payloadSlim.props.body": "200"}
```

## ciselnik-patch

- pozri `/ciselnik-patches/readme.md` 



## pzs@lekar.yaml

```yaml
---
# example how to remove a lekar (including all his per-PZS entries)
# this way a lekar can be deleted
#-
#  delete:      true
#  id:          A34478004
#  pzs:         P52806004202

# example how to add a lekar-per-PZS manually

```