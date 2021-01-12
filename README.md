# TP4 : Renforcement de la politique de mots de passe d'un poste Windows autonome
## Configuration de la stratégie de sécurité locale sous Windows professionnel

## Classe : B3B
## Élèves : Emma Durand **[@emmadrd912](https://github.com/emmadrd912)** et Pierre Ceberio **[@PierreYnov](https://github.com/PierreYnov)** 

![](https://pic.clubic.com/v1/images/1832371/raw?fit=max&width=1200&hash=be1b2baf832bc191629d1930f884f59b720ce2fd)

# Sommaire 

- [Le Lab](#le-lab)


appliquer bonne pratique creation et gestion mdp pour compte user local windows
pas sur un poste AD
ceci peut etre fait sur un controleur de domaine, et propager via gpo

a la fin on aura une strategie de mdp efficace, rendant impossible le cassage de mdp online


## Le lab



# 3.1 Audit des comptes utilisateurs locaux 

Depuis une session admin local, et avec les commande NET intégrer à windows :

    
    - lister precisemment les compter user sur le poste compter user sur le poste compter user sur le poste
    - indiquer le role de chaque user
    - identifier ceux qui ont des privilege admin sur la machine
    - quels sont les groupes locaux config par default sur un poste windows ? preciser ce qui necessite une attentation spéciale et justifiez la rép
    - lister les user de ces groupes particuliers
    - créer un user standard ( membre uniquement du groupe utilisateurs) avec la NET command
    - configurer un mdp pour cet user
    - ouvrer une session avec ce compte pour verifier le bon fonctionnement des manip
    - repartir sur la session admin local puis avec la commande NET, verrouiller le compte créé
    - check qu'il est impossible de se connecter à cet ancien compte




# 3.2 Application d'une stratégie locale de mots de passes :

Rappeller quelles sont les caracteritisque recommandé d'un mdp robuste

    - tapez gpedit.msc depuis un local admin local sur un cmd

dans la partie haute " Config ordinateur "

    - parcourir les parametre









































