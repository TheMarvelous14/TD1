# TD DevSecEmb
### TD sécurité et systeme embarqué

#### TD1: Emily

voici les différentes étapes réaliser pour patch le binaire:
![step 1](/capture_td/step1.png)

![step 2](/capture_td/step2.png)

![step 3](/capture_td/step3.png)

![step 4](/capture_td/step4.png)

![step 5](/capture_td/step5.png)

###### Réponse aux question:

1. La principale différence entre les deux architectures tient dans les choix de conception de leur jeu d’instruction : 
l'architecture x86 est une architecture CISC (Complex Instruction Set Computer), tandis que l’ARM est une architecture RISC (Reduced ISC).

Cela signifie que les puces ARM ne supportent que des instructions simples et de taille fixe (4 octets pour le jeu d’instructions ARM standard, 2 octets pour le jeu réduit Thumb), s’exécutant en un nombre constant de cycles.
A l’inverse les puces x86, permettent de réaliser certaines tâches complexes car les instructions nécessitent plus de cycle.

2. avec le langage assembleur on remarque qu'une boucle for s'execute grâce à des jump entre différentes addresse. On peut donc se servir de ce système pour modifiez l'addresse d'arriver du jump pour executer une autre instruction par exemple.

3. Le patching est par définition difficile à empecher, le seul moyen d'essayer de dissuader des attaquants serait de rendre le code le plus complexe possible au niveau assembleur. 
Pour cela il suffit de rajouter du bruit dans le code, c'est à dire de rajouter des portions de codes inutiles qui ne servent qu'à mélanger du vrai code dans du faux afin de dissuader des attaquants.


#### TD2 Binwalk

On utilise binwalk et en cherchant dans tous les fichier utiliser par l'image on cherche l'image du pingouin de linux.
Après des recherches rapide on peut savoir que le pingouin de linux se nomme Tux. On fait donc une recherche sur **"tux"** et on trouve:
![tux found](/capture_td/binwalk.png)

