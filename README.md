# Universal Language Model Fine-tuning for Text Classification
        (Challenge submission for fellowship.ai)
        
# ULMFiT Sentiment
Apply a supervised or semi-supervised ULMFiT model to Twitter US Airlines Sentiment

# Introduction
Taking a view of the advantages of pretraining we would be able to do better than initializing arbitrarily the remaining parameters of our models. However, finetuning inductive transfer was ineffective for NLP. Language model (LM) fine-tuning requires millions of in-domain documents to achieve good results, which significantly limits its applicability. Universal Language Model Fine-tuning (ULMFiT) solves these issues and facilitates stable, inductive learning transfers for any NLP function.

# Model Description
ULMFiT is essentially a method to enable transfer learning for any NLP task and achieve great results. All this, without having to train models from scratch. ULMFiT achieves state-of-the-art result using novel techniques like:

-Discriminative fine-tuning
-Slanted triangular learning rates, and
-Gradual unfreezing

This method involves fine-tuning a pre-trained language model (LM), trained on the Wikitext 103 dataset, to a new dataset in such a manner that it does not forget what it previously learned.

https://github.com/vibeeshK/Twitter-US-Airline-Sentiment-using-ULMFiT-model/blob/master/Images/ULMFIT.webp

# General-domain LM pretraining 
The model was pre-trained using Wikitext-103 which is consisting of 28,595 preprocessed Wikipedia documents and 103 million words [2].

# Target task LM fine-tuning 
Regardless of how complex the general-domain data used for pre-training is, the target task data would typically come from a different source. Therefore, we fine-tune the language model on target task results. This stage converges more quickly, provided a pre-trained general-domain LM, as it only needs to adjust to the idiosyncrasies of the target data, and it enables us to train a robust language model even for small datasets.

- Discriminative fine-tuning
Because different layers’ capture various information types, they should be fine-tuned to a different degree. Instead of using the same learning rate for all layers of the model, Discriminative fine-tuning allows one to apply specific learning levels to each layer. It was empirically found that it performed well to select the last layer's Alpha^L learning rate first by fine-tuning only the last layer and using Alpha^(L-1) = (Alpha^L)/2.6 as the lesser layer learning rate. For L, the order of the layer in the model.

- Slanted triangular learning rates
To adjust its parameters to task-specific features, at the beginning of the training, make the model converge quickly into an acceptable region of the parameter space, and then refine its parameters. Slanted triangular learning rates (STLR), first increase the learning rate linearly and then decay it linearly. Finally, the learning rate at the stiffest slop will be chosen.

# Target task classifier fine-tuning
The pre-trained language model with two additional linear blocks was augmented to fine-tune the classifier. Following common practice for Computer Vision (CV) classifiers, each block uses batch normalization and dropout, with intermediate layer ReLU activations, and a Softmax activation that outputs a probability distribution at the last layer over target classes. Remember that the only parameters learned from scratch are the parameters in these task-specific classifier strata. The first linear layer takes the last hidden layer being pooled as the input state.

# Results

https://github.com/vibeeshK/Twitter-US-Airline-Sentiment-using-ULMFiT-model/blob/master/Images/Results.png

