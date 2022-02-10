# TD DevSecEmb
### TD sécurité et systeme embarqué

#### TD1: Emily

voici les différentes étapes réaliser pour patch le binaire:
![step 1](/capture_td/step1.png)

![step 2](/capture_td/step2.png)

![step 3](/capture_td/step3.png)

![step 4](/capture_td/step4.png)

![step 5](/capture_td/step5.png)

###### Réponses aux questions:

1. La principale différence entre les deux architectures tient dans les choix de conception de leur jeu d’instruction : 
l'architecture x86 est une architecture CISC (Complex Instruction Set Computer), tandis que l’ARM est une architecture RISC (Reduced ISC).

Cela signifie que les puces ARM ne supportent que des instructions simples et de taille fixe (4 octets pour le jeu d’instructions ARM standard, 2 octets pour le jeu réduit Thumb), s’exécutant en un nombre constant de cycles.
A l’inverse les puces x86, permettent de réaliser certaines tâches complexes car les instructions nécessitent plus de cycle.

2. avec le langage assembleur on remarque qu'une boucle for s'execute grâce à des jump entre différentes addresse. On peut donc se servir de ce système pour modifiez l'addresse d'arriver du jump pour executer une autre instruction par exemple.

3. Le patching est par définition difficile à empecher, le seul moyen d'essayer de dissuader des attaquants serait de rendre le code le plus complexe possible au niveau assembleur. 
Pour cela il suffit de rajouter du bruit dans le code, c'est à dire de rajouter des portions de codes inutiles qui ne servent qu'à mélanger du vrai code dans du faux afin de dissuader des attaquants.


#### TD2 Binwalk

On utilise binwalk et en cherchant dans tous les fichier utiliser par l'image on cherche l'image du pingouin de linux.
Après des recherches rapide on peut savoir que le pingouin de linux se nomme Tux. On fait donc une recherche sur **"tux"** et on trouve sa location dans l'image assez rapidement:
![tux found](/capture_td/binwalk.png)

###### Réponse aux questions

1. Même si on trouve rapidement l'image de tux assez rapidement, on se rend compte que le modifier n'est pas si simple. Ce qui nous en empêche, doit être le fait qu'on ne possède pas les d'écriture sur l'image

2. Pour contourner cette situation il faut réussir à démarrer l'image linux  en tant que root et non en tant qu'user.

3. 


#### TD3 Speedrun

Une fois le build executé et l'image d'ubuntu executé on lance le binaire ***speedrun-001*** en étant root et le programme nous propose d'entrer une chaine de caractère.

On entre alors une chaine de caractère assez longue pour dépasser la mêmoire et créer un buffer overflow. on rentre donc une suite assez longue de A et on obtient:
![segmentation fult](/capture_td/segmentation.PNG)

on peut maintenant utiliser l'outils gdb afin de connaitre l'offset du dépassement afin de savoir ou ajouter du code.

une fois l'offset trouvé on utilise une rop chain afin de pouvoir injecter un buffer assez long et de modifier l'execution du binaire. On obitent alors:
![RopChain](/capture_td/Ropchain.PNG)

###### Question:

1. Une fois root, un attaquant bénéficie des droits administrateur et peux donc executer tous ce qu'il veut dans le système. Ainsi avec les droits root la seule limite d'un attaquant serait son imagination.

4. Tout d'abord il faut absolument éviter d'avoir un code qui permet le segmentation fault. Il faut tenter de proteger son code des bugs en les anticipants le plus possible. Si on peut anticiper un bug alors il est possible, lors du développement du programme, de gérer ces bugs, par exemple à l'aide de try catch. Cela peut permettre de diminuer la surface d'attaque.


#### TD4 Toolbox

Voici des liens vers d'autres github décrivant des attaques man in the middle sur différentes surface.
Pour des raisons de manques de moyens matériels, je n'ai malheuresement pas pu tester ces méthodes, toutefois les analyser et comprendre leur principe fut très enrichissant et m'a permis de mieux appréhender ces interfaces/communication.
J'espère qu'elles seront utiles pour la fabrication de votre toolBox

Attaques Man in the Middle sur:

-USB: https://github.com/0x7ace80/virtualbox_usb_mitm

-Bluetooth: https://github.com/DigitalSecurity/btlejuice 

-WiFi: https://github.com/maneshthankappan/Multi-Channel-Man-in-the-Middle-Attacks-Against-Protected-Wi-Fi-Networks-By-Improved-Variant

-NFC: https://github.com/EMVrace/EMVrace.github.io/blob/master/README.md


###### Question

1. Pour évaluer la criticité d'une vlnérabilité on va prendre deux paramètre en compte:
    - Sa probabilité de survenir
    - le type et la quantité de données en danger

    En effet si la probabilté qu'une faille soit exploiter est grande mais que les données impacté ne sont pas importante ou en très faible quantité, alors la vulnérabilité ne sera pas critique. Il en est de même si les données impactées sont en grande quantité ou très importantes mais que la probabilité que la faille soit exploité est extremement faible. A l'inverse si la probabilité est élévé et que les données sont importantes alors la vulnérabilité peut être considérer comme critique. Tout ceci peut être résumé dans ce tableau évaluant la criticité d'un vulnérabilité:
    ![vulnérbilité](/capture_td/Criticité.PNG)


