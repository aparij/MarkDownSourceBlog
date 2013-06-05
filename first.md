Title: Numpy substring indexing
Date: 2013-05-29 10:20
Category: Python
Tags: python, numpy
Slug: numpy-array-string-search
Author: Alex Parij
Summary: Short version for index and feeds

Working on Kaggle’s Titanic competition I needed to test each Numpy array cell if the string  s1 contained the second string and return another indexed array with True/False.

so if I have

``` python
nparr = np.array([['aaMRac','bbbb'],['ccc','ffff'],['eeee','gggggg']])

[['aaMRac','bbbb'],

['ccc','ffff'],

['eeee','gggggg']]

```
and I’m looking for strings that contain ‘MR’ substring

I want to get

[[ True, False],
[False, False],
[False, False]]

because ‘aaMRac’  is the only that contains ‘MR’.

‘MR’ in nparr

will give me False because it will test for string to string equality and return the answer for entire array.

To get the indexed answer

np.array(['MR' in s for s in nparr.flat]).reshape(nparr.shape)

which flattens and before looking for substring and then creates the new indexed answer with the right shape.

array([[ True, False],
[False, False],
[False, False]], dtype=bool)

 

if you want to go select only one column  you can do like this

np.array(['MR' in s for s in a[0:,1].flat])
