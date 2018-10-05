# TP2 Base de données
**Auteurs** : Baptiste Bouvier et Ancelin Serre\
**Date** : 5/10/2018\
**Année** : 2018/2019\
**POLYTECH GRENOBLE RICM4**

--------------------------
> [Sujet de TD/TP](http://www-verimag.imag.fr/~devismes/BD/sujets_eleve.pdf)\
> Lien vers les cours utiles :
> - [Relations et requêtes](http://www-verimag.imag.fr/~devismes/BD/cours2.pdf)
> - [Opérations sur plusieurs relations](http://www-verimag.imag.fr/~devismes/BD/cours3.pdf)

Dans ce dépôt vous trouverez :
- Un compte-rendu en format Markdown (.md)
- Un fichier SQL (.sql) contenant l'ensemble des requêtes du TP2

## Requêtes du TD2 sur la base de données Repas

1) Obtenir les *noms* des invités du repas organisé le **31 Décembre 2004**.
```sql
SELECT nomI AS invites
FROM repas.lesrepas 
WHERE to_date(dater,'dd/mm/yyyy') = to_date('31-DEC-04','dd/mm/yyyy');
```

2) Obtenir les *noms* des vins qui ont été servis avec **un médaillon de langouste**.
```sql
SELECT DISTINCT nomV AS vin
FROM repas.lemenu 
where nomP = 'Medaillon langouste';
```

3) Obtenir les *noms* des plats (avec le *vin* qui les accompagne) qui ont été servis le **21 octobre 2003**.
```sql
SELECT nomP AS plat, nomV AS vin
FROM repas.lemenu
WHERE to_char(dater,'dd/mm/yyyy') = '21/10/2003';
```

4) Obtenir les *noms* des invités à qui il a été servi **au moins une fois du foie gras**.
```sql
SELECT DISTINCT nomI AS invites
FROM repas.lemenu NATURAL JOIN repas.lesrepas
WHERE nomP = 'Foie gras';
```

5) Obtenir les *noms* des amis qui n'ont **jamais été invités**.
```sql
-- Version avec NOT IN
SELECT DISTINCT nomA AS amis
FROM repas.lespreferences
WHERE nomA NOT IN (SELECT nomI FROM repas.lesrepas);

-- Version avec Minus
SELECT nomA as amis FROM repas.lespreferences
MINUS
SELECT nomI FROM repas.lespreferences;
```

6) Obtenir les *repas (date, plats et vins)* auxquels **Thomas et Patrick ont été invités (ensemble)**.
```sql
-- Version courte
SELECT dateR, nomP AS plat, nomV AS vin 
FROM repas.lesrepas NATURAL JOIN repas.lemenu
WHERE nomI = 'Thomas'
AND dateR IN (SELECT dateR FROM repas.lesrepas WHERE nomI = 'Patrick');

-- Version plus simple utilisant INTERSECT :
SELECT dateR, nomP AS plat, nomV AS vin 
FROM repas.lesrepas NATURAL JOIN repas.lemenu
WHERE nomI = 'Thomas'
INTERSECT
SELECT dateR, nomP AS plat, nomV AS vin 
FROM repas.lesrepas NATURAL JOIN repas.lemenu
WHERE nomI = 'Patrick'
```

7) Obtenir les *noms* des amis qui ont eu, **au moins une fois, un plat de leurs préférences**.
```sql

```

8) Obtenir les *noms* des invités qui **n'aiment que les desserts**.
```sql

```

9) Obtenir les *noms* des amis qui **n'ont jamais eu un de leurs plats préférés**.
```sql

```