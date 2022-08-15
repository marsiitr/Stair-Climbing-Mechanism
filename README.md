int trig1 = 2;
int trig2 = 3;
int trig3 = 4;
int echo1 = 5;
int echo2 = 6;
int echo3 = 7;
int direcF1 = 30;
int direcF2 = 31;
int speedF1 = 8;
int speedF2 = 9;
int direcR1 = 32;
int direcR2 = 33;
int speedR1 = 10;
int speedR2 = 11;
int direcU1 = 34;
int direcU2 = 35;
int speedU1 = 12;
int speedU2 = 13;
long dur1;
long dur2;
long dur3;
int dist1;
int dist2;
int dist3;
void setup()
{
    pinMode(trig1, OUTPUT);
    pinMode(trig2, OUTPUT);
    pinMode(trig3, OUTPUT);
    pinMode(echo1, INPUT);
    pinMode(echo2, INPUT);
    pinMode(echo3, INPUT);
    pinMode(direcF1, OUTPUT);
    pinMode(direcF2, OUTPUT);
    pinMode(direcR1, OUTPUT);
    pinMode(direcR2, OUTPUT);
    pinMode(direcU1, OUTPUT);
    pinMode(direcU2, OUTPUT);
    pinMode(speedF1, OUTPUT);
    pinMode(speedF2, OUTPUT);
    pinMode(speedR1, OUTPUT);
    pinMode(speedR2, OUTPUT);
    pinMode(speedU1, OUTPUT);
    pinMode(speedU2, OUTPUT);
}
void loop()
{
    digitalWrite(trig1, LOW);
    digitalWrite(trig2, LOW);
    digitalWrite(trig3, LOW);
    digitalWrite(direcF1, LOW);
    digitalWrite(direcF2, LOW);
    digitalWrite(direcR1, LOW);
    digitalWrite(direcR2, LOW);
    digitalWrite(direcU1, LOW);
    digitalWrite(direcU2, LOW);
    digitalWrite(speedF1, LOW);
    digitalWrite(speedF2, LOW);
    digitalWrite(speedR1, LOW);
    digitalWrite(speedR2, LOW);
    digitalWrite(speedU1, LOW);
    digitalWrite(speedU2, LOW);
    delay(30);
    digitalWrite(trig1, HIGH);
    digitalWrite(trig2, HIGH);
    delay(10);
    digitalWrite(trig1, LOW);
    digitalWrite(trig2, LOW);
    dur1 = pulseIn(echo1, HIGH);
    dist1 = (dur1)*0.034 / 2;
    dur2 = pulseIn(echo2, HIGH);
    dist2 = (dur2)*0.034 / 2;
    if ((dist1 >= 150) && (dist2 >= 150))
    {
        analogWrite(speedF1, 240);
        analogWrite(speedF2, 240);
        delay(1500);
    }
    else if ((dist1 >= 100) && (dist2 >= 100))
    {
        analogWrite(speedF1, 190);
        analogWrite(speedF2, 190);
        delay(500);
    }
    else if ((dist1 >= 35) && (dist2 >= 35))
    {
        analogWrite(speedF1, 100);
        analogWrite(speedF2, 100);
        delay(500);
    }
    else if ((8 < dist1 < 35) || (8 < dist2 < 35))
    {
        if (dist1 > dist2)
        {
            analogWrite(speedF1, 40);
            delay(200);
            analogWrite(speedF1, 0);
        }
        else
        {
            analogWrite(speedF2, 40);
            delay(200);
            analogWrite(speedF2, 0);
        }
    }
    else if ((6 < dist1 <= 8) || (6 < dist2 <= 8))
    {
        analogWrite(speedR1, 40);
        analogWrite(speedR2, 40);
        delay(200);
        analogWrite(speedR1, 0);
        analogWrite(speedR2, 0);
    }
    else if ((dist1 <= 6) || (dist2 <= 6))
    {
        analogWrite(speedR1, 40);
        analogWrite(speedR2, 40);
        delay(150);
        analogWrite(speedR1, 0);
        analogWrite(speedR2, 0);
        delay(500);
        analogWrite(speedU1, 150);
        delay(3500);
        analogWrite(speedU1, 0);
        delay(500);
    find_dist:
        digitalWrite(trig3, HIGH);
        delay(10);
        digitalWrite(trig3, LOW);
        dur3 = pulseIn(echo3, HIGH);
        dist3 = (dur3)*0.034 / 2;
        if (dist3 > 15)
        {
            analogWrite(speedR1, 90);
            analogWrite(speedR2, 90);
            delay(200);
            analogWrite(speedR1, 0);
            analogWrite(speedR2, 0);
            goto find_dist;
        }
        else if (10 < dist3 <= 15)
        {
            analogWrite(speedR1, 50);
            analogWrite(speedR2, 50);
            delay(200);
            analogWrite(speedR1, 0);
            analogWrite(speedR2, 0);
            goto find_dist;
        }
        else if (6 < dist3 <= 10)
        {
            analogWrite(speedR1, 50);
            analogWrite(speedR2, 50);
            delay(200);
            analogWrite(speedR1, 0);
            analogWrite(speedR2, 0);
            goto find_dist;
        }
        else
        {
            analogWrite(speedF1, 40);
            analogWrite(speedF2, 40);
            delay(200);
            analogWrite(speedF1, 0);
            analogWrite(speedF2, 0);
            delay(500);
            analogWrite(speedU2, 150);
            delay(3500);
            analogWrite(speedU2, 0);
            delay(200);
            analogWrite(speedF1, 40);
            analogWrite(speedF2, 40);
            delay(100);
            analogWrite(speedF1, 0);
            analogWrite(speedF2, 0);
            digitalWrite(direcU1, HIGH);
            digitalWrite(direcU2, HIGH);
            analogWrite(speedU1, 150);
            analogWrite(speedU2, 150);
            delay(3500);
            analogWrite(speedU1, 0);
            analogWrite(speedU2, 0);
        }
    }
}
