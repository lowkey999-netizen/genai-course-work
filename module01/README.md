# Module 01: Foundations & The Model Landscape

This module covers the core physics and economics of Large Language Models: token counting, context window limitations, pricing tiers, high-dimensional vector embeddings, dimensionality reduction (PCA/SVD), and multi-provider orchestration.

---

## Session Directory & Coursework Map

The table below organizes all notebooks, helper modules, datasets, and readings for Module 01:

| Session                                             | Core Lab Notebook                                    | Helper Modules & Data                                                                                                                                              | Concept Docs & Terms                                                                     | Interactive Tools & Visualizers                                                                                                                                                                                                                                                                                                                                                                                                                |
| --------------------------------------------------- | ---------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Session 09b**<br>_Tokens & Embeddings_            | [`s09_tokens.ipynb`](./s09_tokens.ipynb)             | • [`tokens_utils.py`](./tokens_utils.py)<br>• [`embeddings_10words.json`](./embeddings_10words.json)<br>• [`make_embeddings_cache.py`](./make_embeddings_cache.py) | • [`reading_tokens.md`](./reading_tokens.md)<br>• [`terms_s09.md`](./terms_s09.md)       | • [Complete Pipeline Visualizer](https://raw.githack.com/lowkey999-netizen/genai-course-work/main/module01/pipeline_visualizer.html)<br>• [Interactive Embedding & PCA Journey](https://raw.githack.com/lowkey999-netizen/genai-course-work/main/module01/interactive_embedding_pca_journey.html)<br>• [Embeddings & Dimensions Sliders](https://raw.githack.com/lowkey999-netizen/genai-course-work/main/module01/embeddings_visualizer.html) |
| **Session 10**<br>_The Model Landscape_             | [`s10_model_matrix.ipynb`](./s10_model_matrix.ipynb) | • [`landscape_utils.py`](./landscape_utils.py)<br>• [`models_catalog.json`](./models_catalog.json)<br>• `s10_matrix_output.md`                                     | • [`reading_landscape.md`](./reading_landscape.md)<br>• [`terms_s10.md`](./terms_s10.md) | • Model matrix comparison table<br>• Speed vs. intelligence tradeoffs                                                                                                                                                                                                                                                                                                                                                                          |
| **Session 11**<br>_Multi-Provider Calls & Sampling_ | [`s11_providers.ipynb`](./s11_providers.ipynb)       | • [`providers_utils.py`](./providers_utils.py)<br>• [`tickets_data.py`](./tickets_data.py)                                                                         | • [`reading_providers.md`](./reading_providers.md)<br>• [`terms_s11.md`](./terms_s11.md) | • Multi-provider routing (Groq, Ollama)<br>• Temperature & sampling sweeps                                                                                                                                                                                                                                                                                                                                                                     |

---

## Interactive Intuition Guides & Visualizations

This module includes three standalone, animated visual guides created to build deep intuitive mental models for embeddings, vector geometry, PCA, and SVD.

### One-Click Previews (via Raw.Githack CDN)

- **[Complete Embedding & SVD Pipeline Visualizer](https://raw.githack.com/lowkey999-netizen/genai-course-work/main/module01/pipeline_visualizer.html)**  
  _Walks step-by-step through the entire pipeline: `Word → Vector (Sliders) → 768D Space → PCA Shadow → SVD Engine (Rotate/Stretch/Rotate) → Final 2D Matplotlib Plot`._

- **[Interactive Embedding & PCA Journey](https://raw.githack.com/lowkey999-netizen/genai-course-work/main/module01/interactive_embedding_pca_journey.html)**  
  _An interactive visual exploration of multi-dimensional vector spaces and how dimensionality reduction flattens high-dimensional semantic clouds._

- **[Embeddings & Dimensions Sliders Visualizer](https://raw.githack.com/lowkey999-netizen/genai-course-work/main/module01/embeddings_visualizer.html)**  
  _Builds intuition on how words turn into coordinate sliders and why semantic similarity is measured as angles (cosine similarity)._

---

### Running Locally on Your Machine

1. Open your terminal or file explorer and go to `module01/`.
2. Double-click any `.html` file (or right-click → **Open with** → Chrome, Edge, Safari, or Firefox).
3. The visualizer runs locally in your browser with zero dependencies or server setup required.
