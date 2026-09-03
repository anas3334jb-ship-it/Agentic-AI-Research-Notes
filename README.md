# Agentic AI & Systems Research Notes

Welcome! This repository tracks my learning log as I explore how AI agents work in practice, where they break down, and how we can use system-level guardrails to keep them on track.

---

### 📖 The Core Problem: Why Autonomous AI Agents Go Off Track

Working with AI agents is very different from chatting with a standard LLM. When you give an agent a multi-step task and let it run unattended, it frequently drifts off course. Because LLMs lack real-world common sense and context continuity, they tend to fail in two main ways:

* **Goal Drift & Context Loss:** If an agent encounters an unexpected pop-up, a broken link, or an edge-case error while navigating a site, it often forgets its original objective. Instead of recovering, it begins executing completely irrelevant actions—filling out wrong forms or navigating to unrelated pages—without realizing it has strayed.
* **The Infinite Loop Trap:** This is one of the most common failure modes. If a web page doesn't load or an action yields an unexpected result, the agent doesn't stop to re-evaluate. It falls into a repetitive cycle, executing the exact same step (e.g., repeatedly clicking a disabled button) forever. Without an external script monitoring its activity, the agent will consume high CPU resources and burn API credits endlessly.

---

### 📊 The Hard Numbers: Lessons from the WebArena Benchmark

This issue isn't just an anecdotal observation—it is backed by research data from benchmark papers like **WebArena**:

* **Human Success Rate:** **~78.24%** on complex, end-to-end web navigation tasks.
* **AI Agent Success Rate:** **~14.41%** on the exact same benchmark tasks.
* **The Key Takeaway:** Current state-of-the-art models fail over 85% of the time on complex, multi-step web workflows. The primary culprit isn't a lack of intelligence; it is the absence of robust error detection, step verification, and loop-breaking mechanisms.

---

### 💻 My Practical Research & Hardware Focus

Instead of trying to train massive models, my focus is on building practical, deterministic guardrails that sit around the agent to monitor its behavior:

* **Loop Prevention & Timeout Logic:** Writing lightweight C++ and Python wrapper scripts that track action history. If the system detects duplicate actions or zero-progress steps, it forcefully interrupts the agent and triggers a reset.
* **Local Execution Constraints:** Testing small, open-weights models (e.g., Llama 3B, Phi-3) locally on a **Dell Latitude 5420 (Intel 11th Gen Processor)**. 
* **Thermal & Resource Monitoring:** Keeping track of CPU load spikes and thermal limits using monitoring tools to ensure local AI agents run efficiently without frying local system hardware.
* **Goal:** Building privacy-first, low-resource agent frameworks that remain reliable even when the core AI model makes mistakes.
