# Week 4 - 05.08/09.08

12/08/2024

Bonjour Monsier Quitin,

Voici le rapport de ma quatrième semaine de stage.

Cette semaine, j'étais confronté à deux fronts différents : le microcontrôleur et le code PC. 

Mon premier objectif de la semaine était de tester d'envoyer des signaux de déclenchement (trigger signal) à une camera et ainsi, acquérir des images. D'abord, j'ai dû installer la caméra et identifier les fils du câble de trigger (6-pin cable). L'identification des fils était faite avec un multimètre en configuration court-circuit. En posant les sondes dans un des pins, on pouvait détecter le fil correspond en posant l'autre sonde dessus et en espérant que le multimètre sonne. En effet, lorsqu'on a un court-circuit cela veut dire que les sondes sont posées sur le même fil. Une fois l'identification faite, je savais quel fil je devais relier à la masse et celui que je devais relier à mon GPIO. 

Ensuite, je devais configurer le GPIO dans le microcontrôleur. D'abord, j'ai fait ceci dans le clone d'Arduino avec lequel je prototypais le système. Configurer le GPIO était hyper simple et le signal était correct. Ainsi, j'ai pu trigger la camera en utilisant le microcontrôleur, sous commande du logiciel PC. Ceci montre que le module est fonctionnel et que le design est valide. Le microcontrôleur fournit bien la bonne tension nécessaire pour trigger la caméra, c'est-à-dire, 3.3V. Par contre, le problème est venu quand j'ai voulu implémenter un simple programme qu'allait envoyer le signal de trigger à une période constante en utilisant le microcontrôleur que j'ai choisi, Renesas RTK5RX65N. En fait, l'environnement de développement proposé par Renesas est très complet mais pas pour autant très explicite. Il existe beaucoup de documentation sur comment implémenter des fonctionnalités dans les plaques Renesas mais elles sont très théoriques et difficile à lire. La courbe d'apprentissage de cette IDE est trop raide et programmer avec semble contre-productif. Par contre, du fait que ce soit très complet, cela implique aussi qu'il ne faut pas trop écrire. La majorité des configurations se fait via son Smart Configurator qui génère du code automatiquement. Le problème est savoir où chercher ce qu'il faut et savoir comment la fonctionnalité est implémentée dans leur architecture. Ceci montre que l'IDE doit avoir un fort impact sur la décision d'achat d'un microcontrôleur et qu'un microcontrôleur compatible avec l'IDE Arduino aura un développement beaucoup plus rapide.

En parallèle aux tâches de microcontrôleur, je retravaillais l'architecture du logiciel PC. L'idée était de déléguer tous les appels des librairies à des classes spécifiques pour pouvoir faire de l'abstraction. En effet, l'architecture doit être compatible avec n'importe lequel OS et il doit aussi abstraire le type de communication établi entre le PC et le uC, que ce soit serial ou ethernet par exemple. L'idée est d'augmenter la modularité et la compatibilité du logiciel. 

En fin de semaine, je me suis lancé dans la recherche pour mettre en place la communication en série de la plaque Renesas avec le PC. D'abord, j'ai galéré deux jours en essayant de mettre en place la communication en série avec USB. En effet, j'ai fait face à deux problèmes : 1) configurer une interface USB est un travail trop ardu et même déconseillé ; 2) j'essayais de configurer le port USB du débuggueur à faire une communication en série, ce qui n'est pas possible. Au final, j'ai appris beaucoup sur le protocol USB, son implémentation hardware et software. Également, j'ai appris que la communauté de développeur peut sauver ta peau. J'ai dit cela car après avoir galéré pendant deux jours, j'ai lancé une question sur le forum de Renesas et un des développeurs m'a répondu qu'il n'est pas pratique de souder et configurer un nouveau port USB, car selon lui "much work should be done". À la place, il m'a proposé d'acheter et installer un module USB-to-UART et de configurer une des Serial Communication Interfaces (SCI) de la plaque pour enfin mettre en place cette communication. Alors, après avoir discuté avec mes maîtres de stages, nous avons commandé un module FTDI FT232RL.

Et voilà un mois de stage passé. J'ai appris énornement depuis le début de mon stage. Dès le dimensionnement et choix d'un microcontrôleur, à l'implémentation d'un protocole de communication et les parseurs équivalents, au design d'un logiciel d'architecture modulaire et forte abstraite. Aussi, j'aime bien travailler chez Snellium, car je suis engagé dans un projet qui a du sens pour eux, j'ai des libertés et des responsabilités en tant qu'ingénieur et je fais face à des défis.  

Ceci résume ma semaine passée.

Bien à vous,

Brenno Ferreira.