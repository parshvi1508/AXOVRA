# AXOVRA Mission 1 ; AI/Data Proof Audit + Flagship Use-Case Blueprint

**Student:** Parshvi Jain  
**Track:** Flagship AI/Data Proof Conversion  
**Target Role:** Applied AI / ML Engineer (early-stage startups)  
**Mission:** Audit existing AI/Data/GitHub/research work, identify which proof has the strongest real-world use case, create a flagship proof blueprint.

---

## The Problem This Mission Solves

I have work scattered across GitHub, a deployed app, an IEEE paper, production backend internships, and ACM-W community leadership. A recruiter opening my profile has no clear answer to one question: which project proves I can solve a real AI problem and explain its use case?

This mission answers that question by auditing what actually exists versus what is only planned, scoring each asset on use-case clarity, and producing one blueprint that makes the strongest asset application-ready.

---

## Proof Audit ; What I Actually Have

| Asset | Problem Clarity | Named User | Workflow Evidence | Artifact Exists | Verdict |
|---|---|---|---|---|---|
| XAI Forensics | Medium, implicit | No, unstated | Strong, live + API docs | Yes, deployed | Flagship |
| ClaimRoute (RAG) | Strong on paper | Strong (RAG engineers) | None, spec only | No | Kill for now |
| IEEE Energy Forecasting | Strong, quantified | Grid operators | Strong, published | Yes, paper | Secondary |
| Trurism / MedEvidences backend | Real production problem | Real employers | Strong, shipped | Yes, NDA | Off-track for AI/Data lane |

**Key finding:** XAI Forensics is the only AI/Data asset that is both deployed and has a real-world decision problem attached to it. Everything else is either a plan, a notebook, or off-lane for applied ML roles.

**Correction to R001 data entry in AXOVRA ProofOps notebook:** The initial intake recorded `proof_artifact_exists: False` and gap type `Scope Overreach` for my profile. Both are inaccurate as of this submission. The artifact is live at [xai-forensic.vercel.app](https://xai-forensic.vercel.app). The actual gap is a framing gap ; the use case and named user were never stated explicitly, not a missing artifact. This is a fixable gap, not a structural one.

---

## Flagship Proof Blueprint ; XAI Forensics

**Live tool:** [xai-forensic.vercel.app](https://xai-forensic.vercel.app)  
**Source code:** [github.com/parshvi1508/XAI_Forensic](https://github.com/parshvi1508/XAI_Forensic)  
**Backend API docs:** [jainparshvi-xai-forensics-backend.hf.space/docs](https://jainparshvi-xai-forensics-backend.hf.space/docs)

### Problem

Sentiment classifiers fail silently on negation, sarcasm, and domain-mismatched text. Standard accuracy metrics on a held-out test set do not surface these blind spots before deployment. A model that scores 92% on SST-2 can still confidently misread "I am not entirely unhappy with this result" because double negation is underrepresented in formal movie-review training data. Teams ship models without knowing where these failures cluster.

### Named User

An ML engineer or data scientist about to deploy a sentiment classifier into a real product, specifically support ticket triage, review moderation, or social listening pipelines, who needs to know the model's systematic blind spots before users hit them in production.

### Workflow

1. Enter ambiguous or adversarial text ; negation, sarcasm, backhanded compliments, domain-shifted language.
2. **WHY (Attribution)** runs LIME with ~300 perturbed inference calls to identify which tokens pushed the model toward its verdict and by how much.
3. **FLIP (Counterfactual)** removes the single highest-impact token and reruns inference to test whether the prediction label changes. A label flip means the verdict was fragile.
4. **DISAGREE (Dual-model)** runs the same input through DistilBERT-SST2 (trained on formal movie reviews) and Twitter-RoBERTa (trained on 124 million tweets). A split verdict signals that the ambiguity is real and rooted in training domain mismatch, not just model confidence variation.
5. The engineer interprets all three signals together to make a manual call: is this a genuine ambiguity that needs human review in production, or a fixable domain gap that points toward retraining on a different corpus?

The tool is decision-support. It does not auto-remediate. The engineer decides what to do next.

### Evidence

The proof is not a notebook or a screenshot. The frontend is deployed on Vercel, the backend runs on Hugging Face Spaces with public API documentation, and the source is open on GitHub. A recruiter can open the link right now and run inference on their own input.

Methodology tradeoffs are documented inside the tool itself. LIME was chosen over SHAP because SHAP is slower on transformers and expensive on free-tier CPU. Attention weights were explicitly rejected as unreliable explanations, citing Jain and Wallace (2019). These are not afterthoughts ; they are design decisions that show production-awareness, not just tutorial-level implementation.

### What This Proves for Applied AI Roles

- Explainability engineering in practice, not just theory ; LIME implemented end-to-end, not called from a library without understanding
- Model evaluation beyond accuracy ; knowing that a 92% SST-2 score says nothing about sarcasm behavior
- Engineering tradeoffs under real constraints ; CPU-only inference, free-tier backend, deliberate rejection of a more expensive method
- Full-stack delivery ; frontend, backend, API documentation, and a live URL, not just a research script in a notebook
- Production failure-mode thinking ; the three adversarial examples pre-loaded in the UI are not random; they are chosen to expose the three failure modes that most often go undetected in deployed sentiment systems

### Honest Limitations

Input is capped at 1000 characters. The backend has a 30 to 60 second cold start after inactivity on the Hugging Face free tier. The tool is sentiment-specific and has only been tested on English text. LIME attribution is an approximation, not an exact causal explanation. Greedy word removal can produce ungrammatical text after deletion.

Stating these limitations here, not hiding them, is intentional. An engineer who knows their tool's edges is more trustworthy than one who doesn't.

---

## Reflection

**Which existing proof asset is strongest?**  
XAI Forensics. It is the only asset that is deployed, solves a named problem for a named user, and can be opened by a recruiter right now without any explanation from me.

**Why were other projects weak in use case?**  
ClaimRoute is the strongest idea I have but it has no working system, just a specification. A spec is not proof. The IEEE paper is strong evidence but it is not interactive and a recruiter cannot run it. The backend internship work is real production experience but it sits behind NDAs and is backend engineering, not AI/ML, which is the lane I am targeting.

**What does the flagship proof need before it becomes recruiter-readable?**  
Two things. First, the use case and named user need to be stated on the landing page itself, not buried in the methodology section. A recruiter who spends 30 seconds on the site should immediately understand who this tool is for and what decision it helps them make. Second, the DISAGREE output needs a brief interpretive note that tells the user what to do when two models disagree, not just that they disagree.

**What will I upgrade in Mission 2?**  
Mission 2 will upgrade XAI Forensics on both fronts. Add explicit use-case framing to the landing page header. Add a brief recommended action when DISAGREE fires, so the output moves from "here is a divergence" to "here is what this divergence likely means and what you should check next." These are not cosmetic changes, they are the difference between a demo and a decision-support tool.

---

## AXOVRA Standard Statement

I created an AI/Data proof audit and flagship use-case blueprint for an AI/Data recruiter, research mentor, or hiring manager evaluating whether a student can connect technical work to real-world use cases. It proves my ability to evaluate AI proof assets, frame use cases with a named problem and named user, organize evidence, align proof to target role, and communicate technical tradeoffs clearly. I can now use it in my Proof Vault, resume, LinkedIn, and interviews.

Not learning only. Proof.
