## Task 1 - Literature

### 1. Read the research article of the hands-on working group you are assigned to (see file “Student Groups.pdf” in shared folder General course material).

I have read "Human White Adipose Tissue Displays Selective Insulin Resistance in the Obese State.

---
### 2. Answer the following questions:

#### a. What is the medically relevant insight from the article?

The major finding from the study is that the overall insulin-induced transcriptional response in human white adipose tissue (WAT) is selective. Different insulin-regulated pathways are affected differently in obesity, and many of the changes can be reversed after weight loss after bariatric surgery.

#### b. Which genomics technology/ technologies were used?

The primary genomics technology used was 5’ Cap Analysis of Gene Expression (5’ CAGE sequencing). They then analysed the data by using differential expression analysis (generalized linear models), gene set enrichment analysis and genomic region set enrichment analyses (LOLA). They also included previously published ChIPseq and microarray data in their analyses. 

---
### 3. Further related research questions

#### a. List and explain at least three questions/ hypotheses you can think of that extend the analysis presented in the paper.

- xxx
- xxx
- xxx

#### b. [Optional] Devise a computational analysis strategy for (some of) the listed questions under 3a.

- xxx

---
## Task 2 - Git repositories and R Markdown

- I have made an account on Github, started a repository and a new project in that repository.
- All the documentation for Assignment 1 is in this formatted text document.
- During week 2 I will add all my hand-on work as R Markdown documents in the same repository.

---
## Task 3 - Introduction to R and online R course

- I have installed the latest version of R software (4.6.1).
- I had already prior to this course installed the most recent verison of RStudio Desktop (2026.10.0+233).
- I have installed the latest version of the Bioconductor package.
- I am very familiar with Tidyverse and ggplot2 since before this course - I will access them when necessary.
- I have used R many times before, as well as have some experience with R Markdown, but when I get uncertain about something I will look into the optional course as well as the R manuals and the R Markdown cheatsheet. 


---
## Task 4 - R basic operations

### 1. What is the square root of 10?
```r
10^(1/2)
```
Answer: 3.162278

---
### 2. What is the logarithm of 32 to the base 2?
```r
log2(32)
```
Answer: 5

---
### 3. What is the sum of the numbers from 1 to 1000?

```r
sum(1:1000)
```
Answer: 500500

---
### 4. What is the sum of all even numbers from 2 to 1000?
```r
sum(seq(2, 1000, by = 2))
```
Answer: 250500

---
### 5. How many pairwise comparisons are there for 100 genes?
```r
n <- 100
choose(n, 2)
```
Answer: 4950

---
### 6. And how many ways to arrange 100 genes in triples?
```r
n <- 100
choose(n, 3)
```
Answer: 161700

---
## Task 5 - Using R example datasets

### 1. Use the R internal CO2 dataset (“data(CO2)”).

```r
data(CO2)
```

---
### 2. Describe briefly the content of the CO2 dataset using the help function.
```r
help(CO2)
```

The dataset shows the data from an experiment on the cold tolerance of the grass species Echinocloa crus-galli.
The CO2 uptake of six plants from Quebec and six plants from Mississippi was measured at several levels of ambient 
CO2 concentration. Half the plants of each type were chilled overnight before the experiment was conducted.

The dataframe has 84 rows and 5 columns.
There are 7 measurements for every plant. 
In the column plant we see the plant ID:
  - Qn1:3 (Quebec nonchilled plant 1 to 3)
  - Qc1:3 (Quebec chilled plant 1 to 3)
  - Mn1:3 (Mississippi nonchilled plant 1 to 3)
  - Mc1:3 (Mississippi chilled plant 1 to 3)

In the column Type we see levels Quebec and Mississippi, telling us the origin of the plant.
In the column Treatment we see levels nonchilled and chilled
In the column conc we see numeric values of ambient carbon dioxide concentrations (mL/L).
  - The values are systematically ordered - for every plant there are the values 95, 175, 250, 350, 500, 675 and 1000.

In the column uptake we see numeric values of carbon dioxide uptake rates (μmol/m^2sec).

