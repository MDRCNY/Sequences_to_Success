# Sequences to Success in Washington State Project Code Repository

This GitHub repository accompanies the [**Sequences to Success in Washington State**](https://www.mdrc.org/work/projects/sequences-success-washington-state) project, a collaborative effort between MDRC and the Washington Student Achievement Council (WSAC) that mapped the school-to-work trajectories of nearly 64,000 students who graduated from Washington state high schools in 2017.  This repository provides open-source tools for studying pathways young people take after high school using state longitudinal data. It is designed to help researchers and program administrators apply sequence analysis and cluster analysis to administrative data. These methods analyze each student or participant’s full trajectory rather than focusing on outcomes at a single point in time.

The repository includes three R Markdown modules that walk through the complete workflow from data preparation to pathway analysis, along with a synthetic dataset for hands-on practice. Users should work through the modules in order, as each builds on the one before it. The repository also includes a “Module 0” for users who would like to transform their own longitudinal data into a format that can be easily used in the sequence analysis. This module is optional for users who will be working through Modules 1, 2, and 3 using the synthetic data. 

This repository is intended for data users who are comfortable with R and interested in learning or applying sequence and cluster analysis methods. No previous experience with these methods is required.

## Benefits of Sequence Analysis

A **sequence** is an ordered record of the states a person moves through over time. In the context of this project, all students have sequences that capture whether they were enrolled in college, working, both, or neither at each point in a 28-quarter observation window. Rather than summarizing a student's experience with a single outcome measure, a sequence preserves the full trajectory, including when transitions happened, how long a student spent in each state, and the order in which states occurred.

**Sequence analysis** is a set of methods for describing, visualizing, and comparing these trajectories. It allows researchers to quantify how similar or different two students' pathways are and to represent visually how the distribution of states across a cohort changes over time. 

**Cluster analysis** is then used to group students with similar sequences together into pathway clusters. Because the number of unique sequences in a large dataset can be enormous, clustering makes the results interpretable by reducing thousands of individual trajectories into a manageable number of meaningful pathway groups that can be named, described, and compared.

Traditional outcome analyses ask whether students reached a destination (for example, did they earn a credential? were they employed?). Sequence analysis paired with cluster analysis asks a different question: what path did they take to get to their outcomes and how do their paths relate to their outcomes? Together, these methods allow researchers to:

* Describe the full range of pathways that students follow, including nonlinear routes
* Identify groups of students who followed similar trajectories
* Examine how pathway participation varies by student demographics
* Connect pathway groups to downstream outcomes such as wages and employment stability

# Overview of the Sequences to Success in Washington State Repository Structure
The folders and files in this repository are numbered to indicate the suggested order of use. If you are new to this repository, start with the [**How to Use This Repo**](https://github.com/MDRCNY/Sequences_to_Success/blob/main/how_to_use_this_repository.md) section before opening any code files.

### Module 0 - Building Your Analysis File
* [**00_building_your_analysis_file.Rmd**](https://github.com/MDRCNY/Sequences_to_Success/blob/main/code/00_building_your_analysis_file.Rmd): This module is intended for researchers who want to apply the sequence and cluster analysis workflow to their own state longitudinal data. It walks through the process of transforming raw enrollment and wage records into the combined state sequence file used in Modules 1, 2, and 3. The module covers four methodological decisions: defining the quarterly observation window (the consistent set of time periods onto which each student's enrollment and employment records are mapped, also called a “time spine”), handling concurrent enrollment, combining enrollment and employment into a single state, and treating missing records as neither enrolled nor employed. For each decision, the module explains the approach taken in the Sequences to Success in Washington State project and the reasoning behind it, and suggests alternative approaches for researchers whose data or research questions differ. The module concludes with a set of recommended data checks to run before proceeding to the analysis modules. **Users working with the synthetic “toy” dataset provided in this repository can skip this module.**

### Module 1 - Data Preparation and Visualization
* [**01_data_prep_and_visualization.Rmd**](https://github.com/MDRCNY/Sequences_to_Success/blob/main/code/01_data_prep_and_visualization.Rmd): This module introduces the structure of the synthetic dataset; walks through data loading and inspection; and produces descriptive summaries of demographics, postsecondary enrollment patterns, credential attainment, and labor market outcomes. Uses **ggplot2** (part of the tidyverse) for data visualization and **kableExtra** for formatted tables. Start here before moving to the sequence analysis module.

### Module 2 - Sequence Analysis
* [**02_sequence_analysis.Rmd**](https://github.com/MDRCNY/Sequences_to_Success/blob/main/code/02_sequence_analysis.Rmd): This module introduces sequence analysis using the **TraMineR** package (Gabadinho et al., 2011), which provides tools for defining, visualizing, and comparing longitudinal sequences[^1]. Covers how to define sequences and represent them visually, how to choose and compute pairwise distance measures including optimal matching, and how to interpret sequence visualizations such as index plots and state distribution plots. Uses **ggridges** for ridge plots showing the distribution of sequence entropy across the cohort. Sequence entropy is a measure of how varied or complex each student’s pathway is over time, where higher values indicate more frequent transitions between states. Saves two outputs for use in Module 3: the distance matrix, which is a table of pairwise similarity scores that quantify how different each student’s pathway is from every other student’s, and the sequence object, which is the data structure TraMineR uses to store and analyze the sequences. 

[^1]: Alexis Gabadinho, Gilbert Ritschard, Nicolas S. Müller, and Matthias Studer. 2011. “Analyzing and Visualizing State Sequences in R with TraMineR.” *Journal of Statistical Software* 40, 4: 1–37.

### Module 3 - Cluster Analysis
* [**03_cluster_analysis.Rmd**](https://github.com/MDRCNY/Sequences_to_Success/blob/main/code/03_cluster_analysis.Rmd): Builds on the distance matrix from Module 2 to group students with similar trajectories into pathway clusters using hierarchical clustering. Hierarchical clustering works by starting with all students in separate group and then progressively merging the most similar groups together, one step at a time, until all students belong to a single cluster. This process produces a treelike diagram called a dendrogram that shows the order in which groups were merged and how different they were at the point of merging. Researchers then "cut" the dendrogram at a chosen level to produce a specific number of clusters. For example, cutting at 12 clusters produces 12 pathway groups. Ward linkage, the specific variant of hierarchical clustering used here, merges groups in a way that minimizes the total variation within each cluster, which tends to produce compact, evenly sized groups that are easier to interpret. The module uses the **cluster** package for hierarchical clustering and the **WeightedCluster** package for computing cluster quality statistics to aid the user in selecting the number of clusters. These statistics include the Average Silhouette Width (ASW), which measures how well each student fits the assigned cluster compared with the next best alternative; the Calinski-Harabasz index (CH), which captures the ratio of between-cluster to within-cluster variation; and R-squared (R2), which represents the proportion of total variation explained by the cluster solution. Higher values indicate better fit for all three measures. Covers how to represent clusters visually and label them, and how to examine how pathway participation and outcomes vary across clusters and demographic groups.

# About the Synthetic Dataset
The synthetic dataset is fully synthetic and was generated only for the purposes of teaching and demonstrating methods. It does not reflect any real state, institution, or individual. All pathway proportions, earnings figures, and employment rates are illustrative.

The dataset simulates a cohort of **5,000** who graduated high school in 2016 in a fictional state. It tracks their postsecondary enrollment over **14** terms (7 academic years) and their quarterly wages and employment over **24** quarters (through 2022). 

Students are assigned to one of **12 fictional pathway archetypes** ranging from no postsecondary enrollment to nonlinear transfer pathways, with demographic characteristics (race/ethnicity, free or reduced-price lunch status, rural/urban location, first-generation status) influencing pathway sorting and wage outcomes in realistic ways.

The data files listed in the table below are included in the longitudinal_toy_data/ folder for your use.

| File | Description |
|----------|----------|
| students.csv    | One row per student; student background characteristics of race/ethnicity, sex, free or reduced-price lunch status, rural flag, first-generation status, Individualized Education Program flag, and English Language Learner flag    |
| hs_records.csv    | One row per student; high school GPA, diploma type, free or reduced-price lunch status, and dual-credit-participation flag    |
| enrollment_long.csv    | One row per student per term; enrollment status each term (community or technical college, four-year college or university, or none)    |
| enrollment_wide.csv    | One row per student; enrollment status pivoted to wide format with one column per term    |
| credentials.csv    | One row per credential earned; credential type (certificate, associate's, or bachelor's) and term of completion    |
| wage_records_long.csv    | One row per student per quarter; quarterly wages and employment indicator    |
| wage_records_wide.csv    | One row per student; quarterly wages pivoted to wide format    |
| employ_wide.csv    | One row per student; employment indicator pivoted to wide format    |
| combined_seq_long.csv    | One row per student per term; combined enrollment and employment state (for example, community or technical college and work [CTC_Work], four-year institution and no work [4YR_NoWork], Work_Only, Neither)    |
| combined_seq_wide.csv    | One row per student; combined states pivoted to wide format; this is the primary input for sequence analysis in Modules 2 and 3    |
| analysis_flat.csv    | One row per student; demographics, high school record, credential summary, and aggregate labor market outcomes merged into a single, analysis-ready file    |

# Acknowledgements
We are grateful to the Washington State Education Research and Data Center (ERDC) for generously providing access to the data that made this research possible.
Additionally, this work would not have been possible without the work and contributions of the following people:

Dani Fumia, ERDC<br>
KC Deane, WSAC<br>
Sufiyan Syed, MDRC<br>
Annabel Utz, MDRC<br>
Rebekah O’Donoghue, MDRC<br>
Joshua Vermette, MDRC<br>
Ashley Alvarez, MDRC<br>
Richard Dorsett, University of Westminster<br> 
Homar Maurás Rodríguez, WSAC<br>
Dan Oliver, WSAC<br>
Isaac Kwakye, WSAC<br>
Richard Hendra, MDRC<br>
John Hutchins, MDRC<br>

For questions about the code or repository materials, please contact SequencesWA@mdrc.org

<p align="center">
  <img src="MDRC_Logo.png" width="225" height="300">
  <img src="WSAC.LOGO.Rectangle.png" width="550" height="150">
</p>



