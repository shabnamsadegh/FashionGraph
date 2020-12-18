# FashionGraph
![examples of fashion graph](https://github.com/shabnamsadegh/FashionGraph/blob/V0/examples.png)

This is the implementation of the paper "FashionGraph: understanding fashion data using scene graph generation" ICPR2020.

Our contributions:
- Brought the idea of scene graphs to fashion images.
  - helps in better understanding of fine-grained fashion data.
- A model to generate fashion scene graphs. 
  - using object and relationship detection models.
  - we generated new annotations for this purpose.
- Integrated the attribute detection into the scene graph model.
- Highlighted the application of SG for fashion image retrieval.


## Dataset
This project is trained on [Fashionpedia dataset](https://github.com/cvdfoundation/fashionpedia).

More information about the objects and predicates can be found in [their paper](https://arxiv.org/abs/2004.12276).

## FashionGraph annotations
![how to annotate the relationships](https://github.com/shabnamsadegh/FashionGraph/blob/V0/annotations.png)

SG detection models are trained on triplets of object-predicate-subject, where object and subject are segments in an image and their connection(predicate) label is learned by the model. 

An example of a triplet in conventional SG: ```Man[sbj] Sitting-on[predicate] Chair[obj]```

Howevert Fashiongraph is looking for different relationships between the objects:
1. **Hierarchical relationships**
   - ```Pocket[sbj] belongs-to[predicate] Skirt[obj]. ```

2. **Attributes and colors**
In this case we cannot assume the predicates as Skirt[subj] is[predicate] A-line[object]. Because A-line is not a segment in an image (can you find "beautiful" in an image of mountains?). Instead, we annotate the attributes as predicates:
   - ```Skirt[sbj] A-line[predicate] Skirt[obj]```, if the subject is a main clothing part 
   - ```Neckline[sbj] plunging[predicate] Dress[obj]```, when subject has a parent e.g. neckline beongs to dress.

## Model
This work is heavily based on [RELDN repository](https://github.com/NVIDIA/ContrastiveLosses4VRD). 
We used their code to train an object detection model specific for fashionpedia (their obj detection model is based on detectron). 
Then we trained their SGDET model on the relationships we had derived from the original dataset.

Therefore to train our model from scratch or predict SG for a fashion image, follow these steps:

- Follow the instruction of [RELDN for installation](https://github.com/NVIDIA/ContrastiveLosses4VRD).
- If you want to train on a new dataset, you may want to check the changes I made in [my fork of RELDN](https://github.com/shabnamsadegh/ContrastiveLosses4VRD) (unfortunately, RELDN has hardcoded database-related parts all over their code. hopefully my fork would help to figure that out.)
- Download our annotations and models from [here: todo]()

## Experiments in the paper
- "Image Retrieval Experiments.ipynb" for image retrieval experiment (section IV.c of the paper)
- "Recall@k experiment.ipynb" for recall@k experiment (Table I, in the paper)

## To cite us
Coming soon

## The topic of computer vision in fashion is close to my :heart:
It takes some time till I complete the documentation for this repo. Meanwhile, you have my full support if you are contributing to this topic.
