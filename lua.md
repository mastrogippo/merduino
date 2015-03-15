
```
// test USB Linux Magazine Pinguino
// Jean-Pierre MANDON 2008

int i;
uchar caractere,caractere1;

void setup() 
{
for (i=0;i<16;i++) 
	{
		pinMode(i,OUTPUT);

//	pinMode(i,OUTPUT);
//	digitalWrite(i,LOW);
	}
}

void loop() 
{
	uchar ch1, ch2, tmp, pin;
	unsigned int tmpi;
	if (USB.available())
	{
		//TODO: LED on off?

		ch1 = USB.read();
		if(ch1=='U') if (USB.available())
		{
			ch1 = USB.read();
			if (USB.available())
				tmp = USB.read();
    
    pin = tmp; //0-9A-F
    if((pin >= 0x61) && (pin <= 0x66)) //toUpper
        pin -= 0x20;
    if(pin >= 0x41) pin -= 7;
			pin -= 0x30;
    
			switch(ch1)
			{
				//set mode
				case 's': pinMode(pin, INPUT); break;
				case 'S': pinMode(pin, OUTPUT); break;

				//case 'P': //TODO: pwm?? in teoria basta scrivere... pinMode(ch2, INPUT); break;
				//case 'A': //TODO: analog?? in teoria basta leggere... pinMode(ch2, INPUT); break;
				
				//PWM
				case 'p':
				case 'P': 
					if (USB.available())
					{
						tmpi = USB.read();
						analogWrite(pin, tmpi << 2); //TODO: risoluzione 2 byte?
					}
				//iNvert
				case 'n':
				case 'N': digitalWrite(pin, digitalRead(pin)^1); break;
				//set high or low
				case 'w': digitalWrite(pin, 0); break;
				case 'W': digitalWrite(pin, 1); break;
				//read
				case 'R': tmp = digitalRead(pin); //TODO: usbwrite...? break;
				case 'a':
				case 'A': tmpi = analogRead(pin); //TODO: usbwrite...? break;

				//TODO: Serial, I2C, SPI........

			}
			/*if (caractere=='W') if (USB.available())
			{
			caractere1=USB.read()-0x30;
			digitalWrite(caractere1,digitalRead(caractere1)^1);
			}*/
		}
	}
}
```