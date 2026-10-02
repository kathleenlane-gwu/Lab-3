# Lab-3

## Project Structure - what you will be cloning

```text
Lab-3/
├── README.md
├── R6854-Lab3
  ├── renv.lock      
  ├── 6854Lab3.qmd
  ├── messy_samples.csv
  ├── messy_sequences.fasta
├── Comparison.md
└── AI_USAGE.md
```

## Necessary Tools/Downloads for Repository
* Terminal
* Rstudio -- https://posit.co/products/open-source/rstudio
* Renv -- install.packages("renv") in RStudio Console

## Getting Started
Open the terminal on your computer and copy/paste the code below into the terminal. The `cd ~/Desktop` command tells the computer to work within your Desktop folder and will clone the repo there. The `git clone` command will clone the `Lab-3` repository using the GitHub URL. Then `cd Lab-3` enters the repository, and `ls` lets you view the files in the repo. You should see the same files from the project structure above.
```
cd ~/Desktop
git clone https://github.com/kathleenlane-gwu/Lab-3.git
cd Lab-3
ls 
```
## Analysis
To run `6854Lab3.qmd`, you must first recreate the necessary environment. Open RStudio and copy/paste the following code into the R console. We are setting `R6854-Lab3` as our working directory and initializing renv.  
```
setwd("~/Desktop/Lab-3/R6854-Lab3/")
renv::init()
```
`renv::init()` will create four options to choose from. Choose the first option, "Restore the project from the lockfile" by entering '1' into the console. Then run the following in the R console.
```
source("6854Lab3.qmd")
```
