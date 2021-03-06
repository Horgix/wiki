Il y a maintenant 1 mois, j'ai eu la chance d'aller au [RustFest](http://zurich.rustfest.eu/), une conférence sur le [**langage Rust**](https://www.rust-lang.org/en-US/) s'étant tenue à **Zürich**. Cet article est un retour sur les conférences que j'ai pu y voir, d'un point de vue très personnel et y incluant mes propres opinions.

Ce RustFest 2017 était composé de conférences le samedi, et de workshops le dimanche.
La journée du Samedi ayant été relativement dense, avec pas moins de **14 talks successifs sur une seule track**, je vais tenter ici de vous résumer les points principaux ayant retenu mon attention, et me permettrai de passer sous silence les points non pertinents afin d'éviter de vous faire perdre votre temps.

[tl;dr](https://en.wikipedia.org/wiki/TL%3BDR) : rendez-vous à [la conclusion](http://TODO-add-link) en fin d'article !

![rustfest-logo](https://s3-eu-west-1.amazonaws.com/xebia-blog-articles/rustfest-2017/logo.jpg)

# Keynote: A RustFest Carol

- Speaker : [**Felix Klock**](http://zurich.rustfest.eu/sessions/felix) ([`@pnkfelix`](https://twitter.com/pnkfelix)) -  Research Engineer @ Mozilla
- [Vidéo](https://www.youtube.com/watch?v=jywiVWKm1TI&list=PL85XCvVPmGQj9mqbJizw-zi-EhcpS5jTP&index=1)
- [Slides](http://pnkfx.org/presentations/rustfest-zurich-2017.html)

![01-rustfest-carol](https://s3-eu-west-1.amazonaws.com/xebia-blog-articles/rustfest-2017/01-rustfest-carol.jpg)

Felix Klock débute la journée en nous présentant un **historique de Rust** via une narration sous forme d'histoire. L'objectif ? Nous présenter **les principaux points d'évolutions de Rust**, que ce soit dans le langage lui même ou ses bibliothèques principales telles que [Serde](https://serde.rs/), et ce depuis les prémices de Rust jusqu'à aujourd'hui, avec comme message principal **"ne pas avoir peur du changement"**.

Pour ceux qui voudraient le rencontrer, Felix est quelqu'un de très sympathique avec beaucoup de recul sur Rust et il organise le [meetup Rust Paris](https://www.meetup.com/Rust-Paris/); n'hésitez donc pas à aller y faire un tour !

# Rust: an alternative to high-level programming languages?

- Speaker : [**Élisabeth Henry**](http://zurich.rustfest.eu/sessions/elisabeth) ([`@lise_henry`](https://twitter.com/lise__henry) / [`@crowdagger`](https://twitter.com/crowdagger)) - Fantasy novel writer
- [Vidéo](https://www.youtube.com/watch?v=Uocesohc6Z0&index=2&list=PL85XCvVPmGQj9mqbJizw-zi-EhcpS5jTP)
- [Slides](https://lise-henry.github.io/rostifest/pres.pdf)

![02-alt-high-level](https://s3-eu-west-1.amazonaws.com/xebia-blog-articles/rustfest-2017/02-alt-high-level.jpg)

Ce second talk apporte un point de vue très intéressant : celui d'un **utilisateur "high level" de Rust**. L'utilisateur en question ? Une utilisatrice : Elisabeth Henry... auteure française, qui se sert de Rust pour transformer ses livres qu'elle écrit en markdown vers du HTML et PDF (ce qui fait vraiment penser à [Pandoc](http://pandoc.org/) mais là n'est pas la question) !

Le profil n'est donc pas celui de quelqu'un qui attache une grande importance au langage en lui même, mais vraiment à son **utilisation**.

Pour commencer, elle nous présente sa définition de "high level" :

- Applications en ligne de commande, applications graphiques, petits jeux, ...
- Les performances ne sont pas vraiment une problématique
- La *safety* en terme de stabilité non plus
- Pas de réel besoin d’interactions low level
- On se situe plus au niveau de Java/Python/Ruby en terme de comparaison

Elle dresse le portrait suivant des langages de programmation impératifs :

- La plupart rendent vraiment facile le fait de faire des choses
- ... en autorisant de les faire n'importe comment (*"the wrong way"*)
- La plupart des langages faciles à apprendre cachent en réalité beaucoup de complexité
- De manière générale, ils ne rendent pas les choses plus simples sur le long terme

Malgré son utilisation high level, elle a pris le temps de comprendre la notion de références de Rust, qui peuvent être soit partagées, soit mutables, mais pas les deux ! Au final, Rust lui apporte vraiment de la ***memory safety* et évite les *data races***, et même un utilisateur high level fini par se rendre compte de ces avantages.

En résumé :

- Bénéfique sur le **long terme** plutôt que le court terme
- Difficile au début, mais **rend les choses bien plus faciles par la suite**
- Facilite la partie **gestion des bugs**, maintenance, et l'**acceptation des contributions**
- Au final, les alternatives sur ces avantages seraient les langages fonctionnels qui n'autorisent pas du tout de mutations, mais qui sont moins répandus et potentiellement plus complexes encore à prendre en main

# Macromancy - an introduction to Rust macros

- Speaker : [**Geoffroy Couprie**](http://zurich.rustfest.eu/sessions/geoffroy) ([`@gcouprie`](https://twitter.com/gcouprie)) - Security & QA @ CleverCloud
- [Vidéo](https://www.youtube.com/watch?v=8rodUyaGkQo&index=3&list=PL85XCvVPmGQj9mqbJizw-zi-EhcpS5jTP)

![03-macromancy](https://s3-eu-west-1.amazonaws.com/xebia-blog-articles/rustfest-2017/03-macromancy.jpg)

Talk très intéressant sur les macros en Rust... mais **de mon point de vue**, impossible à maintenir et tellement **loin de l'esprit craftsmanship** que je ne m'attarderai pas dessus.
Les points principaux évoqués sont : macros récursives, imbriquées, et *trace macros* pour afficher l'*expansion* des macros.

En résumé : **les macros de Rust permettent de faire énormément de choses...  presque trop**.

# Impractical Macros

- Speaker : [**Alex Burka**](http://zurich.rustfest.eu/sessions/alex) ([`@durka42`](https://twitter.com/durka42))
- [Vidéo](https://www.youtube.com/watch?v=ApOUBBOvZDo&index=4&list=PL85XCvVPmGQj9mqbJizw-zi-EhcpS5jTP)

Pour appuyer le talk précédent, Alex Burka nous a présenté un interpréteur [Brainfuck](https://fr.wikipedia.org/wiki/Brainfuck) en **pures macros Rust**, donc capable de comprendre et d’exécuter du code Brainfuck **à la compilation**.

Bien que très intriguant et démonstratif, ce talk n'a pas vraiment de raison d'être détaillé, sachez juste que c'est possible... ***For science!***

# Antimony: a real time distributed stream processing system

- Speakers :
    - [**Mohammed Makhlouf**](http://zurich.rustfest.eu/sessions/mohammed) ([`@msmakhlouf`](https://twitter.com/msmakhlouf)) - Software/Security Engineer @ Qatar CERT
    - **Mohammad Samir** ([`@_msamir_`](https://twitter.com/_msamir_))
- [Vidéo](https://www.youtube.com/watch?v=gBRwLAyZHlU&index=5&list=PL85XCvVPmGQj9mqbJizw-zi-EhcpS5jTP)
- [Slides](https://speakerdeck.com/msmakhlouf/antimony-a-real-time-stream-processing)
- [Site web - antimony.rs](https://antimony.rs/)

![05-antimony](https://s3-eu-west-1.amazonaws.com/xebia-blog-articles/rustfest-2017/05-antimony.jpg)

Mon point de vue sur ce talk est relativement mitigé. Il nous a été présenté un système d'analyse real-time de requêtes DNS en Rust basé sur Apache Storm afin de détecter des malwares, par exemple via des noms de domaines connus ou proche, ou via des critères tels que la longueur.

Le talk pourrait se résumer en *"On a pris Apache Storm, on a surchargé nos cluster Zookeeper, et on a fini par drastiquement sur-provisionner TOUT et par lancer chaque topologie sur un cluster Storm séparé avec des clusters Zookeeper séparés"*. Mention honorable cependant pour [pyleus](https://github.com/YelpArchive/pyleus), le framework Python de Yelp pour développer et gérer des topologies Storm. Très peu de Rust donc.

Au final, la partie la plus intéressante reste sans doute la mention du [**papier "Héron" de Twitter**](https://dl.acm.org/citation.cfm?id=2742788) sur le stream processing, ainsi que la rapide mention des bibliothèques [Tokio](https://tokio.rs/) et [Mio](https://github.com/carllerche/mio) pour les **IO asynchrones en Rust**, sur lesquelles je reviendrai plus tard.

# Testing strategies and pattern for efficient TDD in Rust

- Speaker : [**Thomas Wickham**](http://zurich.rustfest.eu/sessions/thomas) ([`@mackwic`](https://twitter.com/mackwic)) - Consultant @ Octo
- [Vidéo](https://www.youtube.com/watch?v=U3F7uAOCjEo&index=6&list=PL85XCvVPmGQj9mqbJizw-zi-EhcpS5jTP)
- [Slides](http://slides.com/thomaswickham/efficient-tdd-in-rust/#/)

https://twitter.com/Horgix/status/914098873018327040
![06-tdd](https://s3-eu-west-1.amazonaws.com/xebia-blog-articles/rustfest-2017/06-tdd.jpg)

Je suis un peu biaisé sur ce talk; en effet, le speaker est un ami ! Mais vu qu'il s'agit d'un talk plus sur le côté *TDD* que l'aspect *Rust*, je pense que vous pourrez en retrouver la majorité sur le [reste du blog](http://blog.xebia.fr/?s=TDD) ou sur [son podcast café-craft](http://www.cafe-craft.fr/).

Élément principal côté *"TDD en Rust"* à retenir : au final le compilateur vérifie déjà tellement de choses et garanti une telle *safety* par les **contraintes qu'il impose** que les tests en sont **relativement réduits** et qu'on peut se **concentrer sur les points vraiment utiles** plutôt que d'avoir des tonnes de *"edge cases"*. Par ailleurs, Rust a tendance à faciliter la gestion des cas d'erreurs, ce qui permet de faire émerger un design solide et complet.

# A Rust-based Runtime for the Internet of Things

- Speaker : [**Niklas Adolfsson**](http://zurich.rustfest.eu/sessions/niklas) ([`@niklasad1`](https://twitter.com/niklasad1)) - Embedded software developer @ Cybercom
- [Vidéo](https://www.youtube.com/watch?v=reQ7_oXwECQ&index=8&list=PL85XCvVPmGQj9mqbJizw-zi-EhcpS5jTP)
- [Site web - tockos.org](https://www.tockos.org/)
- [PDF de la thèse sur le sujet](http://publications.lib.chalmers.se/records/fulltext/250074/250074.pdf)

![07-iot](https://s3-eu-west-1.amazonaws.com/xebia-blog-articles/rustfest-2017/07-iot.jpg)

Ce talk nous présentait [TockOS](https://www.tockos.org/), un **OS écrit en Rust** pour tout ce qui est IoT : semblant de micro-kernel, isolation mémoire, processus en user-space, ...

Pourquoi Rust dans un tel contexte ?

- *Memory safety* et *type safety*
- Contrôle fin sur la mémoire
- Très peu d'overhead au runtime

Le design de l'OS lui même et des éléments écrits en Rust est disponible dans la documentation de TockOS : <https://www.tockos.org/documentation/design>

Au final, Rust permet d'avoir exactement ce qu'on cherche sur de l'IoT : de la **fiabilité**, du **contrôle bas niveau** et une **très faible consommation de ressources**.

# A hammer you can only hold by the handle

- Speaker : [**Andrea Lattuada**](http://zurich.rustfest.eu/sessions/andrea) ([`@utaal`](https://twitter.com/utaal)) - Researcher @ ETH Zürich
- [Vidéo](https://www.youtube.com/watch?v=3Q2hQfYW-XM&index=9&list=PL85XCvVPmGQj9mqbJizw-zi-EhcpS5jTP)
- [Slides](https://speakerdeck.com/utaal/a-hammer-you-can-only-hold-by-the-handle)

![08-hammer](https://s3-eu-west-1.amazonaws.com/xebia-blog-articles/rustfest-2017/08-hammer.jpg)

Cette présentation d'Andrea Lattuada était de mon point de vue tout simplement géniale, et **abordait sous un angle limpide les notions d'[ownership](https://doc.rust-lang.org/book/second-edition/ch04-01-what-is-ownership.html) et de [borrow](https://doc.rust-lang.org/book/second-edition/ch04-02-references-and-borrowing.html) de variables** en Rust, qui sont souvent les notions les plus ardues à "prendre en main" lorsque l'on débute avec le langage.

Ce n'est par conséquent pas vraiment un talk facile à résumer, sans vous renvoyer vers la documentation de Rust... Mais pour préciser un peu, il a réalisé une analogie très intéressante de l'allocation d'objets et de la gestion de leur *lifetime* ainsi que l'accès concurrentiel par rapport à une lettre que l'on souhaiterait envoyer :

- Enveloppe = type `Option` contenant potentiellement une lettre
- Lettre = `struct`
- Shipping = méthode utilisant l'enveloppe.

Avec cet exemple, il a démontré comment les primitives du langage nous permettent d'avoir une **garantie d'*"exactly once"* sur certains appels, une garantie d'ordre ainsi qu'une garantie de drop/free**.

# Fearless concurrency in your microcontroller

- Speaker : [**Jorge Aparicio**](http://zurich.rustfest.eu/sessions/jorge) ([`@japaricious`](https://twitter.com/japaricious)) - Self-proclaimed roboticist
- [Vidéo](https://www.youtube.com/watch?v=J4dZRrldMcI&index=10&list=PL85XCvVPmGQj9mqbJizw-zi-EhcpS5jTP)

![09-microcontroller](https://s3-eu-west-1.amazonaws.com/xebia-blog-articles/rustfest-2017/09-microcontroller.jpg)

Ce talk présentait une gestion low-level de la concurrence en Rust, avec comme fil rouge la problématique suivante :

- Tâche 1 : doit se lancer toutes les *10ms* et prend *2ms* à s’exécuter
- Tâche 2 : doit se lancer toutes les *1ms* et prend *100µs* à s’exécuter
- Est-il possible de respecter ces contraintes en utilisant du multitasking coopératif ?

Au final, la problématique n'est **pas spécifique à Rust**, mais le langage permet de la résoudre en restant complètement *memory safe*, avec une absence de *deadlocks*, et des *data races* **détectées à la compilation**. Tout ça sur des microcontrôleurs d'un seul core, sans avoir à se reposer sur un garbage collector; soit exactement le type de points positifs que l'on souhaiterait lorsque l'on travail avec des microcontrôleurs !

Le blog post réalisé bien avant ce talk par son auteur vous donnera bien plus de détails que ce que je ne serais capable d'inclure dans ce résumé : <http://blog.japaric.io/fearless-concurrency/>

# Mistakes to avoid when writing a wrapper around a C library

- Speaker : [**Pierre Krieger**](http://zurich.rustfest.eu/sessions/pierre) ([`@tomaka17`](https://twitter.com/tomaka17)) - Graphics programmer
- [Vidéo](https://www.youtube.com/watch?v=LLde-PJJZQA&index=11&list=PL85XCvVPmGQj9mqbJizw-zi-EhcpS5jTP)
- [Slides (sources)](https://github.com/tomaka/rustfest-2017-slides)

![10-wrap-c-lib](https://s3-eu-west-1.amazonaws.com/xebia-blog-articles/rustfest-2017/10-wrap-c-lib.jpg)

Rust étant régulièrement comparé à *"du C, mais en plus safe"*, il est logique de se retrouver avec des besoins communs. Mais plutôt que de réimplémenter intégralement les bibliothèques bas niveau en C, un choix souvent fait est celui de *wrapper* ces bibliothèques C avec du Rust **afin d'exposer une API plus safe sans pour autant réimplémenter toute la logique**.

Ce talk présentait **9 "erreurs" à éviter lors du wrapping d'une bibliothèque C en Rust**, et en voici le résumé :

Erreur n°1: **Utiliser la lifetime (scoping) pour des objets "long-lived"**

- ⇒ N'utiliser les lifetimes que pour des objets temporaires (comme des locks ou des accesseurs)
- ⇒ Utiliser [Arc](https://doc.rust-lang.org/std/sync/struct.Arc.html)/[Rc](https://doc.rust-lang.org/std/rc/struct.Rc.html) (shared pointers dans la lib standard de Rust) pour les dépendances entre des objets long-lived

Erreur n°2 : **Supposer que les implémentations d'un Trait ne sont pas buguées**

- ⇒ Déréférencer dès le début et faire les vérifications nécessaires ou utiliser un Trait unsafe custom

Erreur n°3 : **Lire des primitives en mémoire sans vérification**

Erreur n°4 : **Oublier les variables globales cachées en C...**

- Qu'en est-il des Mutex par exemple ? Si on charge différentes versions de la même bibliothèque... chaque version aura son propre lock sur des Mutex différentes, et on a perdu !
- ⇒ Certaines bibliothèques sont impossible à wrapper de manière safe, by design, par exemple [OpenAL](http://www.openal.org/) ou [Xlib](https://en.wikipedia.org/wiki/Xlib)

Erreur n°5 : **Ignorer les problèmes de leak potentiels en C**

- ⇒ Ne PAS supposer que les destructeurs seront appelés, et abuser des `assert`s
- ⇒ La manière de décrire la solution m'a fait sourire, alors en voici la citation exacte : *"We'll do something called 'Pre-pooping your pants'.  But don't Google that, or at least do it for Rust."*

Erreur n°6 : **Essayer d'écrire une abstraction haut niveau à la bibliothèque directement**

- Les utilisateurs vont rapidement se plaindre des features de la bibliothèque en C qui ne sont pas exposées par l'abstraction en Rust
- ⇒ Rester aussi proche de la bibliothèque C que possible tout en restant safe
- ⇒ Ajouter des abstractions additionnelles plus tard, dans un second temps
- ⇒ Optimiser les features les plus haut niveau si nécessaire

Erreur n°7 : **Supposer que les `struct`s et les `enum`s ont une certaine disposition en mémoire**

- ⇒ Utiliser l'annotation `#[repr(c)]` pour forcer le layout en mémoire

Erreur n°8 : **Ne pas tester son wrapper à une échelle suffisamment large**

Erreur n°9 : **Ne pas `catch` les potentiels Rust panics au sein de callbacks appelés par la bibliothèque en C**

- ⇒ `catch_unwind` des panics partout où nécessaire

Conclusion sur ce talk : lire <https://doc.rust-lang.org/nomicon/> !

# Rust In Rhymes

- Speaker : [**Andre Bogus**](http://zurich.rustfest.eu/sessions/llogiq) ([`@llogiq`](https://twitter.com/llogiq))
- [Vidéo](https://www.youtube.com/watch?v=JR6aHXlRAOM&index=12&t=181s&list=PL85XCvVPmGQj9mqbJizw-zi-EhcpS5jTP)

![11-rhymes](https://s3-eu-west-1.amazonaws.com/xebia-blog-articles/rustfest-2017/11-rhymes.jpg)

Que dire... Ce talk était un **véritable show**, entièrement en rimes, mais cela s'arrête là.

Du coup, il n'y a pas grand chose à en résumer à l'écrit, et son appréciation dépendra grandement de votre humour ! Si vous souhaitez vous laisser tenter, le lien vers la vidéo est un peu plus haut.

# Create Rust games easily

- Speaker : [**Lisa**](http://zurich.rustfest.eu/sessions/lislis) - Product team @ Travis CI
- [Vidéo](https://www.youtube.com/watch?v=str_mex__0M&index=13&list=PL85XCvVPmGQj9mqbJizw-zi-EhcpS5jTP)

Honnêtement, ce talk bien qu'intéressant m'a un peu déçu. Du live coding à base de copier/coller, trop rapide pour être réellement suivi, et avec un résultat final relativement minimal.

# SHAR: Rust's gamedev experience

- Speaker : [**Fedor Logachev**](http://zurich.rustfest.eu/sessions/fedor) - Game programmer
- [Vidéo](https://www.youtube.com/watch?v=nXR8f4r6ggM&index=14&list=PL85XCvVPmGQj9mqbJizw-zi-EhcpS5jTP)
- [Site web - SHAR project](http://sharonos.com/)

![13-gamedev](https://s3-eu-west-1.amazonaws.com/xebia-blog-articles/rustfest-2017/13-gamedev.jpg)

Retour plus intéressant que le précédent... mais la partie jeux-vidéos est un peu trop spécialisée pour que je sois à même de la critiquer; si vous voulez en savoir plus n'hésitez pas à jeter un œil à la vidéo !

# Type-safe & high-perf distributed actor systems with Rust

- Speaker : [**Anselm Eickhoff**](http://zurich.rustfest.eu/sessions/anselm) ([`@ae_play`](https://twitter.com/ae_play)) - Computer science dentue
- [Vidéo](https://www.youtube.com/watch?v=LiIoE8ArACs&index=15&list=PL85XCvVPmGQj9mqbJizw-zi-EhcpS5jTP)
- [Github - Citybound](https://github.com/citybound/citybound)

![14-actors](https://s3-eu-west-1.amazonaws.com/xebia-blog-articles/rustfest-2017/14-actors.jpg)

**LA** surprise de cette fin de journée. Concrètement, tout est dans le titre, et le talk était une énorme démonstration du résultat avec explications sur l'implémentation. Globalement : création d'un simulateur de ville à base d'**Acteurs distribués, en Rust**, avec des performances vraiment impressionnantes.

Je n'ai pas pris énormément de notes tellement le talk était passionnant pour être honnête. Je vous invite cependant à en regarder la vidéo dont le lien est disponible ci-dessus et qui en vaut le détour !
La partie intéressante était plus la logique en elle-même que ce qui est fait en Rust; le point à retenir sur Rust étant la possibilité d'implémenter un tel **design d'acteurs distribués** de manière vraiment propre et solide notamment grâce à la type-safety fournie par Rust, le tout de manière performante.

# Async I/O and Tokio

- Speaker : [**Alex Crichton**](http://zurich.rustfest.eu/sessions/acrichto) - Rust developer
- [Vidéo](https://www.youtube.com/watch?v=4QZ0-vIIFug&index=16&list=PL85XCvVPmGQj9mqbJizw-zi-EhcpS5jTP)
- [Site web - tokio.rs](https://tokio.rs/)

![15-tokio-1](https://s3-eu-west-1.amazonaws.com/xebia-blog-articles/rustfest-2017/15-tokio-1.jpg)

![15-tokio-2](https://s3-eu-west-1.amazonaws.com/xebia-blog-articles/rustfest-2017/15-tokio-2.jpg)

Ce talk est le seul ayant eu lieu le dimanche matin avant les workshops

Pour contexte, Alex Crichton est un des **Core développeurs de Rust** qui a travaillé dessus pour Mozilla pendant 4 ans. C'est aussi **un des principaux auteurs de [Cargo](http://doc.crates.io/)**, le gestionnaire de dépendances de Rust, ainsi qu'**un des mainteneurs de la lib standard de Rust et de [Tokio](https://tokio.rs/)**, LA lib pour des I/O asynchrones en Rust, sur laquelle cette présentation portait justement.

Ce talk, contrairement à ce qui pourrait sembler à la lecture du titre, n'est PAS une présentation de *"comment faire de l'async avec Tokio"*, mais plutôt...  ***"comment on implémente de l'async, en vrai ?"***. En effet, c'est super d'avoir de l'async en tant qu'utilisateur, mais quelles sont les mécanismes utilisés derrière ?  Cette approche en fait donc définitivement le **talk le plus intéressant de ce RustFest**, ce qui en fait une très belle clôture mais aussi quelque chose de difficile à vraiment résumer.

Tokio c'est quoi ?

- Concrètement :
    1. Utilisateur : *"Je voudrais le contenu de <https://blog.xebia.fr/>"*
    2. Tokio : *"OK, tiens, voilà un `Future<Vec<u8>>`*
- **Tokio = Mio + Futures**
- [Mio](https://github.com/carllerche/mio) = bibliothèque d'I/O cross-platform en Rust
- [Futures](https://docs.rs/futures/0.1.17/futures/) = sortes de ["promises"](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) de Rust
    - Sentinelle pour des valeurs "en cours de calcul"
    - En interne, capture un état pour produire une valeur
    - Composition de Futures possible
    - `Trait`s pour une valeur (Future), plusieurs valeurs (Stream) ou des valeurs *"push"* (Sink)
    - *Oneshot channels* : calcul in-memory de valeurs de manière asynchrone - `std::sync::mpsc` : Channels multi-provider / single-consumer
- Tokio combine donc Mio et les Futures afin de **proposer une event loop et des Futures basées sur des I/O**
- Actuellement, Tokio est utilisé en production par un certain nombre d'entreprises et supporte les méthodes d'I/O suivantes : TCP, UDP, Sockets UNIX, Named pipes, signaux, HTTP, HTTP/2, websockets, ...

Inconvénients des callbacks :

- **Chers au runtime**, force une allocation par transition d'état
- Nécessite de faire de la **"gymnastique" en cas de multithreading**

Les contraintes sont donc :

- Les Futures doivent être des **Traits**
- Le Trait Future doit autoriser du **virtual dispatch** qui reste safe, via des `Box<T>`
- Les transitions d'état doivent être peu coûteuses
- **Pas de gymnastique nécessaire pour être thread safe**

Futures et Tasks :

- Une **Task** est composée de **plusieurs Futures**
- Toutes les Futures au sein d'une Task suivent la même Task
- Les Tasks sont l'**unité de concurrence**
- Très similaire aux greens/lightweight threads

Futures basées sur du polling :

- Une valeur de retour à `None` signifie *"not ready"*
- Un retour de `Some` (type Option) résout la Future
- ... mais en cas de `None`, **quand rappeler `poll` ?**

- Les Futures appartiennent à une seule Task
- Si la Future n'est pas prête... la Task doit **savoir quand réessayer** !
- Une valeur de retour de `None` signifie donc **implicitement et automatiquement** *"je te notifierai plus tard"*
- Utilisation d'Arc (atomic shared pointers en Rust) dans les Tasks

I/O et Futures via poll :

- Dans Tokio, **TOUT est une Future**
- Ces Futures peuvent potentiellement nécessiter d'attendre des I/O
- Le job de Tokio est de **router les notifications d'I/O vers ces Tasks**

Event Loop de Tokio :

- Concrètement :
    - Kernel : *"Le file descriptor 42 est prêt pour que tu ailles lire dessus"*
    - Tokio : *"OK, je vais réveiller la Task qui attendait"*
- Responsable de **bloquer le thread courant**
- Dispatch les évènements reçus de la part du kernel (pas de notifications de ce genre de chose sur Windows visiblement)

Pour conclure, l'implémentation des Futures de Rust est **vraiment passionnante**, et l'event loop de Tokio se charge de "traduire" les notifications d'I/O du kernel en notifications pour les Tasks qui wrappent les Futures. Au final, bien que l'on entende souvent *"poll-er c'est mal"*, **il y a toujours quelque chose à un endroit qui finit par faire du polling**, mais dans le cas présent on le délègue le plus loin possible, en l’occurrence au kernel Linux lui-même.

# Remarques diverses sur l'évènement lui-même

- Le format des slots, 30min, était vraiment agréable
- Les organisateurs proposaient [2 couleurs de tour-de-cou pour les badges](https://twitter.com/Horgix/status/914104844000141313) : noir ou rouge, le noir signifiant *"OK pour les photos"* et le rouge *"Je ne souhaite pas être pris en photo durant l'évènement"*. Un grand bravo à eux pour avoir songé au côté vie privée, tant il est maintenant courant de photographier tout et tout le monde lors de conférences pour ensuite tout publier en ligne.
- Toutes les vidéos sont disponibles sur la [playlist YouTube officielle du RustFest](https://www.youtube.com/playlist?list=PL85XCvVPmGQj9mqbJizw-zi-EhcpS5jTP)

# Conclusion

Cette conférence était vraiment une **excellente vue d'ensemble sur ce qui se fait en Rust**, avec des retours et des exemples de cas d'usage très variés, mais toujours avec le même point commun : **le gros avantage de Rust, c'est la safety qu'il apporte** ! Mention spéciale à **Tokio**, la bibliothèque d'I/O asynchrones en Rust, et au [talk d'Alex Crichton à ce sujet](https://www.youtube.com/watch?v=4QZ0-vIIFug&index=16&list=PL85XCvVPmGQj9mqbJizw-zi-EhcpS5jTP) que je vous invite à regarder.

Au final, ce RustFest confirme mon sentiment que Rust est vraiment approprié lorsque les besoins de *safety* et d'un langage complet se font sentir, là où Go qui lui est souvent opposé, est, je trouve, plus approprié pour prototyper rapidement. Typiquement, je verrais très bien des orchestrateurs ou des composants système bas niveau en Rust ! En revanche, je n'ai vu aucun talk évoquant la construction d'API REST en Rust lors de cette conférence, bien que ce soit évidemment possible et facilité par des bibliothèques telles que [Rocket](https://rocket.rs/). Si ce point vous intéresse, je vous invite à vous tourner vers [la page *"are we web yet?"* de Rust](http://www.arewewebyet.org/)

Pour conclure, l'exemple typique de use-case parfait pour Rust semble être l'embarqué et les tâches vraiment low-level avec besoin de contrôle fin sur la mémoire tout en gardant une certaine solidité.

Enfin, notez que [le prochain RustFest se tiendra à Paris en 2018](https://twitter.com/RustFest/status/914173735976017920), et je vous y donne donc rendez-vous :)

https://twitter.com/Horgix/status/914104108092678144

![group-pic](https://s3-eu-west-1.amazonaws.com/xebia-blog-articles/rustfest-2017/group-pic.jpg)
