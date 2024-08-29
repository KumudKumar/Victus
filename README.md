// Motor control pins
const int motor1Pin1 = 3; // IN1 on motor driver
const int motor1Pin2 = 4; // IN2 on motor driver
const int motor2Pin1 = 5; // IN3 on motor driver
const int motor2Pin2 = 6; // IN4 on motor driver

void setup() {
    // Set motor control pins as outputs
    pinMode(motor1Pin1, OUTPUT);
    pinMode(motor1Pin2, OUTPUT);
    pinMode(motor2Pin1, OUTPUT);
    pinMode(motor2Pin2, OUTPUT);

    // Initialize serial communication with Bluetooth module
    Serial.begin(9600); // Ensure this matches the baud rate of your Bluetooth module
}

void loop() {
    // Check if data is available from Bluetooth
    if (Serial.available()) {
        char command = Serial.read(); // Read the incoming data

        switch (command) {
            case 'F': // Forward
                moveForward();
                break;
            case 'B': // Backward
                moveBackward();
                break;
            case 'L': // Left
                turnLeft();
                break;
            case 'R': // Right
                turnRight();
                break;
            case 'S': // Stop
                stopMotors();
                break;
            default:
                stopMotors();
                break;
        }
    }
}

void moveForward() {
    digitalWrite(motor1Pin1, HIGH);
    digitalWrite(motor1Pin2, LOW);
    digitalWrite(motor2Pin1, HIGH);
    digitalWrite(motor2Pin2, LOW);
}

void moveBackward() {
    digitalWrite(motor1Pin1, LOW);
    digitalWrite(motor1Pin2, HIGH);
    digitalWrite(motor2Pin1, LOW);
    digitalWrite(motor2Pin2, HIGH);
}

void turnLeft() {
    digitalWrite(motor1Pin1, LOW);
    digitalWrite(motor1Pin2, HIGH);
    digitalWrite(motor2Pin1, HIGH);
    digitalWrite(motor2Pin2, LOW);
}

void turnRight() {
    digitalWrite(motor1Pin1, HIGH);
    digitalWrite(motor1Pin2, LOW);
    digitalWrite(motor2Pin1, LOW);
    digitalWrite(motor2Pin2, HIGH);
}

void stopMotors() {
    digitalWrite(motor1Pin1, LOW);
    digitalWrite(motor1Pin2, LOW);
    digitalWrite(motor2Pin1, LOW);
    digitalWrite(motor2Pin2, LOW);
}
