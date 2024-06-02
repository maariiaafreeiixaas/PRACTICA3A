# Pràctica 3

## Pràctica A: Generació d'una pàgina web

### Objectiu
L'objectiu de la pràctica és comprendre el funcionament del WiFi i el Bluetooth en l'ESP32. Es crearà un servidor web i es realitzarà una comunicació sèrie amb una aplicació mòbil utilitzant Bluetooth(Practica3B).

### Codi
Aquest codi configura un servidor web en mode STA, que mostra una pàgina HTML bàsica.

```cpp
#include <WiFi.h>
#include <WebServer.h>

// SSID i Contrasenya
const char* ssid = "*****";       // Introdueix el teu SSID aquí
const char* password = "*****";   // Introdueix la teva contrasenya aquí

WebServer server(80);  // Objecte del WebServer (port HTTP, 80 és per defecte)

//Inicialitza la connexió WiFi amb les credencials proporcionades. Una vegada connectat, mostra la IP de l'ESP32 a la consola sèrie i inicia el servidor HTTP.
void setup() {
  Serial.begin(115200);
  Serial.println("Intentant Connectar a ");
  Serial.println(ssid);

  // Connexió al teu modem wi-fi
  WiFi.begin(ssid, password);

  // Comprova si el wi-fi està connectat a la xarxa wi-fi
  while (WiFi.status() != WL_CONNECTED) {
    delay(1000);
    Serial.print(".");
  }
  Serial.println("");
  Serial.println("WiFi connectat correctament");
  Serial.print("IP obtinguda: ");
  Serial.println(WiFi.localIP());  // Mostra la IP de l'ESP32 al sèrie

  server.on("/", handle_root);
  server.begin();
  Serial.println("Servidor HTTP iniciat");
  delay(100);  
}

//Bucle principal, manté el servidor en funcionament gestionant les peticions dels clients.
Sortides a través de la impressió sèrie:
void loop() {
  server.handleClient();
}

// Contingut HTML i CSS que es mostra al servidor web
String HTML = "<!DOCTYPE html>\
<html>\
<body>\
<h1>La Meva Primera Pàgina amb ESP32 - Mode Estació &#128522;</h1>\
</body>\
</html>";

// Gestiona la url arrel (/)
void handle_root() {
  server.send(200, "text/html", HTML);
}

Sortides a través de la impressió sèrie:

Intentant Connectar a 
*****
........
WiFi connectat correctament
IP obtinguda: 192.168.1.XX
Servidor HTTP iniciat
Visualització de la pàgina web:

Accedint a la IP de la ESP32 des del navegador web, es mostra una pàgina amb el contingut HTML definit.