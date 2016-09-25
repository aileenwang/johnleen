# 6.00 Problem Set 3
# 
# Hangman
#


# -----------------------------------
# Helper code
# (you don't need to understand this helper code)
import random
import string

WORDLIST_FILENAME = "words.txt"

def load_words():
    """
    Returns a list of valid words. Words are strings of lowercase letters.
    
    Depending on the size of the word list, this function may
    take a while to finish.
    """
    print "Loading word list from file..."
    # inFile: file
    inFile = open(WORDLIST_FILENAME, 'r', 0)
    # line: string
    line = inFile.readline()
    # wordlist: list of strings
    wordlist = string.split(line)
    print "  ", len(wordlist), "words loaded."
    return wordlist

def choose_word(wordlist):
    """
    wordlist (list): list of words (strings)

    Returns a word from wordlist at random
    """
    return random.choice(wordlist)

# end of helper code
# -----------------------------------

## actually load the dictionary of words and point to it with 
## the wordlist variable so that it can be accessed from anywhere
## in the program
wordlist = load_words()

## your code begins here!

word = choose_word(wordlist)

print "Welcome to the game, Hangman!"
print "I am thinking of a word that is", len(word), "letters long."
print "-----------"

## return: guesses left, available letters of alphabet, raw input, y/n

guesses_left = 20
letters_left = ["a","b","c","d","e","f","g","h","i","j","k","l","m","n","o","p","q","r","s","t","u","v","w","x","y","z"]

so_far = "_" * len(word)
so_far = list(so_far)
print so_far

# while - there are guesses left and not all letters are found
while guesses_left > so_far.count("_") and so_far.index("_") > -1:
    print "You have", guesses_left, "guesses left."
    print "Available letters: ", letters_left
    guess = raw_input("Please guess a letter: ")

    guesses_left -= 1

    index_alphabet = letters_left.index(guess)
    letters_left.pop(index_alphabet)

    if word.find(guess) is not -1:
        index_word = word.index(guess)
        so_far[index_word] = guess
        print "Good guess: ", str(so_far)
    
    else:
        print "Oops! That letter is not in my word:", str(so_far)

    print word

    print "---------------"

if so_far.index("_") is not -1:
    print "Congratulations, you won!"

else:
    print "u idiot"
    print "The word was: ", word

# neaten up while thing 
