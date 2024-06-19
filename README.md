# MQTT (18/06/2024)

<p align="justify">
O MQTT (Message Queuing Telemetry Transport) é um protocolo de comunicação leve, ideal para dispositivos que requerem eficiência em largura de banda e consumo de energia. Criado nos anos 90 pela IBM, é amplamente usado na Internet das Coisas (IoT), permitindo que sensores e atuadores se comuniquem de forma assíncrona. O MQTT segue um modelo de publicação/assinatura (pub/sub). Os dispositivos se conectam a um broker (servidor) que gerencia as mensagens. Dispositivos podem publicar mensagens em tópicos específicos, e outros dispositivos podem se inscrever nesses tópicos para receber as mensagens relevantes. Essa arquitetura torna o MQTT eficiente e escalável para redes IoT, onde a latência e a confiabilidade são essenciais.
</p>

# MQTT na prática

* <p align="justify"> Publish (Publicar): Dispositivos enviam mensagens para tópicos específicos no broker MQTT. Cada mensagem é enviada para um tópico determinado, organizando a informação de forma clara e acessível. </p>
* <p align="justify"> Subscribe (Assinar): Dispositivos se inscrevem em tópicos para receber mensagens publicadas nesses tópicos. Quando inscritos, os dispositivos recebem automaticamente as mensagens enviadas para esses tópicos.  </p>
* <p align="justify"> Broker MQTT: Servidor que gerencia a comunicação entre dispositivos, recebendo mensagens dos publicadores e distribuindo-as aos assinantes dos tópicos correspondentes. O broker centraliza e organiza a troca de informações. </p>
</p>

## Código comentado

    #include <Arduino.h>         // Biblioteca principal do Arduino
    #include <ESP8266WiFi.h>     // Biblioteca para a conexão WiFi usando ESP8266
    #include <PubSubClient.h>    // Biblioteca para o cliente MQTT
    
    const char* ssid = "Alberto_Zamarchi";        // Nome da rede WiFi
    const char* password = "12345678";   // Senha da rede WiFi
    const char* mqtt_server = "192.168.10.85";  // Endereço do servidor MQTT
    
    WiFiClient espClient;        // Cliente WiFi
    PubSubClient client(espClient);  // Cliente MQTT que usa o cliente WiFi
    const int Relay = D1;        // Define o pino D1 para o relé
    
    void setup_wifi() {          // Função para configurar a conexão WiFi
      delay(10);                 // Pequeno atraso para estabilidade
      Serial.println();          // Linha em branco no Serial Monitor
      Serial.print("Connecting to ");
      Serial.println(ssid);      // Imprime o nome da rede WiFi no Serial Monitor
      WiFi.begin(ssid, password); // Conecta-se à rede WiFi
      while (WiFi.status() != WL_CONNECTED) {  // Espera até a conexão ser estabelecida
        delay(500);
        Serial.print(".");       // Imprime um ponto a cada meio segundo enquanto conecta
      }
      Serial.println("");
      Serial.println("WiFi connected");  // Informa que a conexão foi estabelecida
      Serial.println("IP address: ");
      Serial.println(WiFi.localIP());    // Imprime o endereço IP local
    }
    
    void callback(char* topic, byte* payload, unsigned int length) {  // Função de callback para receber mensagens MQTT
      Serial.print("Message arrived [");
      Serial.print(topic);
      Serial.print("] ");
      String message;
      for (int i = 0; i < length; i++) { 
        Serial.print((char)payload[i]);  // Converte o payload para string
        message += (char)payload[i];
      }
      Serial.println(message);
    
      if (String(topic) == "ControleRelay") {  // Verifica se a mensagem é para o tópico "ControleRelay"
        if (message == "ON") {
          digitalWrite(Relay, LOW);  // Liga o relé (assumindo que LOW é ligar)
        } else if (message == "OFF") {
          digitalWrite(Relay, HIGH); // Desliga o relé (assumindo que HIGH é desligar)
        }
      }
    }
    
    void setup() {
      pinMode(Relay, OUTPUT);    // Define o pino do relé como saída
      digitalWrite(Relay, HIGH); // Desliga o relé inicialmente
      Serial.begin(9600);        // Inicia a comunicação Serial a 9600 bps
      setup_wifi();              // Chama a função para configurar a conexão WiFi
      client.setServer(mqtt_server, 1883);  // Define o servidor MQTT e a porta
      client.setCallback(callback);         // Define a função de callback para mensagens MQTT
    }
    
    void reconnect() {           // Função para reconectar ao servidor MQTT se a conexão for perdida
      while (!client.connected()) {  // Continua tentando até conectar
        Serial.print("Attempting MQTT connection...");
        if (client.connect("ESP8266Client")) {  // Tenta conectar ao servidor MQTT
          Serial.println("connected");
          client.subscribe("ControleRelay");  // Inscreve-se no tópico "ControleRelay"
        } else {
          Serial.print("failed, rc=");
          Serial.print(client.state());  // Imprime o estado da conexão
          Serial.println(" try again in 5 seconds");
          delay(5000);  // Espera 5 segundos antes de tentar novamente
        }
      }
    }
    
    void loop() {
      if (!client.connected()) {  // Verifica se o cliente MQTT está conectado
        reconnect();  // Tenta reconectar se não estiver conectado
      }
      client.loop();  // Mantém a conexão MQTT viva e processa mensagens
    }


# Sistemas Embarcados RTOS (04/06/2024)

## Esqeumatico
![DZFBXFGB](https://github.com/AlbertoZamarchi/SISTEMAS_EMBARCADOS_RTOS/assets/107437069/563a9ae5-7a2a-4acc-b2cc-9e2a8f44f8ab)

## PCD
![DBFXGCGFBG](https://github.com/AlbertoZamarchi/SISTEMAS_EMBARCADOS_RTOS/assets/107437069/34f790a7-ac1b-4aa4-aa6d-9e28ebfe8160)

## 3D
![FSZDFVDXFV](https://github.com/AlbertoZamarchi/SISTEMAS_EMBARCADOS_RTOS/assets/107437069/ada41ec4-bba3-40dc-bd2c-bab7b576fc29)
