# Decision Tree Convexity Visualization 🌳📊

An interactive web-based visualization tool that demonstrates why **Gini Index** and **Entropy** work as impurity measures in decision trees, while **Min** (misclassification error) doesn't.

[![Live Demo](https://img.shields.io/badge/demo-live-success)](https://behradsadeghi.github.io/decision-tree-convexity/)
[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![GitHub Pages](https://img.shields.io/badge/hosted-GitHub%20Pages-blue)](https://pages.github.com/)

## 🚀 Live Demo

### **[👉 Try it now! 👈](https://behradsadeghi.github.io/decision-tree-convexity/)**

Experience the interactive visualization at: `https://behradsadeghi.github.io/decision-tree-convexity/`

## 🎯 What Does This Visualize?

This tool provides an intuitive understanding of a fundamental concept in machine learning: **why concave impurity functions generate positive information gain in decision trees**.

### The Core Problem

When a decision tree splits a node into two children, we want to measure if this split improves purity. The **Information Gain** tells us how much better the split is:

```
Information Gain = Impurity(parent) - Weighted_Average_Impurity(children)
```

But here's the catch: **not all impurity functions work!**

### Why Convexity Matters

- **Gini Index** ✅ - Concave function → Positive information gain
- **Entropy** ✅ - Concave function → Positive information gain  
- **Min (Misclassification)** ❌ - Piecewise linear → Zero information gain

This visualization shows **geometrically** why concave functions create the "gap" needed for information gain.

## ✨ Features

### 🎓 Two Interactive Modes

#### Educational Mode (Recommended for Learning)
- **Realistic Decision Tree Simulation**: Enforces the constraint `p = α × q + (1-α) × r`
- The parent point is automatically calculated based on children and split ratio
- Shows how real decision tree splits work
- Perfect for understanding the mathematics behind CART algorithms

#### Free Mode (Exploratory)
- All parameters are independent
- Experiment with any combination of values
- See what happens when the constraint is violated
- Great for building geometric intuition

### 🎨 Visual Elements

- 🎚️ **Interactive Controls**: Real-time sliders for all parameters
- 📊 **Three Impurity Functions**: Switch between Gini, Entropy, and Min
- 📐 **Geometric Visualization**: Clear display of curves, chords, and gaps
- 🔢 **Precise Calculations**: All coordinates shown to 4 decimal places
- 📱 **Responsive Design**: Works on desktop, tablet, and mobile
- 🧮 **Mathematical Accuracy**: Exact formulas for all impurity functions

## 🎓 Educational Value

Perfect for:
- **Students** learning decision trees and information theory
- **Teachers** explaining why certain impurity measures work better
- **Data Scientists** gaining geometric intuition about splitting criteria
- **ML Engineers** understanding the mathematics behind CART algorithms

## 🛠️ Technical Details

### Built With

- **Pure HTML/CSS/JavaScript** - No build process required
- **Chart.js** - For beautiful, interactive visualizations
- **Zero Dependencies** - Works completely offline after first load

### Impurity Functions Implemented

1. **Gini Index**
   ```javascript
   Gini(p) = 2 * p * (1 - p)
   ```

2. **Entropy**
   ```javascript
   Entropy(p) = -p * log₂(p) - (1-p) * log₂(1-p)
   ```

3. **Min (Misclassification Error)**
   ```javascript
   Min(p) = min(p, 1-p)
   ```

### Information Gain Calculation

#### Educational Mode
```javascript
// Given: q, r, α (user inputs)
// Calculate: p = α × q + (1-α) × r (automatic)

x_avg = α × q + (1-α) × r  // This equals p!
y_avg = α × impurity(q) + (1-α) × impurity(r)

// Information gain (vertical distance)
Gain = impurity(p) - y_avg
```

#### Free Mode
```javascript
// All independent: p, q, r, α (user inputs)

x_avg = α × q + (1-α) × r  // May not equal p
y_avg = α × impurity(q) + (1-α) × impurity(r)

// Information gain (vertical distance at x_avg)
Gain = f(x_avg) - y_avg
```

## 📚 Understanding the Visualization

### Visual Elements

| Element | Color | Meaning |
|---------|-------|---------|
| **Blue Curve** | 🔵 | Impurity function curve |
| **Red Point** | 🔴 | Parent node impurity |
| **Green Points** | 🟢 | Child nodes impurity |
| **Yellow Line** | 🟡 | Chord connecting children |
| **Orange Triangle** | 🟠 | Weighted average on chord |
| **Red Dashed Line** | 🔴 | Information gain (vertical gap) |

### Key Insight

**For concave functions (Gini/Entropy):**
- The chord (yellow line) lies **below** the curve (blue)
- This creates a positive vertical gap
- Information Gain = height of curve - height of chord > 0 ✅

**For piecewise linear functions (Min):**
- The chord **coincides** with the curve
- No vertical gap exists
- Information Gain = 0 ❌

## 🎮 How to Use

### Getting Started

1. **Choose a mode:**
   - 🎓 **Educational Mode**: Learn how real decision trees work
   - 🎨 **Free Mode**: Explore and experiment freely

2. **Select an impurity function** using the tabs:
   - Gini Index
   - Entropy
   - Min (to see why it doesn't work)

3. **Adjust the sliders:**
   - **Educational Mode**: Adjust q, r, and α (p is calculated automatically)
   - **Free Mode**: Adjust all four parameters independently

4. **Observe:**
   - Information Gain updates in real-time
   - Coordinates displayed with 4 decimal precision
   - Vertical gap shows the gain visually

### Recommended Experiments

#### Experiment 1: Perfect Split (Educational Mode)
```
q = 0.0 (pure left)
r = 1.0 (pure right)
α = 0.5 (balanced split)
→ p = 0.5 (calculated)
→ Maximum information gain!
```

#### Experiment 2: No Information (Educational Mode)
```
q = 0.5
r = 0.5 (same as parent)
α = 0.5
→ p = 0.5 (calculated)
→ Zero information gain (no improvement)
```

#### Experiment 3: Unbalanced Split (Educational Mode)
```
q = 0.2
r = 0.8
α = 0.3 (70% go right)
→ p = 0.62 (calculated)
→ See how weights affect gain
```

#### Experiment 4: Why Min Fails (Educational Mode)
- Set any values for q, r, α
- Switch to Min function
- Notice: Gain is always ~0 regardless of split!

#### Experiment 5: Breaking the Constraint (Free Mode)
```
p = 0.9
q = 0.2
r = 0.8
α = 0.5
→ Orange triangle NOT under red parent
→ See the geometric difference
```

## 🚀 Deployment

### Deploy to GitHub Pages

1. Fork this repository
2. Go to **Settings** → **Pages**
3. Under **Source**, select `main` branch
4. Click **Save**
5. Your site will be live at `https://yourusername.github.io/decision-tree-convexity/`

### Deploy to Netlify

[![Deploy to Netlify](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/behradsadeghi/decision-tree-convexity)

### Deploy to Vercel

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https://github.com/behradsadeghi/decision-tree-convexity)

### Local Development

Simply open `index.html` in your browser. No build process needed!

```bash
# Clone the repository
git clone https://github.com/behradsadeghi/decision-tree-convexity.git

# Open in browser
cd decision-tree-convexity
open index.html  # macOS
start index.html # Windows
xdg-open index.html # Linux
```

## 📖 Mathematical Background

### Why Concavity Ensures Positive Information Gain

A function `f` is **concave** if for any two points and their weighted average:

```
f(αx₁ + (1-α)x₂) ≥ αf(x₁) + (1-α)f(x₂)
```

This inequality is **Jensen's Inequality** for concave functions.

In the context of decision trees:
- Left side: `f(x_avg)` = impurity at the weighted average point
- Right side: `y_avg` = weighted average of impurities
- The inequality guarantees: `f(x_avg) ≥ y_avg`
- Therefore: **Information Gain = f(x_avg) - y_avg ≥ 0** ✅

### The Decision Tree Constraint

In a real decision tree split:
- Parent has N samples with class ratio p
- After split:
  - `α × N` samples go left with class ratio q
  - `(1-α) × N` samples go right with class ratio r

This naturally enforces:
```
p = α × q + (1-α) × r
```

The **Educational Mode** simulates this constraint to show realistic splits.

### Why Linear Functions Don't Work

For piecewise linear functions like Min:
- The function is made of straight line segments
- The chord connecting two points **lies on** the function itself
- No gap exists between curve and chord
- Information Gain = 0 (always!) ❌

This is why Min (misclassification error) is not used as a splitting criterion in modern decision tree implementations.

## 🤝 Contributing

Contributions are welcome! Here are some ways you can help:

- 🐛 Report bugs by opening an issue
- 💡 Suggest new features or improvements
- 📝 Improve documentation
- 🎨 Enhance the UI/UX
- 🌍 Add translations
- 📚 Add more educational examples

### Development Setup

```bash
# Fork and clone
git clone https://github.com/yourusername/decision-tree-convexity.git
cd decision-tree-convexity

# Make your changes to index.html

# Test locally by opening index.html in browser

# Commit and push
git add .
git commit -m "Description of changes"
git push origin main
```

## 📚 Further Reading

### Academic Papers
- Breiman, L., et al. (1984). *Classification and Regression Trees*
- Quinlan, J. R. (1986). *Induction of Decision Trees*
- Friedman, J. H. (2001). *Greedy Function Approximation: A Gradient Boosting Machine*

### Online Resources
- [Scikit-learn: Decision Trees](https://scikit-learn.org/stable/modules/tree.html)
- [Information Theory and Decision Trees](https://en.wikipedia.org/wiki/Decision_tree_learning)
- [Understanding Gini Index and Entropy](https://towardsdatascience.com/)

### Related Concepts
- **Jensen's Inequality**: Foundation for understanding why concave functions work
- **CART Algorithm**: Classification And Regression Trees
- **ID3 & C4.5**: Early decision tree algorithms using entropy
- **Information Theory**: Shannon entropy and mutual information

## 🎯 Use Cases

This visualization is being used by:
- University courses on machine learning
- Online ML tutorials and blog posts
- Corporate training programs
- Self-learners exploring decision trees

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Inspired by the classic decision tree literature
- Built with [Chart.js](https://www.chartjs.org/) for beautiful visualizations
- Hosted on [GitHub Pages](https://pages.github.com/)
- Special thanks to the ML education community

## 📧 Contact

**Behrad Sadeghi**

- GitHub: [@behradsadeghi](https://github.com/behradsadeghi)
- Project Link: [https://github.com/behradsadeghi/decision-tree-convexity](https://github.com/behradsadeghi/decision-tree-convexity)
- Live Demo: [https://behradsadeghi.github.io/decision-tree-convexity/](https://behradsadeghi.github.io/decision-tree-convexity/)

## ⭐ Star History

If this project helped you understand decision trees better, please consider giving it a star!

---

<div align="center">

**Made with ❤️ for the ML community**

[🌐 Live Demo](https://behradsadeghi.github.io/decision-tree-convexity/) • [🐛 Report Bug](https://github.com/behradsadeghi/decision-tree-convexity/issues) • [💡 Request Feature](https://github.com/behradsadeghi/decision-tree-convexity/issues)

</div>
