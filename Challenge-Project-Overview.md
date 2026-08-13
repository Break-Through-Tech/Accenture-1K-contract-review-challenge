---

> ## Challenge Advisor: Update & Finalize Your Project Overview
>
> > 💡 **These grey text instructions are just for you, the team's Challenge Advisor; please delete them once you have completed the steps below.**
>
> We've pre-populated this Challenge Project Overview page — which is what will be shared with your Break Through Tech student team in August — using the details from your submission form. You should have received an email inviting you to join this repo as a Collaborator, enabling you to add files and make edits.
> 
> In order for your project to be finalized and assigned to a team, please:
> 1. **Review all sections below** and update or expand any content as needed, making sure to address the SME Feedback in the section immediately below. Look for square brackets to find the places below that require additional inputs from you (e.g., "About [Company / Org Name]").
> 2. **Add your dataset** to the [data folder](data) in this repo.
> 3. **Close the Issue assigned to you in this repo** to let us know that you have made your edits and the overview page is ready for final review. You can do this by going to the _Issues_ tab in the top left section of the menu above, add a comment that says "CA review complete", and click the button to Close the Issue. 
>
> If you're unfamiliar with how to edit a page like this in GitHub, check out [this tutorial](https://ubc-lib-geo.github.io/gis-workshop-waml-template/content/handson/edit-readme.html) for a quick overview (start with step 2 and only edit this page), and [this guide](https://ubc-lib-geo.github.io/gis-workshop-waml-template/content/markdown.html) on how to use Markdown to compose text.
>
>
> ❌ Remember that this is a public repo. Do NOT include: Proprietary data, PII, API keys, credentials, or anything confidential.

---

## 📋 BTT Internal Evaluation Notes
*(This section is for BTT staff and CAs only — remove before sharing with students)*

### Technical Vetting
| Check | Status | Notes |
| :--- | :--- | :--- |
| Python Compatibility | 🟢 | Project utilizes standard libraries (HuggingFace transformers, scikit-learn, pandas) compatible with free-tier Google Colab environments. |
| Data Readiness | 🟡 | CUAD dataset is well-structured but requires significant effort to parse raw PDF text and align token-level labels for 41 categories, which may consume excessive time during early weeks. |
| Resource Check | 🟢 | Project fits within memory constraints; however, fine-tuning large transformer models will require careful batch size management in Colab. |

### Internal Scores
- **Student Fit Score:** 7/10
- **Technical Depth Score:** 8/10
- **Overall Recommendation:** REVISE

### Advisor Feedback Draft
The CUAD-based contract triage pipeline is a high-value industrial use case with excellent potential for technical rigor. To ensure success within the timeframe of the program, I suggest: (i) pivoting from fine-tuning from scratch to utilizing pre-trained lightweight models (e.g., DistilRoBERTa) to reduce hardware overhead demand; and (ii) constraining the scope by focusing on the 10 most impactful clause categories, and having the full 41 as a stretch goal.

---

# Contract Review Challenge

**Company / Org:** Accenture  
**Challenge Advisor:** Adarsh Ravikumar, adarsh.ravikumar@accenture.com  \
**AI Studio Coach:** Shweta Malabade, shweta.malabade@breakthroughtech.org  \
**Program:** Break Through Tech AI Studio - Fall 2026  

---

## 🏢 About Accenture
Accenture is a leading global professional services company that provides a broad range of services and solutions in strategy, consulting, technology, and operations. 

---

## 🎯 The Challenge
### Project Summary
In this project, you will use real-world commercial contracts from the CUAD dataset (510 contracts, 41 expert-annotated clause categories) and NLP techniques including chunk-based multi-label classification with fine-tuned transformer encoders, paired with an explainable rule-based risk-scoring layer, to build a pipeline that automatically detects key clauses, flags them as Low/Medium/High risk, and rolls these up into a contract-level triage score. The team will fine-tune a pre-trained lightweight transformer encoder (e.g., DistilRoBERTa) rather than training a model from scratch, and will focus initial clause detection on the 10 most impactful clause categories, with full coverage of all 41 CUAD categories as a stretch goal. This will help our company address the bottleneck legal and procurement teams face when manually reviewing tens of thousands of contracts a year to find the small number of clauses that carry meaningful risk, enabling reviewers to prioritize which contracts to open first.

