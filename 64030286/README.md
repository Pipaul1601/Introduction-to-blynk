![image](https://github.com/Pipaul1601/Introduction-to-blynk/assets/115067018/0b78c497-2309-4701-90e1-8cee0fc1b55b)


https://drive.google.com/file/d/16o90N0n710GP0rZ5gixei6GQBJvfW3Nx/view?usp=drive_link

		
	 
	
	 /*************************************************************
	
	  This is a simple demo of sending and receiving some data.
	  Be sure to check out other examples!
	 *************************************************************/
	
	/* Fill-in information from Blynk Device Info here */
	#define BLYNK_TEMPLATE_ID           "TMPL6jtwXGEVm"
	#define BLYNK_TEMPLATE_NAME         "Quickstart Template"
	#define BLYNK_AUTH_TOKEN            "zIS8u4ClfWINMNfj-_PW7Wbhra4lHjfu"
	
	/* Comment this out to disable prints and save space */
	#define BLYNK_PRINT Serial
	
	
	#include <WiFi.h>
	#include <WiFiClient.h>
	...032 #include <BlynkSimpleEsp32.h>
	
	// Your WiFi credentials.
	// Set password to "" for open networks.
	char ssid[] = "Areena's iphone";
	char pass[] = "Treasure12";
	
	BlynkTimer timer;
	
	// This function is called every time the Virtual Pin 0 state changes
	BLYNK_WRITE(V0)
	{
	  // Set incoming value from pin V0 to a variable
	  int value = param.asInt();
	
	  // Update state
	  Blynk.virtualWrite(V1, value);
	}
	
	// This function is called every time the device is connected to the Blynk.Cloud
	BLYNK_CONNECTED()
	{
	  // Change Web Link Button message to "Congratulations!"
	  Blynk.setProperty(V3, "offImageUrl", "https://static-image.nyc3.cdn.digitaloceanspaces.com/general/fte/congratulations.png");
	  Blynk.setProperty(V3, "onImageUrl",  "https://static-image.nyc3.cdn.digitaloceanspaces.com/general/fte/congratulations_pressed.png");
	  Blynk.setProperty(V3, "url", "https://docs.blynk.io/en/getting-started/what-do-i-need-to-blynk/how-quickstart-device-was-made");
	}
	
	// This function sends Arduino's uptime every second to Virtual Pin 2.
	void myTimerEvent()
	{
	  // You can send any value at any time.
	  // Please don't send more that 10 values per second.
	  Blynk.virtualWrite(V2, millis() / 1000);
	}
	
	void setup()
	{
	  // Debug console
	  Serial.begin(115200);
	
	  Blynk.begin(BLYNK_AUTH_TOKEN, ssid, pass);
	  // You can also specify server:
	  //Blynk.begin(BLYNK_AUTH_TOKEN, ssid, pass, "blynk.cloud", 80);
	  //Blynk.begin(BLYNK_AUTH_TOKEN, ssid, pass, IPAddress(192,168,1,100), 8080);
	
	  // Setup a function to be called every second
	  timer.setInterval(1000L, myTimerEvent);
	}
	
	void loop()
	{
	  Blynk.run();
	  timer.run();
	  // You can inject your own code or combine it with other sketches.
	  // Check other examples on how to communicate with Blynk. Remember
	  // to avoid delay() function!
	}
