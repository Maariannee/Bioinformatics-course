## Task 1 - Literature

1. Read the research article of the hands-on working group you are assigned to (see file “Student Groups.pdf” in shared folder General course material).

I have read "Human White Adipose Tissue Displays Selective Insulin Resistance in the Obese State.

---
2. Answer the following questions:

a. What is the medically relevant insight from the article?

The major finding from the study is that the overall insulin-induced transcriptional response in human white adipose tissue (WAT) is selective. Different insulin-regulated pathways are affected differently in obesity, and many of the changes can be reversed after weight loss after bariatric surgery.

b. Which genomics technology/ technologies were used?

The primary genomics technology used was 5’ Cap Analysis of Gene Expression (5’ CAGE sequencing). They then analysed the data by using differential expression analysis (generalized linear models), gene set enrichment analysis and genomic region set enrichment analyses (LOLA). They also included previously published ChIPseq and microarray data in their analyses. 

---
3. Further related research questions

a. List and explain at least three questions/ hypotheses you can think of that extend the analysis presented in the paper.

- xxx
- xxx
- xxx

b. [Optional] Devise a computational analysis strategy for (some of) the listed questions under 3a.

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
Answer:
500500

---
### 4. What is the sum of all even numbers from 2 to 1000?
```r
sum(seq(2, 1000, by = 2))
```
Answer:
250500

---
### 5. How many pairwise comparisons are there for 100 genes?
```r
n <- 100
choose(n, 2)
```
Answer:
4950

---
### 6. And how many ways to arrange 100 genes in triples?
```r
n <- 100
choose(n, 3)
```
Answer:
161700

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
