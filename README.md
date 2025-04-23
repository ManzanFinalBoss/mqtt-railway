# 🛰️ MQTT Broker com Mosquitto (Docker + Railway)

Este projeto implementa um broker MQTT baseado no [Mosquitto](https://mosquitto.org/), hospedado gratuitamente em nuvem (ex: Railway, Fly.io, etc), permitindo comunicação entre dispositivos via protocolo MQTT em tempo real.

---

## 🚀 Objetivo

Oferecer um broker MQTT acessível pela internet para testes e integração com microcontroladores, sensores, CLPs ou aplicações Python.

---

## 🧱 Estrutura do Projeto

- `Dockerfile`: Define a imagem Docker baseada no Mosquitto.
- `mosquitto.conf`: Arquivo de configuração do broker.
  - `listener 1883 0.0.0.0`
  - `allow_anonymous true`
  - Persistência de dados ativada

---

## 🌐 Configurações de Acesso (exemplo genérico)

- **Host:** `mqtt.seubroker.com`
- **Porta:** `PORTA`
- **Protocolo:** MQTT (sem SSL)
- **Autenticação:** Desativada (modo anônimo)

---

## ⚙️ Configuração no MQTTX

1. Abra o MQTTX e clique em **"+"** para criar nova conexão.
2. Preencha os campos:

| Campo        | Valor                    |
|--------------|--------------------------|
| Name         | `Meu Broker MQTT`        |
| Protocol     | `mqtt://`                |
| Host         | `mqtt.seubroker.com`     |
| Port         | `PORTA`                  |
| Clean Session| `true`                   |
| SSL/TLS      | `Desativado (OFF)`       |
| Username     | *(em branco)*            |
| Password     | *(em branco)*            |

3. Clique em **Connect**

---
## 📤 Publicar em um tópico (enviar dados)
-Clique em “Publish”
-Tópico: meutopico/sinal
-Payload: 1 ou {"status": "ativo"}
-QoS: 0
### Usando terminal
mosquitto_pub -h mqtt.seubroker.com -p PORTA -t "meutopico/sinal" -m "mensagem aleatória"

---

## 📥 Assinar um tópico (receber dados)

### Usando MQTTX

- Crie uma nova subscription
- Tópico: `meutopico/#`
- QoS: 0

### Usando terminal

```bash
mosquitto_sub -h mqtt.seubroker.com -p PORTA -t "meutopico/#"

