# Facebook Friend Recommendation
### Problem Definition
Given a directed social graph, the task is to predict missing links to recommend friends/connections/followers.

Let's say for a given graph:
* Nodes / Vertices denotes the Number of Users.
* Edges denotes the connection (friends/followers) between them.
### About Dataset
- The dataset is directed graph data.
- The Data has approximately 1.86M nodes and 9.43M edges.
- Data is obtained from Kaggle. The data is available here [Facebook Friend Recommendation](https://www.kaggle.com/c/FacebookRecruiting) 
- We have provided only connected nodes. i.e. 9.43M edges. But for each user among n users, there are n-1 edges. So, for n nodes total possible edges are of 10^12 order.

### Business Objectives and constraints:
a) Objectives
- The main objective is to identify the possible missing link by using the given data.
- The probability of classification is important because by using this a specific number of recommendation options w.r.t the probability can be selected.

b) Constraints
- Probability of prediction is useful to recommend the highest probability links.
- No strict latency constraint, as the objective is more about making the right decision rather than a quick decision. It would be fine and acceptable if the model takes a few seconds to make a prediction.

### Performance Metrics
1) For the predicted missing link to be correct the Recall value should be high.
2) To cover the maximum number of people, the precision value should be high.
3) Therefore, the performance matrix F-1 score is very useful.
4) Confusion matrix

### Training Dataset Preparation
- If an edge is present in between two nodes, Class label y is considered as 1.
- For no Edge present between two nodes, class label y is considered as 0.

### Feature Engineering
Featurization is the most important part of the case study. Below is the list of extracted features:

1) Similarity measures
   - Jaccard Distance
   - Cosine distance
2) Ranking Measure
   - Page Ranking (https://en.wikipedia.org/wiki/PageRank)
3) Graph Features
   - Shortest Path
   - Checking for the same community
   - Adamic/Adar Index
   - Is following back
   - Katz Centrality
   - Hits Score
   - num followers
   - num followees
4) Weight Features
   - the weight of incoming edges
   - the weight of outgoing edges
   - the weight of incoming edges + weight of outgoing edges
   - the weight of incoming edges * weight of outgoing edges
   - 2*weight of incoming edges + weight of outgoing edges
   - the weight of incoming edges + 2*weight of outgoing edges
5) SVD features using Adjacency matrix. (n_components = 6)

### Models
Two Ensemble Models namely RandomForest and XGBOOST are used. For both the models, Follows_back is the most important feature found. Here is the summary result,

| Models           | n_estimators           | max_depth  | Train f1-Score  | Test f1-Score  |
| ---------------- |:----------------------:| ----------:| ---------------:| --------------:|
| Random Forest    | 121                    | 14         |0.9632           |0.9303          |
| XgBoost          | 123                    | 14         |0.9998           |0.9331          |
