# run_gensel.sh Bash Script

This directory has informaiton on how to run my script if you 
ever need to run 100 traits at a time back to back. Or you can split 
it up into a few directories and run them simultaneously. 

## Steps

### 1 - Write out datasets

In R (or your favorite program), loop and right out your datasets. 

```R
# list of files
  for (i in c("AMIRres", "CMIRres")){
   
    # pull out fixed effects and remove missing
    data.cur <- data.prod[, c("ID", i, "Batch", "EntryAge", "HIRTech")]
    
    # change names
    names(data.cur) <- c("SNP", i, "Batch$", "EntryAge", "HIRTech$")
    
    # remove missing
    data.cur <- na.omit(data.cur)
    
    # save to file
    write.table(data.cur, paste0(save_dir_gensel, i, ".dat"), 
      sep=" ", quote=FALSE, col.names = TRUE, row.names = FALSE)
    
  }

```

This will list files as trait1.dat, trait2.dat, etc. Just change 
to the names of your columns and your model. The $ after the 
variable name means it is a factor (class). 

Place these in a folder called 'Data' or whatever you want. 

### 2 - Write a template .inp file

Write a template parameter file with keywords to replace. 
* TRAIT
* EXT
* CAT
* a_var
* e_var

### 3 - Create a file with trait names and starting values

Create a space delimited file with names of traits you want to 
run and starting values. The last column is to say yes/no if it is 
categorical or not. 

### 4 - Run the script first by testing

You should get the following if you run it without any options. 





