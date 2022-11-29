# DHEP Project Template

This is a comprehensive template repository for empirical projects with the DHEP group. This allows us to leverage a shared set of settings and organization to make collaboration easy. It also facilitates the use of Reproducible Analytical Pipelines (RAPs), which automate analytical processes from start to finish to ensure reproducibility.

This template plagarizes heavily from the following excellent resources:

- [Coding for Economists](https://aeturrell.github.io/coding-for-economists)
- [Reproducible Data Analytic Workflows for Economics](https://lachlandeer.github.io/snakemake-econ-r-tutorial)
- [start your lab templates](https://github.com/startyourlab)

## Template Features

- Recommended folder structure organizing project files
- An RStudio project [`template.Rproj`](./template.Rproj)
- Package dependency management using [`renv`](https://github.com/rstudio/renv/)
- Environment-specific configuration using [`config`](https://github.com/rstudio/config)
- A comprehensive [`.gitignore`](./.gitignore) file to keep version tracking history clean
- A Quarto document with code snippet examples
  

## Prerequisites

Make sure you install the latest versions of R and RStudio.

This template is compatible with Git and GitHub by default. I suggest using GitHub Desktop to develop your project from this template, though you can also use standard command line tools if preferred.

For R package dependencies, we use the [`renv` package](https://rstudio.github.io/renv/articles/renv.html). This should be installed on your local computer. While in an active RStudio session, simply run the following line of code in the Console.

```r
install.packages('renv')
```

## Quickstart Guide

To use this template, click the green **Use this template** button above to generate your project. It will ask you to 

1. Choose the repository's username/organization name, i.e., `your-GH-username`.
2. Name the repository, i.e., `new-project`.
3. Add a short description of the project.

Once the repository is generated, you will be redirected to your new repository on GitHub.

### Clone the repository to your local machine

Go to the green **Code** button with a dropdown menu. There are two preferred methods, and we recommend using whichever you prefer:

#### 1. Open with GitHub Desktop

Click **Open with GitHub Desktop**, and pick a location in your personal file system to store it using the GitHub Desktop cloning interface.

#### 2. Command line using HTTPS method

If using Linux or prefer the command line, you will use the HTTPS-based URL from the **Code** dropdown menu. The URL will look like `https://github.com/DHEPlab/dhep-project-template.git`. Click the clipboard icon to copy it. From within your projects directory in the terminal, run `git clone ...`, replacing the "..." with the URL you just copied.

### Usage

### Renaming template files and content

Once the project is cloned to your computer, you need to rename the following files with your own names:

- `DHEP-Project-Template.Rproj`, changing `DHEP-Project-Template` to your repository name
- `sandbox/Notebook-template.qmd`, changing `Notebook-template` to the notebook name that you would like for the project's first notebook.

### Local package installation

After renaming the above files, open the project in RStudio and run the following line of code in your RStudio's Console:

```r
renv::restore()
```

This will install all of the foundational packages needed to begin developing your R project with this template. If installation encounters an error, restart your R session and try again. 

If you would like to install packages specific to your project's goals, now is the time to start! You can install packages like [`tidyverse`](https://www.tidyverse.org/), [`slackr`](https://mrkaye97.github.io/slackr/), or other packages on CRAN. For example, running

```r
install.packages('tidyverse')
```

will install `tidyverse` for your project. If you want to make this a package that the entire team uses for this project, run

```r
renv::snapshot()
```

to record the package with its version number in the `renv.lock` file, which keeps track of all the great packages you and your team use together.




## Project Structure

**Each `project` lives in its own repository/folder.** Everything needed for a given project is somewhere in this directory. Typically, a `project` is a specific paper. 

## Top-level directory structure

```{}
./
|- data-raw/
|- src/
|- out/
|- log/
|- sandbox/
README.md
Snakefile
```

- Root Folder (`./`): This is the main folder of the project. Everything that is used or produced for the project should be located in a this folder, or better yet a sub-folder. Think of it as a ‘one-stop shop’ for what you are working on for this project. If it’s important - you must be able to find it here.

- `data-raw/` is where we store raw data files. These are data files that we downloaded from the survey platform or elsewhere. **Never edit or save over these files.** 

- `out/` folder. This is the output directory. We will put anything that we create by running a R script. For example, it can contain new datasets we create by cleaning and merging our original data, saved regression results and saved figures or summary tables. The main point is that anything we can recreate by running R scripts will get saved here - whether they be ‘temporary’ or ‘intermediate’ outputs that will get used by another R script later in our project, or ‘final’ outputs that we will want to insert into a paper, report or slide deck.

- `log/` folder. When we run and R script it produces output and messages, typically printing them to the screen. If we want to save those messages to a file, so we can refer to them in the future, we will save them here.

- `sandbox/` folder. As we work through our project, we will want to explore new ideas and test out how to code them. While we play with these bits and pieces of code, we save them in the sandbox. Separating them from src means we know that R scripts in here are ‘under development’. When they are finalized, we can move them into src.

- `README.md` file. A README is a text file that introduces and explains the project. We should write information that explains what the project is about and how someone can run the scripts developed for the project in this file. The `README-template.md` file is a template with the typical information that should be included when archiving the project.

- `Snakefile`. We will use the Snakefile to write the steps needed that run all the scripts in the project. Further discussion of Snakefiles are deferred to the next chapter when introduce Snakemake.

## The `src/` folder

The `src/` folder contains all of the source code for the project. 

```
./
|- src/
    |- data-management/
    |- analysis/
    |- utilities/
    |- figures/
    |- tables/
    |- table-specs/
    |- paper/
    |- slides/
```

- `data-management/` contains all R scripts to clean and merge datasets together
- `analysis/` contains all R scripts that are our main analysis. For example, our regression scripts
- `utilities/` contains R scripts that contain functions that can be used more generally. For example helper functions that can be used in both data cleaning and analysis could be put here. So can scripts that contain functions that can be portable across multiple projects.
- `figures/` contains R scripts that produce figures. One script per figure.
- `tables/` contains R scripts that produce summary tables and regression tables. One script per table.
- `paper/` contains the Rmarkdown files to write up project results in a paper, i.e. the paper’s text.
- `slides/` contains the Rmarkdown files to write up project results as a slide deck, i.e. the text of the slides.