# CAIS_Winter_Project
CAIS++ Winter Project
Catherine Lu
clu97123@usc.edu

My project was to create a model that could determine whether or not a news headline was sarcastic. In the digital information age, misinformation is easily spread, and it is necessary to start training AI to recognize sarcasm.

<ins>Dataset:</ins>
The dataset I used was the News Headlines for Sarcasm Detection dataset (v2). This dataset had 28,619 headlines from TheOnion and HuffPost. Each headline was labeled using binary classification for is_sarcastic, where 1 was sarcastic and 0 otherwise. There was also a column for the link to the original article, but that was not used for training the model. 

<ins>Model Development and Training:</ins>
I decided to use a pretrained BERT model, specifically BERT base model (uncased), since all the headlines in the dataset were in lowercase. Since it was my first time creating a NLP model, I borrowed most of the code from the Lesson 4 Notebook. One difference I made was to separate the original dataset into a training, validation, and testing dataset. The training and validation datasets were 64% and 16% of the original dataset respectively (18,316 and 4,579 sentences) and to be used during training. The testing dataset was the remaining 20% of the dataset, kept hidden from the model so it could be used to evaluate its accuracy after being trained. I used the standard batch size of 32. As the dataset was relatively small for an NLP model, and BERT has a catastrophic forgetting issue, a very small learning rate of 2e-5 was used. Using Adam as the optimizer and setting epsilon to 1e-8 was taken from the L4 notebook. Only 2 epochs were used, since the authors of BERT recommend between 2-4 epochs, and training on my laptop takes a fairly long time (~20 minutes per run). Given that 2 epochs produced a fairly high accuracy score, I used the minimum number of epochs in the interest of time.

<ins>Model Evaluation/Results:</ins>
After being trained, the model was producing an accuracy score of 93% on the validation dataset. I then ran the testing dataset through the model, which produced a very high Matthew's Correlation Coefficient of 0.846. I also took the accuracy, precision, and recall scores, which were 0.923, 0.926, and 0.91 respectively. This meant that the model was very good at predicting both positive and negative samples correctly. 

Just for fun, I also made my own dataset of TheOnion and HuffPost headlines to test the model on. I chose 10 headlines, 5 from each company across the years 2019-2023. To my surprise, the model performed quite well, predicting 8 out of 10 headlines to be sarcastic correctly. Additionally, the two wrong predictions could be confusing to human judgement as well. The first headline was "inmate stuck on u.s. death row despite vacated death sentence", which sounds like it shouldn't be true, but is actually a case of bureaucratic issues in the prison system. The second headline, "worst career advice baby boomers give millennials", requires knowing the prior context baby boomers being mocked for being out-of-touch to be read as sarcastic.

<ins>Discussion:</ins>
Overall, the News Headlines for Sarcasm Detection dataset provided very clean and easy to understand data using real and satirical articles as examples. Sarcasm detection is a very valuable tool for AI, as it will prevent spreading misinformation to users. There is some limitation in only using TheOnion for sarcastic headlines and HuffPost for serious headlines, as news companies can write articles about different content, as well as have different writers with varying writing styles. The dataset could be improved by including headlines from multiple news companies in the future. Additionally, for the goal of "detecting sarcasm online", only training off of news headlines could be limiting. If we want to train AI to be able to recognize online information written satirically and not factually, it would be necessary to obtain more sources of data. These could include social media posts or other online media. 

If I were to continue this project, my next steps would be to perform more training runs of the model while testing different hyperparameters. I would also like to include more training data like headlines from other news companies and posts from sites like X and Reddit.

Dataset used:
1. Misra, Rishabh and Prahal Arora. "Sarcasm Detection using News Headlines Dataset." AI Open (2023).
2. Misra, Rishabh and Jigyasa Grover. "Sculpting Data for ML: The first act of Machine Learning." ISBN 9798585463570 (2021).
