# AI Visualized

Interactive visualizations that make AI and machine learning concepts intuitive. Built with pure HTML/CSS/JS (+ Three.js for 3D) — no build step, no frameworks, free hosting on GitHub Pages.

**[Launch the homepage](https://dondo0936.github.io/ai-visualized/)**

---

## Visualizations

| Name | Live Demo |
|------|-----------|
| Gradient Descent (3D) | [Open](https://dondo0936.github.io/ai-visualized/topics/gradient-descent.html) |
| Activation Functions | [Open](https://dondo0936.github.io/ai-visualized/topics/activation-functions.html) |
| The Perceptron | [Open](https://dondo0936.github.io/ai-visualized/topics/perceptron.html) |

More topics coming: Linear Transformations, Loss Functions, Backpropagation, Self-Attention, Tokenization, Embeddings, Softmax Temperature, KNN & Vector Search.

---

## What's inside

Each visualization is a self-contained HTML page with inline JavaScript. No npm, no bundler — open the file and it works.

- **Gradient Descent** — 3D rotatable loss surface (Three.js), three optimizers (SGD/Momentum/Adam), step-by-step mode, dual-optimizer comparison, failure preset experiments, loss chart, minimap, play-by-play narration
- **Activation Functions** — 8 functions (ReLU, Sigmoid, Tanh, Leaky ReLU, ELU, Swish, GELU, Softplus) with derivatives, parameter sliders, interactive probe
- **The Perceptron** — Click to place data points, train a single neuron, watch the decision boundary move, preset datasets, live neuron diagram

## Run locally

```bash
# Any static file server works
npx serve .
# or
python3 -m http.server 8000
```

Then open `http://localhost:8000`.

## Contributing

PRs welcome! Each topic is a standalone HTML file in `topics/`. To add a new visualization:

1. Create `topics/your-topic.html` (use any existing page as template)
2. Add a card to `index.html` in the appropriate category
3. Update the table in this README

## License

MIT
