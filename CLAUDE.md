# Site web de Christian Gagné, version anglaise — règles de gestion

Dépôt Jekyll de la version anglaise du site, servie par GitHub Pages sous
`christiangagne.net/english` : le domaine du site français couvre tout l'hôte
`chgagne.github.io`, dépôts de projet compris. La langue de travail de ce dépôt
est le **français** : ces instructions et les messages de commit sont en
français, comme dans le dépôt du CV.

Le site français vit dans un dépôt séparé, `~/Claude/Webpage/chgagne.github.io`,
qui porte les mêmes règles. Les deux sont indépendants : chacun a son
historique, ses commits et ses poussées.

## Le CV est la source

Le contenu factuel vient de `~/Claude/CV` et de nulle part ailleurs.

- **Rien de plus riche que le CV.** Aucun fait qui n'y soit d'abord. Ce qui
  paraît d'abord ici est une dette à reporter au CV, pas une source parallèle.
- **Le site en dit moins, jamais autre chose.** Il est un sous-ensemble choisi :
  une page personnelle se lit vite, le CV est exhaustif. Omettre est permis,
  contredire ne l'est pas.
- Ce qui est délibérément absent se consigne dans `~/Claude/CV/tools/liaison-web.txt`,
  avec son motif et sa date. Sans cela le contrôle le signalera à chaque passage
  et on finira par ne plus le lire.

## Symétrie français / anglais

**Toute modification factuelle s'applique aux deux dépôts dans le même geste.**
Une correction faite d'un seul côté est un travail incomplet, pas un travail
partiel.

C'est la règle qui manquait. Au 2026-09-28, trois défauts n'existaient que de ce
côté-ci : GIF-3000 listé deux fois, le lien vers la page d'Anne-Sophie Charest
tronqué d'une lettre, et une parenthèse doublée qui cassait le lien de la
section spéciale *Evolutionary Art*. Les deux cours actuels portaient encore
leur titre français.

Seules les différences proprement linguistiques diffèrent légitimement :
formulation, titres de cours et d'organismes, variantes d'URL (`/en`).

## Marqueurs de liaison

Des commentaires HTML, invisibles au rendu, relient les pages au CV. Ils sont
lus par `check-web.py` ; **ne pas les retirer**.

| marqueur | où | rôle |
|---|---|---|
| `<!-- cv-section: a, b -->` | après un titre | les sous-sections du CV que cette rubrique couvre |
| `<!-- cv-hors-portee -->` | après un titre | zone propre au site, jamais confrontée au CV |
| `<!-- cv: slug -->` | en fin d'entrée | apparie l'entrée à un `% web: slug` du `.tex` |

`cv-section` et `cv-hors-portee` portent du titre qui les précède jusqu'au titre
suivant de même niveau ou de niveau supérieur ; placés avant tout titre, ils
couvrent le préambule de la page.

Deux points à retenir :

- **Deux rubriques qui couvrent la même portion du CV portent la même
  déclaration.** « Current Appointments » et « Previous Appointments » se partagent
  une seule liste du CV ; sans la déclaration sur les deux, chacune signale les
  entrées de l'autre comme manquantes.
- **`cv-section` gouverne la complétude, pas l'appariement.** Une entrée marquée
  se rapproche de son item du CV où qu'il vive. C'est ce qui laisse le groupe de
  travail sur l'électrification des transports figurer ici alors qu'il est rangé
  au CV parmi les comités locaux, hors du contrôle.

Les personnes, les cours et les logiciels n'ont pas besoin de marqueur : le nom,
le sigle et le nom du projet suffisent à les apparier.

## Vérification avant commit

```sh
python3 ~/Claude/CV/tools/check-web.py
```

Aucun écart non expliqué, sans quoi le commit attend. Le contrôle lit les deux
sites d'un coup, donc il vaut pour les deux dépôts.

**La construction Jekyll locale n'est pas possible sur cette machine** : seul le
Ruby système 2.6.10 est installé, sans `Gemfile.lock` ni chaîne `github-pages`.
À ajouter à cette liste le jour où une chaîne Ruby sera en place.

En attendant, à l'œil sur toute page modifiée : syntaxe des liens markdown
(`]((` doublé, espace collée à l'astérisque d'italique, parenthèses
déséquilibrées) et adresses sortantes. Au 2026-09-28, seize liens sur cent
trente-quatre ne résolvaient plus, dont quatre en page d'accueil : Université
Laval déplace ses sites vers `fsg.ulaval.ca`, et les pages personnelles des
anciens étudiants déménagent.

## Autonomie

Une modification vérifiée est commitée sans demander : un changement logique par
commit, message en français à l'impératif ou en substantif, dans le style de
l'historique.

**Ne jamais pousser sans demander.** La poussée *est* la mise en ligne : GitHub
reconstruit le site à la révision poussée et la publie aussitôt. Il n'y a pas
d'étape entre `git push` et le site public.

## Garde-fous de contenu

- **Ne jamais inventer un fait.** Date, nom d'étudiant, titre de thèse, lieu,
  adresse : ce qui n'est ni au CV ni fourni par Christian fait l'objet d'une
  question, pas d'une supposition plausible. Une URL est un fait : la résoudre
  avant de l'écrire, jamais la construire par analogie.
- **Demander avant de retirer du contenu.** Seules les corrections de forme et
  de coquilles se font sans demander.
- **Noms et diacritiques à l'identique.** Reproduits exactement tels que
  fournis, jamais normalisés ni anglicisés.

## Publication du CV

Les PDF vivent dans `files/`. Les recopier depuis `~/Claude/CV` fait partie de
la publication du CV, décrite dans le `CLAUDE.md` de ce dépôt-là.
