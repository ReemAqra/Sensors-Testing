# Sensors-Testing
int Echo1 = A5;//LEFT_SENSOR ECHO
int Trig1 = A4;//LEFT_SENSOR TRIG
int Echo2 = A3;//MID_SENSOR ECHO
int Trig2 = A2;//MID_SENSOR TRIG
int Echo3 = A1;//RIGHT_SENSOR ECHO
int Trig3 = A0;//RIGHT_SENSOR TRIG
int ledPin =(13);
int in1=7;
int in2=6;
int in3=4;
int in4=3;
int ENA=5;
int ENB=2;

int ABS=200;

int Left_Distance=0,Middle_Distance=0,Right_Distance=0;

void setup() {
  pinMode (ledPin, OUTPUT);
  pinMode (Trig1, OUTPUT);
  pinMode (Echo1, INPUT);
  pinMode (Trig2, OUTPUT);
  pinMode (Echo2, INPUT);
  pinMode (Trig3, OUTPUT);
  pinMode (Echo3, INPUT);
   
  pinMode(ENA,OUTPUT);
  pinMode(ENB,OUTPUT);
  pinMode(in1,OUTPUT);
  pinMode(in2,OUTPUT);
  pinMode(in3,OUTPUT);
  pinMode(in4,OUTPUT);
}

 void _mForward(){
  digitalWrite(in1,LOW);
  digitalWrite(in2,HIGH);
  digitalWrite(in3,LOW);
  digitalWrite(in4,HIGH);
  analogWrite(ENA,ABS);
  analogWrite(ENB,ABS);
  Serial.println("ROPOOT_MOVING_FORWARD");
}
void _mBack(){
  digitalWrite(in1,HIGH);
  digitalWrite(in2,LOW);
  digitalWrite(in3,HIGH);
  digitalWrite(in4,LOW);
  analogWrite(ENA,ABS);
  analogWrite(ENB,ABS);
  Serial.println("ROPOOT_MOVING_BACKWARD");  
}
void _mLeft(){
  digitalWrite(in1,LOW);
  digitalWrite(in2,HIGH);
  digitalWrite(in3,LOW);
  digitalWrite(in4,LOW);
  analogWrite(ENA,ABS);
  analogWrite(ENB, 0);
  Serial.println("ROPOOT_MOVING_LEFT");  
}
void _mRight(){
  digitalWrite(in1,LOW);
  digitalWrite(in2,LOW);
  digitalWrite(in3,LOW);
  digitalWrite(in4,HIGH);
  analogWrite(ENA,0);
  analogWrite(ENB,ABS);
  Serial.println("ROPOOT_MOVING_RIGHT");  
}
void _mStop(){
  digitalWrite(in1,LOW);
  digitalWrite(in2,HIGH);
  digitalWrite(in3,LOW);
  digitalWrite(in4,HIGH);
  analogWrite(ENA,0);
  analogWrite(ENB,0);
  Serial.println("ROPOOT_STOP"); 
}

int Read_Left_Distance(){
  digitalWrite(Trig1,HIGH);
  delayMicroseconds(20);
  digitalWrite(Trig1,LOW);
  float Fdistance=pulseIn(Echo1,HIGH);
  delay(10);
  
  Fdistance=(Fdistance/2)/29.1;
  return(int)Fdistance;
  }

int Read_Middle_Distance(){
  digitalWrite(Trig2,HIGH);
  delayMicroseconds(20);
  digitalWrite(Trig2,LOW);
  float Fdistance=pulseIn(Echo2,HIGH);
  delay(10);
  
  Fdistance=(Fdistance/2)/29.1;
  return(int)Fdistance;
  }

int Read_Right_Distance(){
  digitalWrite(Trig3,HIGH);
  delayMicroseconds(20);
  digitalWrite(Trig3,LOW);
  float Fdistance=pulseIn(Echo3,HIGH);
  delay(10);
  
  Fdistance=(Fdistance/2)/29.1;
  return(int)Fdistance;
  }  
  
void loop(){
  
  digitalWrite (ledPin, LOW); 
  Left_Distance=Read_Left_Distance();
  delay(10);
  Middle_Distance=Read_Middle_Distance();
  delay(10);
  Right_Distance=Read_Right_Distance();
  delay(10);

  if(Left_Distance <=10) // If the sensor detects an obstacle less than 30 cm in distance, the LED will start to blink.
  digitalWrite (ledPin, HIGH);
  delay(50);
  if(Left_Distance >=10)// If no obstacle is there within 30 cm, the Led should turn off.
  digitalWrite (ledPin, LOW);
  
   
}

