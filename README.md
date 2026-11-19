#Python program to detect and analyse substitution mutations in *S. pombe* samples from NGS sequencing data 

##Purpose: 

To automate the analysis of substitution mutations between groups, and to generate a summary of mutation patterns to aid investigation into the effect of the independent variable/s on the type/frequency/position of mutations and changes to read validity for each sample or group.

##How to run in colab:
**Option 1:** Go to (https://colab.research.google.com/) -> Upload Notebook -> GitHub -> Paste the url of this repo -> save a copy to your Drive -> Run all


##Inputs:
**reads:** A list of dictionaries from reads.csv containing the following keys: read_id, sample, group, sequence, each with strings as values. The program assumes that each sample and group has a unique name, and that each sample is unique to one group.

**reference:** a single string of valid reference DNA from reference.txt of the unmutated sequence you want to compare the reads against.

##Outputs:
**Finished:**


*   A nested dictionary of summarised samples and a summary table for each group, with analysed metrics for each sample within each group.

**Unfinished:**

*    An accompanying substitution summary table for each group
*    A statistical analysis of the top mismatch positions



##Code design: 


*   In clean_format_sequence, I used .strip(), as it's easy to accidentary add spaces in excel, especially if pasting. This means an otherwise valid sequence like 'ACGT   ' wouldn't be mislabeled as invalid - which would effect the analysis and resulting statistics. 

* Similarly, the error message in is_dna uses !r syntax to make whitespace obvious if manually checking pasted/typed sequences that haven't been cleaned.

*   For samples_summary, I initially planned to make an helper function that made an intermediate dataframe and then make variables that would calculate each key, but to reduce complexity, I chose to initialise a dictionary instead and instead used increment operators.





##Testing: 


*  Made test_reads_three to verify if top_positions displayed less than 3 positions
*   Modified test_summary to verify sample_summary was correct, especially for top_positions and testing position counts, which led to me discovering it was adding positions in the order it found them in the sample, which I fixed by using sort and lambda.
