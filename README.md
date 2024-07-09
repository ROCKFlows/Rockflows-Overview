# Rockflows-Overview
Welcome to the Rockflows organization on GitHub! This repository serves as the central hub for all our projects, providing an overview and links to each individual repository.

## About Rockflows
Rockflows is dedicated to creating machine learning (ML) workflows tailored to problem-solving needs. We pursue several operational objectives:
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

Below is a list of our main repositories, each accompanied by a brief description:

- [Comparison of Workflows: a Step Further](https://github.com/ROCKFlows/experiments-public/tree/master): The questions focus on predicting key performance metrics (accuracy, execution time, and memory usage) of machine learning workflows on user datasets without undergoing the evaluation phase.
    - **_Lessons Learned:_**  
            - [Luca Parisi'report](https://github.com/ROCKFlows/experiments-public/blob/master/doc/tesi.pdf) Comparing workflows is not about testing if one metric has a better value, whether once or on average, but **about assessing if there is a significant difference**. Consequently, it is more interesting to build classes of algorithms for a given problem and metric, which requires storing a large number of results and computations.  
          - [Luca Parisi'report](https://github.com/ROCKFlows/experiments-public/blob/master/doc/tesi.pdf) To evaluate a workflow, it is essential to master the evaluation processes, notably by reproducing not only the experiment but also by conducting it on the same data split.   
          - [Luca Parisi'report](https://github.com/ROCKFlows/experiments-public/blob/master/doc/tesi.pdf) Preprocessing has a significant impact; it is not about comparing algorithms but **comparing workflows.**  
          - [Luca Parisi'report](https://github.com/ROCKFlows/experiments-public/blob/master/doc/tesi.pdf) Metadata dependencies seem difficult/impossible to identify through logical patterns.
- Learning from experiments on Machine Learning Workflows   
  - **_Lessons Learned:_**  
           - [Miguel Fabián ROMERO RONDÓN'report]
- Version de Miguel
- RF V1
- Version Nicolas L.
- Version Gunther
- Version Yacine
- Version Yann
