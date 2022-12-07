GERALD: Conversational AI

This Project Implements an open source and open domain conversation AI model that uses a sequential ensemble of a retrieval based and generation-based system to intelligently respond to user queries while maintaining contextual and structural relevance. The retrieval-based system has been trained on a large dataset based on conversational AI question-answer pairs and natural language conversations from reddit, Counsel Chat and IRC Chat Rooms etc. Top k queries in the dataset that match closely with a user query are extracted and processed. These queries are then evaluated and passed on to the generative model which intelligently generates new responses which are contextually relevant and structurally aligned with the user query. The retrieval-based system uses a BERT transformer to contextually evaluate a user query against the dataset and the generative model uses a T5 transformer model which conditions on the retrieved text and the user query to generate new sequences. This ensemble system is known to outperform retrieval based and generation-based models working independently.


Requirements

•	Python 3.5+
•	Keras
•	tensorflow
•	NLTK
•	Pyaudio
•	Speech_recognition
•	Pickle
•	Transformers
•	Pyttsx3
•	Msvcrt


Algorithm

When a user presents a query to the model, a vector representation of length 768 is formed using the BERT transformer for the query. 
This dimensionality of this vector is then reduced using the same PCA model used to reduce the dimensions of the training data. When 
saved as a .pkl file, the PCA model does not need to be retrained every time the model is run. The reduced length vector is compared 
against all queries within the data using cosine similarity. A vector having the length of the number of data observations is created 
and the indices of this vector are sorted based on the match similarity. Indices corresponding to the top 3 matching queries are taken 
and the answers corresponding to these queries (w¬¬hich share the same indices) are extracted. From the perspective of optimizing the 
algorithm, the next part of the program is categorized into a Layer 1 and Layer 2, and the top 3 retrieved responses are evaluated before 
being pushed to the generative model. Layer 1 is engaged when a similarity of 90% or greater exists between the user query and the first 
retrieved response. The query within the dataset and the answer corresponding to this query are fed to the pre-trained T5 Conditional 
Generator. The T5 model contextualizes the data query and response into a single output which is then presented to the user. The length 
of the output sequence is capped at 1.5 times the length of the answer within the dataset to ensure relevance and prevent the T5 model 
from including meaningless sequences to the response. When left uncapped, it has been observed that the T5 model elongates decoder output 
to include meaningless sequences of text.Layer 2 is engaged when the retrieval system cannot find a response having a similarity higher 
than 90% within the dataset. In this case the top 3 data queries and their corresponding responses are extracted and fed individually to 
the T5 generator which creates generates a sequences of max length 25 for each of the 3 query-response pairs. In the next step, each of 
these 3 generated responses along with the user query are fed to the T5 generator again and this time a sequences of max length 60 is 
generated. This is presented as an output to the user.   



Example Output:

Program Input: how far is the Moon from Earth
moon is 238 857 miles 384 392 kilometers from earth. the distance between the moon and the earth is 238 857 miles.

Program Input: what's the shape of the Earth
Program Output: earth's oblate spheroid is a spheroidal o


Who is JK Rowling
jk rowling is a british novelist best known for her work on the Harry potter series. she is also the author of the harry potter series of books.

I often have headaches
headaches are caused by stress, tension or prolonged tension. the most common cause of headaches is stress.

How do I relieve stress
meditation, yoga and regular exercise can relieve stress. if you talk to someone about your feelings exercise helps relieve stress.

Who was George Mason
mason was an american patriot statesman and a delegate from virginia to the u s constitutional convention. mason was a member of the u s. senate who was a member of the senate who was a member of the senate who was a member of the senate.

How many awards did Beyonce win
beyonce won 20 grammys.

Are therapists any good
therapist can help you cope with feelings and symptoms and change behavior patterns. a therapist can help you change your thinking and behavior.

What is your age
what is your age, i am still young by your standards. i am still a student


Dataset 
The dataset for the program has been synthesised and is not public. It can be downloaded using the following link:
https://drive.google.com/drive/folders/1nMZd5lHQBb6zIyI_BhziQXBwS_qckISf?usp=share_link

The following three files are required to use to program: 

1. q_a_pairs.csv (CSV files containing 0.6M pairs of questions and Answers, stored as text data, the first 2 columns are redundant indexes which can be discarded). 
2. q_pca_embed.txt (Text file that contains weights that are used by the retreival model. These weights are dimension-reduced using PCA. 
3. pca.pkl (.pkl file that has the trained PCA model. It is also used by the retrieval model to reduce dimensions of user input). 









