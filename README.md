# Titanic Mini Exploratory Data Analysis (EDA) – Task 3

## 📌 Project Overview

This project is part of **Task 3: Mini Exploratory Data Analysis (EDA) on the Titanic Dataset**.

The main objective of this project is to explore the Titanic passenger dataset, handle missing values, create meaningful age-group categories, and analyze how survival rates varied across different passenger groups and embarkation ports.

The analysis is performed using **Python, Pandas, Seaborn, and Matplotlib**.

---

## 🎯 Objectives

The main objectives of this project are:

* Load and inspect the Titanic dataset.
* Identify and handle missing values.
* Remove the `Cabin` column because it contains a large number of missing values.
* Create meaningful age-group categories.
* Calculate survival rates for different age groups.
* Calculate survival rates based on embarkation port.
* Visualize the findings using bar plots.
* Understand patterns and relationships in the Titanic survival data.

---

## 📂 Dataset

The project uses the **Titanic Dataset**.

The dataset contains information about **891 passengers** and includes features such as:

* `PassengerId` – Unique passenger identification number
* `Survived` – Survival status (0 = No, 1 = Yes)
* `Pclass` – Passenger class
* `Name` – Passenger name
* `Sex` – Passenger gender
* `Age` – Passenger age
* `SibSp` – Number of siblings/spouses aboard
* `Parch` – Number of parents/children aboard
* `Ticket` – Ticket number
* `Fare` – Passenger fare
* `Cabin` – Cabin number
* `Embarked` – Port of embarkation

The notebook loads the dataset using:

```python
df = pd.read_csv("Titanic-Dataset.csv")
```

The first few rows are displayed using `df.head()`.

---

## 🛠️ Technologies Used

* **Python**
* **Pandas**
* **Seaborn**
* **Matplotlib**
* **Google Colab / Jupyter Notebook**

---

## 🔍 Project Workflow

### 1. Import Required Libraries

The following Python libraries are imported:

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
```

Pandas is used for data manipulation and analysis, while Seaborn and Matplotlib are used for visualization.

---

### 2. Load the Titanic Dataset

The Titanic dataset is loaded into a Pandas DataFrame.

```python
df = pd.read_csv("Titanic-Dataset.csv")
df.head()
```

## The dataset contains **891 rows** and 12 original columns.

### 3. Handle Missing Values

Missing values in the `Age` column are handled by replacing them with the mean age.

```python
df["Age"].fillna(df["Age"].mean(), inplace=True)
```

After this step, the `Age` column has no missing values.

## The missing-value check shows that `Cabin` has 687 missing values and `Embarked` has 2 missing values.

### 4. Remove the Cabin Column

Because the `Cabin` column contains a very large number of missing values, it is removed from the dataset.

```python
df.drop(columns=["Cabin"], inplace=True)
```

This simplifies the dataset and avoids using a feature with extensive missing information.

---

### 5. Create Age Groups

The `Age` column is converted into meaningful age categories using `pd.cut()`.

The categories created are:

| Age Range | Category   |
| --------- | ---------- |
| 0–12      | Child      |
| 12–18     | Teen       |
| 18–30     | YoungAdult |
| 30–50     | Adult      |
| 50–80     | Senior     |

The notebook creates these categories using:

```python
df["AgeGroup"] = pd.cut(
    df["Age"],
    bins=[0, 12, 18, 30, 50, 80],
    labels=["Child", "Teen", "YoungAdult", "Adult", "Senior"]
)
```

---

# 📊 Exploratory Data Analysis

## Question 1: What is the Survival Rate by Age Group?

The survival rate is calculated by grouping passengers according to `AgeGroup`.

```python
age_survival = df.groupby("AgeGroup")["Survived"].mean()
print(age_survival)
```

The observed survival rates are:

| Age Group  | Survival Rate |
| ---------- | ------------: |
| Child      |        57.97% |
| Teen       |        42.86% |
| YoungAdult |        33.11% |
| Adult      |        42.32% |
| Senior     |        34.38% |

The analysis shows that the **Child** age group had the highest survival rate among the defined age groups, while the **YoungAdult** group had the lowest in this analysis.

### Visualization

A Seaborn bar plot is used to visualize the survival rate by age group.

```python
sns.barplot(x="AgeGroup", y="Survived", data=df)
plt.title("Survival Rate by Age Group")
plt.show()
```

---

## Question 2: What is the Survival Rate by Embarkation Port?

The survival rate is also analyzed according to the passenger's embarkation port.

```python
port_survival = df.groupby("Embarked")["Survived"].mean()
print(port_survival)
```

The results are:

| Embarkation Port | Survival Rate |
| ---------------- | ------------: |
| C                |        55.36% |
| Q                |        38.96% |
| S                |        33.70% |

According to the analysis, passengers who embarked from **Port C** had the highest survival rate, while passengers from **Port S** had the lowest survival rate among the three ports.

### Visualization

A bar plot is used to visualize the survival rate by embarkation port.

```python
sns.barplot(x="Embarked", y="Survived", data=df)
plt.title("Survival Rate by Embarkation Port")
plt.show()
```

---

## 📈 Key Findings

From the analysis:

1. The Titanic dataset contains **891 passenger records**.
2. Missing values in the `Age` column were handled using the mean age.
3. The `Cabin` column was removed because it contained a large number of missing values.
4. Passengers were divided into five age groups: Child, Teen, YoungAdult, Adult, and Senior.
5. The **Child** group showed the highest survival rate among the age groups analyzed.
6. The **YoungAdult** group showed the lowest survival rate among the age groups.
7. Survival rates differed across embarkation ports.
8. Port **C** had the highest observed survival rate.
9. Port **S** had the lowest observed survival rate.

## These findings are based on the calculations and visualizations present in this notebook.

## 📁 Project Structure

```text
titanic-mini-eda-task-3/
│
├── Titanic-Dataset.csv
├── task_3_internship.ipynb
└── README.md
```

> Make sure the dataset filename in the repository matches the filename used in the notebook: `Titanic-Dataset.csv`.

---

## 🚀 How to Run the Project

### Step 1: Clone the Repository

```bash
git clone https://github.com/your-username/titanic-mini-eda-task-3.git
```

### Step 2: Open the Project

Open the project folder in **Jupyter Notebook** or **Google Colab**.

### Step 3: Upload the Dataset

Make sure `Titanic-Dataset.csv` is available in the same working directory as the notebook.

### Step 4: Run the Notebook

Run the notebook cells from top to bottom to reproduce the analysis and visualizations.

---

## 📌 Conclusion

This project demonstrates the basic workflow of **Exploratory Data Analysis (EDA)** using the Titanic dataset.

The analysis focuses on data cleaning, missing-value handling, feature categorization, grouping, survival-rate calculation, and data visualization.

The project provides a simple understanding of how passenger characteristics such as **age group and embarkation port** were associated with survival outcomes in the Titanic dataset.

---

## 👩‍💻 Author

**Nandini Yadav**

### Internship Task

**Task 3 – Mini Exploratory Data Analysis (EDA) on Titanic Dataset**
