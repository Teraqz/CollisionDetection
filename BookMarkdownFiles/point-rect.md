## POINT/RECTANGLE  
Checking for collision with circular objects is fairly easy, since it is the same distance from the center to the edge in every direction. Rectangles require a bit more complex algorithm.

Let's say we have a square:

	float rx = 10;	// x position
	float ry = 10;	// y position
	float rw = 30;	// width
	float rh = 30;	// height

To test if a point is inside the square, we have to test if:

	Is the point's X position to the RIGHT of the LEFT EDGE?
	Is the point's X position to the LEFT of the RIGHT EDGE?
	Is the point's Y position BELOW the TOP EDGE?
	Is the point's Y position ABOVE the BOTTOM EDGE?

If all of these are true, then the point is inside. Let's look at testing the left edge first:

	if (px >= rx) {
		// to the right of the left edge
	}

Pretty easy! If we want to check the right edge, we need to get the X position of that edge:

	float rightEdge = rx + rw;
	if (px <= rightEdge) {
		// to the left of the right edge
	}

Here's the full if statement. Note that we combine the addition into the statement, rather than create separate variables. This is more concise and may save processing on complex projects.
		
	if (px >= rx &&			// right of the left edge AND
		px <= rx + rw &&	// left of the right edge AND
		py >= ry &&			// below the top AND
		py <= py + rh) {	// above the bottom 
			return true;
	}
	return false;

If all the statements are true, then the point is inside the square. Note we can break our if statement into multiple lines, which makes it a little easier to read. This is personal preference, but we'll keep doing that here for the sake of clarity.

Here's a full example:

	float px = 0;      // point position (move with mouse)
	float py = 0;

	float sx = 200;    // square position
	float sy = 100;
	float sw = 200;    // and dimensions
	float sh = 200;


	void setup() {
	  size(600,400);
	  noCursor();
	  
	  strokeWeight(5);    // thicker stroke so points are easier to see
	}


	void draw() {
	  background(255);
	  
	  // update point to mouse coordinates
	  px = mouseX;
	  py = mouseY;
	  
	  // check for collision
	  // if hit, change rectangle color
	  boolean hit = pointRect(px,py, sx,sy,sw,sh);
	  if (hit) {
	    fill(255,150,0);
	  }
	  else {
	    fill(0,150,255);
	  }
	  noStroke();
	  rect(sx,sy, sw,sh);
	  
	  // draw the point
	  stroke(0);
	  point(px,py);  
	}


	// POINT/RECTANGLE
	boolean pointRect(float px, float py, float rx, float ry, float rw, float rh) {
	    
	  // is the point inside the rectangle's bounds?
	  if (px >= rx &&        // right of the left edge AND
	      px <= rx + rw &&   // left of the right edge AND
	      py >= ry &&        // below the top AND
	      py <= py + rh) {   // above the bottom 
	        return true;
	  }
	  return false;
	}