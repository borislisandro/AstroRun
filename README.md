### JavaProcessing_AstroRun
Java Processing Astrorun Indie Game


  This game is an example of what a small amount of time, 3 heads and some creativity can develop.
  Me and my colleges did this indie game in about 1 month, obviously not full time.

### How to use

  Since this is just a project, we didn´t release a full executable file, so in order to play the game you need to download Processing [here](https://processing.org/download) and a certain sound library.

  Install sound processing library guide:
  
![1](https://user-images.githubusercontent.com/92954277/138365643-f804c2a5-60bf-4bba-a25c-1a7155832b35.png)

![2](https://user-images.githubusercontent.com/92954277/138365799-4790e808-021f-4b5b-b586-01707329bf14.png)

  If you have questions or problems using the library, the best place for help is the [Processing Discourse](https://discourse.processing.org/). 


### How to play

  To move in the menu and even in the game the only keys you need are the arrow keys, space bar and enter.
  The main objetive is to dodge the falling meteors and get the most amount of points by staying alive.


### Main charts of code

  These classes are just examples of what type of information some of the objects in this game might have. The following examples are for *ASTRO* the main caracter and the meteor that try to hit him.

```
class ASTRO {
  private float x,xspeed;
  float x_hitbox,y_hitbox_1,y_hitbox_2,y_hitbox_3, radius_1, radius_2,radius_3;
  
  // CONSTRUTOR
  ASTRO() {
    x = 466;
    xspeed = 6;
  }
  
  void reset() {
    x = 466;
    moveLeft= false; 
    moveRight = false;
  }
 
  void display() {
    image(astro_image,x, y_const, astro_image.width*0.7, astro_image.height*0.7);
    radius_1 = 53;
    radius_2 = 65;
    radius_3 = 40;
    if(show_hitboxes){ 
      fill(0,255,0);
      circle(x_hitbox,y_hitbox_1,radius_1); //HITBOX CABEÇA
      circle(x_hitbox,y_hitbox_2,radius_2); //HITBOX CORPO 
      circle(x_hitbox,y_hitbox_3,radius_3); //HITBOX pernas
    }
  }
 
  void move() {  
    if(moveLeft && x != -2) x -= xspeed; // LIMITE ESQUERDO
    if(moveRight && x != 946) x += xspeed; // LIMITE DIREITO
    x_hitbox = x+40;
    y_hitbox_1=y_const+28;
    y_hitbox_2=y_const+75;
    y_hitbox_3=y_const+112;
  }
}
```

```
class METEOR{
  private float x, y, yspeed, size;
  
  float x_hitbox,y_hitbox,y_hitbox2,y_hitbox3,radius,radius2,radius3;
  
  METEOR(int yspeed_in, float size_in) {
    x= ran.nextInt(995) + 5; // GERA UMA POSIÇÃO ALEATORIA NO EIXO X
    y = -200;
    yspeed = yspeed_in;
    size = size_in;
  }
  
   void display() {
    image(meteor_image,x, y, meteor_image.width*0.1*size, astro_image.height*0.5*size);
    if(show_hitboxes){ 
      fill(0,255,0);
      circle(x_hitbox,y_hitbox, radius); // HITBOX 1 METEORO 
      circle(x_hitbox,y_hitbox2, radius2);// HITBOX 2 METEORO 
      circle(x_hitbox,y_hitbox3, radius3);// HITBOX 3 METEORO 
    }
    radius=size*50;
    radius2=radius/2.3;
    radius3= radius/3;
  }
  ```
  
  Since the essense of the game is to dodge all the falling meteors the most important algorithm is what we call the colision checker, this funcion went through the array of objects called meteors and checked their individual position to compare to the main caraters's one, if any collision was detected the game would go to a death screen.
  The code seeems complicated but it uses a very simple algorithm that calculates the distances of the hitboxes. Keep in mind that each hitbox was done with circles in order to simplify it.


![3](https://user-images.githubusercontent.com/92954277/138367825-e90fd837-3eb4-44e3-a203-1836034fb81c.png)


```
void colisionChecker() { // FUNÇÃO DE DETEÇÃO DE COLISÃO
  for(int i = 0; i < temp_n_meteoros; i++) {
    //HITBOX 1 METEORO
    float distance_between= sqrt(pow(character.x_hitbox-meteor[i].x_hitbox,2)+pow(character.y_hitbox_1-meteor[i].y_hitbox,2)); // calcula a distancia entre os doiso caracter e o meteoro (hitbox cabeça)
    float distance_min = (character.radius_1+meteor[i].radius)*0.50; // distancia minima que podem ter(hitbox cabeça) 
    float distance_between_1= sqrt(pow(character.x_hitbox-meteor[i].x_hitbox,2)+pow(character.y_hitbox_2-meteor[i].y_hitbox,2));//(hitbox corpo)
    float distance_min_1 =(character.radius_2+meteor[i].radius)*0.50;//(hitbox corpo)
    float distance_between_2= sqrt(pow(character.x_hitbox-meteor[i].x_hitbox,2)+pow(character.y_hitbox_3-meteor[i].y_hitbox,2));//(hitbox pernas)
    float distance_min_2 =(character.radius_3+meteor[i].radius)*0.50;//(hitbox pernas)
    //HITBOX 2 METEORO
    float distance_between_3= sqrt(pow(character.x_hitbox-meteor[i].x_hitbox,2)+pow(character.y_hitbox_1-meteor[i].y_hitbox2,2)); // calcula a distancia entre os doiso caracter e o meteoro (hitbox cabeça)
    float distance_min_3 = (character.radius_1+meteor[i].radius2)*0.50; // distancia minima que podem ter(hitbox cabeça) 
    float distance_between_4= sqrt(pow(character.x_hitbox-meteor[i].x_hitbox,2)+pow(character.y_hitbox_2-meteor[i].y_hitbox2,2));//(hitbox corpo)
    float distance_min_4 =(character.radius_2+meteor[i].radius2)*0.50;//(hitbox corpo)
    float distance_between_5= sqrt(pow(character.x_hitbox-meteor[i].x_hitbox,2)+pow(character.y_hitbox_3-meteor[i].y_hitbox2,2));//(hitbox pernas)
    float distance_min_5 =(character.radius_3+meteor[i].radius2)*0.50;//(hitbox pernas)
    //HITBOX 3 METEORO
    float distance_between_6= sqrt(pow(character.x_hitbox-meteor[i].x_hitbox,2)+pow(character.y_hitbox_1-meteor[i].y_hitbox3,2)); // calcula a distancia entre os doiso caracter e o meteoro (hitbox cabeça)
    float distance_min_6 = (character.radius_1+meteor[i].radius3)*0.50; // distancia minima que podem ter(hitbox cabeça) 
    float distance_between_7= sqrt(pow(character.x_hitbox-meteor[i].x_hitbox,2)+pow(character.y_hitbox_2-meteor[i].y_hitbox3,2));//(hitbox corpo)
    float distance_min_7=(character.radius_2+meteor[i].radius3)*0.50;//(hitbox corpo)
    float distance_between_8= sqrt(pow(character.x_hitbox-meteor[i].x_hitbox,2)+pow(character.y_hitbox_3-meteor[i].y_hitbox3,2));//(hitbox pernas)
    float distance_min_8 =(character.radius_3+meteor[i].radius3)*0.50;//(hitbox pernas)
    
    if(distance_min > distance_between || distance_min_1 > distance_between_1 || distance_min_2 > distance_between_2 || 
    distance_min_3 > distance_between_3 || distance_min_4 > distance_between_4 || distance_min_5 > distance_between_5 || 
    distance_min_6 > distance_between_6 || distance_min_7 > distance_between_7 || distance_min_8 > distance_between_8){// TERMINA  O JOGO SE DETETAR IMPACTO
      //println("Meteor "+i+" colidiu");
      start = false;
      death_screen = true;
      reset(); // FAZ RESET DAS POSIÇÕES TANTO TO CARACTER, TANTO DOS METEOROS
    }
  }
}
```

### Extra features

* Ingame menu
* Diferent variety of caracters to choose from
* Volume mute buttom and bar
* Coin system (collet in game in order to obtain more points)
* Scoreboard with sorting algorithm ( scores and respective names are exported to a .txt file )

### Conclusion

Processing is a good platform for people that want to create a beginers project and simply have fun. We had a great time, even through the game looks simple we surely used a lot time in simple details that make the diference.
 
### Developing team

* Boris Teixeira 
* Francisco Heleno
* Filipe Silva


All the code can be used freely.

*Have a good one.*
