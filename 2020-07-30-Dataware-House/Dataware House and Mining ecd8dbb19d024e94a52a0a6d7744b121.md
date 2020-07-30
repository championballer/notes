# Dataware House and Mining

- Define Dataware house, its need and its architecture
    - Datawarehouse → easy and consistent store to store data from various heterogenous and homogenous data bases such that it can be used easily in business context.
    - Need
        - Dealing with heterogeneity of data
        - Fragmentation
            - Horizontal → Breaking the table across tuples
            - Vertical → Breaking the table across attributes
    - Architecture

        ![Dataware%20House%20and%20Mining%20ecd8dbb19d024e94a52a0a6d7744b121/Screenshot_2020-07-29_at_7.58.31_PM.png](Dataware%20House%20and%20Mining%20ecd8dbb19d024e94a52a0a6d7744b121/Screenshot_2020-07-29_at_7.58.31_PM.png)

- ETL process
    - Extraction - Transfer - Load is defined as the process of copying data from various sources to a system. Its three steps are :
        - Extraction → Extraction of data from various sources
        - Transformation → Applying data cleaning and various transformations to ensure easy and fast query processing
        - Load → Loading the transformed data into the destination system
- Compare OLAP and OLTP
    - 
- Types of OLAP
    - Relational OLAP
        - Extended RDBMS along with multi dimensional data mapping to perform standard procedure
    - Multi dimensional OLAP
    - Hybrid OLAP
    - Others → Application / Domain specific
        - WOLAP → Web specific
        - DOLAP → Desktop ori
- Compare top down and bottom up approaches of designing dataware houses.
- Different schemas
    - Star schema
    - Snowflakes schema
    - Galaxy schema
- What is meta data?
    - Types of meta data
        - Operational Meta data
        - Extraction and transformation meta data
        - End user meta data
- Dimensional modeling, and how it is different from ER modeling?
- MDX → Multi dimensional Expression Query → applicable on OLAP system → SELECT * FROM Datacube, dimension WHERE, WITH clause
- EIMS → Executive Information Mgmt. System
- KDD Process → Knowledge discovery of database

    Databases → Dataware house → Target data (Data mining→) Pattern (Pattern eval→) Knowledge

    - Preprocessing
    - Datamining
    - Post processing
- Association Rules
    - Support
    - Confidence → To check validity of derived association rule from frequent itemset
    - Apriori algorithm
- Naive Bayes Algorithm
- Decision Tree Algorithm
    - Accuracy
    - Information Gain
        - For every node we define the entropy term = $- \sum_{class} P_i \log P_i$
        - Choose split with maximum decrease in entropy. Pure nodes have 0 entropy.
        - Decrease in entropy → Information Gain
        - For the entropy computation post split, we can take weighted average. Weights can be assigned on the basis no. of samples in a node.
        - Disadvantage → Might lead to many nodes, for example for unique id feature.
    - Gain Ratio
        - Information Gain / Split info
        - Split info = $-\sum_{splits}\frac{D_i}{D} \log{\frac{Di}{D}}$ where $D_i$ refers to no. of samples in node.
        - May lead to unbalanced nodes
    - Gini Index
        - $1 - \sum_{class} P_i^2$
        - Splits on feature with maximum gini index gain
- Classification and Prediction
- KNN Classifier
- Clustering & Outlier Analysis
    - Clustering Method
        - Partitioning method
        - Hierarichal method
            - Agglomerative method
            - Divisive method
        - Density method
        - Grid - based method
        - Model based method
        - Constraint based method
    - Requirements of Clustering : The following points throw light on why clustering is required in data mining −
        - Scalability − We need highly scalable clustering algorithms to deal with large databases.
        - Ability to deal with different kinds of attributes − Algorithms should be capable to be
        applied on any kind of data such as interval-based (numerical) data, categorical, and
        binary data.
        - Discovery of clusters with attribute shape − The clustering algorithm should be
        capable of detecting clusters of arbitrary shape. They should not be bounded to only
        distance measures that tend to find spherical cluster of small sizes.
        - High dimensionality − The clustering algorithm should not only be able to handle low-
        dimensional data but also the high dimensional space.
        - Ability to deal with noisy data − Databases contain noisy, missing or erroneous data.
        Some algorithms are sensitive to such data and may lead to poor quality clusters.
        - Interpretability − The clustering results should be interpretable, comprehensible, and
        usable.
    - Outlier analysis
        - Discard entry
        - Dropping entry but keeping record
            - Coach example
        - Clipped values
        - Variable transformation : x → log(x)
- Genetic Algorithm
    - Selection, Cross-over and Mutation
    - Ticket mailing example
- FP Growth Algorithm
    - FP Tree Construction
        - 1 frequent item set priority
        - Reordering of items in transactions
        - Constructing tree
    - Conditional Pattern Base
    - Conditional FP Tree
    - Frequent Item set
- Neural Networks
- Data Mining Tools

    ![Dataware%20House%20and%20Mining%20ecd8dbb19d024e94a52a0a6d7744b121/Screenshot_2020-07-30_at_6.56.38_AM.png](Dataware%20House%20and%20Mining%20ecd8dbb19d024e94a52a0a6d7744b121/Screenshot_2020-07-30_at_6.56.38_AM.png)

    - Orange
    - R
    - Weka
    - Rapidminer
- K Mean Clustering
    - Take initial points as the centroid of k different clusters.
    - Then for each data point find distance from each cluster's centroid, and on the basis of this distance, assign the data point a cluster. Then recalculate the cluster's centroid. Continue this process for all datapoints.
    - Once done, restart the process. And find the distance between all datapoints and centroid, and find new clusters. If the cluster set remains the same, then we stop and we get the final clusters.
    - Distance can be found using Euclidean (L2) and Manhattan (L1).
- MBR and Link Analysis
    - Nearest neighbour approaches → Memory based reasoning (analogous situations in the past) and collaborative filtering (analogous situations in the past + preferences).
    - MBR → Distance function + Combination function to compute neighbourly
    - MBR Challenges
        - Choosing appropriate historical data for use in training.
        - Choosing the most efficient way to represent the training data
        - Choosing the distance function, combination function, and the number of
        neighbors
    - MBR → Distance between new record and records in dataset is calculated (euclidean, manhattan, etc.)
    - Collaborative filtering → Using similar rated item sets to recommend to other users. If we have the same behaviour feature set, so if one likes some movie, then there is high probability that the other person will like it too.
    - Link Analysis → Patterns from Relationships → Mines relationships and discovers knowledge
        - Association Discovery : Bread → Butter
        - Sequential Pattern Discovery : Language Modelling
        - Similar Time Sequence Discovery : Applying pattern discovered in one area to another area.
- ARFF → Attribute Relation File Format → Set of instances sharing a set of attributes → ASCII file