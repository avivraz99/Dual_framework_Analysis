# User Help: Dual Framework 

## Overview
Welcome to the official codebase for the research paper: **Anomaly Detection in Citation Networks via Deep Structural Learning (GLAD) and Spectral Analysis**. 

This repository implements a robust, dual-framework approach designed to detect structural anomalies in directed graphs, specifically tailored for scholarly citation networks. It combines the rapid, deterministic execution of Spectral Analysis (using the Power Method) with the deep representational capabilities of Graph Neural Networks (GLAD) to isolate anomalous behavior such as coercive citations, citation cartels, self-citation chains, and paper mills.

---

## 🧭 User Guidance System

To ensure a smooth experience executing the pipeline, please follow this step-by-step guidance system. This system is designed to walk you through data formatting, environment configuration, and execution of the dual frameworks.

### Step 1: Prerequisites & Requirements
To operate the system successfully, you must have the following environment set up:
* **Compute Environment:** Google Colab with a **GPU runtime enabled** (strictly required for `cuML`, `CuPy`, and PyTorch tensor execution).
* **Dependencies:** Python 3.x, `torch`, `networkx`, `scipy`, `numpy`, `pandas`, `cuml`, `cupy`, `scikit-learn`, `plotly`, `ipywidgets`, `firebase_admin`, and `google-genai`. *(Note: The provided notebook contains a cell to install required external packages automatically).*
* **API Keys/External Services:**
  * **Firebase Service Account Key (JSON):** Required if you plan to import the default dataset or back up your dataset to Firebase Storage.
  * **Gemini API Key:** Required to utilize the "Create AI Report" advanced summarization feature.
  * 📝 **Note on Credentials:** *The notebook comes pre-configured with a default Gemini API key and Firebase JSON file so you can run the project out-of-the-box. However, you can easily change or update these credentials within the notebook if you prefer to use your own personal accounts.*

### Step 2: Getting Started
1. **Get the Code:** You have a few options to access the environment:
   * Clone this GitHub repository to your local machine.
   * Mount it directly into your Google Drive for Colab access.
   * **Download the `Project_Phase_B.ipynb` file directly from this repository and upload it to Google Colab.**
2. **Open the Environment:** Ensure `Project_Phase_B.ipynb` is open in Google Colab.
3. **Initialize the System:** From the Colab top menu, select **Runtime > Run all**. This will:
   * Install the required libraries.
   * Initialize Firebase.
   * Compile the model definitions.
   * Launch the interactive visual interface at the bottom of the notebook.


### Step 3: Pipeline Execution Stages
Once the UI is loaded, execute the framework using the interactive portal:

#### Stage 1: The Entry Page
* Upon launching the interface, the welcome portal will appear. 
* Click the **Start Analysis** button to proceed.

#### Stage 2: The Parsing Page (Dataset Setup)
* **Select Data Source:** * Choose **"Import from Firebase (Default)"** to pull the pre-configured OpenAlex Computer Science citation subgraph.
  * Choose **"Upload a New Dataset"** to use your own academic data.
    * *Requirement for Custom Data:* The uploaded file must be a CSV explicitly named `papers_metadata.csv`. It must include the columns: `id`, `referenced_works`, and `primary_topic` (which must contain 'Computer Science' entries).
* **Run the Pipeline:** Click **Load and Generate Datasets**. The system will automatically parse your graph and inject 5 synthetic anomaly typologies for controlled validation. It will then initiate the multi-run learning loop (N=5) and Power Method computation.
* *Note: The evaluation loop may take several minutes depending on the graph size. Once finished, the dashboard will open automatically.*

#### Stage 3: Multi-Perspective Result Analysis (The Dashboard)
The final stage provides an interactive dashboard to explore the topological results:
* **Select Dataset:** Toggle between the 5 generated anomaly scenarios (e.g., Coercive Citations, Citation Cartels) to see how the system responded to different threats.
* **Select View:** Navigate through various visual analytics:
  1. **Convergence Analysis Plots:** View Recall@K, Precision@K, and Overlap Ratios comparing the global spectral baseline against the local GNN metrics.
  2. **Anomaly Score Distribution:** Inspect logarithmic histograms mapping the statistical separability of normal versus injected anomalous nodes.
  3. **Local Topological Visualizations:** Examine the directed structural neighborhoods (subgraphs) of heavily flagged nodes.
  4. **3D Network Visualization:** Explore the manipulated network topography interactively via Plotly.
* **Advanced Features & Export:** * **Download Raw Data:** Extract the raw numeric convergence metrics log to your local machine for further academic review.
  * **Create AI Report:** Automatically summarize the empirical performance using the integrated Gemini API to output a comprehensive, publication-ready markdown analysis.

