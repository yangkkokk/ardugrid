## Installation de l'éolienne Skystream effectuée le 10 juin 2011 sur le site de test de Mercinat à Etel (Morbihan 56) ##

http://pachube.com/feeds/35020

  * ID0 = Puissance instantanée (mesure sur l’injection réseau toutes les 10 secondes)
  * ID5 = Production journalière (données historiques récupérées par SkyView)
  * ID6 = Production depuis l'installation (à partir de l'historique Skyview)

Les données anémomètres 6/9/12/18 mètres sont dispos en temps réel sur les autres datafeeds Mercinat.

L’instrumentation développée par Mercinat fait appel en partie à du matériel et du logiciel Open Source. La quasi-totalité des détails (hw et sw) sera disponible fin novembre 2011 sur Google Code Project Hosting à http://code.google.com/u/thierry.brunetdecourssou@gmail.com/ afin de permettre à tout le monde d’effectuer la remontée en temps réel des informations sur Pachube.

La variante Nanode de l’Arduino (http://www.nanode.eu http://www.arduino.cc ) a été retenue car celle-ci permet d’envoyer directement les données sur le site de Pachube et d’être mise en place facilement par tout le monde. Notre instrumentation avec ZigBee a été mise de côté pour l’instant car beaucoup plus couteuse et plus complexe à mettre au point. Nanode en kit est dispo à 25 euros. Des switch 8-ports 100mb sont dispo chez Amazon.fr pour 12 euros. Attention, Arduino IDE version Alpha 0022 est encore assez buggé. La version Arduino RC2 vient juste d’être dispo et nous allons la tester sous peu. C’est ce qui explique que les datafeed sur Pachube stoppent de temps en temps. Pour l’instant nous rebootons automatiquement les CPUs toutes les 4 heures en utilisant la fonction schedule du système IJENKO. On verra si les prochaines mises à jour des librairies EtherShield intégrées à l’IDE solutionnent ce bug. Pour l’instant les données sont envoyées sur Pachube toutes les 10 secondes. Nous passerons prochainement à 1 seconde puisque notre abonnement PRO nous permet 250 updates par seconde.

La méthode de mesure de l’injection au réseau fait appel à la technologie développée par Analog Devices utilisée dans les compteurs intelligents, notamment ADE7755, ADE7753, pour le monophasé. Il y a d’autres références pour le triphasé. Ces circuits permettent une précision de mesure de 0.1% sur une dynamique de signal de 500 à 1.

Nous utilisons les cartes Smart meter de Hoch (Chine)

http://hochgroup.en.alibaba.com/product/424588718-200841852/single_phase_electric_kilowatt_hour_ph_meter.html?tracelog=cgsotherproduct1

De même les circuits ADE7755 équipent les Smart Metering Power Plug que l’on trouve à 12 euros dans les grands supermarchés tels que Carrefour et Leclerc.

Il faut recupérer la sortie CF haute fréquence après opto-coupleur qui est lu par un Arduino/Nanode sur l’entrée D3 en mode d’interruption (avec une technique de mesure d’intervalle de précision). La sortie REVP après opto-coupleur est lu sur l’entrée D4 d’un Arduino pour obtenir le signe de la puissance mesurée (Production/Consommation).

Un dispositif avec ADE7753 en utilisant l’Energy Shield de http://www.olimex.cl (oui fabricant au Chili) sera mis en place prochainement sur notre site de test afin de mesurer les variations de la tension du réseau 230V CA (mesure RMS) et les données seront envoyées sur Pachube en temps réel. Le circuit ADE7755 est notamment utilisé dans la Smart Plug de INJENKO (voir l’offre Maitrise de l’Energie avec Bouygues Telecom BBOX bbox.ijenko.net).

Pour obtenir la Téléinfo de votre compteur EDF et l’envoyer sur Pachube, utiliser le Shield téléinfo2 de http://www.cartelectronic.fr/


---


## Pour récupérer les infos numériques de Pachube, voir l’exemple ci-dessous ##


http://api.pachube.com/v2/feeds/38281/datastreams/0.csv?start=2011-11-02T12:00:00+1&end=2011-11-02T17:59:00+1&interval=0&timezone=+1&per_page=1000&page=1

http://api.pachube.com/v2/feeds/38281/datastreams/0.csv?start=2011-11-02T12:00:00+1&end=2011-11-02T17:59:00+1&interval=0&timezone=+1&per_page=1000&page=2

http://api.pachube.com/v2/feeds/38281/datastreams/0.csv?start=2011-11-02T12:00:00+1&end=2011-11-02T17:59:00+1&interval=0&timezone=+1&per_page=1000&page=3


---


## Autres exemples de visualization des infos ##

https://api.pachube.com/v2/feeds/35020/datastreams/0.png?width=730&height=250&colour=%23f15a24&duration=30minutes&legend=watts&title=Skystream%20Etel%20-%20Real%20Time%20Power%20(30%20mn)&show_axis_labels=true&detailed_grid=true&scale=auto&min=0&max=3000&timezone=+1

https://api.pachube.com/v2/feeds/35020/datastreams/0.png?width=730&height=250&colour=%23f15a24&duration=1day&legend=watts&title=Skystream%20Etel%20-%20Real%20Time%20Power%20(24%20hours)&show_axis_labels=true&detailed_grid=true&scale=auto&min=0&max=3000&timezone=+1

https://api.pachube.com/v2/feeds/35020/datastreams/0.png?width=730&height=250&colour=%23f15a24&duration=7days&legend=watts&title=Skystream%20Etel%20-%20Real%20Time%20Power%20(7%20days)&show_axis_labels=true&detailed_grid=true&scale=auto&min=0&max=3000&timezone=+1

https://api.pachube.com/v2/feeds/35020/datastreams/0.png?width=730&height=250&colour=%23f15a24&duration=30days&legend=watts&title=Skystream%20Etel%20-%20Real%20Time%20Power%20(30%20days)&show_axis_labels=true&detailed_grid=true&scale=manual&min=0&max=3500&timezone=+1

https://api.pachube.com/v2/feeds/35020/datastreams/5.png?width=730&height=250&colour=%23f15a24&duration=6months&legend=kW&title=Skystream%20Etel%20-%20Daily%20Power%20(6%20months)&show_axis_labels=true&detailed_grid=true&scale=manual&min=0&max=50&timezone=+1

https://api.pachube.com/v2/feeds/35020/datastreams/6.png?width=730&height=250&colour=%23f15a24&duration=6months&legend=kW&title=Skystream%20Etel%20%E2%80%93%20Cumulated%20Daily%20Power%20(6%20months)&show_axis_labels=true&detailed_grid=true&%20scale=auto%20&timezone=+1