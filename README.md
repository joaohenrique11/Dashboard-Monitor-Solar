# ☀️ Monitor Solar - Dashboard ThingSpeak

O **Monitor Solar** é uma interface web simples para monitorar e visualizar em tempo real os dados de geração de energia fornecidos por um painel solar. 

Os dados são lidos em campo por um microcontrolador **ESP32** via barramento **RS-485** (utilizando sensores/medidores de energia dedicados), enviados para a plataforma IoT **ThingSpeak** e consumidos automaticamente por este painel de controle.

---

## 🚀 Funcionalidades

* **Mostrador Analógico (Arc Gauge):** Exibe a potência gerada instantaneamente em Watts (W), com cálculo proporcional de escala ajustável.
* **Métricas Principais:** Leituras em tempo real de **Tensão (V)**, **Corrente (mA)** e **Energia Acumulada (Wh)**.
* **Gráficos em Tempo Real:**
  * **Tensão x Corrente:** Gráfico de eixo duplo permitindo comparar variações simultâneas de V e mA.
  * **Potência Gerada:** Histórico de consumo instantâneo em mW.
  * **Energia Acumulada:** Histórico de consumo energético em Wh.
* **Atualização Automática:** Sincronização periódica a cada 20 segundos para acompanhar a frequência do firmware do ESP32.
* **Persistência Local:** Salva as configurações do canal (ID e API Key) diretamente no navegador (`localStorage`), sem necessidade de reconfigurar a cada acesso.

---

## 🛠️ Tecnologias Utilizadas

* **HTML5 / CSS3** (Design responsivo e paleta de cores temática)
* **JavaScript ES6+** (Consumo da API REST do ThingSpeak)
* **Chart.js v4.4.4** (Renderização dos gráficos)
* **ThingSpeak API** (Broker/Plataforma IoT)

---

## 📡 Mapeamento dos Dados no ThingSpeak

Para que a interface exiba os dados corretamente, o firmware do ESP32 deve enviar as leituras para o ThingSpeak nos seguintes campos (Fields):

| Campo (`Field`) | Dado Representado | Unidade |
| :--- | :--- | :--- |
| **Field 1** | Tensão | Volts (V) |
| **Field 2** | Corrente | Miliamperes (mA) |
| **Field 3** | Potência Instantânea | Miliwatts (mW) |
| **Field 4** | Energia Acumulada | Watt-hora (Wh) |

---

## ⚙️ Como Usar

1. Faça o download ou clone este repositório.
2. Abra o arquivo `index.html` em qualquer navegador de sua preferência.
3. Clique em **⚙️ Configurar canal do ThingSpeak**:
   * **Channel ID:** Digite o ID do seu canal no ThingSpeak.
   * **Read API Key:** Informe sua chave de leitura (necessário apenas se o seu canal for privado).
   * **Potência máxima do painel (W):** Defina a potência máxima nominal das suas placas solares para ajustar o limite do ponteiro visual.
4. Clique em **Salvar e conectar**.

---

## 📐 Arquitetura do Sistema

```text
[Placa Solar] ──> [Medidor / Módulo RS-485] ──(RS-485)──> [ESP32]
                                                            │
                                                          (Wi-Fi)
                                                            │
                                                            ▼
                                                   [ThingSpeak Cloud]
                                                            │
                                                          (HTTP API)
                                                            │
                                                            ▼
                                                   [Monitor Solar Web UI]