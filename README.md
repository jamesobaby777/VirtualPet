import processing.serial.*;
import cc.arduino.*;

Arduino arduino;
int leftButton = 0;
int rightButton = 0;

void setup() {
  size(1000, 1000);
  arduino = new Arduino(this, Arduino.list()[0], 57600); // change the [0] to a [1] or [2] etc. if your program doesn't work
}

void draw() {
  background(192);

  // Read button states
  leftButton = arduino.analogRead(1); // Left button
  rightButton = arduino.analogRead(6); // Right button
  
  // Pet's mood and color
  fill(255, 255, 0); // Default color of the pet (yellow face)
  ellipse(500, 500, 300, 300); // Draw pet's face
  
  // Eyes
  fill(0);
  ellipse(425, 425, 50, 50); // Left eye
  ellipse(575, 425, 50, 50); // Right eye
  
  // Determine mood based on button presses
  if (leftButton <= 500 && rightButton <= 500) {
    // Both buttons not pressed
    fill(0);
    ellipse(425, 425, 20, 20); // Left eye (happy face)
    ellipse(575, 425, 20, 20); // Right eye (happy face)
    stroke(0);
    noFill();
    arc(500, 550, 100, 100, 0, PI); // Happy mouth
  } else if (leftButton <= 500) {
    // Only left button pressed
    fill(0);
    ellipse(425, 425, 20, 20); // Left eye (happy face)
    fill(255, 0, 0);
    ellipse(575, 425, 20, 20); // Right eye (sad face)
    stroke(0);
    noFill();
    arc(500, 550, 100, 100, PI, 0); // Sad mouth
  } else if (rightButton <= 500) {
    // Only right button pressed
    fill(255, 0, 0);
    ellipse(425, 425, 20, 20); // Left eye (sad face)
    fill(0);
    ellipse(575, 425, 20, 20); // Right eye (happy face)
    stroke(0);
    noFill();
    arc(500, 550, 100, 100, PI, 0); // Sad mouth
  } else {
    // Both buttons pressed
    fill(255, 0, 0);
    ellipse(425, 425, 20, 20); // Both eyes (angry face)
    ellipse(575, 425, 20, 20); // Both eyes (angry face)
    stroke(0);
    noFill();
    arc(500, 550, 100, 100, PI/4, 3*PI/4); // Angry mouth
  }
}
