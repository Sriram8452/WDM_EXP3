# EX3:Implementation of GSP Algorithm In Python
# DATE: 

## AIM:
To implement GSP Algorithm In Python.

## Description:
The Generalized Sequential Pattern (GSP) algorithm is a data mining technique used for discovering frequent patterns within a sequence database. It operates by identifying sequences that frequently occur together. GSP works by employing a depth-first search strategy to explore and extract frequent patterns efficiently.

## Steps:
1. <strong>Database Scanning:</strong> GSP scans the sequence database to determine the support of each item in the dataset.
2. <strong>Candidate Generation:</strong> It generates a set of candidate sequences using frequent items found in the previous step.
3. <strong>Pattern Growth:</strong> It extends the candidate sequences by merging them to form longer patterns, checking their support against a user-defined minimum support threshold.
4. <strong>Repeat:</strong> The process continues until no new sequences meet the minimum support threshold.
<p align="justify">
GSP finds application in various domains such as market basket analysis, web usage mining, bioinformatics, and more. For instance, in retail, GSP can identify common purchasing patterns, helping businesses understand customer behavior for targeted marketing or inventory management.
</p>

## Procedure:
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

## Program:
```
from collections import defaultdict
from itertools import combinations
from tabulate import tabulate  # Import tabulate to display in table format

# Function to generate candidate k-item sequences
def generate_candidates(dataset, k):
    candidates = defaultdict(int)
    for seq in dataset:
        for comb in combinations(seq, k):
            candidates[comb] += 1
    return {item: support for item, support in candidates.items() if support >= min_support}

# Function to perform GSP algorithm
def gsp(dataset, min_support):
    frequent_patterns = defaultdict(int)  # Added assignment operator
    k = 1
    sequences = dataset
    while True:
        candidates = generate_candidates(sequences, k)
        if not candidates:
            break
        frequent_patterns.update(candidates)
        k += 1
    return frequent_patterns

# Example dataset for each category
top_wear_data = [
    ["blouse", "t-shirt", "tank_top"],
    ["hoodie", "sweater", "top"],
    ["hoodie"],
    ["hoodie", "sweater"]
    # Add more sequences for top wear
]

bottom_wear_data = [
    ["jeans", "trousers", "shorts"],
    ["leggings", "skirt", "chinos"],
    # Add more sequences for bottom wear
]

party_wear_data = [
    ["cocktail_dress", "evening_gown", "blazer"],
    ["party_dress", "formal_dress", "suit"],
    ["party_dress", "formal_dress", "suit"],
    ["party_dress", "formal_dress", "suit"],
    ["party_dress", "formal_dress", "suit"],
    ["party_dress"],
    ["party_dress"],
    # Add more sequences for party wear
]

# Minimum support threshold
min_support = 2

# Perform GSP algorithm for each category
top_wear_result = gsp(top_wear_data, min_support)
bottom_wear_result = gsp(bottom_wear_data, min_support)
party_wear_result = gsp(party_wear_data, min_support)

# Function to format the output in tabular form
def print_table(result, category):
    table = []
    if result:
        for pattern, support in result.items():
            # Add row with Pattern, Support, Category, and Number of Items
            table.append([pattern, support, category, len(pattern)])
        # Print the table in a formatted way
        print(tabulate(table, headers=["Pattern", "Support", "Category", "Number of Items"], tablefmt="grid"))
    else:
        print(f"No frequent sequential patterns found in {category}.")

# Output the frequent sequential patterns for each category in tabular format
print("Frequent Sequential Patterns - Top Wear:")
print_table(top_wear_result, "Top Wear")

print("\nFrequent Sequential Patterns - Bottom Wear:")
print_table(bottom_wear_result, "Bottom Wear")

print("\nFrequent Sequential Patterns - Party Wear:")
print_table(party_wear_result, "Party Wear")
```

## Output:

![368181427-ab8f627e-9347-48f8-a78e-9b3e89851305](https://github.com/user-attachments/assets/5f180b4f-32b0-4ae6-a7fa-8703ab95f9cc)

## Visualization:
```
import matplotlib.pyplot as plt
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
visualize_patterns_line(party_wear_result, 'Party Wear')
```


## Output:

![image](https://github.com/user-attachments/assets/d4c0c460-9967-424b-9b79-47d111c4ee93)


## Result:
Thus the implementation of the GSP algorithm in python has been successfully executed.
