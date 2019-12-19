# proteomic_tutorials
How-to tutorials to run proteomic software programs.

## Table of Contents
[Software](#software)

[Topological Score](#Topological-Score-(TopS))

## Software

You will need RStudio to run the following:

* Topological Score
* Proteus

## Topological Score (TopS)

The purpose of this tool is to score protein interactions.

The code for this program is available at https://github.com/WashburnLab/Topological-score-TopS-.

The paper describing this program can be obtained at https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6408525/.

### Installation

To download the program, use the following command:
<pre>
git clone https://github.com/WashburnLab/Topological-score-TopS-.git
</pre>

### Prepare input

There must be an input file called *input_file.csv* in the same folder as the code. 

Since TopS can take averages, use the output file from process_maxquant.py called *norm_avg.xlsx*. This file contains the averages for both the control and experimental groups. 

To obtain the scores, the *input_file.csv* can contain only one stimulant/timepoint at a time. 

The input_file.csv must have three columns:
1. Protein ID
2. Control average
3. Experiment average

Example:

<img src="https://github.com/jonessarae/proteomic_tutorials/blob/master/images/tops_input.PNG" height=300 width=300>

Make sure to save the file as a CSV (Comma delimited) when using excel.

<img src="https://github.com/jonessarae/proteomic_tutorials/blob/master/images/csv.PNG">

### Run tool

__Open RStudio.__

If this is your first time running TopS, install the following packages in RStudio:

<pre>
install.packages("devtools")
install.packages("gplots")
install.packages("gridExtra")  
install.packages("shiny")          
</pre>

__Load the library *shiny*__ 
<pre>
library(shiny)
</pre>

__Set your working directory to the TopS folder__
<pre>
setwd("C:/Users/jonesse3/Topological-score-TopS-")
</pre>

__Run the program__
<pre>
runApp()
</pre>

A user interface will appear, but you do not need it to get the output. 

Image of user interface:

<img src="https://github.com/jonessarae/proteomic_tutorials/blob/master/images/tops_gui.PNG" height=300, width=300>


### Save the results
In the TopS folder, the scores can be found in a file called *output_file.txt*. 

Save the results to a new file before running the app again.

### Stop the app
Stop the app by pressing the Stop button in RStudio to rerun the program again with runApp() on a new *input_file.csv*.

<img src="https://github.com/jonessarae/proteomic_tutorials/blob/master/images/stop.PNG" height=500, width=700>

## SAINTq

### Installation

Download SAINTq from the following website: https://sourceforge.net/projects/saint-apms/files/.

### Prepare input files

#### Parameter file

<pre>
### SAINTq parameter file
## use # to mark a line as comment

## normalize control intensities
normalize_control=true

## name of file with intensities
input_filename=PolyIC_120.txt

## valid: protein, peptide, fragment
input_level=protein

## column names
protein_colname=Protein

## control bait selection rules
compress_n_ctrl=100

## test bait replicate selection rules
compress_n_rep=100
</pre>





