# traffic-signals-node
#include <WiFi.h>
#include <HTTPClient.h>

const char* ssid = "YOUR_WIFI_SSID";
const char* password = "YOUR_WIFI_PASSWORD";
const char* server = "http://192.168.X.X/trigger_signal";

void setup() {
  Serial.begin(115200);
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) {
    delay(1000);
  }
}

void loop() {
  if (Serial.available() > 0) {
    HTTPClient http;
    http.begin(server);
    http.addHeader("Content-Type", "application/json");
    http.POST("{\"ambulance_status\":\"stuck\"}");
    http.end();
    delay(5000);
  }
}
