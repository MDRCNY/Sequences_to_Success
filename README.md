# Sequences to Success in Washington State Project Code Repository

This GitHub repository accompanies the **Sequences to Success in Washington State** project, a collaborative effort between MDRC and the Washington Student Achievement Council (WSAC) that mapped the school-to-work trajectories of nearly 64,000 students who graduated from Washington State high schools in 2017.  This repository provides open-source tools for studying postsecondary to workforce pathways using state longitudinal data. It is designed to help researchers and program administrators apply sequence analysis and cluster analysis to administrative data. These methods treat the full trajectory of a student or participant as the unit of analysis, rather than focusing on outcomes at a single point in time.

The repository includes three R Markdown modules that walk through the complete workflow from data preparation to pathway analysis and a synthetic dataset for hands-on practice. Users should navigate the modules in order, as each builds on the one before it. The repository also includes a “Module 0” for users who would like to transform their own longitudinal data into a format that can be easily used in the sequence analysis. This module is optional for users who will be working through modules 1 – 3 using the synthetic data. 

This repository is intended for data users who are comfortable with R and interested in learning or applying sequence and cluster analysis methods. No prior experience with these methods is required.

## Benefits of Sequence Analysis

A **sequence** is an ordered record of the states a person moves through over time. In the context of this project, each student has a sequence that captures whether they were enrolled in college, working, both, or neither at each point in a 28-quarter observation window. Rather than summarizing a student's experience with a single outcome measure, a sequence preserves the full trajectory, including when transitions happened, how long a student spent in each state, and the order in which states occurred.

**Sequence analysis** is a set of methods for describing, visualizing, and comparing these trajectories. It allows researchers to quantify how similar or different two students' pathways are and to visualize how the distribution of states across a cohort changes over time. 

**Cluster analysis** is then used to group students with similar sequences together into pathway clusters. Because the number of unique sequences in a large dataset can be enormous, clustering makes the results interpretable by reducing thousands of individual trajectories into a manageable number of meaningful pathway groups that can be named, described, and compared.

Traditional outcome analyses ask whether students reached a destination (e.g., did they earn a credential? Were they employed?). Sequence analysis paired with cluster analysis asks a different question: what path did they take to get to their outcome, and how does that path relate to their outcomes? Together, these methods allow researchers to:

* Describe the full range of pathways that students follow, including non-linear routes
* Identify groups of students who followed similar trajectories
* Examine how pathway participation varies by student demographics
* Connect pathway groups to downstream outcomes such as wages and employment stability

# Overview of the Sequences to Success in Washington State Repository Structure
The folders and files in this repository are numbered to indicate the suggested order of use. If you are new to this repository, start with the **How to Use This Repo** section below before opening any code files.

### Module 0 - Building Your Analysis File
* **00_building_your_analysis_file.Rmd** — This module is intended for researchers who want to apply the sequence and cluster analysis workflow to their own state longitudinal data. It walks through the process of transforming raw enrollment and wage records into the combined state sequence file used in Modules 1, 2, and 3. The module covers four key methodological decisions: defining the quarterly time spine, handling concurrent enrollment, combining enrollment and employment into a single state, and treating missing records as neither enrolled nor employed. For each decision, the module explains the approach taken in the Sequences to Success in WA State project and the reasoning behind it, and flags alternative approaches for researchers whose data or research questions differ. The module concludes with a set of recommended data checks to run before proceeding to the analysis modules. **Users working with the synthetic “toy” dataset provided in this repository can skip this module.**

### Module 1 - Data Preparation and Visualization
* **01_data_prep_and_visualization.Rmd** — Introduces the structure of the synthetic dataset; walks through data loading and inspection; and produces descriptive summaries of demographics, postsecondary enrollment patterns, credential attainment, and labor market outcomes. Uses **ggplot2** (part of the tidyverse) for data visualization and **kableExtra** for formatted tables. Start here before moving to the sequence analysis module.

### Module 2 - Sequence Analysis
* **02_sequence_analysis.Rmd** — Introduces sequence analysis using the **TraMineR** package (Gabadinho et al., 2011), which provides tools for defining, visualizing, and comparing longitudinal sequences. Covers how to define and visualize sequences, how to choose and compute pairwise distance measures including Optimal Matching, and how to interpret sequence visualizations such as index plots and state distribution plots. Uses **ggridges** for ridge plots showing the distribution of sequence entropy across the cohort. Saves the distance matrix and sequence object for use in Module 3.

### Module 3 - Cluster Analysis
* **03_cluster_analysis.Rmd** — Builds on the distance matrix from Module 2 to group students with similar trajectories into pathway clusters using hierarchical clustering. Uses the cluster package for hierarchical clustering with Ward linkage and the **WeightedCluster** package for computing cluster quality statistics such as ASW, CH, and R2 to help select the number of clusters. Covers how to visualize and label clusters and how to examine how pathway participation and outcomes vary across clusters and demographic groups.

# How to Use This Repository
This repository contains three R Markdown modules and a folder of synthetic data files. The modules are designed to be run in order, and each one builds on the previous, but experienced users may find it useful to jump directly to a specific module.

### Getting the Files
**If you are familiar with GitHub**, you can clone this repository to your local machine using:

```
git clone https://github.com/[repo-url].git

```

**If you are new to GitHub**, the easiest way to access the files is to download them directly:
1.	Click the green **Code** button near the top right of this page
2.	Select **Download ZIP**
3.	Unzip the downloaded folder to a location on your computer

### Setting Up Your R Environment
Once you have the files, open RStudio and set your working directory to the folder where you saved the repository files. The GitHub repository includes a folder called longitudinal_toy_data/ that contains all of the data files you will need. As long as you do not move or rename any of the files or folders, the code will be able to find them automatically and you won't need to change any file paths.

