# 🚀 TrendSpotter: The Automated Insight Engine

![Project Banner](https://workable-application-form.s3.us-east-1.amazonaws.com/advanced/production/67ee681e80c99af9453ef9e1/c83c8c79-10fd-9da0-bae2-daf435c0877c)

> **Tagline:** An event-driven data pipeline that converts raw CSV logs into executive-ready PDF reports with AI-generated narratives in under 30 seconds.

---

## 1. Problem Statement
**The Challenge:**
Marketing Account Managers currently spend 4-6 hours per week manually stitching together data from SQL and Excel to create "Weekly Performance Reports." This latency means clients often miss critical drops in Cost-Per-Visit (CPV) until it is too late to adjust the budget.

**Our Solution:**
We built **TrendSpotter**, a zero-touch pipeline. As soon as raw campaign data hits our system, it is processed, analyzed for statistical anomalies, and summarized into a natural language report distributed via Slack and Email.

## 2. Expected End Result
**For the User:**
* **Input:** Drop a raw CSV file into the folder.
* **Action:** Wait 30 seconds.
* **Output:** Receive a professionally formatted PDF via email containing:
    * Week-over-Week growth charts.
    * A list of detected anomalies (e.g., "Traffic dropped 40% in Miami").
    * An AI-written paragraph explaining *why* the drop happened (correlated with Weather API).

## 3. Technical Approach
We avoided simple "wrapper" logic and built a robust **ETL (Extract, Transform, Load)** pipeline.

**System Architecture:**
1.  **Ingestion (Event-Driven):** A Python `watchdog` script listens for file changes.
2.  **Processing (High Performance):** We use **Polars** (instead of Pandas) to clean and aggregate data 10x faster.
3.  **Anomaly Detection:** We implemented the **Isolation Forest** algorithm (Scikit-Learn) to mathematically identify outliers in foot traffic data.
4.  **Generative AI (The Analyst):**
    * We pass the anomaly metadata to **Google Gemini 1.5 Pro**.
    * We use a **Few-Shot Prompt** technique to force the AI to sound like a Senior Data Analyst.
    * *Guardrail:* We validate the AI's math against the Polars dataframe to prevent hallucinations.
5.  **Reporting:** `WeasyPrint` renders the final HTML/CSS report into a pixel-perfect PDF.



[Image of System Architecture Diagram showing Data Flow]


## 4. Tech Stack
* **Language:** Python 3.11
* **Data Engine:** Polars (Rust-based DataFrame library)
* **Machine Learning:** Scikit-Learn (Isolation Forest)
* **AI Model:** Google Gemini 1.5 Pro (via Vertex AI)
* **Orchestration:** Docker & Docker Compose
* **Visualization:** Plotly & WeasyPrint

## 5. Visual Proof
| **Anomaly Detected (Terminal)** | **Final Report (PDF)** |
| :---: | :---: |
| ![Terminal](https://via.placeholder.com/400x300?text=Isolation+Forest+Output) | ![PDF](https://via.placeholder.com/400x300?text=Executive+PDF+Report) |

## 6. How to Run
```bash
# 1. Clone Repository
git clone [https://github.com/username/trendspotter.git](https://github.com/username/trendspotter.git)

# 2. Add API Key
export GEMINI_API_KEY="your_key_here"

# 3. Build & Run Container
docker-compose up --build

# 4. Test
# Move the sample.csv to the input folder to trigger the pipeline
mv data/sample.csv data/input/
