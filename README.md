# Image-data-collection-and-tagging
from py3pin.Pinterest import Pinterest
import pandas as pd

pinterest = Pinterest(email='your pinterest email',
                      password='set password',
                      username='pinterest username',
                      cred_root='cred_root')

pinterest.login()

# Loading a profile on pinterest
# pinterest.pin(board_id="https://pin.it/5Ix86fT",#unique identifier of every board
#              image_url="https://pin.it/3qo7qQc",  #URL of the image you want to pin, right-click and copy image address
# user_profile
user_profile = pinterest.get_user_overview()


# Board and pin management
boards = pinterest.boards(username='sirishagadepalli')
boards

# pins
pins = pinterest.board_feed(board_id='930063829235184680')
pins[3]['images']['orig']["url"]

df_boards = pd.DataFrame(boards)

df_pins = pd.DataFrame(pins)
pd.set_option('display.max_columns', None)
pd.set_option('display.max_rows', None)
#df_pins.head()

# df_pins.to_csv('image_signature.csv')#, index = False, sep = "\t")
# print('DataFrame is written to csv File successfully.')

# Append all pins to a list

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
 
 
 # Delete pin or repin
 
 ##pinterest.delete_pin(pin_id='pin_id')
##pinterest.repin(board_id='board_id', pin_id='pin_id')

# Follow-unfollow user

# pinterest.follow_user(user_id='target_user_id', username='target_username')
# pinterest.unfollow_user(user_id='target_user_id', username='target_username')
# following_batch = pinterest.get_following(username='some_user')
# followers_batch=pinterest.get_user_followers(username='some_user')
# pinterest.follow_board(board_id=board_id)
# pinterest.unfollow_board(board_id=board_id)

# Pin information by id and support

# pinterest.load_pin(pin_id='pin_id')
# pinterest.create_board_section(board_id=board_id, section_name=section_name)
# pinterest.delete_board_section(section_id=section_id)
# pinterest.get_board_sections(board_id=board_id)

# board recommendations

## rec_batch = pinterest.board_recommendations(board_id='930063829235184680')
## rec_batch[1]['images']['orig']["url"]
## pinterest.pin(board_id='930063829235184680', image_url='https://i.pinimg.com/originals/e1/0a/9f/e10a9f5929fb7548cd522e31f788061b.jpg', description='Puff sleeve test', title='Puff sleeve test1') #pin image using a web URL to my board


