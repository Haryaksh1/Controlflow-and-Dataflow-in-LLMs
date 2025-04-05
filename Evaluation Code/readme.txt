Objective:
- Evaluates a language model's ability to understand procedural sequences in recipes
- Tests if the model can identify the correct order of steps when presented with multiple choices
- Creates a control flow evaluation framework for language models using recipe steps

Functions:
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