# Workshop Point & Click 2D

## Introduction

Durant cet atelier, on va découvrir Unity et voir comment créer un jeu point and click en 2D

---

## Setup

- Pour commencer, il faut avoir installé Unity version **2019.4.20.**
- Maintenant vous pouvez créer un projet 2D, en ajoutant le chemin et un titre par exemple *workshopPointAndClick.*
- Une fois que vous avez créé un projet, on va télécharger quelques assets
    - En haut à gauche, Assets → Import Package → Custom Package et importez le **Workshop-point-and-click-setup.unitypakage** veillez à avoir toutes les cases cochez lors de l’import.
- Bravo, vous avec réussi à setup le projet. Passons en revue ce que vous venez de télécharger
    
    
    ![files.png](Workshop%20Point%20&%20Click%202D/files.png)
    
    - Inventory: les textures pour l’UI de l’inventaire
    - Items: les PNG des items à intégrer dans l’inventaire
    - MuchoPixels: Les éléments de la map
    - Scène: les Scènes du jeu, vous pouvez double clic sur BasicScene
    - Scripts:
        - Inventoty: le système d’inventaire avec des méthodes pour ajouter, supprimer des éléments et les déclarer
        - UI: le système d’UI, avec les dialogues et l’inventaire
        - Player: le joueur, un composant qui contient une UI et un inventaire
    
    ![scene.png](Workshop%20Point%20&%20Click%202D/scene.png)
    
    - La scène contient :
        - Main Caméra: une caméra fixe sur notre map
        - Canvas, si vous avez fait le workshop sur les menus vous savez déjà comment ça fonctionne. On à deux composants, un pour les dialogues et l‘autre pour l’inventaire
        - ItemAssets, un script qui lie un PNG à un enum
        - Grid: très pratique pour la 2d, ça représente notre map
    
    ---
    
    ## Step 1
    
    Maintenant qu’on à passer en revue les composants on peut commencer à créer un jeu et les premiers game event
    
    Pour commencer, 
    
    - Créez un **gameObject** vide en l’appelant *GameEvent* par exemple, il contiendra toutes nos futures interactions
    - Pour plus de clarté, on va découper les évents en fonction des pièces ou ils prennent place, ajoutez dans *GameEvent* un **GameObject** *Garage*
    - On peut maintenant ajouter des composants dans notre garage,
    
    ![garage.png](Workshop%20Point%20&%20Click%202D/garage.png)
    
    - Créez un **GameObject** dans le garage en l’appelant B*ox* ou tous autres objets qui vous inspirent. Ajouter lui un composant **Box Collider2D** et positionné le autour de votre objet. Vous pouvez également **Edit Collider** afin de le redimensionner. Il s’agit de la zone dans laquelle on va cliquer pour lancer un évent
    - Ajoutez un script à votre composant, deux fonctions sont normalement générées
        - Start, appelé une fois, lors de l’initialisation de notre composant.
        - Update, appelé à chaque frame, vous pouvez la supprimée
    
    Vous pouvez déclarer deux variables
    
    ```cpp
    /*
    dialogueUI représente notre dialogueBox dans le Canvas,
    il contient une méthode ShowDialogue(string dialogue)
    qui fait défiler ... un dialogue, pas simple à devinez
    */
    
    [SerializeField] private DialogueUI dialogueUI;
    
    /* 
    player permet d'accéder à l'inventaire et son UI
    */
    
    [SerializeField] private Player player;
    ```
    
    Puis, ajoutez une méthode qui est appelé lors du clique sur un box collider, 
    
    ```csharp
    void MaMéthode() { /* A remplacer par La méthode que vous avez trouvé */
        player.inventory.AddItem(
    			// vous pouvez ajouter un Fusible ou un autre type
    			// présent dans l'enum ItemType de Script/Inventory/Item.cs
    			// Mais, seuls les fusibles sont stackable, voir IsStackble()
    			new Item { itemType = Item.ItemType.Fusible, amount = 1 }
    		);
    		dialogueUI.ShowDialogue("Votre Dialogue");
    }
    ```
    
    N’oubliez pas d’ajoutez vos composants
    
    ![BoxEvent.png](Workshop%20Point%20&%20Click%202D/BoxEvent.png)
    
    Vous pouvez maintenant appuyer sur **play** et cliquer sur votre objet, vous devriez voir apparaitre votre dialogue et l’objet que vous avez choisi d’ajouter dans votre inventaire. 
    
    Par défaut c’est un fusible, pour fermer le dialogue appuyé sur **espace**
    
    ---
    
    ## Step 2
    
    Une boite qui contient des fusibles à l’infini n’est pas très réaliste, créez deux comportements si la boite est vide ou pleine, avec deux dialogues distincts. 
    
    N’hésiter pas essayer de changer le type d’objet ou à rajouter les vôtres
    
    La prochaine étape c’est de se servir de l’objet que vous venez de trouver
    
    Avec ces deux fonctions, vous pouvez détecter les objets dans l’inventaire 
    
    ```csharp
    public bool IsTypePresent(Item.ItemType itemType)
    public bool IsEnoughTypePresent(Item.ItemType itemType, int amount)
    ```
    
    Et vous pouvez en supprimer avec 
    
    ```cpp
    public void RemoveItem(Item item)
    ```
    
    Maintenant, crée un **GameEvent** qui vous convient
    
    Par exemple, réparer l’ordinateur avec un fusible, ouvrir l’armoire avec une clé, créez différents dialogues si vous avec l’objet, s’il vous le manque, etc.
    
    ---
    
    ## Step 3
    
    Vous savez tous ce dont vous avez besoin pour créer un jeu, essayer de multiplier les **GameEvent** dans différentes pièces de la maison.
    
    Avec au moins 4 GameEvent différents, 3 items et pourquoi pas une fin en trouvant les clés de la voiture, le mot de passe de l’ordinateur ou autre.
    
    ---
    
     
    
    ## Pour aller plus loin
    
    Vous avez un jeu, avec des interactions, un système de dialogue, et d’inventaire.
    
    Pourquoi ne pas rajouter un système pour lire des notes à ramasser, ou visualiser l’ordinateur afin de transmettre une histoire.