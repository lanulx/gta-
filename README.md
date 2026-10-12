
from ursina import *

app = Ursina()

# Ground
ground = Entity(
    model='plane',
    scale=100,
    color=color.green,
    collider='box'
)

# Player
player = Entity(
    model='cube',
    color=color.azure,
    scale=(1, 2, 1),
    position=(0, 1, 0),
    collider='box'
)

# Follow camera
camera.parent = player
camera.position = (0, 5, -12)
camera.rotation_x = 20

# City buildings
for x in range(-20, 21, 8):
    for z in range(5, 30, 8):
        Entity(
            model='cube',
            color=color.gray,
            scale=(4, 5 + (x % 3), 4),
            position=(x, 2.5, z),
            collider='box'
        )

# Simple car
car = Entity(
    model='cube',
    color=color.red,
    scale=(2, 1, 4),
    position=(4, 0.5, 0)
)

speed = 5

def update():
    player.x += (
        held_keys['d'] - held_keys['a']
    ) * speed * time.dt

    player.z += (
        held_keys['w'] - held_keys['s']
    ) * speed * time.dt

    if held_keys['space']:
        player.y = 1.5
    else:
        player.y = 1

    camera.position = player.position + Vec3(0, 5, -12)

app.run()
