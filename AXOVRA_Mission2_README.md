# AXOVRA Mission 2: Flagship AI/Data Case Study Upgrade

**Student:** Parshvi Jain  
**Track:** Flagship AI/Data Proof Conversion  
**Flagship Proof:** XAI Forensics  
**Target Role:** AI Intern / ML Intern / Data Science Intern / Applied AI Engineer  

**Live Tool:** [xai-forensic.vercel.app](https://xai-forensic.vercel.app)  
**Source Code:** [github.com/parshvi1508/XAI_Forensic](https://github.com/parshvi1508/XAI_Forensic)  
**Backend API Docs:** [jainparshvi-xai-forensics-backend.hf.space/docs](https://jainparshvi-xai-forensics-backend.hf.space/docs)


## A. Proof Title

**XAI Forensics: Sentiment Model Failure Inspection Tool**


## B. Short Summary

XAI Forensics is a deployed AI tool that helps ML engineers inspect sentiment model decisions before trusting them in production. It combines LIME attribution, counterfactual word removal, and dual-model disagreement analysis to expose hidden failure modes such as negation errors, sarcasm confusion, fragile token dependence, and domain mismatch.

Mission 2 upgraded this proof from a working technical demo into a recruiter-readable case study with a clear problem, named user, workflow, evidence links, technical decisions, limitations, resume bullet, LinkedIn draft, and Proof Vault-ready packaging.

## C. Main Output Link

**Live deployed proof:**  
https://xai-forensic.vercel.app

## D. Evidence Links

1. **Live frontend:** https://xai-forensic.vercel.app  
2. **GitHub repository:** https://github.com/parshvi1508/XAI_Forensic  
3. **Backend API docs:** https://jainparshvi-xai-forensics-backend.hf.space/docs  
4. **Demo video:** https://drive.google.com/file/d/1lEXwtQ5qg7sJCF9Ytm_dGJDJ0hVGeCAS/view?usp=sharing
5. **Screenshots:** https://drive.google.com/drive/folders/11JUx4fUnQ1k7CbEm3P8uiRbt7b71yEUX?usp=sharing


# Flagship Case Study

## 1. What Changed Since Mission 1

Mission 1 identified XAI Forensics as my strongest AI/Data proof and diagnosed its main gap: the tool worked, but the use case and named user were not immediately clear to a recruiter.

Mission 2 closes that gap in two ways.

First, the project is now framed around a clear decision: **stress-test a model decision before trusting it**. The tool's WHY, FLIP, and DISAGREE sections now make it easier for a first-time visitor to understand what each method reveals.

Second, this document packages the project as a complete case study: problem, user, workflow, technical approach, evidence, results, limitations, and role relevance.


## 2. Problem

Sentiment classifiers can fail silently on real-world language. A model may score well on a benchmark such as SST-2 but still misread ambiguous sentences like:

> "I am not entirely unhappy with this result."

This happens because real-world text often contains double negation, sarcasm, backhanded compliments, informal phrasing, and domain-shifted language. Standard held-out accuracy does not clearly expose these blind spots before deployment.

The real problem is not only whether a model is wrong. The bigger problem is that an engineer may not know **why** the model made a specific decision, whether the decision is fragile, or whether the failure is caused by a mismatch between training data and real user language.

## 3. Named User and Use Case

**Named user:**  
An ML engineer or data scientist preparing to deploy a sentiment classifier into a real product.

**Product contexts:**

- Support ticket triage
- Review moderation
- Social listening
- Customer feedback analytics

**Decision the tool supports:**  
For a given ambiguous input, should this class of text be routed to human review, or does the failure point toward a retraining or data-domain gap?

**Why it matters:**  
In support ticket triage, a misread negative message may cause an angry customer to be deprioritized. In review moderation, sarcasm may be incorrectly classified as positive. In social listening, domain mismatch can distort product sentiment reports. These are production failures that a single benchmark accuracy number may hide.


## 4. Technical Approach

XAI Forensics runs three inspection methods on an input text and presents the signals side by side.

### WHY: Attribution

The WHY module uses LIME to perturb the input and estimate which tokens pushed the model toward its prediction.

This helps answer:

> Which words influenced the model's decision most?

LIME was chosen because it gives an interpretable token-level explanation that fits the project's interactive model-inspection goal.


### FLIP: Counterfactual Fragility

The FLIP module removes the highest-impact token and reruns inference.

If removing one word changes the prediction, the decision is fragile. This helps expose cases where the classifier depends too strongly on one token instead of understanding the full sentence.

This helps answer:

> Can one word flip the verdict?


### DISAGREE: Dual-Model Domain Check

The DISAGREE module compares two sentiment models:

- DistilBERT-SST2
- Twitter-RoBERTa

These models come from different training domains. If they disagree, the input may be ambiguous or affected by training-domain mismatch.

This helps answer:

> Is this failure coming from real ambiguity or from one model's training domain?


## 5. Key Technical Decisions

**LIME over SHAP:**  
SHAP can be more expensive and slower for transformer-based models. LIME was selected because it is practical for an interactive tool running under free-tier infrastructure constraints.

**Attention weights rejected as explanations:**  
Attention weights can look convincing but are not always reliable as explanations. The tool avoids presenting attention as the main explanation method.

**Two deliberately different models:**  
Using models trained on different domains makes disagreement meaningful. A split verdict can reveal that the input does not fit one model's learned language distribution.

**Decision-support, not auto-remediation:**  
The tool does not automatically fix or retrain the model. It surfaces evidence so the engineer can decide whether the case needs human review, retraining, or further testing.


## 6. Workflow

1. The engineer enters an ambiguous or adversarial sentence, or selects a preloaded example.
2. WHY shows which tokens influenced the model's decision.
3. FLIP removes the highest-impact token and checks whether the label changes.
4. DISAGREE compares outputs from two sentiment models trained on different domains.
5. The engineer reads all three signals together.
6. A fragile verdict plus model disagreement suggests that similar text should be reviewed manually or added to an adversarial evaluation set.
7. Stable attribution plus model agreement suggests that the prediction is more trustworthy.


## 7. Output and Result

The tool outputs:

- Sentiment prediction
- Confidence score
- Token-level attribution
- Counterfactual word-removal result
- Dual-model disagreement result
- Interpretation of whether the decision is stable or risky

The result is a working, publicly deployed model-inspection tool rather than a notebook or static report. A reviewer can open the live link, run their own input, inspect the output, check the source code, and verify the backend documentation.

Mission 2 improved the proof by making the project understandable as a real applied AI case study, not only a deployed demo.


## 8. Limitations

Current limitations:

- LIME attribution is approximate, not exact causal proof.
- Greedy word removal can sometimes create unnatural text.
- Input length is capped.
- Hugging Face free-tier backend may have cold-start delays.
- The tool is sentiment-specific.
- The tool has been tested only on English text.
- There is no aggregate evaluation yet across a large adversarial benchmark.

The sharpest missing piece is quantitative self-evaluation. Right now, the tool demonstrates failure cases one by one. The next improvement is to run it on a small adversarial benchmark of negation, sarcasm, and domain-shift examples, then publish flip rates and disagreement rates by category.


## E. Skills Proven

- Applied machine learning evaluation
- Explainable AI implementation
- LIME-based attribution
- Counterfactual testing
- Model disagreement analysis
- Transformer sentiment model inspection
- FastAPI backend deployment
- Next.js frontend deployment
- Technical documentation
- Evidence-based project packaging
- Recruiter-readable AI communication


## F. Role Relevance

This project is directly relevant to AI/ML internship and applied AI engineering roles because it shows more than model usage. It shows that I can inspect model behavior, identify failure modes, explain technical tradeoffs, and deploy a usable AI tool.

For early-stage startups, this matters because small teams need engineers who can build practical AI systems under real constraints. XAI Forensics demonstrates applied ML thinking, full-stack deployment, explainability awareness, and the ability to communicate technical work clearly to recruiters, mentors, and hiring managers.


## G. Resume Bullet

Built and deployed **XAI Forensics**, a model-inspection tool for pre-deployment auditing of transformer sentiment classifiers; combined LIME token attribution, counterfactual verdict-fragility testing, and dual-model disagreement analysis behind a public FastAPI backend and Next.js frontend.

## H. LinkedIn Proof Post Draft

I completed AXOVRA Mission 2 by upgrading my strongest AI/Data proof into a recruiter-readable flagship case study.

The project is **XAI Forensics**, a deployed tool that helps inspect sentiment model decisions before trusting them in production.

Instead of only asking whether a model predicts positive or negative sentiment, the tool asks:

Why did the model make this prediction?  
Can one word flip the verdict?  
Do two models trained on different domains disagree?

The tool uses LIME attribution, counterfactual word removal, and dual-model disagreement analysis to expose hidden failure modes such as negation errors, sarcasm confusion, fragile token dependence, and domain mismatch.

The biggest learning: a strong AI project is not only about building or deploying the model. It becomes real proof when the problem, user, workflow, evidence, limitations, and technical decisions are clear enough for someone else to trust.


## I. Reflection

In Mission 1, I identified XAI Forensics as my strongest AI/Data proof because it was deployed, open-source, and connected to a real model evaluation problem. But the use case was not immediately visible. A recruiter could open the project and see that it worked, but they might not immediately understand who it was for or what decision it supported.

Mission 2 changed that. The project is now framed around a specific user: an ML engineer or data scientist preparing to deploy a sentiment classifier. It is also framed around a specific decision: whether an ambiguous class of text should be trusted, routed to human review, or used as evidence for retraining.

The most important technical decision was combining three signals instead of relying on one explanation method. Attribution shows which words mattered. Counterfactual removal checks fragility. Dual-model disagreement checks domain mismatch. Together, these signals make the tool more useful than a simple sentiment prediction demo.

The main limitation is that the tool does not yet include aggregate evaluation across a labeled adversarial dataset. The next improvement would be to run the tool over examples of negation, sarcasm, and domain-shifted text, then report flip rates and disagreement rates by failure type.

In an interview, I would explain this project in one line: sentiment models fail silently on ambiguous language, so I built a deployed tool that lets engineers stress-test individual model decisions using attribution, counterfactuals, and cross-domain disagreement before trusting them in production.

# Final Proof Vault Entry

**Proof Name:**  
XAI Forensics: Sentiment Model Failure Inspection Tool

**Proof Type:**  
AI / Applied ML / Explainable AI / Technical Case Study

**Target Role:**  
AI Intern / ML Intern / Data Science Intern / Applied AI Engineer

**Short Summary:**  
Deployed an explainability-based sentiment model inspection tool that helps ML engineers detect hidden failure modes such as negation errors, sarcasm confusion, fragile token dependence, and domain mismatch using LIME attribution, counterfactual testing, and dual-model disagreement analysis.

**What This Proves:**  
Applied ML execution, explainable AI implementation, model evaluation thinking, full-stack deployment, technical documentation, result interpretation, use-case framing, and recruiter-ready proof packaging.

**Evidence Links:**  
Live Tool: https://xai-forensic.vercel.app  
GitHub: https://github.com/parshvi1508/XAI_Forensic  
Backend API Docs: https://jainparshvi-xai-forensics-backend.hf.space/docs  
Demo video: https://drive.google.com/file/d/1lEXwtQ5qg7sJCF9Ytm_dGJDJ0hVGeCAS/view?usp=sharing
Screenshots:https://drive.google.com/drive/folders/11JUx4fUnQ1k7CbEm3P8uiRbt7b71yEUX?usp=sharing


**Resume Bullet:**  
Built and deployed XAI Forensics, a model-inspection tool for pre-deployment auditing of transformer sentiment classifiers; combined LIME token attribution, counterfactual verdict-fragility testing, and dual-model disagreement analysis behind a public FastAPI backend and Next.js frontend.

**AXOVRA Standard Statement:**  
I created a recruiter-readable flagship AI/Data case study for an AI/Data recruiter, hiring manager, or research mentor evaluating whether a student can connect technical work to real-world use cases and explain it clearly. It proves my ability in applied AI/Data execution, use-case framing, technical documentation, result explanation, evidence packaging, and technical communication, and I can now use it in my Proof Vault, resume, LinkedIn, portfolio, and interviews.
