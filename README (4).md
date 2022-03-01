
# Data Collection using Pinterest package
Image data collection and exploration using Pinterest package in Python
## Authors

- [@Siri-7](https://www.github.com/Siri-7)


## Installation and Code

```bash
from py3pin.Pinterest import Pinterest
import pandas as pd

pinterest = Pinterest(email='your pinterest email',
                      password='set password',
                      username='pinterest username',
                      cred_root='cred_root')

pinterest.login()

user_profile = pinterest.get_user_overview()


#### Board and pin management
boards = pinterest.boards(username='sirishagadepalli')
boards

#### pins
pins = pinterest.board_feed(board_id='930063829235184680')
pins[3]['images']['orig']["url"]

df_boards = pd.DataFrame(boards)

df_pins = pd.DataFrame(pins)
pd.set_option('display.max_columns', None)
pd.set_option('display.max_rows', None)

#### Append all pins to a list

url_pins = []
for i in df_pins.iloc():
    url_pins.append(i['images'])  
    
url_pins[0]

url_pins[0]['orig']["url"]

url_pinsorig = []
for d in url_pins:
    try:
       s = d['orig']["url"] 
       url_pinsorig.append(s)
    except:
        print(d)
        
 url_pinsorig
 
 
 
```
    