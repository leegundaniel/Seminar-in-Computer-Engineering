# Human-Data Interaction
Jaemin Jo (jmjo@skku.edu)
- Interactive Data Computing Laboratory
- College of Computing and Informatics
- SKKU

## Human-Computer Interaction (HCI)
- HCI studies the design and use of computer technology, focused on the interfaces between humans and computers

- Human <- Interaction -> User Interface -> Application, Databases, ML/AI/DL, Data mining / Compilers & Languages -> Operating System -> Architecture & Network -> SemiConductor Chips

## HCI is Interdisciplinary
- Computer science
- Engineering
- Ergonomics and human factors
- Cognitive/social psychology
- Design
- Art
- Anthropology/Sociology

## Topics in HCI
- User Experience and Usability, Learning, Education and Families,...
- Diverse
- Too broad

## Human-Data Interaction
- facilitate the interaction between humans and data
    - better understanding, insights and knowledge, decision making
    - Through interactive visual interfaces
- **Information visualization: the use of computer-supported interactive visual representations of abstract data to amplify cognition
    - Charts, graphs, figures, tables,...

## Why Visualization
-  Statistically may be the same or similar, but visually very different

## New Challenges in HDI
1. Scalability
2. Dimensionality

### Scalability Challenge
- Data are becoming larger and larger
    - Size > TBs
    - number of rows > a few billion
    - number of columns > a few hundred
- **Interactive systems are no more "interactive**

#### Progressive Visual Analytics (PVA)
- Dahstuhl seminar [Dags19], the most recent definition of "progressiveness" is given.

- [Dags19]: computation bounded on time and data
    - which reports intermediate outputs, namely
        - a result
        - a measure of quality
        - a measure of progress
    - **within bounded latency**
    - converging towards the true result
    - and **controllable** by a user during execution either by
        - aborting, pausing, etc.
        - or by tuning parameters (steering)

##### Time Limits in PVA
- Three time limits [Niel94]
    - 0.1s for continuous feedback (animation)
    - 1s for maintaing the user's flow of thought
    - 10s for keeping the user's attention
- Target latency: **a few seconds**(up to 10 secs)
    - Reasonable and feasible delays
    - Supported by user study results [Bada17, Zgra17]

### Dimensionality Challenge
- Data is becoming high dimensional
- AI models
    - Google search engines
    - YouTube recommendation
    - Smart speakers, chatbots, ads,...

#### What is the Dimensionality of Data
- **Univariate** dataset dimensionality = 1
    - barcode plot
- **bivariate** dataset dimensionality = 2
    - scatterplot
- **trivariate** dataset dimensionality = 3
    - 3D scatterplot
- **multivariate** dataset dimensionality = ?

#### Dimensionality Reduction
- Find a lower-dimensional representation of the original dataset that maintains the distances between points in the original space

- Distance between points
    - Euclidean distance ($L^2$ norm)

$$ d(x,y) = \sqrt{\sum_{i=1}^n{(x_i - y_i)^2}}$$

##### Example: Dimensionality Reduction
- The Swiss Role dataset
- 3D
- $(x,y) -> (x cosx, y, x sinx)$
- can we visualize the dataset on a 2D plane

- Result1: PCA (linear DR)
- Good: 2D
- Bad
    - Distant points in 3D are placed nearby in 2D
    - Loss of the "spiral" structure

- Result2: Isomap (non-linear DR)
- Good:
    - 2D
    - Close points in 2D are actually close in 3D
- Bad:
    - Loss of the "spiral" structure

## AI as "Blackboxes"
- Cat Image -> Black Box -> Class: CAT

### Visualizing Inner-workings
- Several layers interpret the images to classify it

- While going through the layers, the different information slowly group together with similar colors/categories

### Joint t-SNE (Wang et al., 2021)
- A visualization technique for generting **comparable** projections between layers in a neural architecture

## Limitation of Nonlinear Dimensionality Reduction (NLDR)
- NLDR techniques are used to capture nonlinear structures in a high-dimensional space
    - t-SNE[Maat08], UMAP [Mcln18]
- Limitation: computation takes too long!
    - ~a few hours

### Computing t-SNE Progressively

- t-SNE[Maat08]
1. Data read
2. Neighbor computation
3. Loss optimization

- Initial Delay until loss optimization
- long time

- Approximate t-SNE [Pezz15]
1. Data read
2. Approximate Neighbor computation
3. Loss optimization

- Initial delay reduced
- shorter time for computation

- Responsive t-SNE (ours)
1. Data read
2. Neighbor computation
3. Loss optimization
- but shorter terms and more continuous results

## Conclusion
- Two important challenges in Human-Data Interaction
    - Challenge 1: Scalability
    - Challenge 2: Dimensionality
- Designing interactive visual interfaces to bridge the gap
    - Scalability, latency, transparency, and explainability