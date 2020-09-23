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

Example: Create a Pane

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
border.setTop(hbox);        // adds the HBox pane to the top region of the border pane. 
border.setLeft(addVBox());
addStackPane(hbox);         // Add stack to HBox in top region

border.setCenter(addGridPane());
border.setRight(addFlowPane());
```

## 3.HBox
The HBox layout pane provides an easy way for arranging a series of nodes in a single row.

![HBox](https://docs.oracle.com/javafx/2/layout/img/hbox.png "HBox")

Example: Create a HBox

```
public HBox addHBox() {
    HBox hbox = new HBox();
    hbox.setPadding(new Insets(15, 12, 15, 12));
    hbox.setSpacing(10);
    hbox.setStyle("-fx-background-color: #336699;");

    Button buttonCurrent = new Button("Current");
    buttonCurrent.setPrefSize(100, 20);

    Button buttonProjected = new Button("Projected");
    buttonProjected.setPrefSize(100, 20);
    hbox.getChildren().addAll(buttonCurrent, buttonProjected);

    return hbox;
}
```

## 4.VBox
The VBox layout pane is similar to the HBox layout pane, except that the nodes are arranged in a single column. Figure 1-4 shows an example of a VBox pane.

![VBox](https://docs.oracle.com/javafx/2/layout/img/vbox.png "VBox")

Example: Create a VBox Pane
```
public VBox addVBox(); {
    VBox vbox = new VBox();
    vbox.setPadding(new Insets(10));
    vbox.setSpacing(8);

    Text title = new Text("Data");
    title.setFont(Font.font("Arial", FontWeight.BOLD, 14));
    vbox.getChildren().add(title);

    Hyperlink options[] = new Hyperlink[] {
        new Hyperlink("Sales"),
        new Hyperlink("Marketing"),
        new Hyperlink("Distribution"),
        new Hyperlink("Costs")};

    for (int i=0; i<4; i++) {
        VBox.setMargin(options[i], new Insets(0, 0, 0, 8));
        vbox.getChildren().add(options[i]);
    }

    return vbox;
}
```

## 5.StackPane
The StackPane layout pane places all of the nodes within a single stack with each new node added on top of the previous node. This layout model provides an easy way to overlay text on a shape or image or to overlap common shapes to create a complex shape.

![StackPane](https://docs.oracle.com/javafx/2/layout/img/stack.png "StackPane")

Example: Create a StackPane
```
public void addStackPane(HBox hb) {
    StackPane stack = new StackPane();
    Rectangle helpIcon = new Rectangle(30.0, 25.0);
    helpIcon.setFill(new LinearGradient(0,0,0,1, true, CycleMethod.NO_CYCLE,
        new Stop[]{
        new Stop(0,Color.web("#4977A3")),
        new Stop(0.5, Color.web("#B0C6DA")),
        new Stop(1,Color.web("#9CB6CF")),}));
    helpIcon.setStroke(Color.web("#D0E6FA"));
    helpIcon.setArcHeight(3.5);
    helpIcon.setArcWidth(3.5);

    Text helpText = new Text("?");
    helpText.setFont(Font.font("Verdana", FontWeight.BOLD, 18));
    helpText.setFill(Color.WHITE);
    helpText.setStroke(Color.web("#7080A0")); 

    stack.getChildren().addAll(helpIcon, helpText);
    stack.setAlignment(Pos.CENTER_RIGHT);     // Right-justify nodes in stack
    StackPane.setMargin(helpText, new Insets(0, 10, 0, 0)); // Center "?"

    hb.getChildren().add(stack);            // Add to HBox from Example 1-2
    HBox.setHgrow(stack, Priority.ALWAYS);    // Give stack any extra space
}
```
![StackPane2](https://docs.oracle.com/javafx/2/layout/img/hbox_stack.png "StackPane2")

## 6.VBoxGridPane 
## 7.VBoxFlowPane 
## 8.VBoxTilePane 
## 9.VBoxAnchorPane
