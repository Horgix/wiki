Ce week-end, j'ai eu la chance d'aller au RustFest. Comment ? Grâce à Xebia !
Pour citer mon manager : "on ne t'y envoie pas parce que c'est stratégique, ça
ne l'est clairement pas, mais on est contents de ce que tu fais donc vas y".




Il y a 2 semaines, j'ai eu la chance d'aller au RustFest (http://zurich.rustfest.eu/), une conférence sur le langage Rust s'étant tenue à Zurich. Ci après se trouve un résumé de ce que j'ai pu y voir !

Ce RustFest 2017 se déroulait comme suit : conférences le samedi, et workshops le dimanche.
La journée du Samedi ayant été relativement dense, avec pas moins de 14 talks successifs sur une seule track, je vais tenter ici de vous résumer les points principaux ayant retenu mon attention, et me permettrai de passer sous silence les points non pertinents afin d'éviter de vous faire perdre votre temps.

Pour info, j'ai glissé quelques liens vers des Tweets que j'ai fait en live dans lesquels vous trouverez certaines photos de slide à défaut d'avoir les liens pour chaques sous la main.

# Keynote: A RustFest Carol

Speaker : Felix Klock

https://twitter.com/Horgix/status/914057591453569024

Felix Klock débute la journée en nous présentant un historique de Rust via une narration sous forme d'histoire. L'objectif ? Nous présenter les principaux points d'évolutions, depuis les prémices de Rust jusqu'à aujourd'hui, avec comme message principal "ne pas avoir peur du changement".

Pour ceux qui voudraient le rencontrer, Felix est quelqu'un de sympa avec beaucoup de recul sur Rust et il organise le meetup Rust Paris, et je l'y avais d'ailleurs rencontré il y a un mois ! Le prochain est dans 2 semaines :)

# Rust: an alternative to high-level programming languages?

Speaker : Élisabeth Henry ; `@lise_henry` / `@crowdagger`

Ce second talk apporte un point de vue très intéressant : celui d'un utilisateur "high level" de Rust. L'utilisateur en question ? Une utilisatrice : Elisabeth Henry... autrice ! Pour quoi se sert elle de Rust ? Pour transformer ses livres qu'elle écrit en markdown vers du HTML et du PDF ! (oui, ça fait vraiment penser à Pandoc, là n'est pas la question :) )

Le profil n'est donc pas celui de quelqu'un qui attache une grande importance au langage en lui même, mais vraiment à son utilisation.

Pour commencer, elle nous présente sa vision de "high level" :

- Applications en ligne de commande, Applications graphiques, petits jeux...
- Les performances ne sont pas vraiment une problématique
- La safety en terme de stabilité non plus
- Pas de réel besoin d'intéractions low level
- On est plus sur Java/Python/Ruby en terme de comparaison

Elle dresse le portrait suivant des langages de programmation impératifs :

- La plupart rendent vraiment facile le fait de faire des choses
- ... en autorisant de les faire n'importe comment ("the wrong way")
- La plupart des langages faciles à apprendre cachent en réalité beaucoup de complexité; elle prenait par exemple Python pour illustrer son propos, où sans connaître le langage on ne sait pas vraiment si on manipule une copie des données ou un pointeur vers celles-ci et où ça nous retombe fatalement dessus un jour où l'autre
- De manière générale, ils ne rendent pas les choses plus simples sur le long terme

Malgré son utilisation high level, elle a très bien pris en considération la notion de référence de Rust, qui peuvent être soit partagées, soit mutables, mais pas les deux ! Au final, Rust apporte vraiment de la memory safety et évite les data races, et même un utilisateur high level fini par s'en rendre compte.

En résumé :

- Court terme VS long terme
- Difficile au début, mais rend les choses bien plus faciles par la suite
- Facilite la partie gestion des bugs, maintenance, et l'acceptation des contributions
- Au final, les alternatives sur ces avantages seraient les langages fonctionnels qui n'autorisent pas du tout de mutations, mais qui sont moins répandus et potentiellement plus complexes encore à prendre en main

# Macromancy - an introduction to Rust macros

Speaker : Geoffroy Couprie ; `@gcouprie` / Security & QA at CleverCloud

