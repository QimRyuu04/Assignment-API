#MTBjYjJmN2YtMDM1MS00YWNjLTg2NWEtNTdlYjQyNDVlNjRiMjBmZGI2OGUtNzUy_P0A1_36820416-bfff-433a-84bf-39585b2b3f67
import requests
import json

acc_token = input("Please enter you access token: ")
print("\nMENU OPTION")
print("-" * 130 )
print("Test connection_____________(0)")
print("Display User Information____(1)")
print("Display 5 Rooms_____________(2)")
print("Create a room_______________(3)")
print("Send message to a room______(4)")
print("-" * 130 )

option  = input("\nplease choose option: ")
headers = {
            'Authorization' : 'Bearer {}'. format(acc_token),
            'Content-Type': 'application/json'
        }
url='https://webexapis.com/v1/people/me'
res = requests.get(url, headers=headers)

if option== "0":
        
        try:
            if res.status_code == 200:
                print("\nconnection to webex server successfull")
            else:
                print("\nconnection to webex server failed")
        except Exception as e:
            print(f"Connection failed with error: {e}")

elif option == "1":
        
        userInfo = res.json()
        print("USER INFORMATION")
        print("-" * 130)
        print(f"User Displayed name: {userInfo['displayName']} ")
        print(f"User Nickname: {userInfo['nickName']}")
        print(f"User email: {', '.join(userInfo['emails'])}")
        print("-" * 130)

elif option == "2":
    url = "https://webexapis.com/v1/rooms"
    params = {'max' : '5'}
    res = requests.get(url, headers=headers, params=params)
    roomInfo = res.json()

    if res.status_code == 200:
         
         if "items" in roomInfo:
              print ("ROOM INFORMATION")
              print ("-" * 120)
              for item in roomInfo['items']:
                   print (f"Room Id: {item['id']}")
                   print (f"Room name: {item['title']}")
                   print (f"Room's date  created: {item['created']}")
                   print (f"Last activity: {', '.join(item['lastActivity'])}")
                   print ("-" * 120)

if option == "3":
     url = 'https://webexapis.com/v1/rooms'
     RName = input("Give the room to want to create a name: ")
     params = {'title': RName}

     res = requests.post(url, headers=headers, json=params)
     if res.status_code == 200:
          print (f"\nRoom: {RName} has been created")
     else:
          print (f"\nFailed to created a room due to {res.status_code}")

elif option == "4":
     url = 'https://webexapis.com/v1/rooms'
     params = {'max':'5'}
     res = requests.get(url, headers=headers, params=params)
     roomInfo = res.json()

     if res.status_code == 200:
          print ("\tROOMS")
          print ("-" * 120)
          for i,item in enumerate (roomInfo['items']):
               print(f"({i + 1}) {item['title']}")

          print ("-" * 120)
          roomChoice = int(input("\nPlease choose a room you want to send a message: "))-1

          if 0 <= roomChoice <len(roomInfo['items']):
               roomIDsel = roomInfo['items'] [roomChoice]['id']
               roomNameSel = roomInfo['items'] [roomChoice]['title']
               mesToRoom = input("Enter the message you want to send: ")
               params = {'roomId': roomIDsel, 'markdown':mesToRoom}
               url = 'https://webexapis.com/v1/messages'
               res = requests.post(url, headers=headers, json=params)

               if res.status_code == 200:
                    print (f"\nMessage: {mesToRoom} is successfully to room: {roomNameSel}")
               else:
                    print (f"\nFailed to send message due to error: {res.status_code}")

else:
     print ("\nPlease choose the right option")
userInput = input("\nPress enter to enter to main menu...........")