Each module lists the R packages it requires at the top. If you are missing any, you can install them by running `install.packages("package_name")` in your RStudio console.

### Running the Modules

Open and run the modules in order:
0.	00_building_your_analysis_file.Rmd – creating analysis file from state longitudinal data
1.	01_data_prep_and_visualization.Rmd — data structure, descriptive summaries, and visualizations
2.	02_sequence_analysis.Rmd — defining sequences and computing distances using TraMineR
3.	03_cluster_analysis.Rmd — clustering sequences and interpreting pathway groups

To run a module, open the .Rmd file in RStudio and click **Knit** to render the full document, or run individual code chunks using the green play button on each chunk.

### Frequently Asked Questions and Troubleshooting

#### Why am I getting a "file not found" error?
This is almost always a working directory issue. Make sure your working directory is set to the top-level repository folder and that you have not moved or renamed any files or folders. See the "Setting Up Your R Environment" section above for instructions on setting your working directory. You can check your current working directory at any time by running getwd() in your RStudio console.

#### Why am I getting a "there is no package called X" error?
You need to install the package before you can load it. Run `install.packages("package_name")` in your RStudio console, replacing package_name with the name of the missing package. Each module lists the packages it requires at the top. If you are starting fresh, you can install all of them at once by running `install.packages(c("tidyverse", "TraMineR", "cluster", "WeightedCluster", "scales", "knitr", "kableExtra"))`.

#### Why does my output look different from the examples in the module?
If you are using the toy dataset, small differences may be due to random variation in the data generation process. If you are working with your own state data, differences are expected. The toy dataset is synthetic, and the patterns are illustrative only.

#### Why is my sequence object showing unexpected states or missing states?
This is often caused by a mismatch between the state labels in your data and the alphabet argument in `seqdef()`. Make sure the values in your combined state columns exactly match the states defined in your STATES vector, including capitalization and underscores. You can check the unique values in your data by running `unique(unlist(combined_wide[, seq_cols]))`.

#### Why is my cluster dendrogram taking a long time to compute?
Computing pairwise distances for large datasets is computationally intensive. With 5,000 students and 28 quarters, expect the distance matrix computation to take several minutes. If you are working with a larger dataset, consider running the distance computation on a subset of students first to check your code before running the full analysis.

#### Why are some of my clusters very small or very large?
Very small clusters (fewer than 2-3% of students) may indicate that your chosen value of k is too large and is splitting a coherent group into fragments. Very large clusters (more than 30-40% of students) may indicate that k is too small and is merging meaningfully different groups together. See Section 8 of Module 3 for guidance on choosing and evaluating different values of k.

# About the Synthetic Dataset
The synthetic dataset is fully synthetic and was generated for teaching and methods demonstration only. It does not reflect any real state, institution, or individual. All pathway proportions, earnings figures, and employment rates are illustrative. The dataset simulates a cohort of **5,000** students from a fictional state who graduated high school in 2016. It tracks their postsecondary enrollment over **14** terms (7 academic years) and their quarterly wages and employment over **24** quarters (through 2022). 

Students are assigned to one of **12 fictional pathway archetypes** ranging from no postsecondary enrollment to nonlinear transfer pathways, with demographic characteristics (race/ethnicity, FRPL status, rural/urban location, first-generation status) influencing pathway sorting and wage outcomes in realistic ways.

The data files listed in the table below are included in the longitudinal_toy_data/ folder for your use.

| File | Description |
|----------|----------|
| students.csv    | One row per student; demographic characteristics including race/ethnicity, sex, FRPL status, rural flag, first-generation status, IEP flag, and ELL flag    |
| hs_records.csv    | One row per student; high school GPA, diploma type, FRPL status, and dual credit participation flag    |
| enrollment_long.csv    | One row per student × term; enrollment status each term (CTC, 4YR, or None)    |
| enrollment_wide.csv    | One row per student; enrollment status pivoted to wide format with one column per term    |
| credentials.csv    | One row per credential earned; credential type (Certificate, Associate's, or Bachelor's) and term of completion    |
| wage_records_long.csv    | One row per student × quarter; quarterly wages and employment indicator    |
| wage_records_wide.csv    | One row per student; quarterly wages pivoted to wide format    |
| employ_wide.csv    | One row per student; employment indicator pivoted to wide format    |
| combined_seq_long.csv    | One row per student × term; combined enrollment + employment state (e.g., CTC_Work, 4YR_NoWork, Work_Only, Neither)    |
| combined_seq_wide.csv    | One row per student; combined states pivoted to wide format; this is the primary input for sequence analysis in Modules 2 and 3    |
| analysis_flat.csv    | One row per student; demographics, high school record, credential summary, and aggregate labor market outcomes merged into a single analysis-ready file    |

# Acknowledgements
We are grateful to the Washington State Education Research and Data Center (ERDC) for generously providing access to the data that made this research possible. Additionally, this work would not have been possible without the work and contributions of the following people:

Dani Fumia, ERDC<br>
KC Deane, WSAC<br>
Sufiyan Syed, MDRC<br>
Annabel Utz, MDRC<br>
Rebekah O’Donoghue, MDRC<br>
Joshua Vermette, MDRC<br>
Ashley Alvarez, MDRC<br>
Richard Dorsett<br> 
Homar Maurás-Rodríguez<br>
Dan Oliver, WSAC<br>
Isaac Kwakye, WSAC<br>
Richard Hendra, MDRC<br>
John Hutchins, MDRC<br>

For questions about the code or repository materials, please contact brit.henderson@mdrc.org





