---
layout: about
title: about
permalink: /
subtitle: AI and Machine Learning Researcher | Seeking Ph.D. Opportunities

profile:
  align: right
  image: prof_pic.jpg
  image_circular: false
  address: >
    <p>s.dastouri@alumni.sbu.ac.ir</p>
    <p><a href="https://www.researchgate.net/profile/Seyed-Dastouri">ResearchGate</a></p>
    <p>+98 913 4209486</p>
    <p>Iran</p>

news: false
selected_papers: false
social: false
---

<style>
  @media (max-width: 768px) {
    .profile img {
      max-width: 200px !important;
      width: 100% !important;
      height: auto !important;
    }
    
    /* Fix horizontal scroll on mobile */
    body {
      overflow-x: hidden !important;
    }
    
    .container {
      max-width: 100vw !important;
      overflow-x: hidden !important;
    }
    
    /* Responsive typography */
    h1, h2, h3 {
      word-wrap: break-word !important;
      overflow-wrap: break-word !important;
    }
    
    /* Responsive tables */
    table {
      width: 100% !important;
      display: block !important;
      overflow-x: auto !important;
      -webkit-overflow-scrolling: touch !important;
    }
    
    /* Responsive images and SVGs */
    img, svg {
      max-width: 100% !important;
      height: auto !important;
    }
    
    /* Fix typing SVG on mobile */
    .typing-svg-container {
      max-width: 100% !important;
      overflow: hidden !important;
    }
  }
  
  /* Skill tags styling */
  .skill-tag {
    display: inline-block;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    padding: 4px 12px;
    margin: 4px;
    border-radius: 20px;
    font-size: 0.9em;
    font-weight: 500;
  }
  
  .skill-category {
    margin-bottom: 1.5rem;
  }
  
  .skill-category h4 {
    color: #667eea;
    margin-bottom: 0.5rem;
  }
</style>

<div align="center" class="typing-svg-container">
  <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=500&size=18&pause=1000&color=2E8B57&center=true&vCenter=true&width=600&lines=AI+Researcher+%7C+Deep+Learning+Enthusiast;Exploring+Multimodal+Learning+%26+Visual+Recognition;Building+Intelligent+Systems+for+Tomorrow" alt="Typing SVG" />
</div>

---

## 👨‍🔬 Research Focus

I hold an M.Sc. in Computer Science (GPA: 3.7/4.0) from **Shahid Beheshti University**, where my thesis established rigorous convergence guarantees for **spike-timing-dependent plasticity (STDP)** in recurrent spiking neural networks through Lyapunov stability analysis. This work demonstrated that STDP-based learning converges under specific conditions in recurrent architectures. I validated these theoretical guarantees experimentally on time-series classification benchmarks from the UCR archive. My research combined **dynamical systems theory**, **stochastic optimization**, and **neuromorphic computing** to understand not merely what works empirically, but the fundamental mathematical principles governing adaptation in biologically-inspired neural systems.

Building on this foundation, I have investigated **in-context learning dynamics** in transformer-based models, examining how these architectures adapt to new tasks without explicit gradient updates. I have also developed **graph-theoretic methods** for detecting contagion risk and concentration vulnerabilities in decentralized finance lending protocols.

> **Goal:** I seek a Ph.D. position to deepen my work on **statistical learning theory**, **adversarial robustness**, and **provably convergent algorithms**. My goal is to develop rigorous theoretical guarantees for modern learning systems while demonstrating their practical applicability through open-source implementations and reproducible experiments.

<div align="center" style="margin: 2rem 0;">
  <a href="https://github.com/MehrdadDastouri" target="_blank" rel="noopener noreferrer">
    <img src="https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white" alt="GitHub"/>
  </a>
  <a href="https://www.researchgate.net/profile/Seyed-Dastouri?ev=hdr_xprf" target="_blank" rel="noopener noreferrer">
    <img src="https://img.shields.io/badge/ResearchGate-00CCBB?style=for-the-badge&logo=researchgate&logoColor=white" alt="ResearchGate"/>
  </a>
</div>

---

## 🎓 Education

### Shahid Beheshti University | Tehran, Iran
**Master of Science in Computer Science (Data Mining)**  
📅 Sep 2020 - Sep 2022  
📚 **Thesis:** Convergence Analysis of Spike-Timing-Dependent Plasticity Learning Rules in Recurrent Spiking Neural Networks with Applications to Time-Series Classification  
🎯 **GPA:** 3.7/4.0

### Isfahan University of Technology | Isfahan, Iran
**Bachelor of Science in Software Engineering**  
📅 Sep 2008 - Sep 2012  
🎯 **GPA:** 3.0/4.0

---

## 💼 Research & Professional Experience

### 🧠 SNN Convergence Analysis Toolkit
*Independent Research | Jan 2025 – Mar 2025*

I implemented the theoretical framework from my M.Sc. thesis as an **open-source Python library** for analyzing convergence properties of spike-timing-dependent plasticity (STDP) in recurrent spiking neural networks. The toolkit provides:
- Numerical methods for **Lyapunov stability verification**
- Energy landscape visualization
- Systematic benchmarking across time-series classification tasks from the UCR archive

Through this work, I translated rigorous mathematical results into **reproducible computational experiments**, demonstrating how dynamical systems theory can guide the design of more stable neuromorphic learning algorithms. The project includes comprehensive documentation, automated testing, and interactive Jupyter notebooks that allow researchers to explore convergence behavior under different architectural choices and hyperparameter configurations.

