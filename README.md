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


## 6.GridPane 
The GridPane layout pane enables you to create a flexible grid of rows and columns in which to lay out nodes. Nodes can be placed in any cell in the grid and can span cells as needed. A grid pane is useful for creating forms or any layout that is organized in rows and columns.

![GridPane](https://docs.oracle.com/javafx/2/layout/img/grid.png "GridPane")

Example: Create a Grid Pane
```
public GridPane addGridPane() {
    GridPane grid = new GridPane();
    grid.setHgap(10);
    grid.setVgap(10);
    grid.setPadding(new Insets(0, 10, 0, 10));

    // Category in column 2, row 1
    Text category = new Text("Sales:");
    category.setFont(Font.font("Arial", FontWeight.BOLD, 20));
    grid.add(category, 1, 0); 

    // Title in column 3, row 1
    Text chartTitle = new Text("Current Year");
    chartTitle.setFont(Font.font("Arial", FontWeight.BOLD, 20));
    grid.add(chartTitle, 2, 0);

    // Subtitle in columns 2-3, row 2
    Text chartSubtitle = new Text("Goods and Services");
    grid.add(chartSubtitle, 1, 1, 2, 1);

    // House icon in column 1, rows 1-2
    ImageView imageHouse = new ImageView(
      new Image(LayoutSample.class.getResourceAsStream("graphics/house.png")));
    grid.add(imageHouse, 0, 0, 1, 2); 

    // Left label in column 1 (bottom), row 3
    Text goodsPercent = new Text("Goods\n80%");
    GridPane.setValignment(goodsPercent, VPos.BOTTOM);
    grid.add(goodsPercent, 0, 2); 

    // Chart in columns 2-3, row 3
    ImageView imageChart = new ImageView(
     new Image(LayoutSample.class.getResourceAsStream("graphics/piechart.png")));
    grid.add(imageChart, 1, 2, 2, 1); 

    // Right label in column 4 (top), row 3
    Text servicesPercent = new Text("Services\n20%");
    GridPane.setValignment(servicesPercent, VPos.TOP);
    grid.add(servicesPercent, 3, 2);

    return grid;
}
```


## 7.FlowPane 
The nodes within a FlowPane layout pane are laid out consecutively and wrap at the boundary set for the pane. Nodes can flow vertically (in columns) or horizontally (in rows). 

![FlowPane](https://docs.oracle.com/javafx/2/layout/img/flow.png "FlowPane")

Example: Create a Flow Pane
```
public FlowPane addFlowPane() {
    FlowPane flow = new FlowPane();
    flow.setPadding(new Insets(5, 0, 5, 0));
    flow.setVgap(4);
    flow.setHgap(4);
    flow.setPrefWrapLength(170); // preferred width allows for two columns
    flow.setStyle("-fx-background-color: DAE6F3;");

    ImageView pages[] = new ImageView[8];
    for (int i=0; i<8; i++) {
        pages[i] = new ImageView(
            new Image(LayoutSample.class.getResourceAsStream(
            "graphics/chart_"+(i+1)+".png")));
        flow.getChildren().add(pages[i]);
    }

    return flow;
}
```


## 8.TilePane 

A tile pane is similar to a flow pane. The TilePane layout pane places all of the nodes in a grid in which each cell, or tile, is the same size.

Example: Create a Tile Pane
```
TilePane tile = new TilePane();
tile.setPadding(new Insets(5, 0, 5, 0));
tile.setVgap(4);
tile.setHgap(4);
tile.setPrefColumns(2);
tile.setStyle("-fx-background-color: DAE6F3;");

ImageView pages[] = new ImageView[8];
for (int i=0; i<8; i++) {
     pages[i] = new ImageView(
        new Image(LayoutSample.class.getResourceAsStream(
        "graphics/chart_"+(i+1)+".png")));
     tile.getChildren().add(pages[i]);
}
```


## 9.AnchorPane

The AnchorPane layout pane enables you to anchor nodes to the top, bottom, left side, right side, or center of the pane. As the window is resized, the nodes maintain their position relative to their anchor point. Nodes can be anchored to more than one position and more than one node can be anchored to the same position. 

![AnchorPane](https://docs.oracle.com/javafx/2/layout/img/anchor.png "AnchorPane")

Example: Create an Anchor Pane
```
public AnchorPane addAnchorPane(GridPane grid) {
    AnchorPane anchorpane = new AnchorPane();
    Button buttonSave = new Button("Save");
    Button buttonCancel = new Button("Cancel");

    HBox hb = new HBox();
    hb.setPadding(new Insets(0, 10, 10, 10));
    hb.setSpacing(10);
    hb.getChildren().addAll(buttonSave, buttonCancel);

    anchorpane.getChildren().addAll(grid,hb);   // Add grid from Example 1-5
    AnchorPane.setBottomAnchor(hb, 8.0);
    AnchorPane.setRightAnchor(hb, 5.0);
    AnchorPane.setTopAnchor(grid, 10.0);

    return anchorpane;
}
```


Final layout:
![AnchorPane2](https://docs.oracle.com/javafx/2/layout/img/anchor_in_border_big.png "AnchorPane")
