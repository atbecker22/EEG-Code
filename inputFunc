/*
 Name:		EEG_Input Algorithm
 Created:	2/24/2019 12:01:05 PM
 Author:	Adam Becker
*/

float inputV[20];
float maxima[10];
float amplitude;
float frequency;
unsigned long period[10];

int maxndx = 0;
int maxFlag = 0;

unsigned long timer;
int sensorPin = 26;

// the setup is actually main because I'm a C-code perfectionist
void setup() { 
	timer = millis(); //initialize timer
	while (1) { //do this indefinitely
		int ndx = 0;
		while (ndx < 20) { //do the following 20 times
			if (analogRead(sensorPin)) { //wait until we have a reading from pin A0
				inputV[ndx] = analogRead(sensorPin); //store it in our buffer of 20
				ndx++; //increment base indexing variable
			}
		}
		for (int ndx = 0; ndx < 18; ndx++) { //now do the following 18 times after we have 20 local maxima
			if (inputV[ndx + 1] > inputV[ndx]) { 
				if (inputV[ndx + 1] > inputV[ndx + 2]) { //if we find a local maximum
					maxima[maxndx] = inputV[ndx + 1]; //store it in the array of maxima
					period[maxndx] = timer - millis();  //store the period in the array of periods
					timer = millis(); //merc the timer
					maxndx++; //move max index along 
					if (maxndx == 10) { //if the buffer is full
						for (int i = 1; i < 10; i++) {
							amplitude += inputV[i]; //take the mean average of both arrays
							frequency += period[i];
						}
						frequency = 1 / frequency / 9 / 1000; //calculate the frequency and amplitude from that
						amplitude = amplitude / 9;
						maxndx = 0; //merc the max index
					}
				}
			}
		}
	}
}

// fuck the loop
void loop() {  
	//contemplateSuicide();
}