---
### 3. What is the average and median CO2 uptake of the plants from Quebec and Mississippi?
```r
Quebec <- subset(CO2, Type == "Quebec")
summary(Quebec$uptake)
```
Answer:
|Median|Mean|
|-|-|
|37.15|33.54|

The average CO2 uptake of the plants from Quebec is 33.54, while the median is 37.15.

```r
Mississippi <- subset(CO2, Type == "Mississippi")
summary(Mississippi$uptake)
```

Answer:
|Median|Mean|
|-|-|
|19.30|20.88|

The average CO2 uptake of the plants from Mississippi is 20.88, while the median is 19.30.

---
### 4. [Optional] In the “airway” example data from Bioconductor, how many genes are expressed in each sample? How many genes are not expressed in any sample?
```r
library(airway)
data(airway)
help(airway)
counts_mat <- assay(airway)
```
#### Genes expressed in each sample

```r
colSums(counts_mat > 0)
```
Answer:
|SRR1039508|SRR1039509|SRR1039512|SRR1039513|SRR1039516|SRR1039517|SRR1039520|SRR1039521|
|-|-|-|-|-|-|-|-|
|24633|24527|25699|23124|25508|25998|24662|23991|


#### Genes not expressed in any sample
```r
sum(rowSums(counts_mat) == 0)
```
Answer: 30208

---
## Task 6 - R Functions

### 1. Write a function that calculates the ratio of the mean and the median of a given vector.

```r
ratio_mean_median <- function(vector) { 
  return (mean(vector)/median(vector))
}
```
This function calculates the mean divided by the median, or the ratio of the mean and the median. 


---
### 2. Write a function that ignores the lowest and the highest value from a given vector and calculate the mean.

```r
trimmed_mean <- function(vector) { 
  sort_vector <- sort(vector)
  return (mean(sort_vector[2:(length(sort_vector) -1)]))
}
```
This functions sorts the vector, and then calculates the mean based on indices 2 and up to the second largest value. 

---
### 3. Read about piping from here:https://r4ds.had.co.nz/pipes.html#pipes (you don’t have to learn everything, a basic understanding of the usage is enough). Write a short (max. 300 characters, no spaces) explanation of why, how, and when not to use pipes.

Answer: ...

---
### 4. Familiarize yourself with the apply-family of functions (apply, lapply, sapply etc.) http://uc-r.github.io/apply_family Write a short explanation (max. 300 characters, no spaces) of why they could be useful in your work.

Answer: ...

---
## Task 7 - Basic visualization with R

### 1. Compare the distributions of the body heights of the two species from the 'magic_guys.csv' dataset graphically

```r
magic_guys <- read.csv(file.choose())
install.packages("ggplotify")
                 
library(ggplotify)
library(tidyverse)
library(patchwork)
```

#### a. using the basic 'hist' function as well as ‘ggplot’ and ‘geom_histogram’ functions from the ggplot2 package. Optimize the plots for example by trying several different 'breaks'. Note that ggplot2-based functions give you many more options for changing the visualization parameters, try some of them.

Basic 'hist' function:
```r
par(mfrow = c(1, 2))

art1_data <- subset(magic_guys, species == "jedi")
art2_data <- subset(magic_guys, species == "sith")

hist1 <- hist(art1_data$length, main = "Jedi", xlab = "Length", col = "skyblue")
hist2 <- hist(art2_data$length, main = "Sith", xlab = "Length", col = "salmon")

par(mfrow = c(1, 1))
```

ggplot2 version:
```r
gg_hist <- ggplot(magic_guys, aes(x=length, fill=species)) + 
  geom_histogram(alpha=0.5, position="identity", color="black")+
  facet_wrap(~ species) +
  labs(title="Distribution of length per species", x="Length", y="Frequency")+
  scale_fill_manual(values = c("jedi" = "skyblue", "sith" = "salmon")) +
  theme_minimal()
gg_hist
```

#### b. Do the same comparison as in a. but with boxplots. If you want to use the ggplot2-package, use the functions ‘ggplot’ and ‘geom_boxplot’.

