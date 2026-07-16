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

0.	[00_building_your_analysis_file.Rmd](https://github.com/MDRCNY/Sequences_to_Success/blob/main/code/00_building_your_analysis_file.Rmd) – creating analysis file from state longitudinal data
1.	[01_data_prep_and_visualization.Rmd](https://github.com/MDRCNY/Sequences_to_Success/blob/main/code/01_data_prep_and_visualization.Rmd) — data structure, descriptive summaries, and visualizations
2.	[02_sequence_analysis.Rmd](https://github.com/MDRCNY/Sequences_to_Success/blob/main/code/02_sequence_analysis.Rmd) — defining sequences and computing distances using TraMineR
3.	[03_cluster_analysis.Rmd](https://github.com/MDRCNY/Sequences_to_Success/blob/main/code/03_cluster_analysis.Rmd) — clustering sequences and interpreting pathway groups

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
