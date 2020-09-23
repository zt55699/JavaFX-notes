# JavaFX-Layout
```
  java.lang.Object
    javafx.scene.Node
      javafx.scene.Parent
        javafx.scene.layout.Region
          javafx.scene.layout.Pane
```

## 1.Pane

`public class Pane extends Region`

Base class for layout panes which need to expose the children list as public so that users of the subclass can freely add/remove children.

```
  Pane canvas = new Pane();
  canvas.setStyle("-fx-background-color: black;");
  canvas.setPrefSize(200,200);
  Circle circle = new Circle(50,Color.BLUE);
  circle.relocate(20, 20);
  Rectangle rectangle = new Rectangle(100,100,Color.RED);
  rectangle.relocate(70,70);
  canvas.getChildren().addAll(circle,rectangle);
```

## 2.BorderPane
The BorderPane layout pane provides five regions in which to place nodes: top, bottom, left, right, and center. If your application does not need one of the regions, you do not need to define it and no space is allocated for it.

![BorderPane](https://docs.oracle.com/javafx/2/layout/img/border.png "BorderPane")

Example: Create a Border Pane

```
BorderPane border = new BorderPane();
HBox hbox = addHBox()
border.setTop(hbox);
border.setLeft(addVBox());
addStackPane(hbox);         // Add stack to HBox in top region

border.setCenter(addGridPane());
border.setRight(addFlowPane());
```
