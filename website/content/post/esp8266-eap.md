+++
slug = "esp8266-eap"
author = ""
comments = true
image = ""
tags = ["ESP8266",""]
title = "Get an ESP8266 on a network using WPA EAP"
draft = false
menu = ""
share = true
date = "2017-03-10T14:51:56+01:00"

+++

## Steps for WPA EAP with ESP8266
Here is a summary of what I did in order to get the Arduino-module connecting to a network secured with WPA EAP.  
Details are duscussed in https://github.com/esp8266/Arduino/issues/1032  
And the solution was provided by https://github.com/ninjabe86 and https://github.com/adriencapaine   


1. Assuming a working Arduino IDE or similar environment  
2. Get the experimental branch update_sdk_2.0.0 from the repo https://github.com/esp8266/Arduino.git  
3. Replace the existing library in .../packages/esp8266/hardware/esp8266 with this branch  
4. Modify the file libwpa2.a (in .../packages/esp8266/hardware/esp8266/2.3.0/tools/sdk/lib):  
	Using a hex editor(i.e. vi), replace anonymous@espressif.com with your mail address, fill the spare positions with . (periods)  
5. Include this code  

{{< highlight cpp >}}
extern "C" {
  #include "user_interface.h"
  #include "wpa2_enterprise.h"
}
/*******************************************************************/
#define SERIAL_BAUD_RATE      57600
#define STARTUP_DELAY_MS      1000
/*******************************************************************/
// SSID to connect to
static const char* ssid = "ssidname";
// Username for authentification
static const char* username = "identity";
// Password for authentification
static const char* password = "password";
{{< /highlight >}}


...

{{< highlight cpp >}}
  Serial.begin(SERIAL_BAUD_RATE);
  delay(STARTUP_DELAY_MS);

  // Setting ESP into STATION mode only (no AP mode or dual mode)
  wifi_set_opmode(STATION_MODE);

  struct station_config wifi_config;

  memset(&wifi_config, 0, sizeof(wifi_config));
  strcpy((char*)wifi_config.ssid, ssid);

  wifi_station_set_config(&wifi_config);

  wifi_station_clear_cert_key();
  wifi_station_clear_enterprise_ca_cert();

  wifi_station_set_wpa2_enterprise_auth(1);
  wifi_station_set_enterprise_username((uint8*)username, strlen(username));
  wifi_station_set_enterprise_password((uint8*)password, strlen(password));

  wifi_station_connect();

  // Wait for connection AND IP address from DHCP
  while (WiFi.status() != WL_CONNECTED) {
    delay(2000);
    Serial.print(".");
  }

  // Now we are connected
  Serial.println("");
  Serial.println("WiFi connected");
  Serial.println("IP address: ");
  Serial.println(WiFi.localIP());
{{< /highlight >}}


