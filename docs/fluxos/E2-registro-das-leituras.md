# Fluxo do E2 Registro das leituras

**Feito quando da Entrega 1:** Após uma leitura do sensor, o sistema armazena a data e os valores de CO₂, temperatura e umidade, que permanecem disponíveis para consulta posterior.

## Passos

1. O Coordenador Pedagógico mantém o ambiente sob monitoramento.
2. O Dispositivo IoT publica uma nova leitura válida no Broker MQTT por meio de CT1 `publicarLeitura`.
3. O Broker MQTT encaminha a leitura ao Backend por meio de CT2 `entregarLeitura`.
4. O Backend valida os campos e determina a situação do nível de CO₂.
5. O Backend grava a leitura na tabela `medicao` utilizando CT3.
6. O Banco confirma a gravação e a medição fica disponível para consultas posteriores.

## Diagrama

```mermaid
sequenceDiagram
    actor Coordenador as Coordenador Pedagógico
    participant IoT as Dispositivo IoT
    participant Broker as Broker MQTT
    participant Backend
    participant Banco
    Coordenador->>IoT: Mantém o ambiente monitorado
    IoT->>Broker: CT1 publicarLeitura
    Broker->>Backend: CT2 entregarLeitura
    Backend->>Backend: Valida e classifica a leitura
    Backend->>Banco: CT3 medicao
    Banco-->>Backend: Gravação confirmada
```

**Contratos usados:** CT1 `publishReading`, CT2 `sensor_reading`

