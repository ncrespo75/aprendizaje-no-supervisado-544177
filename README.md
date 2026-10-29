# Unsupervised Learning — Students

Hands-on Jupyter Notebooks for the unsupervised learning module of the course (UDEM): clustering with **K-Means** and **DBSCAN**, dimensionality reduction with **PCA**, and a capstone case that combines them.

## Project Structure

Each session folder has the theory notebook (`fundamentos.ipynb`), the lab you complete in class (`caso_*.ipynb`) and the slides.

**Session 0 — Foundations**
- `00-fundamentos/fundamentos.ipynb`: Theory — supervised vs unsupervised, distances (euclidean, Manhattan, cosine, Haversine), why scaling matters, evaluating a clustering with the silhouette
- `00-fundamentos/slides/`: Introduction to unsupervised learning

**Session 1 — K-Means**
- `01-kmeans/fundamentos.ipynb`: Theory — Lloyd's algorithm step by step, inertia, k-means++ and `n_init`, elbow + silhouette, limitations (moons, circles, uneven sizes)
- `01-kmeans/caso_mall.ipynb`: 🎯 3-hour lab — customer segmentation of a shopping mall (2D and 3D), choosing k with several metrics, naming each segment and a campaign per segment
- `01-kmeans/slides/`: Slides for the session

**Session 2 — DBSCAN**
- `02-dbscan/fundamentos.ipynb`: Theory — core/border/noise points, ε and `min_samples`, k-distance plot, DBSCAN vs K-Means, varying densities and HDBSCAN
- `02-dbscan/caso_mall.ipynb`: 🎯 Lab — DBSCAN on the same mall customers: who are the outliers and how does it compare with K-Means
- `02-dbscan/caso_entregas.ipynb`: 🎯 Lab — synthetic GPS deliveries in Monterrey: Haversine distance and where to open micro distribution centers
- `02-dbscan/slides/`: Slides for the session

**Session 3 — PCA**
- `03-pca/fundamentos.ipynb`: Theory — PCA by hand in 2D, projection and reconstruction, scaling, scree plot, loadings and biplot
- `03-pca/caso_vinos.ipynb`: 🎯 3-hour lab — how many chemical measurements do we really need to tell the wines apart? (Wine dataset)
- `03-pca/slides/`: Slides for the session

**Session 4 — Capstone case**
- `04-caso-integrador/caso_mayoristas.ipynb`: 🎯 3-hour lab — wholesale customers: log transform → scaling → PCA → K-Means and DBSCAN → profiles in original units → business recommendations
- `04-caso-integrador/datos/wholesale_customers.csv`: Dataset (UCI, CC BY 4.0)
- `04-caso-integrador/slides/`: From data to decision — the full unsupervised workflow

**Extra material** (demos not worked in class)
- `extra/mnist/compresion_mnist.ipynb`: Compressing MNIST digits with PCA
- `extra/eigenfaces/eigenfaces.ipynb`: Eigenfaces and progressive face reconstruction (downloads ~200 MB the first time)
- `extra/digits/pca_kmeans_digits.ipynb`: PCA before K-Means on handwritten digits, evaluated with the silhouette and a crosstab against the real digit
- `extra/mascotas-virtuales/index.html`: Standalone virtual-pet demo; open it in a browser to feed, play with, and customize a pet

**Environment**
- `pyproject.toml` / `uv.lock`: Project dependencies and the exact pinned versions
- `.python-version`: Exact Python version used everywhere
- `.devcontainer/`: GitHub Codespaces / Dev Container configuration

Lab notebooks start with a "Preparación" section of helper functions (plots, clustering metrics, data loading): run those cells once and then just call the functions.

## Tools and Technologies

- Python 3.14 (exact version in `.python-version`)
- [uv](https://docs.astral.sh/uv/) to manage Python and dependencies
- Jupyter Notebooks (VS Code + Jupyter extension)
- pandas, NumPy, SciPy, scikit-learn, Plotly, Matplotlib

## Environment

The local environment and GitHub Codespaces are built from the same files, so they are identical:

- `.python-version` pins the exact Python version (installed by uv, same build on every machine).
- `uv.lock` pins the exact version of every package.
- Codespaces runs `uv sync --frozen` when the container is created, which is the same command used locally.

### Option A: GitHub Codespaces (recommended)

Click **Code → Codespaces → Create codespace on main**. When the setup finishes, open any notebook and select the `.venv` kernel.

### Option B: Local

1. Install uv:
   ```bash
   # macOS
   brew install uv

   # Windows (PowerShell)
   powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
   ```

2. Clone this repository and create the environment:
   ```bash
   git clone https://github.com/jorgermzg15/aprendizaje-no-supervisado-student.git
   cd aprendizaje-no-supervisado-student
   uv sync --frozen
   ```

3. Open the folder in VS Code and select the `.venv` interpreter/kernel in the notebooks.

### Updating dependencies (maintainer)

```bash
uv lock --upgrade   # resolve the newest compatible versions
uv sync --frozen    # apply them locally
```

Commit `uv.lock` (and `.python-version` if you change it). Codespaces will pick up the same versions on the next rebuild.

## Troubleshooting

1. Make sure the notebook kernel is the project's `.venv` (not a Conda/Anaconda environment).
2. If the environment gets out of sync, recreate it:
   ```bash
   rm -rf .venv
   uv sync --frozen
   ```
3. In Codespaces, if something breaks after changing `.devcontainer/`, run **Codespaces: Rebuild Container** from the command palette.
4. Some notebooks download data the first time (Mall Customers CSV, MNIST, LFW faces) and need internet access.

## For Students

Each lab tells the story of a business question. Make sure to:

1. Follow the environment instructions carefully
2. Run the "Preparación" cells first, then execute the notebook cells in order
3. Complete the cells marked with ✍️ (`# ✍️ Tu código aquí` and `RELLENAR CON TUS COMENTARIOS`) in the labs (`caso_*.ipynb`) and in the short exercises of each `fundamentos.ipynb`
4. Experiment with the parameters (k, eps, number of components) to deepen your understanding

## License

This project is available for educational purposes. Feel free to use and learn from it!

## Data Credits

- **Mall Customers**: hosted in [jorgermzg15/data-files](https://github.com/jorgermzg15/data-files).
- **Wholesale customers**: Fernandes Cardoso, M. G. M. (2014). *Wholesale customers* [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C5030X — licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).
- **Wine, Iris, digits** (`sklearn.datasets`), **MNIST** (OpenML) and **Labeled Faces in the Wild** (`fetch_lfw_people`).
- The GPS deliveries of `02-dbscan/caso_entregas.ipynb` are synthetic (generated with a fixed seed).
