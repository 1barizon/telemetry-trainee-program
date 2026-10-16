# Semana 2 - Python aplicado (pacotes)

## Objetivo

Implementar um parser de pacotes de telemetria a partir de um log serial cru e um validador de dados.

## Preparação

- [ ] Semana 1 concluída
- [ ] Ler a [Trilha Python](../trilhas/python.md) (seções 1.2 e 1.3)
- [ ] Ver o [Slide deck](../slides/semana-02.html)
- [ ] Fazer o [Quiz](../quiz/semana-02.html)

## Dataset

O arquivo `entregas/dados/semana-02/voo_thonyan.txt` é o **log serial cru** de uma sessão de recepção. Ele mistura vários tipos de linha:

```
[LoRa] RX (RSSI=-121): #51,2003976,34647,39.53,...    # pacote recebido via LoRa
[STATS] Primeiro pacote recebido — count=34647        # estatística do receptor
[MESH] Beacons ativos: 0/0 | ouvindo o satellite: 0  # status da malha
[LOST] 22 pacote(s) perdido(s) — count 34647 -> 34670 # pacotes perdidos
#51,2003976,34647,39.53,42.34,...                     # pacote completo (24 campos)
```

O pacote tem os **mesmos 24 campos da Semana 1**, separados por vírgula e começando com `#51`:

`ID, millis, pckt, alt, temp, humi, press, gx, gy, gz, ax, ay, az, vz, maxalt, state, hora, data, gps_alt, lat, lon, sat, pqd, rssi`

> Atenção às linhas `[LoRa] RX`: elas trazem o pacote **sem os campos `hora` e `data`** (22 campos) e com o `rssi` zerado (o valor real está no texto `RSSI=...`). Elas têm formato diferente das linhas `#51,` completas.

## Problema

Seu script deve:

### Tarefa 1 - Parser

Função que recebe uma linha bruta e retorna um dicionário com os campos tipados.

Regras do parser:
- Aceitar apenas linhas que contenham um pacote que começa com `#51,`
- Retornar `None` para as demais linhas (`[LoRa] RX`, `[STATS]`, `[MESH]`, `[LOST]`, vazias)
- Remover o `#` do campo `ID` (vira `51`)
- Rejeitar pacotes com número de campos diferente de 24 (ex.: os de 22 campos do `[LoRa] RX`)
- Rejeitar campos não numéricos (ex: letra onde deveria vir número)
- Retornar `None` para linhas inválidas (não levantar exceção)

### Tarefa 2 - Validador

Função que recebe o dicionário do parser e valida os ranges físicos:

| Campo | Range |
|---|---|
| `alt` (altitude) | -100 a 10000 m |
| `temp` | -40 a 85 °C |
| `press` | 300 a 1100 hPa |
| `lat` | -90 a 90 |
| `lon` | -180 a 180 |
| `sat` | 0 a 30 |
| `rssi` | -140 a 0 dBm |

Retorna `True`/`False`.

### Tarefa 3 - Processador

Leia o arquivo linha por linha, aplique parser + validador, e exiba:

```
Processando...

Resumo:
  Linhas lidas:     118
  Pacotes:           38
  Validos:           38
  Parse err:          0
  Valid rej:          0
  Taxa OK:          100%
  Ignoradas:         80   # [LoRa] RX, [STATS], [MESH], [LOST]
  Pacotes perdidos: 762   # soma dos [LOST]
```

## Requisitos

- Pode usar a biblioteca padrão (`csv`, `str.split`) ou `pandas`
- Aceite o arquivo de entrada como argumento (`sys.argv`)
- Trate arquivo inexistente com mensagem de erro amigável

## Dicas

- Uma forma de extrair o pacote de uma linha `[LoRa] RX (...) : #51,...` é procurar a posição de `#51`
- `str.lstrip("#")` remove o `#` do ID
- `str.split(",")` separa os campos
- `try/except ValueError` em volta de cada `float()` ou `int()`
- Para contar pacotes perdidos, some o valor de cada linha `[LOST]`

## Extra (opcional)

- Exporte os pacotes válidos para um CSV
- Reconstrua a série temporal (`millis` × `alt`) e gere um gráfico com `matplotlib`
- Compare o intervalo de `pckt` com o total de pacotes perdidos

## Critérios de aceite

- [ ] Parser rejeita a linha `[LoRa] RX` (22 campos) sem quebrar
- [ ] Parser ignora `[STATS]`, `[MESH]` e `[LOST]`
- [ ] Validador rejeita valores fora do range
- [ ] Estatísticas no final
- [ ] Commit com tipo semântico

## Perguntas para reflexão

- Por que separar parser e validador em funções diferentes?
- O que acontece se um campo de altitude vier como `"NaN"`?
- Como você testaria manualmente o parser com 20 linhas diferentes?

## Referências

- [Trilha Python](../trilhas/python.md)
- [Slide deck](../slides/semana-02.html)
- [Quiz](../quiz/semana-02.html)
