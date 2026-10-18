# Semana 9 (extra) - Simulação do computador de bordo no Wokwi

> **Status: esqueleto / rascunho.** Esta semana ainda não está no cronograma oficial de 8 semanas. Os itens marcados com `TODO` precisam ser definidos antes de aplicar.

## Objetivo

Montar o computador de bordo (ESP32-S3 + BMP585 + LSM6DS3 + NEO-8M) no [Wokwi](https://wokwi.com/) usando os custom chips do repositório, rodar um firmware que gere a telemetria e analisar o log gerado.

## Preparação

- [ ] Semanas 1 e 2 concluídas (pandas/Colab e parser -> CSV tratado)
- [ ] Conta no [Wokwi](https://wokwi.com/)
- [ ] Ler o [README dos chips](../../entregas/dados/wokwi-chips/README.md)
- [ ] (Opcional) Semana 3 concluída (Arduino IDE)

## Contexto

TODO: texto curto explicando por que simulamos o computador de bordo (validar firmware e pipeline de telemetria antes do voo, sem depender do hardware físico).

A ideia é fechar o ciclo do treinamento:

```
sensores (Wokwi) -> firmware (ESP32-S3) -> log cru -> parser -> CSV tratado -> gráficos (Colab)
```

## Kit de simulação

Os custom chips estão em [`entregas/dados/wokwi-chips/`](../../entregas/dados/wokwi-chips/):

| Chip | Pasta | Interface | Endereço / Baud |
|------|-------|-----------|-----------------|
| BMP585 (barômetro) | `bmp585/` | I2C | `0x7E` (ajustável) |
| LSM6DS3 (IMU) | `lsm6ds3/` | I2C | `0x6B` (ajustável) |
| NEO-8M (GPS) | `neo-8m/` | UART | `9600` baud |

Ligação (baseada no `config.h` do computador de bordo) - veja `wokwi-chips/diagram-exemplo.json`:

| Sensor | Sinal | ESP32-S3 |
|--------|-------|----------|
| BMP585 | SDA / SCL | GPIO 8 / GPIO 9 |
| LSM6DS3 | SDA / SCL | GPIO 8 / GPIO 9 |
| NEO-8M | TX / RX | GPIO 17 / GPIO 18 |

## Tarefas (rascunho)

1. **Montar o circuito**: criar o projeto no Wokwi (ESP32-S3) e importar os três chips e o `diagram-exemplo.json`. TODO: definir se os alunos devem montar do zero ou partir do exemplo.
2. **Firmware**: ler os três sensores e enviar a telemetria pela serial no formato do computador de bordo. TODO: definir o formato exato do pacote (o do onboard computer usa 24 campos `ID,millis,pckt,...`; o da Semana 3 usa `#timestamp_ms;alt;temp;pressao#`).
3. **Log**: salvar um trecho do log serial cru (como o `voo_thonyan.txt` da Semana 2). TODO: definir duração e como o aluno exporta o log.
4. **Parser**: processar o log com o parser da Semana 2 e gerar o `dados_tratados.csv`.
5. **Análise**: abrir o CSV no Colab (Semana 1) e gerar os gráficos (aceleração, velocidade, altitude).

TODO: decidir quais tarefas são obrigatórias e quais são extras.

## Formato do pacote

TODO: especificar o formato exato que o firmware deve enviar (campos, separador, taxa de amostragem).

## Critérios de aceite (rascunho)

- [ ] Projeto no Wokwi com ESP32-S3 + BMP585 + LSM6DS3 + NEO-8M
- [ ] Firmware lê os três sensores sem travar
- [ ] Log gerado e processado pelo parser -> `dados_tratados.csv`
- [ ] Gráficos no Colab a partir do CSV tratado
- [ ] Link do projeto no Wokwi e do notebook no README da semana

## Perguntas para reflexão (rascunho)

- Por que simular os sensores antes de voar?
- O que muda entre o log real (`voo_thonyan.txt`) e o log gerado na simulação?
- Como validar que o firmware não perde amostras?

## Referências

- [Chips customizados do Wokwi](../../entregas/dados/wokwi-chips/README.md)
- [Semana 1](semana-01.md) - análise no Colab
- [Semana 2](semana-02.md) - parser e CSV tratado
- [Semana 3](semana-03.md) - Arduino IDE / Wokwi
- [Documentação dos Custom Chips do Wokwi](https://docs.wokwi.com/chips-api/getting-started)