Basic boxplot function:
```r
basic_box <- boxplot(length ~ species, data = magic_guys, 
        main = "Length per Species", xlab = "Species", ylab = "Length",
        col = c("skyblue", "salmon"))
```

ggplot2 version:
```r
gg_box <- ggplot(magic_guys, aes(x=species, y=length, fill=species)) + 
  geom_boxplot(alpha=0.5, color="black")+
  labs(title="Distribution of length per species", x="Species", y="Length")+
  scale_fill_manual(values = c("jedi" = "skyblue", "sith" = "salmon")) +
  theme_minimal()
gg_box
```


#### c. Save the plots with the ‘png’, ‘pdf’, and ‘svg’ formats. In which situation would you use which file format?

Save plot from basic 'hist' function:
```r
par(mfrow = c(1, 2))

art1_data <- subset(magic_guys, species == "jedi")
art2_data <- subset(magic_guys, species == "sith")

hist1 <- as.ggplot (function() hist(art1_data$length, main = "Jedi", xlab = "Length", col = "skyblue"))
hist2 <- as.ggplot (function() hist(art2_data$length, main = "Sith", xlab = "Length", col = "salmon"))

comb_hist <- hist1 + hist2

par(mfrow = c(1, 1))

ggsave("jedi_sith_histogram.png", plot = comb_hist, width = 10, height = 5)
ggsave("jedi_sith_histogram.pdf", plot = comb_hist, width = 10, height = 5)
ggsave("jedi_sith_histogram.svg", plot = comb_hist, width = 10, height = 5)
```

Save ggplot2 histogram:
```r
ggsave("ggplot2_histogram.png", plot = gg_hist, width = 10, height = 5)
ggsave("ggplot2_histogram.pdf", plot = gg_hist, width = 10, height = 5)
ggsave("ggplot2_histogram.svg", plot = gg_hist, width = 10, height = 5)
```

Save plot from basic boxplot function:
```r
ggsave("jedi_sith_boxplot.png", plot = basic_box, width = 10, height = 5)
ggsave("jedi_sith_boxplot.pdf", plot = basic_box, width = 10, height = 5)
ggsave("jedi_sith_boxplot.svg", plot = basic_box, width = 10, height = 5)
```

Save ggplot2 boxplot:
```r
ggsave("ggplot2_boxplot.png", plot = gg_box, width = 10, height = 5)
ggsave("ggplot2_boxplot.pdf", plot = gg_box, width = 10, height = 5)
ggsave("ggplot2_boxplot.svg", plot = gg_box, width = 10, height = 5)
```

Answer: I would use svg when I want to create a high-quality photo for web use, while pdf is better for printing. Both are vector format. Png can be used for both web use and printing, but one has to ensure that it is of good quality (raster format).  


---
### 2. Load the gene expression data matrix from the ‘microarray_data.tab’ dataset provided in the shared folder, it is a big tabular separated matrix.

```r
microarray <- read_tsv(file.choose())
```

#### a. How big is the matrix in terms of rows and columns?

```r
dim(microarray)
```
Answer: There are 551 rows and 1000 columns (genes).

#### b. Count the missing values per gene and visualize this result.

```r
missing_per_gene <- colSums(is.na(microarray))
missing_per_gene

missing_df <- data.frame(
  Gene = names(missing_per_gene),
  Missing = missing_per_gene
)
missing_df

ggplot(missing_df, aes(x = Missing)) +
  geom_histogram(binwidth = 1) +
  labs(
    title = "Distribution of missing values per gene",
    x = "Number of missing values",
    y = "Number of genes"
  ) +
  theme_bw()
```

#### c. Find the genes for which there are more than X% (X=10%, 20%, 50%) missing values.

X=10%:
```r
genes_over_10pct <- names(missing_per_gene[missing_per_gene > 0.10 * nrow(microarray)])
genes_over_10pct
```

X=20%:
```r
genes_over_20pct <- names(missing_per_gene[missing_per_gene > 0.20 * nrow(microarray)])
genes_over_20pct
```

X=50%:
```r
genes_over_50pct <- names(missing_per_gene[missing_per_gene > 0.50 * nrow(microarray)])
genes_over_50pct
```

