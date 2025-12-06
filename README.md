# CodeAlpha_Hangman-Game
import random

def hangman():
    # 1. Predefined list of 5 words
    words = ["python", "coding", "intern", "project", "script"]
    
    # 2. Randomly choose one word
    secret_word = random.choice(words)
    
    # 3. Game state variables
    guessed_letters = set()            # letters the player has already guessed
    correct_letters = set(secret_word) # unique letters in the word
    attempts_left = 6                  # maximum incorrect guesses
    
    print("====== Welcome to Hangman Game ======")
    print("Guess the word, one letter at a time.")
    print(f"You have {attempts_left} incorrect attempts.\n")
    
    # Main game loop
    while attempts_left > 0:
        # Show current progress: _ for not-guessed letters
        display_word = ""
        for ch in secret_word:
            if ch in guessed_letters:
                display_word += ch + " "
            else:
                display_word += "_ "
        
        print("Word: ", display_word.strip())
        print("Guessed letters:", " ".join(sorted(guessed_letters)) if guessed_letters else "None")
        print(f"Attempts left: {attempts_left}")
        
        # Take user input
        guess = input("Enter a letter: ").lower().strip()
        
        # Input validation
        if len(guess) != 1 or not guess.isalpha():
            print("Please enter a single alphabet letter.\n")
            continue
        
        if guess in guessed_letters:
            print("You already guessed that letter. Try another one.\n")
            continue
        
        # Add guess to guessed letters
        guessed_letters.add(guess)
        
        # Check if guess is correct
        if guess in correct_letters:
            print("✅ Good guess!\n")
            
            # Check if all letters are guessed
            if correct_letters.issubset(guessed_letters):
                print("🎉 Congratulations! You guessed the word correctly!")
                print(f"The word was: {secret_word}")
                break
        else:
            attempts_left -= 1
            print("❌ Wrong guess.\n")
            
            if attempts_left == 0:
                print("😢 Game Over! You ran out of attempts.")
                print(f"The word was: {secret_word}")
                break

if __name__ == "__main__":
    hangman()
