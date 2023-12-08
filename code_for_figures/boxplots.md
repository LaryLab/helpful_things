# Some R code for making boxplots the way Jennifer made them for the beta blocker pharmacogenetics project  

Note: this is not meant to show every step I took when making this particular plot. I haven't shown my reading in of the data, making sure multiple files had similar formats and merging them together. I have shown the packages I used and the creation of the dataframe I used for plotting. Then I also show the plotting code itself and how I saved it.  

In this example I am plotting the raw (de-identified) percent changes in bmd or ctx measured at a particular site in response to taking a beta-blocking drug (or placebo) for 20 weeks.

```r
#load in necessary libraries
library(dplyr)
library(ggplot2)
```

Now read in the data and prepare it for plotting. I had to make the formats of multiple dataframes agree, merge them together, and calculate a few measurements necessary for the boxplot (these steps will be different for every different project).

In the next code block, I trim down the dataframe into the columns I need for the plot, including filtering for the treatments I want to include.

```r
#create the dataframe used in the plot from a larger dataframe with way more info
#select out the columns needed and filter for the treatments that were significant (and therefore that we want to plot)  
adrb2_rs1042717 <- adrb2_pheno %>% 
  select(FID, percent_change_spine, allele_freq_rs1042717, treat) %>% 
  filter(treat %in% c("A", "N", "P80", "Pl"))
```

The ggplot2 command (below) takes the dataframe containing the information and column names for each of the variables we are plotting. Here I have an allele frequency along the x axis, percent change down the y axis, and the boxes will be filled with colors according to which treatment they represent. I've commented at the end of each line about what its purpose is.

```r
#plot for rs1042717
adrb2_rs1042717_boxplot <- ggplot(adrb2_rs1042717, aes(x = allele_freq_rs1042717, y = percent_change_spine, fill = treat)) +
  geom_boxplot(outlier.shape = NA) + #boxplots will show outlier points by default. I've taken these off because I've added dots to the plots also and they would be redundant
  geom_jitter(position = position_jitterdodge(jitter.width = 0.08)) + #this is how I added the dots. They need to have the position_jitterdodge part in order to line up with the boxes correctly
  ggtitle("ADRB2 - rs1042717 - Lumbar Spine") + #specify the title of the whole plot (can be easily removed later for publication
  ylab("Percent Change") + xlab("Allele Frequency (rs1042717)") + #specify the axis titles
  theme_classic() + #removes the gray background that is the default in ggplot2 and adds axis lines instead
  scale_fill_manual(name = "Treatment", #change the legend title
                    values = c("skyblue1", "royalblue", "forestgreen", "gray87"), #pick the colors we want for the plot
                    labels = c("Atenolol", "Nebivolol", "Propranolol 80", "Placebo")) #change the categories in the legend
```

Now we can visualize the plot to make sure it looks the way we want.

```r
adrb2_rs1042717_boxplot
```

And if it does, this is how I save them. I specified the width and height because it was really squashed at first.

```r
ggsave('pharmacogenetics/results/boxplots/adrb2_rs1042717_totalbody_aten_nebiv_prop80.png', plot = adrb2_rs1042717_boxplot, device = png, width = 7, height = 5)
```

## Variations  

If you want to make a more minimal plot without the dots:  

```r
#plot for rs1042717
adrb2_rs1042717_boxplot <- ggplot(adrb2_rs1042717, aes(x = allele_freq_rs1042717, y = percent_change_spine, fill = treat)) +
  geom_boxplot() + 
  ggtitle("ADRB2 - rs1042717 - Lumbar Spine") + #specify the title of the whole plot (can be easily removed later for publication
  ylab("Percent Change") + xlab("Allele Frequency (rs1042717)") + #specify the axis titles
  theme_classic() + #removes the gray background that is the default in ggplot2 and adds axis lines instead
  scale_fill_manual(name = "Treatment", #change the legend title
                    values = c("skyblue1", "royalblue", "forestgreen", "gray87"), #pick the colors we want for the plot
                    labels = c("Atenolol", "Nebivolol", "Propranolol 80", "Placebo")) #change the categories in the legend
```

If you want to make a plot in which you have control over the colors of the fill and the colors of the lines:

```r
#plot for rs1042717
adrb2_rs1042717_boxplot <- ggplot(adrb2_rs1042717, aes(x = allele_freq_rs1042717, y = percent_change_spine, fill = treat, color = treat)) +
  geom_boxplot(outlier.shape = NA) + #boxplots will show outlier points by default. I've taken these off because I've added dots to the plots also and they would be redundant
  geom_jitter(position = position_jitterdodge(jitter.width = 0.08)) + #this is how I added the dots. They need to have the position_jitterdodge part in order to line up with the boxes correctly
  ggtitle("ADRB2 - rs1042717 - Lumbar Spine") + #specify the title of the whole plot (can be easily removed later for publication
  ylab("Percent Change") + xlab("Allele Frequency (rs1042717)") + #specify the axis titles
  theme_classic() + #removes the gray background that is the default in ggplot2 and adds axis lines instead
  scale_fill_manual(name = "Treatment", #change the legend title
                    values = c("skyblue1", "royalblue", "forestgreen", "gray87"), #pick the colors we want for the plot
                    labels = c("Atenolol", "Nebivolol", "Propranolol 80", "Placebo")) + #change the categories in the legend
  scale_color_manual(values = c("skyblue3", "royalblue4", "darkgreen", "gray63"), #pick the colors we want for the outlines of each box and for the dots
                     guide = "none")
```

If you want to make the axis and legend text/titles larger:

```r
adrb2_rs1042717_boxplot <- ggplot(adrb2_rs1042717, aes(x = allele_freq_rs1042717, y = percent_change_spine, fill = treat)) +
  geom_boxplot(outlier.shape = NA) + #boxplots will show outlier points by default. I've taken these off because I've added dots to the plots also and they would be redundant
  geom_jitter(position = position_jitterdodge(jitter.width = 0.08)) + #this is how I added the dots. They need to have the position_jitterdodge part in order to line up with the boxes correctly
  ggtitle("ADRB2 - rs1042717 - Lumbar Spine") + #specify the title of the whole plot (can be easily removed later for publication
  ylab("Percent Change") + xlab("Allele Frequency (rs1042717)") + #specify the axis titles
  theme(panel.grid.major = element_blank(), #theme.classic() is a good shortcut if you want to use the defaults, but it doesn't allow for customization
        panel.grid.minor = element_blank(), panel.background = element_blank(), #I still like to remove the gray background, so that's what these first parts are doing
        axis.line = element_line(colour = "black"), axis.title.y = element_text(size = 20), #with the normal theme, we can edit all the sizes of the text individually
        axis.title.x = element_text(size = 20), axis.text = element_text(size = 14),
        legend.title = element_text(size = 16), legend.text = element_text(size = 14)) +
  scale_fill_manual(name = "Treatment", #change the legend title
                    values = c("skyblue1", "royalblue", "forestgreen", "gray87"), #pick the colors we want for the plot
                    labels = c("Atenolol", "Nebivolol", "Propranolol 80", "Placebo")) #change the categories in the legend
```

If you want to put multiple plots together:  

```r
library(ggpubr)

all_plots <- ggarrange(adrb1_rs12414657_ultradist_boxplot, hdac4_spine_boxplot, adrb1_rs1801253_boxplot, hdac4_ctx_boxplot,
                       labels = c("A", "C", "B", "D"),
                       ncol = 2, nrow = 2, align = "hv", font.label = list(size = 20))
```
