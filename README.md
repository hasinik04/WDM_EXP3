### EX3 Implementation of GSP Algorithm In Python
### DATE: 06-02-2026
### AIM: To implement GSP Algorithm In Python.
### Description:
The Generalized Sequential Pattern (GSP) algorithm is a data mining technique used for discovering frequent patterns within a sequence database. It operates by identifying sequences that frequently occur together. GSP works by employing a depth-first search strategy to explore and extract frequent patterns efficiently.
### Steps:
1. <strong>Database Scanning:</strong> GSP scans the sequence database to determine the support of each item in the dataset.
2. <strong>Candidate Generation:</strong> It generates a set of candidate sequences using frequent items found in the previous step.
3. <strong>Pattern Growth:</strong> It extends the candidate sequences by merging them to form longer patterns, checking their support against a user-defined minimum support threshold.
4. <strong>Repeat:</strong> The process continues until no new sequences meet the minimum support threshold.
<p align="justify">
GSP finds application in various domains such as market basket analysis, web usage mining, bioinformatics, and more. For instance, in retail, GSP can identify common purchasing patterns, helping businesses understand customer behavior for targeted marketing or inventory management.
</p>

### Procedure:
<p align="justify">
1. From collections import defaultdict, from itertools import combinations: Imports necessary libraries/modules. defaultdict is
used to create a dictionary with default values and combinations generates all possible combinations of a sequence.</p>
<p align="justify">
2. generate_candidates(dataset, k): Function to generate candidate k-item sequences from a dataset. It loops through each sequence in the
dataset and finds combinations of length k for each sequence, updating their counts in a dictionary.</p>
<p align="justify">
3. gsp(dataset, min_support): Function that implements the Generalized Sequential Pattern (GSP) algorithm. It iterates through increasing
sequence lengths (k) until no new frequent patterns are found. It calls generate_candidates() to find patterns of varying lengths.</p>
<p align="justify">
4. Example dataset for each category: Defines example sequences for top wear, bottom wear, and party wear categories.</p>
<p align="justify">
5. Minimum support threshold: Sets the minimum support count required for a pattern to be considered frequent.</p>
<p align="justify">
6. Perform GSP algorithm for each category: Applies the GSP algorithm for each category using the defined example datasets and the
minimum support threshold.</p>
<p align="justify">
7. Output the frequent sequential patterns for each category: Prints the frequent sequential patterns 
    along with their support counts
for each wear category.</p>
<p align="justify">
8. Visulaize the sequence patterns using matplotlib.
</p>
### Program:

```python
from collections import defaultdict
from itertools import combinations

# Function to generate candidate k-item sequences
def generate_candidates(dataset, k):
    c = defaultdict(int)
    for seq in dataset:
        flat_seq = []
        for itemset in seq:
            if isinstance(itemset, str):
                flat_seq.extend(itemset.split(','))
            else:
                flat_seq.extend(itemset)

        # count each combination once per sequence
        for comb in set(combinations(sorted(flat_seq), k)):
            c[comb] += 1

    res = {}
    for item, support in c.items():
        if support >= min_support:
            res[item] = support
    return res

# Function to perform GSP algorithm
def gsp(dataset, min_support):
    k = 1
    fp = defaultdict(int)
    while True:
        c = generate_candidates(dataset, k)
        if not c:
            break
        fp.update(c)
        k += 1
    return fp

# Example dataset
top_wear_data = [
    [["a"],["b"],["c"],["b","e"],["c"],["f"],["g"],["a","b","e"]],
    [["a"],["d"],["b","c"],["c"],["f","g"],["c","h"]],
    [["b"],["c"],["a","d"],["e"],["b"],["f"],["c","d","f","g","h"]],
    [["c"],["e","c"],["e","h"]]
]

min_support = 3

# Run GSP
top_wear_result = gsp(top_wear_data, min_support)

# ---------- TABULAR OUTPUT ----------
patterns_by_length = defaultdict(list)

for pattern, support in top_wear_result.items():
    patterns_by_length[len(pattern)].append((pattern, support))

print("\nFrequent Sequential Patterns - Top Wear\n")

for length in sorted(patterns_by_length):
    print(f"{length}-Length Patterns")
    print("-" * 30)
    print(f"{'Pattern':20} {'Support'}")
    print("-" * 30)
    for pattern, support in patterns_by_length[length]:
        print(f"{str(pattern):20} {support}")
    print()
```
### Output:
<img width="1761" height="717" alt="Screenshot 2026-02-07 134548" src="https://github.com/user-attachments/assets/673f5c8b-f40f-4871-88cf-39cf8e4aa83e" />
<img width="1760" height="816" alt="Screenshot 2026-02-07 134659" src="https://github.com/user-attachments/assets/0d9fe5ac-cbb3-4ccc-961f-74b9e0889040" />
<img width="1752" height="358" alt="image" src="https://github.com/user-attachments/assets/8046b13d-d1ae-4c3e-8cd4-7c810f28bdf4" />

### Visualization:
```python

# Function to visualize frequent sequential patterns with a line plot
def visualize_patterns_line(result, category):
    if result:
        patterns = list(result.keys())
        support = list(result.values())

        plt.figure(figsize=(10, 6))
        plt.plot([str(pattern) for pattern in patterns], support, marker='o', linestyle='-', color='blue')
        plt.xlabel('Patterns')
        plt.ylabel('Support Count')
        plt.title(f'Frequent Sequential Patterns - {category}')
        plt.xticks(rotation=90)
        plt.tight_layout()
        plt.show()
    else:
        print(f"No frequent sequential patterns found in {category}.")

# Visualize frequent sequential patterns for each category using a line plot
visualize_patterns_line(top_wear_result, 'Top Wear')
visualize_patterns_line(bottom_wear_result, 'Bottom Wear')
```
### Output:
<img width="1026" height="607" alt="image" src="https://github.com/user-attachments/assets/75a03e27-8477-4903-9438-442da5003dd9" />

<img width="1033" height="611" alt="Screenshot 2026-02-07 135017" src="https://github.com/user-attachments/assets/5da15d31-c7a0-4d5d-ab33-19f7c66c0f0a" />

### Result:
Thus the implementation of the GSP algorithm in python has been successfully executed.
