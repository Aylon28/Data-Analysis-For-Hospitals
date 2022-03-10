import pandas as pd
import matplotlib.pyplot as plt

# for better visualization
pd.set_option('display.max_columns', 8)

# reading files
general = pd.read_csv('test/general.csv')
prenatal = pd.read_csv('test/prenatal.csv')
sports = pd.read_csv('test/sports.csv')

# changing column names to the same for every file
prenatal.columns = ['Unnamed: 0', 'hospital', 'gender', *prenatal.columns[3:]]
sports.columns = ['Unnamed: 0', 'hospital', 'gender', *prenatal.columns[3:]]
all_hospitals = pd.concat([general, prenatal, sports], ignore_index=True)
all_hospitals.drop(columns=['Unnamed: 0'], inplace=True)

# dropping empty, changing gender column to the same content
all_hospitals.dropna(axis=0, how='all', inplace=True)
all_hospitals.loc[all_hospitals.gender == 'man', 'gender'] = 'm'
all_hospitals.loc[all_hospitals.gender == 'male', 'gender'] = 'm'
all_hospitals.loc[all_hospitals.gender == 'woman', 'gender'] = 'f'
all_hospitals.loc[all_hospitals.gender == 'female', 'gender'] = 'f'
all_hospitals['gender'] = all_hospitals['gender'].fillna('f')

# filling NaNs with zeros
all_hospitals['bmi'] = all_hospitals['bmi'].fillna(0)
all_hospitals['blood_test'] = all_hospitals['blood_test'].fillna(0)
all_hospitals['diagnosis'] = all_hospitals['diagnosis'].fillna(0)
all_hospitals['ecg'] = all_hospitals['ecg'].fillna(0)
all_hospitals['ultrasound'] = all_hospitals['ultrasound'].fillna(0)
all_hospitals['mri'] = all_hospitals['mri'].fillna(0)
all_hospitals['xray'] = all_hospitals['xray'].fillna(0)
all_hospitals['children'] = all_hospitals['children'].fillna(0)
all_hospitals['months'] = all_hospitals['months'].fillna(0)

# printing statistics
general = all_hospitals.loc[(all_hospitals['hospital'] == 'general')]
sports = all_hospitals.loc[(all_hospitals['hospital'] == 'sports')]
prenatal = all_hospitals.loc[(all_hospitals['hospital'] == 'prenatal')]

second = round(len(all_hospitals.loc[(all_hospitals['hospital'] == 'general') & (general['diagnosis'] == 'stomach')]) / len(general), 3)
third = round(len(all_hospitals.loc[(all_hospitals['hospital'] == 'sports') & (all_hospitals['diagnosis'] == 'dislocation')]) / len(sports), 3)
fourth = general.age.median() - sports.age.median()

fifth_1 = len(all_hospitals.loc[(all_hospitals['hospital'] == 'general') & (all_hospitals['blood_test'] == 't')])
fifth_2 = len(all_hospitals.loc[(all_hospitals['hospital'] == 'sports') & (all_hospitals['blood_test'] == 't')])
fifth_3 = len(all_hospitals.loc[(all_hospitals['hospital'] == 'prenatal') & (all_hospitals['blood_test'] == 't')])

if fifth_1 > fifth_2 and fifth_1 > fifth_3:
    name = 'general'
elif fifth_2 > fifth_3:
    name = 'sports'
else:
    name = 'prenatal'

print('The answer to the 1st question is', str(all_hospitals['hospital'].value_counts()).split()[0])
print('The answer to the 2nd question is', second)
print('The answer to the 3rd question is', third)
print('The answer to the 4th question is', fourth)
print('The answer to the 5th question is', name + ',',  max(fifth_1, fifth_2, fifth_3), 'blood test')

# printing charts
age_column = all_hospitals['age'].to_list()
bins = [0, 15, 35, 55, 70, 80]
plt.hist(age_column, bins=bins)
plt.show()

diagnosis_column = all_hospitals['diagnosis'].to_list()
diagnosis_column_int = list(set(diagnosis_column))
diagnosis_pie = []
for item in diagnosis_column_int:
    count = 0
    for item_2 in diagnosis_column:
        if item == item_2:
            count += 1
    diagnosis_pie.append(count)
plt.pie(diagnosis_pie)
plt.legend(diagnosis_column_int)
plt.show()

print('The answer to the 1st question: 15-35')
print('The answer to the 2nd question: pregnancy')

# printing info from dataframe
print(all_hospitals.head(600))
print(all_hospitals.tail(5))
print(all_hospitals.shape)
print(all_hospitals.sample(n=20, random_state=30))
