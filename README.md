# Reconnaissance-d-objets-avec-le-descripteur-SIFT


Détecteur de points
d'intérêt SIFT et descripteur SIFT
Pour ce tp, vous allez utiliser les points d'intérêt calculés par la méthode SIFT (voir cours sur les
points d'intérêt). Bien que cette méthode soit a priori difficile à comprendre d'un point de vue
théorique, son utilis ation est très simple grâce à la démo disponible sur la page de David Lowe
http://www.cs.ubc.ca/~lowe/keypoints/
Pour commencer, allez sur cette page, télécharger la démo et essayez
là avec les exemples donnés.
Avec le code (en C), vous comprendrez comment calculer les points d'intérêt et comment faire la
correspondance ( entre deux points. Tout y est. Cependant, vous n'avez pas accès à tout le
code (pour raison de brevet). Mais les exem ples donnés vous permettent de calculer les points
d'intérêts dans un fichier, puis vous devrez lire ce fichier texte dans votre programme. Ne cherchez
pas à tout inclure dans un seul programme, mais procédez en deux étapes comme dans la démo. Vous
pouvez appeler le calcul de SIFT par des appel system dans votre code, ou en précalculant toutes
les valeurs dans des fichiers texte par exemple.
Actuellement, SIFT est aussi implémenté dans OpenCV, donc vous pouvez l'utiliser à la place du
fichier exécutable du David Lowe. Donc, c'est à votre choix.
N'hésitez pas à télécharger et à lire les articles de recherche disponibles sur la page de David Lowe.
Outre les explications théoriques, on y trouve des explications pratiques et simples à comprendre sur
l'utilisat ion de SIFT pour plusieurs applications.
Reconnaissance d'objets avec SIFT
Remarque
: La méthode décrite ci dessous est sim ple. Elle n'est ni complète ni parfaite. Il vous
restera plusieurs points à résoudre pour bien réussir ce tp. Je vous encourage fortement à étudier les
différentes solutions et idées existantes sur Internet. Il existe une documentation abondante disponible
pour ce tp, donc profitez en. Dans votre rapport, expliquez bien les idées que vous avez implémentées,
en citant les références extérieures au besoin.
Le but de ce tp consiste à faire la reconnaissance d'objets à l'aide du descripteur SIFT. Premièrement,
il faut extraire les points SIFT d'images de référence (d'apprentissage) représentant plusieurs classes
d'objets. Ensuite, à partir d'une i mage représentant un objet inconnu, on extrait les points SIFT et on
compare avec les classes connues pour identifier l'objet.
Bases d'images
Deux bases d'images sont proposées pour ce tp (voir ci
Deux bases d'images sont proposées pour ce tp (voir ci--dessous). Vous en choisissez une, celle de dessous). Vous en choisissez une, celle de votre choix. Quvotre choix. Quelque soit la base d'images utilisée, séparezelque soit la base d'images utilisée, séparez--la (environ) 50% base de référence la (environ) 50% base de référence (apprentissage) et 50% base de test.(apprentissage) et 50% base de test.
Chaque base d'images possède plusieurs milliers d'images. Votre programme devra être capable de
Chaque base d'images possède plusieurs milliers d'images. Votre programme devra être capable de traiter automatiquement toutes les images.traiter automatiquement toutes les images. Voici trois conseils pour vous aider :Voici trois conseils pour vous aider :
• Précalculer les vecteurs SIFT à l'avance et travailler ensuite sur les fichiers texte contenant Précalculer les vecteurs SIFT à l'avance et travailler ensuite sur les fichiers texte contenant ces descripteursces descripteurs
• Votre programme ne traite qu'une seule image à la fois. Faites un script Linux pour traiter Votre programme ne traite qu'une seule image à la fois. Faites un script Linux pour traiter toutes les toutes les images de la base. Vous éviterez ainsi bien des problèmes.images de la base. Vous éviterez ainsi bien des problèmes.
• Chaque image comporte déjà sa classe d'appartenance, soit par son nom de fichier, soit par Chaque image comporte déjà sa classe d'appartenance, soit par son nom de fichier, soit par son nom de répertoire. Utilisez ces noms lors de la construction de votre base de référence et son nom de répertoire. Utilisez ces noms lors de la construction de votre base de référence et lors de la lors de la phase de validation.phase de validation.
Calcul des descripteurs SIFT
Calcul des descripteurs SIFT
Vous allez extraire les descripteurs SIFT de toutes les images de la base d'images. Chaque descripteur
Vous allez extraire les descripteurs SIFT de toutes les images de la base d'images. Chaque descripteur SIFT consiste en un vecteur de 128 valeurs. Pour une seule image, il est possible d'extraire des SIFT consiste en un vecteur de 128 valeurs. Pour une seule image, il est possible d'extraire des dizaidizaines ou même des centaines de points SIFT. Pour stocker ce vecteur, vous pouvez les séparer par nes ou même des centaines de points SIFT. Pour stocker ce vecteur, vous pouvez les séparer par image (un fichier texte par image avec tous les points SIFT de cette image) ou dans un seul fichier image (un fichier texte par image avec tous les points SIFT de cette image) ou dans un seul fichier texte pour toutes les images (préfixer chaque ligne par le notexte pour toutes les images (préfixer chaque ligne par le nom de l'image).m de l'image).
Mise en correspondance (matching) de points d’intérêts
Mise en correspondance (matching) de points d’intérêts
Etudiez la méthode de mise en correspondance présenté dans la démo SIFT. Il s'agit d'une méthode
Etudiez la méthode de mise en correspondance présenté dans la démo SIFT. Il s'agit d'une méthode possible, mais pas la seule. La mise en correspondance de deux images se fait en calculapossible, mais pas la seule. La mise en correspondance de deux images se fait en calculant les nt les correspondances entre tous les descripteurs SIFT de ces deux images.correspondances entre tous les descripteurs SIFT de ces deux images.
La distance entre deux vecteurs SIFT peut se faire simplement en prenant la distance Euclidienne
La distance entre deux vecteurs SIFT peut se faire simplement en prenant la distance Euclidienne entre les deux vecteurs. On considère la distance la plus courte (petite) entre deentre les deux vecteurs. On considère la distance la plus courte (petite) entre deux vecteurs comme la ux vecteurs comme la meilleure.meilleure.
Afin de réduire le nombre de fausses correspondances, une métrique possible est de calculer le ratio
Afin de réduire le nombre de fausses correspondances, une métrique possible est de calculer le ratio entre la distance la plus courte et la deuxième plus courte distance. Si ce ratio est inférieur à un seuil entre la distance la plus courte et la deuxième plus courte distance. Si ce ratio est inférieur à un seuil (à (à déterminer), alors la correspondance peut être considérée comme robuste, sinon elle est rejetée :déterminer), alors la correspondance peut être considérée comme robuste, sinon elle est rejetée :
𝑟𝑎𝑡𝑖𝑜=𝑑𝑝𝑙𝑢𝑠𝑝𝑟𝑜𝑐ℎ𝑒𝑑𝑑𝑒𝑢𝑥𝑖è𝑚𝑒𝑝𝑙𝑢𝑠𝑝𝑟𝑜𝑐ℎ𝑒<𝑠𝑒𝑢𝑖𝑙
Remarque
Remarque : Comme indiqué auparavant, il s'agit d'un exemple de mesure possible (pas forcément la : Comme indiqué auparavant, il s'agit d'un exemple de mesure possible (pas forcément la meilleure) pour déterminer les bonnes et les mauvaises comeilleure) pour déterminer les bonnes et les mauvaises correspondances. Il existe d'autres façons de rrespondances. Il existe d'autres façons de déterminer cela et vous êtes libre d'utiliser une autre méthode, tant que vous l'expliquez dans votre déterminer cela et vous êtes libre d'utiliser une autre méthode, tant que vous l'expliquez dans votre rapport.rapport.
Calcul de correspondance entre images
Calcul de correspondance entre images
Une fois la correspondance entre tous les points SIFT calculés
Une fois la correspondance entre tous les points SIFT calculés, on peut compter le score de , on peut compter le score de correspondances réussies. Plus ce nombre de correspondances réussies, plus les deux images ont des correspondances réussies. Plus ce nombre de correspondances réussies, plus les deux images ont des chances de représenter la même classe d'objets. Le score peut être calculé comme suit :chances de représenter la même classe d'objets. Le score peut être calculé comme suit :
𝑠𝑐𝑜𝑟𝑒=# correspondances réussies# descripteurs de l'image modèle
«
« L'image modèleL'image modèle » étant l'image de» étant l'image de la base d'apprentissage. On comptera donc ce score de la base d'apprentissage. On comptera donc ce score de correspondances pour l'image inconnue et pour toutes les «correspondances pour l'image inconnue et pour toutes les « images modèlesimages modèles » de la base » de la base d'apprentissage. Les N images ayant le score le plus élevé détermineront la classe de l'objet inconu d'apprentissage. Les N images ayant le score le plus élevé détermineront la classe de l'objet inconu (N=1,3,5,...)(N=1,3,5,...)..
Remarque
Remarque : Même remarque que ci: Même remarque que ci--dessus pour la mesure du score.dessus pour la mesure du score.
Rapport à remettre
Rapport à remettre
Dans votre rapport, montrez quelques résultats de mise en correspondances, bon et mauvais.
Dans votre rapport, montrez quelques résultats de mise en correspondances, bon et mauvais. Expliquez la composition de vos bases d'apprentissage et de test.Expliquez la composition de vos bases d'apprentissage et de test.
Calculez et
Calculez et montrezmontrez lala (les) (les) matrice(s) de confusion matrice(s) de confusion (si vous connaissez pas la matrice de confusions, (si vous connaissez pas la matrice de confusions, n'hésitez pas à consulter sur n'hésitez pas à consulter sur wikipédiawikipédia) sur votre base d'images. Il vaut mieux de faire une ) sur votre base d'images. Il vaut mieux de faire une repréreprésentation par couleur plutôt que par valeur. Expliquez les classes qui fonctionnent bien et celles sentation par couleur plutôt que par valeur. Expliquez les classes qui fonctionnent bien et celles qui se confondent facilement. Donnez (et surtout expliquez) des exemples qui fonctionnent bien et qui se confondent facilement. Donnez (et surtout expliquez) des exemples qui fonctionnent bien et d'autres qui fonctionnent moins bien. Analysez et expliquezd'autres qui fonctionnent moins bien. Analysez et expliquez pourquoi vous obtenez ces résultats.pourquoi vous obtenez ces résultats.
Expliquez bien les idées que vous avez implémentées et qui ne sont pas expliquées dans cet énoncé.
Expliquez bien les idées que vous avez implémentées et qui ne sont pas expliquées dans cet énoncé. Si vous avez d'autres idées pour améliorer les résultats, discutezSi vous avez d'autres idées pour améliorer les résultats, discutez--les. Donnez les références si les. Donnez les références si nécessaire.nécessaire.
Bases d
Bases d'images pour ce TP'images pour ce TP
Choisissez UNE base d'images parmi les suivantes :
Choisissez UNE base d'images parmi les suivantes :
• Columbia University Image Library (COILColumbia University Image Library (COIL--100)100)
• Caltech 101Caltech 101
Note
Note (1) : Pour ceux qui veulent tester et comparer leur programme sur deux bases d'images (1) : Pour ceux qui veulent tester et comparer leur programme sur deux bases d'images différentes, un bonus sera accordé.différentes, un bonus sera accordé.
Note
Note (2) : Pour convertir les images TIFF, JP(2) : Pour convertir les images TIFF, JPEG ou PNG en PGM, je vous suggère l'utilitaire EG ou PNG en PGM, je vous suggère l'utilitaire convertconvert de la suite de la suite ImageMagickImageMagick. Vous pouvez aussi utiliser cet utilitaire pour convertir vos images couleurs . Vous pouvez aussi utiliser cet utilitaire pour convertir vos images couleurs een niveaux de gris ou modifier la résolution des images.n niveaux de gris ou modifier la résolution des images.
Bon travail
Bon travail !!
