# NRI - Update 2
February 28, 2020


Helen Huang, Shivam Misra, Priya Padmanabhan, Surya Pugal,  Yixiao Yue


## Summary

### King & Plink Results

**Summary**

Using the .bed/.fam/.bim data, we fed the data into these two programs, and used the linux command line to produce 2 output files.

Command for King : ` king -b InputFilename.bed --related --prefix OutputFileName`

Command for Plink : ` plink --bfile InputFileName --genome --nonfounders --out OutputFileName `

One notable thing is that for the plink command, the filename do not need any extensions.


**Format of King Outputs**

The output file has .kin extension. Each row compares the DNA of 2 individuals from the same family. We are interested in the column named "PropIBD" because it is the coefficient of relatedness. The column named "InfType" also provided useful information that infered relationship type based on PropIBD values.

**Format of Plink Outputs**

The output file has .genome extension. Each row also compares the DNA of 2 individuals from the same family. The content of the columns are different, but the coefficients of relatedness information is still there, named "PI_HAT" this time.

**Challenges**

While seemingly straight-forward at first, this task did not go smoothly. When we ran the command on our own computers, the execution always got stuck, which led us to conclude that our computers did not have enough CPU power for it. Then we set up to ssh to CNSI (California Nanosystem Institute) computers. Unfortunately, it got stuck on those computers as well. Strangely, our mentors were able to run the commands when they ssh to CNSI computers. The problems ended up being the version of the software. We downloaded the latest version which had a bug. We got an older version, and were able to got the outputs successfully.

### Kinship2 Results

**Summary**

Given the .bed/.fam/.bim data for multiple inviduals in the same family, we were asked to feed in the data into Kinship2 in order to produce a pedigree and calculate the coefficients of relatedness. This value is the percentage of genes between a pair of individuals that is the same. We then had to compare the values produced by Kinship2 with what came from the King and Plink software. 

**Introduction of The Package (Kinship2)**

Kinship2 is a package in R. Accoriding to its official documentation, it is a routine to handle family data with a pedigree object. It can be used to create correlation structure that can describe family relationships, draw pedigrees focusing on producing compact layouts without intervention, trim the pedigree object with various criteria, and so forth.

For our project, we fed in the data containing family relationship and disease carrying information. With the help of Kinship2, we were able to produce the pedigree and obtain the theoretical relatedness coefficients for all pairs of individuals in the family.

**Kinship Coefficient vs. Relatedness Coefficient**

What we got from Kinship2 are the kinship coefficients. To get the relatedness coefficients, we needed to multiply the kinship coefficients by 2:

Relatedness Coefficient = Kinship Coefficient * 2

In comparison to relatedness coefficient, the kinship coefficient is defined as the probability that a pair of randomly sampled homologous alleles are identical by descent (IBD, see Update 1 for definition). In simple words, it is the probability that an randomly chosen allele selected from individual 1 and an allele selected at the same autosomal locus from individual 2 are IBD. Because humans are diploid, meaning that cells contain 2 copies of each chromosome, we need to multiply the kinship coefficient by two to get the relatedness coefficient.

**Format of Output**

Our output file produced a matrix in a similar format to the structure shown below. For example, row 3 column 2 and row 2 column 3 both contain the kinship2 coefficient of the pair id1 and id2. The values on the diagonal are all 1s because they represent the relationship  of an individual to themself. After removing the individuals who were not directly part of the family, our file reduced to a 29 by 29 matrix.  

![](kinship2example.png)

**What We Did**

1. Created a .ped (txt) file which contains the information for all the PSEN1 family members. Each individual has the information of family id, individual id, paternal id, maternal id, sex id, and phenotype info
2. Used R to read in the .ped file
3. Created a pedigree structure and plotted it 
4. Created the Kinship2 coeffcient matrix 
5. Multiplied all of the values by 2 (see above for why)
6. Removed all of the rows who were not fully sequenced (i.e. the individuals that we do not have their entire genome/DNA sequence)


## Data Processing


## Data Analysis


## Future Vision