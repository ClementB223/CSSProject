# INSERT COIN — Site vitrine d’un salon du jeu vidéo

Ouvrir **index.html** directement dans Chrome, Edge ou Firefox récent. Aucun serveur, build, package ni connexion ne sont nécessaires.

## Groupe et périmètre
- J’ai choisi le thème du salon du jeu vidéo et le nom INSERT COIN. L’événement, les invités, les tarifs et le lieu sont fictifs.
- Membres et répartition des contributions : à compléter.
- Convention : BEM (.guest__role, .programme__day--one), utilitaires u-.
- Le site est placé à la racine de ce dépôt, sans les documents pédagogiques du dépôt de départ.
- Les exercices complémentaires du dépôt sont des activités de cours distinctes du projet noté et ne font pas partie de cette livraison.

## Localisation des exigences
| Exigence | Élément | Localisation | Explication |
|---|---|---|---|
| Architecture | Ordre des cinq layers | `css/main.css:1` | Une seule déclaration d’ordre, puis imports. |
| Architecture | Primitifs | `css/tokens.css:5` | Palette et échelles brutes. |
| Architecture | Sémantiques | `css/tokens.css:25` | Rôles utilisés par les composants ; light-dark pour les thèmes. |
| Architecture | Nesting / BEM | `css/components.css:19` | Exemple .btn ; .bloc__element et .bloc--variante ; au plus trois blocs imbriqués. |
| Mise en page | Zones Grid mobile / desktop | `css/layout.css:7` | intro, art, info ; programme avec heading, day-one, day-two. |
| Mise en page | Subgrid visible | `css/layout.css:17` | Chaque carte couvre cinq lignes, partagées avec ses voisines. |
| Mise en page | Flexbox | `css/components.css:8` | Navigation avec gap et retour à la ligne. |
| Responsive | Media query mobile-first | `css/layout.css:22` | Deux colonnes à partir de 48rem. |
| Responsive | Typographie fluide | `css/tokens.css:51` | clamp pour le titre ; corps et titres de section fluides aussi. |
| Responsive | Conteneurs | `css/layout.css:20` | Bandeau large après le programme et colonne étroite de la FAQ. |
| Responsive | Container query | `css/components.css:39` | event-card passe de vertical à horizontal à 35rem de conteneur. |
| Responsive | Protection des petites largeurs | `css/layout.css:15` | min(100%, 20rem), min-inline-size: 0, textes avec overflow-wrap. Test visuel 320 px encore à effectuer. |
| Sélecteurs | :has() utile | `css/components.css:50` | La présence du badge met automatiquement le pass en avant. |
| Sélecteurs | :where() / :is() | `css/base.css:4` | Faible spécificité pour les titres ; focus factorisé. |
| Thème | Clair / sombre / auto | `css/tokens.css:4` | light-dark ; Auto suit le système. |
| Thème bonus | Bascule CSS-only | `css/tokens.css:58` | Boutons radio natifs, aucun JavaScript. |
| Animations | Transition bouton | `css/components.css:73` | Couleurs et translate, durées dans les tokens. |
| Animations | Transition carte | `css/components.css:75` | Mouvement lorsque le lien est survolé ou reçoit le focus. |
| Animations | Keyframes | `css/components.css:78` | Apparition unique de l’introduction, 420 ms. |
| Animations | Mouvement réduit | `css/utilities.css:6` | Neutralisation dans utilities ; mouvement activé seulement sous no-preference. |
| Bonus | Popover animé | `css/components.css:81` | État initial ; display et overlay allow-discrete. Sans transition de sortie, fermeture immédiate. |
| Accessibilité | HTML sémantique | `index.html:42` | Un seul h1, sections titrées, FAQ details, lien d’évitement. |
| Accessibilité | Focus visible | `css/base.css:11` | Anneau de 3px ; adaptation sur fond jaune. |
| Accessibilité | Alternatives images | `index.html:59` | SVG locaux ; portraits descriptifs et visuel d’arcade. |
| Qualité | Pas de JavaScript | `index.html:1` | Zéro ligne JavaScript, aucun build ni framework. |

