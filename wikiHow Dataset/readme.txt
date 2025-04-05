First we prepared datasets using wikihow data
wikihow dataset ( hereafter referred to as original dataset): https://github.com/HiDhineshRaja/WikiHow-Dataset?tab=readme-ov-file  
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
