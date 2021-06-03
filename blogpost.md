# What Texts Whisper: Information retrieval and Prediction from Corporate Documents to Performance

Automatization of repetitive tasks represents the future of work. It contributes to transforming busineese by increasing productivity and enabling humans to focus their attention on creative, newer and more challenging problems. And since machine learning (ML) models automatize decisions, they are a good thing in general, as well.

[Idee despre faptul ca big data si puterea de calcul au dus la revolutia cu machine learning]
PARAGRAPH I
Basicaly the ML algorithms that are used in production are almost the same with those used  back in the 90'. So what  realy has changed since then ? The increasing of computing power and the fact that now we are able to crawl and access big datasets 

[Daca am vorbit despre cat de importante sunt datele, acum trebuie sa vedem cum facem: foarte multe companii au documente cu informatii structurate, problema vine acum cu extragerea informatiilor structurate si cum le facem labeluirea] Aici intervine PIPELINE PROCESSING
PARAGRAPH II

a) Cum am extras text din PDF uri cu pdf2text si apoi am impartit textul in pagini/blocuri/propozitii si am incercat sa le labeluim
a1) Cum am folosit GROBID pt a extrage paragrafe din PDF uri si pe acestea am 
b) Cum am NER uit textele deoarece  am observat o imbunatatire la crestere TP
c) Cum am facut fuzzy matching (deoarece avem noise in text) cu TFIDF si DOT PRODUCT pe textele extrase pt a atasa citatele extrase de adnotatori

d) Cum am encodat paragrafele cu SentenceBERT si apoi am aplicat un model clasificator cu attention head pe ele.
e) Problema ca desi aveam recall mare, aveam foarte multe False Positives