### Success Criteria
Success has two tracks:
- For clause detection: per-category precision/recall/F1 clearly beating the baseline (accuracy is misleading under CUAD's imbalance), with error analysis on where the model struggles.   
- For risk scoring: since there are no ground-truth labels, success means strong Spearman correlation and bucket agreement between the model's risk rankings and the advisor's hand-ranked clauses, plus a sensitivity analysis showing the High/Medium boundary is stable.

Overall, a successful December outcome is a working end-to-end pipeline producing risk-scored clause registers the advisor finds plausible and useful, a clean documented repo, and a final report covering results, limitations, and estimated reviewer time saved — an auditable triage tool the advisor would actually trust, not a black box.

### Stretch Goals
Stretch goals include span extraction, a trained risk model benchmarked against the rule-based baseline, LLM-generated clause explanations, broader category coverage, a Streamlit/Gradio demo, and an active-learning loop using advisor/model disagreements. These extend modeling or usability without affecting core deliverables.

### Project Milestones
Use these milestones to guide your work. Your team will create a GitHub Projects board to track tasks within each milestone.
| Month | Milestone | Key Activities |
|-------|-----------|----------------|
| **September** | [Title] | Clean and split the CUAD data, run EDA on class imbalance, build a chunking strategy, and establish a TF-IDF/keyword baseline with per-category metrics. |
| **October** | [Title] | Fine-tune a transformer encoder for multi-label clause classification, address class imbalance, evaluate with per-category precision/recall/F1, and conduct error analysis. |
| **November** | [Title] | Build and calibrate the four-signal risk-scoring layer, assemble the end-to-end pipeline, and validate risk rankings against advisor-labeled examples. |

> **Note for the team:** Please create a GitHub Projects board in this repository to break these milestones into weekly tasks. Go to the **Projects** tab → **New project** → Choose **Board** → Add columns for each month.

---

## 📊 Dataset
**Name and Source:** CUAD Dataset (Contract Understanding Atticus Dataset)  
**Format:** JSON, Raw Text/PDF  
**Size:** under 1gb  
**Location:** https://github.com/TheAtticusProject/cuad  

### Key Details
- Real-world commercial contracts from the CUAD dataset (510 contracts, 41 expert-annotated clause categories), raw text/PDF available.
- Teams must implement strict preprocessing rules to handle document length variance and ensure text cleaning captures the necessary legal terminology for high-accuracy classification.
- Initial clause detection is scoped to the 10 categories below, with full coverage as a stretch goal.

### Focus Categories
| Category | Contracts (of 510) | Share |
|---|---|---|
| Governing Law | 437 | 85.7% |
| Anti-Assignment | 374 | 73.3% |
| Cap On Liability | 275 | 53.9% |
| License Grant | 255 | 50.0% |
| Audit Rights | 214 | 42.0% |
| Termination For Convenience | 183 | 35.9% |
| Exclusivity | 180 | 35.3% |
| Change Of Control | 121 | 23.7% |
| Non-Compete | 119 | 23.3% |
| Uncapped Liability | 111 | 21.8% |

---

## 🛠️ Suggested Approach
**ML Problem Type:** NLP & Classification  
**Recommended Libraries:** HuggingFace Transformers, PyTorch/TensorFlow, Scikit-learn, Pandas  
**Modeling Approach:** Fine-tune a pre-trained lightweight transformer encoder (e.g., DistilRoBERTa) rather than training from scratch.  
**Evaluation Metrics:** Precision, Recall, F1-Score for classification; Spearman Correlation for risk-ranking alignment.

---

## 📚 Resources to Get Started
The following resources will help your team understand the problem space and potential technical approaches for this project:

**Background Reading:**
- [CUAD: An Expert-Annotated NLP Dataset for Legal Contract Review (Hendrycks et al., 2021)](https://arxiv.org/abs/2103.06268) — the original paper introducing the dataset. Covers what the 41 clause categories are, why transformer models struggle with this task, and how performance is shaped by model design and training data.
- [Multi-label NLP: An Analysis of Class Imbalance and Loss Function Approaches (KDNuggets, 2023)](https://www.kdnuggets.com/2023/03/multilabel-nlp-analysis-class-imbalance-loss-function-approaches.html) — explains why multi-label classification becomes hard under imbalance and how loss functions like weighted BCE and Focal Loss address it. Directly relevant to the class imbalance problem in CUAD.
- [AI Explainability in Contract Risk Scoring (Sirion, 2026)](https://www.sirion.ai/library/contract-insights/ai-explainability-tools-contracts/) — a practical explainer on how flagged clauses are traced back to their rationale to produce auditable decisions rather than black-box outputs. Useful context for framing the risk-scoring layer.

**Technical Tutorials:**
- [Learn Hugging Face: Text Classification Tutorial](https://www.learnhuggingface.com/notebooks/hugging_face_text_classification_tutorial) — a hands-on, code-focused walkthrough for loading a pretrained DistilBERT model, fine-tuning it on a custom dataset, and evaluating results. Reusable patterns directly applicable to this project.
- [HuggingFace Official Docs: Sequence Classification](https://huggingface.co/docs/transformers/tasks/sequence_classification) — the canonical reference for fine-tuning encoder models (DistilBERT, RoBERTa, DistilRoBERTa) using the `Trainer` API. Covers tokenization, `TrainingArguments`, `DataCollatorWithPadding`, and evaluation hooks.
- [Spearman Rank Correlation Explained (Simplilearn)](https://www.simplilearn.com/tutorials/statistics-tutorial/spearmans-rank-correlation) — a clear introduction to Spearman's ρ as a non-parametric measure of ranking agreement. Relevant for evaluating whether the model's contract risk rankings match the advisor's hand-ranked examples.

**Code Examples:**
- [Official CUAD GitHub Repository (The Atticus Project)](https://github.com/TheAtticusProject/cuad) — contains the dataset, baseline model code, and evaluation scripts from the original paper. Good reference for understanding the intended evaluation setup before adapting it to a classification framing.
- [CUAD on Hugging Face Datasets](https://huggingface.co/datasets/cuad) — loads the dataset directly via `datasets.load_dataset("cuad")`, bypassing manual JSON parsing and enabling easy integration with the HuggingFace `Trainer` pipeline. The fastest way to get data into a training loop.
- [Hybrid NLP Framework for Contract Risk Assessment (IJSRS, 2025)](http://ijsrs.org/v2i11/1.php) — an implementation paper combining fine-tuned RoBERTa with a rule-based risk assessment layer, close in architecture to what this project is building. Includes a Streamlit interface and covers the explainability angle explicitly — useful as a reference design.

**Other:**
- [Stanford CS224N HuggingFace Transformers Tutorial (2026)](https://web.stanford.edu/class/cs224n/materials/hf_transformers_tutorial.pdf) — lecture slides from Stanford's NLP course covering the full HuggingFace ecosystem: tokenizers, AutoModel classes, the Trainer API, and fine-tuning on custom datasets. Good structured background before diving into project code.
- [DistilRoBERTa Base Model Card (HuggingFace)](https://huggingface.co/distilroberta-base) — the recommended base model per the advisor's guidance. The model card explains its distillation from RoBERTa, speed/accuracy tradeoffs, and how to load it for sequence classification.

*Feel free to explore beyond these, and share anything interesting you find with me!*

---

## 🤝 How We'll Work Together

**Official check-ins:** During our biweekly 45-minute AI Studio Lab Section meeting block (2nd and 4th week of every month)

 **Other ways to reach out to me with questions:** 
* [e.g., Your team's channel within Break Through Tech’s Discord space]
* [e.g., Email; please copy your teammates and AI Studio Coach]
* [e.g., Request a team check-in on Zoom]
* [Note: I will aim to respond within 48 hours. Please reach out to your AI Studio Coach with urgent questions.]

> 💡 **Challenge Advisor: Please update the above based on your availability and preference. If you are not able to answer questions or meet with fellows outside of the biweekly Lab Section check-ins, simply write in "N/A (only available during the official check-in times)"**

**Recommended free coding / collaboration tools**
* […]
* […]

---

## 🚀 Getting Started

1. **Review this overview document** and note any questions for our first meeting
2. **Begin reviewing the dataset** using the link above
3. **Read the GitHub Projects documentation** [here](https://docs.github.com/en/issues/planning-and-tracking-with-projects/learning-about-projects/about-projects)

I’m excited to work with you!

---

## ❓ Questions?

Please bring any questions to our first meeting during the week of August 24th (Break Through Tech’s Bridge to Studio - Session C). 

## Data & Format

- **Q: Should we use the CUAD JSON files (question-answer format) as-is, or reshape them into per-chunk classification format, since the milestone doc calls for "chunk-based multi-label classification"?**
  - A: Reshape them. The JSON format is set up for a different task — finding answer spans — which isn't what we're building. You'll need to convert contracts into overlapping text chunks and label each one. It's a bit of upfront work in September but the right foundation for everything that follows.

- **Q: Is the pre-made train/test split okay to reuse, or should the team build its own after reshaping?**
  - A: Build your own. The existing split was designed for the original QA task and won't carry over cleanly. The main thing to get right is splitting by contract, not by chunk — if chunks from the same contract end up in both train and test, your evaluation numbers will look better than they actually are.

---

## Scoping the 41 Clause Categories

- **Q: Which ~10 clause categories matter most to Accenture's actual legal/procurement teams? Can you help rank them?**
  - A: From what I've seen in practice, the ones that come up most in reviews are: Limitation of Liability, Indemnification, Termination for Convenience, Governing Law, Auto-Renewal, IP Ownership Assignment, Change of Control, Non-Compete, Audit Rights, and Most Favored Nation. Liability and indemnification clauses are where the real exposure sits, so I'd prioritize getting those right before the others. That said, run your EDA first — if any of these have very few examples in the data, flag it and we can swap one out.

---

## Risk Scoring

- **Q: What specific signals define "risky"? (e.g., missing liability cap, one-sided termination, vague language) Do you have a real checklist from experience?**
  - A: The things that consistently raise flags in real reviews: a liability clause with no monetary cap, termination rights that only run one way, indemnification that's completely open-ended, auto-renewal with no notice window, and IP assignment language that's ambiguous about who owns what. Vague language on its own is harder to score consistently, so I'd keep the signals concrete for now and revisit once the core model is working.

- **Q: Can you hand-rank a small batch (20-30) of clauses as a reference the team can compare against?**
  - A: Yes, happy to do that. Put together a spreadsheet with 20–30 clause excerpts pulled from the test set and I'll go through and score them. A simple 1–5 scale works fine. Give me a couple weeks once you have the data prepped.

- **Q: What does Low/Medium/High mean in practice at Accenture — existing rubric, or do we define it from scratch?**
  - A: We don't have a formal rubric for this, so define it from scratch and I'll react to it. My rough instinct: Low is a standard clause with no red flags, Medium is something that warrants a closer look but isn't a dealbreaker, and High is either a missing clause that should be there or language that creates real financial or legal exposure. Run your proposed thresholds by me before you lock them in for November.

- **Q: Should a missing clause (one that should exist but doesn't) count as a risk signal on its own?**
  - A: Yes, absolutely. A contract that's silent on liability or IP ownership isn't neutral — it usually defaults to the worse position for whoever didn't catch it. Treat absence as at least a Medium for any of the high-priority categories.

- **Q: Should the risk signals be weighted equally, or do some matter more?**
  - A: Some matter more. I'd treat an uncapped liability or a completely missing indemnification clause as automatically High, regardless of what else looks fine. Equal weighting is a reasonable starting point to get the system running, but build it so weights can be adjusted — we'll want to tune that in November once we can see how the scores are landing.

---

## Modeling / Implementation

- **Q: Is Google Colab free tier sufficient, or should the team have Colab Pro / paid compute access?**
  - A: Free tier will probably cause headaches — sessions disconnect and training runs that take a few hours aren't realistic on it. Colab Pro is worth it at $10/month, or the team can use Kaggle Notebooks for free, which gives 30 GPU hours a week with more stable sessions. I'd sort this out before October when the actual fine-tuning starts.

- **Q: How should long contracts be chunked — paragraph-based, sentence-based, fixed token length, or team's discretion?**
  - A: Fixed token length with some overlap is the way to go — 512 tokens with roughly a 64-token overlap is standard and will work well here. Paragraph-based sounds intuitive but legal paragraphs are all over the place in length, so it gets messy fast. Stick with the fixed window approach and document what you chose so it's reproducible.
