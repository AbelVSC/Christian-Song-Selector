# Christian-Song-Selector
A python program that can help you select a song and give its lyrics as well. The program will also copy those lyrics to your clipboard so that you can paste it anywhere.

I made this program because it allows me to select a song faster and save time compared to me spending lots of time figuring out which song to sing in the church. I hope it becomes useful for you as well. If you like it please consider giving a 🌟 and share it to others.

# Modules used in this program
1. This python script is connected to a ```SQL``` database written in SQLite that contains all the song names, their lyrics and their language.
2. Python and SQLite is connected through the ```sqlite3``` module which is a built-in module in python for Windows. As for MacOS and Linux you'll have to install it in your environment. The script runs from the database file.
4. The python script uses ```random``` module which is a built-in module in python for all platforms that chooses a song randomly from the database.
5. To copy the lyrics to the clipboard it uses ```pyperclip``` module.

# To run it
1. Make sure python is installed in your device. Any of the newer versions will work.
2. Make sure to download the database file.
3. Make sure that the modules mentioned above are installed. You can use ```pip install [module]``` command to install them. Just replace "[module]" with your desired module and put this command in the command prompt.
4. The database file and the python script doesn't have to be in the same folder. Just make sure to give the file path of the database file in line 8 of the python script.
   ```python
   connection=sqlite3.connect("Database_File_path.db")
   ```

