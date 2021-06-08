# What Texts Whisper: Information retrieval and Prediction from Corporate Documents to Performance

## INTRO

Automatization of repetitive tasks represents the future of work. It contributes to transforming bussineses by increasing productivity and enabling humans to focus their attention on creative and more challenging problems.

Basicaly most of the ML algorithms that are used in production today were developed  back in the 80'. So what  has changed since then ? The real break out that happened in Machine Learning, and in Deep Learning is the fact that computational power used to train the largest models has doubled every 4 months since 2012. Also the data has become much more accesible and easier to crawl from websites and store . 

The majority of algorithms used today needs to be trained with adnotated data to learn.THIS IS THE REASON WHY  labeling data is CONSIDERED  the engine that powers machine learning.BUT this process is expensive and time consuming. Fortunatelly, in our company, we have human experts specialized on key domains who manually addnotated our documents by extracting  bussiness specific citations. They helped us by building a adnotated citations database.
A citation is composed by a chunk of text from a document which the human expert adnotated as beeing relevant for  a certain business requirement and it has attached a label to it.
Note that at this point the addnotations are done at the document level, and are not very precise. It takes to read the entire document to find relevant citations and not all the information from the document is important for the requirement itself.
    
In our final solution we want to automatically filter all the irellevant information from the document.SO  We  extracted all paragraphs from documents and if the paragraph contains the citation we consider  the information from the paragraph as sufficient for the citation.AS WE CAN SEE  the dataset will contain paragraphs from the documents which have attached labels for specific requirements. HERE WE DEFINE a label as beeing the INDICATOR CODE PLUS a TICKBOX ID which serves as identifiers for the citation.

IN ORDER TO OBTAIN THE DATASET WE NEED A PROCESSING PIPELINE

THe raw data is stored into PDFs. We learn how to turn a pdf into a structured text document by using a tool called GROBID. THe names stands for GeneRation Of Bibliographic Data. It outputs a XML document for each PDF. This approach has advantages over other OCR techniques:
    is easy to use, 
    is much faster than other OCR( it takes couple seconds to process a PDF vs minutes using Teseract for example), 
    the output is an XML file that is easy to parse and extract the paragraphs from, which is exactly what we needed.

In our pipeline we take the PDF document file convert it into a structured XML file, Parse the XML file and extract all the paragraphs from it.
After that we cleaned the text from each paragraph and applied SpaCy Named Entity Recognition to hash all the named entities. We observed that by doing this we increased the True Positives and decrease the False Positive from matching paragraph with the correct citation.
After that we applied Term Frequency- Inverse Domain Frequency and turn each parapgrah into a Bag Of Words features vector.
We applied the same Term Frequency Inverse Domain Frequency model on each citation from the Database.
We compute the cosine similarity between the paragraphs and the Citations by taking the Dot product between their TF-IDF Bag of Words vectors. If the cosine similarity was greater than a THRESHOLD than we attach a LABEL to the paragraph in the dataset, otherwise not.

## DATASET AND METRICS

As a quich statistics the final dataset contains one hundered fifty thousands citations, three point five milions paragraphs and there are around two hundred classes.
We used a special metric to measure the performance of classification models: Mathew Correlation Coefficient
The Mathew Correlation Coefficient is a performance metric used as a measure o the quality of binary classification. It is quite more complex than other correlation metrics such as Precision, Recall, F1 Score and Accuracy. It s quite said that is better than Accuracy on unbalanced dsitributions.
We observe that in the numerator is using the four terms from the CONFUTION MATRICES(True Positives, False Positives, True negatives and False Negatives). We should not care so much about  the denominator becasue it is a NORMALIZATION constant that is always positive. THIS points out that the result of MATHEW CORRELATION COEFFICIENT will always be between -1 and 1.
A high value closer to one means that both classes are predicted well, even if one class is disproportionaly over represented than the other. 
A low value closer to zero  means that the classifiers performs randomly and a even lower value closer to -1 means that there is a total disagrement between predicted values and the actuals values.


EXPERIMENTS

In our experiments we played with more versions of spliting the documents:
    we ve tried spliting documents at sentence level,but in this case the precision is very low
    we've splited at page level, but in this case there was to much irrelevant information and the granularity is low
    even when we split into bloks of 500 tokens there was still to much irrelevant information 
    we found out that the best splitting was at paragraph level as described earlier.



