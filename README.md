# High-level approach:
This is a socket client program in python that communicates with a server to play Wordle. It first establishes a connection to the server with the provided host name and username, and additional constraints such as port number or if TLS encrtypted connection is required.\
It starts the game with sending a hello message with username. The server responds with a message with an id. The client then sends a guess message with a word from a provided word list and the id. The server will send back either a message of type "bye" or "retry". If the type is "bye", this means that the guess is correct. The program prints the flag in the respond from server and closes the connection. If the type is "retry", this means that the guess was incorrect and the client should send another guess message with a new word. An algorithm checks for marks responded by the server and removes words that do not satisfy the marks from the word list. This shrinks the size of possible guesses and makes the guessing process more efficient.

# Challenges faced:
The first challenge I faced was understanding the project. I had little knowledge about networks, so I did some research on sockets and followed the python socket tutorial.\
Another challenge I faced was I didn't know 2 supercedes 1 in marks. This caused words that have duplicate letters, while one of them is at the correct position, to be removed from the list. This sometimes results in elimination of the answer word and thus the program runs out of words to guess without finding the right answer. After reading the related questions on Piazza, I modified my elimination algorithm, which prevents words that have letters marked 0 that are marked 1 or 2 elsewhere to be removed from list.

# Guessing strategy:
My guessing strategy is to guess the words in the word list one by one while removing words that don't satisfy the marks in previous guess result.
Everytime after sending a guess, the program removes the words that do not satisfy the marks in previous guess result by calling `modify_words`.

## How `modify_words` works:
We take care of the cases when a letter is marked 1 and 2 first, since if a 2 is received for a given letter in a given position, a 1 will not be received for that letter in other positions, even if that letter appears in the word multiple times.

We first go through the marks array once:\
If a letter is marked 1:\
This means the answer contains this letter but not at this position. Remove all words that do not have this letter form the word list.

If a letter is marked 2:\
This means the letter appears in the answer at the exact position. Remove all words that do not have this letter at this position from the word list.

Then go through the marks array again:\
If a letter is marked 0 and is not marked 2 or 1 elsewhere:\
This means the answer does not contain this letter. Remove all words that has this letter form the word list. 

Repeat the above guessing+removing words process untill the answer is found.

# Testing Strategy:
I tested the program with all possible command line input combinations to make sure all possible cases are covered. I also checked if the two flags are different so I know if the TLS connection is working. To test the guessing algorithm, I printed out the guessing process to make sure the word list modifying function is working properly.