---

### 📊 Statistical Learning Theory Experiments
*Theoretical Investigation | Mar 2025 – Apr 2025*

I developed an educational framework for visualizing core concepts in **statistical learning theory**, including:
- PAC learnability
- VC dimension
- Rademacher complexity

Using synthetic datasets and controlled experiments, I implemented **interactive demonstrations** showing how sample complexity scales with hypothesis class complexity, empirical risk minimization behaviors, and the bias-variance tradeoff across different model families. This work bridges abstract theoretical guarantees with concrete computational experiments, making foundational machine learning theory more accessible through hands-on exploration. The project employs **Streamlit** for interactive dashboards and includes detailed mathematical derivations alongside experimental validations.

---

### 📈 Real-Time Cryptocurrency Market Intelligence Dashboard
*Applied ML Engineering | Apr 2025 – May 2025*

I built a **production-grade system** for real-time monitoring and forecasting of cryptocurrency market dynamics, integrating WebSocket streams from multiple exchanges with time-series prediction models. The architecture employs:
- **Redis** for low-latency message queuing
- **TimescaleDB** for efficient storage of high-frequency tick data
- **Prophet/LSTM models** for short-term price forecasting

I implemented the backend using **FastAPI** with comprehensive testing (>80% coverage), containerized the entire stack with **Docker Compose**, and deployed monitoring dashboards that visualize order book imbalances, volatility regimes, and anomaly detection alerts. This project demonstrates my ability to translate theoretical time-series analysis into scalable, production-ready systems.

---

### 🔐 DeFi Protocol Risk Monitoring API
*Applied Research | May 2025 – Jun 2025*

I designed a **RESTful API** for continuous risk assessment of decentralized finance lending protocols, focusing on:
- Collateralization ratios
- Liquidation cascades
- Systemic contagion risk

Using **Web3.py** to query on-chain data from protocols like Aave and Compound, I implemented asynchronous task scheduling with **Celery** to compute risk metrics across multiple blockchain networks. The system calculates health factors for individual positions, identifies concentration risks in collateral pools, and provides early warning signals for potential liquidation events. The API follows production best practices including comprehensive error handling, rate limiting, structured logging, and automated integration tests, showcasing my ability to build reliable infrastructure for financial applications.

---

## 🛠️ Core Skills

<div class="skill-category">
  <h4>💻 Programming Languages</h4>
  <span class="skill-tag">Python</span>
  <span class="skill-tag">Rust</span>
  <span class="skill-tag">MATLAB</span>
</div>

<div class="skill-category">
  <h4>🤖 AI/ML Frameworks</h4>
  <span class="skill-tag">PyTorch</span>
  <span class="skill-tag">TensorFlow</span>
  <span class="skill-tag">JAX</span>
  <span class="skill-tag">Scikit-learn</span>
  <span class="skill-tag">Pandas</span>
  <span class="skill-tag">NumPy</span>
  <span class="skill-tag">SciPy</span>
</div>

<div class="skill-category">
  <h4>🧠 SNN & Neuromorphic</h4>
  <span class="skill-tag">snnTorch</span>
  <span class="skill-tag">Brian2</span>
  <span class="skill-tag">NEST</span>
  <span class="skill-tag">Surrogate Gradient Methods</span>
</div>

<div class="skill-category">
  <h4>🌐 Backend & DevOps</h4>
  <span class="skill-tag">FastAPI</span>
  <span class="skill-tag">Flask</span>
  <span class="skill-tag">Docker</span>
  <span class="skill-tag">Redis</span>
  <span class="skill-tag">Celery</span>
  <span class="skill-tag">WebSocket</span>
</div>

<div class="skill-category">
  <h4>📊 Data Infrastructure</h4>
  <span class="skill-tag">TimescaleDB</span>
  <span class="skill-tag">PostgreSQL</span>
  <span class="skill-tag">Web3.py</span>
</div>

<div class="skill-category">
  <h4>🔍 Monitoring & Testing</h4>
  <span class="skill-tag">Pytest</span>
  <span class="skill-tag">GitHub Actions</span>
  <span class="skill-tag">Prometheus</span>
  <span class="skill-tag">Grafana</span>
</div>

<div class="skill-category">
  <h4>🎯 Specializations</h4>
  <span class="skill-tag">Convergence Analysis</span>
  <span class="skill-tag">Statistical Learning Theory</span>
  <span class="skill-tag">Spiking Neural Networks</span>
  <span class="skill-tag">Time Series Forecasting</span>
  <span class="skill-tag">DeFi Risk Modeling</span>
  <span class="skill-tag">Production ML Systems</span>
</div>

---

## 🌍 Languages

| Language | Proficiency |
|----------|-------------|
| **English** | Professional Working Proficiency |
| **Persian (فارسی)** | Native |

---

## 📈 Research Philosophy

> My approach combines rigorous experimentation with clear documentation and collaborative spirit. I believe in systematic evaluation, making research accessible and reproducible, and staying updated with the latest advances in the field.

### Core Principles:
- **🔍 Rigorous Experimentation:** Systematic evaluation and ablation studies
- **📖 Clear Documentation:** Making research accessible and reproducible  
- **🤝 Collaborative Spirit:** Learning from and contributing to the community
- **🌱 Continuous Learning:** Staying updated with latest advances

---

> *"In God we trust, all others must bring data."* — W. Edwards Deming
