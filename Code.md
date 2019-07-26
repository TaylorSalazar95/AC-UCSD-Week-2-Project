class Main: # The Main class prints the "hangman" with a new limb every time the user gets an incorrect answer
    game = Game()# Calls the game class
    game.__init__()# Initializes the game class
    missedLetters = []# A new letter is added every time a user guesses an incorrect letter
    guessedLetters = []# A new letter is added every time a user guesses a letter
    word = game.getWord()# Uses the game class' method to choose a word from the word list
    guessWord = game.getEmptyWord(word)# Creates a list of underlines that is the same length of the word
    win = False# Bool Value changes to true when every letter is correctly guessed
    cont = True# Constant variable that will stay true as long as the user has not won
    while (cont == True):# While loop which runs the game
        if (len(missedLetters) == 0):# None of the body appears at the beginning 
            print(" -------")
            print(" |     |")
            print(" |")
            print(" |")
            print(" |")
            print(" |")
            print(" |")
            print("===")
        elif (len(missedLetters) == 1):# The head appears after one incorrect leter guess
            print(" -------")
            print(" |     |")
            print(" |    (ツ) ")
            print(" |     ")
            print(" |     ")
            print(" |")
            print(" |")
            print("===")
        elif (len(missedLetters) == 2):# The torso appears after two incorrect letter guesses
            print(" -------")
            print(" |     |")
            print(" |    (ツ) ")
            print(" |     ||")
            print(" |     ||")
            print(" |")
            print(" |")
            print("===")
        elif (len(missedLetters) == 3):# One arm appears after three incorrect letter guesses
            print(" -------")
            print(" |     |")
            print(" |    (ツ) ")
            print(" |    \||")
            print(" |     ||")
            print(" |")
            print(" |")
            print("===")
        elif (len(missedLetters) == 4):# The oter arm appears after four incorrect letter guesses
            print(" -------")
            print(" |     |")
            print(" |    (ツ) ")
            print(" |    \\||/")
            print(" |     ||")
            print(" |")
            print(" |")
            print("===")
        elif (len(missedLetters) == 5):# One leg appears after five incorrect letter guesses
            print(" -------")
            print(" |     |")
            print(" |    (ツ) ")
            print(" |    \||/")
            print(" |     ||")
            print(" |    /  ")
            print(" |")
            print("===")
        else:                           # If more than 5 letters are incorrectly guessed, the whole "hangman" shows and the game ends
            print(" -------")
            print(" |     |")
            print(" |    (ツ) ")
            print(" |    \||/")
            print(" |     ||")
            print(" |    /  \\")
            print(" |")
            print("===")
            break
        print('Missed Letters ', end='')# Displays a list of missed letters the user has accumulated
        print(missedLetters)# Displays a list of missed letters the user has accumulated
        letter = game.guess(guessedLetters, guessWord, word)# Calls the guess method in the game class using the following parameters
        inWord = game.checkWord(letter, word)# Calls the checkWord method and then uses the following if statement
        if (inWord == True):# Runs only if the letter is in the word
            print(str(letter) + " is in the word!")# Prints a confirmation message
            for i in range(len(word)):# For loop in range of the length of the randomly chosen word
                if word[i].lower() == letter:# Checks if the lowercase version of the indexed letter is equal to the letter inputted by the user
                    if (i != 0):# Checks if the letter is not at the beginning of word
                        guessWord[i] = letter# The lowercase letter is correctly guessed
                    else:# Checks if the letter is at the beginning of the word
                        guessWord[i] = letter.upper()# Uses the uppercase version of the letter given because all of the words begin with capitals
            guessedLetters.append(letter)# Adds the letter to guessedLetters list
        else: # Runs if the letter is not in the word
            print(str(letter) + " is not in the word :(")# Prints a confirmation that the letter was guessed incorrectly
            missedLetters.append(letter)# Adds the incorrectly guessed letter to the missedLetters list
            guessedLetters.append(letter)# Adds the incorrectly guessed letter to the guessedLetters list
        win = game.checkWin(guessWord, word)# Checks if all letters in the word were correctly guessed
        if (win == True):# Checks if the letters are in the word
            cont = False# Changes the constant variable to false to end the loop
    if (win == True): #Checks if the user won
        print("Congratulations, the word was " + word + ". You won!!!")# Prints a confirmation statement that the user has won the game
    else: #Checks if the user lost
        print("You have been hanged. The word was " + word)# Prints a confirmation statement that the user lost


