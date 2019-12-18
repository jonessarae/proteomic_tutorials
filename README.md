# proteomic_tutorials
How-to tutorials to run proteomic software programs.

## Table of Contents
[Software](#software)

[Topological Score](#Topological-Score-(TopS)

## Software

RStudio

## Topological Score (TopS)

The code for this program is available at https://github.com/WashburnLab/Topological-score-TopS-.

The paper describing this program can be found here: 

### Installation

To download the program, use the following command:
<pre>
git clone https://github.com/WashburnLab/Topological-score-TopS-.git
</pre>

### Prepare input

There must be an input file called *input_file.csv* in the same folder as the code. 

Since TopS can take averages, use the output file from process_maxquant.py called *norm_avg.xlsx*. This file contains the averages for both the control and experimental groups. 

To obtain the scores, the *input_file.csv* can contain only one stimulant/timepoint at a time. 

The input_file.csv should have three columns:
1. Protein ID
2. Control average
3. Experiment average

Example:

Make sure to save the file as a CSV (Comma delimited) when using excel.

### Run tool

__Open RStudio.__

If this is your first time running TopS, install the following packages in RStudio:

<pre>
install.packages(“devtools”)
install.packages(“gplots”)
install.packages(“gridExtra”)  
install.packages(“shiny”)          
</pre>

__Load the library *shiny*__ 
<pre>
library(shiny)
</pre>

__Set your working directory to the TopS folder__
<pre>
setwd("C:/Users/jonesse3/Desktop/Joe_proteomic/TopS")
</pre>

__Run the program__
<pre>
runApp()
</pre>

### Save the results
In the TopS folder, the scores can be found in a file called *output_file.txt*. 

Save the results to a new file before running the app again.

### Stop the app
Stop the app to rerun the program again with runApp() on a new *input_file.csv*.


