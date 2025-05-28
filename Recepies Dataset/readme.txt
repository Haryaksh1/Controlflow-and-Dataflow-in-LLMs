Why this dataset was choosen:
- steps are simple enough
- no of entries: 9997
- license : MIT
- https://www.kaggle.com/datasets/mayankkurta/recipe-dataset ( hereafter in pt3 referred to as original dataset)

Procedure to get ground truth dataset, control flow dataset and data flow dataset from original dataset: 
- Columns ‘Name’ and ‘RecipeInstructions’ were chosen from original dataset
- Manually modify few cells 
- Clean and extract steps from the RecipeInstructions column
- Process each row to extract steps(ground truth: recipes_correct_steps.csv)
- Create a new dataframe with the same column names
- Keep the 'Name' column the same
- For each row, shuffle the step columns(control flow: controlflow_recipies.csv)
- Categorize each recipe
- For each step to replace, find a random step from a different category(data flow: dataflow_recipies.csv)




Code to get preferred ground truth dataset from it: attached
ground truth dataset from it: attached
benchmark control flow dataset : attached
benchmark data flow dataset : attached
