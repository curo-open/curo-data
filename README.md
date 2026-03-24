# curo-data

## vykony.csv

- sluzi na dodatocne doplnenie do uz existujucich vykonov
- kod - bude pouzity na sparovanie s vykonom existujucim v NCZI (case-insensitive)
- body,typ,nazov -> tieto polozky budu potom prepisane

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