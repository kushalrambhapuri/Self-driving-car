# Build Your Own Self-Driving Car with Python!
Want to create a self-driving car simulation? With just 60 lines of Python, you can design a virtual car that navigates left, right, and forward on a track. Here's how you can do it using Pygame.

Requirements
Python Installed on your computer
Pygame Library (Install it using pip install pygame)
A track image (track6.png) and a car image (tesla.png)
Step-by-Step Guide
Step 1: Install Pygame
Open your terminal or command prompt and run:

pip install pygame  
Step 2: Prepare the Files
Place the track image (track6.png) and car image (tesla.png) in the same directory as your script. These will be used for the background and car visualization.

Step 3: The Python Code
Here's the full code:

import pygame  

Initialize Pygame  
pygame.init()  

Set up the display  
window = pygame.display.set_mode((1200, 400))  

Load images  
track = pygame.image.load('track6.png')  
car = pygame.image.load('tesla.png')  
car = pygame.transform.scale(car, (30, 60))  

Initial positions and offsets  
car_x, car_y = 155, 300  
focal_dis = 25  
cam_x_offset, cam_y_offset = 0, 0  
direction = 'up'  
drive = True  

Clock for controlling frame rate  
clock = pygame.time.Clock()  

Main game loop  
while drive:  
    for event in pygame.event.get():  
        if event.type == pygame.QUIT:  
            drive = False  

    clock.tick(60)  

    # Camera logic  
    cam_x = car_x + cam_x_offset + 15  
    cam_y = car_y + cam_y_offset + 15  
    up_px = window.get_at((cam_x, cam_y - focal_dis))[0]  
    right_px = window.get_at((cam_x + focal_dis, cam_y))[0]  
    down_px = window.get_at((cam_x, cam_y + focal_dis))[0]  

    # Direction logic  
    if direction == 'up' and up_px != 255 and right_px == 255:  
        direction = 'right'  
        cam_x_offset = 30  
        car = pygame.transform.rotate(car, -90)  

    elif direction == 'right' and right_px != 255 and down_px == 255:  
        direction = 'down'  
        car_x += 30  
        cam_x_offset = 0  
        cam_y_offset = 30  
        car = pygame.transform.rotate(car, -90)  

    elif direction == 'down' and down_px != 255 and right_px == 255:  
        direction = 'right'  
        car_y += 30  
        cam_x_offset = 30  
        cam_y_offset = 0  
        car = pygame.transform.rotate(car, 90)  

    elif direction == 'right' and right_px != 255 and up_px == 255:  
        direction = 'up'  
        car_x += 30  
        cam_x_offset = 0  
        car = pygame.transform.rotate(car, 90)  

    # Car movement logic  
    if direction == 'up' and up_px == 255:  
        car_y -= 2  
    elif direction == 'right' and right_px == 255:  
        car_x += 2  
    elif direction == 'down' and down_px == 255:  
        car_y += 2  

    # Render track and car  
    window.blit(track, (0, 0))  
    window.blit(car, (car_x, car_y))  
    pygame.draw.circle(window, (0, 255, 0), (cam_x, cam_y), 5, 5)  

    # Update the display  
    pygame.display.update()  
Step 4: Run Your Simulation
Save the script as self_driving_car.py.
Run it using Python in your preferred editor (e.g., PyCharm).
Watch your virtual Tesla navigate the track on its own!
How It Works
Track and Car Loading: The track6.png serves as the road, and tesla.png is the car.
Sensors: The program uses "virtual sensors" (pixel checks) to detect the path ahead.
Automatic Navigation: Based on the detected pixels, the car adjusts its direction to stay on the track.
Notes
Ensure the track image has a distinct white path (RGB: 255,255,255).
Adjust car_x, car_y, and focal_dis for different tracks.
Enjoy coding your self-driving car simulation! 🚗
