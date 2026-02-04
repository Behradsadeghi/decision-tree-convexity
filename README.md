# Decision Tree Convexity Visualization 🌳📊

An interactive web-based visualization tool that demonstrates why **Gini Index** and **Entropy** work as impurity measures in decision trees, while **Min** (misclassification error) doesn't.

[![Live Demo](https://img.shields.io/badge/demo-live-success)](https://behradsadeghi.github.io/decision-tree-convexity/)
[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![GitHub Pages](https://img.shields.io/badge/hosted-GitHub%20Pages-blue)](https://pages.github.com/)

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

## 🚀 Live Demo

### **[👉 Try it now! 👈](https://behradsadeghi.github.io/decision-tree-convexity/)**

Experience the interactive visualization at: `https://behradsadeghi.github.io/decision-tree-convexity/`

## ✨ Features

- 🎚️ **Interactive Controls**: Adjust parent and children impurity values with real-time updates
- 📊 **Three Impurity Functions**: Switch between Gini, Entropy, and Min to see the difference
- 📐 **Geometric Visualization**: See the chord connecting children points and the curve above it
- 🔢 **Precise Calculations**: All coordinates and information gain shown to 4 decimal places
- 📱 **Responsive Design**: Works perfectly on desktop, tablet, and mobile
- 🎨 **Beautiful UI**: Modern gradient design with smooth animations
- 🧮 **Mathematical Accuracy**: Implements exact formulas for all impurity functions

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

```javascript
// Weighted average of children (point on chord)
x_avg = α * q + (1-α) * r
y_avg = α * impurity(q) + (1-α) * impurity(r)

// Information gain (vertical distance)
Gain = f(x_avg) - y_avg
```

Where:
- `q` = left child class ratio
- `r` = right child class ratio
- `α` = fraction of samples going left
- `f()` = impurity function

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

1. **Select an impurity function** using the tabs at the top
2. **Adjust the sliders:**
   - **Parent Point (p)**: The class ratio at the parent node
   - **Left Child (q)**: Class ratio if split goes left
   - **Right Child (r)**: Class ratio if split goes right
   - **Left Weight (α)**: Fraction of samples going to left child
3. **Observe the changes:**
   - Watch the information gain update in real-time
   - See coordinates with 4 decimal precision
   - Notice how the vertical gap changes

### Recommended Experiments

Try these configurations to build intuition:

**Experiment 1: Pure Split**
- p = 0.5, q = 0.0, r = 1.0, α = 0.5
- Observe maximum information gain

**Experiment 2: No Information**
- p = 0.5, q = 0.5, r = 0.5, α = 0.5
- Observe zero information gain (no improvement)

**Experiment 3: Unbalanced Split**
- p = 0.5, q = 0.3, r = 0.7, α = 0.3
- See how weights affect the gain

## 🚀 Deployment

### Deploy to GitHub Pages

1. Fork this repository
2. Go to **Settings** → **Pages**
3. Under **Source**, select `main` branch
4. Click **Save**
5. Your site will be live at `https://yourusername.github.io/decision-tree-convexity/`

### Deploy to Netlify

[![Deploy to Netlify](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/yourusername/decision-tree-convexity)

### Deploy to Vercel

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https://github.com/yourusername/decision-tree-convexity)

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

In our case:
- Left side = `f(x_avg)` = impurity at the weighted average point
- Right side = `y_avg` = weighted average of impurities
- The inequality guarantees: `f(x_avg) ≥ y_avg`
- Therefore: **Information Gain = f(x_avg) - y_avg ≥ 0** ✅

### Why Linear Functions Don't Work

For piecewise linear functions like Min:
- The function is made of straight line segments
- The chord connecting two points **lies on** the function itself
- No gap exists between curve and chord
- Information Gain = 0 (always!) ❌

## 🤝 Contributing

Contributions are welcome! Here are some ways you can help:

- 🐛 Report bugs by opening an issue
- 💡 Suggest new features or improvements
- 📝 Improve documentation
- 🎨 Enhance the UI/UX
- 🌍 Add translations

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

### Related Projects
- [Interactive ML Visualizations](https://github.com/topics/machine-learning-visualization)
- [Decision Tree Playground](https://github.com/topics/decision-tree)

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Inspired by the classic decision tree literature
- Built with [Chart.js](https://www.chartjs.org/) for beautiful visualizations
- Hosted on [GitHub Pages](https://pages.github.com/)

## 📧 Contact

**Behrad Sadeghi**

- GitHub: [@behradsadeghi](https://github.com/behradsadeghi)
- Project Link: [https://github.com/behradsadeghi/decision-tree-convexity](https://github.com/behradsadeghi/decision-tree-convexity)

---

<div align="center">

**If this helped you understand decision trees better, give it a ⭐!**

Made with ❤️ for the ML community

[🌐 Live Demo](https://behradsadeghi.github.io/decision-tree-convexity/) • [🐛 Report Bug](https://github.com/behradsadeghi/decision-tree-convexity/issues)

</div>
