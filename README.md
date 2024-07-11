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



Below is a list of our main repositories, each accompanied by a brief description and an abstract of lessons learned.
## Repository List, History and Lessons Learned

Below is a list of our main repositories, each accompanied by a brief description and an abstract of lessons learned.

- **2016** - [**Comparison of Workflows: a Step Further**](https://github.com/ROCKFlows/experiments-public/tree/master): The questions focus on predicting key performance metrics (accuracy, execution time, and memory usage) of machine learning workflows on user datasets without undergoing the evaluation phase.
    - **_Lessons Learned:_**  
      - [Luca Parisi'report](https://github.com/ROCKFlows/experiments-public/blob/master/doc/tesi.pdf) Comparing workflows is not about testing if one metric has a better value, whether once or on average, but **about assessing if there is a significant difference**. Consequently, it is more interesting to build classes of algorithms for a given problem and metric, which requires storing a large number of results and computations.  
      - [Luca Parisi'report](https://github.com/ROCKFlows/experiments-public/blob/master/doc/tesi.pdf) To evaluate a workflow, it is essential to master the evaluation processes, notably by reproducing not only the experiment but also by conducting it on the same data split.   
      - [Luca Parisi'report](https://github.com/ROCKFlows/experiments-public/blob/master/doc/tesi.pdf) Preprocessing has a significant impact; it is not about comparing algorithms but **comparing workflows.**  
      - [Luca Parisi'report](https://github.com/ROCKFlows/experiments-public/blob/master/doc/tesi.pdf) Metadata dependencies seem difficult/impossible to identify through logical patterns.
      
- **2017** - [**Learning from experiments on Machine Learning Workflows**](https://github.com/ROCKFlows/experiments-public/tree/master)  (same repository):  As we cannot predict performances from a logic approach, we deviate to the construction of a Meta-Learning system. The theoretic model we have designed is focused on supervised classification problems, although it can be extended to unsupervised or supervised regression problems. We used the results of different Machine Learning experiments, precisely the results of 1086 workflows (composed of 16 pre-processing techniques, 68 classifiers, and 10 parameter strategies) tested over 101 datasets from the UCI repository. This input data was processed to produce the meta-datasets, with which we trained different sub-models to predict three properties: accuracy, total time, and model size.
    - **_Lessons Learned:_**    
      - [Miguel Fabián ROMERO RONDÓN'report] **Meta-Feature selection and extraction:** Based on the learning phases, we developed a module to extract the 48 most representative meta-features of a given dataset, which influence accuracy. It should be noted that the most significant meta-features vary depending on the workflow. We used these meta-features for prediction by leveraging the similarities between the meta-features of the given dataset and those of datasets already in the Meta-Learning system. Calculating meta-features is not free, and selecting the most impactful meta-features is necessary to reduce the computational load.  
      - [Miguel Fabián ROMERO RONDÓN'report] **Scalability of the Meta-Learning Model:**
      We focused on designing a highly scalable Meta-Learning model that does not require additional computations before adding a new instance to the knowledge base. So, we enhanced scalability by using regression algorithms instead of classification ones and rejected online learning as we found no incremental learning algorithm for regression in the literature that performs as well as its batch learning counterpart. However, after multiple experiments, we used one sub-model L_meta i,j for each classifier i and property j. For scalability purposes, we included preprocessing techniques and other workflow steps (e.g., parameter strategy) in the meta-features.   
   - **_Sub-conclusion:_** **_Recognizing the True Scale of Computational Demands in Research_**
      -  Beyond the limitations related to the number of datasets used and the predefined workflows, it became evident that, in line with autoML research, the required learning processes, i.e., the experiments needed to achieve our goals, exceeded the reasonable capacities of the computing grids at our disposal. 
      - Ultimately, (i) we were not truly learning by merely predicting performance without gaining real insights, and (ii) to avoid learning on new datasets, we needed to train on a large number of datasets.

- **2018** - [**Automating the Learning Processes for Extensive Experimentation**]: Given the large number of experiments required, it is essential to automate the learning processes. This automation includes composing pipelines, training on appropriate datasets, and recording measurements. Since it is not sufficient to compare a single set of measurements but rather to compare sets of measurements, it is also necessary to automate ranking and meta-learning processes. To ensure precision, we must maintain consistency in execution and measurement environments. Additionally, considering our limited resources, we aim to reuse data preparation and implement a form of crowd experimenting to add new experiments to our knowledge base at a constrained cost.
    - **_Lessons Learned:_**
        - [Günther Jungbluth'report (French)] **Automating valid Pipeline Composition based on Constraints and Graph Representation** enhances the automation of learning processes, ensuring valid ML workflow compositions while efficiently managing complexity. 
          - **Data-centric constraints** are expressed as pre- and post-conditions on algorithms relative to metadata. For example, a pipeline like "_NumericTransformationToNominal; NumericNormalization; SVM"_ is invalid because the preprocessing step _NumericNormalization_ requires numeric data, which the previous algorithm removes.
          - **Pipeline-centric constraints** define a partial order between algorithms. For instance, the constraint "_Missing value removal must always precede normalization_" invalidates the pipeline "_Normalization; ...; MissingValueRemoval; SVM._" These constraints significantly reduce the combinatorial complexity between datasets and pipelines.
          - **A graph structure** is used to handle the mass of compositions, incremental addition of new algorithms, and strategic graph traversal for launching experiments. We were unable to design it using constraint solvers, as they never scaled effectively.
            Ensuring Consistent and Scalable Experimentation with Docker and Efficient Resource Management
        - [Günther Jungbluth'report (French)] **Leveraging Docker Encapsulation to Manage Reproducibility and Resource Limitation:**
           - **Docker** is used to encapsulate the execution environment, ensuring reproducibility and resource limitation. Each algorithm is encapsulated in a Docker image, and the pipeline is executed in a container. This approach ensures that the pipeline is executed in a controlled environment with limited resources and that the results are _reproducible_.
           - **Aggregating Metrics** is crucial and requires significant modeling effort. 
           - **Tasks are considered idempotent**, ensuring that repeated executions produce the same outcome. Intermediate results are saved to prevent redundant task executions within workflows. The scheduler handles task dependencies to maintain the correct execution order of workflows, thus avoiding unnecessary re-executions. Users only need to declare the pipelines they wish to execute, with dependency management handled seamlessly in the background.
      - [Günther Jungbluth'report (French)]  **Embracing Errors and Monitoring for Enhanced Learning** Detecting and tracking errors among numerous results is pivotal for extracting valuable insights, such as pinpointing missing algorithm preconditions.  Traditional monitoring tools have proven invaluable: Integrated Prometheus offers real-time monitoring to uphold scheduler functionality.
Grafana provides graphical insights into execution processes, enhancing monitoring capabilities.
           - These safeguards are essential for developers to remain aware of issues and avoid insecure situations. Treating error management as a functional concern within the study of extensive experimentation should be a prerequisite for instilling confidence in the system and viewed as an opportunity for enrichment.
      - [Günther Jungbluth'report (French)] **Event-Driven Scheduler for Automated Experimentation** An event-driven scheduler orchestrates automated pipeline compositions based on new algorithms or datasets, deciding the optimal order to minimize evaluations. 
      - [Günther Jungbluth'report (French)] **Empowering Experimentation with DSL for Pipeline Description** The implementation of a domain-specific language (DSL) has empowered users by simplifying pipeline descriptions and enhancing readability, mastery, and control. This DSL facilitates efficient pipeline articulation and generation, ensuring independence from the target language while promoting operational clarity and control. 
           It was a great tool for Rockflows, but we struggled to promote it, especially when we encountered resistance from data scientists' established practices.
      - [Günther Jungbluth'report (French)] **Integrating External Experiments requires Rigorous Reproducibility Evaluation** We enriched our training dataset by integrating results from our legacy experimentation system into a new metrics registry. This process involved rigorous Reproducibility evaluation to ensure that the added elements were comparable. Additionally, experiments from third parties, like OpenML100, were included after verifying their compatibility with our processes.
  - **_sub-conclusion:_** **_Balancing Research Ambition with Engineering Feasibility in Academic Contexts_**
      - The automation of learning processes is essential for extensive experimentation. It is crucial to ensure valid pipeline compositions, manage resources efficiently, and maintain reproducibility. Docker encapsulation, error monitoring, and event-driven scheduling are key components of this automation. A domain-specific language (DSL) can simplify pipeline descriptions, but promoting it may be challenging. Integrating external experiments requires rigorous reproducibility evaluation. 
      -  Despite all this automation work, at this stage of the project, we have a large code base spread across many repositories, deployed on different virtual machines, and accessible externally. However, we lack the means for proper maintenance or to transition to widespread adoption. This effort serves as a springboard for discussions with industry partners but needs to be more utilized in the development foundation. Today, we understand that we risk losing control over the system, which was not apparent to us at the time, explaining subsequent challenges.
   
  - 
- RF V1
- Lagardere
- Version Nicolas L.
- Version Gunther
- Version Yacine
- Version Yann