# Code
Below is the script:
```python
import sqlite3

import random

import pyperclip


connection=sqlite3.connect("Database_File_path.db")
communication=connection.cursor()
def sname_generation_1():  #Select song names from database
    communication.execute("SELECT SONG_NAME FROM CHRISTIAN_SONGS_TB")
    result_name_1=communication.fetchall()
    sname_bank=[]
    for i in result_name_1:
        sname_bank.append(i[0])
    song_name=random.choice(sname_bank)
    return song_name

def slyrics_generation_1(sname):  #Select song lyrics from the database
    communication.execute("SELECT SONG_NAME,SONG_LYRICS FROM CHRISTIAN_SONGS_TB")
    result_lyrics_1=communication.fetchall()
    slyrics_bank=[]
    for j in result_lyrics_1:
        if j[0]==sname:
            slyrics_bank.append(j[1])
    song_lyrics=slyrics_bank[0]
    return song_lyrics

def slyrics_copy(slyrics):  #Copy the lyrics to clipboard
    pyperclip.copy(slyrics)
    print("\nLyrics copied to the clipboard")

def sname_generation_2_eng():  #Select english song names from database
    communication.execute("SELECT SONG_NAME FROM CHRISTIAN_SONGS_TB WHERE LANGUAGE='English'")
    result_name_2_eng=communication.fetchall()
    sname_bank_eng=[]
    for k in result_name_2_eng:
        sname_bank_eng.append(k[0])
    song_name_eng=random.choice(sname_bank_eng)
    return song_name_eng

def slyrics_generation_2_eng(sname_eng):  #Select english song lyrics from the database
    communication.execute("SELECT SONG_NAME,SONG_LYRICS FROM CHRISTIAN_SONGS_TB WHERE LANGUAGE='English'")
    result_lyrics_2_eng=communication.fetchall()
    slyrics_bank_eng=[]
    for l in result_lyrics_2_eng:
        if l[0]==sname_eng:
            slyrics_bank_eng.append(l[1])
    song_lyrics_eng=random.choice(slyrics_bank_eng)
    return song_lyrics_eng

def slyrics_eng_copy(slyrics_eng):  #Copy the lyrics to clipboard
    pyperclip.copy(slyrics_eng)
    print("\nLyrics copied to the clipboard")

def sname_generation_2_mal():  #Select malayalam song names from database
    communication.execute("SELECT SONG_NAME FROM CHRISTIAN_SONGS_TB WHERE LANGUAGE='Malayalam'")
    result_name_2_mal=communication.fetchall()
    sname_bank_mal=[]
    for m in result_name_2_mal:
        sname_bank_mal.append(m[0])
    song_name_mal=random.choice(sname_bank_mal)
    return song_name_mal

def slyrics_generation_2_mal(sname_mal):  #Select malayalam song lyrics from the database
    communication.execute("SELECT SONG_NAME,SONG_LYRICS FROM CHRISTIAN_SONGS_TB WHERE LANGUAGE='Malayalam'")
    result_lyrics_2_mal=communication.fetchall()
    slyrics_bank_mal=[]
    for n in result_lyrics_2_mal:
        if n[0]==sname_mal:
            slyrics_bank_mal.append(n[1])
    song_lyrics_mal=random.choice(slyrics_bank_mal)
    return song_lyrics_mal

def slyrics_mal_copy(slyrics_mal):  #Copy the lyrics to clipboard
    pyperclip.copy(slyrics_mal)
    print("\nLyrics copied to the clipboard")

def sname_generation_2_hin():  #Select hindi song names from database
    communication.execute("SELECT SONG_NAME FROM CHRISTIAN_SONGS_TB WHERE LANGUAGE='Hindi'")
    result_name_2_hin=communication.fetchall()
    sname_bank_hin=[]
    for o in result_name_2_hin:
        sname_bank_hin.append(o[0])
    song_name_hin=random.choice(sname_bank_hin)
    return song_name_hin

def slyrics_generation_2_hin(sname_hin):  #Select hindi song lyrics from the database
    communication.execute("SELECT SONG_NAME,SONG_LYRICS FROM CHRISTIAN_SONGS_TB WHERE LANGUAGE='Hindi'")
    result_lyrics_2_hin=communication.fetchall()
    slyrics_bank_hin=[]
    for p in result_lyrics_2_hin:
        if p[0]==sname_hin:
            slyrics_bank_hin.append(p[1])
    song_lyrics_hin=random.choice(slyrics_bank_hin)
    return song_lyrics_hin

def slyrics_hin_copy(slyrics_hin):  #Copy the lyrics to clipboard
    pyperclip.copy(slyrics_hin)
    print("\nLyrics copied to the clipboard")


if __name__=="__main__":
    print("#################### Welcome to Christian Song Generator ####################")
    print("""\nPress '1' to generate a song from any language
Press '2' to generate a song from a specific language""")
    while True:
        choice=input("\nEnter your choice: ")
        if choice not in ["1","2"]:
            print("Ohh invalid input, please enter '1' or '2' according to your needs")
        else:
            break


    if choice=='1':
        print("\nWould you like the program to choose a song for you?")
        print("Press (Y/y) to continue or (N/n) to exit the program")
        while True:
            dec=input("\nEnter your decision: ").lower()
            if dec not in ["y","n"]:
                print("Ohh invalid input, please enter 'y' or 'n' according to your needs")
            else:
                break
        while True:
            if dec=="y":
                sname=sname_generation_1()
                print("\nSelected song name is: ",sname)
                print("\nIs this song fine?")
                print("Press (Y/y) to confirm or (N/n) to generate again")
                while True:
                    dec1=input("\nEnter your decision: ").lower()
                    if dec1 not in ["y","n"]:
                        print("Ohh invalid input, please enter 'y' or 'n' according to your needs")
                    else:
                        break
                if dec1=="y":
                    print("\nWould you like to have its lyrics as well?")
                    print("Press (Y/y) to continue or (N/n) to not continue")
                    while True:
                        dec2=input("\nEnter your decision: ").lower()
                        if dec2 not in ["y","n"]:
                            print("Ohh invalid input, please enter 'y' or 'n' according to your needs")
                        else:
                            break
                    if dec2=="y":
                        print("\nThe lyrics of the selected song is: ")
                        slyrics=slyrics_generation_1(sname)
                        print(slyrics)
                    elif dec2=="n":
                        print("\nOkay Great!! Would you like the program to choose another song for you?")
                        print("Press (Y/y) to continue or (N/n) to not continue")
                        while True:
                            dec3=input("\nEnter your decision: ").lower()
                            if dec3 not in ["y","n"]:
                                print("Ohh invalid input, please enter 'y' or 'n' according to your needs")
                            else:
                                break
                        if dec3=="y":
                            print("\nSelected song name is: ",sname)
                            print("\nIs this song fine?")
                            print("Press (Y/y) to confirm or (N/n) to generate again")
                            while True:
                                dec4=input("\nEnter your decision: ").lower()
                                if dec4 not in ["y","n"]:
                                    print("Ohh invalid input, please enter 'y' or 'n' according to your needs")
                                else:
                                    break
                            if dec4=="y":
                                print("\nWould you like to have its lyrics as well?")
                                print("Press (Y/y) to continue")
                                while True:
                                    dec5=input("\nEnter your decision: ").lower()
                                    if dec5 not in ["y"]:
                                        print("Ohh invalid input, please enter 'y'")
                                    else:
                                        break
                                if dec5=="y":
                                    print("\nThe lyrics of the selected song is: ")
                                    slyrics=slyrics_generation_1(sname)
                                    print(slyrics)
                            elif dec4=="n":
                                continue
                        elif dec3=="n":
                            print("""Okay Great!!
Exiting the program
See you later👋""")
                            break
                elif dec1=="n":
                    continue
                

                #Copy to Clipboard
                print("\nDo you want the lyrics to be copied to your clipboard?")
                print("Press (Y/y) to continue or (N/n) to exit the program")
                while True:
                    decision_1=input("\nEnter your decision: ").lower()
                    if decision_1 not in ["y","n"]:
                        print("Ohh invalid input, please enter 'y' or 'n' according to your needs")
                    else:
                        break
                if decision_1=="y":
                    slyrics_copy(slyrics)
                    print("Thank You for using the program😊")
                    break
                elif decision_1=="n":
                    print(""""\nExiting the program
See you later👋""")
                    break                    
            elif dec=="n":
                print("""\nExiting the program
See you later👋""")
                break

                


    elif choice=='2':
        print("\nWould you like the program to choose a song for you?")
        print("Press (Y/y) to continue or (N/n) to exit the program")
        while True:
            dec6=input("\nEnter your decision: ").lower()
            if dec6 not in ["y","n"]:
                print("Ohh invalid input, please enter 'y' or 'n' according to your needs")
            else:
                break
        if dec6=="y":
            print("\nFrom which language do you want the program to choose a song?")
            print("""Languages we have are:
1. English
2. Malayalam
3. Hindi""")
            while True:
                lang=input("\nEnter the language: ").lower()
                if lang not in ['english', 'malayalam', 'hindi']:
                    print("Ohh invalid input, please enter the appropriate language as given")
                else:
                    break
            while True:
                if lang=="english":
                    sname_eng=sname_generation_2_eng()
                    print("\nSelected song name is: ",sname_eng)
                    print("\nIs this song fine?")
                    print("Press (Y/y) to confirm or (N/n) to generate again")
                    while True:
                        dec7=input("\nEnter your decision: ").lower()
                        if dec7 not in ["y","n"]:
                            print("Ohh invalid input, please enter 'y' or 'n' according to your needs")
                        else:
                            break
                    if dec7=="y":
                        print("\nWould you like to have its lyrics as well?")
                        print("Press (Y/y) to continue or (N/n) to not continue")
                        while True:
                            dec8=input("\nEnter your decision: ").lower()
                            if dec8 not in ["y","n"]:
                                print("Ohh invalid input, please enter 'y' or 'n' according to your needs")
                            else:
                                break
                        if dec8=="y":
                            print("\nThe lyrics of the selected song is: ")
                            slyrics_eng=slyrics_generation_2_eng(sname_eng)
                            print(slyrics_eng)
                        elif dec8=="n":
                            print("\nOkay Great!! Would you like the program to choose another song for you?")
                            print("Press (Y/y) to continue or (N/n) to not continue")
                            while True:
                                dec9=input("\nEnter your decision: ").lower()
                                if dec9 not in ["y","n"]:
                                    print("Ohh invalid input, please enter 'y' or 'n' according to your needs")
                                else:
                                    break
                            if dec9=="y":
                                print("\nSelected song name is: ",sname_eng)
                                print("\nIs this song fine?")
                                print("Press (Y/y) to confirm or (N/n) to generate again")
                                while True:
                                    dec10=input("\nEnter your decision: ").lower()
                                    if dec10 not in ["y","n"]:
                                        print("Ohh invalid input, please enter 'y' or 'n' according to your needs")
                                    else:
                                        break
                                if dec10=="y":
                                    print("\nWould you like to have its lyrics as well?")
                                    print("Press (Y/y) to continue")
                                    while True:
                                        dec11=input("\nEnter your decision: ").lower()
                                        if dec11 not in ["y"]:
                                            print("Ohh invalid input, please enter 'y'")
                                        else:
                                            break
                                    if dec11=="y":
                                        print("\nThe lyrics of the selected song is: ")
                                        slyrics_eng=slyrics_generation_2_eng(sname_eng)
                                        print(slyrics_eng)
                                elif dec10=="n":
                                        continue
                            elif dec9=="n":
                                print("""\nExiting the program
See you later👋""")
                                break


                        #Copy to Clipboard(English)
                        print("\nDo you want the lyrics to be copied to your clipboard?")
                        print("Press (Y/y) to continue or (N/n) to exit the program")
                        while True:
                            decision_1=input("\nEnter your decision: ").lower()
                            if decision_1 not in ["y","n"]:
                                print("Ohh invalid input, please enter 'y' or 'n' according to your needs")
                            else:
                                break
                        if decision_1=="y":
                            slyrics_eng_copy(slyrics_eng)
                            print("Thank You for using the program😊")
                            break
                        elif decision_1=="n":
                            print(""""\nExiting the program
See you later👋""")
                            break
                    elif dec7=="n":
                        continue


                elif lang=="malayalam":
                    sname_mal=sname_generation_2_mal()
                    print("\nSelected song name is: ",sname_mal)
                    print("\nIs this song fine?")
                    print("Press (Y/y) to confirm or (N/n) to generate again")
                    while True:
                        dec12=input("\nEnter your decision: ").lower()
                        if dec12 not in ["y","n"]:
                            print("Ohh invalid input, please enter 'y' or 'n' according to your needs")
                        else:
                            break
                    if dec12=="y":
                        print("\nWould you like to have its lyrics as well?")
                        print("Press (Y/y) to continue or (N/n) to not continue")
                        while True:
                            dec13=input("\nEnter your decision: ").lower()
                            if dec13 not in ["y","n"]:
                                print("Ohh invalid input, please enter 'y' or 'n' according to your needs")
                            else:
                                break
                        if dec13=="y":
                            slyrics_mal=slyrics_generation_2_mal(sname_mal)
                            print(slyrics_mal)
                        elif dec13=="n":
                            print("\nOkay Great!! Would you like the program to choose another song for you?")
                            print("Press (Y/y) to continue or (N/n) to not continue")
                            while True:
                                dec14=input("\nEnter your decision: ").lower()
                                if dec14 not in ["y","n"]:
                                    print("Ohh invalid input, please enter 'y' or 'n' according to your needs")
                                else:
                                    break
                            if dec14=="y":
                                print("\nSelected song name is: ",sname_mal)
                                print("\nIs this song fine?")
                                print("Press (Y/y) to confirm or (N/n) to generate again")
                                while True:
                                    dec15=input("\nEnter your decision: ").lower()
                                    if dec15 not in ["y","n"]:
                                        print("Ohh invalid input, please enter 'y' or 'n' according to your needs")
                                    else:
                                        break
                                if dec15=="y":
                                    print("\nWould you like to have its lyrics as well?")
                                    print("Press (Y/y) to continue")
                                    while True:
                                        dec16=input("\nEnter your decision: ").lower()
                                        if dec16 not in ["y"]:
                                            print("Ohh invalid input, please enter 'y'")
                                        else:
                                            break
                                    if dec16=="y":
                                        print("\nThe lyrics of the selected song is: ")
                                        slyrics_mal=slyrics_generation_2_mal(sname_mal)
                                        print(slyrics_mal)
                                elif dec15=="n":
                                        continue
                            elif dec14=="n":
                                print("""\nExiting the program
See you later👋""")
                                break


                        #Copy to Clipboard(Malayalam)
                        print("\nDo you want the lyrics to be copied to your clipboard?")
                        print("Press (Y/y) to continue or (N/n) to exit the program")
                        while True:
                            decision_1=input("\nEnter your decision: ").lower()
                            if decision_1 not in ["y","n"]:
                                print("Ohh invalid input, please enter 'y' or 'n' according to your needs")
                            else:
                                break
                        if decision_1=="y":
                            slyrics_mal_copy(slyrics_mal)
                            print("Thank You for using the program😊")
                            break
                        elif decision_1=="n":
                            print(""""\nExiting the program
See you later👋""")
                            break   
                    elif dec12=="n":
                        continue

                    
                elif lang=="hindi":
                    sname_hin=sname_generation_2_hin()
                    print("\nSelected song name is: ",sname_hin)
                    print("\nIs this song fine?")
                    print("Press (Y/y) to confirm or (N/n) to generate again")
                    while True:
                        dec16=input("\nEnter your decision: ").lower()
                        if dec16 not in ["y","n"]:
                            print("Ohh invalid input, please enter 'y' or 'n' according to your needs")
                        else:
                            break
                    if dec16=="y":
                        print("\nWould you like to have its lyrics as well?")
                        print("Press (Y/y) to continue or (N/n) to not continue")
                        while True:
                            dec17=input("\nEnter your decision: ").lower()
                            if dec17 not in ["y","n"]:
                                print("Ohh invalid input, please enter 'y' or 'n' according to your needs")
                            else:
                                break
                        if dec17=="y":
                            print("\nThe lyrics of the selected song is: ")
                            slyrics_hin=slyrics_generation_2_hin(sname_hin)
                            print(slyrics_hin)
                        elif dec17=="n":
                            print("\nOkay Great!! Would you like the program to choose another song for you?")
                            print("Press (Y/y) to continue or (N/n) to not continue")
                            while True:
                                dec18=input("\nEnter your decision: ").lower()
                                if dec18 not in ["y","n"]:
                                    print("Ohh invalid input, please enter 'y' or 'n' according to your needs")
                                else:
                                    break
                            if dec18=="y":
                                print("\nSelected song name is: ",sname_hin)
                                print("\nIs this song fine?")
                                print("Press (Y/y) to confirm or (N/n) to generate again")
                                while True:
                                    dec19=input("\nEnter your decision: ").lower()
                                    if dec19 not in ["y","n"]:
                                        print("Ohh invalid input, please enter 'y' or 'n' according to your needs")
                                    else:
                                        break
                                if dec19=="y":
                                    print("\nWould you like to have its lyrics as well?")
                                    print("Press (Y/y) to continue")
                                    while True:
                                        dec20=input("\nEnter your decision: ").lower()
                                        if dec20 not in ["y"]:
                                            print("Ohh invalid input, please enter 'y'")
                                        else:
                                            break
                                    if dec20=="y":
                                        print("\nThe lyrics of the selected song is: ")
                                        slyrics_hin=slyrics_generation_2_hin(sname_hin)
                                        print(slyrics_hin)
                                elif dec19=="n":
                                        continue
                            elif dec18=="n":
                                print("""\nExiting the program
See you later👋""")
                                break


                        #Copy to Clipboard(Hindi)
                        print("\nDo you want the lyrics to be copied to your clipboard?")
                        print("Press (Y/y) to continue or (N/n) to exit the program")
                        while True:
                            decision_1=input("\nEnter your decision: ").lower()
                            if decision_1 not in ["y","n"]:
                                print("Ohh invalid input, please enter 'y' or 'n' according to your needs")
                            else:
                                break
                        if decision_1=="y":
                            slyrics_hin_copy(slyrics_hin)
                            print("Thank You for using the program😊")
                            break
                        elif decision_1=="n":
                            print(""""\nExiting the program
See you later👋""")
                            break    
                    elif dec16=="n":
                        continue
        elif dec6=="n":
            print("""\nExiting the program
See you later👋""")
connection.close()
```

# Optional Adjustments
Currently the database has only 20 songs but you can use any another database with more songs and connect that to the script. Just make sure that the databse file is of sqlite. Also update the SQL commands in the script according to the columns of your table which is in the database file you wish to use. The updation must be done in the script for all the custom functions as all of them use SQL commands corresponding to the database I created.

Otherwise you can add more songs in the database manually by using the necessary SQL commands.
