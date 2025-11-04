---
layout: about
title: about
permalink: /
subtitle: Machine Learning Researcher | Convergence Analysis & Neuromorphic Computing

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
    
    body {
      overflow-x: hidden !important;
    }
    
    .container {
      max-width: 100vw !important;
      overflow-x: hidden !important;
    }
    
    h1, h2, h3 {
      word-wrap: break-word !important;
      overflow-wrap: break-word !important;
    }
    
    table {
      width: 100% !important;
      display: block !important;
      overflow-x: auto !important;
      -webkit-overflow-scrolling: touch !important;
    }
    
    img, svg {
      max-width: 100% !important;
      height: auto !important;
    }
    
    .typing-svg-container {
      max-width: 100% !important;
      overflow: hidden !important;
    }
  }
  
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

I hold an M.Sc. in Computer Science (GPA: 3.7/4.0) from **Shahid Beheshti University**, where my thesis established convergence guarantees for spike-timing-dependent plasticity (STDP) in recurrent spiking neural networks. Using Lyapunov stability analysis, I proved that STDP-based learning converges under specific conditions and validated these results on time-series benchmarks from the UCR archive. My research combines dynamical systems theory, stochastic optimization, and neuromorphic computing to understand the mathematical principles governing adaptation in biologically-inspired systems.

Building on this foundation, I have investigated in-context learning dynamics in transformer models and developed graph-theoretic methods for detecting risk in decentralized finance protocols.

> **Goal:** I seek a Ph.D. position to advance my work on statistical learning theory, adversarial robustness, and provably convergent algorithms. I aim to develop rigorous theoretical guarantees while demonstrating practical applicability through open-source implementations.

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

I implemented my M.Sc. thesis as an open-source Python library for analyzing convergence of STDP in recurrent spiking neural networks. The toolkit provides numerical methods for Lyapunov stability verification, energy landscape visualization, and systematic benchmarking across UCR time-series tasks. This work translated rigorous mathematical results into reproducible experiments, showing how dynamical systems theory guides more stable neuromorphic learning. The project achieved >95% accuracy in predicting convergence behavior and reduced analysis time from days to hours through automated verification. It includes comprehensive documentation, automated testing (85% coverage), and interactive Jupyter notebooks for exploring convergence under different architectures.

---

### 📊 Statistical Learning Theory Experiments
*Theoretical Investigation | Mar 2025 – Apr 2025*

I developed an educational framework visualizing PAC learnability, VC dimension, and Rademacher complexity. Using synthetic datasets and controlled experiments, I created interactive demonstrations showing how sample complexity scales with hypothesis class complexity and the bias-variance tradeoff across model families. The Streamlit dashboards make foundational ML theory accessible through hands-on exploration, with detailed mathematical derivations alongside experimental validations. Based on instructor feedback, this approach reduced student confusion on key concepts by approximately 40%.

---

### 📈 Real-Time Cryptocurrency Market Intelligence Dashboard
*Applied ML Engineering | Apr 2025 – May 2025*

I built a production system for real-time cryptocurrency market monitoring and forecasting. The architecture integrates WebSocket streams from five major exchanges with Redis for low-latency messaging, TimescaleDB for high-frequency data storage, and Prophet/LSTM models for price forecasting. I implemented the FastAPI backend with >80% test coverage, containerized the stack with Docker Compose, and deployed monitoring dashboards for order book analysis and anomaly detection. The system processes over 10,000 market events per second with sub-100ms latency and achieved 99.9% uptime in deployment.

---

### 🔐 DeFi Protocol Risk Monitoring API
*Applied Research | May 2025 – Jun 2025*

I designed a RESTful API for continuous risk assessment of DeFi lending protocols, focusing on collateralization ratios and liquidation cascades. Using Web3.py to query on-chain data from Aave and Compound, I implemented asynchronous task scheduling with Celery to compute risk metrics across blockchain networks. The system tracks over 1,000 lending positions representing $50M+ in collateral, calculating health factors and identifying concentration risks. In backtesting, it successfully identified 3 potential liquidation events representing over $2M at risk. The API follows production best practices with comprehensive error handling and 99.5% reliability.

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
