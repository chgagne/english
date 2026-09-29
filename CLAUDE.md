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

Le `<span class="an">` qui entoure le millésime n'est pas un marqueur de
liaison, mais `check-web.py` le connaît : il retire les balises avant de
comparer, et sort le millésime de la clé d'appariement.

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

## Feuille de style et conventions de balisage

Depuis le 2026-09-29, `assets/css/main.scss` n'importe plus Minimal Mistakes :
tout le style tient dans `_sass/cgagne.scss`. Le thème reste sur le disque et
le balisage de ses gabarits est inchangé — `#main`, `.sidebar`,
`.page__content` — donc rebrancher son import ferait revenir en arrière.

Ce qui a été retiré : Font Awesome et sa requête vers un CDN, jQuery et ses
cinq greffons. **Le seul JavaScript servi est la bascule entre le style clair
et le style sombre**, en clair dans `_includes/scripts.html` ; n'y rien ajouter
sans nécessité. Le style suit le réglage du système, qu'un bouton de l'en-tête
permet de contredire ; le choix est retenu dans `localStorage` et appliqué en
`<head>` avant tout rendu, sans quoi la page clignote au chargement.

Les pages appellent quelques classes, toutes définies dans `cgagne.scss` :

| écriture | où | effet |
|---|---|---|
| `<span class="an">2019</span>` | fin d'une entrée de liste | le millésime passe dans la gouttière de gauche |
| `{: .lignes}` | après un paragraphe | lignes serrées, pour les rattachements et les coordonnées |
| `{: .mots}` | après une liste | des puces plutôt que des rangées séparées par un filet |
| `{: .coupure}` | après un titre de niveau 2 | titre en corps de texte, qui ouvre une vraie section |
| `{: .rubrique}` | après un titre de niveau 3 | étiquette, comme les titres de niveau 2 ordinaires |
| `<div class="axes" markdown="1">` | autour de deux titres et leurs listes | deux colonnes |
| `{: .gens}` | après une liste d'étudiants | nom en gras, reste en gris |
| `{: .cours}` | après une liste de cours | sigle en chasse fixe, titre en gras |
| `{: .logiciels}` | après la liste des logiciels | nom en gras, description en gris |
| `{: .mandats}` | après une liste de mandats | l'organisme lié ressort du rôle |
| `<span class="sigle">GIF-7010</span>` | début d'une entrée de cours | sigle en chasse fixe |
| `<span class="cpt">14</span>` | dans un titre de rubrique | le nombre d'entrées, **vérifié par `check-web.py`** |

Le compte annoncé par `<span class="cpt">` est écrit à la main, mais il ne peut
pas vieillir en silence : `check-web.py` le confronte au nombre de puces de la
rubrique et signale « compte annoncé faux » dès qu'un étudiant est ajouté sans
que le nombre suive. Les rubriques d'étudiants portent aussi un identifiant
fixe — `{: #doctorat}`, `{: .rubrique #anciens-doctorat}` — sans quoi kramdown
fabriquerait l'ancre à partir du titre, compte inclus, et elle changerait à
chaque nouvel étudiant.

Les liens du bandeau latéral et du pied de page portent un pictogramme, nommé
par `icon:` dans `_config.yml` et dessiné dans `_includes/icones.html`. Le jeu
est posé une seule fois par page, en `<symbol>`, et repris par `<use>` ; c'est
du SVG en ligne, donc **aucune requête vers un tiers**. Les quatre marques
viennent de Simple Icons (CC0) ; le courriel et le document sont dessinés à la
main. Ajouter un lien sans `icon:` fonctionne : le libellé paraît seul.

**Il n'y a plus d'analytique.** Le script Google pointait depuis des années sur
`UA-4723811-1`, un identifiant Universal Analytics que Google n'alimente plus
depuis 2023 : il se chargeait en production sans rien mesurer. Le bloc de
configuration, l'appel et les inclusions du thème ont été retirés le
2026-09-29. N'en remettre qu'à la demande de Christian.

Le millésime **reste en fin de ligne**, là où le CV l'écrit : c'est la feuille
de style qui le remonte, pas le balisage. Le mettre en tête casserait la clé
d'appariement de `check-web.py`, qui lit le début du texte.

`nav:` dans l'en-tête Jekyll porte l'identifiant du lien de navigation à
marquer comme courant ; il doit correspondre à un `id:` de
`_data/navigation.yml`. Comparer les URL ne fonctionnerait pas des deux côtés,
le site anglais étant servi sous `/english`.

La gouttière repose sur `li:has(> .an)`. Si un navigateur ancien ignore
`:has()`, le millésime reste en fin de ligne : la page se lit encore.

## Vérification avant commit

Deux contrôles, tous deux obligatoires.

**L'écart avec le CV :**

```sh
python3 ~/Claude/CV/tools/check-web.py
```

Aucun écart non expliqué, sans quoi le commit attend. Le contrôle lit les deux
sites d'un coup, donc il vaut pour les deux dépôts.

**La construction Jekyll :**

```sh
export PATH="/opt/homebrew/opt/ruby@3.3/bin:$PATH"
bundle exec jekyll build
```

Ruby 3.3 de Homebrew est *keg-only* : sans cette ligne de `PATH`, c'est le Ruby
système 2.6.10 qui répond et rien ne fonctionne. Les gems vivent dans
`vendor/bundle`, hors du suivi de version ; `bundle install` les réinstalle.

Trois avertissements sont attendus et sans objet : la pagination sans page
d'index (le thème l'active pour un blogue qui n'existe pas ici), l'absence
d'authentification à l'API GitHub, et `faraday-retry`. **Tout le reste est un
défaut à corriger avant de commiter.** Vérifier aussi que `_site/` ne contient
que les pages voulues : `CLAUDE.md` s'y publiait comme page jusqu'à ce qu'il
soit ajouté aux exclusions du `_config.yml`.

**Prévisualiser localement.** `python3 -m http.server` ne suffit pas : GitHub
Pages sert `/recherche` en retombant sur `recherche.html`, ce que le serveur de
la bibliothèque standard ne fait pas, et les liens français paraissent alors
tous cassés. Utiliser `bundle exec jekyll serve`, qui fait la même retombée.

**Pourquoi `github-pages` est épinglée à `~> 232`** : sans contrainte, bundler
résout vers Jekyll 3.9 et Liquid 4.0.3, qui appelle `Object#tainted?`, retiré de
Ruby en 3.2. La 232 est la version que GitHub exécute et apporte Jekyll 3.10.0
avec Liquid 4.0.4. Elle exige Ruby < 4.0, d'où le 3.3 plutôt que le Ruby par
défaut de Homebrew.

**À l'œil sur toute page modifiée**, ce que la construction ne dit pas : syntaxe
des liens markdown (`]((` doublé, espace collée à l'astérisque d'italique,
parenthèses déséquilibrées) et adresses sortantes. Au 2026-09-28, seize liens
sur cent trente-quatre ne résolvaient plus, dont quatre en page d'accueil :
Université Laval déplace ses sites vers `fsg.ulaval.ca`, et les pages
personnelles des anciens étudiants déménagent. Ne jamais conclure à un lien mort
sur un seul outil : `curl` rendait 000 sur des hôtes parfaitement vivants.

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
