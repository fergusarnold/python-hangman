"# python-hangman" 
"""
Created on Thu Jun  4 15:30:45 2020

@author: User
"""

import random

#Picture of hanging man

HANGMANPICTURE =[''' 
   +---+
   |   |
       |
       |
       |
       |
 =========''', '''
   +---+
   |   |
   O   |
       |
       |
       |
 =========''', '''
   +---+
   |   |
   O   |
   |   |
       |
       |
=========''', '''

   +---+
   |   |
   O   |
  /|   |
       |
       |
 =========''', '''
   +---+
   |   |
   O   |
  /|\  |
       |
       |
 =========''', '''
   +---+
   |   |
   O   |
  /|\  |
  /    |
       |
=========''', '''
   +---+
   |   |
   O   |
  /|\  |
  / \  |
       |
=========''']

words = 'fergus pyton snake canada river mountain tree brad dana'.split()

## set up functions
#random word generator

def word_generator(words):
   wordindex = random.randint(0,len(words)-1)
   correct_word = words[wordindex]
   return correct_word    

#display board
def display_board(HANGMANPICTURE, missedletters, correctletters, secretword):
    print(HANGMANPICTURE[len(missedletters)])
    print('The word has '+ str(len(secretword)) + ' letters, total')
    print('Missed Letters: '+ missedletters)
    blanks = '_' * len(secretword)
    for i in range(len(blanks)):
        if secretword[i] in correctletters:
            blanks = blanks[:i] + secretword[i] + blanks[i+1:]
    print(blanks)
            
#guess rules
def recieve_guess(already_guessed):
    while True:
        guess = input('Guess the letter: ').lower()
        if len(guess) != 1:
            print('Please only submit one letter')
        elif guess in already_guessed:
            print('You\'ve already guessed that letter')
        elif guess not in ('abcdefghijklmnopqrstuvwxyz' or 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'):
            print('You must use a lower-case alphabetic letter')
        else:
            return guess

#play again
def play_again():
    return input('Would you like to play HANGMAN again?:').lower().startswith('y')

## take stock of variables
#letters used in functions: missedletters, correctletters, secretword, already_guessed)

missedletters = ''
correctletters = ''
secretword = word_generator(words)
already_guessed = ''
game_is_done = False


while True:
    display_board(HANGMANPICTURE, missedletters, correctletters, secretword)
    guess = recieve_guess(correctletters + missedletters)
    if guess in secretword:
        correctletters = correctletters + guess
        foundAllLetters = True
        for i in range(len(secretword)):
            if secretword[i] not in correctletters:
                foundAllLetters = False
                break
        if foundAllLetters:
            print('Congradulations! You\'ve done it!')
            game_is_done = True
    else:
        missedletters = missedletters + guess
        if len(missedletters) == len(HANGMANPICTURE) - 1:
            display_board(HANGMANPICTURE, missedletters, correctletters, secretword)
            print('\n You\'ve let someone die today! \n')
            game_is_done = True
    if game_is_done:
        if play_again():
            missedletters = ''
            correctletters = ''
            secretword = word_generator(words)
            already_guessed = ''
            game_is_done = False
        else:
            break
    

    

    
