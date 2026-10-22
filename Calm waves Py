# ============================================================
# CALM WAVES
# Interactive Generative Digital Artwork
# ============================================================

# ------------------------------------------------------------
# GLOBAL VARIABLES
# ------------------------------------------------------------

wave_offset = 0.0
colour_offset = 0.0

# Store all particles
particles = []

# Number of waves
NUMBER_OF_WAVES = 7


# ------------------------------------------------------------
# SETUP
# Runs once when the program starts
# ------------------------------------------------------------

def setup():

    global particles

    # Canvas
    size(1000, 700)

    # Smooth shapes
    smooth()

    # Use RGB colours
    colorMode(RGB, 255)

    # Create starting particles
    for i in range(100):

        particles.append(
            Particle(
                random(width),
                random(height)
            )
        )


# ------------------------------------------------------------
# DRAW
# Runs continuously
# ------------------------------------------------------------

def draw():

    global wave_offset
    global colour_offset

    # --------------------------------------------------------
    # SOFT BACKGROUND
    # --------------------------------------------------------

    # Slightly transparent background creates a soft trail
    noStroke()
    fill(225, 242, 244, 25)
    rect(0, 0, width, height)


    # --------------------------------------------------------
    # MOUSE INTERACTION
    # --------------------------------------------------------

    # Mouse X controls the speed of the waves
    mouse_speed = map(
        mouseX,
        0,
        width,
        0.5,
        2.0
    )

    # Mouse Y controls the height of the waves
    mouse_height = map(
        mouseY,
        0,
        height,
        25,
        80
    )


    # --------------------------------------------------------
    # DRAW THE WAVES
    # --------------------------------------------------------

    for wave in range(NUMBER_OF_WAVES):

        # Position of each wave
        base_y = 180 + wave * 75

        # Slight variation between waves
        wave_height = mouse_height + wave * 5

        # Different colours for each wave
        red_value = 90 + wave * 8
        green_value = 175 + wave * 5
        blue_value = 190 + wave * 6

        stroke(
            red_value,
            green_value,
            blue_value,
            150
        )

        strokeWeight(2)

        noFill()

        beginShape()

        # Draw the wave from left to right
        for x in range(0, width + 10, 10):

            # Main flowing movement
            y = base_y

            y += sin(
                x * 0.015
                + wave_offset * mouse_speed
                + wave * 0.7
            ) * wave_height


            # ------------------------------------------------
            # MOUSE EFFECT
            # ------------------------------------------------

            # Distance between the wave point and mouse
            distance = abs(x - mouseX)

            # Only affect the wave when mouse is nearby
            if distance < 220:

                mouse_effect = (
                    220 - distance
                ) / 220.0

                # Bend the wave around the mouse
                y += sin(
                    x * 0.025
                    + wave_offset
                ) * mouse_effect * 70


            # Add the point to the wave
            vertex(x, y)

        endShape()


    # --------------------------------------------------------
    # UPDATE WAVE ANIMATION
    # --------------------------------------------------------

    wave_offset += 0.018

    colour_offset += 0.5


    # --------------------------------------------------------
    # PARTICLES
    # --------------------------------------------------------

    for particle in particles:

        particle.update()
        particle.display()


# ============================================================
# PARTICLE CLASS
# ============================================================

class Particle:

    def __init__(self, x, y):

        # Position
        self.x = x
        self.y = y

        # Movement
        self.speed_x = random(-0.4, 0.4)
        self.speed_y = random(-0.3, 0.3)

        # Size
        self.size = random(2, 5)

        # Transparency
        self.alpha = random(30, 100)


    # --------------------------------------------------------
    # UPDATE PARTICLE
    # --------------------------------------------------------

    def update(self):

        # Move particle
        self.x += self.speed_x
        self.y += self.speed_y


        # ----------------------------------------------------
        # MOUSE INTERACTION
        # ----------------------------------------------------

        distance = dist(
            self.x,
            self.y,
            mouseX,
            mouseY
        )

        # Particles react when mouse gets close
        if distance < 150:

            force = (
                150 - distance
            ) / 150.0

            # Move particle away from mouse
            if self.x < mouseX:
                self.x -= force * 1.5
            else:
                self.x += force * 1.5

            if self.y < mouseY:
                self.y -= force * 1.5
            else:
                self.y += force * 1.5


        # ----------------------------------------------------
        # WRAP PARTICLES AROUND SCREEN
        # ----------------------------------------------------

        if self.x < 0:
            self.x = width

        if self.x > width:
            self.x = 0

        if self.y < 0:
            self.y = height

        if self.y > height:
            self.y = 0


    # --------------------------------------------------------
    # DISPLAY PARTICLE
    # --------------------------------------------------------

    def display(self):

        noStroke()

        fill(
            170,
            210,
            215,
            self.alpha
        )

        ellipse(
            self.x,
            self.y,
            self.size,
            self.size
        )


# ============================================================
# MOUSE PRESSED
# ============================================================

def mousePressed():

    # Create a small burst of particles
    for i in range(15):

        particles.append(
            Particle(
                mouseX + random(-25, 25),
                mouseY + random(-25, 25)
            )
        )
