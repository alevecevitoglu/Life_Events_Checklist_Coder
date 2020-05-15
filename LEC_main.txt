import pandas as pd
from pandas import ExcelWriter
from pandas import ExcelFile
import numpy as np

#from google.colab import files
#uploaded = files.upload() #This row is for uploading the excel file to colab, if you use smtg else, you might not need it

dataset = pd.read_excel('babip_lec2.xlsx')        #Reading the file
dataset_2 = dataset.reset_index()                   #Indexing the rows

m = dataset.shape[0]
n = dataset.shape[1]

A = np.zeros((m,5))

print (m,n)
print( dataset.iloc[0][0])



''' matrix A:
1st column: Counts the number of nan values
2nd column: Counts the number of positive values
3rd column: Aggregation of the positive values
4th column: Counts the number of negative values
5th column: Aggregation of the negative values

Each row represents a participant
'''

for i in range(m):
  dataset_3 = dataset_2.loc[i, :]
  for j in range(n):
    x = dataset.iloc [i][j]
    if x > 0:
      A[i][1] += 1                                  #A[x][y] selects xth row and yth column of a matrix
      A[i][2] += x
    elif x  < 0:
      A[i][3] += 1
      A[i][4] += x
    elif x  == 0:
      A[i][0] += 1

print(A)
  
df = pd.DataFrame(A)
writer = ExcelWriter('BABIP_LEC2_coded.xlsx')
df.to_excel(writer,'Sheet1',index=False)
writer.save()




