# Revisiting Rogers' Paradox on a Branching Knowledge Map

This repository contains the implementation and analysis code for our research project: **"Revisiting Rogers' Paradox on a Branching Knowledge Map: The Trade-Off Between Mastery Speed and Collective Innovation"**

## Authors
- Ghina Al Shdaifat (gha2009@nyu.edu)
- Maitri Patel (mp7075@nyu.edu)
- Jeevesh Attri (ja5593@nyu.edu)

**Institution**: New York University, Center for Data Science

## Abstract

Rogers's paradox demonstrates that cheap social learning offers no lasting fitness advantage over costly individual learning in dynamic environments. We extend this framework by introducing a multi-state "Knowledge Map" with two pathways: a low-risk branch (local optimum, V ≈ 0.92) and a high-risk branch (global optimum, V ≈ 0.95). Through agent-based simulations, we investigate how AI-assisted social learning affects the fundamental tension between exploitation (rapid mastery) and exploration (long-term innovation).

## Key Features

### Knowledge Map Architecture
- **Binary state → Multi-state transition**: Replaces simple adapted/not-adapted with a branching knowledge structure
- **Low-Risk Branch**: Fast gains, plateaus at local optimum (V ≈ 0.92)
- **High-Risk Branch**: Slower initial progress, reaches global optimum (V ≈ 0.95)
- **Exploratory Individual Learning**: Allows discovery of high-risk pathway

### AI Learning Strategies
We implement and compare three AI learning strategies:
1. **Modal AI**: Copies the most common population state
2. **Prestige AI**: Copies the highest-fitness agent
3. **Mean AI**: Averages population states

### Agent Learning Mechanisms
- **Individual Learning (IL)**: Costly (c_I = 0.05), risky (success rate z_i = 0.66), provides up-to-date knowledge
- **Social Learning from Humans (SL-H)**: Free, prestige-biased sampling
- **Social Learning from AI (SL-AI)**: Free, learns from AI's aggregated knowledge
- **Critical Social Learning (CSL)**: Attempts AI learning first, falls back to IL if unsuccessful

## Installation

### Prerequisites
- Python 3.8 or higher
- Jupyter Notebook or JupyterLab

### Setup

1. Clone the repository:
```bash
git clone https://github.com/[YOUR-USERNAME]/rogers-paradox-knowledge-map.git
cd rogers-paradox-knowledge-map
```

2. Create a virtual environment (recommended):
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

## Usage

### Running the Main Simulation

Open and run the Jupyter notebook:
```bash
jupyter notebook RogersParadox_KnowledgeMap.ipynb
```

The notebook is organized into the following sections:

#### Phase 1: Environment Setup
- Knowledge Map definition
- Agent state representation
- Fitness landscape implementation

#### Phase 2: Learning Mechanisms
- Individual Learning (IL) with exploration
- Social Learning (SL) with prestige bias
- AI learning strategies (Modal, Prestige, Mean)

#### Phase 3: Simulations and Analysis
- Baseline comparisons (No AI vs. different AI strategies)
- Critical Social Learning experiments
- Parameter sweeps (varying u and c_I)

### Key Parameters

| Parameter | Symbol | Default Value | Description |
|-----------|--------|---------------|-------------|
| Population size | N | 500 | Number of agents |
| Time steps | T | 20,000 | Simulation duration |
| IL cost | c_I | 0.05 | Cost of individual learning |
| IL success rate | z_i | 0.66 | Base success probability |
| Environmental volatility | u | 0.01 | Probability of world change |
| Exploratory IL probability | p_e | 0.02 | Chance to discover high-risk |
| Prestige bias | α | 2.0 | Strength of fitness-based sampling |
| Mutation rate | μ | 0.005 | Strategy inheritance mutation |

### Running Parameter Sweeps

The notebook includes parameter sweep experiments. Modify these sections to test different configurations:

```python
# Example: Varying environmental volatility
u_values = [0.005, 0.01, 0.05, 0.10]

# Example: Varying individual learning cost
c_I_values = [0.025, 0.05, 0.10, 0.20]
```

## Key Results

### Main Findings

1. **Modal AI accelerates convergence but doesn't stabilize**: Tc ≈ 9 vs. Tc ≈ 19 for No AI, but population oscillates between branches

2. **Prestige AI achieves stable global optimum**: Rapidly stabilizes at V ≈ 0.95 (Tc ≈ 5)

3. **Innovation suppression trade-off**: Prestige AI reduces long-run discovery rate (RD_high) by up to 80% compared to No AI

4. **Critical Social Learning reaches optimum**: CSL achieves global optimum (Tc = 4) while maintaining some exploration

5. **Context matters**: Relative benefits depend heavily on:
   - Exploration cost (c_I)
   - Environmental volatility (u)
   - AI update cadence

