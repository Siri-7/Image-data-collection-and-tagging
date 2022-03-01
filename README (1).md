
# Image data auto-tagging using product-name in description


## Authors

- [@Siri-7](https://www.github.com/Siri-7)


## Installation

Install my-project with npm

```bash
import pandas as pd
import re
import random
import json
import os
```
    
## Usage/Examples

files = []
for x in os.listdir('data_jsons'):
    try:
        dff=pd.read_json(f'data_jsons/{x}')
        files.append(dff)
    except:
        print(x)

df = pd.concat(files)

df['product_name_small'] = df['product_name'].str.lower()

j = json.load(open('wrap_toptype.json'))

def match(s):
    try:
        s = s.lower()
        random.shuffle(j["toptype"])
        for w in j["toptype"]:
            if w in s:
                return w
            return "NONE"
    except:
        pass

df['Match'] = df.product_name.apply(match)

df_final = df[['product_name_small', 'feature_image_s3', 'Match']]

df_data = df_final[df_final['Match']!="NONE"]

df_datafinal = df_data.dropna()

df_datafinal.head()

df_noduplicates = df_datafinal.drop_duplicates()
len(df_noduplicates)

filess = []
for x in os.listdir('final/toptype'):
    try:
        dfff=pd.read_csv(f'final/toptype/{x}',delimiter='\t')
        filess.append(dfff)
    except:
        pass

dffff = pd.concat(filess)
y = set(dffff.feature_image_s3.values.tolist())

def values(s):
    return s not in y
def removeurl(s):
    return '.jpg' in s

df_noduplicates = df_noduplicates[df_noduplicates.feature_image_s3.apply(values)]
df_noduplicates = df_noduplicates[df_noduplicates.feature_image_s3.apply(removeurl)]

df_noduplicates.to_csv('wrap_tops.csv', index = False, sep = "\t")
print('DataFrame is written to csv File successfully.')

