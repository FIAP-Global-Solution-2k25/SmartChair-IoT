# 🪑 PosturAI - Sistema de Monitoramento de Postura com Edge Computing
<p align="center">
  <img src="https://img.shields.io/badge/FIAP%20Global%20Solution%202K25-2%C2%BA%20Semestre-blue?style=for-the-badge&logo=github&logoColor=white" alt="Global Solution 2K25 Badge">
</p>

> Repositório oficial do componente de **Edge Computing e Sistemas Embarcados** do projeto PosturAI, desenvolvido para a Global Solution 2K25 da FIAP.

---

## 💡 Sobre o Projeto
O **PosturAI** resolve o problema crescente da má postura em ambientes de trabalho remoto e híbrido, através de uma solução integrada de Inteligência Artificial, Edge Computing e IoT.

O projeto consiste em uma **cadeira inteligente** que monitora ativamente a postura do usuário. Ao detectar um desvio postural por um tempo pré-definido (via análise de vídeo feita pela IA), o sistema envia um comando que aciona um **motor de vibração** embutido na cadeira, fornecendo um *feedback* tátil imediato e discreto para a correção.

### Foco em Edge Computing
A solução implementa o conceito de Edge Computing ao utilizar uma **Máquina Virtual local** (hospedada em Ubuntu Server) para rodar o **Broker MQTT** e o servidor que recebe as requisições da IA de Visão Computacional (PosturAI-Python). Isso garante baixa latência na comunicação e processamento de decisões perto da fonte de dados (o usuário).

---

## ⚙️ Arquitetura do Sistema

O sistema PosturAI é dividido em três camadas principais:

1.  **Visão Computacional (Edge AI):** Módulo em Python que utiliza `opencv` e `mediapipe` para monitorar a postura do usuário em tempo real.
2.  **Nível Intermediário (Broker/Edge):** O servidor na Máquina Virtual (Ubuntu + Mosquitto + Ngrok) atua como um hub central, recebendo comandos da IA e roteando-os para o hardware.
3.  **Hardware (IoT):** O microcontrolador **ESP32** na cadeira, que recebe a instrução do broker MQTT e ativa o circuito do relé/motor de vibração.

O fluxo de dados é: **PosturAI-Python (IA) → Broker MQTT (VM) → ESP32 (Cadeira) → Motor de Vibração.**

[![Diagrama de Arquitetura do Sistema](/diagram.png)](/FIAP-Global-Solution-2k25/Edge-Computing-And-Computer-Systems/blob/main/diagram.png)

---

## 🛠️ Tecnologias e Componentes

| Tipo | Componente | Descrição |
| :--- | :--- | :--- |
| **Hardware Embarcado** | **ESP32** | Microcontrolador responsável pela conectividade Wi-Fi e controle do atuador. |
| **Comunicação** | **MQTT** | Protocolo leve de mensagens utilizado para comunicação entre a IA (Python) e o ESP32, gerenciado pelo Mosquitto. |
| **Infraestrutura** | **Ubuntu Server & VirtualBox** | Sistema Operacional e software de virtualização da máquina que hospeda o Broker na Edge. |
| **Networking** | **Ngrok** | Serviço de túnel utilizado para expor o Broker MQTT local à internet. |
| **Atuador** | **Relé e Motor de Vibração** | Componentes responsáveis por gerar o feedback tátil ao usuário. |
| **Bibliotecas (ESP32)** | `WiFi.h`, `PubSubClient.h` | Bibliotecas padrão para conexão à rede e comunicação MQTT. |

---

## 🚀 Configuração e Uso (Componente ESP32)

Este guia foca na configuração do código que roda no **ESP32** (arquivo `src/main.ino`).

### Pré-requisitos
1.  **Arduino IDE** instalado.
2.  **Placa ESP32** configurada no Gerenciador de Placas da IDE.
3.  **Bibliotecas Instaladas** no Arduino IDE:
    * `WiFi.h` (Geralmente nativa)
    * `PubSubClient.h` (Instalar via Gerenciador de Bibliotecas)

### Passos de Execução
1.  **Clonar o Repositório:**
    ```bash
    git clone [https://github.com/FIAP-Global-Solution-2k25/Edge-Computing-And-Computer-Systems.git](https://github.com/FIAP-Global-Solution-2k25/Edge-Computing-And-Computer-Systems.git)
    ```
2.  **Abrir o Código:** Abra o arquivo `src/main.ino` na Arduino IDE.
3.  **Credenciais de Conexão:** Altere as seguintes variáveis globais no código para as suas credenciais:
    * `default_SSID` e `default_PASSWORD` (Sua rede Wi-Fi).
    * `default_BROKER_MQTT` e `default_BROKER_PORT` (IP e porta do seu Broker MQTT, geralmente o túnel Ngrok).
4.  **Hardware:** Monte o circuito conforme o esquema de fiação (conectando o ESP32 ao relé/motor de vibração).
5.  **Upload:** Compile e faça o upload do código para o seu ESP32.

---

## 🔗 Links Úteis

| Recurso | Descrição | Link |
| :--- | :--- | :--- |
| **Simulação Wokwi** | Simulação online do circuito do ESP32. | [Acessar Simulação](https://wokwi.com/projects/447811277727744001) |
| **Código Principal** | Código-fonte do ESP32/Arduino. | [main.ino](/FIAP-Global-Solution-2k25/Edge-Computing-And-Computer-Systems/blob/main/src/main.ino) |
| **Repositório da Infra** | Referência ao repositório base para a configuração da VM. | [fabiocabrini/fiware](https://github.com/fabiocabrini/fiware) |
| **Documentação ESP32** | Documentação oficial da plataforma. | [Docs ESP32](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/index.html) |

---

## 👥 Participantes
* Prof. Paulo Marcotti (PF2150)
* Arthur Berlofa Bosi (RM564438)
* Arthur Ferreira Alves dos Santos RM564958
* Ulisses Ribeiro Abreu (RM562230)

---

## 📄 Licença
Este projeto está sob a licença **MIT**. Consulte o arquivo [`LICENSE`](/FIAP-Global-Solution-2k25/Edge-Computing-And-Computer-Systems/blob/main/LICENSE) para mais detalhes.

---
