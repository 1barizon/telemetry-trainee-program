# BOM - Lista de Componentes

Componentes usados ao longo do treinamento.

## Eletrônica

| Componente | Quantidade | Onde é usado |
|---|---|---|
| ESP32-C3 Super Mini | 1 | Semanas 3 a 9 |
| BMP280 (ou BME280) | 1 | Semanas 3 a 7 |
| LED 5mm | 1 | Semanas 3, 5 e 6 |
| Resistor 220Ω | 1 | Para o LED |
| Resistor 10kΩ | 2 | Pull-up I2C |
| Botão tátil | 1 | Semana 3 (extra) |
| Buzzer ativo 5V | 1 | Semana 3 (extra) |
| Micro servo MG92B | 1 | Semana 3 (extra) |
| Protoboard 400 pontos | 1 | Todas as semanas |
| Jumpers macho-macho | 20 | Todas as semanas |
| Jumpers macho-fêmea | 10 | Sensor → protoboard |
| Cabo USB-C | 1 | Programação do ESP32 |

## Ferramentas

| Ferramenta | Versão | Onde é usado |
|---|---|---|
| Arduino IDE | 2.x | Semanas 3 e 4 |
| Wokwi (web) | — | Semana 4 (chips personalizados) |
| VS Code | Última | Todas |
| PlatformIO (extensão) | Última | Semana 5 em diante |
| KiCad | 8+ | Semana 7 |
| Python | 3.10+ | Semanas 1, 2, 6, 9 |
| Git | 2.x | Todas |

## Pinagem (ESP32-C3 Super Mini)

| GPIO | Componente | Semana |
|---|---|---|
| GPIO 0 | Buzzer | Extra |
| GPIO 1 | LED | 3, 5, 6 |
| GPIO 2 | Botão | Extra |
| GPIO 3 | Servo | Extra |
| GPIO 4 | I2C SDA (BMP280) | 3, 5, 6 |
| GPIO 5 | I2C SCL (BMP280) | 3, 5, 6 |
