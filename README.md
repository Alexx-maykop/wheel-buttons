# wheel-buttons
int rez;
int scd = 0;
int sec = 0;
int knop[] = {0,7,17,31,56,103,5}; // mute, vol+, vol -, mode, up, down , +- параметр подбора


const int r = 2;  // 0r
const int p1 = 3; // 3k
const int p2 = 4; // 16k
const int p3 = 5; // 24k
const int p4 = 6; // 1.2k
const int p5 = 7; // 8.2k
const int p6 = 8; // 10k
const int p7 = 9; // 5.6k

void setup() {
    Serial.begin(9600);
    pinMode(r, INPUT);
    pinMode(p1, INPUT);
    pinMode(p2, INPUT);
    pinMode(p3, INPUT);
    pinMode(p4, INPUT);
    pinMode(p5, INPUT);
    pinMode(p6, INPUT);
    pinMode(p7, INPUT);    
}


void loop() {

  rez = analogRead(A0);
 Serial.println(rez);
delay(200);
  
  
 //-------------------- счетчик удержания кнопки -------------------------- 
  if(rez < (knop[5]+100)) { 
      scd++; 
    } 
  else  {
      scd = 0;
      sec = 0;
    }  
  delay(5);  
  
  
 //-------------------- длинное нажатие --------------------------   
  if (scd >= 100) 
  {
    if (sec == 0) {
      if ( rez < knop[0] + knop[6]){fun_L1();}
      if ( rez > knop[0] + knop[6]  && rez < knop[1] + knop[6] ){fun_L2();}
      if ( rez > knop[1] + knop[6]  && rez < knop[2] + knop[6] ){fun_L3();}
      if ( rez > knop[2] + knop[6]  && rez < knop[3] + knop[6] ){fun_L4();}
      if ( rez > knop[3] + knop[6]  && rez < knop[4] + knop[6] ){fun_L5();}
      if ( rez > knop[4] + knop[6]  && rez < knop[5] + knop[6] ){fun_L6();}
    }
    sec = 1;
  }
  
  
  //-------------------- короткое нажатие ---------------------------
 
    if (scd >0 && scd < 100 && analogRead(A0) > (knop[5] + 100)) 
  {
      if ( rez < knop[0] + knop[6]){fun_S1();}
      if ( rez > knop[0] + knop[6]  && rez < knop[1] + knop[6] ){fun_S2();}
      if ( rez > knop[1] + knop[6]  && rez < knop[2] + knop[6] ){fun_S3();}
      if ( rez > knop[2] + knop[6]  && rez < knop[3] + knop[6] ){fun_S4();}
      if ( rez > knop[3] + knop[6]  && rez < knop[4] + knop[6] ){fun_S5();}
      if ( rez > knop[4] + knop[6]  && rez < knop[5] + knop[6] ){fun_S6();}
  }
}

void fun_S1() { // answer ring
  Serial.println("answer ring");
  pinMode(r, OUTPUT);
  pinMode(p1, OUTPUT);
  digitalWrite(r, LOW);
  digitalWrite(p1, LOW);
  delay(50);
  pinMode(r, INPUT);
  pinMode(p1, INPUT);
  
  
}

void fun_S2() {
  Serial.println("vol+");
  pinMode(p2, OUTPUT);
  digitalWrite(p2, LOW);
  delay(50);
  pinMode(p2, INPUT);
}

void fun_S3() {
  Serial.println("vol-");
  pinMode(p3, OUTPUT);
  digitalWrite(p3, LOW);
  delay(50);
  pinMode(p3, INPUT);
}

void fun_S4() {
  Serial.println("source");
  pinMode(p4, OUTPUT);
  digitalWrite(p4, LOW);
  delay(50);
  pinMode(p4, INPUT);
}

void fun_S5() {
  Serial.println("next treck");
  pinMode(p5, OUTPUT);
  digitalWrite(p5, LOW);
  delay(50);
  pinMode(p5, INPUT);
}

void fun_S6() {
  Serial.println("prev. treck");
  pinMode(p6, OUTPUT);
  digitalWrite(p6, LOW);
  delay(50);
  pinMode(p6, INPUT);
}



void fun_L1() {
  Serial.println("mute");
  pinMode(p1, OUTPUT);
  digitalWrite(p1, LOW);
  delay(50);
  pinMode(p1, INPUT);
  
}

void fun_L2() {
  Serial.println("display ");
  pinMode(p7, OUTPUT);
  digitalWrite(p7, LOW);
  delay(50);
  pinMode(p7, INPUT);
  
}

void fun_L3() {
  Serial.println("hang up");
  pinMode(r, OUTPUT);
  pinMode(p7, OUTPUT);
  digitalWrite(r, LOW);
  digitalWrite(p7, LOW);
  delay(50);
  pinMode(r, INPUT);
  pinMode(p7, INPUT);
}

void fun_L4() {
  Serial.println("tel.menu");
  pinMode(r, OUTPUT);
  pinMode(p4, OUTPUT);
  digitalWrite(r, LOW);
  digitalWrite(p4, LOW);
  delay(50);
  pinMode(r, INPUT);
  pinMode(p4, INPUT);
}

void fun_L5() {
  Serial.println("folder up");
  pinMode(r, OUTPUT);
  pinMode(p5, OUTPUT);
  digitalWrite(r, LOW);
  digitalWrite(p5, LOW);
  delay(50);
  pinMode(r, INPUT);
  pinMode(p5, INPUT);
}

void fun_L6() {
  Serial.println("folder down");
  pinMode(r, OUTPUT);
  pinMode(p6, OUTPUT);
  digitalWrite(r, LOW);
  digitalWrite(p6, LOW);
  delay(50);
  pinMode(r, INPUT);
  pinMode(p6, INPUT);
}