https://twitter.com/Horgix/status/914057484230434816


Talk très intéressant sur les macros en Rust... mais de mon point de vue, tellement impossible à maintenir et tellement loin de l'esprit craftsmanship que je ne m'attarderai pas vraiment dessus.
Points principaux : macros récursives, imbriquées, et trace macros pour afficher l'expanding des macros (unstable)

En résumé : les macros de Rust permettent de faire énormément de choses...  presque trop.

# Impractical Macros

Speaker : Alex Burka

Pour appuyer le talk précédent, Alex Burka nous a présenté.... un interpréteur [Brainfuck](https://fr.wikipedia.org/wiki/Brainfuck) en pures macros Rust, donc capable de comprendre et d'éxecuter du code Brainfuck **à la compilation**.

Bien que très intriguant et démonstratif, ce talk n'a pas vraiment de raison d'être détaillé, sachez juste que c'est possible... For science!

# Antimony: a real time distributed stream processing system

Speakers :
    - Mohammed Makhlouf - Software Engineer @ GCert
    - Mohammad Samir
Speakers : `@msmakhlouf` / `@_msamir_`

https://antimony.rs/


Mon point de vue sur ce talk est relativement mitigé.

Ils nous ont présenté un système d'analyse realtime de requêtes DNS en Rust afin de détecter des malwares, par exemple via des noms de domaines connus ou proche, ou via des critères tels que la longueur.

Le talk pourrait se résumer en "On a pris Apache Storm, on a overloadé nos cluster Zookeeper, et on a fini par drastriquement overprovisionner TOUT et par lancer chaque topologies sur un cluster storm séparé avec des clusters ZK séparés". Mention honorable pour [pyleus](https://github.com/YelpArchive/pyleus), le framework Python de Yelp pour développer et gérer des topologies Storm.

Au final, la partie la plus intéressante reste sans doute la mention du [paper "Héron" de Twitter](https://dl.acm.org/citation.cfm?id=2742788) sur le stream processing, ainsi que la rapide mention des bibliothèques [Tokio](https://tokio.rs/) et [Mio](https://github.com/carllerche/mio) pour les IO asynchrones en Rust (j'y reviens plus tard).

# Testing strategies and pattern for efficient TDD in Rust

Speaker : Thomas Wickham

http://slides.com/thomaswickham/efficient-tdd-in-rust/#/

https://twitter.com/Horgix/status/914096045952520195

Je suis un peu biaisé sur ce talk; en effet, le speaker est un ami ! Mais vu qu'il s'agit d'un talk plus sur l'aspect "TDD" que l'aspect "Rust", je pense que vous trouverez tout ce qui a été dit en plus complet à Xebia ;)

Elément principal côté "TDD en Rust" à retenir : au final le compilateur vérifie déjà tellement de choses et garanti une telle safety par les contraintes qu'il impose que les tests en sont relativement réduits et qu'on peut se concentrer sur les points vraiment utiles plutôt que d'avoir des tonnes de "edge cases".

# A Rust-based Runtime for the Internet of Things

Speaker : Niklas Adolfsson

https://twitter.com/Horgix/status/914098873018327040

https://www.tockos.org/

Ce talk nous présentait un OS écrit en Rust pour tout ce qui est IoT.

Pourquoi Rust ?

- Memory Safety et type safety
- Contrôle fin sur la mémoire
- Très peu d'overhead au runtime

Au final, Rust permet d'avoir exactement ce qu'on cherche sur de l'IoT : de la fiabilité, du contrôle low level et une très faible consommation de ressources.

Design de l'OS et des éléments écrits en Rust : https://www.tockos.org/documentation/design

# A hammer you can only hold by the handle / Andrea Lattuada


https://twitter.com/Horgix/status/914122981777035265

Ce talk était de mon point de vue tout simplement génial, et présentait sous un excellent angle les notions d'[ownership](https://doc.rust-lang.org/book/second-edition/ch04-01-what-is-ownership.html) et de [borrow](https://doc.rust-lang.org/book/second-edition/ch04-02-references-and-borrowing.html) de variables en Rust, qui sont souvent les notions les plus ardues à "prendre en main" lorsque l'on débute en Rust.

Ce n'est par conséquent pas vraiment un talk facile à résumer, sans vous renvoyer vers la documentation de Rust... Mais pour préciser un peu, il a fait une analogie très intéressante de l'allocation d'objets et de la gestion de leur lifetime ainsi que l'accès concurrentiel par rapport à une lettre que l'on souhaiterait envoyer :

- Enveloppe = type Option contenant potentiellement une lettre
- Lettre = struct
- Shipping = méthode utilisant l'enveloppe.

Avec cet exemple, il a démontré comment les primitives du langage nous permettent d'avoir une garantie d'*"exactly once"* sur certains appels, une garantie d'ordre ainsi qu'une garantie de drop/free.

Les slides se trouvent ici, même si elles ne sont pas des plus faciles à comprendre sans les explications qui vont avec : https://speakerdeck.com/utaal/a-hammer-you-can-only-hold-by-the-handle

# Fearless concurrency in your microcontroller

Speaker : Jorge Aparicio

https://twitter.com/Horgix/status/914122928802942976
https://twitter.com/Horgix/status/914123286983905280

Ce talk présentait une gestion low-level de la concurrence en Rust, avec comme guideline la problématique suivante :

- Tâche 1 : doit se lancer toutes les 10ms et prend 2ms à s'éxecuter
- Tâche 2 : doit se lancer toutes les 1ms et prend 100µs à s'éxecuter
- Est-il possible de respecter ces contraintes en utilisant du multitasking coopératif ?

Au final, la problématique n'est pas spécifique à Rust, mais le langage permet de la résoudre en restant complètement memory safe, avec une absence de deadlocks, et des data races détectées à la compilation. Tout ça sur des microcrontrollers d'un seul core, sans avoir à se reposer sur un garbage collector, soit exactement le type de points positifs que l'on souhaiterait lorsque l'on travail avec des microcontrolleurs.

Le blog post réalisé bien avant ce talk par son auteur vous donnera bien plus de détails que ce que je serai capable de faire rentrer dans ce résumé : http://blog.japaric.io/fearless-concurrency/

# Mistakes to avoid when writing a wrapper around a C library

Speaker : Pierre Krieger

https://twitter.com/Horgix/status/914130959695478786

Rust étant régulièrement comparé à "du C mais en plus safe", il est logique de se retrouver avec des besoins communs. Mais plutôt que de réimplémenter intégralement les bibliothèques low level en C, un choix souvent fait est celui de wrapper ces bibliothèques C avec du Rust afin d'exposer une API plus safe sans pour autant réimplémenter toute la logique.

Ce talk présentait 9 "erreurs" à éviter lors du wrapping d'une bibliothèque C en Rust, et en voici le résumé :

Erreur n°1: Utiliser la lifetime (scoping) pour des objets "long-lived"

- => N'utiliser les lifetimes que pour des objets temporaires (comme des locks ou des accesseurs)
- => Utiliser Arc/Rc (shared pointers dans la lib standard de Rust) pour les dépendences entre des objets long-lived

Erreur n°2 : Supposer que les implémentations d'un Trait ne sont pas buguées

- => Déréférencer dès le début et faire les vérifications nécessaires OU utiliser un Trait unsafe custom

Erreur n°3 : Lire des primitives en mémoire sans vérification

Erreur n°4 : Oublier les variables globales cachées en C...

- Qu'est ce qu'il en est des Mutex ? Si on charge différentes versions de la même bibliothèque... chaque version aura son propre lock sur des Mutex différentes, et on a perdu !
- => Impossible à wrapper de manière safe, by design :(

Erreur n°5 : Ignorer les problèmes de leak potentiels en C

- => Ne PAS supposer que les destructeurs seront appelés, et abuser des asserts
- => La manière de décrire la solution m'a fait sourire, alors en voici la citation exacte : "We'll do something called 'Pre-pooping your pants'.  But don't Google that, or at least do it for Rust."

Erreur n°6 : Essayer d'écrire une abstraction haut niveau à la bibliothèque directement

- Les utilisateurs vont rapidement se plaindre des features de la bibliothèque en C qui ne sont pas exposées par l'abstraction en Rust
- => Rester aussi proche de la bibliothèque C que possible tout en restant safe
- => Ajouter des abstractions additionnelles plus tard, après coup
- => Optimiser les features les plus haut niveau si nécessaire

Erreur n°7 : Supposer que les structs et les enums ont une certaine disposition en mémoire

- => Utiliser l'annotation `#[repr(c)]` pour forcer le layout en mémoire

Erreur n°8 : Ne pas tester son wrapper à une échelle suffisamment large

Erreur n°9 : Ne pas catch les potentiels Rust panics au sein de callbacks appelés par la bibliothèque en C

- => `catch_unwind` des panics partout où nécessaire

Conclusion sur ce talk : lire https://doc.rust-lang.org/nomicon/ :)

# Rust In Rhymes

Speaker : Andre 'llogiq' Bogus

https://twitter.com/Horgix/status/914139627350630400

Que dire... Ce talk était un véritable show, entièrement en rhymes, mais ça s'arrête là.
Du coup, il n'y a pas grand chose à en résumer à l'écrit, et honnêtement l'humour ne m'a pas particulièrement atteint.

# Create Rust games easily

Speaker : Lisa

Speaker : Lisa @ Travis CI

Honnêtement, ce talk bien qu'intéressant m'a un peu déçu. Du live coding à base de copier/coller, trop rapide pour être réellement suivi, et avec un résultat final relativement minimal.

Nothing to do here.

# SHAR: Rust's gamedev experience

Speaker : Fedor Logachev

Retour plus intéressant que le précédent... mais la partie jeux vidéos est un peu trop spécialisée pour que je sois à même de la critiquer; si vous voulez en savoir plus n'hésitez pas à venir m'en parler ceci dit !

# Type-safe & high-perf distributed actor systems with Rust

Speaker : Anselm Eickhoff

https://github.com/citybound/citybound

LA surprise de cette fin de journée. Concrêtement, tout est dans le titre, et le talk était une énorme démo du résultat avec explications sur l'implémentation. Globalement : création d'un simulateur de ville à base d'Acteurs distribués, en Rust, avec des performances vraiment impressionnantes.

Je n'ai pas pris énormément de notes tellement le talk était passionnant pour être honnête. Je vais tenter de faire une description plus complète pour ce talk, mais la partie intéressante était plus la logique en elle-même que ce qui est fait en Rust; le point sur Rust à retenir c'est que c'est possible de faire des choses vraiment performantes et propres avec !

# Async I/O and Tokio

Speaker : Alex Crichton

https://tokio.rs/

Ce talk est le seul ayant eu lieu le dimanche matin avant les workshop.
Pour contexte, Alex Crichton est un des Core développeurs de Rust qui a travaillé dessus pour Mozilla pendant 4 ans. C'est aussi un des principaux auteurs de Cargo, le gestionnaire de dépendances de Rust, ainsi qu'un des mainteneurs de la lib standard de Rust et de Tokio, LA lib pour des I/O asynchrones en Rust, sur laquelle ce talk portait.

Ce talk, contrairement à ce qui pourrait sembler à la lecture du titre, n'est PAS une présentation de "comment faire de l'async avec Tokio", mais plutôt...  "comment on implem de l'async en vrai ?". C'est super d'avoir de l'async en tant qu'utilisateur, mais quelles sont les mécaniques utilisées dérrière ?  Cette approche en fait donc définitivement le talk le plus intéressant de ce RustFest, ce qui en fait une très belle clôture mais en fait aussi quelque chose de difficile à vraiment résumer, je vais néanmoins tenter de faire au moins :)


Tokio c'est quoi ?

- Concrêtement :
    1. Utilisateur : "Je voudrais le contenu de https://xebia.fr/"
    2. Tokio : "Ok, tiens, voilà un `Future<Vec<u8>>`
- Tokio = Mio + Futures
- Mio = bibliothèque d'I/O cross-platform en Rust
- Futures = sortes de "promises" de Rust
    - Sentinelle pour des valeurs "en cours de calcul"
    - Internallement, capture un état pour produire une valeur
    - Composition de Futures !
- Tokio combine donc Mio et les Futures afin de proposer une event loop et des Futures basées sur des I/O
- Actuellement, Tokio est utilisé en production par un certain nombre d'entreprises et supporte les méthodes d'I/O suivantes : TCP, UDP, Sockets Unix, Named pipes, signaux, HTTP, HTTP/2, websockets, ...

Les Futures aujourd'hui :

- Traits pour une valeur (Future), plusieurs valeurs (Stream) ou des valeurs "push" (Sink)
- "Oneshot channels" : calcul in-memory de valeurs de manière asynchrone - `std::sync::mpsc : Channels multi-provider / single-consumer

Inconvénients des callbacks :

- Chers au runtime, force une allocation par transition d'état
- Nécessite de faire de la "gymnastique" en cas de multithreading

=> Contraintes :

- Les Futures doivent être des Traits
- Le Trait Future doit autoriser du virtual dispatch qui reste safe, via des `Box<>`
- Les transitions d'état doivent être peu coûteuses
- Pas de gymnastique nécessaire pour être thread safe

Futures et Tasks :

- Une Task est composée de plusieurs Futures
- Toutes les Futures au sein d'une Task suivent la même Task
- Les Tasks sont l'unité de concurrence
- Très similaire aux greens/lightweight threads

Futures basées sur du polling :

- Une valeur de retour à `None` signifie "not ready"
- Un retour de `Some` (type Option) résoud la Future
- ... mais en cas de `None`, quand rappeller poll ?

- Les Futures appartiennent à une seule Task
- Si la Future n'est pas prête... la Task doit savoir quand réessayer !
- Une valeur de retour de `None` signifie donc implicitement et automatiquement "je te notifierai plus tard"
- Utilisation d'Arc (atomic shared pointers en Rust) dans les Tasks

I/O et Futures via poll :

- Dans Tokio, TOUT est une Future
- Ces Futures peuvent potentiellement nécessiter d'attendre des I/O
- Le job de Tokio est de router les notifications d'I/O vers ces Tasks

Event Loop de Tokio :

- Concrêtement :
    - Kernel : "Le file descriptor 42 est prêt pour que tu ailles lire dessus"
    - Tokio : "Ok, je vais réveiller la Task qui attendait"
- Responsable de bloquer le thread courant
- Dispatch les events reçus de la part du kernel (pas de notifications de ce genre de chose sur Windows visiblement)


Pour conclure, l'implémentation des Futures de Rust est vraiment passionnante, et l'event loop de Tokio se charge de "traduire" les notifications d'I/O du kernel en notifications pour les Tasks qui wrappent les Futures.

# Conclusion

Cette conférence était vraiment une super vue d'ensemble sur ce qui se fait en Rust, avec des retours et des exemples de cas d'usage très variés, mais toujours avec le même point commun : le gros avantage de Rust, c'est sa safety ! Mention spéciale à Tokio, la bibliothèque d'I/O asynchrones en Rust.

Au final, tout ça confirme mon sentiment comme quoi Go c'est bien pour prototyper ou faire des applications vraiment minimales, mais que Rust reste plus approprié lorsque les besoins de safety et d'un langage complet arrivent (ça fait très troll comme phrase, mais je serai ravi d'en discuter !). Typiquement, je verrais très bien des orchestrateurs en Rust :) En revanche je n'ai vu aucun talk parlant d'API REST en Rust bien que ça soit évidemment possible et qu'il y a ait des bibliothèques pour en faciliter la construction.

L'exemple typique de use-case parfait pour Rust était l'embarqué et les tâches vraiment low-level avec besoin de contrôle fin sur la mémoire tout en gardant une certaine safety.

Notes :

- Le format des slots, 30min, était vraiment agréables.
- Je vais probablement enrichir la page Confluence de ce write-up sur le RustFest avec des liens vers les slides, éventuelles vidéos, etc. et le transformer en blog post :)


N'hésitez pas si vous avez des questions et/ou remarques !

Bonne soirée,




Room defrag! https://twitter.com/Horgix/status/914033174379995137
https://twitter.com/Horgix/status/914104108092678144

https://twitter.com/Horgix/status/914104844000141313

