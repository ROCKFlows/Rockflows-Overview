# Rockflows-Overview
Welcome to the Rockflows organization on GitHub! This repository serves as the central hub for all our projects, providing an overview and links to each individual repository.

## About Rockflows
Rockflows aims to help non-expert users on the selection of the Machine Learning Workflows to solve their Machine Learning problems.

We pursue several operational objectives:
1. Constructing a suitable workflow based on data and business requirements.
2. Retrieving similar past experiments based on data information, business requirements, and algorithmic choices.
3. Automatically enriching the knowledge base from past experiences.
4. Discovering new knowledge by exploring past experiments.
5. (In progress) Automatically determining the profile of an ML workflow.
6. (In progress) Automatically verifying that an ML workflow adheres to best practices.
7. (In progress) Automatically verifying that an ML workflow meets FATES properties (during construction or deployment).
8. (In progress) Automatically justifying best practices through proof construction and justification diagrams.

The project has been ongoing for nine years, exploring various dimensions evident in the different repositories listed below. Today, we aim to provide a more structured framework, leveraging the lessons learned.

## Repository List

Below is a list of our main repositories, each accompanied by a brief description and an abstract of lessons learned.

- [Comparison of Workflows: a Step Further](https://github.com/ROCKFlows/experiments-public/tree/master): The questions focus on predicting key performance metrics (accuracy, execution time, and memory usage) of machine learning workflows on user datasets without undergoing the evaluation phase.
    - **_Lessons Learned:_**  
            - [Luca Parisi'report](https://github.com/ROCKFlows/experiments-public/blob/master/doc/tesi.pdf) Comparing workflows is not about testing if one metric has a better value, whether once or on average, but **about assessing if there is a significant difference**. Consequently, it is more interesting to build classes of algorithms for a given problem and metric, which requires storing a large number of results and computations.  
          - [Luca Parisi'report](https://github.com/ROCKFlows/experiments-public/blob/master/doc/tesi.pdf) To evaluate a workflow, it is essential to master the evaluation processes, notably by reproducing not only the experiment but also by conducting it on the same data split.   
          - [Luca Parisi'report](https://github.com/ROCKFlows/experiments-public/blob/master/doc/tesi.pdf) Preprocessing has a significant impact; it is not about comparing algorithms but **comparing workflows.**  
          - [Luca Parisi'report](https://github.com/ROCKFlows/experiments-public/blob/master/doc/tesi.pdf) Metadata dependencies seem difficult/impossible to identify through logical patterns.
- [Learning from experiments on Machine Learning Workflows](https://github.com/ROCKFlows/experiments-public/tree/master)  (same repository):  As we cannot predict performances from a logic approach, we deviate to the construction of a Meta-Learning system. The theoretic model we have designed is focused on supervised classification problems, although it can be extended to unsupervised or supervised regression problems. We used the results of different Machine Learning experiments, precisely the results of 1086 workflows (composed of 16 pre-processing techniques, 68 classifiers, and 10 parameter strategies) tested over 101 datasets from the UCI repository. This input data was processed to produce the meta-datasets, with which we trained different sub-models to predict three properties: accuracy, total time, and model size.

We developed a module to extract the 48 most representative meta-features of a given dataset, which is an essential part of the prediction flow. When a user comes with her dataset, a tool extracts the meta-features of the dataset. Then, thanks to this description, the prediction is made by exploiting the similarities between the vector of Meta-Features of the given dataset and the Meta-Features of the datasets already in the Meta-Datasets of the Meta-Learning system.
The Meta-Learning Model we designed and implemented is highly scalable, as it does not require additional computations before adding a new instance to the knowledge base. We further enhanced its scalability by using Regression Algorithms instead of Classification ones.
We studied the online learning approach to reduce the incremental training time of the model. However, among the different incremental learning solutions for regression in the literature, we did not find an algorithm comparably good to its batch learning counterpart. For this reason, each sub-model of the Meta-Learning system uses a Random Forest regressor.
The hyperparameter optimization results show that after using 250 trees in the Random Forests, a law of diminishing return is observed; in other words, the accuracy is not significantly improved by using more than 250 trees in the Meta-Learning system's sub-models.
The structure of the Meta-Learning system proposed was studied
throughout the project, searching for a solution that provides good accuracy results, manageable model size, and training, loading, and prediction times that satisfy the requirements of the web service implemented for the ROCKFlows platform. 
The final structure for this system consists in using one sub-model L_meta i,j for each classifier i and property j, and including in the Meta-Features the pre-processing technique and the other workflow steps (i.e. Parameter Strategy).
The research of this work is limited by the number of datasets used and the number of workflows defined. We propose to extend the research in this direction, looking for ways to increase the number of datasets in the knowledge base of the Meta-Learning system to understand better the effect of the nature of the dataset (given by the Meta-Features) on the performance of the workflows. Finally, a similar work should be conducted to extend this work in predicting other Machine Learning problems such as clustering, regression, and reinforcement learning tasks.
  - **_Lessons Learned:_** 
           - [Miguel Fabián ROMERO RONDÓN'report] **Meta-Feature selection and extraction:** Based on the learning phases, we developed a module to extract the 48 most representative meta-features of a given dataset, which influence accuracy. It should be noted that the most significant meta-features vary depending on the workflow. We used these meta-features for prediction by leveraging the similarities between the meta-features of the given dataset and those of datasets already in the Meta-Learning system. Calculating meta-features is not free, and selecting the most impactful meta-features is necessary to reduce the computational load.
           - [Miguel Fabián ROMERO RONDÓN'report] **Scalability of the Meta-Learning Model:**
We focused on designing a highly scalable Meta-Learning model that does not require additional computations before adding a new instance to the knowledge base. So, we enhanced scalability by using regression algorithms instead of classification ones and rejected online learning as we found no incremental learning algorithm for regression in the literature that performs as well as its batch learning counterpart. However, after multiple experiments, we used one sub-model L_meta i,j for each classifier i and property j. For scalability purposes, we included preprocessing techniques and other workflow steps (e.g., parameter strategy) in the meta-features.
           - [Miguel Fabián ROMERO RONDÓN'report] **Research Limitations:** (Insights from Extensive Meta-Learning Experiments)  
Beyond the limitations related to the number of datasets used and the predefined workflows, it became evident that, in line with autoML research, the required learning processes, i.e., the experiments needed to achieve our goals, exceeded the reasonable capacities of the computing grids at our disposal. Ultimately, (i) we were not truly learning by merely predicting performance without gaining real insights, and (ii) to avoid learning on new datasets, we needed to train on a large number of datasets.

- Version de Miguel
- RF V1
- Version Nicolas L.
- Version Gunther
- Version Yacine
- Version Yann
