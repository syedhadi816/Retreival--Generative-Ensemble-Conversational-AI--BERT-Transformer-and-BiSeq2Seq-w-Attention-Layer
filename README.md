# Gerald - A Retreival and Generative Ensemble for Conversational AI - with BERT Transformer and T5 Conditional Generator

An open-source and open-domain conversation AI model named GERALD (named after Gerald Salton) that uses a sequential ensemble of a retrieval-based and generation-based system to intelligently respond to user queries while maintaining contextual and structural relevance. The retrieval-based system has been trained on a large dataset based on conversational AI question-answer pairs and natural language conversations from multiple sources. The top k queries in the dataset that match closely with a user query are extracted and processed. These queries are then evaluated and passed on to the generative model, which intelligently generates new responses which are contextually relevant and structurally aligned with the user query. The main objective of the program is to generate queries intelligently.

The retrieval-based system uses a BERT transformer to contextually evaluate a user query against the dataset and the generative model uses a T5 transformer model which conditions on the retrieved text and the user query to generate new sequences. This ensemble system is known to outperform retrieval based and generation-based models working independently.


## Dataset

The dataset for the program has been synthesised and is not public. It can be downloaded using the following link:
https://drive.google.com/drive/folders/1nMZd5lHQBb6zIyI_BhziQXBwS_qckISf?usp=share_link

The following three files are required to use to program: 

1. q_a_pairs.csv (CSV files containing 0.6M pairs of questions and Answers, stored as text data, the first 2 columns are redundant indexes which can be discarded). 
2. q_pca_embed.txt (Text file that contains weights that are used by the retreival model. These weights are dimension-reduced using PCA. 
3. pca.pkl (.pkl file that has the trained PCA model. It is also used by the retrieval model to reduce dimensions of user input). 



## Sample Output: 
Example Output:

> how far is the Moon from Earth?  
moon is 238 857 miles 384 392 kilometers from earth. the distance between the moon and the earth is 238 857 miles.

> what's the shape of the Earth?  
earth's oblate spheroid is a spheroidal. 


> Who is JK Rowling?  
jk rowling is a british novelist best known for her work on the Harry potter series. she is also the author of the harry potter series of books.

> I often have headaches.
headaches are caused by stress, tension or prolonged tension. the most common cause of headaches is stress.

> How do I relieve stress?  
meditation, yoga and regular exercise can relieve stress. if you talk to someone about your feelings exercise helps relieve stress.

> Who was George Mason?  
mason was an american patriot statesman and a delegate from virginia to the u s constitutional convention. mason was a member of the u s. senate who was a member of the senate who was a member of the senate who was a member of the senate.

> How many awards did Beyonce win?  
beyonce won 20 grammys.

> Are therapists any good?  
therapist can help you cope with feelings and symptoms and change behavior patterns. a therapist can help you change your thinking and behavior.

> What is your age?  
what is your age, i am still young by your standards. i am still a student


