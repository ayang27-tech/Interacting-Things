let circle1, circle2;
let speed1, speed2;
let originalColor1, originalColor2;
let touchedColor;

function setup() {
  createCanvas(400, 400);
  resetCircles();
}

function draw() {
  background(220);
  
  // Move the circles
  circle1.x += speed1.x;
  circle1.y += speed1.y;
  circle2.x += speed2.x;
  circle2.y += speed2.y;
  
  // Check if circles touch each other
  if (dist(circle1.x, circle1.y, circle2.x, circle2.y) <= circle1.d / 2 + circle2.d / 2) {
    fill(touchedColor);
    speed1.x *= -1; // Reverse direction of both circles
    speed1.y *= -1;
    speed2.x *= -1;
    speed2.y *= -1;
  } else {
    fill(originalColor1);
  }
  ellipse(circle1.x, circle1.y, circle1.d);
  
  fill(originalColor2);
  ellipse(circle2.x, circle2.y, circle2.d);

  // Check for canvas boundary collision
  if (circle1.x < 0 || circle1.x > width) speed1.x *= -1;
  if (circle1.y < 0 || circle1.y > height) speed1.y *= -1;
  if (circle2.x < 0 || circle2.x > width) speed2.x *= -1;
  if (circle2.y < 0 || circle2.y > height) speed2.y *= -1;
}

function resetCircles() {
  circle1 = { x: 100, y: 200, d: 50 };
  circle2 = { x: 300, y: 200, d: 50 };
  
  speed1 = createVector(random(1, 3), random(1, 3));
  speed2 = createVector(random(1, 3), random(1, 3));
  
  originalColor1 = color(255, 0, 0);
  originalColor2 = color(0, 0, 255);
  touchedColor = color(0, 255, 0);
}

function keyPressed() {
  if (key === 'r' || key === 'R') {
    resetCircles();
  }
}
