# Comparison Write-up

## Comparing the Sequence Outputs
1. Where did they agree?
> The AI was able to identify the different segments of the FASTA header, which includes the sample ID, organism name, and gene   name.
2. Which caught edge cases the other didn't?
> Following the first AI prompt, Claude gave me code that standardized the output for each column, much like I did with the Samples table. For example, the organism column for each sample said Homo Sapien. However, in the case of the FASTA files, you want to extract the exact text that is in the header, so instead of writing out Homo Sapien for each of the sequences, the output should include text variance like H.sapiens. I had to write a second prompt to get the desired output.
3. Time/effort comparison: which was faster to get right?
> Obviously, with correct prompting, AI is incredible and provided me with a fast solution. However, my code is much more straightforward and succinct, which is preferable. I do think that the code that AI provided was much longer because it only used base R and did not import any packages.
4. Failure modes: 2 specific records where one or both approaches got something wrong (or ambiguous).
> As mentioned, the original AI code standardized the header information. This was the first error the AI made and demonstrates the difference between AI and human comprehension. I gave AI the exact prompt from the Lab 3 site explaining what we were supposed to do with the FASTA. However, I knew from class that we were expected to extract the exact text from the header, and AI didn't. Hence, I had to prompt AI again with more specific instructions. The second error that AI made was including the length of the FASTA sequences as a column called seq_length in the table output. I specifically mentioned what the columns should be in the prompt I gave Claude, but they added this column anyway. This was not an issue with my data. If anything, it provides more context about the sequence. However, if you were potentially sharing the output with someone else without credentialing, and the column that was accidentally added included PHI, that could be a big problem. 
## Comparing the Samples Outputs
1. Where did they agree?
> Both my code and the AI code standardized the column information. For example, the sample IDs differed row to row, and we each chose a standardized format for the column values.
2. Which caught edge cases the other didn't?
> I was actually surprised how well Claude caught edge cases. For example, when I was converting the glucose value to mg/dL (which involves multiplying by 18.02), sometimes the glucose value exceeded what is humanly possible. Both AI and I caught this and assumed that the glucose values were put in as mmol/L, when they were probably an mg/dL value. We also both identified the arbitrary asterisks next to some glucose values. Ultimately, we both identified the same edge cases, but we approached them differently regarding how we standardized the columns.
3. Time/effort comparison: which was faster to get right?
> AI was faster. I wasn't as confident with using regex expressions to standardize a dataframe, so it took me some time to achieve my desired output. However, the code from AI didn't create the exact output I wanted, so I would have had to spend more time prompting AI to achieve my exact desired result.
4. Failure modes: 2 specific records where one or both approaches got something wrong (or ambiguous).
> Our approaches to standardizing the glucose units were different. In my case, when I identified the ambiguity of the glucose value after unit conversion, instead of keeping those new values and making a note, I decided to remove all of the values that originally had the mmol/L unit. AI decided to keep the converted values, with the questionable glucose values, and made an extra categorization column called "glucose_qc" that labeled the glucose value as "ok", "missing", or "out_of_range". But AI forgot to change the mmol/L units to mg/dL units after conversion! Similarly, I decided to remove the arbitrary asterisks on the glucose values immediately, assuming they were a typo. AI also removed the asterisks, but created a new column called "glucose_flagged" with boolean values that display whether that glucose value was marked with an asterisk. Neither of us was wrong. We don't have enough context about how the data was collected to edit the dataframe's discrepancies.


## Samples x Features x Metadata Table
A quick note --> I didn't create a separate Samples x Features x Metadata Table as I think my samples output table is already in this format. There is a single row for each sample, a feature column (the glucose value), and necessary metadata like the DOB and sex.
1. Are types consistent?
> Throughout the standardization process, column values all have the same formatting. Therefore, the data is cleaner and more reliable.
2. Is missingness documented rather than silently dropped?
> I silently dropped certain data, including the glucose values that originally had mmol/L units and the asterisk on the glucose values. I did so knowing that I would document these choices in my README. However, if I were sending the raw table to a peer, I would make sure to document this within the table itself.
3. Are units resolved to one system
> Yes. mg/dL.
