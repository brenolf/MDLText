# MDLText
------------------------------------------------------------------------------

## How to use mdl-train

------------------------------------------------------------------------------
Usage: 
```mdl-train [options] [input_fileName] [model_fileName]``` 

```input_fileName: Relative path to a text file. Such file can be just one text sample to be trained, a index
   file with the paths to a set of samples, a file with a sample per line in the format
   <class>,<text> or a file in libsvm format  ```

```model_fileName: Name given to output model created by MDL after training```

```
Options:
    -i input_type : set type of input file (default 0)  
        -0 -- the path to just one text document  
        -1 -- the path to a text file which has a list of paths to text documents  
        -2 -- the path to a text file where each line is a sample in the format <class>,<text>      
        -3 -- the path to a file in libsvm format 
        
   -c class: document class (necessary only when input_type = 0)
   -t tokenizer_id : set the type of tokenizer (default 1)
       1 -- tokenizer A: Convert any non-alphanumeric char to whitespace and tokenize by space
       2 -- tokenizer B: Tokenize by {. , ; space enter return tab} and preserve the first
                         and last chars. The remainder ones are kept if they are alphanumeric
   -n apply_normalization : (default 0)
       0 -- false (don't normalize words, e.g. 'going' -> 'go')
       1 -- true (apply text normalization)
   -r remove_stopWords : (default 1)
       0 -- false (don't remove the stop words)
       1 -- true (remove the stop words)
   -s save_type : how model should be updated (default 0)
       0 -- the model is updated only after all documents are trained
       1 -- the model is updated after each document is trained
``` 


## How to use mdl-classify

------------------------------------------------------------------------------
Usage: ```mdl-classify [options] [input_fileName] [model_fileName] [output_fileName]```

```
input_fileName:
   Relative path to a text file. Such file can be just one text sample to be trained, a index
   file with the paths to a set of samples, a file with a sample per line in the format
   <class>,<text> or a file in libsvm format

model_fileName:
   File name of the model used by MDL to classify the messages

Options:

   -i input_type : set the type of input file (default 0)
       0 -- the path to just one text document
       1 -- the path to a text file which has a list of paths to text documents
       2 -- the path to a text file where each line is a sample
       3 -- the path to a file in libsvm format
   -t tokenizer_id : set the type of tokenizer (default 1)
       1 -- tokenizer A: Convert any non-alphanumeric char to whitespace and tokenize by space
       2 -- tokenizer B: Tokenize by {. , ; space enter return tab} and preserve the first
                         and last chars. The remainder ones are kept if they are alphanumeric
   -n apply_normalization : (default 0)
       0 -- false (don't normalize words, e.g. 'going' -> 'go')
       1 -- true (apply text normalization)
   -r remove_stopWords : (default 1)
       0 -- false (don't remove the stop words)
       1 -- true (remove the stop words)
   -f feature_relevance_function : function to calculate the relevance of tokens (default CF)
       CF -- Confidence Factors
       DFS -- Distinguishing Feature Selector
       NO -- not use any function
   -o omega : set omega (vocabulary size) (default 2^10) 
```

## Examples

We provide some text collections in folder ```examples/```


To employ MDL classifier on polarityReview text collection in which each sample is a text file:

* For training:
		
		./mdl-train -i 1 examples/polarityReview/polarityReview_train models/mdl_polarityReview.mod
		
* For classifying:
		
		./md-classify -i 1 examples/polarityReview/polarityReview_test models/mdl_polarityReview.mod results/mdlCF_polarityReview.res
		


To employ MDL classifier on SMS Spam Collection in which each sample is a line of a text file:

* For training:
		
		./mdl-train -i 2 examples/SMSSpamCollection/smsspamcollection_train models/mdl_SMS.mod
		
* For classifying:
		
		./mdl-classify -i 2 examples/SMSSpamCollection/smsspamcollection_test models/mdl_SMS.mod results/mdlCF_SMS.res
		

To employ MDL classifier on datasets stored in LIBSVM format:

* For training:
		
		./mdl-train -i 3 examples/libsvm_format/reuters_train.libsvm models/mdl_reuters.mod
		
* For classifying:
		
		./mdl-classify -i 3 examples/libsvm_format/reuters_test.libsvm models/mdl_reuters.mod results/mdlCF_reuters.res