# MQTT (18/06/2024)

<p align="justify">
O MQTT (Message Queuing Telemetry Transport) é um protocolo de comunicação leve, ideal para dispositivos que requerem eficiência em largura de banda e consumo de energia. Criado nos anos 90 pela IBM, é amplamente usado na Internet das Coisas (IoT), permitindo que sensores e atuadores se comuniquem de forma assíncrona. O MQTT segue um modelo de publicação/assinatura (pub/sub). Os dispositivos se conectam a um broker (servidor) que gerencia as mensagens. Dispositivos podem publicar mensagens em tópicos específicos, e outros dispositivos podem se inscrever nesses tópicos para receber as mensagens relevantes. Essa arquitetura torna o MQTT eficiente e escalável para redes IoT, onde a latência e a confiabilidade são essenciais.
</p>

# MQTT na prática

* Publish (Publicar): Dispositivos enviam mensagens para tópicos específicos no broker MQTT. Cada mensagem é enviada para um tópico determinado, organizando a informação de forma clara e acessível.
* Subscribe (Assinar): Dispositivos se inscrevem em tópicos para receber mensagens publicadas nesses tópicos. Quando inscritos, os dispositivos recebem automaticamente as mensagens enviadas para esses tópicos.
* Broker MQTT: Servidor que gerencia a comunicação entre dispositivos, recebendo mensagens dos publicadores e distribuindo-as aos assinantes dos tópicos correspondentes. O broker centraliza e organiza a troca de informações.

# SISTEMAS_EMBARCADOS_RTOS (04/06/2024)

## Esqeumatico
![DZFBXFGB](https://github.com/AlbertoZamarchi/SISTEMAS_EMBARCADOS_RTOS/assets/107437069/563a9ae5-7a2a-4acc-b2cc-9e2a8f44f8ab)

## PCD
![DBFXGCGFBG](https://github.com/AlbertoZamarchi/SISTEMAS_EMBARCADOS_RTOS/assets/107437069/34f790a7-ac1b-4aa4-aa6d-9e28ebfe8160)

## 3D
![FSZDFVDXFV](https://github.com/AlbertoZamarchi/SISTEMAS_EMBARCADOS_RTOS/assets/107437069/ada41ec4-bba3-40dc-bd2c-bab7b576fc29)
