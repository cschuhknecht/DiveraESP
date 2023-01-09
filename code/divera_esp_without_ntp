#include <ESP8266WiFi.h> //library provides ESP8266 specific WiFi methods we are calling to connect to network
#include <ESP8266HTTPClient.h> //library provides ESP8266 specific http methods
//#include <WiFiClient.h> // additional and unused Wifi Library


const char* ssid = "xxx"; // your wifi ssid
const char* password = "xxx"; // your wifi password

//Your Domain name with URL path or IP address with path (use http instead of https)
const char* serverName = "http://www.divera247.com/api/xxx";

// The setup runs only ones. Its used for wifi connection.
void setup() {
  Serial.begin(115200); // initialize serial (text) output

  WiFi.begin(ssid, password); // connect to wifi
  Serial.println("Connecting");
  while(WiFi.status() != WL_CONNECTED) { // wait for wifi connection
    delay(500);
    Serial.print(".");
  }
  Serial.println("");
  Serial.print("Connected to WiFi network with IP Address: ");
  Serial.println(WiFi.localIP());

}

// The loop runs multiple times. But I blocked that with a huge delay at the end.
void loop() {

  String httpRequestData;
  httpRequestData = "type=Einsatz";

  Serial.print(", Alarmtyp: ");
  Serial.println(httpRequestData);


  //Check WiFi connection status
  if(WiFi.status()== WL_CONNECTED){ // Ask if wifi is still connected because if not the following would be unnessesary
    HTTPClient http; // initialize http client with the simple name http

    // Your Domain name with URL path or IP address with path
    http.begin(serverName);

    // Specify content-type header
    http.addHeader("Content-Type", "application/x-www-form-urlencoded");

    // Send HTTP POST request
    int httpResponseCode = http.POST(httpRequestData);
    // Get http payload
    String payload = http.getString();
    // print response and payload
    Serial.print("HTTP Response code: ");
    Serial.println(httpResponseCode);
    Serial.print("Payload: ");
    Serial.println(payload);

    // Free resources
    http.end();

  }
  else {
    Serial.println("WiFi Disconnected");
  }
  delay(300000); // huge delay - blocks loop

}
