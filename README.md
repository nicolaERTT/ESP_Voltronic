# ESP_Voltronic
Collegare Inverter Voltronic a Home Assistant senza MQTT con ESPHome
https://www.pcloft.it/android/162-collegare-inverter-voltronic-a-homeassistant-senza-mqtt-esphome

**Collegare Inverter Voltronic a Home Assistant senza MQTT con ESPHome**

Questa guida e' rivolta a tutti coloro che vogliono monitorare da remoto il loro inverter Voltronic o "similari" attraverso il cellulare o il pc in maniera semplice senza bisogno di MQTT , completamente Wi-Fi e con tantissime potenzialita' :

**Prerequisiti :**

Istanza Home Assistant Installation - Home Assistant (home-assistant.io) installata per esempio : raspberry, miniPC, macchina virtuale ecc...
![ras](https://github.com/user-attachments/assets/8147a74f-9b06-45e4-8389-261e35d54be9)


Inverter Voltronic o similare che abbiano la porta di comunicazione RS-232 ( porta PC - porta RJ45 )
 ![porta rs232](https://github.com/user-attachments/assets/2c6ff71c-67b2-47e0-bce9-db8b022bcf91)

**Progetto:**

L'idea nasce dal fatto che all'interno degli Inverter Voltronic che hanno già integrata la scheda Wi-FI , e che quindi hanno la possibilità di essere monitorati attraverso le varie APP e il sito https://www.dessmonitor.com/ , esiste (per effettuare questa connessione) una schedina ESP32 (veramente una ESP8266) che ha a bordo un firmware ed una chiave API che ne consentono l'autenticazione sui "server Voltronic".

Da questo, girando in rete, abbiamo realizzato di poter fare la stessa cosa con un server locale dedicato, ma ancora più semplicemente di acquisire i dati su una piattaforma come Homeassistant.

**Documentazione :**

Istruzioni ESPHome dedicate per inverter: [PipSolar PV Inverter — ESPHome](https://esphome.io/components/pipsolar.html)

Pagina GitHub di riferimento : [GitHub - syssi/esphome-pipsolar: ESPHome component to monitor and control a pipsolar inverter via RS232](https://github.com/syssi/esphome-pipsolar?tab=readme-ov-file)

Pin-Out per collegamenti: https://powerforum.co.za/topic/10589-esphome-axpert-5k-rs232-pinout/  e anche  https://github.com/syssi/esphome-pipsolar/issues/3

Piedinatura dei vari modelli di ESP32 ESP8266: https://randomnerdtutorials.com/esp8266-pinout-reference-gpios/

Procedura in italiano per installare il componente aggiuntivo ESPHome su homeassistant : https://www.mauroalfieri.it/informatica/esphome-installazione-su-home-assistant.html
 

**Componenti necessari :**

Modulo ESP32 ( questo è il più piccolo ed economico D1 mini ESP8266 )

<img width="500" height="2400" alt="modulo_D1" src="https://github.com/nicolaERTT/ESP_Voltronic/blob/main/diagrammaD1.jpg" />

Modulo conversione RS232 in TTL per ESP32

<img width="250" height="2400" alt="RS232" src="https://github.com/nicolaERTT/ESP_Voltronic/blob/main/rs232.jpg" />

Modulo di alimentazione diretta da Inverter ( preleva i 12V dal piedino n.4 dell'Inverter e lo converte in 3.3V per il circuito ESP32 )

<img width="200" height="2400" alt="Modulo_3V" src="https://github.com/nicolaERTT/ESP_Voltronic/blob/main/modulo3_3V.jpg" />


**Cablaggi :**

 ![schema1](https://github.com/user-attachments/assets/750ca7e9-894d-46a3-85ba-90116ecd3afc)

<img width="300" height="2400" alt="Pin_12Vb" src="https://github.com/nicolaERTT/ESP_Voltronic/blob/main/pin_12vb.jpg" />   .   <img width="250" height="2400" alt="ESP_Real" src="https://github.com/nicolaERTT/ESP_Voltronic/blob/main/esp_real.jpg" /> 
 
**Programmazione:**

Una volta cablate le varie schedine, e inizializzato l'ESP8266 come da documentazione , è sufficiente andare nel menu ESPHome e dal link EDIT aggiungere il codice come qui :

https://github.com/syssi/esphome-pipsolar/blob/main/esp8266-example.yaml



ovviamente adattandolo alle proprie esigenze, ad esempio inserendo od escludendo dei parametri per noi interessanti ( inserendo o cancellando il simbolo # davanti alle linee di codice si esclude/include il sensore ) .

Consigliamo di eliminare tutta la parte MQTT broker che a noi non interessa, lasciare invece attiva la parte "api" che dovrebbe essere gia' presente nel file ( cosi come la parte wifi ) e di eliminare la parte "switch" che potrebbe dare problemi.

PS: Tutti gli aggiornamenti che faremo da ora in avanti saranno caricati via Wi-Fi in quanto il collegamento dell'ESP via USB va fatto solo la prima volta per inizializzarlo!

**Monitoraggio Remoto Inverter dalla APP Homeassistant :**

Ora le impostazioni dei pannelli di controllo, AUTOMAZIONI e personalizzazioni sono infinite, dal controllo di "EVENTI" particolari in base al carico o alla produzione, l'invio di notifiche (anche vocali tramite script), grafici, consumi, statistiche, ecc...

Qui qualche screen dalla app di esempio:

<img width="300" height="2400" alt="Screenshot_20240329-081711" src="https://github.com/user-attachments/assets/edd7e484-1cd0-4c80-a276-b1044f50900c" />
<img width="300" height="2400" alt="Screenshot_20240329-081735" src="https://github.com/user-attachments/assets/0fbdf288-0627-475b-be37-f12ada1d0b5e" />
<img width="300" height="2400" alt="Screenshot_20240329-081807" src="https://github.com/user-attachments/assets/2e553d71-a7fc-41d7-8bb4-60dc574cf785" />

      

mail : info@pcloft.it

.
