# FashionGraph

![examples of fashion graph](https://github.com/shabnamsadegh/FashionGraph/blob/V0/examples.png)

This project is an implementation of the paper "FashionGraph: understanding fashion data using scene graph generation" ICPR2020.

It brings the idea of scene graphs to the fashion domain. 
Scene graph generators focus on subject-object relationships. However, with a twist in an existing idea, we also integrated attributes into a scene graph generator.
This is the first time that the fashion domain can benefit from such graph representation. 
We showed the effectiveness of our method on the tasks of scene graph generation and fashion image retrieval. 

## Dataset
This work is trained on Fashionpedia dataset downloaded from the [kaggle competition, iMaterialist 2020,](https://www.kaggle.com/c/imaterialist-fashion-2020-fgvc7/overview) "Fine-grained segmentation task for fashion and apparel"
More information about the objects and predicates can be found in [their paper](https://arxiv.org/abs/2004.12276)

## How it works
RELDN SG generator is trained on triplets of object-predicate-subject and their positions in an image. Where object and subject are segments in an image and their connection(predicate) is learned by the model. The predicate [in conventional SG] is the type of interaction between object and subject (e.g. positions such as behind, in front of, ... or actions such as holding, sitting,...). 
an example of a triplet is: Man[sbj] Sitting-on[predicate] Chair[obj]
The same applies to clothing hierarchy(without attributes): 
Pocket[subject] belongs-to[predicate] Skirt[object]. (how we drive these triplets in our dataset? refer to our paper)

For the attributes, the story is different. Intuitively you may think of it as a triplet: Skirt[sub] is[predicate] A-line[object] or Neckline[sub] is[predicate] Plunging[obj]. However, the problem is an attribute is not a segment in an image. To tackle this problem, we annotate the attributes as the following: 
- Skirt[sub] A-line[predicate] Skirt[obj] , if sub is a main clothing part 
- Neckline[sub] plunging[predicate] Dress[obj], when subj has a parent e.g. neckline beongs to dress

## Model
This work is heavily based on [RELDN repository](https://github.com/NVIDIA/ContrastiveLosses4VRD). 
We used their code to train an object detection model for imaterialist fashion dataset(their obj detection model is based on detectron). 
Then we trained their SGDET model on the relationships we had derived from the original dataset.
Therefore to train our model, follow these steps:
- follow the instruction of RELDN for installation
- If you are not using our annotations, you may need to check the changes I made in [my fork of RELDN](todo) (unfortunately, RELDN has hardcoded database-related part all over their code. hopefully my fork would help to figure that out.)
- you can download our annotations here
- you can also find our trained model here. [todo: I will provide a better how-to. for now contact me if you have a problem.]

## To reproduce the results
Follow the jupyter notebooks: 
- "" for image retrieval
- "" for recall@k 

## To cite us
Coming soon

## The topic of computer vision in fashion is close to my :heart:
So you have my full support if you are contributing to this topic. I would be more than happy to answer your questions.