## Tests réellement effectués
- Vérification des ancres, identifiants uniques, cibles des trois popovers et existence des fichiers locaux.
- Un h1, six créneaux sur deux jours, six cartes, trois offres et six questions FAQ.
- Équilibre des blocs CSS ; absence de transition: all, de déclaration !important, de scripts et de dépendances externes.
- Calcul des contrastes selon la luminance relative sRGB (formule WCAG), sans service externe.
- git diff --check : exécuté lors de la finalisation.
- Les tests visuels, clavier et responsive restent à effectuer ; ils ne sont pas inclus dans les vérifications ci-dessus.

### Contrastes calculés
| Paire | Couleurs | Rapport |
|---|---|---|
| Clair : texte / fond | #17191d / #f4f2e9 | 15.69:1 |
| Clair : texte secondaire / surface | #53565c / #ffffff | 7.36:1 |
| Clair : texte secondaire / fond | #53565c / #f4f2e9 | 6.56:1 |
| Clair : lien / fond | #2446dc / #f4f2e9 | 6.27:1 |
| Sombre : texte / surface | #f4f2e9 / #25282e | 13.17:1 |
| Sombre : secondaire / surface | #bfc3cb / #25282e | 8.36:1 |
| Sombre : lien / surface | #a8b9ff / #25282e | 7.77:1 |
| Bouton et bandeau : encre / jaune | #17191d / #e2fa58 | 15.13:1 |
| Bande bleue : blanc / bleu | #ffffff / #2446dc | 7.04:1 |

Ces paires passent 4,5:1. Les illustrations décoratives ne portent pas de texte essentiel à la navigation. Les contours de focus des liens du bandeau jaune et du pass mis en avant sont adaptés au fond.

### Vérifications manuelles avant dépôt
1. À 320, 768, 1280 et 1440 px : vérifier tout le document, sans barre horizontale ; contrôler aussi le zoom 200 %.
2. Parcourir au clavier : lien d’évitement, navigation, radios (flèches), liens des invités, pass, fermeture par Échap, FAQ et contact.
3. Passer en clair et sombre ; Auto suit le réglage du système. La préférence n’est pas mémorisée au rechargement (choix sans JS).
4. Comparer le bandeau village indépendant large et celui de la FAQ : ils utilisent le même composant, mais changent selon leur conteneur.
5. Inspecter la grille des invités : cinq pistes partagées par rangée. Les longueurs de biographies différentes ne décalent pas les liens.
6. Émuler prefers-reduced-motion: reduce : introduction et cartes immobiles, popovers instantanés, aucun contenu masqué.
7. Tester Chrome/Edge et Firefox ; une fermeture sans fondu reste un repli acceptable.

## Validation W3C
Validation W3C **non exécutée**. Il reste à vérifier le CSS sur https://jigsaw.w3.org/css-validator/ et le HTML sur https://validator.w3.org/nu/.
Les syntaxes modernes éventuellement signalées sont : nesting natif, @layer, light-dark(), :has(), subgrid, container queries, @starting-style, transition de display/overlay avec allow-discrete. Reporter ici les messages réellement obtenus, avec leurs lignes.

## Bonus techniques et replis
- Thème Auto / Clair / Sombre CSS-only : radios et :root:has ; light-dark recalcule les couleurs sans script.
- Popover déclaratif : les boutons présentent le pass choisi ; @starting-style fournit le point de départ et allow-discrete maintient l’affichage pendant la sortie. La fonction reste utilisable si l’animation n’est pas prise en charge.

## JavaScript
Aucun. FAQ native, navigation par ancres, radios pour le thème et Popover API pour la billetterie. Le site ne collecte aucune donnée et ne vend aucun billet réel. L’adresse .example et les réseaux fictifs sont des éléments de démonstration.

## Visuels
J’ai utilisé OpenAI Codex pour générer les illustrations SVG du site : la borne d’arcade et les six portraits fictifs.

## Crédits
Illustrations SVG originales produites pour ce projet avec assistance de Codex : img/arcade.svg et les six portraits. Aucun portrait réel, aucune image tierce. Polices système Impact / Arial / Courier New (fichiers non distribués). Aucun téléchargement externe, framework ou gabarit Internet.

Voir **WIREFRAME.md** et **VERIFICATION.json** pour la structure et les contrôles du projet.
