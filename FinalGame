import arcade

Width = 1000
Height = 650
title = "Dungeon Crawl"
Character_Scaling = 1
Character_Movement = 5
Character_Jump = 20
Gravity = 1
Tile_Scaling = .5
Coin_Scaling = .5
Font_Size = 20

class MyGame(arcade.Window):

    def __init__(self):
        super().__init__(Width, Height, title)
        self.scene = None
        self.player_sprite = None
        self.physics_engine = None
        self.camera = None
        self.gui_camera = None
        self.score = 0
        arcade.set_background_color(arcade.color.STORMCLOUD)
        self.collect_coin_sound = arcade.load_sound(":resources:sounds/coin1.wav")
        self.jump_sound = arcade.load_sound(":resources:sounds/jump1.wav")
    
    def setup(self):
        self.camera = arcade.Camera(Width, Height)
        self.gui_camera = arcade.Camera(self.width, self.height)
        self.score = 0
        self.scene = arcade.Scene()
        self.scene.add_sprite_list("Player")
        self.scene.add_sprite_list("Walls", use_spatial_hash=True)
        image_source = ":resources:images/animated_characters/female_adventurer/femaleAdventurer_idle.png"
        self.player_sprite = arcade.Sprite(image_source, Character_Scaling)
        #self.player_sprite.center_x = 64
        #self.player_sprite.center_x = 128 
        self.player_sprite.center_x = 250
        self.player_sprite.center_y = 1450
        self.scene.add_sprite("Player", self.player_sprite)
        for x in range(0,1280,64):
            wall = arcade.Sprite(":resources:images/tiles/stoneCenter.png",Tile_Scaling)
            wall.center_x = x
            wall.center_y = 32
            self.scene.add_sprite("Walls", wall)
        for x in range(0,1216,64):
            wall = arcade.Sprite(":resources:images/tiles/stoneCenter.png",Tile_Scaling)
            wall.center_x = x
            wall.center_y = 532
            self.scene.add_sprite("Walls", wall)
        for y in range(0,1408,64):
            wall = arcade.Sprite(":resources:images/tiles/stoneCenter.png",Tile_Scaling)
            wall.center_x = 0
            wall.center_y = y
            self.scene.add_sprite("Walls", wall)
        coordinate_list_1 = [[1408,182],[1344,365]]
        for coordinate in coordinate_list_1:
            wall = arcade.Sprite(":resources:images/tiles/stoneCenter.png",Tile_Scaling)
            wall.position = coordinate
            self.scene.add_sprite("Walls", wall)
        coordinate_list_2 = [[512,96], [256, 96], [768, 96]]
        for coordinate in coordinate_list_2:
            wall = arcade.Sprite(":resources:images/tiles/boxCrate_double.png",Tile_Scaling)
            wall.position = coordinate
            self.scene.add_sprite("Walls", wall)
        self.physics_engine = arcade.PhysicsEnginePlatformer(self.player_sprite, gravity_constant=Gravity, walls=self.scene["Walls"])
        coordinate_list_3 = [[64,700],[192,875], [64,1050],[192,1225]]
        for coordinate in coordinate_list_3:
            wall = arcade.Sprite(":resources:images/tiles/stoneCenter.png",Tile_Scaling)
            wall.position = coordinate
            self.scene.add_sprite("Walls", wall)
        for x in range (256,1506,64):
            wall = arcade.Sprite(":resources:images/tiles/stoneCenter.png",Tile_Scaling)
            wall.center_x = x
            wall.center_y = 768
            self.scene.add_sprite("Walls", wall)
        for y in range (0,768,64):
            wall = arcade.Sprite(":resources:images/tiles/stoneCenter.png",Tile_Scaling)
            wall.center_x = 1472
            wall.center_y = y
            self.scene.add_sprite("Walls", wall)
        for y in range (768,1408,64):
            wall = arcade.Sprite(":resources:images/tiles/stoneCenter.png",Tile_Scaling)
            wall.center_x = 256
            wall.center_y = y
            self.scene.add_sprite("Walls", wall)
        for x in range (256,1536,64):
            wall = arcade.Sprite(":resources:images/tiles/stoneCenter.png",Tile_Scaling)
            wall.center_x = x
            wall.center_y = 1216
            self.scene.add_sprite("Walls", wall)
        for y in range(1280,1408,64):
            for x in range(320,1472,64):
                lava = arcade.Sprite(":resources:images/tiles/lava.png",Tile_Scaling)
                lava.center_x = x
                lava.center_y = y
                self.scene.add_sprite("Lava", lava)
        for y in range(1280,1408,64):
            wall = arcade.Sprite(":resources:images/tiles/stoneCenter.png",Tile_Scaling)
            wall.center_x = 1472
            wall.center_y = y
            self.scene.add_sprite("Walls", wall)
        coordinate_list_4 = [[384,1472], [640,1408],[704,1600], [896,1664],[1152,1408], [1216,1408]]
        for coordinate in coordinate_list_4:
            wall = arcade.Sprite(":resources:images/tiles/stoneCenter.png",Tile_Scaling)
            wall.position = coordinate
            self.scene.add_sprite("Walls", wall)
        for x in range(128, 1250, 256):
            coin = arcade.Sprite(":resources:images/items/coinGold.png", Coin_Scaling)
            coin.center_x = x
            coin.center_y = 96
            self.scene.add_sprite("Coins", coin)
        Flag = arcade.Sprite(":resources:images/items/flagGreen2.png", Tile_Scaling)
        Flag.center_x = 1216
        Flag.center_y = 832
        self.scene.add_sprite("Finish", Flag)
                   

    def on_draw(self):
        arcade.start_render()
        self.camera.use()
        self.scene.draw()
        self.gui_camera.use()
        score_text = f"Score: {self.score}"
        arcade.draw_text(
            score_text,
            10,
            10,
            arcade.csscolor.WHITE,
            18,
        )
        #if self.finish == True:
        #    arcade.draw_text("YOU WIN!!!",832,1216,arcade.color.RED,Font_Size*5,width=Width, align="center")
    
    def on_key_press(self,key,modifiers):
        if key == arcade.key.UP or key == arcade.key.W:
            if self.physics_engine.can_jump():
                self.player_sprite.change_y = Character_Jump
                arcade.play_sound(self.jump_sound)
        elif key == arcade.key.LEFT or key == arcade.key.A:
            self.player_sprite.change_x = -Character_Movement
        elif key == arcade.key.RIGHT or key == arcade.key.D:
            self.player_sprite.change_x = Character_Movement

    def on_key_release(self, key, modifiers):
        if key == arcade.key.LEFT or key == arcade.key.A:
            self.player_sprite.change_x = 0
        elif key == arcade.key.RIGHT or key == arcade.key.D:
            self.player_sprite.change_x = 0

    def Center_Camera_to_Player(self):
        screen_center_x = self.player_sprite.center_x-(self.camera.viewport_width/2)
        screen_center_y = self.player_sprite.center_y-(self.camera.viewport_height/2)
        if screen_center_x < 0:
            screen_center_x = 0
        if screen_center_y < 0:
            screen_center_y = 0
        player_centered = screen_center_x, screen_center_y
        self.camera.move_to(player_centered)
    
    def on_update(self, delta_time):
        self.physics_engine.update()
        self.Center_Camera_to_Player()
        coin_hit_list = arcade.check_for_collision_with_list(
            self.player_sprite, self.scene["Coins"]
        )
        for coin in coin_hit_list:
            coin.remove_from_sprite_lists()
            arcade.play_sound(self.collect_coin_sound)
            self.score += 1
        if self.player_sprite.center_y <= 0:
            if self.player_sprite.center_x < 1250:
                self.player_sprite.center_x = 64
                self.player_sprite.center_y = 128
            else:
                self.player_sprite.center_y = 650
                self.player_sprite.center_x = 180
        if self.player_sprite.center_x < 0:
            self.player_sprite.center_x = 180
            self.player_sprite.center_y = 650
        if self.player_sprite.center_y >= 1280 and self.player_sprite.center_y <= 1408:
            if self.player_sprite.center_x >= 320 and self.player_sprite.center_x <=1472:
                self.player_sprite.center_x = 180
                self.player_sprite.center_y = 650
        #if self.player_sprite.center_y >= 1184 and self.player_sprite.center_y <= 1248:
        #    if self.player_sprite.center_x == 864:
        #        self.finish = True
                

def main():
    window = MyGame()
    window.setup()
    arcade.run()

if __name__ == "__main__":
    main()
