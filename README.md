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

  To move in the menu and even in the game the only keys you need are the *arrow keys*, *space bar* and *enter*.
  The *main objetive is to dodge the falling meteors and get the most amount of points by staying alive*.


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
  
  Since the essense of the game is to dodge all the falling meteors the most important algorithm is what we call the colision checker, this funcion goes through the array of objects called meteors and checks their individual position and compares to the main caraters's one, if any collision is detected the game would finish.
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
* Coin system (collect in game in order to obtain more points)
* Scoreboard with sorting algorithm ( scores and respective names are exported to a .txt file )

### Conclusion

Processing is a good platform for people that want to create a beginers project and simply have fun. We had a great time, even through the game looks simple we surely used a lot time in simple details that make the diference.
 
### Developing team

* Boris Teixeira 
* Francisco Heleno
* Filipe Silva


All the code can be used freely.

*Have a good one.*


RAW CODE (comments and varibles are most likely to be in portuguese):
```
import java.util.Random;
import java.util.Arrays;
import java.util.ArrayList;
import processing.sound.*;
import processing.serial.*;

Random ran = new Random();

//---Opções----------------
boolean show_hitboxes = true;
int n_meteoros= 3; //
//-------------------------

PImage astro_image,meteor_image, seta,select_char,insert_name,gears,empty,pause,play,arrow,space,return_i,return_1,coin;
PImage[] bg = new PImage[8];
PImage[] icons_1 = new PImage[2];
PImage[] icons_2 = new PImage[2];
PImage[] icons_3 = new PImage[2];
PImage[] pause_menu = new PImage[6];
PImage[] astro = new PImage[3]; 
PImage[] ar1 = new PImage[3];
PImage[] al1 = new PImage[3];
PImage[] ar2 = new PImage[3];
PImage[] al2 = new PImage[3];
PImage[] am_l = new PImage[3];
PImage[] am_r = new PImage[3];
PImage[] retangle = new PImage[2];
PImage[] soundb = new PImage[2];
PFont font;
SoundFile file;

PImage bg_option;

PLAYER[] players = new PLAYER[100];
COIN[] coins = new COIN[10];
METEOR[] meteor = new METEOR[200];

ASTRO character;

String temp= "", temp2="",temp3="";
char mute;

static final float y_const= 620; 
boolean start= false, selected= false, menuconfig= false, ask_name= false,death_screen = false,askname_2players = false,start_2 = false,pause_game = false, select_pause = false,volume_option = false,select_menu_config = false,music = true;

int option= 1, option_char= 0, cont_pessoas= 3,temp_n_meteoros=n_meteoros,ver = 0,ver_1=0,opcao = 0, option_ambient = 0, nivel = 0, on_off= 0,opcao_menu = 1,cont_pessoas_2=3, volume = 5, char_selected = 0,bg_selected = 1,n_coins = 0, astromov = 0, astrodance = 0,temp_char=0,conf_char=0,conf_ambient=0;

void setup() { // SÓ CORRE 1 VEZ
  players[0]=new PLAYER("Boris\n");
  players[1]=new PLAYER("Francisco\n");
  players[2]=new PLAYER("Filipe\n");
  players[0].pontuacao =3950;
  players[1].pontuacao = 10200;
  players[2].pontuacao = 7950;
  size(1024,768);//resolução
  frameRate(60);//fps
  
  for(int i= 0; i < 3 ; i++)// prenche o astro[] = array com imagens dos tipos de astronautas
    astro[i] = loadImage("player"+(i+1)+".png");
  for(int i= 0; i < 3 ; i++) // prenche o ar1[] = array com imagens dos tipos de astronautas de lado
    ar1[i] = loadImage("AR1_"+(i+1)+".png");
  for(int i= 0; i < 3 ; i++) // prenche o al1[] = array com imagens dos tipos de astronautas de lado
    al1[i] = loadImage("AL1_"+(i+1)+".png");
  for(int i= 0; i < 3 ; i++) // prenche o ar1[] = array com imagens dos tipos de astronautas de lado
    ar2[i] = loadImage("AR2_"+(i+1)+".png");
  for(int i= 0; i < 3 ; i++) // prenche o al1[] = array com imagens dos tipos de astronautas de lado
    al2[i] = loadImage("AL2_"+(i+1)+".png");   
  for(int i= 0; i < 8 ; i++) // prenche o al1[] = array com imagens dos tipos de astronautas de lado
    bg[i] = loadImage("bg"+(i+1)+".png");
  for(int i= 0; i < 3 ; i++) // prenche o al1[] = array com imagens dos tipos de astronautas de lado
    am_r[i] = loadImage("AMR_"+(i+1)+".png");
  for(int i= 0; i < 3 ; i++) // prenche o al1[] = array com imagens dos tipos de astronautas de lado
    am_l[i] = loadImage("AML_"+(i+1)+".png"); 
  bg_option = bg[1];
  icons_1[0]= loadImage("MENU_1PLAYER.png");// icons_1[] = array com botão singleplayer e versão primida
  icons_1[1]= loadImage("MENU_1PLAYER_SELEC.png");
  icons_3[0]=loadImage("MENU_CONFIG.png");
  icons_3[1]=loadImage("MENU_CONFIG_SELEC.png");
  pause_menu[0] = loadImage("PAUSE_1.png");
  pause_menu[1] = loadImage("PAUSE_1_1.png");
  pause_menu[2] = loadImage("PAUSE_2.png");
  pause_menu[3] = loadImage("PAUSE_2_2.png");
  pause_menu[4] = loadImage("volume.png");
  pause_menu[5] = loadImage("volume_selec.png");
  retangle[0] = loadImage("retangulo_player.png");
  retangle[1] = loadImage("retangulo_bg.png");
  soundb[0]= loadImage("sound_on.png");
  soundb[1]= loadImage("sound_off.png");
  empty = loadImage("empty.png");
  seta = loadImage("seta.png");
  return_i=loadImage("retun.png");
  return_1 = loadImage("retun_1.png");
  arrow = loadImage("arrow.png");
  space = loadImage("SPACE.png");
  coin = loadImage("coin.png");
  select_char = loadImage("SELECT_CHARACTER.png");
  insert_name= loadImage("insert_name.png");
  pause = loadImage("pause_button.png");
  play = loadImage("play_button.png");
  gears = loadImage("gears.png");
  file = new SoundFile(this, "soundtrack.mp3");
  file.amp(0.005);
  file.loop();
  font = createFont("Evil Empire.otf", 32);
  textFont(font);
  
  
  astro_image = astro[0]; //
  meteor_image = loadImage("meteor.png");// 


  character = new ASTRO(); // character 1
  generate_meteor(); // chama a função generate_meteor, que enche/substitui o array de meteoros com novos
}

void draw() {// LOOP  INFINITO
if(music== true){
  if(volume == 0)
    file.amp(0);
  else if ( volume > 0 && volume <31)
    file.amp(0.005*volume);
}
    
  if(start == false && start_2 == false ){    // MENU
    fill(255,255,255);
    
    background(bg[0]);// background do menu
    textSize(15);
    if(music== false) {
      image(soundb[1],932,15,soundb[1].width*0.5,soundb[1].height*0.5);
      file.amp(0);
      text("Press M to unmute",910,110);
    }
    else{
      image(soundb[0],932,15,soundb[0].width*0.5,soundb[0].height*0.5);
      file.amp(0.005*volume);
      text("Press M to mute",920,110);
    }
    
    sort_players(players);
    for(int i =0; i < cont_pessoas_2;i++){
      temp2= i+1+"  Name: "+players[i].nome;
      temp3="Points: "+players[i].pontuacao;
      textSize(20);
      text(temp2, 350,250+i*50);
      text(temp3,350,270+i*50);
      
    }
    
    if( option == 1 && menuconfig == false && ask_name== false && death_screen == false ){ // quando clicas UP
      image(icons_1[1],750,480); // OPÇÃO 1- imagem 1 jogador
      image(icons_3[0],750,580); // OPÇÃO 3- config
      astrodance++;
         if(astrodance < 8)
           astro_image= ar1[option_char];// DÁ LOAD A IMAGEM DO BONECO A ANDAR PARA A ESQUERDA
         if(astrodance < 16 && astrodance >= 8)
           astro_image= am_l[option_char];
         if(astrodance < 24 && astrodance >= 16)
           astro_image= astro[option_char];
         if(astrodance < 32 && astrodance >= 24)
           astro_image = am_r[option_char];
         if(astrodance < 40 &&astrodance >= 32)
            astro_image= al1[option_char];
         if(astrodance >= 40 )
         astrodance=0;
      image(astro_image,50,460);
      if(selected){
        selected = false;
        ask_name= true;
        astro_image= astro[char_selected];
        ver = 0;
        n_coins= 0;
      }
    }
    else if( option == 2 && menuconfig == false && ask_name== false && death_screen == false){
      image(icons_1[0],750,480); // OPÇÃO 1- imagem 1 jogador
      image(icons_3[1],750,580); // OPÇÃO 3- config
      image(gears,40,510, gears.width*0.4, gears.height*0.4);
      if(selected){
        selected = false;
        menuconfig = true;
        opcao = 0;
        option_ambient = 0;
        temp_char = 0;
        conf_char=0;
        conf_ambient=0;
      }
    }
    else if(menuconfig == true && ask_name== false && death_screen == false){
      background(bg[2]);
      image(astro[0],300,75);
      image(astro[1],450,75);
      image(astro[2],600,75);
      image(bg[1],310,410,bg[1].width*0.1,bg[2].height*0.1);
      image(bg[6],460,410,bg[6].width*0.1,bg[6].height*0.1);
      image(bg[7],610,410,bg[7].width*0.1,bg[7].height*0.1);
      textSize(40);
      text("Select character",377, 55);
      text("Select wallpaper",377, 365);
      textSize(50); 
      image(pause_menu[4],315,540);
      image(return_i,315,660);
      for(int i = 0 ; i < volume ; i++) {
        fill(0);
        text("| ",520+i*5,595.5);
      }       
      if( char_selected == 0)
        image(retangle[0],300,75);
      if( char_selected == 1)
        image(retangle[0],450,75);
       if( char_selected == 2)
        image(retangle[0],600,75);
      if( bg_selected == 1)
        image(retangle[1],305,405,retangle[1].width*0.11,retangle[1].height*0.11);
      if( bg_selected == 6)
        image(retangle[1],455,405,retangle[1].width*0.11,retangle[1].height*0.11);
       if( bg_selected == 7 )
        image(retangle[1],605,405,retangle[1].width*0.11,retangle[1].height*0.11);        
       if(opcao == 0) {
         if ( temp_char == 0)
          image(seta,341.8,285,seta.width*0.4,seta.height*0.4);
         if ( temp_char == 1)
          image(seta,491.8,285,seta.width*0.4,seta.height*0.4);
         if ( temp_char == 2)
          image(seta,641.8,285,seta.width*0.4,seta.height*0.4);
       }
      if(temp_char == 0 && opcao == 0){
        if ( select_menu_config == true ) {
          option_char = 0;
          astro_image = astro[option_char];// astronauta branco
          select_menu_config = false;
          char_selected = 0;
        }
      }
      if(temp_char == 1 && opcao == 0){
        if ( select_menu_config == true ) {
          option_char = 1;
          astro_image = astro[option_char];// astronauta branco
          select_menu_config = false;
          char_selected = 1;
        }  
      }
      else if(temp_char == 2 && opcao == 0){
        if ( select_menu_config == true ) {
          option_char = 2;
          astro_image = astro[option_char];// astronauta branco
          select_menu_config = false;
          char_selected = 2;
        }
      }
      else if(option_ambient == 0 && opcao == 1){
        if ( select_menu_config == true ) {
          bg_option = bg[1];// bg1
          select_menu_config = false;
          bg_selected = 1;
          conf_ambient =1;
        }          
        image(seta,343.8,505,seta.width*0.4,seta.height*0.4);      
      }
      else if(option_ambient == 1 && opcao == 1){
        if ( select_menu_config == true ) {        
          bg_option = bg[6];// bg6 
          select_menu_config = false;
          bg_selected = 6;
          conf_ambient =1;
        }           
        image(seta,493.8,505,seta.width*0.4,seta.height*0.4);
      }
      else if(option_ambient == 2 && opcao == 1){
        if ( select_menu_config == true ) {        
          bg_option = bg[7];// bg7
          select_menu_config = false;
          bg_selected = 7;
          conf_ambient =1;
        }           
        image(seta,643.8,505,seta.width*0.4,seta.height*0.4);
      }
      else if( opcao == 2) {
        image(pause_menu[5],315,540);
        for(int i = 0 ; i < volume ; i++) {
          fill(0);
          text("| ",520+i*5,595.5);
        }
      }
      else if(opcao == 3) {
        image(return_1,315,660);
      }
    }
    else if(ask_name == true && death_screen == false){
      background(bg[5]);
      image(arrow,237,650,arrow.width*0.2,arrow.height*0.2);
      image(space,557,650,space.width*0.2,space.height*0.2);
      fill(255);
      textSize(30);
      text("Movement keys",200,600);
      text("Pause key",610,600);
      textSize(60);
      text("Insert name:",100,375);
      textSize(50);
      text(temp,410,375);
      textSize(20);
      text("Minimum 3 characters",100,400);
      nivel = 0;
      textSize(50);
    }
    else if( death_screen == true ){
      background(bg[3]);
      textSize(120);
      text("You are dead",210,200);
      textSize(80);
      text("Points: "+players[cont_pessoas].pontuacao+" ",225,500);
      textSize(40);
      text("Press ENTER to continue",225,600);
    }
  }
  else if(start == true){ // JOGO
    if( start == true && pause_game == false ){
      opcao_menu = 1;
      background(bg_option);//background do jogo
      character.move();//função de movimento do character
      character.display();//função que atualiza a posição do caracter consoante a imagem
      fill(255);
      text("Points: "+players[cont_pessoas].pontuacao,10,50);
      text("Level "+nivel,10,90);
      image(pause,940,15,pause.width*0.5,pause.height*0.5);
      if( (players[cont_pessoas].pontuacao > 500) && ( players[cont_pessoas].pontuacao < 1000)){
        if( ver == 0){
          nivel++;
          add_more_meteor_1();
          add_coin();
        }
        ver = 1;
      }
      else if( (players[cont_pessoas].pontuacao > 1000) && ( players[cont_pessoas].pontuacao < 2000)){
        if( ver == 1) {
          nivel++;
          add_coin();
          for(int i = 0; i < 2; i++)
            add_more_meteor_1();
        }
        ver = 0;
      }
      else if( ( players[cont_pessoas].pontuacao > 2000) && ( players[cont_pessoas].pontuacao < 3000)){
        if( ver == 0) {
          nivel++;
          add_coin();
          for(int i = 0; i < 2; i++)
            add_more_meteor_1();
        }
        ver = 1;
      }
      else if( ( players[cont_pessoas].pontuacao > 3000) && ( players[cont_pessoas].pontuacao < 4000) ){
        if( ver == 1) {
          nivel++;
          add_coin();
          for(int i = 0; i < 2; i++)
            add_more_meteor_1();
        }
        ver = 0;
      }
      else if( ( players[cont_pessoas].pontuacao > 4000) && ( players[cont_pessoas].pontuacao < 5000)){
        if(ver == 0) {
          nivel++;
          add_coin();
          add_more_meteor_1();
          add_more_meteor_2();
        }
        ver = 1;
      } 
      else if(( players[cont_pessoas].pontuacao > 5000) && ( players[cont_pessoas].pontuacao < 6000)){
        if(ver == 1) {
          nivel++;
          add_coin();
          for(int i = 0; i < 2; i++)
            add_more_meteor_1();
        }
        ver = 0;
      }
      else if((players[cont_pessoas].pontuacao > 6000) && (players[cont_pessoas].pontuacao < 7000)){
        if( ver == 0 ){
          nivel++;
          add_coin();
          add_more_meteor_1();
          add_more_meteor_2();        
        }
        ver = 1;
      }
  
      else if((players[cont_pessoas].pontuacao > 7000) && (players[cont_pessoas].pontuacao < 8000)){
        if( ver == 1 ){
          nivel++;
          add_coin();
          add_more_meteor_2();        
        }
        ver = 0;
      }
      else if((players[cont_pessoas].pontuacao > 8000) && ( players[cont_pessoas].pontuacao < 9000)){
        if( ver == 0 ){
          nivel++;
          add_coin();
          add_more_meteor_2();        
        }
        ver = 1;
      }
      else if((players[cont_pessoas].pontuacao > 9000) && ( players[cont_pessoas].pontuacao < 10000)){
        if( ver == 1 ){
          nivel++;
          add_more_meteor_2();        
        }
        ver = 0;
      }
      else if( players[cont_pessoas].pontuacao > 10000){
        if( ver == 0 ){
          nivel++;
          for(int i = 0; i < 2; i++)
            add_more_meteor_2();
        }
        ver = 1;
      } 
      for(int i = 0; i < temp_n_meteoros; i++){ // 
        meteor[i].move(); // função de movimento do character
        meteor[i].display();// função que atualiza a posição dos meteoros consoante a imagem
      }
      for(int i = 0; i < n_coins; i++){ // 
      coins[i].move();
      coins[i].display();      
      }
      colisionChecker(); // função de verificação de impacto caracter/metoro
      coin_collet();
    }
    else if ( start == true && pause_game == true ){
      image(play,940,15,pause.width*0.5,pause.height*0.5);
      image(pause_menu[0],315,300);
      image(pause_menu[4],315,390);
      image(pause_menu[2],435,480);
      fill(0);
      for(int i = 0 ; i < volume ; i++) {
        text("| ",520+i*5,446.5);
      }
      if ( opcao_menu == 1 ){
        image(pause_menu[1],315,300);
        if (select_pause == true) {
          select_pause = false;
          pause_game = false;
        }
      }
      if ( opcao_menu == 2 ){
      image(pause_menu[5],315,390);
      for(int i = 0 ; i < volume ; i++) {
        text("| ",520+i*5,446.5);
      }        
          volume_option = true;
      }      
      if ( opcao_menu == 3 ){
        image(pause_menu[3],435,480);
        if (select_pause == true) {
          select_pause = false;
          pause_game = false;
          start = false;
          reset(); 
        }
      }      
    }
  } 
}

void keyPressed() {
  if(start == false && menuconfig == false && ask_name == false && death_screen == false && volume_option == false){ // LEITURA DE COMANDOS NO MENU
    if (key == CODED) {
       if (keyCode == UP) {
         if( option != 1)option--; // se for a primeira opção e clicar para cima vai para a ultima
         else option = 2;
       } 
       else if(keyCode == DOWN) {
         if( option != 2)option++; // se for a ultima opção e clicar para baixo volta a primeira
         else option = 1;
       }
    }
    else if( keyCode == ENTER) { // SELECIONAR
       selected=true;
    }
    if( key == 77 || key == 109) {
      if ( music == true)
        music = false;
      else
        music = true;
    }
  }
  else if(start == true && pause_game == false && menuconfig == false && ask_name == false && death_screen == false && volume_option == false){ // LEITURA DE COMANDOS NO JOGO
    if (key == CODED) {
       if (keyCode == LEFT) {
         if(character.x != -2){
         moveLeft = true;
         astromov++;
          if(astromov < 6)
           astro_image= ar1[option_char];// DÁ LOAD A IMAGEM DO BONECO A ANDAR PARA A ESQUERDA
         if(astromov < 12 && astromov >= 6)
           astro_image= am_l[option_char];
         if(astromov < 18 && astromov >= 12)
           astro_image= ar2[option_char];
         if(astromov < 24 && astromov >= 18)
           astro_image = am_l[option_char];
         if(astromov >= 24)
           astromov = 0;
         }
         if(character.x == -2){
           astro_image= am_l[option_char];
         }
       }else if(keyCode == RIGHT) {
         if(character.x != 946){
         moveRight = true;
         astromov++;
          if(astromov < 6)
           astro_image= al1[option_char];// DÁ LOAD A IMAGEM DO BONECO A ANDAR PARA A ESQUERDA
         if(astromov < 12 && astromov >= 6)
           astro_image= am_r[option_char];
         if(astromov < 18 && astromov >= 12)
           astro_image= al2[option_char];
         if(astromov < 24 && astromov >= 18)
           astro_image = am_r[option_char];
         if(astromov >= 24)
           astromov = 0;
         }
         if(character.x == 946){
           astro_image= am_r[option_char];
         }
       }
    }
    else if( key == ' '){
      pause_game = true; 
    }
  }
  else if(start == true && pause_game == true && menuconfig == false && ask_name == false && death_screen == false && volume_option == false){ // LEITURA DE COMANDOS NO JOGO
      if (key == CODED) {
         if (keyCode == UP) {
           if( opcao_menu != 1)opcao_menu--; // se for a primeira opção e clicar para cima vai para a ultima
           else opcao_menu = 3;
         } 
         else if(keyCode == DOWN) {
           if( opcao_menu != 3)opcao_menu++; // se for a ultima opção e clicar para baixo volta a primeira
           else opcao_menu = 1;
         }
      }
      if( key == ENTER) {
       select_pause = true;
      }
    }
  else if(start == true && pause_game == true && volume_option == true && menuconfig == false && ask_name == false && death_screen == false) {
      if( key == CODED) {
        if( keyCode == LEFT) {
          if(volume > 0)
            volume--; 
        }
        else if( keyCode == RIGHT) {
          if( volume < 31)
            volume++; 
        }
        else if( keyCode == UP) {
         volume_option = false;
         select_pause = false;
         opcao_menu = 1;
         
        } 
        else if( keyCode == DOWN) {
         volume_option = false;
         select_pause = false;
         opcao_menu = 3;
        }   
      }
    }
  
  else if(menuconfig == true && ask_name == false && death_screen == false ) {
      if (key == CODED) {
        if (keyCode == UP) {
           if( opcao != 0)opcao--; // se for a primeira opção e clicar para cima vai para a ultima
           else opcao = 3;
        }
        else if (keyCode == DOWN) {
           if( opcao != 3)opcao++; // se for a primeira opção e clicar para cima vai para a ultima
           else opcao = 0;
         }
        else if (keyCode == LEFT) {
          if(opcao == 0) {
            if( temp_char != 0)temp_char--; // se for a primeira opção e clicar para cima vai para a ultima
            else temp_char = 2;
          }
          else if (opcao == 1){
            if( option_ambient != 0)option_ambient--; // se for a primeira opção e clicar para cima vai para a ultima
            else option_ambient = 2;
          }
          else if (opcao == 2){
            if(volume > 0)
              volume--; 
          }        
        } 
        else if(keyCode == RIGHT) {
          if(opcao == 0) {
            if( temp_char != 2)temp_char++; // se for a primeira opção e clicar para cima vai para a ultima
            else temp_char = 0;
          }
          else if (opcao == 1){
            if( option_ambient != 2)option_ambient++; // se for a primeira opção e clicar para cima vai para a ultima
            else option_ambient = 0;
          }
          else if (opcao == 2){
            if( volume < 31)
              volume++; 
          }
        }
      }
      else if(keyCode == ENTER) {
       if( opcao == 3)
         menuconfig=false;
        else{
          select_menu_config= true;
          }
      }
  
  }
  else if(ask_name == true && death_screen == false ) {
    if(( temp.length() < 3 && key != '\n')  || (temp.length() >= 3)) {
      if( key == 8)
          temp = "";
      else
      temp = temp + key;
    }
    if( temp.length() >= 3 && (key == ENTER || temp.length() == 32)){
      if(temp.length() == 32)
      if( temp.charAt(31) != '\n')
        temp = temp +"\n";
        players[cont_pessoas]=new PLAYER(temp);
        ask_name = false;
        start = true;
        temp = "";
    }
  }
  else if(death_screen == true ) {     
    if( key == ENTER){
      death_screen = false;
      cont_pessoas++;
      if(cont_pessoas_2 < 10)
        cont_pessoas_2++;
   }
  }
}


 

void keyReleased() {  // VERIFICA QUANDO A TECLA DEIXA DE SER PREMIDA
  if(start == true){
    if (key == CODED) {
      //println("x =" + character.get_x());
       if (keyCode == LEFT) {
         moveLeft = false;
         astromov = 0;
         astro_image = astro[option_char];// DÁ LOAD A IMAGEM DO BONECO PARADO
       } else if(keyCode == RIGHT) {
         moveRight = false;
         astromov = 0;
         astro_image = astro[option_char];// DÁ LOAD A IMAGEM DO BONECO PARADO
       } 
    }
  }
}
void coin_collet() {
  for(int i = 0; i < n_coins; i++) {
    
    float distance_between= sqrt(pow(character.x_hitbox-coins[i].x_hitbox,2)+pow(character.y_hitbox_1-coins[i].y_hitbox,2)); // calcula a distancia entre os doiso caracter e o meteoro (hitbox cabeça)
    float distance_min = (character.radius_1+coins[i].radius)*0.50; // distancia minima que podem ter(hitbox cabeça) 
    float distance_between_1= sqrt(pow(character.x_hitbox-coins[i].x_hitbox,2)+pow(character.y_hitbox_2-coins[i].y_hitbox,2));//(hitbox corpo)
    float distance_min_1 =(character.radius_2+coins[i].radius)*0.50;//(hitbox corpo)
    float distance_between_2= sqrt(pow(character.x_hitbox-coins[i].x_hitbox,2)+pow(character.y_hitbox_3-coins[i].y_hitbox,2));//(hitbox pernas)
    float distance_min_2 =(character.radius_3+coins[i].radius)*0.50;//(hitbox pernas)
    if(distance_min > distance_between || distance_min_1 > distance_between_1 || distance_min_2 > distance_between_2){
      players[cont_pessoas].add_points(100);
      coins[i].reset();
      
    }
  }
}

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

void sort_players(PLAYER[] a) {
    boolean sorted = false;
    String temp_s;
    int temp_i;
    while(!sorted) {
        sorted = true;
        for (int i = 0; i < cont_pessoas - 1; i++) {
            if (a[i].pontuacao < a[i+1].pontuacao) {
                temp_s = a[i].nome;
                temp_i = a[i].pontuacao;
                a[i].nome = a[i+1].nome;
                a[i].pontuacao= a[i+1].pontuacao;
                a[i+1].nome = temp_s;
                a[i+1].pontuacao = temp_i;
                sorted = false;
            }
        }
    }
}

void generate_meteor(){
  for(int i = 0; i < temp_n_meteoros ; i++)
    meteor[i] = new METEOR(ran.nextInt(6) + 3,1); // gerador de meteoros, parametros aleatorios
}

void add_more_meteor_1() {
  meteor[temp_n_meteoros++] = new METEOR(ran.nextInt(6) + 3,1);
}
void add_more_meteor_2() {
  meteor[temp_n_meteoros++] = new METEOR(ran.nextInt(6) + 3,2);
}
void add_more_meteor_1_5() {
  meteor[temp_n_meteoros++] = new METEOR(ran.nextInt(6) + 3,1.5);
}
void add_coin() {
  coins[n_coins++] = new COIN(2);
}


void reset() {
 generate_meteor();
 character.reset();
 astro_image = astro[option_char];
 temp_n_meteoros = n_meteoros;
}

  

static boolean moveLeft= false, moveRight = false;
static boolean moveLeft_2= false, moveRight_2 = false;

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
  
  
  void move() {
    if(y < 850) {
      y += yspeed;
    }
    else  {
      if(size == 1)
        players[cont_pessoas].add_points(50);
      else if(size == 1.5)
        players[cont_pessoas].add_points(100);   
      else if(size == 2)
        players[cont_pessoas].add_points(150);   
        
      y = -200;
      x = ran.nextInt(980) + 5;
    }
    if(size == 1){
      x_hitbox = x+25;
      y_hitbox= y+71;
      y_hitbox2= y+32.5;
      y_hitbox3= y+7.5;
    }
    else if(size == 1.5) {
      x_hitbox = x+37.5;
      y_hitbox= y+108.5;
      y_hitbox2= y+43;
      y_hitbox3= y+10;
    }
    else if(size == 2){
      x_hitbox = x+50;
      y_hitbox= y+145;
      y_hitbox2= y+65;
      y_hitbox3= y+15;
      
    }
  }
}
class COIN{
  private float x, y, yspeed;
  
  float x_hitbox,y_hitbox,radius,radius2;
  
  COIN(float yspeed_in) {
    x= ran.nextInt(995) + 5; // GERA UMA POSIÇÃO ALEATORIA NO EIXO X
    y = -200;
    yspeed = yspeed_in;

  }
  
   void display() {
    image(coin,x, y, coin.width*0.1, coin.height*0.1);
    if(show_hitboxes){ 
      fill(0,255,0);
      circle(x_hitbox,y_hitbox, radius); // HITBOX coin
    }
    radius=73;
  }
  
  
  void move() {
    if(y < 850) {
      y += yspeed;
    }
    else  {   
      y = -200;
      x= ran.nextInt(995) + 5;
    }
      x_hitbox = x+37;
      y_hitbox= y+37;      
   }
   void reset() {
      y = -200;
      x= ran.nextInt(995) + 5;
   }
   
}


class PLAYER{
  String nome;
  public int pontuacao;
  
  PLAYER(String nome_in) {
  nome=nome_in;
  pontuacao = 0;
  }
  
  void add_points(int x ){
  pontuacao += x;
  }
  
  int get_points(){
    return pontuacao;
  }
}
  
  
```
