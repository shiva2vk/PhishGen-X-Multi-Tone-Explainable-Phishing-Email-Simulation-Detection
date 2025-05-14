#  PhishGen-X: Multi-Tone, Explainable Phishing Email Simulation & Detection

##  Abstract

**PhishGen-X** is a cybersecurity project designed to simulate and detect phishing emails using modern NLP techniques. It uniquely integrates **GPT-2** to generate realistic multi-tone phishing emails and **BERT** for classifying them, enriched with **explainability using SHAP**. The project supports adversarial email simulation, psychological tactic tagging, and visual diagnostics, making it ideal for AI-driven phishing detection research and SOC analyst training tools.

---

##  Neural Network Architecture

###  Phishing Email Generator (GPT-2)
- Model: `GPT2LMHeadModel`
- Role: Generates phishing emails with configurable tone, intent, and target.
- Features: Temperature sampling, nucleus filtering, repeat penalty.

###  Phishing Detector (BERT)
- Model: `BertForSequenceClassification`
- Role: Binary classifier (phishing vs legitimate).
- Fine-tuned on simulated and real email datasets.

###  SHAP Explainability Layer
- Uses `shap.Explainer` and Hugging Face `TextClassificationPipeline`.
- Provides token-level attribution for BERT predictions.

---

##  Pipeline Overview

1. **Generate Emails** using `generate_phishing_email(tone, intent, target)`
2. **Simulate Threads** with `simulate_email_thread(initial_email)`
3. **Train Detector** using `train_explainable_detector(phish_emails, legit_emails)`
4. **Classify and Explain** via `infer_and_explain(email_text)` using BERT + SHAP
5. **Tag Social Engineering Tactics** using rule-based keyword extractor

---

## Dataset Used

-  wget https://www.cs.cmu.edu/~enron/enron_mail_20110402.tgz 
-  Custom simulated phishing emails generated via GPT-2
-  Legitimate emails sourced from Enron dataset or user input
-  Balanced classes (phishing = legit) for robust training
-  Future extensibility for real APT samples or red-team scenarios

---

##  Novelty in This Project

 Uses GPT-2 to dynamically generate **multi-tone phishing emails**.
 Simulates **threaded email conversations** using autoregressive modeling.
 Adds **SHAP-based explainability** to visualize why an email was classified as phishing.
 Combines GPT-generated attacks with a **BERT-based phishing detector** for robust adversarial training.
 Implements an adversarial generator-detector loop using transformer models.



##  What Makes This Project Unique?

PhishGen-X goes beyond traditional phishing detection pipelines by integrating **adversarial generation**, **threaded simulation**, and **explainable AI** in a unified system.

### Novel Features & Innovations:

- ** Generative Phishing Simulation (GPT-2)**  
  Unlike most datasets that rely on static phishing samples, PhishGen-X uses GPT-2 to **generate phishing emails on the fly**, allowing simulation of:
  - Different tones (e.g., urgent, friendly, fearful)
  - Varied social engineering intents (e.g., credential theft, malware delivery)
  - Multiple target departments (e.g., HR, IT, Finance)

- ** Threaded Email Conversations**  
  Simulates realistic **multi-turn email threads** using GPT-2 autoregressive replies — a rarity in most phishing datasets and detection systems that analyze only single-shot emails.

- ** SHAP Explainability Layer**  
  Provides **token-level attribution** showing which words made an email look like phishing — useful for:
  - Analyst trust
  - Forensic review
  - Model debugging

- ** Dual-Tactic Detector**  
  Combines:
  - A fine-tuned **BERT model** for classification
  - A **rule-based psychological tagger** that detects urgency, fear, and manipulation tactics
  
- ** Generator vs Detector Adversarial Setup**  
  The same pipeline that generates phishing emails is used to challenge and evaluate the robustness of the phishing detector — enabling **automated red-team vs blue-team testing**.

---

###  Why It’s Better Than Standard Approaches

| Traditional Detectors         | PhishGen-X                          |
|------------------------------|-------------------------------------|
| Static email samples          | Dynamically generated emails       |
| Single-message inference      | Threaded email simulation          |
| No explainability             | SHAP-based token attribution       |
| One-size-fits-all model       | Customizable by tone, intent, target |
| Lacks adversarial testing     | Built-in adversarial challenge loop |

---

##  Use Cases

- ✔️ Training datasets for phishing detectors
- ✔️ Testing SOC alerting systems under adversarial conditions
- ✔️ Research on explainable AI for cybersecurity
- ✔️ Education: teach employees about phishing through AI-generated examples
- ✔️ Dataset augmentation for low-data security environments

---

##  Pros

- ✔️ End-to-end pipeline: generation, simulation, detection, and explanation
- ✔️ Human-readable explanations with SHAP
- ✔️ Customizable phishing tone, intent, and target
- ✔️ Works with simulated and real emails
- ✔️ Lightweight and modular design

---

##  Cons

-  GPT-2 may hallucinate unrelated content
-  SHAP runs slowly on CPU and doesn't scale well to thousands of samples
-  Rule-based tactic tagging could be improved with NLP models
-  Model performance is sensitive to imbalanced or noisy training data

---

##  Requirements

- `transformers`
- `torch`
- `shap`
- `scikit-learn`
- `matplotlib`, `seaborn`
- GPU recommended for training


## Authors

- Developed by Vivek K.  
- 

---

##  License

MIT License
