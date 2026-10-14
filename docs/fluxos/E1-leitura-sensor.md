# Fluxo: Leitura e Publicação de Dados do Sensor de CO₂

Feito quando: O dispositivo IoT realiza a leitura da qualidade do ar (CO₂, temperatura e umidade) via sensor SCD30 e publica os dados na rede de forma automatizada.

## Passos

1. O Dispositivo IoT (ESP32) coleta ciclicamente os dados de CO₂, temperatura e umidade através do sensor SCD30 via barramento I2C.
2. O ESP32 formata os dados coletados em um objeto JSON contendo o ID do dispositivo, as métricas e o carimbo de data/hora.
3. O ESP32 publica a mensagem MQTT no tópico correspondente através da rede. (CT5)
4. O Broker MQTT recebe a mensagem e a distribui instantaneamente para todos os módulos assinantes.
5. O Backend consome a mensagem enviada pelo broker e realiza a validação e o armazenamento dos registros no banco de dados.

## Diagramas e Contratos

```mermaid
sequenceDiagram
    participant IoT as Dispositivo IoT (ESP32)
    participant Broker as Broker MQTT
    participant Backend as Backend
    
    IoT->>Broker: CT5 publicarLeitura (MQTT)
    Broker->>Backend: Repassa dados da telemetria
