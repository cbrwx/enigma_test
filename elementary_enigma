import string
from collections import deque

class SimpleEnigma:
    def __init__(self, rotor_shifts, plugboard_pairs):
        self.alphabet = string.ascii_uppercase
        self.rotors = [self.shift_alphabet(shift) for shift in rotor_shifts]
        self.plugboard = self.create_plugboard(plugboard_pairs)

    def shift_alphabet(self, shift):
        return deque(self.alphabet[shift:] + self.alphabet[:shift])

    def create_plugboard(self, plugboard_pairs):
        plugboard = list(self.alphabet)
        for pair in plugboard_pairs:
            a, b = pair.upper()
            plugboard[self.alphabet.index(a)] = b
            plugboard[self.alphabet.index(b)] = a
        return plugboard

    def rotate_rotors(self):
        self.rotors[0].rotate(1)
        for i in range(1, len(self.rotors)):
            if self.rotors[i - 1][0] == self.alphabet[0]:
                self.rotors[i].rotate(1)
            else:
                break

    def process_char(self, char, encrypt=True):
        if char.upper() in self.alphabet:
            # Apply plugboard
            char = self.plugboard[self.alphabet.index(char.upper())]

            # Go through rotors (forward)
            index = self.alphabet.index(char)
            for rotor in self.rotors if encrypt else reversed(self.rotors):
                index = rotor.index(self.alphabet[index])

            # Go through rotors (backward)
            for rotor in reversed(self.rotors) if encrypt else self.rotors:
                index = self.alphabet.index(rotor[index])

            # Apply plugboard
            char = self.plugboard[index]
        return char

    def encrypt(self, text):
        return ''.join(self.process_char(c, encrypt=True) for c in (self.rotate_rotors() or text))

    def decrypt(self, text):
        return ''.join(self.process_char(c, encrypt=False) for c in (self.rotate_rotors() or text))

# Example usage:
rotor_shifts = [3, 5, 7]
plugboard_pairs = [('A', 'M'), ('F', 'L'), ('T', 'O')]

enigma = SimpleEnigma(rotor_shifts, plugboard_pairs)

plaintext = "Ich mag Schildkröten" # Attempt at Engima humor might be 70 years too late and 60 years too early
ciphertext = enigma.encrypt(plaintext)
decrypted_text = enigma.decrypt(ciphertext)

print("Plaintext:", plaintext)
print("Ciphertext:", ciphertext)
print("Decrypted text:", decrypted_text)
