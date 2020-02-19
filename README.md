# proteomic_tutorials
How-to tutorials to run proteomic software programs.

## Table of Contents
* [Software](#software)
* [Topological Score](#Topological-Score-(TopS))
* [SAINTq](#SAINTq)
* [Proteus](#Proteus)

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

<img src="https://github.com/jonessarae/proteomic_tutorials/blob/master/images/tops_gui.PNG" height=400, width=300>


### Save the results
In the TopS folder, the scores can be found in a file called *output_file.txt*. 

Save the results to a new file before running the app again.

### Stop the app
Stop the app by pressing the Stop button in RStudio to rerun the program again with runApp() on a new *input_file.csv*.

<img src="https://github.com/jonessarae/proteomic_tutorials/blob/master/images/stop.PNG" height=500, width=700>

## SAINTq

SAINTq is a tool that uses a probabilistic method for scoring bait‐prey interactions against negative controls in affinity purification – mass spectrometry experiments.

The SAINTq program can be found at this website, https://sourceforge.net/projects/saint-apms/files/.

The paper describing the program can be found at https://onlinelibrary.wiley.com/doi/full/10.1002/pmic.201500499.

### Installation

Click on the green button to download the latest version of the executable. 

<img src="https://github.com/jonessarae/proteomic_tutorials/blob/master/images/download_saintq.PNG" height=300 width=500>

### Prepare input files

There are two input files that is used by SAINTq. The first is a table of intensity measurements, and the second is a parameter file for the input data information and optional parameters for inclusion criteria in scoring.

#### Parameter file

Example: 
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

The only parameter you will need to change in the parameter file is *input_filename*. Everything else can be kept as is.

An example of the parameter file, *param_prot_level.txt*, is included in the folder, *example_files*. 

#### Intensity table file

You will need to create an intensity table file for each stimulant/timepoint.  Use the output file from process_maxquant.py called *all_norm.xlsx*. This file contains the intensity values for each replicate in the control and experimental groups. Copy the pertinent columns as well as the protein ID column, "Majority protein IDs", to a new excel file.  

The first three lines in this excel file must describe the bait and experimental information as shown in the example below. 

<img src="https://github.com/jonessarae/proteomic_tutorials/blob/master/images/saintq_input.PNG">

The first line indicates whether each bait is a test protein (T) or control (C). 

The second line indicates the bait name.

The third line indicates the bait replicate IP names. Note that "Majority protein IDs" was changed to "Protein" to match the parameter *protein_colname* in the parameter input file. 

Save this file as a Text (Tab delimited) in excel. 

<img src="https://github.com/jonessarae/proteomic_tutorials/blob/master/images/file_save.PNG">

### Run the program

<pre>
./saintq_v0.0.4.exe param_prot_level.txt
</pre>

or in Windows Command Prompt

<pre>
saintq_v0.0.4.exe param_prot_level.txt
</pre>

The output file is a tab-separated value (TSV) file that starts with *scores_list*. It contains the probability score, AvgP, and the Bayesian false discovery rate, BFDR, for each bait-prey interaction. 

### Post-processing
Since *scores_list* files representing each timepoint for one condition (ex. LPS) don't include all the proteins in the original input file, *saintq_scores_formulas.xlsx* is included in the *example_files* folder. 

Paste the original proteins, prey proteins, AvgP, and BFDR for each timepoint in their respective columns. To the right of these columns is another set of columns pre-filled with formulas that will match each prey protein to the original protein. Anything that is missing will have a AvgP of 0 and a BFDR of 1. 


## Proteus

Proteus is an R package for downstream analysis of MaxQuant output. Proteus offers many visualisation and data analysis tools and allows simple differential expression using limma.

The code for Proteus is available at https://github.com/bartongroup/Proteus.

The paper describing Proteus can be found at https://www.biorxiv.org/content/10.1101/416511v2.

An in-depth tutorial that demonstrates how to analyse data using Proteus is found here: http://www.compbio.dundee.ac.uk/user/mgierlinski/proteus/proteus.html

### Installation

Open RStudio and run the following commands to install Proteus and its dependencies:

<pre>
install.packages("BiocManager")
BiocManager::install()
BiocManager::install("limma")
install.packages("devtools")
devtools::install_github("bartongroup/Proteus", build_opts= c("--no-resave-data", "--no-manual"), build_vignettes=FALSE)
</pre>

### Prepare input files

#### Intensity input file

Proteus can directly read in MaxQuant proteinGroups.txt file. To prepare this file, we can use the output file from process_maxquant.py called *all_norm_rand.xlsx*. We are using this file, which doesn't contain any 0's, to obtain differential expression results. Otherwise, if the file contained 0's, any protein hits with 0's across all replicates in either the control group or experimental group will not output any result such as the p-values.

Proteus expects three columns from the proteinGroups.txt file:
* Majority protein IDs
* Reverse
* Potential contaminant

Using excel, we can add columns for "Reverse" and "Potential contaminant" as shown in the example below:

<img src="https://github.com/jonessarae/proteomic_tutorials/blob/master/images/proteus_input.PNG">

*Note: Sort the column "Majority protein IDs" to prevent misalignment of the intensity data when using Proteus' interactive tools such as plotVolcano_live.*

Save the file in the Text (Tab delimited) format in excel.

#### Metadata file

A metadata file describing the design of the experiment is also needed. It should look like the example below:

<img src="https://github.com/jonessarae/proteomic_tutorials/blob/master/images/proteus_meta.PNG">

Save the file in the Text (Tab delimited) format in excel.

An example of the metadata file, *PolyIC_meta.txt*, is included in the folder, *example_files*. 

### Running Proteus

#### Load Proteus 
<pre>
library(proteus)
</pre>

#### Read in metadata file

<pre>
# path to metadata file
metadataFile <- "LPS_meta.txt"
# read in metadata file
meta <- read.delim(metadataFile, header=TRUE, sep="\t")
# create list with names corresponding to sample names in the intensity file
new_measure_cols <- setNames(paste("",meta$sample,"",sep=""),meta$sample)
</pre>

#### Read in proteinGroups file

<pre>
# path to proteinGroups file
proteinGroupsFile <- "LPS_norm_intensity.txt"
# read in proteinGroups file to create proteusData object
prot_data <-readProteinGroups(proteinGroupsFile, meta, measure.cols=new_measure_cols)
</pre>

#### Differential Expression

Intensity data are log2 transformed using the transform.fun function (a parameter of limmaDE) before applying limma to do differential expression between the control and experiment for each timepoint.  

<pre>
L_0 <- limmaDE(prot_data, sig.level=0.05, transform.fun = log2, conditions=c("LC_0","LM_0"))
L_10 <- limmaDE(prot_data, sig.level=0.05, transform.fun = log2, conditions=c("LC_10","LM_10"))
L_30 <- limmaDE(prot_data, sig.level=0.05, transform.fun = log2, conditions=c("LC_30","LM_30"))
L_60 <- limmaDE(prot_data, sig.level=0.05, transform.fun = log2, conditions=c("LC_60","LM_60"))
L_120 <- limmaDE(prot_data, sig.level=0.05, transform.fun = log2, conditions=c("LC_120","LM_120"))
# combine results for each timepoint
L_all <- cbind(L_0, L_10, L_30, L_60, L_120)
# save to a file
write.table(L_all, file="LPS_proteus_stats.txt",sep="\t", row.names=TRUE)
</pre>

#### Other useful commands for analysis

For more information on others commands and example output, please refer to this tutorial: [Using proteus R package: label-free data](http://www.compbio.dundee.ac.uk/user/mgierlinski/proteus/proteus.html).

##### Volcano plots

<pre>
plotVolcano(L_10)
</pre>

##### Dendograms

<pre>
plotClustering(prot_data)
</pre>

##### Heatmaps

<pre>
plotDistanceMatrix(prot_data)
</pre>

##### Normalization

<pre>
# median normalization
prodat.med <- normalizeData(prot_data)
</pre>

##### Violin plots of sample distributions

<pre>
plotSampleDistributions(prot_data, title="Not normalized", fill="condition", method="violin")
</pre>

##### Annotation

<pre>
# dataframe of UniProt IDs
ids <- as.data.frame(prot_data$proteins)
# add column name to dataframe
names(ids) <-"protein"
# fetch basic annotations (gene names and protein names) from UniProt
annotations <- fetchFromUniProt(ids$protein, verbose=TRUE)
# merge the two dataframes
annotations.id <- merge(ids, annotations, by.x="protein", by.y="id")
# keep only unique IDs
annotations.id <- unique(annotations.id)
# add annotations to proteus object
prot_data <- annotateProteins(prot_data, annotations.id)
</pre>

*Note that if there's more than one UniProt ID in a cell, no annotation will be provided. You will need to edit the cell to contain just one UniProt ID.* 
##### Interactive plots

<pre>
plotVolcano_live(prot_data, L_10)
</pre>

Example:

<img src="https://github.com/jonessarae/proteomic_tutorials/blob/master/images/plot_volcano.PNG">