### Visualization Examples

The notebook generates several types of visualizations:
- Time-series plots of Mastery Score (Q_M)
- Discovery Rate (R_D) over time
- Population distribution across branches
- Parameter sweep heatmaps

## Metrics

We track three interdependent metrics:

1. **Mastery Score (Q_M)**: Average population fitness
   ```
   Q_M(t) = (1/N) × Σ V(K_j(t))
   ```

2. **Discovery Rate (R_D)**: Frequency of new node discoveries
   ```
   R_D(t) = (1/Δt) × Σ 1[K_j(t) ∉ D_{t-1}]
   ```

3. **Convergence Time (T_c)**: Time to reach competence threshold
   ```
   T_c = min{t | Q_M(t) ≥ 0.90}
   ```

## Reproducing Results

### Expected Runtime
- Single simulation (T=20,000): ~15-30 minutes on standard hardware
- Complete parameter sweeps: ~2-4 hours
- Full experimental suite: ~48 hours

### Hardware Requirements
- **Processor**: Intel Core i7 or equivalent
- **Memory**: 16GB RAM minimum
- **Storage**: ~1GB for code and results

### Step-by-Step Reproduction

1. **Baseline Comparisons** (Section: "Step 3: Running Simulations")
   - Run No AI condition
   - Run Modal AI condition
   - Run Prestige AI condition
   - Compare Q_M, R_D, and T_c

2. **Critical Social Learning** (Section: "Step 4: CSL Strategy")
   - Run Modal AI + CSL
   - Compare with baseline conditions

3. **Parameter Sweeps** (Section: "Step 5: Parameter Analysis")
   - Vary u (environmental volatility)
   - Vary c_I (individual learning cost)
   - Generate heatmap visualizations

## Extending the Code

### Adding New AI Strategies

To implement a new AI learning strategy, add a function in the notebook:

```python
def new_ai_strategy(population_states):
    """
    Custom AI learning strategy.
    
    Args:
        population_states: List of current agent states
        
    Returns:
        AI's learned state
    """
    # Your implementation here
    return ai_state
```

### Modifying the Knowledge Map

Edit the `knowledge_map` dictionary to test different fitness landscapes:

```python
knowledge_map = {
    0: {'fitness': 0.86, 'branch': 'start', 'next_node': 1},
    # Add more nodes here
}
```

### Custom Metrics

Add custom metric tracking in the simulation loop:

```python
# Example: Track strategy diversity
strategy_entropy = calculate_entropy(agent_strategies)
custom_metrics.append(strategy_entropy)
```

## Limitations

1. **No statistical testing**: Results are based on qualitative comparisons and visual inspection
2. **Single runs**: Each parameter combination is tested once (no replicates for variance estimation)
3. **Simplified fitness landscape**: Real-world knowledge structures are more complex
4. **Homogeneous agents**: All agents have identical learning parameters
5. **Single AI system**: Multiple competing AI systems not modeled

## Future Work

Potential extensions include:
- Statistical significance testing with multiple replicates
- Heterogeneous agent populations with varying learning abilities
- Dynamic knowledge maps that evolve over time
- Multiple AI systems with different training data
- Negative feedback mechanisms (deskilling effects)
- Temporal credit assignment with delayed feedback
- Empirical validation through online experiments

## Citation

If you use this code in your research, please cite:

```bibtex
@article{alshdaifat2024rogers,
  title={Revisiting Rogers' Paradox on a Branching Knowledge Map: The Trade-Off Between Mastery Speed and Collective Innovation},
  author={Al Shdaifat, Ghina and Patel, Maitri and Attri, Jeevesh},
  institution={New York University, Center for Data Science},
  year={2024}
}
```

## References

This work builds upon:

- **Collins, K. M., Bhatt, U., & Sucholutsky, I.** (2025). Revisiting Rogers' Paradox in the Context of Human-AI Interaction. *arXiv preprint arXiv:2501.10476*.

- **Rogers, A. R.** (1988). Does biology constrain culture? *American Anthropologist*, 90(4), 819-831.

- **Enquist, M., Eriksson, K., & Ghirlanda, S.** (2007). Critical social learning: A solution to Rogers's paradox of nonadaptive culture. *American Anthropologist*, 109(4), 727-734.

## Contact

For questions, issues, or contributions:
- Contact: gha2009@nyu.edu, mp7075@nyu.edu, ja5593@nyu.edu

## Acknowledgments

We thank our course instructor, Ilia Sucholutsky, for guidance on this project and the original authors of "Revisiting Rogers' Paradox in the Context of Human-AI Interaction" for making their simulation code open-source, which served as inspiration for our extended framework.

---
