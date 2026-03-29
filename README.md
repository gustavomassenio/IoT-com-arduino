# Estudo sobre algumas maneiras de usar o arduino junto a um roteador.

# 🌐 Arduino Ethernet Web Server

Projeto utilizando **Arduino Uno + Ethernet Shield** para criar um servidor web local, capaz de responder requisições HTTP diretamente pela rede.

---

## 📌 Descrição

Este projeto demonstra como conectar um Arduino à rede utilizando um **Ethernet Shield** e hospedar um servidor web simples.

O endereço IP é atribuído automaticamente via **DHCP**, permitindo acesso ao servidor pelo navegador.

---

## 🛠️ Tecnologias Utilizadas

- Arduino Uno
- Ethernet Shield (W5100/W5500)
- Linguagem C++ (Arduino)
- Protocolo HTTP
- DHCP (Dynamic Host Configuration Protocol)

#
 ![roteador_e_arduino](roteador_e_arduino.jpeg)

---

## ⚙️ Funcionamento

1. O Arduino inicia a comunicação via Ethernet
2. Solicita um endereço IP ao roteador (DHCP)
3. Inicia um servidor web na porta 80
4. Exibe as configurações de rede no Serial Monitor
5. Responde requisições HTTP com uma página simples


 
---

## 📡 Como funciona
 - O Arduino solicita um IP ao roteador usando DHCP
 - O roteador atribui automaticamente um IP disponível
 - O IP pode ser visualizado pelo Serial Monitor

## 🔍 Descobrindo o IP do Arduino

Você pode descobrir o IP de duas formas:

1. Pelo Serial Monitor

Ao iniciar, o Arduino imprime:

IP: 192.168.0.238
2. Pelo roteador (DHCP)

No painel do roteador:

Acesse a lista de clientes DHCP
Procure pelo MAC Address configurado no código

Exemplo:

MAC: 90-A2-DA-56-B3-D1
IP: 192.168.0.238
📌 Reserva de IP (Recomendado)

Para evitar que o IP mude:

Configure uma reserva de IP no roteador
Associe o MAC Address ao IP desejado

Isso garante que o Arduino sempre terá o mesmo IP.

![clientesdhcp](clientesdhcp.jpeg)

🌍 Acessando o servidor

Após obter o IP, basta acessar no navegador:

![webserver](webserver.jpeg)

## 💻 Código

```cpp
#include <SPI.h>
#include <Ethernet.h>

// Definição do MAC Address (deve ser único na rede)
byte mac[6] = { 0x90, 0xA2, 0xDA, 0x50, 0x70, 0xB1 };

// Inicializa servidor HTTP na porta 80
EthernetServer server(80);

void setup() {
  Serial.begin(9600);

  // Inicializa conexão via DHCP
  Ethernet.begin(mac);

  // Inicia o servidor
  server.begin();

  // Exibe informações de rede
  Serial.println("Arduino Ethernet Web Server");

  Serial.print("IP: ");
  Serial.println(Ethernet.localIP());

  Serial.print("Mascara: ");
  Serial.println(Ethernet.subnetMask());

  Serial.print("Gateway: ");
  Serial.println(Ethernet.gatewayIP());

  Serial.print("DNS: ");
  Serial.println(Ethernet.dnsServerIP());
}

void loop() {
}