Alternative method:
```r
percent_missing <- colSums(is.na(microarray)) / nrow(microarray) * 100
names(percent_missing[percent_missing > 10])
names(percent_missing[percent_missing > 20])
names(percent_missing[percent_missing > 50])
```

#### d. Replace the missing values by the average expression value for the particular gene. (Note: Imputing data has to be used with caution!)

```r
sum(is.na(microarray))
```
In total there are 115 826 NAs. To remove them I am using lapply to go over every value in a gene, calculate the mean and then replace the NAs with the mean for that specific gene. 

```r
microarray_imputed <- as.data.frame(
  lapply(microarray, function(x) {
    x[is.na(x)] <- mean(x, na.rm = TRUE)
    x
  })
)

sum(is.na(microarray_imputed))
```
Not all NAs were removed - 18734 remain. 

Finding error:
```r
which(colSums(!is.na(microarray)) == 0)
gene_means <- sapply(microarray, mean, na.rm = TRUE)
sum(is.nan(gene_means))
problem_genes <- names(gene_means[is.nan(gene_means)])
problem_genes
```
34 genes contained only missing values. These values are now removed before imputing. Below is the updated code to calculate the mean and replace the NAs with the mean for the specific gene the value belongs to, without the genes with only NA. 

```r
microarray_filtered <- microarray[, colSums(!is.na(microarray)) > 0]

microarray_imputed <- as.data.frame(
  lapply(microarray_filtered, function(x) {
    x[is.na(x)] <- mean(x, na.rm = TRUE)
    x
  })
)

sum(is.na(microarray_imputed))
```
Now, there are no NAs in the datafile. 

---
### 3. Visualize the data in the CO2 dataset in a way that gives you a deeper understanding of the data. What do you see?

```r
boxplot(uptake ~ Type,
        data = CO2,
        col = c("darkgreen", "orange"))


ggplot(CO2,
       aes(x = conc,
           y = uptake,
           color = Type,
           linetype = Treatment,
           group = interaction(Type, Treatment))) +
  stat_summary(fun = mean, geom = "line", linewidth = 1) +
  stat_summary(fun = mean, geom = "point", size = 2) +
  scale_color_manual(values = c(
    "Quebec" = "darkgreen",
    "Mississippi" = "orange")
  ) +
  labs(
    title = "Mean CO2 uptake across concentrations",
    x = "CO2 concentration",
    y = "Mean uptake"
  ) +
  theme_bw()



ggplot(CO2,
       aes(x = conc,
           y = uptake,
           group = Plant,
           color = Treatment)) +
  geom_line(alpha = 0.7) +
  geom_point(alpha = 0.7) +
  facet_wrap(~ Type) +
  scale_color_manual(values = c(
    "chilled" = "steelblue",
    "nonchilled" = "firebrick"
  )) +
  labs(
    title = "CO2 uptake for individual plants",
    x = "CO2 concentration",
    y = "CO2 uptake"
  ) +
  theme_bw()
```

The Quebec plants have a higher general CO2 uptake than the Mississippi plants (seen from mean, median and boxplot). In the interaction plot, we see that again, but also that the mean uptake of the chilled plants are lower than that of the non-chilled plants. The difference is larger between chilled and non-chilled plants from Mississippi. In the interaction plot it also looks like the Mississippi plants reach a plateau in CO2 uptake with the higher concentrations. The Quebec plants does not seem as if they have completely reached the plateau just yet at the highest measured CO2 concentration. Looking at the trajectories of the individual plants, coloured based on treatment, we can see that while the Mississippi plants separate clearly based on treatment, the same effect is not as obvious in the plants from Quebec, with one non-chilled plant reaching less CO2 uptake than one-two chilled plants for the majority of the measurements. Individual variation has a bigger effect in the Quebec plants - or the plants from Quebec seemes to be better at withstanding the cold so being chilled or not does not have a great effect on the CO2 uptake. 


---
## Task 8 - Basic visualization with R

### 1. Install the Tidybiology package, which includes the data ‘chromosome’ and ‘proteins’
devtools::install_github("hirscheylab/tidybiology")

