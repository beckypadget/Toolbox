This code produces a plot of a continuous response with multiple categorical predictors. It has violins showing the data and pointranges showing the model predictions, as shown in the figure below. This code can be changed to add faceting, change colours etc to suit the needs of the plot.
## Template

🔔 Remember to import `ggplot2` and `dplyr` first.

```r
raw_data <- your_data %>%
  mutate(grouping_variable = your_group, response_variable = your_response)

summary_data <- raw_data %>%
  group_by(grouping_variable) %>%
  summarise(
    median_value = median(response_variable),
    lower_value = quantile(response_variable, 0.25),
    upper_value = quantile(response_variable, 0.75),
    .groups = "drop"
  )

plot_template <- ggplot() +
  geom_violin(data = raw_data, aes(x = grouping_variable, y = log(response_variable + 1),
    fill = grouping_variable), alpha = 0.15, color = NA) +
  geom_pointrange(data = summary_data, aes(x = grouping_variable, y = log(median_value + 1),
    col = grouping_variable, ymin = log(lower_value + 1), ymax = log(upper_value + 1)),
    show.legend = FALSE) +
  scale_color_manual(values = c("Group_1" = "#2a9d8f", "Group_2" = "#5f0f40",
    "Group_3" = "chocolate")) +
  scale_fill_manual(values = c("Group_1" = "#2a9d8f", "Group_2" = "#5f0f40",
    "Group_3" = "chocolate")) +
  labs(x = "Grouping variable", y = "log(Response variable + 1)") +
  theme_classic(base_size = 14) +
  theme(legend.position = "none")

plot_template
#ggsave("plot_template.png", plot = plot_template, width = 8, height = 5)
```


## An example using the iris dataset

```r
raw_data <- iris %>%
  mutate(grouping_variable = Species, response_variable = Sepal.Length)

summary_data <- raw_data %>%
  group_by(grouping_variable) %>%
  summarise(
    median_value = median(response_variable),
    lower_value = quantile(response_variable, 0.25),
    upper_value = quantile(response_variable, 0.75),
    .groups = "drop"
  )

species_order <- c("setosa", "virginica", "versicolor")
raw_data$grouping_variable <- factor(raw_data$grouping_variable, levels = species_order)
summary_data$grouping_variable <- factor(summary_data$grouping_variable, levels = species_order)

plot_template <- ggplot() +
  geom_violin(data = raw_data, aes(x = grouping_variable, y = log(response_variable + 1),
    fill = grouping_variable), alpha = 0.15, color = NA) +
  geom_pointrange(data = summary_data, aes(x = grouping_variable, y = log(median_value + 1),
    col = grouping_variable, ymin = log(lower_value + 1), ymax = log(upper_value + 1)),
    show.legend = FALSE) +
  scale_color_manual(values = c("setosa" = "#2a9d8f", "virginica" = "#5f0f40",
    "versicolor" = "chocolate")) +
  scale_fill_manual(values = c("setosa" = "#2a9d8f", "virginica" = "#5f0f40",
    "versicolor" = "chocolate")) +
  scale_x_discrete(limits = species_order) +
  labs(x = "Species", y = "log(Sepal Length + 1)") +
  theme_classic(base_size = 14) +
  theme(legend.position = "none")

plot_template
# ggsave("plot_template.png", plot = plot_template, width = 8, height = 5)
```

I used ChatGPT to convert my own code (which I developed with input from ChatGPT) into the template version and the iris dataset version (the text, including the gratuitous use of emojis, was written by me).