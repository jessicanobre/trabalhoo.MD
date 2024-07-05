int soma = 13; // Control pin for the addition operation
int carryBit = 0; // Variable to store the carry bit
int nib1a, nib1b, nib1c, nib1d = 0; // Variables to store the bits of the first 4-bit number
int nib2a, nib2b, nib2c, nib2d = 0; // Variables to store the bits of the second 4-bit number
int res1a, res1b, res1c, res1d = 0; // Variables to store the result bits of the addition

void setup() {

    // Configure digital pins for inputs and outputs

    pinMode(0, INPUT); // Input bit 1 of the first number
    pinMode(1, INPUT); // Input bit 2 of the first number
    pinMode(2, INPUT); // Input bit 3 of the first number
    pinMode(3, INPUT); // Input bit 4 of the first number
    pinMode(4, INPUT); // Input bit 1 of the second number
    pinMode(5, INPUT); // Input bit 2 of the second number
    pinMode(6, INPUT); // Input bit 3 of the second number
    pinMode(7, INPUT); // Input bit 4 of the second number
    pinMode(8, OUTPUT); // Output bit 1 of the result
    pinMode(9, OUTPUT); // Output bit 2 of the result
    pinMode(10, OUTPUT); // Output bit 3 of the result
    pinMode(11, OUTPUT); // Output bit 4 of the result
    pinMode(12, OUTPUT); // Output carry bit
    pinMode(13, INPUT); // Input control for the addition operation
}

// Function to sum two bits and a carry bit
int somaBit(int b1a, int b2a, int cBit) {
    // Logic for a full adder
    return (b1a ^ b2a) ^ cBit; // Sum of bits including carry-in
}

// Function to calculate the carry bit
int somaCarryBit(int b1a, int b2a, int cBit) {
    // Logic for a full adder carry-out
    return (b1a && b2a) || (b1a && cBit) || (b2a && cBit); // Carry-out logic
}

void loop() {
    
    soma = digitalRead(13); // Read the control signal
    // Read the bits of the first 4-bit number
    nib1a = digitalRead(0);
    nib1b = digitalRead(1);
    nib1c = digitalRead(2);
    nib1d = digitalRead(3);

    // Read the bits of the second 4-bit number
    nib2a = digitalRead(4);
    nib2b = digitalRead(5);
    nib2c = digitalRead(6);
    nib2d = digitalRead(7);

    if (soma == 1) { // If the control signal is active
        carryBit = 0; // Initialize carry bit

        // Calculate the sum and carry for each bit

        res1a = somaBit(nib1a, nib2a, carryBit);
        carryBit = somaCarryBit(nib1a, nib2a, carryBit);
        res1b = somaBit(nib1b, nib2b, carryBit);
        carryBit = somaCarryBit(nib1b, nib2b, carryBit);
        res1c = somaBit(nib1c, nib2c, carryBit);
        carryBit = somaCarryBit(nib1c, nib2c, carryBit);
        res1d = somaBit(nib1d, nib2d, carryBit);
        carryBit = somaCarryBit(nib1d, nib2d, carryBit);
    }

    // Output the result bits and carry bit

    digitalWrite(8, res1a);
    digitalWrite(9, res1b);
    digitalWrite(10, res1c);
    digitalWrite(11, res1d);
    digitalWrite(12, carryBit);
}