import random # Uses the random import to choose a random word from the wordList

class Game: # Class that generates the word and records if the input fits or doesn't fit in the word
    wordlist = []
    def __init__(self): # Function that has a list of words
        self.wordList = ['Eat', 'Crow' , 'Spin', 'Weather', 'Play', 'Black', 'Beat', 'Seat', 'Told', 'Face', 'Truck', 'Train', 'Mold', 'Bread', 'Phone', 'Eye', 'Share', 'Nose', 'Computer', 'Wire', 'Lanyard', 'Mouse', 'Cat', 'Headphones', 'Apple', 'Orange', 'Student', 'Teacher', 'Bad', 'Smell', 'Stench', 'Window', 'Leave', 'Breakfast', 'Late', 'Merge', 'Recursion', 'Email', 'Black', 'Marker', 'Cheat', 'StackOverflow', 'Fibonacci', 'Pascal', 'Array', 'Triangle', 'Bubble', 'Selection', 'Sort', 'Fort', 'Keyboard', 'Desk', 'Ceiling', 'Floor', 'While', 'Loop', 'Algorithm', 'List', 'Logic', 'Variable', 'Boolean', 'Function', 'Class', 'Method', 'Constructor', 'Binary', 'Decimal', 'String', 'Bounce', 'Jupyter', 'PyCharm', 'Independent', 'Clock', 'Potatoes', 'Toaster', 'Watch', 'Baseball', 'Soccer', 'Football', 'Basketball', 'Lacrosse', 'Television', 'Shirt', 'Shorts', 'Pants', 'Socks', 'Shoes', 'Dance', 'Sight', 'Dictionary', 'Thesaurus', 'Font', 'Append', 'Bold', 'Underline', 'Italic', 'YouTube', 'Instagram', 'Amazon', 'Twitter', 'Google', 'Revelle', 'Muir', 'Pines', 'Internet', 'Dragon', 'Follow', 'Chicago', 'Shell', 'Gas', 'Concentrate', 'Food'
    def getWord(self): # Function that picks a word from the word bank
        index = random.randint(0, len(self.wordList) - 1)
        return self.wordList[index]
    def getEmptyWord(self, word): # Function that creates a list filled with _
        emptyWord = [] #initializes list
        for i in range(len(word)): 
            emptyWord.append(" _ ") #appends _ onto the list
        return emptyWord #returns the new list
    def guess(self, guessedLetters, emptyWord, word): # function that detects the letter guessed by the user and determines whether or not it was already guessed
        cont = True
        for i in range(len(emptyWord)):
            print(emptyWord[i], end=' ') # prints the guessed word
        print()
        while cont == True: # While loop that runs if you still have guesses
            cont = False
            letter = input("Guess a letter: ") #takes in input for a letter
            for i in range(len(guessedLetters)): # For loop to check if the letter has been guessed already
                if (letter.lower() == guessedLetters[i].lower()): #Checks if the lowercase version of the letter is the same as the lowercase version of a letter that has already been guessed
                    print("Letter already guessed. Guess again")
                    cont = True # Lets you guess again if you have guessed the same letter twice
        return letter #returns the correct letter
    def checkWord(self, letter, word): # Function that checks if letter input is the same as a letter in the word generated
        for i in range(len(word)): #For loop to traverse the word
            if (word[i].lower() == letter): #checks if the letter is the same as each of the letters in the word
                return True #if that is the case, it returns true
        return False # If the letter is not in the word it returns false
    def checkWin(self, guessWord, word): # Checks if the user has guessed the whole word
        for i in range(len(word)): #Traverses the word comparing the letters in the guessed word to the letters in the word 
            if (guessWord[i].lower() != word[i].lower()): # If anything is different, it returns False
                return False
        return True #if nothing is different, it returns True
