# Computer Science & ML Cheat-sheet

---

## 1. Sets & Elements
- **Set**: `{a, b, c}` → a collection of elements  
- **Membership**: `x ∈ S` → x is in set S  
- **Not in**: `x ∉ S`  
- **Subset**: `A ⊆ B` → A is contained in B  
- **Empty set**: `∅` or `Φ`  
- **Set difference**: `S - {x}` → remove x from S  

---

## 2. Brackets & Parentheses
- **( )** → grouping, function call, e.g. `f(x) = x²`  
- **[ ]** → indexing, e.g. `A[i,j]`  
- **{ }** → sets, e.g. `{1,2,3}`  
- **⟨ ⟩** → inner product or tuple, e.g. `⟨x,y⟩`  

---

## 3. Logic & Conditions
- `∀ x ∈ S` → for all x in S  
- `∃ x ∈ S` → there exists x in S  
- Logical AND: `∧`  
- Logical OR: `∨`  
- NOT: `¬`  
- Implication: `A ⇒ B`  
- Equivalence: `A ⇔ B`  

---

## 4. Common Greek Letters in CS/ML
- `α (alpha)` → learning rate  
- `β (beta)` → regression coefficients, momentum  
- `γ (gamma)` → discount factor (RL)  
- `δ (delta)` → small change, error term  
- `ε (epsilon)` → small tolerance, error bound  
- `θ (theta)` → model parameters  
- `λ (lambda)` → regularization strength  
- `μ (mu)` → mean  
- `σ (sigma)` → standard deviation, also sigmoid  
- `π (pi)` → policy (RL)  
- `φ, ψ` → feature maps, transforms  
- `ω (omega)` → weight vector or frequency  

---

## 5. Functions & Operators
- Function mapping: `f: X → Y`  
- Minimum: `min f(x)`  
- Maximum: `max f(x)`  
- Argmin/Argmax: `argmin f(x)`, `argmax f(x)`  
- Summation: `∑_{i=1}^n x_i`  
- Product: `∏_{i=1}^n x_i`  
- Union: `A ∪ B`  
- Intersection: `A ∩ B`  
- Expectation: `E[X]`  
- Probability: `P(X)`  
- Gradient: `∇f(x)`  
- Partial derivative: `∂f/∂x`  

---

## 6. Vectors & Matrices
- Vector: **x** = `[x₁, x₂, ..., xₙ]ᵀ`  
- Matrix: `A ∈ ℝ^{m×n}`  
- Transpose: `Aᵀ`  
- Dot product: `x · y = ∑ xᵢ yᵢ`  
- Norms:  
  - `‖x‖₂` → Euclidean distance  
  - `‖x‖₁` → Manhattan distance  

---

## 7. Probability & ML Specific
- Random variable: `X ~ N(μ, σ²)` → Normal distribution  
- Loss function: `L(θ)`  
- Hypothesis/model: `h_θ(x)`  
- Training set: `{(x^(i), y^(i))} for i=1..m`  
- Gradient descent:  
  `θ ← θ - α ∇_θ L(θ)`  

---

## 8. Misc
- Infinity: `∞`  
- Approximately equal: `≈`  
- Proportional to: `∝`  
- Big-O notation: `O(n²)`  
- Floor: `⌊x⌋`, Ceil: `⌈x⌉`  