#### a. Extract summary statistics (mean, median and maximum) for the following variables from the ‘chromosome’ data: variations, protein coding genes, and miRNAs. Utilize the tidyverse functions to make this as simply as possible.

```r
data(chromosome)

summary_stats <- chromosome %>%
  summarise(
    across(
      c(variations, protein_codinggenes, mi_rna),
      list(
        mean = mean,
        median = median,
        max = max
      )
    )
  )

summary_stats
```

Answer:
|variations_mean|variations_median|variations_max|protein_codinggenes_mean|protein_codinggenes_median|protein_codinggenes_max|mi_rna_mean|mi_rna_median|mi_rna_max|
|-|-|-|-|-|-|-|-|-|
|6484572|6172346|12945965|849.9583|836|2058|73.16667|75|134|

---
#### b. How does the chromosome size distribute? Plot a graph that helps to visualize this by using ggplot2 package functions.

```r
ggplot(chromosome, aes(x = length_mm)) +
  geom_histogram(color = "black", fill = "skyblue", bins = 15) +
  geom_vline(aes(xintercept = mean(length_mm)),
             color = "red",
             linewidth = 1) +
  theme_minimal()
```

Answer: The length varies between rougly 13-88mm, with a mean length around 45mm. There are no chromosomes in the data set with a length between roughly 70-80mm. 

---
#### c. Does the number of protein coding genes or miRNAs correlate with the length of the chromosome? Make two separate plots to visualize these relationships.

```r
cor.test(chromosome$length_mm,
         chromosome$protein_codinggenes,
         method = "pearson")

cor.test(chromosome$length_mm,
         chromosome$mi_rna,
         method = "pearson")


ggplot(chromosome,
       aes(x = length_mm,
           y = protein_codinggenes)) +
  geom_point(size = 3, alpha = 0.7) +
  geom_text(aes(label = id),
            vjust = -0.9,
            size = 3)+
  geom_smooth(method = "lm", se = TRUE, color = "red") +
  labs(
    title = "Protein-coding genes vs chromosome length",
    subtitle = "Pearson r = 0.61, p < 0.001",
    x = "Length in mm",
    y = "Number of protein coding genes"
  ) +
  theme_bw()


ggplot(chromosome,
       aes(x = length_mm,
           y = mi_rna)) +
  geom_point(size = 3, alpha = 0.7) +
  geom_text(aes(label = id),
            vjust = -0.9,
            size = 3)+
  geom_smooth(method = "lm", se = TRUE, color = "red") +  
  labs(
    title = "miRNAs vs chromosome length",
    subtitle = "Pearson r = 0.74, p < 0.001",
    x = "Length in mm",
    y = "Number of miRNAs"
  ) +
  theme_bw()
```

Answer: There is a correlation between length and number of miRNAs, and length and number of protein-coding genes, showing that longer genes tend to have more miRNAs and more protein-coding genes. The correlation with length is stronger for number of miRNAs than for number of protein-coding genes.

---
#### d. Calculate the same summary statistics for the ‘proteins’ data variables length and mass. Create a meaningful visualization of the relationship between these two variables by utilizing the ggplot2 package functions. Play with the colors, theme- and other visualization parameters to create a plot that pleases you.

```r
data(proteins)

stats_proteins <- proteins %>%
  summarise(
    across(
      c(length, mass),
      list(
        mean = mean,
        median = median,
        max = max
      )
    )
  )

stats_proteins


cor.test(proteins$length,
         proteins$mass,
         method = "pearson")

ggplot(proteins,
       aes(x = length,
           y = mass)) +
  geom_point(size = 3, alpha = 0.7) +
  geom_smooth(method = "lm", se = TRUE, color = "red") +  
  labs(
    title = "Protein mass vs length",
    subtitle = "Pearson r = 0.999, p < 0.001",
    x = "Protein length",
    y = "Protein mass"
  ) +
  theme_bw()
```

Answer: There is a very strong correlation between protein length and protein mass (Pearson r = 0.999, p < 0.001).

---
