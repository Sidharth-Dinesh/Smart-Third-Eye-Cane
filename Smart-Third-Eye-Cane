int led=3;
int buzz=4;
int trig1=10;
int echo1=11;
int trig2=6;
int echo2=5;
int trig3=12;
int echo3=13;
int motor=7;
int t1;
int d1;
int val;
int t2;
int d2;
int t3;
in d3;
int d;

void setup()
 {
 pinMode(trig1,OUTPUT);
 pinMode(echo1,INPUT);
 pinMode(led,OUTPUT);
 pinMode(buzz,OUTPUT);
 pinMode(trig2,OUTPUT);
 pinMode(echo2,INPUT);
 pinMode(trig3,OUTPUT);
 pinMode(echo3,INPUT);
 pinMode(motor,OUTPUT);
 Serial.begin(9600);
}

void loop()
{
 //for forward obstacle detection (2 sensors):
 
 digitalWrite(trig1,LOW);
 delayMicroseconds(2);
 digitalWrite(trig1,HIGH);
 delayMicroseconds(10);
 digitalWrite(trig1,LOW);
 t1=pulseIn(echo1,HIGH);
 d1=t1*(0.01715); //distance = (duration/2) / 29.1
 digitalWrite(trig2,LOW);
 delayMicroseconds(2);
 digitalWrite(trig2,HIGH);
 delayMicroseconds(10);
 digitalWrite(trig2,LOW);
 t2=pulseIn(echo2,HIGH);
 d2=t2*(0.01715); //distance = (duration/2) / 29.1
 
if (d1<d2)
 d=d1;
 else
 d=d2;

 if (d<0)
 analogWrite(led,0); //LED is LOW for distances<0
 else if(d<=20)
 {
 val=12.75*(20-d);
 analogWrite(led,val); //brightness of LED depends on the distance
 digitalWrite(buzz,HIGH); // buzzer is HIGH for closer distances
 delayMicroseconds(8);
 }
 else
 {
 val=0;
 analogWrite(led,val); //LED is low for distances>20
 digitalWrite(buzz,LOW); // buzzer is LOW for farther distances
 delayMicroseconds(8);
 }
 
//for pothole/bump detection (one bottom sensor) which detects only when the reflected ray
//from the ground reaches the Echo sensor.
//As the third sensor is kept tilted at an angle for detection of bump as well as pothole,
//we set two distance thresholds, d3<10 for hump and 20<d3<30 for potholes.

 digitalWrite(trig3,LOW);
 delayMicroseconds(2);
 digitalWrite(trig3,HIGH);
 delayMicroseconds(10);
 digitalWrite(trig3,LOW);
 
 t3=pulseIn(echo3,HIGH);
 d3=t3*(0.01715);
 
if(d3<=10) //10cm is set as the threshold for hump detection
 {
 digitalWrite(motor,HIGH); // vibration motor is HIGH for nearby humps
 delayMicroseconds(8);
 }
 else if(d3<=30 && d3>=20) //range of 20-30cms is set as the threshold (pothole detection)
 {
 digitalWrite(motor,HIGH); //vibration motor is HIGH for nearby potholes
 delayMicroseconds(8);
 }
else
{
digitalWrite(motor,LOW); //for large distances and for those rays which didn’t reach the
//Echo sensor after reflection, vibration motor is LOW
 delayMicroseconds(8);
}

 Serial.print("Distance1: ");
 Serial.println(d1);
 Serial.print("Distance2: ");
 Serial.println(d2);
 Serial.print("Distance3: ");
 Serial.println(d3);
 }

