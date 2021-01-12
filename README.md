# TP4 : Renforcement de la politique de mots de passe d'un poste Windows autonome
## Configuration de la stratégie de sécurité locale sous Windows professionnel

## Classe : B3B
## Élèves : Emma Durand **[@emmadrd912](https://github.com/emmadrd912)** et Pierre Ceberio **[@PierreYnov](https://github.com/PierreYnov)** 

![](https://pic.clubic.com/v1/images/1832371/raw?fit=max&width=1200&hash=be1b2baf832bc191629d1930f884f59b720ce2fd)

# Sommaire 

- [Le Lab](#le-lab)
- [Audit des comptes utilisateurs locaux](#audit-des-comptes-utilisateurs-locaux)
- [Application d'une stratégie locale de mots de passe](#application-dune-strat%C3%A9gie-locale-de-mots-de-passe)



## Le lab

- 1 machine avec Windows 10 Professionnel

## Audit des comptes utilisateurs locaux 


On liste les comptes présents sur la machine avec la commande ``net user``

![](img/list_user.png)

L'utilisateur **Emma** a le rôle ``Administrateur``.

L'autre a le rôle ``Invité``.

L'utilisateur **Emma** a donc les privilèges administrateurs.

Les groupes sont visibles avec la commande ``net localgroup``

![](img/list_group.png)

Ceux avec des commandes administrateurs nécessitent une attention particulière, donc ceux ci-dessous:

- Administrateurs
- Administrateurs Hyper-V
- System Managed Accounts Group
- Utilisateurs de gestion à distance
- Propriétaires d'appareils

Pour lister les utilisateurs de ces groupes on tape la commande ``net local group nom_du_groupe``

Utilisateurs du groupe **Administrateurs** : Emma, Administrateur

Utilisateurs du groupe **Administrateurs Hyper-V** : 

Utilisateurs du groupe **System Managed Accounts Group** : 
DefaultAccount

Utilisateurs du groupe **Utilisateurs de gestion à distance** : 

Utilisateurs du groupe **Propriétaires d'appareils** : 

On crée l'utilisateur **pierre** qui sera uniquement membre du groupe ``Utilisateurs`` avec la commande :

``net user pierre root /add`` 

Il est bien dans ``Utilisateurs`` :

![](img/net_user.png)


Et pas dans ``Administrateurs`` :

![](img/localgroup_verif.png)

On passe sur le compte **pierre**

![](img/pierre.png)

On rentre le mot de passe, les animations de premières connexions Windows 10 s'animent puis nous pouvons vérifier que tout est bon :

![](img/pierre2.png)

On se déconnecte et on repasse sur le compte Administrateur, puis on tape la commande ``net user pierre /ACTIVE:NO``

On rentre le mot de passe, le compte est bien désactivé :

![](img/lock_pierre.png)

## Application d'une stratégie locale de mots de passe

**Rappeler quelles sont les caractéristiques recommandées d'un mot de passe robuste**

    
Le mot de passe doit respecter ces conditions :

- Suffisamment long (> 10 caractères)

- Composé de caractères variés (chiffre, majuscule, minuscule, ponctuation ...)

- N'est pas présent dans un dictionnaire ou n'est pas une phrase connue

- En lien avec votre identité

**Tapez gpedit.msc depuis un local admin local sur un cmd et dans la partie haute " Config ordinateur "**



    - Parcourir les paramètres et s'assurer que le poste est configuré pour refuser l'ouverture de session pour des user avec un mot de passe vide. sinon modifier et justifier la réponse
    
Le paramètre se trouve dans ``Configuration de l’ordinateur\Paramètres Windows\Paramètres de sécurité\Stratégies locales\Options de sécurité`` et il est bien activé donc c'est déjà bien paramétré : 

![](https://i.gyazo.com/98774e2f02b1e361a6d32d873b295956.png)

Le paramètre doit être activé. Un mot de passe vide est une menace pour la sécurité. 

    - appliquer la stratégie de mot de passe suivant :
        - longueur min : 10 caractères
        - le mot de passe doit respecter des exigences de complexité
        - durée de vie maximum du mot de passe : 6 mois
        - Le système de gestion des mots de passe ne doit pas utiliser un algorithme de chiffrement réversible pour le stockage du mot de passe.

On va dans ``Configuration de l’ordinateur\Paramètres Windows\Paramètres de sécurité\Stratégies de comptes\Stratégies de mot de passe\`` puis dans Longueur minimale du mot de passe, on passe le paramètre à 10 :

![](https://i.gyazo.com/9629803c2cb8351c278ade1a72bdffb3.png)

![](https://i.gyazo.com/1e8db0f625fde0ea540c1618811da760.png)

![](https://i.gyazo.com/e00ebd58f0e83c4ab96d9f27e2931b5d.png)

![](https://i.gyazo.com/97a31b74aeecd29e71416d94e6e5ac35.png)


    - appliquez également la stratégie de verrouillage de compte, afin de limiter les chances de succès d'attaques sur les mot de passe :
        - Le système doit verrouiller un compte pendant 15 minutes après 5 tentatives de connexions infructueuses en moins 5 minutes.

On va dans ``Configuration de l’ordinateur\Paramètres Windows\Paramètres de sécurité\Stratégies de comptes\Stratégies de verrouillage du compte\``

![](https://i.gyazo.com/6ee6b0477022eb9ca547302fe91794d4.png)

![](https://i.gyazo.com/c1199fa766e34bbd12910e73bc85e0fa.png)

![](https://i.gyazo.com/49a535b6f9f017a717deb508e321c11f.png)

**On vérifie les modifications**

Avec un faible mot de passe : 

![](https://i.gyazo.com/f2a1f024ae3e2163880eb04469ae7734.png)

Avec un mot de passe long, mais pas complexe :

![](https://i.gyazo.com/32a4a89b84ebb42239ff8032d0c7f3c0.png)

Avec un mot de passe complexe, ça marche :

![](https://i.gyazo.com/b8745b226cd164c9a68acf10ed69d09c.png)


On remarque que la stratégie s'est bien appliquée.

- Tentative de connexions infructueuses :

![](https://i.gyazo.com/25f4c8312d0e379ccd8bf8d5817bfc1f.png)

Notre stratégie s'est bien appliquée, au bout de 5 tentatives de connexion, le compte s'est verrouillé.































