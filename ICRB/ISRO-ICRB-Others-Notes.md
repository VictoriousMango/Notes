# ISRO ICRB CSE - "Others" Topics Comprehensive Notes
*Complete Theoretical & Numerical Cheat Sheet for Exam Preparation*

---

## **Table of Contents**
1. [Software Engineering](#software-engineering)
2. [Image Processing](#image-processing)
3. [Computer Graphics](#computer-graphics)
4. [Artificial Intelligence](#artificial-intelligence)
5. [Machine Learning](#machine-learning)
6. [Important Formulas & Quick Reference](#formulas-quick-reference)

---

## **1. Software Engineering**

### **1.1 Software Development Life Cycle (SDLC) Models**

#### **Waterfall Model**
- **Definition**: Linear and sequential approach where each phase must be completed before moving to the next
- **Phases**: Requirements → Design → Implementation → Testing → Deployment → Maintenance
- **Advantages**: Simple, well-documented, predictable
- **Disadvantages**: Inflexible, late testing, limited client involvement
- **Use Cases**: Well-defined requirements, small to medium projects

#### **V-Model (Verification & Validation Model)**
- **Structure**: V-shaped where left side = Verification (development), right side = Validation (testing)
- **Key Feature**: Each development phase has corresponding testing phase
- **Verification Phases**: Requirements Analysis → System Design → Architecture Design → Module Design → Coding
- **Validation Phases**: Unit Testing → Integration Testing → System Testing → Acceptance Testing
- **Advantages**: Early defect detection, clear traceability, thorough testing
- **Disadvantages**: Rigid, expensive, not suitable for changing requirements

#### **Spiral Model**
- **Definition**: Risk-driven iterative development process combining waterfall and iterative elements
- **Four Quadrants**:
  1. **Objectives Defined**: Requirements gathering and analysis
  2. **Risk Analysis**: Identify and resolve risks, build prototypes
  3. **Development**: Code and test the next version
  4. **Planning**: Review and plan next phase
- **Advantages**: Risk management, iterative refinement, suitable for large projects
- **Disadvantages**: Complex, expensive, requires risk assessment expertise
- **Use Cases**: Large, complex, high-risk projects

#### **RAD Model (Rapid Application Development)**
- **Definition**: Minimal planning with rapid prototyping approach
- **Phases**: Requirements Planning → User Design → Construction → Cutover
- **Key Features**: Reusable components, time-boxed development (60-90 days), parallel development
- **Advantages**: Fast delivery, user involvement, flexible to changes
- **Disadvantages**: Requires skilled developers, not suitable for large teams
- **Use Cases**: Time-critical projects, well-understood domains

#### **Agile Model**
- **Principles**: Individuals over processes, working software over documentation, customer collaboration, responding to change
- **Characteristics**: Iterative development, continuous feedback, adaptive planning
- **Difference from Waterfall**: Overlapping phases, change-friendly, continuous testing

### **1.2 Software Testing**

#### **Testing Levels**
1. **Unit Testing**: Test individual modules/components
2. **Integration Testing**: Test interaction between modules
   - **Big Bang**: Integrate all at once
   - **Top-Down**: Start from top-level modules
   - **Bottom-Up**: Start from bottom-level modules
3. **System Testing**: Test complete integrated system
4. **Acceptance Testing**: Final testing by end users

#### **Testing Types**
- **Functional Testing**: Unit, Integration, System, Acceptance
- **Non-Functional Testing**: Performance, Security, Usability
- **Black Box Testing**: Input-output based without internal knowledge
- **White Box Testing**: Internal structure and logic based

### **1.3 Software Cost Estimation - COCOMO Model**

#### **Basic COCOMO Formula**
```
Effort (E) = a × (KLOC)^b
Time (T) = c × (E)^d
People (P) = E/T
```

#### **Project Types & Constants**
| Project Type | a | b | c | d |
|-------------|---|---|---|---|
| Organic | 2.4 | 1.05 | 2.5 | 0.38 |
| Semi-detached | 3.0 | 1.12 | 2.5 | 0.35 |
| Embedded | 3.6 | 1.20 | 2.5 | 0.32 |

- **Organic**: Small teams, well-understood problems, experienced developers
- **Semi-detached**: Medium complexity, mixed team experience
- **Embedded**: Complex, large teams, tight constraints

#### **Intermediate COCOMO**
- Uses 15 cost drivers (multipliers)
- **Categories**: Product attributes, Hardware attributes, Personnel attributes, Project attributes
- **Formula**: Effort = Basic_Effort × ∏(Cost_Drivers)

### **1.4 UML Diagrams**

#### **Structural Diagrams**
- **Class Diagram**: Shows classes, attributes, methods, relationships
- **Object Diagram**: Shows instances of classes at specific time
- **Component Diagram**: Shows components and dependencies

#### **Behavioral Diagrams**
- **Use Case Diagram**: Shows system functionality from user perspective
  - **Components**: Actors, Use Cases, Relationships (Include, Extend, Generalization)
- **Sequence Diagram**: Shows object interactions over time
- **Activity Diagram**: Shows workflow/process flow
- **State Diagram**: Shows state transitions of objects

---

## **2. Image Processing**

### **2.1 Image Enhancement**

#### **Spatial Domain Techniques**

##### **Point Processing**
- **Contrast Stretching (Normalization)**:
  ```
  g(x,y) = (f(x,y) - c) × (b-a)/(d-c) + a
  ```
  Where: f(x,y) = input pixel, g(x,y) = output pixel
  c,d = min,max of input range, a,b = desired output range

- **Histogram Equalization**:
  ```
  s = T(r) = (L-1) × Σ(i=0 to k) p_r(r_i)
  ```
  Where: L = gray levels, p_r = probability density function

##### **Neighborhood Processing**
- **Spatial Filtering**: Uses convolution with masks/kernels
- **Common Filters**:
  - **Averaging Filter**: Noise reduction, blurring
  - **Gaussian Filter**: Smoothing with preserved edges
  - **Median Filter**: Salt-and-pepper noise removal

#### **Frequency Domain Techniques**
- **Fourier Transform**: Converts spatial domain to frequency domain
- **Low-pass Filters**: Remove high frequencies (smoothing)
- **High-pass Filters**: Remove low frequencies (sharpening)
- **Band-pass/Band-reject Filters**: Allow/reject specific frequency ranges

### **2.2 Edge Detection**

#### **Gradient-Based Methods**
- **Sobel Operator**:
  ```
  Gx = [-1 0 1; -2 0 2; -1 0 1]
  Gy = [-1 -2 -1; 0 0 0; 1 2 1]
  Magnitude = √(Gx² + Gy²)
  ```

- **Prewitt Operator**:
  ```
  Gx = [-1 0 1; -1 0 1; -1 0 1]
  Gy = [-1 -1 -1; 0 0 0; 1 1 1]
  ```

- **Roberts Cross**:
  ```
  Gx = [1 0; 0 -1]
  Gy = [0 1; -1 0]
  ```

#### **Advanced Edge Detection**
- **Canny Edge Detection**:
  1. Gaussian smoothing
  2. Gradient computation
  3. Non-maximum suppression
  4. Hysteresis thresholding

- **Laplacian**:
  ```
  ∇²f = ∂²f/∂x² + ∂²f/∂y²
  Kernel = [0 1 0; 1 -4 1; 0 1 0]
  ```

### **2.3 Morphological Operations**

#### **Basic Operations**
- **Erosion**: A ⊖ B = {z | (B)_z ⊆ A}
  - Shrinks objects, removes noise
- **Dilation**: A ⊕ B = {z | (B̂)_z ∩ A ≠ ∅}
  - Expands objects, fills gaps

#### **Compound Operations**
- **Opening**: A ○ B = (A ⊖ B) ⊕ B
  - Removes small objects, smooths contours
- **Closing**: A • B = (A ⊕ B) ⊖ B
  - Fills small holes, connects nearby objects

#### **Applications**
- Noise removal
- Object separation/connection
- Skeleton extraction
- Boundary cleaning

---

## **3. Computer Graphics**

### **3.1 Line Drawing Algorithms**

#### **Bresenham's Line Algorithm**
- **Purpose**: Draw lines using integer arithmetic only
- **Key Steps**:
  1. Calculate Δx = x₂ - x₁, Δy = y₂ - y₁
  2. Initial decision parameter: P₀ = 2Δy - Δx
  3. For each x coordinate:
     - If P < 0: next point (x+1, y), P = P + 2Δy
     - If P ≥ 0: next point (x+1, y+1), P = P + 2Δy - 2Δx

#### **DDA Algorithm**
- **Formula**:
  ```
  If |Δx| > |Δy|: steps = |Δx|
  Else: steps = |Δy|
  x_increment = Δx/steps
  y_increment = Δy/steps
  ```

### **3.2 Circle Drawing Algorithms**

#### **Bresenham's Circle Algorithm**
- **Initial values**: x = 0, y = r, P₀ = 3 - 2r
- **Decision parameter**:
  - If P < 0: next point (x+1, y), P = P + 4x + 6
  - If P ≥ 0: next point (x+1, y-1), P = P + 4(x-y) + 10
- **Symmetry**: Plot 8 symmetric points for each calculated point

#### **Midpoint Circle Algorithm**
- **Decision parameter**: P₀ = 1 - r
- **Uses circle equation**: x² + y² = r²

### **3.3 2D Transformations**

#### **Basic Transformations**
- **Translation**: T(tx, ty) = [1 0 tx; 0 1 ty; 0 0 1]
- **Scaling**: S(sx, sy) = [sx 0 0; 0 sy 0; 0 0 1]
- **Rotation**: R(θ) = [cosθ -sinθ 0; sinθ cosθ 0; 0 0 1]

#### **Composite Transformations**
- **Matrix Multiplication**: T₃ = T₁ × T₂
- **Order Matters**: Generally not commutative

### **3.4 3D Transformations**
- **Translation**: Add translation vector
- **Scaling**: Multiply by scaling factors
- **Rotation**: Around x, y, z axes using rotation matrices

---

## **4. Artificial Intelligence**

### **4.1 Search Algorithms**

#### **Uninformed Search (Blind Search)**
- **Characteristics**: No domain knowledge, explores systematically
- **Types**:
  - **Breadth-First Search (BFS)**: Level by level, optimal for unit costs
  - **Depth-First Search (DFS)**: Goes deep first, uses less memory
  - **Uniform Cost Search**: Expands lowest cost node first

#### **Informed Search (Heuristic Search)**
- **Characteristics**: Uses heuristic function h(n) to guide search
- **Types**:
  - **Greedy Best-First**: Selects node closest to goal
  - **A* Search**: f(n) = g(n) + h(n)
    - g(n) = cost from start to n
    - h(n) = heuristic cost from n to goal
  - **Hill Climbing**: Local search, can get stuck in local maxima

#### **Comparison Criteria**
- **Completeness**: Guarantees finding solution if exists
- **Optimality**: Finds best solution
- **Time Complexity**: Number of nodes expanded
- **Space Complexity**: Memory requirement

### **4.2 Heuristic Functions**
- **Admissible**: Never overestimates actual cost
- **Consistent**: h(n) ≤ c(n,n') + h(n')
- **Examples**: Manhattan distance, Euclidean distance

### **4.3 Knowledge Representation**
- **Propositional Logic**: True/False statements
- **Predicate Logic**: Variables, quantifiers, predicates
- **Semantic Networks**: Nodes and labeled arcs
- **Frames**: Data structures with slots and values

---

## **5. Machine Learning**

### **5.1 Types of Learning**

#### **Supervised Learning**
- **Definition**: Learning with labeled training data
- **Types**:
  - **Classification**: Predict discrete categories
    - Examples: Decision Trees, SVM, Neural Networks
  - **Regression**: Predict continuous values
    - Examples: Linear Regression, Polynomial Regression
- **Evaluation**: Train-test split, cross-validation

#### **Unsupervised Learning**
- **Definition**: Learning from unlabeled data
- **Types**:
  - **Clustering**: Group similar data points
    - Examples: K-means, Hierarchical clustering
  - **Association**: Find relationships between variables
    - Examples: Market basket analysis
  - **Dimensionality Reduction**: Reduce feature space
    - Examples: PCA, ICA

#### **Semi-supervised Learning**
- **Definition**: Combines labeled and unlabeled data
- **Applications**: When labeling is expensive
- **Examples**: Fraud detection, sentiment analysis

### **5.2 Performance Metrics**

#### **Classification Metrics**
- **Accuracy**: (TP + TN) / (TP + TN + FP + FN)
- **Precision**: TP / (TP + FP)
- **Recall**: TP / (TP + FN)
- **F1-Score**: 2 × (Precision × Recall) / (Precision + Recall)

#### **Regression Metrics**
- **Mean Squared Error**: MSE = Σ(y - ŷ)² / n
- **Root Mean Squared Error**: RMSE = √MSE
- **Mean Absolute Error**: MAE = Σ|y - ŷ| / n

### **5.3 Overfitting and Underfitting**
- **Overfitting**: Model memorizes training data, poor generalization
- **Underfitting**: Model too simple, poor performance on both train and test
- **Solutions**: Regularization, cross-validation, feature selection

---

## **6. Formulas & Quick Reference**

### **6.1 COCOMO Calculations**
```
Basic COCOMO:
- Effort (Person-months) = a × (KLOC)^b
- Time (months) = c × (Effort)^d
- People = Effort / Time

Cost Estimation:
- Cost = Effort × Cost_per_person_month
```

### **6.2 Image Processing Formulas**
```
Contrast Stretching:
- g(x,y) = (f(x,y) - fmin) × (gmax - gmin)/(fmax - fmin) + gmin

Histogram Equalization:
- s = T(r) = (L-1) × Σ P_r(r_i)

Edge Detection (Gradient Magnitude):
- |∇f| = √(Gx² + Gy²)
- θ = arctan(Gy/Gx)
```

### **6.3 Computer Graphics Formulas**
```
2D Rotation:
- x' = x×cosθ - y×sinθ
- y' = x×sinθ + y×cosθ

Circle Equation:
- x² + y² = r²

Line Equation:
- y = mx + c (slope-intercept form)
- Δy/Δx = slope
```

### **6.4 AI Search Complexity**
```
BFS: Time O(b^d), Space O(b^d)
DFS: Time O(b^m), Space O(bm)
A*: Time O(b^d), Space O(b^d)

Where:
- b = branching factor
- d = depth of solution
- m = maximum depth
```

### **6.5 Machine Learning Evaluation**
```
Classification:
- Precision = TP/(TP+FP)
- Recall = TP/(TP+FN)
- F1 = 2×(Precision×Recall)/(Precision+Recall)

Regression:
- MSE = Σ(y-ŷ)²/n
- MAE = Σ|y-ŷ|/n
- R² = 1 - (SSres/SStot)
```

---

## **7. Exam Strategy & Tips**

### **7.1 High-Priority Topics**
1. **Software Engineering**: SDLC models, Testing levels, COCOMO
2. **Image Processing**: Enhancement techniques, Edge detection, Morphological operations
3. **Computer Graphics**: Line/Circle algorithms, 2D transformations
4. **AI**: Search algorithms comparison, Heuristic functions
5. **Machine Learning**: Supervised vs Unsupervised, Performance metrics

### **7.2 Quick Revision Checklist**
- [ ] Waterfall vs Agile vs Spiral models
- [ ] V-Model phases and testing levels
- [ ] COCOMO formulas and project types
- [ ] UML diagram types and purposes
- [ ] Histogram equalization vs contrast stretching
- [ ] Morphological operations (erosion, dilation, opening, closing)
- [ ] Bresenham's line and circle algorithms
- [ ] BFS vs DFS characteristics
- [ ] A* search algorithm components
- [ ] Supervised vs Unsupervised learning differences

### **7.3 Numerical Problem Practice**
- COCOMO effort and time calculations
- Image enhancement transformations
- Bresenham's algorithm step-by-step
- A* search with heuristic functions
- Classification performance metrics

---

**Remember**: Focus on understanding concepts rather than memorizing. Practice numerical problems and be able to explain the "why" behind each method. Good luck with your ISRO ICRB CSE preparation!