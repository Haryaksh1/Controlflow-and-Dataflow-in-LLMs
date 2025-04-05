# Controlflow-and-Dataflow-in-LLMs
## Objective: 
1.Preparation of datasets for testing control flow and data flow capabilities of LLMs
2.Evaluation of LLMs for their control flow and data flow capabilities 

## Methods: 
First we prepared datasets using wikihow data
wikihow dataset ( hereafter in pt1 referred to as original dataset): https://github.com/HiDhineshRaja/WikiHow-Dataset?tab=readme-ov-file  
Procedure to get ground truth dataset and control flow dataset from it original dataset: 
- Dropped column 3
- Sort a large CSV file based on the 'title' column using chunking for memory efficiency.
- Filter CSV rows to keep only those ending with numbers 1-8
- Filtered rows that were inconsistent in: grammar, meaning or structure explained in readme of repository. 
- Filter dataset to keep only tasks with more than 2 steps.
- Restructure WikiHow data to create columns for each step.(changed structure of earlier csv file to get the csv file that would be appropriate for out objective )
- Gives ground truth dataset (wikihowAll-5-dataset before jumbling.csv)
- Randomly shuffle the steps for each task while maintaining task names gives control flow dataset (control_flow_dataset.csv)

Code: Attached

Ground Truth Dataset: Attached

Benchmark Control Flow Dataset: Attached


The steps in these datasets were complex, and the lack of consistent notations made it challenging to simplify them. To improve the evaluation of LLMs, the focus was shifted to a specific category, and a cleaner dataset was sought that would provide simpler and clearer steps, be more consistent in length and support better testing.

Why this dataset was choosen:
- steps are simple enough
- no of entries: 9997
- license : MIT
- https://www.kaggle.com/datasets/mayankkurta/recipe-dataset ( hereafter in pt3 referred to as original dataset)

Procedure to get ground truth dataset, control flow dataset and data flow dataset from original dataset: 
- Columns ‘Name’ and ‘RecipeInstructions’ were chosen from original dataset
- Manually modify few cells 
- Clean and extract steps from the RecipeInstructions column
- Process each row to extract steps(ground truth: recipes_final.csv)
- Create a new dataframe with the same column names
- Keep the 'Name' column the same
- For each row, shuffle the step columns(control flow: controlflow_recipies.csv)
- Categorize each recipe
- For each step to replace, find a random step from a different category(data flow: dataflow_recipies.csv)




Code to get preferred ground truth dataset from it: attached
ground truth dataset from it: attached
benchmark control flow dataset : attached
benchmark data flow dataset : attached

Code for testing it using Gemma3 : Attached
Explanation: 
- Evaluates a language model's ability to understand procedural sequences in recipes
- Tests if the model can identify the correct order of steps when presented with multiple choices
- Creates a control flow evaluation framework for language models using recipe steps

- Extracts recipe steps from dataframe rows
- Filters out empty or NaN values
- Processes steps with a specified prefix (default "step-")
- Creates incorrect sequences as distractors
- Shuffles the correct steps randomly
- Ensures distractors differ from the correct sequence
- Formats distractors as semicolon-separated strings
- Creates multiple-choice prompts for evaluation
- Formats the correct sequence and distractors as options (Prompt Construction)
- Randomizes option order for unbiased testing
- query_llm: Interfaces with the language model
- Uses Ollama for model inference (Model Interaction)
- Handles errors and returns model's response
- Converts response to lowercase for consistent matching
- Evaluation System

Procedure:
- Loads recipe data from two CSV files:
- Ground truth file with correct sequences
- Jumbled file with alternative step orders
- Processes recipes and evaluates model performance
- Reports overall accuracy on control flow understanding

Can be extended to compare multiple language models

Due to computational limitations LLM evaluations will be updated later
