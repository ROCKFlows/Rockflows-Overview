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

- **2016** - [**Comparison of Workflows: a Step Further**](https://github.com/ROCKFlows/experiments-public/tree/master)  
   The questions focus on predicting key performance metrics (accuracy, execution time, and memory usage) of machine learning workflows on user datasets without undergoing the evaluation phase.
    - **_Lessons Learned:_**  
      -  Comparing workflows is not about testing if one metric has a better value, whether once or on average, but **about assessing if there is a significant difference**. Consequently, it is more interesting to build classes of algorithms for a given problem and metric, which requires storing a large number of results and computations.  
      - To evaluate a workflow, it is essential to master the evaluation processes, notably by reproducing not only the experiment but also by conducting it on the same data split.   
      - Preprocessing has a significant impact; it is not about comparing algorithms but **comparing workflows.**  
      -  Metadata dependencies seem difficult/impossible to identify through logical patterns.
    - **_Publications:_**
        - [Luca Parisi'report, Master 2, Ubinet, 2016](./docs/reports/2016_Parisi_tesis.pdf)  
      
- **2016** - [**Towards a software product line for machine learning workflows**](https://github.com/ROCKFlows/rockflows.github.io.git)
    - Repositories
      - **[Main repository](https://github.com/ROCKFlows/rockflows.github.io.git)**
      - [CORE](https://github.com/ROCKFlows/core)
      - [SPLAR](https://github.com/ROCKFlows/splar-fm-reasoner) A feature model reasoner adapted to the needs of the project.
      - [WS to configure FM](https://github.com/ROCKFlows/ws-fm-configuration)
      - [FM as excel sheet](https://github.com/ROCKFlows/ui-fm-to-excel-metadata)
      - ... so many !!
    - **_Publications:_**
      - [Camillieri, C., Parisi, L., Blay-Fornarino, M., Precioso, F., Riveill, M., & Cancela-Vaz, J. (2016, October). Towards a software product line for machine learning workflows: Focus on supporting evolution. In 10th Workshop on Models and Evolution co-located with ACM/IEEE 19th International Conference on Model Driven Engineering Languages and Systems (MODELS 2016).](https://scholar.archive.org/work/qkyqja53pzh55betygpxctx5te/access/wayback/http://ceur-ws.org/Vol-1706/paper9.pdf)
      - [Camillieri, C.,  Blay-Fornarino, M., Precioso, F., Riveill, M. (2016). Request your Own Knowledge Flows (ROCKFlows)](https://github.com/ROCKFlows/rockflows-papers/blob/master/cnrs-innovatives-bigdata-16/poster.pdf)


- **2017** - [**Learning from experiments on Machine Learning Workflows**](https://github.com/ROCKFlows/pfe-expe-learning)  
  As we cannot predict performances from a logic approach, we deviate to the construction of a Meta-Learning system. The theoretic model we have designed is focused on supervised classification problems, although it can be extended to unsupervised or supervised regression problems. We used the results of different Machine Learning experiments, precisely the results of 1086 workflows (composed of 16 pre-processing techniques, 68 classifiers, and 10 parameter strategies) tested over 101 datasets from the UCI repository. This input data was processed to produce the meta-datasets, with which we trained different sub-models to predict three properties: accuracy, total time, and model size.
    - **_Lessons Learned:_**
        -  **Meta-Feature selection and extraction:** Based on the learning phases, we developed a module to extract the 48 most representative meta-features of a given dataset, which influence accuracy. It should be noted that the most significant meta-features vary depending on the workflow. We used these meta-features for prediction by leveraging the similarities between the meta-features of the given dataset and those of datasets already in the Meta-Learning system. Calculating meta-features is not free, and selecting the most impactful meta-features is necessary to reduce the computational load.
        - **Scalability of the Meta-Learning Model:**
          We focused on designing a highly scalable Meta-Learning model that does not require additional computations before adding a new instance to the knowledge base. So, we enhanced scalability by using regression algorithms instead of classification ones and rejected online learning as we found no incremental learning algorithm for regression in the literature that performs as well as its batch learning counterpart. However, after multiple experiments, we used one sub-model L_meta i,j for each classifier i and property j. For scalability purposes, we included preprocessing techniques and other workflow steps (e.g., parameter strategy) in the meta-features.
    - **_Sub-conclusion:_** **_Recognizing the True Scale of Computational Demands in Research_**
        -  Beyond the limitations related to the number of datasets used and the predefined workflows, it became evident that, in line with autoML research, the required learning processes, i.e., the experiments needed to achieve our goals, exceeded the reasonable capacities of the computing grids at our disposal.
        - Ultimately, (i) we were not truly learning by merely predicting performance without gaining real insights, and (ii) to avoid learning on new datasets, we needed to train on a large number of datasets.
    - **_Publications:_**
        -  [Miguel Fabián ROMERO RONDÓN'report, Master 2, Ubinet, 2017](./docs/reports/2017_Romero-Report-Internship.pdf)
        - [Duffau, C., Camillieri, C., & Blay-Fornarino, M. (2017). Improving confidence in experimental systems through automated construction of argumentation diagrams. ICEIS 2017 - Proceedings of the 19th International Conference on Enterprise Information Systems, 2.](https://hal.science/hal-01678797/document)  


- **2018** -**Automating the Learning Processes for Extensive Experimentation**  
   Given the large number of experiments required, it is essential to automate the learning processes. This automation includes composing pipelines, training on appropriate datasets, and recording measurements. Since it is not sufficient to compare a single set of measurements but rather to compare sets of measurements, it is also necessary to automate ranking and meta-learning processes. To ensure precision, we must maintain consistency in execution and measurement environments. Additionally, considering our limited resources, we aim to reuse data preparation and implement a form of crowd experimenting to add new experiments to our knowledge base at a constrained cost.
    - **_Lessons Learned:_**
        -  **Automating valid Pipeline Composition based on Constraints and Graph Representation** enhances the automation of learning processes, ensuring valid ML workflow compositions while efficiently managing complexity.
            - **Data-centric constraints** are expressed as pre- and post-conditions on algorithms relative to metadata. For example, a pipeline like "_NumericTransformationToNominal; NumericNormalization; SVM"_ is invalid because the preprocessing step _NumericNormalization_ requires numeric data, which the previous algorithm removes.
            - **Pipeline-Centric Constraints** define a partial order between algorithms. For instance, the constraint "_Missing value removal must always precede normalization_" invalidates the pipeline "_Normalization; ...; MissingValueRemoval; SVM._" These constraints significantly reduce the combinatorial complexity between datasets and pipelines.
            - A **Graph structure** is used to handle the mass of compositions, incremental addition of new algorithms, and strategic graph traversal for launching experiments. We were unable to design it using constraint solvers, as they never scaled effectively.
              Ensuring Consistent and Scalable Experimentation with Docker and Efficient Resource Management
        -  **Leveraging Docker Encapsulation to Manage Reproducibility and Resource Limitation:**
            - **Docker** is used to encapsulate the execution environment, ensuring reproducibility and resource limitation. Each algorithm is encapsulated in a Docker image, and the pipeline is executed in a container. This approach ensures that the pipeline is executed in a controlled environment, with limited resources, and that the results are _reproducible_.
            - **Aggregating Metrics** is crucial and requires significant modeling effort.
            - **Tasks are considered as idempotent**, ensuring that repeated executions produce the same outcome. Intermediate results are saved to prevent redundant task executions within workflows. The scheduler handles task dependencies to maintain the correct execution order of workflows, thus avoiding unnecessary re-executions. Users only need to declare the pipelines they wish to execute, with dependency management handled seamlessly in the background.
        -  **Embracing Errors and Monitoring for Enhanced Learning** Detecting and tracking errors among numerous results is pivotal for extracting valuable insights, such as pinpointing missing algorithm preconditions.  Traditional monitoring tools have proven invaluable: Integrated Prometheus offers real-time monitoring to uphold scheduler functionality.
          Grafana provides graphical insights into execution processes, enhancing monitoring capabilities.
            - These safeguards are essential for developers to remain aware of issues and avoid insecure situations. Treating error management as a functional concern within the study of extensive experimentation should be a prerequisite for instilling confidence in the system and viewed as an opportunity for enrichment.
        -  **Event-Driven Scheduler for Automated Experimentation** An event-driven scheduler orchestrates automated pipeline compositions based on new algorithms or datasets, deciding the optimal order to minimize evaluations.
        - **Empowering Experimentation with DSL for Pipeline Description** The implementation of a domain-specific language (DSL) has empowered users by simplifying pipeline descriptions and enhancing readability, mastery, and control. This DSL facilitates efficient pipeline articulation and generation, ensuring independence from the target language while promoting operational clarity and control.
            - It was a great tool for Rockflows, but we struggled to promote it, especially encountering resistance from data scientists' established practices.
        -  **Integrating External Experiments requires Rigorous Reproducibility Evaluation** We enriched our training dataset by integrating results from our legacy experimentation system into a new metrics registry. This process involved rigorous Reproducibility evaluation to ensure that the added elements were comparable. Additionally, experiments from third parties, like OpenML100, were included after verifying their compatibility with our processes.
    - **_sub-conclusion:_**     **Balancing Research Ambition with Engineering Feasibility in Academic Contexts**
        - The automation of learning processes is essential for extensive experimentation. It is crucial to ensure valid pipeline compositions, manage resources efficiently, and maintain reproducibility. Docker encapsulation, error monitoring, and event-driven scheduling are key components of this automation. A domain-specific language (DSL) can simplify pipeline descriptions, but promoting it may be challenging. Integrating external experiments requires rigorous reproducibility evaluation.
        -  Despite all this automation work, at this stage of the project, we have a large code base spread across many repositories, deployed on different virtual machines, and accessible externally. However, we lack the means for proper maintenance or to transition to widespread adoption. This effort serves as a springboard for discussions with industry partners but needs to be more utilized in the development foundation. Today, we understand that we risk losing control over the system, which was not apparent to us at the time, explaining subsequent challenges.
        - Le domaine évolue de plus en plus vite, il faut trouver un moyen de capturer la connaissance de manière plus "automatique" mais sans basculer dans le meta-learning.
        - On est conscient que le projet devient gros on tente une [exploration des dépendances](https://rimel-uca.github.io/chapters/2019/architecture-analysis-rockflows-2019/contents)
    - **_Publications:_**
        - [Günther Jungbluth'report (French), Engineer, Polytech Nice Sophia, 2018](./docs/reports/2018_Ghunter.pdf)
        - [Benni, B., Blay Fornarino, M., Mosser, S., Precisio, F., & Jungbluth, G. When DevOps meets meta-learning: A portfolio to rule them all. Proceedings - 2019 ACM/IEEE 22nd International Conference on Model Driven Engineering Languages and Systems Companion, MODELS-C 2019, 605–612](https://doi.org/10.1109/MODELS-C.2019.00092)
        - [Blay-Fornarino, M., Jungbluth, G., & Mosser, S. (2018). Applying DevOps to Machine Learning: ROCKFlows, a Story from the Trenches.](https://www.academia.edu/download/104996357/document.pdf)
        - [Etude au niveau Master 2 : Comment est organisé le développement d’un projet Open Source de Machine Learning ? ]https://rimel-uca.github.io/chapters/2018/machine-learning-explorations-2018/comment-est-organise-le-developpement-dun-projet-open-source-de-machine-learning

- Interface web un element clef rapport de Joel -- RF V1 + travail de simon + eddy + .... un composant réutilisable...
  - **_sub-conclusion:_**
    - On ne peut pas gérer les changements de verions d'outils tels que angular ! 

- Version Mireille : impliqué les data-scientists;  Au coueur des feature Models
- Lagardere
- Version Nicolas L.

- **2020** - **[Deriving New Insights from ML Workflow Modeling](https://github.com/ROCKFlows/FromMLWFConfigurationToBPMN)**
  While we had established the basics of generating valid ML pipelines by configuring a feature model in a predefined order, we embarked on a journey to facilitate pipeline construction for data scientists using a novel approach to configuration. This approach not only aimed to make the process more intuitive but also to provide new insights through more user-friendly tools, such as pipeline modeling. Despite having a dedicated language at this stage, we chose to explore the path of graphical modeling, aligning with the BPMN standard, to bring a new perspective.
  Beyond code generation, we faced two challenges:  (i) extending the BPMN language to allow the input of additional, coherent information helpful in enriching our knowledge base (e.g., new 'qualified' algorithms and constraints on orders) ; (ii) automatically updating our knowledge base with new information and managing potential conflicts.
    - **_Lessons Learned:_**
        -   **Custom Merging Approach Required** A classical merge approach is unsuitable as individuals can perceive each algorithm differently. We utilized our access to the Feature Model (FM) structure to implement an ad-hoc algorithm, which still needs to be fully validated.
        -  **Dual Formalization for Algorithm Constraints** Understanding the complexities involved, we adopted a dual formalization for algorithm constraints. This thorough approach, driven by the algorithms and the organization of the pipelines, was crucial in managing the intricacies of the project.
    - **_sub-conclusion:_** **Challenges of Managing Growing Codebases**
      We are increasingly dealing with large volumes of code, and despite significant efforts in structuring, we are beginning to see projects proliferate. This project was initiated from scratch by a second-year undergraduate student for pedagogical purposes and is likely to be repeated, leading to our results becoming increasingly scattered.   
    - **_Publications:_**  
        - [Nicolas L. rapport(French), DUT, 2020](./docs/reports/2020_rapport_NicolasLacroix.pdf)
      
- **2020 ** - ** Extraction automatique Des bibliothques de ML aux FM** depot de Mireille sur weka?
    - **_Publications:_**
        - [Etude au niveau Master 2 : Comment les bibliothèques de codes de Machine Learning évoluent-elles ?, 2020](https://rimel-uca.github.io/chapters/2020/MLAndEvolution/model2020)
        - [Etude au niveau Master 2 : Extraire les préconditions des codes de RapidMiner,2022]!https://rimel-uca.github.io/chapters/2022/Extraire%20les%20pr%C3%A9conditions%20des%20codes%20de%20RapidMiner/content)
    -
- **2021-2024** - **Evolvable SPL management**
    - **_Lessons Learned:_**
    - **_Publications:_**
        -  [Amraoui, Y. el, Blay-Fornarino, M., Collet, P., Precioso, F., & Muller, J. (2022). Evolvable SPL management with partial knowledge: an application to anomaly detection in time series. Proceedings of the 26th ACM International Systems and Software Product Line Conference-Volume A, 222–233.](https://hal.science/hal-03811038/document)
        -  Yassine El Amraoui, Phd  2024

- **2023** - (In progress) [**Taming the Diversity of Computational Notebooks**](https://src.koda.cnrs.fr/users/sign_in)In response to the practices of data scientists, who typically prefer starting from notebook analysis and acknowledging the industrial challenge of finding suitable notebooks that meet business requirements (beyond just data), we focused on retrieving "adapted" notebooks based on the expression of business requirements and automatic analysis of datasets.
    - **_Lessons Learned:_**
        - nécessité d'adapter le processus même d'analyse des données pour en extraire les méta-data et les transformer en features puis en feature booleene.
        - pas si facile de faire comprendre à la communauté des SPL que les notebooks peuvent être vu comme des artefacts de SPL (produits/clones de code) et que de représenter les produits dans un FM peut aider à retrouver "facilement" des produits existants.
    - **_Publications:_**
        - [Brault, Y., El Amraoui, Y., Blay-Fornarino, M., Collet, P., Jaillet, F., & Precioso, F. (2023, August). Taming the Diversity of Computational Notebooks. In Proceedings of the 27th ACM International Systems and Software Product Line Conference-Volume A (pp. 27-33).](https://hal.science/hal-04247860/file/tamingTheDiversity-SPLC2023.pdf)
        - [Etude au niveau Master 2 : Qualité logicielle dans les notebooks Jupyter, 2023](https://rimel-uca.github.io/chapters/2023/Qualit%C3%A9%20logicielle%20dans%20les%20notebooks%20Jupyter/content)
        - [Etude au niveau Master 2 : Quelle qualité logicielle dans les codes des notebooks?,2923](https://rimel-uca.github.io/chapters/2023/Jupyter%20Notebooks%20et%20bonnes%20pratiques_entre%20conventions%20implicites%20et%20besoin%20de%20formalisation/content)

- **2024** -(In progress) vers MLOPS et LLMs
    - **_Lessons Learned:_**
    - **_Publications:_**
        - [Etude au niveau Master 2 : Are Data scientists embracing DevOps principles for Model versioning ?, 2024](https://rimel-uca.github.io/chapters/2024/Are%20Data%20scientists%20embracing%20DevOps%20principles%20for%20Model%20versioning%20%3F/content)
        - [Etude au niveau Master 2 : De DevOps à MLops : Quelle place pour MLFlow ?, 2024](https://rimel-uca.github.io/chapters/2024/Tra%C3%A7abilit%C3%A9%20des%20exp%C3%A9riences%20par%20MLFlow/content)
        - [Etude au niveau Master 2 : Abstraction de l’utilisation de LangChain, 2024](https://rimel-uca.github.io/chapters/2024/Abstraction%20de%20l'utilisation%20de%20LangChain/content)
        - [Etude au niveau Master 2 : Variabilité de Langchain dans l’implémentation de chatbots, 2024](https://rimel-uca.github.io/chapters/2024/Variabilit%C3%A9%20de%20LangChain%20dans%20l'impl%C3%A9mentation%20de%20chatbots/content)
- Version Yacine

