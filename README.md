# maincraft-internship-task-1
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

#----1 # Load the dataset with semicolon delimiter-----------
data = pd.read_csv(r"C:\Users\smdta\Documents\MAincraft internship\student-mat.csv", sep=';')

#-------------------2 Explore & Clean Data-------------
# Check for missing values
null_values = data.isnull().sum()
print("Missing values in each column:")
print(null_values)

# Remove duplicates
data = data.drop_duplicates()
print("\nDuplicates removed.")

# Inspect dataset shape and data types
print("\nDataset shape:", data.shape)
print("\nData types of each column:")
print(data.dtypes)
print("\nColumn names:")
print(data.columns.tolist())

#------------------3 # Analysis-----------------

# Average final grade (G3)
average_grade = data['G3'].mean()
print("\nAverage final grade (G3):", average_grade)

# Number of students who scored above 15
students_above_15 = data[data['G3'] > 15].shape[0]
print("\nNumber of students who scored above 15:", students_above_15)

# Correlation between study time and performance
correlation = data['studytime'].corr(data['G3'])
print("\nCorrelation between study time and performance:", correlation)

# Gender performance comparison
average_score_by_gender = data.groupby('sex')['G3'].mean()
print("\nAverage score by gender:")
print(average_score_by_gender)

#-----------4 # Visualizations-----------------

# Histogram of grades
plt.figure(figsize=(8, 5))
sns.histplot(data['G3'], bins=10, kde=True, color='blue')
plt.title('Histogram of Final Grades (G3)')
plt.xlabel('Final Grade (G3)')
plt.ylabel('Frequency')
plt.show()

# Scatterplot: study time vs grades
plt.figure(figsize=(8, 5))
sns.scatterplot(x=data['studytime'], y=data['G3'], color='green')
plt.title('Study Time vs Final Grades')
plt.xlabel('Study Time')
plt.ylabel('Final Grade (G3)')
plt.show()

# Bar chart: male vs female average score
plt.figure(figsize=(8, 5))
average_score_by_gender.plot(kind='bar', color=['orange', 'purple'])
plt.title('Average Final Grade by Gender')
plt.xlabel('Gender')
plt.ylabel('Average Final Grade (G3)')
plt.xticks(rotation=0)
plt.show()
