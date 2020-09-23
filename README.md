# JavaFX-notes
## Layout
```
  java.lang.Object
    javafx.scene.Node
      javafx.scene.Parent
        javafx.scene.layout.Region
          javafx.scene.layout.Pane
```

### 1.Pane
`public class Pane extends Region`

Base class for layout panes which need to expose the children list as public so that users of the subclass can freely add/remove children.
