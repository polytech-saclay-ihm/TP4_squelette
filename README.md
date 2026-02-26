Programmation Java @ Et3 \
Polytech Paris-Saclay | 2025-26

# TP4

L'objectif de ce TP est de réaliser un éditeur graphique minimal en suivant le pattern MVC (Modèle-Vue-Contrôleur). Cet éditeur permet de dessiner des formes géométriques (des ellipses, des rectangles ou des lignes), de les déplacer, les supprimer, les dupliquer, et d'en changer la couleur.

<br><div align="center"><img src="images/interface.jpg" width="500"></img></div><br>

1. Clonez ce projet et configurez votre IDE de la même manière que le TP1, en suivant les instructions sur https://github.com/polytech-ihm-et3/HowToUseJavaFxWithIDE. Pour l'instant, le dossier _src_ contient le code minimal pour afficher une fenêtre vierge à partir d'un fichier fxml.

2. Créez une interface la plus proche possible de la figure ci-dessus avec _SceneBuilder_, en modifiant le fichier _src/main/resources/application/interface.fxml_. Vous pouvez vous aider des éléments suivants :
   -   des [_Label_](https://openjfx.io/javadoc/21/javafx.controls/javafx/scene/control/Label.html) pour décrire certaines parties de l'interface.
   -   des [_RadioButton_](https://openjfx.io/javadoc/21/javafx.controls/javafx/scene/control/RadioButton.html) correspondant à différentes commandes de l'éditeur : (1) "_Select / Move_", (2) "_Ellipse_", (3) "_Rectangle_" et (4) "_Line_". Puisque l'on souhaite qu'un seul de ces boutons puisse être sélectionné à la fois, on peut leur attribuer le même [_ToggleGroup_](https://openjfx.io/javadoc/21/javafx.controls/javafx/scene/control/ToggleGroup.html) directement depuis SceneBuilder, dans l'inspecteur (section _Properties_).
   -   des [_Separator_](https://openjfx.io/javadoc/21/javafx.controls/javafx/scene/control/Separator.html) pour structurer l'interface.
   -   un [_ColorPicker_](https://openjfx.io/javadoc/21/javafx.controls/javafx/scene/control/ColorPicker.html) permettant de sélectionner une couleur dans une palette.
   -   des [_Button_](https://openjfx.io/javadoc/21/javafx.controls/javafx/scene/control/Button.html) correspondant à différentes commandes de l'éditeur : (a) "_Delete_" et (b) "_Clone_".
   -   un [_AnchorPane_](https://openjfx.io/javadoc/21/javafx.graphics/javafx/scene/layout/AnchorPane.html) servant de canevas, qui sera la zone de dessin.

3. On souhaite utiliser le pattern MVC (Modèle-Vue-Contrôleur) pour structurer l'application, qui ne contiendrait qu'une seule vue.

    Un fichier fxml a besoin d'un contrôleur pour le lier à une classe en Java (à ne pas confondre avec le contrôleur du pattern MVC. Le même mot est utilisé pour deux notions différentes).

    Dans notre cas, on peut donc considérer la vue (du MVC) comme étant le contrôleur (fxml).

    Créez une vue (le contrôleur fxml), un contrôleur et un modèle minimaux, et connectez-les dans le fichier _Main.java_. Pour lier le contrôleur à la vue et utiliser la vue pour gérer le fxml, vous pouvez vous inspirer du code suivant :

> ```Java
> //On crée le modèle (MVC)
> Model modele = new Model();
> //On crée le contrôleur (MVC)
> Controller controlleur = new Controller(modele);
> //On crée la vue (MVC)
> View vue = new View(controlleur);
> //On prépare le fichier FXML en définissant son controlleur comme étant la vue (MVC).
> FXMLLoader loader = new FXMLLoader(getClass().getResource("interface.fxml"));
> loader.setController(vue);
> //On charge le fichier FXML, il appellera la méthode *initialize()* de la vue (MVC)
> Parent root = loader.load();
> //On crée la scène
> Scene scene = new Scene(root);
> //On définit cette scène comme étant la scène de notre première fenêtre
> primaryStage.setScene(scene);
> //On rend cette fenêtre visible
> primaryStage.show();
> ```

4. Faites en sorte que, en ayant préalablement sélectionné un des [_RadioButton_](https://openjfx.io/javadoc/21/javafx.controls/javafx/scene/control/RadioButton.html), l'utilisateur puisse :

    - (a) Créer une [_Ellipse_](https://openjfx.io/javadoc/21/javafx.graphics/javafx/scene/shape/Ellipse.html). En cliquant n'importe où sur le canevas, une [_Ellipse_](https://openjfx.io/javadoc/21/javafx.graphics/javafx/scene/shape/Ellipse.html) avec une taille pré-configurée se crée. Cette [_Ellipse_](https://openjfx.io/javadoc/21/javafx.graphics/javafx/scene/shape/Ellipse.html) devra être de la couleur actuellement sélectionnée dans le [_ColorPicker_](https://openjfx.io/javadoc/21/javafx.controls/javafx/scene/control/ColorPicker.html), pour cela, vous pourrez utiliser la méthode [`setFill(Paint value)`](<https://openjfx.io/javadoc/21/javafx.graphics/javafx/scene/shape/Shape.html#setFill(javafx.scene.paint.Paint)>).

    - (b) Créer un [_Rectangle_](https://openjfx.io/javadoc/21/javafx.graphics/javafx/scene/shape/Rectangle.html) similairement à la manière de créer une [_Ellipse_](https://openjfx.io/javadoc/21/javafx.graphics/javafx/scene/shape/Ellipse.html).

    - (c) Créer une [_Line_](https://openjfx.io/javadoc/21/javafx.graphics/javafx/scene/shape/Line.html) similairement à la manière de créer un rectangle. Plutôt que d'utiliser la méthode [`setFill(Paint value)`](<https://openjfx.io/javadoc/21/javafx.graphics/javafx/scene/shape/Shape.html#setFill(javafx.scene.paint.Paint)>), vous pourrez utiliser la méthode [`setStroke(Paint value)`](<https://openjfx.io/javadoc/21/javafx.graphics/javafx/scene/shape/Shape.html#setStroke(javafx.scene.paint.Paint)>).

    - (d) Sélectionner une figure en cliquant dessus. Il faudra alors donner à l'utilisateur un retour validant la sélection de la figure (par exemple, grossir la figure, changer son contour, la faire clignoter, ...).

    - (e) Déplacer une figure grâce à un "_drag & drop_" ("_glisser & déposer_"). L'utilisateur devra éventuellement sélectionner la figure au préalable.

5. Faites en sorte que les [_Button_](https://openjfx.io/javadoc/21/javafx.controls/javafx/scene/control/Button.html) (a) "_Delete_" et (b) "_Clone_" soient grisés par défaut. Ces [_Button_](https://openjfx.io/javadoc/21/javafx.controls/javafx/scene/control/Button.html) ne pourront être accessible que si une figure est déjà sélectionnée par l'utilisateur.

6. Si une figure (_cf_ [_Shape_](https://openjfx.io/javadoc/21/javafx.graphics/javafx/scene/shape/Shape.html)) est préalablement sélectionnée par l'utilisateur. Faites en sorte que :

    - (a) en sélectionnant une nouvelle couleur dans le [_ColorPicker_](https://openjfx.io/javadoc/21/javafx.controls/javafx/scene/control/ColorPicker.html), la couleur de la figure change, en accord avec cette nouvelle couleur.

    - (b) en cliquant sur le bouton "_Delete_", la figure soit supprimée du canevas.

    - (c) en cliquant sur le bouton "_Clone_", une nouvelle figure, identique à celle sélectionnée soit créée et ajoutée au canevas, avec un léger décalage par rapport à la position de la première figure.

7. Modifiez votre code pour que l'utilisateur puisse choisir les dimensions d'une [_Ellipse_](https://openjfx.io/javadoc/21/javafx.graphics/javafx/scene/shape/Ellipse.html), d'un [_Rectangle_](https://openjfx.io/javadoc/21/javafx.graphics/javafx/scene/shape/Rectangle.html) ou d'une [_Line_](https://openjfx.io/javadoc/21/javafx.graphics/javafx/scene/shape/Line.html) au moment de la créer grâce à un "_drag & drop_" ("_glisser & déposer_") sur le canevas.

8. Bonus : Améliorez votre éditeur en y rajoutant des fonctionnalités de la liste ci-dessous ou de votre choix. 

    Quelques exemples :
   - Spécifier et de modifier le contour (stroke) des figures.
   - Montrer sous forme d'un champ de texte éditable la position de la figure pour la positionner plus précisément qu'à la souris.
   - Modifier la taille d'une figure sélectionnée après sa création avec des poignées.
   - Revenir en arrière afin d'annuler la toute dernière action.
   - Sauvegarder le contenu du canevas et le restaurer.
   - ...