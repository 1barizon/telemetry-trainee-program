# Semana 2 - Python aplicado (pacotes)

## Objetivo

Parsear os pacotes do log cru (`entregas/dados/semana-02/voo_thonyan.txt`) e validar os dados.

## Tarefas

- [ ] Implementar parser (24 campos, ignorar linhas que nao sao pacote)
- [ ] Implementar validador (ranges de alt, temp, press, lat, lon, sat, rssi)
- [ ] Processar o arquivo e exibir o resumo
- [ ] Contar pacotes perdidos a partir das linhas `[LOST]` (opcional)

## Criterios de aceite

- [ ] Parser rejeita os pacotes de 22 campos (`[LoRa] RX`) sem quebrar
- [ ] Parser ignora `[STATS]`, `[MESH]` e `[LOST]`
- [ ] Validacao detecta valores fora do range
- [ ] README atualizado

## Referencias

- [Trilha Python](../trilhas/python.md)
- [Exemplo Python](../examples/python-exemplo.md)
