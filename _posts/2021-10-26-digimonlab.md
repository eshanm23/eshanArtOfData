---
layout: post
title: Digimon Lab
subtitle: by Eshan Mehere
cover-img: /assets/img/download (1).jpeg
---


{def avgSpeed(filepath):
    d={
        "Total Speed": 0,
        "Number of Digimon": 0

    }
    with open(filepath, "r") as file:
        data = csv.DictReader(file)

        for row in data:

            d["Total Speed"]+= float(row["Spd"])
            d["Number of Digimon"] += 1
            d["Average"]= (d["Total Speed"])/(d["Number of Digimon"])
    return d
        
    
print(avgSpeed("datasets/digimon.csv"))
{'Total Speed': 29980.0, 'Number of Digimon': 249, 'Average': 120.40160642570281}
    }

The average speed of all Digimon is ~120.401. Above is the code I used to get this result. I basically thought of this problem in a similar manner to the Penguins Practice worksheet. I knew it could very easily be done with dictionaries. I knew my end result would be a dictionary with keys that show the total number of digimon in the dataset, and the total speed of all Digimon. And then I would want to have a third key that computes the average. This is similar to how I found the Total Bill Length and Total Number of Penguins for Penguins Practice. Now let's talk through our actual code. 

I first created a new dictionary "d" which I knew would be my final dictionary that held all of my important values. I defined d to have keys of total speed and number of digimon, and I knew that before running through the CSV, the value of these keys would be 0, so I set them to that. I could define my keys here because I knew I did not require any if statements to define keys of the dictionary (as seen in Penguins Practice). 

I then opened the file using DictReader, and looped through the CSV. For each row in the CSV I took the Speed (Spd) for that Digimon, turned it into a float so it could be manipulated arithmetically, and then added it to my total speed key in the dictionary d. I added 1 to the Number of Digimon key for each row in the CSV, because each row represents a new Digimon. Below this line, I also defined my average key, and very simply, my average was just Total Speed/Number of Digimon. I returned the dictionary, and then printed out the Average Speed function using the digimon dataset. Below the Print statement shows the Output in the Terminal for this method (the dictionary d, filled with values) . 

def count_digimon(key, value):
    with open("datasets/digimon.csv", "r") as file:
        data = csv.DictReader(file)
        match_trait = 0
        for row in data: 
            if row[key] == value:
                match_trait+=1
    return match_trait

print(count_digimon("Type", "Vaccine"))
70

There are 70 Digimon in this dataset with the type of "Vaccine." Above is the code I used to determine this. I figured out very quickly that you could more generally call keys and values of a dictionary using the terms "key" and "value." This created my roadmap for how to solve this problem. I was able to think of this solution relatively quickly, and utilizing the key and value terms was the first way I thought of this function. I will explain the actual code (and more of the process) next. 

I started by opening my data set. I used key and value as inputs for this function because I want this function to work for any attribute and any value, and so the user can choose which two they would like. I created a new variable match_trait that basically serves as what I use to count. I set that equal to zero since obviously nothing has been counted before I loop through the data. I then loop through the data, and essentially just add 1 whenever we come across a Digimon that has the desired attribute combo. After returning my count variable (which now houses a number that shows the number of Digimon that fit this attribute), I can just print out my function. It is important to note that the print statement is where I choose which attribute I would like to run this function for. In this case we are looking for how many Digimon have a type of Vaccine. This prints out 70 in the terminal, indicating that in our dataset of 249 Digimon, 70 have this attribute. 

def createTeam():
    with open("datasets/digimon.csv", "r") as file:
        data = list(csv.DictReader(file))
    
    for row1 in data:
        for row2 in data:
            for row3 in data:
                if (float(row1["Memory"])+ float(row2["Memory"])+ float(row3["Memory"]))<=15 and (float(row1["Atk"])+float(row2["Atk"])+float(row3["Atk"]))>=300 and row1!=row2!=row3:
                    return(row1["Digimon"], row2["Digimon"], row3["Digimon"])
    
print(createTeam())
('Kuramon', 'Pabumon', 'Ogremon')

"Kuramon," "Pabumon," and "Ogremon" are a team of three Digimon that fit this criteria. There are several other combinations that match this criteria. The code for determining this shown above. I knew right from the get go that I would need to use a triple nested for loop because I needed 3 Digimon for this to work. I also knew that I would have to manually enter the conditions that are required to be fulfilled. The actual code will be explained below.

I started by defining the function, and I knew the function would not require any inputs because there were not any specific cases we had to account for. I opened the file and used the DictReader because I knew the CSV had to be manipulated as such. I ran the triple nested for loop which is essentially a for loop, but runs through every 3 row combination in the CSV instead of every row. I then inputted my conditions. I knew that the memory of these three Digimon had to be less than 15, so I indicated that in the first part of the if statement, turning the strings into floats so they could be manipulated arithemtically. I also knew that they needed to have Attack (Atk) of at least 300 in order to be considered a viable team, and so I indicated that in the second part of the if statement. I once again turned the Atk strings into floats so that they could be manipulated arithmetically. Finally, I also knew that a viable team could not consist of repeated Digimon so I had to indicate that the three Digimon were all distinct; this was done in the last part of the if statement. Finally, I returned the Digimon (name) of the three rows that matched the criteria and printed the function out.  


