# FashionGraph

![examples of fashion graph](https://github.com/shabnamsadegh/FashionGraph/blob/V0/examples.png)

This project is the implementation of the paper "FashionGraph: understanding fashion data using scene graph generation" ICPR2020.

Our Novel contributions:
 - We trained a scene graph generation for fashion's fine-grained segments. 
 - For the first time, we integrated attribute prediction into the scene graph generation model. 
 - We showed how Fashiongraph can improve the search and retrieval of fashion images.

## Dataset
This project is trained on Fashionpedia dataset downloaded from the [kaggle competition, iMaterialist 2020,](https://www.kaggle.com/c/imaterialist-fashion-2020-fgvc7/overview) "Fine-grained segmentation task for fashion and apparel".

More information about the objects and predicates can be found in [their paper](https://arxiv.org/abs/2004.12276).

For Downloading the data, you have to agree to their condition. Then if you send [me](mailto:sadegh.shabnam@gmail.com) a screenshot that you have access to the Kaggle data, I will send you the complementary annotations needed for this project.

## How it works
RELDN SG generator is trained on triplets of object-predicate-subject and their positions in an image. Where object and subject are segments in an image and their connection(predicate) is learned by the model. The predicate [in conventional SG] is the type of interaction between object and subject (e.g. positions such as behind, in front of, ... or actions such as holding, sitting,...). 

An example of a triplet is: Man[sbj] Sitting-on[predicate] Chair[obj]

The same applies to clothing hierarchy(without attributes): 

Pocket[subject] belongs-to[predicate] Skirt[object]. (how we drive these triplets in our dataset? refer to our paper)

For the attributes, the story is different. Intuitively you may think of it as a triplet: Skirt[sub] is[predicate] A-line[object] or Neckline[sub] is[predicate] Plunging[obj]. However, the problem is an attribute is not a segment in an image. To tackle this problem, we annotate the attributes as the following: 
- Skirt[sub] A-line[predicate] Skirt[obj] , if sub is a main clothing part 
- Neckline[sub] plunging[predicate] Dress[obj], when subj has a parent e.g. neckline beongs to dress

## Model
This work is heavily based on [RELDN repository](https://github.com/NVIDIA/ContrastiveLosses4VRD). 
We used their code to train an object detection model for imaterialist fashion dataset (their obj detection model is based on detectron). 

Then we trained their SGDET model on the relationships we had derived from the original dataset.

Therefore to train our model, follow these steps:

- Follow the instruction of [RELDN for installation](https://github.com/NVIDIA/ContrastiveLosses4VRD).
- If you want to train on a new dataset, you may need to check the changes I made in [my fork of RELDN](https://github.com/shabnamsadegh/ContrastiveLosses4VRD) (unfortunately, RELDN has hardcoded database-related parts all over their code. hopefully my fork would help to figure that out.)
- Download our annotations and models (you will receive them as well as a how-to guide, if you send me the kaggle policy confirmation of the dataset via email.)

## To reproduce the results
Follow the jupyter notebooks: 
- "Image Retrieval Experiments.ipynb" for image retrieval experiment (section IV.c of the paper)
- "Recall@k experiment.ipynb" for recall@k experiment (Table I, in the paper)

## To cite us
Coming soon

## The topic of computer vision in fashion is close to my :heart:
It takes some time till I complete the documentation for this repo. Meanwhile, you have my full support if you are contributing to this topic. I would be more than happy to answer your questions.
