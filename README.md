# Spectral-Check: Graph-Theoretic Hallucination Detection

This project proposes **Spectral-Check**, a significant methodological advancement over the baseline **LLM-Check** framework. It transitions hallucination detection from simple scalar probability analysis to spectral graph theory, while expanding the domain from text-only to multimodal environments.

## 1. The Baseline: LLM-Check (NeurIPS 2024)
*   **Methodology:** Utilized **Scalar Analysis**. It detected hallucinations by summing the log-probabilities of the diagonal entries in the Self-Attention matrix (the "Attention Score").
*   **Domain:** Strictly **Text-only** (e.g., summarizing news or checking facts).
*   **Proxy Model:** Used standard Text LLMs (e.g., Llama-2).
*   **Limitation:** By treating attention weights as simple scalar sums, it failed to capture the structural "shape" of information flow and could not handle visual inputs.

## 2. The Improvement: Spectral-Check (Proposed)
*   **Methodology:** Utilizes **Spectral Graph Theory**. We interpret the attention mechanism as a weighted directed graph. Instead of summing probabilities, we compute the **Laplacian Eigenvalues** ($L = D - A$) of the attention map. This allows us to detect hallucinations as specific "structural breaks" or bottlenecks in the model's reasoning process.
*   **Domain:** **Joint Cross-Modal & Cross-Lingual**. We address the "Curse of Multi-Modalities" by verifying if generated text aligns with input images across different languages.
*   **Proxy Model:** Replaces the text-only proxy with a Vision-Language Model (**Qwen2-VL**) to enable visual grounding.

## Comparison Summary

| Feature | Base Paper (LLM-Check) | Our Improvement (Spectral-Check) |
| :--- | :--- | :--- |
| **Mathematical Basis** | Scalar (Log-Determinant) | Graph Theory (Laplacian Eigenvalues) |
| **Detection Signal** | Uncertainty / Entropy | Structural Connectivity |
| **Input Modality** | Text $\to$ Text | Image + Text $\to$ Multilingual Text |
| **Model Architecture**| Llama-2 (Text) | Qwen2-VL (Vision-Language) |
