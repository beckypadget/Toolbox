Sometimes we want to make lots of plots and annotate them with something but we don't necessarily know the dimensions of the plots. In this case, we can tell ggplot to put the text in the top right corner, with a little offset.

* x, y, = Inf tells it that it's the top right corner
* hjust, vjust = tell it to bring it inwards slightly in both directions

```
annotate("text", 
               x = Inf, y = Inf, 
               hjust=1.1,
               vjust=1.1,
               label = "your_label")
```