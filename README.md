# Control Flow and Data Flow in Large Language Models (LLMs)
This repository contains research conducted during an internship at the AI Institute of South Carolina, focusing on evaluating LLMs' capabilities in handling control flow and data flow tasks. The work involved creating specialized datasets and developing evaluation frameworks to assess how well different language models can understand and process procedural information.

The research demonstrates that while LLMs have made impressive advances in many natural language tasks, their ability to follow procedural instructions correctly and track information flow between steps remains a challenging area that requires specialized evaluation frameworks and targeted datasets.

## Table of Contents
- [Project Overview](#project-overview)
- [Objectives](#objectives)
- [Methodology](#methodology)
  - [Dataset Preparation: WikiHow](#dataset-preparation-wikihow)
  - [Dataset Preparation: Recipes](#dataset-preparation-recipes)
  - [Evaluation Framework](#evaluation-framework)
- [Repository Structure](#repository-structure)
- [Installation and Usage](#installation-and-usage)
- [Results and Key Findings](#results-and-key-findings)
- [Contributions](#contributions)
- [Acknowledgments](#acknowledgments)

## Project Overview
Control flow and data flow understanding are two fundamental capabilities required for LLMs to successfully perform complex, multi-step tasks that involve procedural knowledge:

- **Control Flow**: The ability of a model to understand and follow a sequence of steps in the correct order (procedural knowledge).
- **Data Flow**: The capability to track how information passes between steps and how variables change throughout a process.

This research developed specialized datasets and evaluation frameworks to test these capabilities in various LLMs, with a particular focus on creating benchmarks that can help improve model performance on tasks requiring sequential reasoning.
## Objectives
1. Preparation of high-quality datasets for benchmarking control flow and data flow capabilities in LLMs
2. Evaluation of LLMs for their control flow and data flow understanding
3. Development of evaluation methodologies to assess how well LLMs can:
   - Follow sequential instructions in the correct order
   - Track information transfer between steps and maintain variable state
4. Implementation of testing frameworks to quantitatively measure LLM performance

## Methodology
### Dataset Preparation: WikiHow
The first phase involved creating a control flow dataset from WikiHow instructions:

1. Started with the [WikiHow Dataset](https://github.com/HiDhineshRaja/WikiHow-Dataset)
2. Applied preprocessing steps
3. Created two datasets:
- Ground truth dataset: "wikihowAll-5-dataset before jumbling.csv"
- Control flow benchmark: "control_flow_dataset.csv" (with randomly shuffled steps)

The WikiHow dataset presented challenges due to complex steps and inconsistent notations, which motivated the creation of a second dataset with cleaner structure.

### Dataset Preparation: Recipes
To address limitations in the WikiHow dataset, a recipe dataset was adopted:

1. Selected from Kaggle: [Recipe Dataset](https://www.kaggle.com/datasets/mayankkurta/recipe-dataset) 
2. Key advantages:
- Simple, clear procedural steps
- 9,997 entries
- MIT license
- Consistent formatting
3. Preprocessing workflow
4. Created three datasets:
- Ground truth: "recipes_final.csv"
- Control flow benchmark: "controlflow_recipies.csv" (shuffled steps)
- Data flow benchmark: "dataflow_recipies.csv" (steps replaced with ones from different categories)

### Evaluation Framework
The evaluation approach tests LLMs' ability to identify correct procedural sequences:

1. Multiple-choice prompts present models with the correct sequence and distractor options
2. Implementation using Ollama framework for model inference
3. Key functions:
4. def load_steps_from_row(row, prefix="step-"):
- """Extracts non-empty steps from row"""
steps = []
for col in sorted(row.index):
if col.startswith(prefix):
cell = str(row[col]).strip()
# Skip if empty or just a placeholder (like NaN)
if cell and cell.lower() != "nan":
steps.append(cell)
return steps

- def generate_distractor(correct_steps, num_distractors=3):
"""Generates list of distractor sequences by shuffling the correct sequence"""
distractors = []
for _ in range(num_distractors):
shuffled = correct_steps.copy()
# Reshuffle until it is not the same as the correct order
while True:
random.shuffle(shuffled)
if shuffled != correct_steps:
break
distractors.append("; ".join(shuffled))
return distractors
4. Evaluation metrics:
- Accuracy: percentage of correct sequence identifications
- Error analysis: patterns in model mistakes

This framework provides a standardized approach for comparing different LLM architectures on their procedural reasoning capabilities.

## Repository Structure
├── Evaluation Code <br>
│ ├── controlflow_dataflow_Gemma3.ipynb # Evaluation code for Gemma3<br>
│ └── readme.txt # Documentation for evaluation code<br>
│<br>
├── Recipes Dataset<br>
│ ├── code.ipynb # Data processing code<br>
│ ├── controlflow_recipies.csv # Control flow benchmark<br>
│ ├── dataflow_recipies.csv # Data flow benchmark<br>
│ ├── recipes_final.csv # Ground truth dataset<br>
│ └── readme.txt # Dataset documentation<br>
│<br>
├── wikiHow Dataset<br>
│ ├── code.ipynb # Data processing code<br>
│ ├── control_flow_dataset.csv # Control flow benchmark<br>
│ ├── wikihowAll-5-dataset before ju... # Ground truth dataset<br>
│ └── readme.txt # Dataset documentation<br>
│<br>
├── LICENSE # MIT License<br>
└── README.md # Project documentation<br>


## Installation and Usage
### Prerequisites
- Python 3.8+
- pandas
- re (regular expressions)
- Ollama (for model inference)

### Setup
- Clone the repository<br>
git clone https://github.com/Haryaksh1/Controlflow-and-Dataflow-in-LLMs<br>
cd Controlflow-and-Dataflow-in-LLMs<br>

- Install required packages<br>
pip install pandas<br>

- Install Ollama following instructions at https://ollama.ai/ <br>


## Results and Key Findings
The research provides several insights into LLMs' procedural reasoning capabilities:

1. **Control Flow Understanding**:
   - Models struggle more with longer procedural sequences
   - Performance varies significantly between model architectures
   - Specific procedural patterns cause consistent difficulties

2. **Data Flow Challenges**:
   - Tracking variable state changes remains difficult for most models
   - Models often fail to maintain consistency when information must be carried through multiple steps

3. **Future Directions**:
   - Developing specialized pre-training tasks for procedural reasoning
   - Creating more diverse benchmarks across domains
   - Exploring hybrid approaches that combine symbolic reasoning with neural language models

## Contributions
As highlighted in the recommendation letter from Prof. Amit Sheth:

1. **Creation and Curation of Control Flow and Data Flow Datasets**
   - Independently sourced and curated high-quality datasets
   - Developed structured datasets from recipe repositories with clear step dependencies
   - Formatted datasets for compatibility with LLM analysis tools

2. **Development of Analysis Code for LLM Workflows**
   - Implemented Python code using the Ollama framework
   - Generated step dependency graphs and tracked variable states
   - Provided statistical analysis of control and data flow consistency

3. **Collaborative Problem Solving and Initiative**
   - Proactively identified and addressed dataset quality issues
   - Maintained consistent communication with the research team
   - Demonstrated adaptability by responding to evolving project requirements

4. **Engagement with Research Community**
   - Regularly attended AI Institute meetings from September 2024 onward
   - Maintained detailed documentation and organized GitHub repository

## Acknowledgments
- **Prof. Amit Sheth** - Supervisor, AI Institute of South Carolina
- **Vishal Pallaghani** - PhD student mentor
- **AI Institute of South Carolina** - For providing research infrastructure and support

This research contributes to the growing body of work on evaluating and improving procedural reasoning in large language models, addressing fundamental capabilities needed for real-world applications.



