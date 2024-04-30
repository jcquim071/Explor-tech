# Quelques bonnes pratiques :

* Fermer si possible les applications graphiques lourdes avant votre déconnexion de X2GO.
* Compiler vos applications avec les bonnes options de vectorisation (AVX) et instructions. Les partitions **std** et **hf** supporte AVX2, les partitions **ivy** et **k20** supporte AVX.
* Spécifier une estimation correcte du temps de calcul de votre job, une durée de job correctement estimée permet de fluidifier l'exécution des jobs.