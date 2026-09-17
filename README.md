# Interprète

Traduction orale en temps réel, dans les deux sens, entre **français, anglais, espagnol, chinois mandarin, japonais et hindi**.

Une seule page web. Rien à installer, rien à compiler, aucun serveur. Elle tourne sur téléphone comme sur ordinateur, et une fois hébergée quelque part, le lien est à vous pour aussi longtemps que vous gardez le dépôt.

---

## 1. Ce qu'il faut pour que ça marche

| | Fonctionne | Ne fonctionne pas |
|---|---|---|
| **iPhone / iPad** | Safari | Chrome iOS (il n'a pas la reconnaissance vocale) |
| **Android** | Chrome, Edge | Firefox |
| **Windows / macOS / Linux** | Chrome, Edge | Firefox, Safari desktop (partiel) |

Il faut aussi une **connexion internet** : la reconnaissance vocale du navigateur et la traduction passent toutes les deux par le réseau.

Deux choses à préparer une seule fois :

1. **Une clé API Anthropic** (voir §3). C'est ce qui traduit.
2. **Les voix de synthèse** des langues que vous utilisez (voir §5). Sans elles, la traduction s'affiche mais ne se dit pas.

---

## 2. Mettre le lien en ligne sur GitHub Pages

Vous n'avez besoin ni de git, ni de ligne de commande. Tout se fait depuis le site.

### Étape par étape

1. Créez un compte sur **github.com** si vous n'en avez pas.
2. En haut à droite, **+** puis **New repository**.
3. Nommez-le, par exemple `interprete`. Laissez-le sur **Public** — l'hébergement de pages depuis un dépôt privé demande un compte payant. Le dépôt ne contient aucune donnée personnelle et jamais votre clé API : elle ne sera tapée que dans le navigateur, au moment de l'usage.
4. Cochez rien d'autre, cliquez **Create repository**.
5. Sur la page du dépôt vide, cliquez **uploading an existing file**.
6. Glissez-y **tous les fichiers de ce dossier** : `index.html`, `manifest.webmanifest`, `sw.js`, `robots.txt`, `icon-192.png`, `icon-512.png`, `icon-maskable.png`, `apple-touch-icon.png`.
7. Tout en bas, cliquez **Commit changes**.
8. Onglet **Settings** du dépôt, puis **Pages** dans la colonne de gauche.
9. Sous *Build and deployment* → *Source*, choisissez **Deploy from a branch**. Juste en dessous : branche **main**, dossier **/ (root)**. Cliquez **Save**.
10. Attendez une à deux minutes, rechargez la page. GitHub affiche votre adresse :

```
https://VOTRE-NOM.github.io/interprete/
```

C'est ce lien que vous ouvrez sur vos téléphones. Il ne changera plus.

### Le fichier `.nojekyll`

Il est fourni mais facultatif ici. Si votre système d'exploitation refuse de vous laisser glisser un fichier dont le nom commence par un point, ignorez-le : rien ne cassera. Si vous y tenez, dans le dépôt : **Add file → Create new file**, tapez `.nojekyll` comme nom, laissez vide, validez.

### Le mettre sur l'écran d'accueil

- **iPhone** : ouvrez le lien dans Safari → bouton Partager → *Sur l'écran d'accueil*.
- **Android** : ouvrez le lien dans Chrome → menu ⋮ → *Ajouter à l'écran d'accueil*.

Il s'ouvrira alors en plein écran, sans barre d'adresse, comme une application installée.

### Sur l'indexation par les moteurs de recherche

Trois protections sont déjà en place : une balise `noindex` dans la page, un `robots.txt` qui interdit tout, et le fait qu'aucun site ne pointe vers votre adresse. Les moteurs sérieux ne la référenceront pas.

Soyez lucide cependant : **une adresse non indexée n'est pas une adresse secrète**. Quiconque connaît le lien peut ouvrir la page. Ce n'est pas grave — la page ne contient aucune de vos données, et la clé API de chacun reste dans son propre navigateur.

### Autres hébergeurs, si GitHub ne vous convient pas

- **Netlify Drop** (`app.netlify.com/drop`) : vous glissez le dossier, vous obtenez une adresse aléatoire du type `https://mot-mot-123456.netlify.app`. Plus discret qu'une adresse `github.io` qui contient votre pseudo. Pas de compte obligatoire pour essayer.
- **Cloudflare Pages** : même principe, gratuit, avec la possibilité de mettre votre propre nom de domaine.

Dans tous les cas, ce sont les mêmes fichiers, sans rien modifier.

---

## 3. La clé API

La page a besoin d'un modèle pour traduire. Sur votre hébergement, c'est votre clé qui le fournit.

1. Allez sur **console.anthropic.com**, créez un compte, ajoutez du crédit.
2. **API keys → Create key**. Copiez la clé, elle ne sera plus affichée ensuite.
3. Dans l'appli : **Réglages → Traducteur**, collez la clé, puis **Tester la connexion**.

**Précautions, dans l'ordre d'importance :**

- Créez une clé **dédiée à cet usage**, pas celle qui sert ailleurs.
- Mettez un **plafond de dépense mensuel** dans la console. C'est votre vrai filet de sécurité.
- La clé est enregistrée dans le navigateur de l'appareil. Toute personne qui a l'appareil déverrouillé peut la lire. Si vous prêtez le téléphone, videz le champ.
- Si vous donnez le lien à quelqu'un d'autre, **il met sa propre clé**. Ne partagez jamais la vôtre.

**Ce que ça coûte.** Avec le modèle Haiku, chaque phrase traduite revient à environ un dixième de centime. Un rendez-vous d'une heure bien rempli tourne autour de **20 à 30 centimes**. Une conférence en mode notes, autour de **15 centimes de l'heure**. Le modèle Sonnet est trois à quatre fois plus cher, et se justifie surtout quand le jargon technique est dense.

---

## 4. Les trois modes

### Conversation — le téléphone entre vous deux

Deux gros boutons : *Interlocuteur* et *Moi*. Vous appuyez sur celui de la personne qui va parler. La traduction s'affiche en grand et se dit à voix haute, dans le haut-parleur.

Activez **Mains libres** : après chaque prise de parole, l'appli bascule seule sur l'autre canal. Vous ne touchez plus le téléphone de la réunion.

### Oreillette — un appareil chacun

C'est la réponse au problème des deux écouteurs. Un téléphone ne peut pas envoyer deux langues différentes vers deux oreillettes, mais **deux téléphones le peuvent** — et ils n'ont rien à se connecter.

- Sur **votre** téléphone, mode Oreillette, langues `EN → FR`. Un écouteur dans votre oreille. L'appli n'écoute que l'anglais et ne vous parle qu'en français. Ce que vous dites, vous, est ignoré.
- Sur **son** téléphone, vous lui envoyez le même lien. Elle le règle en `FR → EN`, met son propre écouteur. Son appli n'écoute que le français et ne lui parle qu'en anglais.

Chacun entend sa langue, discrètement, et personne n'a rien à appairer.

**Le point délicat, à savoir avant d'essayer :** si vous utilisez un casque Bluetooth avec micro, le navigateur prendra sans doute le micro du casque — donc votre bouche, pas celle d'en face. Utilisez plutôt un écouteur **sans micro**, ou des écouteurs filaires simples, pour que le téléphone continue d'écouter la pièce avec son propre micro.

### Conférence — des notes en puces

L'appli écoute en continu et écrit les idées clés sous forme de puces dans votre langue, toutes les 45 secondes par défaut. Pas de traduction dans l'oreille : on lit, ce qui fatigue infiniment moins qu'écouter une voix synthétique pendant deux heures.

Le bouton **Résumé complet** rédige à la fin une synthèse structurée : sujet, points clés, chiffres, décisions, questions ouvertes.

---

## 5. Installer les voix de synthèse manquantes

L'appli utilise les voix du système. Le chinois, le japonais et l'hindi ne sont presque jamais installés par défaut sur un appareil français. L'écran **Langues** vous dit lesquelles manquent.

**iPhone / iPad**
Réglages → Accessibilité → **Lire et énoncer** (ce menu s'appelait *Contenu énoncé* avant iOS 26) → **Voix** → choisissez la langue → touchez l'icône de nuage à côté d'une voix pour la télécharger. Prenez la version *Amélioré* ou *Premium* quand elle existe : la différence est nette. Comptez 100 à 400 Mo par voix, en wifi.

**Android**
Réglages → Accessibilité → **Synthèse vocale** (parfois Réglages → Système → Langues et saisie → Synthèse vocale) → roue dentée à côté du moteur → **Installer les données vocales** → choisissez la langue. Quand plusieurs voix sont proposées, prenez celle marquée *neural* ou *naturelle*. Sur Samsung, un second moteur maison est disponible dans le même écran.

**Windows**
Paramètres → Heure et langue → Langue et région → **Ajouter une langue**, en cochant la synthèse vocale dans les options. Les voix neuronales se trouvent aussi dans Paramètres → Accessibilité → Narrateur → *Ajouter des voix naturelles*.

**macOS**
Réglages Système → Accessibilité → Contenu énoncé → Voix système → **Gérer les voix**.

Une fois installée, la voix est disponible hors ligne et l'appli la détecte au rechargement. Vous pouvez choisir précisément laquelle utiliser dans **Réglages → Voix et intonation**.

---

## 6. Le jargon

Deux leviers, dans **Réglages**, et le second compte davantage que le premier.

**Le domaine technique** applique une discipline terminologique générale : médical, juridique, aéronautique et spatial, industrie, informatique, finance, commerce, BTP, recherche. Le traducteur cesse alors de choisir le mot courant quand le mot de métier existe.

**Le glossaire imposé** est votre vrai outil de précision. Une paire par ligne :

```
bleed valve = vanne de prélèvement
stakeholder = partie prenante
notice period = préavis
```

Ces équivalences sont appliquées mot pour mot, dans les deux sens, et priment sur tout le reste. Trois lignes bien choisies avant un rendez-vous valent mieux qu'un domaine générique.

**Le contexte du rendez-vous**, juste au-dessus, est le réglage le plus rentable de toute l'application. Deux phrases suffisent :

> Réunion de maintenance sur un Airbus A320, on parle du circuit hydraulique vert. Mon interlocuteur est le chef d'équipe piste.

Cela lève à lui seul la majorité des ambiguïtés.

---

## 7. Le bruit ambiant

**Réglages → Micro et bruit ambiant → Filtre voix proche.**

L'application ouvre une analyse du son en parallèle, mesure en continu le niveau de fond de la pièce, et **écarte les phrases prononcées trop loin ou trop bas** par rapport à ce fond. Les conversations voisines, dans un marché ou un hall de conférence, passent rarement le seuil. Le curseur de sensibilité règle la marge, et la barre sous le texte en cours vous montre en direct le niveau capté et le seuil : c'est le moyen le plus simple de le calibrer.

Le bouton **Capturer** mémorise en trois secondes la hauteur de voix de la personne en face. L'appli rejette ensuite ce qui s'en écarte trop. Utile quand une voix grave et une voix aiguë se croisent à portée de micro, inutile entre deux voix proches.

Deux avertissements honnêtes :

- Ce n'est **pas** du filtrage directionnel. Un navigateur ne donne pas accès aux micros individuels d'un téléphone ; on ne peut donc pas viser une direction depuis une page web. Ce que fait réellement l'appli, c'est écarter le lointain et le faible — ce qui, en pratique, règle la plus grande partie du problème. Le vrai traitement directionnel, lui, est déjà appliqué par le système d'exploitation en amont, et l'appli demande explicitement qu'il soit actif.
- Le filtre a besoin d'un **second accès au micro**, en plus de celui de la reconnaissance vocale. Sur iPhone, les deux cohabitent mal selon les versions. Si les phrases cessent de remonter, désactivez le filtre : c'est le premier réflexe.

---

## 8. L'intonation

**Réglages → Voix et intonation → Refléter l'intonation.**

Pendant que la personne parle, l'appli mesure trois choses sur sa voix : le **débit** (caractères par seconde rapportés au rythme normal de sa langue), l'**amplitude mélodique** (l'écart entre ses notes hautes et basses, ce qui distingue une voix monocorde d'une voix expressive), et l'**énergie** par rapport au fond sonore. Elle reporte ces trois mesures sur la voix de synthèse : débit, hauteur, volume. Le traducteur, de son côté, reçoit la consigne de préserver le registre et la ponctuation finale — un point d'interrogation ou d'exclamation est ce qui porte l'intonation quand un moteur vocal lit un texte.

Résultat concret : une question sonne comme une question, une phrase lancée vite reste vive, une remarque appuyée garde son poids.

Le curseur d'intensité dose l'effet. À 100 %, c'est expressif mais parfois caricatural ; **50 % est le bon réglage** dans la plupart des cas.

Ce que ça ne fait pas, et ne peut pas faire depuis un navigateur : **reproduire le timbre de la personne**. Sa voix reste celle du système, pas la sienne. Cloner une voix demande un service de synthèse dédié, payant, avec une latence qui rend l'exercice difficile en temps réel. Si vous voulez aller par là un jour, le point d'accroche dans le code est la fonction `drainSpeech()` : c'est le seul endroit où le texte devient du son.

---

## 9. Dépannage

| Symptôme | Cause la plus fréquente |
|---|---|
| Les boutons de canal sont grisés | Navigateur sans reconnaissance vocale. Passez à Chrome, ou Safari sur iPhone. |
| « Micro refusé » | Autorisez le micro pour ce site dans les réglages du navigateur, puis rechargez. |
| Le texte s'affiche mais rien ne se dit | Voix manquante pour cette langue (§5), ou volume média coupé. Sur iPhone, vérifiez aussi le petit interrupteur silencieux. |
| Plus rien ne remonte après quelques minutes | Le filtre voix proche entre en conflit avec le micro. Désactivez-le. |
| « Clé API refusée » | Clé mal collée, ou crédit épuisé sur le compte Anthropic. |
| « Limite atteinte » | Trop d'appels rapprochés. Espacez les prises de parole, ou augmentez l'intervalle des puces en mode conférence. |
| L'appli se traduit elle-même | Le micro entend le haut-parleur. Baissez le volume, ou passez en mode Oreillette. |
| Rien ne marche hors ligne | C'est normal. La reconnaissance vocale et la traduction exigent le réseau ; seul l'affichage de l'appli est mis en cache. |

---

## 10. Vie privée

- Les paroles sont transcrites par le **service de reconnaissance vocale du navigateur** (Google pour Chrome, Apple pour Safari) : l'audio transite par leurs serveurs. C'est une contrainte du navigateur, pas un choix de cette application.
- Le texte transcrit part ensuite à **l'API Anthropic** pour être traduit, avec votre clé.
- **Rien n'est envoyé ailleurs.** Aucune analyse d'audience, aucun traceur, aucun serveur intermédiaire. La page n'appelle que `api.anthropic.com` et Google Fonts.
- Les transcriptions ne quittent jamais l'appareil, et disparaissent quand vous fermez l'onglet, sauf si vous les enregistrez vous-même. Vos réglages, glossaires et clé restent dans le stockage local du navigateur.

Dans un cadre professionnel sensible — santé, défense, secret des affaires — vérifiez que ce trajet est compatible avec vos obligations avant d'utiliser l'outil en réunion réelle.

---

## 11. Fichiers du dépôt

```
index.html              toute l'application : structure, styles, logique
manifest.webmanifest    permet l'installation sur l'écran d'accueil
sw.js                   met l'interface en cache pour un démarrage instantané
robots.txt              interdit l'indexation
icon-*.png              icônes de l'application
.nojekyll               facultatif, désactive le traitement Jekyll de GitHub
```

Tout tient dans `index.html`. Vous pouvez le modifier directement : il n'y a ni dépendance, ni étape de compilation.
