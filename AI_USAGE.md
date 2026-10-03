# AI Usage

## AI Models
I used the free version of Claude, Sonnet 5.5, to create the code for the AI-assisted cleaning. Claude is generally better at generating code than my go-to AI, Copilot. I then used Copilot Chat (basic) to give me code for standardizing the date column. This is a simpler task that it can handle.

## AI-Assisted Cleaning

### Sequences AI Prompt
I gave Claude this prompt and attached the `messy_sequences.fasta` to create the desired sequence output:

* Write an R script that uses regular expressions to parse the messy file into a clean, consistent structured table (header fields split into separate columns for the FASTA case). The table should have a column for the full header, the sample id, the organism, and the gene name. 

This prompt originally gave me code that standardized the output of all of the sequences. For example, all of the organisms were written as Homo Sapiens instead of including the variety of text: H.Sapiens, Hsapiens, etc. I prompted Claude again with this:

* Rewrite the code please. The data in the fasta doesn't need to be standardized. Rather, the exact values from the fasta should be pulled (i.e. H.Sapiens instead of Homo sapiens). 

This prompt gave me my desired output.

### Samples AI Prompt
I gave Claude this prompt and attached the `messy_samples.csv` to create the desired samples output:

* Write an R script that uses regular expressions to parse the messy file into a clean, consistent structured table (standardized date format, standardized categorical values, standardized units with conversion where needed). The csv data should be read into the file under the name 'ai_samples'. 

This prompt immediately gave me the code necessary for a cleaned table (though different from my cleaned table), so I did not have to follow up with any corrections or further prompts. 

## Editing the Date Format
I was unsure how to standardize the date format in the samples table, so I asked AI.
* Prompt: Use regex to clean up this column (I included a screenshot with the varying date formats in the column).

### AI Response
AI gave me many options, but I wanted to stick with the output that I understood the best. I chose this code.
```
library(dplyr)
library(stringr)
library(lubridate)

df <- df %>%
  mutate(
    dob_clean = str_replace_all(dob, "\\.", "/"),
    dob_clean = parse_date_time(
      dob_clean,
      orders = c("mdy", "ymd", "dby")
    ) %>% as.Date()
  )
```
