# Introducing MLOps
<img src="img/book_cover.png" alt="cover" width="200"/>


## Table of Contents
1. [Why Now and Challenges](#chapter-1---why-now-and-challenges)
2. [People of MLOps](#chapter-2---people-of-mlops)
3. [Key MLOps Features](#chapter-3---key-mlops-features)
4. [Developing Models](#chapter-4---developing-models)
5. [Preparing for Production](#chapter-5---preparing-for-production)
6. [Deploying to Production](#chapter-6---deploying-to-production)
7. [Monitoring and Feedback Loop](#chapter-7---monitoring-and-feedback-loop)


## Chapter 1 - Why Now and Challenges <a name="chapter_1"></a>

Machine learning operations (**MLOps**) is quickly becoming a critical component of successful data science project deployment in the enterprise.

It’s a process that helps organizations and business leaders generate long-term value and reduce risk associated with data science, machine learning, and AI initiatives. 

### Defining MLOps and Its Challenges

At its core, MLOps is the standardization and streamlining of machine learning life cycle management.

<img src="img/ml_lifecycle.png" alt="ml lifecycle" width="350"/>

There are three key reasons that managing machine learning life cycles at scale is challenging:

- There are many dependencies. 
    - Not only is data constantly changing, but business needs shift as well.
- Not everyone speaks the same language. 
    - Even though the machine learning life cycle involves people from the business, data science, and IT teams, none of these groups are using the same tools or even, in many cases, share the same fundamental skills to serve as a baseline of communication.
- Data scientists are not software engineers. 
    - Most are specialized in model building and assessment, and they are not necessarily experts in writing applications.

Below, the representation of a ML lifecycle in an organization today.

<img src="img/ml_lifecycle_2.png" alt="ml lifecycle 2" width="500"/>

If the definition (or even the name MLOps) sounds familiar, that’s because it pulls heavily **from the concept of DevOps**, which streamlines the practice of software changes and updates. Indeed, the two have quite a bit in common. For example, they both center around:

- Robust automation
- Trust between teams
- The idea of collaboration and increased communication between teams
- The end-to-end service life cycle (build, test, release)
- Prioritizing continuous delivery and high quality

Yet there is one critical **difference** between MLOps and DevOps that makes the latter not immediately transferable to data science teams: deploying software code into production is fundamentally different than deploying machine learning models into production.
While software code is relatively static, data is always changing,
which means machine learning models are constantly learning and adapting.

### MLOps to Mitigate Risk

MLOps is important to any team that has even one model in production because, depending on the model, continuous performance monitoring and adjusting is essential.

By allowing safe and reliable operations, MLOps is key in mitigating the risks induced by the use of ML models. However, MLOps practices do come at a cost, so a proper **cost-benefit evaluation** should be performed for each use case.

#### Risk Assessment

When it comes to machine learning models, risks vary widely. For example, the stakes are much lower for a recommendation engine used once a month to decide which marketing offer to send a customer than for a travel site whose pricing and revenue depend on a machine learning model. 

Therefore, when looking at MLOps as a way to mitigate risk, an analysis should cover:
- The risk that the model is unavailable for a given period of time
- The risk that the model returns a bad prediction for a given sample
- The risk that the model accuracy or fairness decreases over time
- The risk that the skills necessary to maintain the model (i.e., data science talent) are lost

Below, a table that helps decision makers with quantitative risk analysis.

<img src="img/risk_matrix.png" alt="risk matrix" width="400"/>

#### MLOps for Scale

Good MLOps practices will help teams at a minimum:
- Keep track of versioning, especially with experiments in the design phase
- Understand whether retrained models are better than the previous versions (and promoting models to production that are performing better)
- Ensure (at defined periods—daily, monthly, etc.) that model performance is not degrading in production


## Chapter 2 - People of MLOps <a name="chapter_2"></a>

### Overview 

<img src="img/people_table.png" alt="people table" width="650"/>

### Subject Matter Experts

The first profile to consider as part of MLOps efforts is the subject matter experts (SMEs); after all, the ML model life cycle starts and ends with them. While the dataoriented profiles (data scientist, engineer, architect, etc.) have expertise across many areas, they tend to lack a deep understanding of the business and the problems or questions that need to be addressed using machine learning.

Subject matter experts usually come to the table—or, at least, they should come to the table—with clearly defined goals, business questions, and/or key performance indicators (KPIs) that they want to achieve or address.

Subject matter experts have a role to play not only at the beginning of the ML model life cycle, but at the end (post-production) as well. Oftentimes, to understand if an ML model is performing well or as expected, data scientists need subject matter experts to close the feedback loop because traditional metrics (accuracy, precision, recall, etc.) are not enough.

### Data Scientists

From the very beginning, data scientists need to be involved with subject matter experts, understanding and helping to frame business problems in such a way that they can build a viable machine learning solution.

Following deployment, data scientists’ roles include constantly assessing model quality to ensure the way it’s working in production answers initial business questions or needs.

### Data Engineers

Data pipelines are at the core of the ML model life cycle, and data engineers are, in turn, at the core of data pipelines.

The role of data engineers in the life cycle is to optimize the retrieval and use of data to eventually power ML models. Generally, this means working closely with business teams, particularly subject matter experts, to identify the right data for the project at hand and possibly also prepare it for use. On the other end, they work closely with data scientists to resolve any data plumbing issues that might cause a model to behave undesirably in production.

Data engineers require not only visibility into the performance of all models deployed in production, but the ability to take it one step further and directly drill down into individual data pipelines to address any underlying issues.

### Software Engineers

ML models aren’t just standalone experiments; the machine learning code, training, testing, and deployment have to fit into the Continuous Integration/Continuous Delivery (CI/CD) pipelines that the rest of the software is using.

The ML model was built by the data scientist, but to integrate it into the larger functioning of the site, software engineers will necessarily need to be involved. 

Similarly, software engineers are responsible for the maintenance of the website as a whole, and a large part of that includes the functioning of the ML models in production.

### DevOps

DevOps teams have two primary roles in the ML model life cycle. First, they are the people conducting and building operational systems as well as tests to ensure security, performance, and availability of ML models. Second, they are responsible for CI/CD pipeline management.

### Machine Learning Architect

Machine learning architects play a critical role in the ML model life cycle, ensuring a scalable and flexible environment for model pipelines. In addition, data teams need their expertise to introduce new technologies (when appropriate) that improve ML model performance in production.

As they have a strategic, tactical role, they need an overview of the situation to identify bottlenecks and use that information to find long-term improvements. Their role is one of pinpointing possible new technology or infrastructure for investment, not necessarily operational quick fixes that don’t address the heart of the scalability of the system.

## Chapter 3 - Key MLOps Features <a name="chapter_3"></a>

### Model Development

#### Establishing Business Objectives

The process of developing a machine learning model typically starts with a business objective, which can be as simple as reducing fraudulent transactions to < 0.1% .

Business objectives naturally come with performance targets, technical infrastructure requirements, and cost constraints; all of these factors can be captured as key performance indicators, or KPIs, which will ultimately enable the business performance of models in production to be monitored.

#### Data Sources and Exploratory Data Analysis

With clear business objectives defined, it is time to bring together subject matter experts and data scientists to begin the journey of developing the ML model.

Key **questions** for finding **data to build ML models** include:

- What relevant datasets are available?
- Is this data sufficiently accurate and reliable?
- How can stakeholders get access to this data?
- What data properties (known as features) can be made available by combining multiple sources of data?
- Will this data be available in real time?
- Is there a need to label some of the data with the “ground truth” that is to be predicted, or does unsupervised learning make sense? If so, how much will this cost in terms of time and resources?
- What platform should be used?
- How will data be updated once the model is deployed?
- Will the use of the model itself reduce the representativeness of the data?
- How will the KPIs, which were established along with the business objectives, be measured?

The **constraints of data governance** bring even more **questions**, including:

- Can the selected datasets be used for this purpose?
- What are the terms of use?
- Is there personally identifiable information (PII) that must be redacted or anonymized?
- Are there features, such as gender, that legally cannot be used in this business context?
- Are minority populations sufficiently well represented that the model has equivalent performances on each group?

Since data is the essential ingredient to power ML algorithms, it always helps to build an understanding of the patterns in data before attempting to train models. Exploratory data analysis (EDA) techniques can help build hypotheses about the data, identify data cleaning requirements, and inform the process of selecting potentially
significant features. 

EDA can be carried out visually for intuitive insight and statistically if more rigor is required.

#### Feature Engineering and Selection

EDA leads naturally into feature engineering and feature selection. Feature engineering is the process of taking raw data from the selected datasets and transforming it into “features” that better represent the underlying problem to be solved. “Features” are arrays of numbers of fixed size, as it is the only object that ML algorithms understand.

Feature engineering includes data cleansing, which can represent the largest part of an ML project in terms of time spent.

#### Training and Evaluation

After data preparation by way of feature engineering and selection, the next step is training. The process of training and optimizing a new ML model is iterative; several algorithms may be tested, features can be automatically generated, feature selections may be adapted, and algorithm hyperparameters tuned. In addition to—or in many cases because of—its iterative nature, training is also the most intensive step of the ML model life cycle when it comes to computing power.

#### Reproducibility

The aim in ML is to save enough information about the environment the model was developed in so that the model can be reproduced with the same results from scratch.

### Productionalization and Deployment

Productionalizing and deploying models is a key component of MLOps that presents an entirely different set of technical challenges than developing the model. It is the domain of the software engineer and the DevOps team, and the organizational challenges in managing the information exchange between the data scientists and these teams must not be underestimated.

#### Containerization

Containerization is an increasingly popular solution to the headaches of dependencies when deploying ML models. Container technologies such as Docker are lightweight alternatives to virtual machines, allowing applications to be deployed in independent, self-contained environments, matching the exact requirements of each model.

#### Model Deployment Requirements

In customer-facing, mission-critical use cases, a more robust CI/CD pipeline is required. This typically involves:

1. Ensuring all coding, documentation and sign-off standards have been met
2. Re-creating the model in something approaching the production environment
3. Revalidating the model accuracy
4. Performing explainability checks
5. Ensuring all governance requirements have been met
6. Checking the quality of any data artifacts
7. Testing resource usage under load
8. Embedding into a more complex application, including integration tests

In heavily regulated industries (e.g., finance and pharmaceuticals), governance and regulatory checks will be extensive and are likely to involve manual intervention. The desire in MLOps, just as in DevOps, is to automate the CI/CD pipeline as far as possible. This not only speeds up the deployment process, but it enables more extensive regression testing and reduces the likelihood of errors in the deployment.

### Monitoring

Once a model is deployed to production, it is crucial that it continue to perform well over time. But good performance means different things to different people, in particular to the DevOps team, to data scientists, and to the business.

#### DevOps Concerns

The concerns of the DevOps team are very familiar and include questions like:
- Is the model getting the job done quickly enough?
- Is it using a sensible amount of memory and processing time?

#### Data Scientist Concerns

The data scientist is interested in monitoring ML models for a new, more challenging reason: they can degrade over time.

The real world doesn’t stand still: the training data used to build a fraud detection model six months ago won’t reflect a new type of fraud that has started to occur in the last three months.

But first, how can data scientists tell a model’s performance is degrading? It’s not always easy. There are two common approaches, one based on ground truth and the other on input drift.

##### Ground truth

The ground truth, put simply, is the correct answer to the question that the model was asked to solve—for example, “Is this credit card transaction actually fraudulent?”

In knowing the ground truth for all the predictions a model has made, one can judge how well that model is performing.

##### Input drift

Input drift is based on the principle that a model is only going to predict accurately if the data it was trained on is an accurate reflection of the real world. So if a comparison of recent requests to a deployed model against the training data shows distinct differences, then there is a strong likelihood that the model performance is compromised.

This is the basis of input drift monitoring. The beauty of this approach is that all the data required for this test already exists, so there is no need to wait for ground truth or any other information.

#### Business Concerns

The business has a holistic outlook on monitoring, and some of its concerns might include questions like:
- Is the model delivering value to the enterprise?
- Do the benefits of the model outweigh the cost of developing and deploying it? (And how can we measure this?)

### Iteration

In some fast-moving business environments, new training data becomes available every day. Daily retraining and redeployment of the model are often automated to ensure that the model reflects recent experience as closely as possible.

Questions to be answered:
- Does the new training data look as expected? Automated validation of the new data through predefined metrics and checks is essential.
- Is the data complete and consistent?
- Are the distributions of features broadly similar to those in the previous training set? Remember that the goal is to refine the model, not radically change it.

With a new model version built, the next step is to compare the metrics with the current live model version. Doing so requires evaluating both models on the same development dataset, whether it be the previous or latest version.

#### The Feedback Loop

One approach to mitigating this uncertainty is **shadow testing**, where the new model version is deployed into the live environment alongside the existing model. All live scoring is handled by the incumbent model version, but each new request is then scored again by the new model version and the results logged, but not returned to the requestor. Once sufficient requests have been scored by both versions, the results can be compared statistically. Shadow scoring also gives more visibility to the SMEs on the future versions of the model and may thus allow for a smoother transition.


## Chapter 4 - Developing Models <a name="chapter_4"></a>

<img src="img/ml_lifecycle_3.png" alt="ml lifecycle" width="550"/>

### Required Components

Building a machine learning model requires many components as outlined in the table below.

<img src="img/ml_components.png" alt="ml components" width="550"/>

### Different ML Algorithms, Different MLOps Challenges

<img src="img/algorithms_challenges.png" alt="algorithm challenges" width="550"/>

### Data Exploration

The processes can include:
- Documenting how the data was collected and what assumptions were already made
- Looking at summarizing statistics of the data: What is the domain of each column? Are there some rows with missing values? Obvious mistakes? Strange outliers? No outliers at all?
- Taking a closer look at the distribution of the data
- Cleaning, filling, reshaping, filtering, clipping, sampling, etc.
- Checking correlations between the different columns, running statistical tests on some subpopulations, fitting distribution curves
- Comparing that data to other data or models in the literature: Is there some usual information that seems to be missing? Is this data comparably distributed?

Of course, domain knowledge is required to make informed decisions during this exploration.

### Feature Engineering and Selection

The table below provides examples of how features may be
engineered:

<img src="img/feature_engineering.png" alt="feature engineering" width="550"/>

Ultimately, most ML algorithms require a table of numbers as input, each row representing a sample, and all samples coming from the same dataset. When the input data is not tabular, data scientists can use other tricks to transform it.

#### How Feature Selection Impacts MLOps Strategy

When it comes to feature creation and selection, the question of how much and when to stop comes up regularly. Adding more features may produce a more accurate
model, achieve more fairness when splitting into more precise groups, or compensate for some other useful missing information. 

However, it also comes with downsides, all of which can have a significant impact on MLOps strategies down the line:
- The model can become more and more expensive to compute.
- More features require more inputs and more maintenance down the line.
- More features mean a loss of some stability.
- The sheer number of features can raise privacy concerns.

### Experimentation

Goals of experimentation include:
- Finding the best modeling parameters (algorithms, hyperparameters, feature preprocessing, etc.).
- Tuning the bias/variance trade-off for a given training cost to fit that definition of “best.”
- Finding a balance between model improvement and improved computation costs. (Since there’s always room for improvement, how good is good enough?)

### Evaluating and Comparing Models

**Cross-validation**: a scheme in which a test dataset is a holdout (in gray) in order to perform the evaluation. The remaining data is split into three parts to find the best hyperparameter combination by training the model three times with a given combination on each of the blue datasets, and validating its performance on their respective green datasets. The gray dataset is used only once with the best hyperparameter  combination, while the other datasets are used with all of them.

<img src="img/cross_validation.png" alt="cross validation" width="550"/>

### Cross-Checking Model Behavior

- Cross-checking different metrics (and not only the ones on which the model was initially optimized)
- Checking how the model reacts to different inputs—e.g., plot the average prediction (or probability for classification models) for different values of some inputs and see whether there are oddities or extreme variability
- Splitting one particular dimension and checking the difference in behavior and metrics across different subpopulations—e.g., is the error rate the same for males and females?

### Version Management and Reproducibility

With data scientists building, testing, and iterating on several versions of models, they need to be able to keep all the versions straight.

**Version management and reproducibility** address two different needs:
- During the experimentation phase, data scientists may find themselves going back and forth on different decisions, trying out different combinations, and reverting when they don’t produce the desired results. That means having the ability to go back to different “branches” of the experiments—for example, restoring a previous state of a project when the experimentation process led to a dead end.
- Data scientists or others (auditors, managers, etc.) may need to be able to replay the computations that led to model deployment for an **audit** team several years after the experimentation was first done.

**Repeatability** makes debugging much easier (sometimes even simply possible). To this end, all facets of the model need to be documented and reusable, including:

- Assumptions
    - When a data scientist makes decisions and assumptions about the problem at hand, its scope, the data, etc., they should all be explicit and logged so that they can be checked against any new information down the line.
- Randomness
    - A lot of ML algorithms and processes, such as sampling, make use of pseudorandom numbers. Being able to precisely reproduce an experiment, such as for debugging, means to have control over that pseudo-randomness, most often by controlling the “seed” of the generator (i.e., the same generator initialized with the same seed would yield the same sequence of pseudo-random numbers).
- Data
    - To get repeatability, the same data must be available. This can sometimes be tricky because the storage capacity required to version data can be prohibitive depending on the rate of update and quantity. Also, branching on data does not yet have as rich an ecosystem of tools as branching on code.
- Settings
    - This one is a given: all processing that has been done must be reproducible with the same settings.
- Results
    - While developers use merging tools to compare and merge different text file versions, data scientists need to be able to compare in-depth analysis of models (from confusion matrices to partial dependence plots) to obtain models that satisfy the requirements.
- Implementation
    - Ever-so-slightly different implementations of the same model can actually yield different models, enough to change the predictions on some close calls. And the more sophisticated the model, the higher the chances that these discrepancies happen. On the other hand, scoring a dataset in bulk with a model comes with different constraints than scoring a single record live in an API, so different implementations may sometimes be warranted for the same model. But when debugging and comparing, data scientists need to keep the possible differences in mind.
- Environment
    - Given all the steps covered in this chapter, it’s clear that a model is not just its algorithm and parameters. From the data preparation to the scoring implementation, including feature selection, feature encoding, enrichment, etc., the environment in which several of those steps run may be more or less implicitly tied to the results. For instance, a slightly different version of a Python package involved in one step may change the results in ways that can be hard to predict. Preferably, data scientists should make sure that the runtime environment is also repeatable. Given the pace at which ML is evolving, this might require techniques that freeze the computation environments.


## Chapter 5 - Preparing for Production <a name="chapter_5"></a>

<img src="img/prepare_for_prd.png" alt="prepare for prd" width="550"/>

### Runtime Environments

Ideally, **models running in the development environment would be validated and sent as is to production**; this minimizes the amount of adaptation work and improves the chances that the model in production will behave as it did in development. Unfortunately, this ideal scenario is not always possible, and it’s not unheard of that teams finish a long-term project only to realize it can’t be put in production.

#### Adaptation from Development to Production Environments

In terms of adaptation work, on one end of the spectrum, the **development and production platforms are from the same vendor or are otherwise interoperable**, and the dev model can run without any modification in production. In this case, the technical steps required to push the model into production are reduced to a few clicks or commands, and all efforts can be focused on validation.

### Data Access Before Validation and Launch to Production

Another technical aspect that needs to be addressed before validation and launch to production is data access. 

For example, a model evaluating apartment prices may use the average market price in a zip code area; however, the user or the system requesting the scoring will probably not provide this average and would most likely provide simply the zip code, meaning a lookup is necessary to fetch the value of the average.

In some cases, data can be frozen and bundled with the model. But when this is not possible (e.g., if the dataset is too large or the enrichment data needs to always be up to date), the production environment should access a database and thus have the appropriate network connectivity, libraries, or drivers required to communicate with the data storage installed, and authentication credentials stored in some form of production configuration.

#### Final Thoughts on Runtime Environments

Training a model is usually the most impressive computation, requiring a high level of software sophistication, massive data volumes, and high-end machines with powerful GPUs. But in the whole life cycle of a model, there is a good chance that most of the compute is spent at inference time (even if this computation is orders of magnitude simpler and faster). This is because a model is trained once and can be used billions of times for inference.

### Model Risk Evaluation

Before putting a model in production (and in fact constantly from the beginning of the machine learning project), teams should ask the uncomfortable questions:
- What if the model acts in the worst imaginable way?
- What if a user manages to extract the training data or the internal logic of the model?
- What are the financial, business, legal, safety, and reputational risks?

For high-risk applications, it is essential that the whole team (and in particular the engineers in charge of validation) be fully aware of these risks so that they can design the validation process appropriately and apply the strictness and complexity appropriate for the magnitude of the risks.

#### The Origins of ML Model Risk

ML model risk originates essentially from:
- Bugs, errors in designing, training, or evaluating the model (including data prep)
- Bugs in the runtime framework, bugs in the model post-processing/conversion, or hidden incompatibilities between the model and its runtime
- Low quality of training data
- High difference between production data and training data
- Expected error rates, but with failures that have higher consequences than expected
- Misuse of the model or misinterpretation of its outputs
- Adversarial attacks
- Legal risk originating in particular from copyright infringement or liability for the model output
- Reputational risk due to bias, unethical use of machine learning, etc.

The probability of materialization of the risk and its magnitude can be amplified by:
- Broad use of the model
- A rapidly changing environment
- Complex interactions between models

### Quality Assurance for Machine Learning

QA for machine learning does not occur only at the final validation stage; rather, it should accompany all stages of model development.

#### Key Testing Considerations

Obviously, model testing will consist of applying the model to carefully curated data and validating measurements against requirements. How the data is selected or generated as well as how much data is required is crucial, but it will depend on the problem tackled by the model.

Metrics must be collected on both statistical (accuracy, precision, recall, etc.) as well as computational (average latency, 95th latency percentile, etc.) aspects, and the test scenarios should fail if some assumptions on them are not verified.

##### Subpopulation Analysis and Model Fairness

It can be useful to design test scenarios by splitting data into **subpopulations** based on a “sensitive” variable (that may or may not be used as a feature of the model). This is how **fairness** (typically between genders) is evaluated.

### Reproducibility and Auditability

In general, **reproducibility** in MLOps also involves the ability to easily rerun the exact same experiment.

**Auditability** is related to reproducibility, but it adds some requirements. For a model to be auditable, it must be possible to access the full history of the ML pipeline from a central and reliable storage and to easily fetch metadata on all model versions including:
- The full documentation
- An artifact that allows running the model with its exact initial environment
- Test results, including model explanations and fairness reports
- Detailed model logs and monitoring metadata


## Chapter 6 - Deploying to Production <a name="chapter_6"></a>

Business leaders view the rapid deployment of new systems into production as key to maximizing business value. But this is only true if deployment can be done smoothly and at low risk.

<img src="img/deploy_to_prd.png" alt="deploy to prd" width="550"/>

### CI/CD Pipelines

CI/CD is a common acronym for continuous integration and continuous delivery (or put more simply, deployment).

CI/CD concepts apply to traditional software engineering, but they apply just as well to machine learning systems and are a critical part of MLOps strategy. After successfully
developing a model, a data scientist should push the code, metadata, and documentation to a central repository and trigger a CI/CD pipeline. An example of such pipeline could be:

1. Build the model
    - Build the model artifacts
    - Send the artifacts to long-term storage
    - Run basic checks (smoke tests/sanity checks)
    - Generate fairness and explainability reports
2. Deploy to a test environment
    - Run tests to validate ML performance, computational performance
    - Validate manually
3. Deploy to production environment
    - Deploy the model as canary
    - Fully deploy the model

Generally speaking, an **incremental approach to building a CI/CD pipeline** is preferred: a simple or even naïve workflow on which a team can iterate is often much better than starting with complex infrastructure from scratch.

This means the best path forward is **starting** from a **simple** (but fully functional) CI/CD workflow and introducing additional or more sophisticated steps along the way as quality or scaling challenges appear.

### Building ML Artifacts

The goal of a continuous integration pipeline is to avoid unnecessary effort in merging the work from several contributors as well as to detect bugs or development conflicts as soon as possible. The very first step is using centralized version control systems (unfortunately, working for weeks on code stored only on a laptop is still quite common).

The most common **version control system** is **Git**, an open source software initially developed to manage the source code for the Linux kernel. The majority of software engineers across the world already use Git, and it is increasingly being adopted in scientific computing and data science. It allows for maintaining a clear history of changes, safe rollback to a previous version of the code, multiple contributors to work on their own branches of the project before merging to the main branch, etc.

While **Git is appropriate for code**, it was not designed to store other types of assets common in data science workflows, such as large binary files (for example, trained model weights), or to version the data itself. **Data versioning is a more complex topic** with numerous solutions, including Git extensions, file formats, databases, etc.

### What’s in an ML Artifact ?

Once the code and data is in a centralized repository, a testable and deployable bundle of the project must be built. These bundles are usually called artifacts in the context of CI/CD. Each of the following elements needs to be bundled into an artifact that goes through a testing pipeline and is made available for deployment to production:
- Code for the model and its preprocessing
- Hyperparameters and configuration
- Training and validation data
- Trained model in its runnable form
- An environment including libraries with specific versions, environment variables, etc.
- Documentation
- Code and data for testing scenarios

### The Testing Pipeline

- A test on a fixed (not automatically updated) **dataset with simple data** and not too-restrictive performance thresholds can be executed first and called “base case.”
- Then, a number of **datasets that each have one specific oddity** (missing values, extreme values, etc.) could be used with tests appropriately named so that the test report immediately shows the kind of data that is likely to make the model fail.
- Then, an essential part of model validation is **testing on recent production data**.

The most widespread tool for software engineering **continuous integration** is **Jenkins**, a very flexible build system that allows for the building of CI/CD pipelines regardless of the programming language, testing framework, etc. Jenkins can be used in data science to orchestrate CI/CD pipelines, although there are many other options.

### Deployment Strategies

To understand the details of a deployment pipeline, it is important to distinguish among **concepts** often used inconsistently or interchangeably.

- Integration
    - The process of merging a contribution to a central repository (typically **merging a Git feature branch** to the main branch) and **performing more or less complex tests**.
- Delivery
    - As used in the continuous delivery (CD) part of CI/CD, the process of **building a fully packaged and validated version of the model** ready to be deployed to production.
- Deployment
    - The process of **running a new model version on a target infrastructure**. Fully automated deployment is not always practical or desirable and is a business decision as much as a technical decision, whereas continuous delivery is a tool for the development team to improve productivity and quality as well as measure progress more reliably. Continuous delivery is required for continuous deployment, but it also provides enormous value without.
- Release
    - In principle, release is yet another step, as deploying a model version (even to the production infrastructure) does not necessarily mean that the production **workload is directed to the new version**. As we will see, multiple versions of a model can run at the same time on the production infrastructure.

#### Categories of Model Deployment
 
In addition to different deployment strategies, there are two ways to approach model deployment:
- **Batch scoring**, where whole datasets are processed using a model, such as in daily scheduled jobs.
- **Real-time scoring**, where one or a small number of records are scored, such as when an ad is displayed on a website and a user session is scored by models to decide what to display.

Deploying many real-time scoring systems is conceptually simpler since the records to be scored can be dispatched between several machines (e.g., using a load balancer).

Batch scoring can also be parallelized, for example by using a parallel processing runtime like Apache Spark, but also by splitting datasets (which is usually called partitioning
or sharding) and scoring the partitions independently. 

Note that these two concepts of splitting the data and computation can be combined, as they can address different problems.

#### Considerations When Sending Models to Production

When sending a new model version to production, the first consideration is often to avoid downtime, in particular for real-time scoring. The basic idea is that rather than shutting down the system, upgrading it, and then putting it back online, a new system can be set up next to the stable one, and when it’s functional, the workload can be directed to the newly deployed version (and if it remains healthy, the old one is shut down). This deployment strategy is called **blue-green**—or sometimes red-black— deployment. There are many variations and frameworks (like Kubernetes) to handle this natively.

Another more advanced solution to mitigate the risk is to have **canary releases** (also called canary deployments). The idea is that the stable version of the model is kept in production, but a certain percentage of the workload is redirected to the new model, and results are monitored. This strategy is usually implemented for real-time scoring, but a version of it could also be considered for batch.

#### Maintenance in Production

Once a model is released, it must be maintained. At a high level, there are three maintenance measures:

- Resource monitoring
    - Just as for any application running on a server, collecting IT metrics such as CPU, memory, disk, or network usage can be useful to detect and troubleshoot issues.
- Health check
    - To check if the model is indeed online and to analyze its latency, it is common to implement a health check mechanism that simply queries the model at a fixed interval (on the order of one minute) and logs the results.
- ML metrics monitoring
    - This is about analyzing the accuracy of the model and comparing it to another version or detecting when it is going stale. Since it may require heavy computation, this is typically lower frequency, but as always, will depend on the application; it is typically done once a week. Chapter 7 details how to implement this feedback loop.

Finally, when a malfunction is detected, a **rollback** to a previous version may be necessary. It is critical to have the rollback procedure ready and as automated as possible; **testing it regularly** can make sure it is indeed functional.

### Containerization

As described earlier, managing the versions of a model is much more than just saving its code into a version control system. In particular, it is necessary to provide an exact description of the **environment** (including, for example, all the Python libraries used as well as their versions, the system dependencies that need to be installed, etc.).

But storing this metadata is not enough. Deploying to production should automatically and reliably rebuild this environment on the target machine. In addition, the target machine will typically run multiple models simultaneously, and two models may have **incompatible dependency versions**. 

Finally, several models running on the same machine could compete for resources, and one misbehaving model could hurt the **performance** of multiple cohosted models.

Containerization technology is increasingly used to tackle these challenges.

Unlike virtual machines (VMs), containers do not duplicate the complete operating system; multiple containers share a common operating system and are therefore far more resource efficient.

The most well-known containerization technology is the open source platform **Docker**. Released in 2014, it has become the de facto standard. It allows an application to be packaged, sent to a server (the Docker host), and run with all its dependencies in isolation from other applications.

### Scaling Deployments

As ML adoption grows, organizations face two types of growth challenges:
- The ability to use a model in production with high-scale data
- The ability to train larger and larger numbers of models

Handling more data for **real-time scoring** is made much easier by frameworks such as **Kubernetes**. 
Since most of the time trained models are essentially formulas, they can be replicated in the cluster in as many copies as necessary. With the **auto-scaling** features in Kubernetes, both provisioning new machines and **load balancing** are **fully handled by the framework**, and setting up a system with huge scaling capabilities is now relatively simple.

For **batch scoring**, the situation can be more complex. When the volume of data becomes too large. Use a framework that handles distributed computation natively, in particular
**Spark**.


## Chapter 7 - Monitoring and Feedback Loop <a name="chapter_7"></a>

When a machine learning model is deployed in production, it can start degrading in quality fast—and without warning—until it’s too late (i.e., it’s had a potentially negative impact on the business). That’s why model monitoring is a crucial step in the ML model life cycle and a critical piece of MLOps.

<img src="img/monitoring_and_feeback_loop.png" alt="monitoring and feedback loop" width="550"/>

Machine learning models need to be **monitored** at two levels:

- At the **resource level**, including ensuring **the model is running correctly in the production environment**. Key questions include: Is the system alive? Are the CPU, RAM, network usage, and disk space as expected? Are requests being processed at the expected rate?
- At the **performance level**, meaning monitoring the **pertinence of the model over time**. Key questions include: Is the model still an accurate representation of the pattern of new incoming data? Is it performing as well as it did during the design phase?

### How Often Should Models Be Retrained?

Unfortunately, there is no easy answer, as this question depends on many factors, including:

- The domain
    - Models in areas like cybersecurity or real-time trading need to be updated regularly to keep up with the constant changes inherent in these fields. Physical models, like voice recognition, are generally more stable, because the patterns don’t often abruptly change. However, even more stable physical models need to adapt to change: what happens to a voice recognition model if the person has a cough and the tone of their voice changes?
- The cost
    - Organizations need to consider whether the cost of retraining is worth the improvement in performance. For example, if it takes one week to run the whole data pipeline and retrain the model, is it worth a 1% improvement?
- The model performance
    - In some situations, the model performance is restrained by the limited number of training examples, and thus the decision to retrain hinges on collecting enough new data.

### Understanding Model Degradation

Once a machine learning model is trained and deployed in production, there are two approaches to monitor its performance degradation: ground truth evaluation and
input drift detection. Understanding the theory behind and limitations of these approaches is critical to determining the best strategy.

#### Ground Truth Evaluation

Ground truth retraining requires waiting for the label event. 

For example, in a fraud detection model, the ground truth would be whether or not a specific transaction was actually fraudulent. For a recommendation engine, it would be whether or not the customer clicked on—or ultimately bought—one of the recommended products.

With the new ground truth collected, the next step is to compute the performance of the model based on ground truth and compare it with registered metrics in the training phase. When the difference surpasses a threshold, the model can be deemed as outdated, and it should be retrained.

The metrics to be monitored can be of two varieties:
- **Statistical metrics like accuracy**, ROC AUC, log loss, etc. As the model designer has probably already chosen one of these metrics to pick the best model, it is a first-choice candidate for monitoring. For more complex models, where the average performance is not enough, it may be necessary to look at metrics computed by subpopulations.
- **Business metrics, like cost-benefit assessment**. For example, the credit scoring business has developed its own specific metrics.

---
*A Stats Primer: From Null Hypothesis to p-Values*

The null hypothesis says that there is no relationship between the variables being compared; any results are due to sheer chance.

The alternative hypothesis says that the variables being compared are related, and the results are significant in supporting the theory being considered, and not due to chance.

The level of statistical significance is often expressed as a p-value between 0 and 1. The smaller the p-value, the stronger the evidence that one should reject the null hypothesis.

---

The drawback is that the drop may be statistically significant without having any noticeable impact. Or worse, the cost of retraining and the risk associated with a redeployment may be higher than the expected benefits. 

Business metrics are far more interesting because they ordinarily have a monetary value, enabling subject matter experts to better handle the cost-benefit trade-off of the retraining decision.

When available, ground truth monitoring is the best solution. However, it may be problematic. The main **challenge** is that the **ground truth is not always (immediately) available**.

### Input Drift Detection

Given the challenges and limitations of ground truth retraining presented in the previous section, a more practical approach might be input drift detection.

#### Example Causes of Data Drift

There are two frequent root causes of data drift:
- **Sample selection bias**, where the training sample is not representative of the population. 
- **Non-stationary environment**, where training data collected from the source population does not represent the target population. This often happens for timedependent tasks—such as forecasting use cases—with strong seasonality effects.

#### Input Drift Detection Techniques

##### Univariate statistical tests

This method requires applying a statistical test on data from the source distribution and the target distribution for each feature. A warning will be raised when the results of those tests are significant.

The choice of hypothesis tests have been extensively studied in the literature, but the basic approaches rely on these two tests:
- For **continuous features**, the **Kolmogorov-Smirnov test** is a nonparametric hypothesis test that is used to check whether two samples come from the same distribution. It measures a distance between the empirical distribution functions.
- For **categorical features**, the **Chi-squared test** is a practical choice that checks whether the observed frequencies for a categorical feature in the target data match the expected frequencies seen from the source data.

##### Domain classifier

In this approach, data scientists **train a model that tries to discriminate between** the original **dataset** (input features and, optionally, predicted target) and the development dataset. 

In other words, they stack the two datasets and train a classifier that aims at predicting the data’s origin. The performance of the model (its accuracy, for example) can then be considered as a metric for the drift level.

If this model is successful in its task, and thus has a high drift score, it implies that the data used at training time and the new data can be distinguished, so it’s fair to say that the new data has drifted.

### The Feedback Loop

All effective machine learning projects implement a form of data feedback loop; that is, information from the production environment flows back to the model prototyping environment for further improvement.

<img src="img/feedback_loop.png" alt="feedback loop" width="550"/>

This infrastructure is comprised of three
main components:
- A **logging system** that collects data from several production servers
- A **model evaluation store** that does versioning and evaluation between different model versions
- An **online system** that does **model comparison on production environments**, either with the shadow scoring (champion/challenger) setup or with A/B testing

#### Logging

// TODO

