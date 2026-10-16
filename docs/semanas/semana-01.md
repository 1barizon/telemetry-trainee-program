# Semana 1 - Python básico

## Objetivo

Ler o CSV de telemetria de um voo, calcular estatísticas e salvar um resumo.

## Preparação

- [ ] Python 3.10+ instalado
- [ ] `pandas` instalado (`pip install pandas`) - permitido nesta e nas próximas semanas
- [ ] Ler a [Trilha Python](../trilhas/python.md) (seções 1.1 e 2.1)
- [ ] Ver o [Slide deck](../slides/semana-01.html)
- [ ] Fazer o [Quiz](../quiz/semana-01.html)

## Dataset

Os dados estão em `entregas/dados/semana-01/cleaned.csv`. Cada linha é um pacote de telemetria que o foguete enviou pela serial.

O arquivo **não tem cabeçalho** e cada linha começa com o prefixo `#51` (o `ID` do pacote). São 24 campos separados por vírgula, nesta ordem:

| # | campo | descrição |
|---|---|---|
| 0 | `ID` | identificador do pacote (`#51`) |
| 1 | `millis` | timestamp em milissegundos |
| 2 | `pckt` | contador de pacotes |
| 3 | `alt` | altitude (m) |
| 4 | `temp` | temperatura (°C) |
| 5 | `humi` | umidade |
| 6 | `press` | pressão (hPa) |
| 7 | `gx` | giroscópio X |
| 8 | `gy` | giroscópio Y |
| 9 | `gz` | giroscópio Z |
| 10 | `ax` | acelerômetro X |
| 11 | `ay` | acelerômetro Y |
| 12 | `az` | acelerômetro Z |
| 13 | `vz` | velocidade vertical |
| 14 | `maxalt` | altitude máxima atingida |
| 15 | `state` | estado do voo |
| 16 | `hora` | hora |
| 17 | `data` | data |
| 18 | `gps_alt` | altitude do GPS |
| 19 | `lat` | latitude |
| 20 | `lon` | longitude |
| 21 | `sat` | satélites no fix do GPS |
| 22 | `pqd` | qualidade do pacote |
| 23 | `rssi` | potência do sinal recebido (dBm) |

Exemplo de linha:

```
#51,2003976,34647,39.53,42.34,0.00,957.29,1.87,0.26,-0.34,-39.20,-0.82,2.53,0.00,39.53,2,0,2000,487.80,-21.942293,-48.951912,12,0,-121
```

## Problema

Seu script deve:

1. Ler o arquivo `cleaned.csv` e transformá-lo em uma tabela (dica: `pandas` com `header=None` e os nomes das colunas acima)
2. Limpar o campo `ID`, removendo o `#` (vira `51`)
3. Calcular para o campo `alt`: média, máximo, mínimo e número de amostras
4. Exibir na tela de forma legível
5. Salvar o resumo em um arquivo `.txt`

## Requisitos

- **Pode usar `pandas`** (recomendado) ou a biblioteca padrão (`csv`)
- O caminho do CSV deve ser recebido como argumento (`sys.argv`)
- Trate arquivo inexistente com mensagem de erro amigável
- Trate CSV vazio (0 linhas) sem quebrar

## Formato de saída

```
Arquivo: cleaned.csv
Amostras: 38
Altitude media: 257.57 m
Altitude max:   359.42 m
Altitude min:   39.53 m
Duracao:        15.98 s
```

## Dicas

- `pandas.read_csv(caminho, header=None, names=COLUNAS)` lê um CSV sem cabeçalho
- Remova o `#` do ID com `df["ID"].str.lstrip("#")`
- Se um campo vier com texto, `pd.to_numeric(..., errors="coerce")` gera `NaN` - decida como tratar
- `sys.argv[1]` pega o primeiro argumento depois do nome do script
- `pathlib.Path.exists()` verifica se o arquivo existe
- Duração: `(df["millis"].max() - df["millis"].min()) / 1000`

## Extra (opcional)

- Gere um gráfico de `alt` × tempo (`millis`) com `matplotlib` e salve como PNG
- Adicione mais campos ao resumo: `temp`, `press`, `rssi`
- Compare quantas amostras você tem com o intervalo de `pckt` (pacotes podem ter se perdido na transmissão)

## Critérios de aceite

- [ ] Script roda com `python3 leitor.py ../../dados/semana-01/cleaned.csv` sem erros
- [ ] Estatísticas corretas de `alt` (confira na mão com 3 linhas)
- [ ] Resumo salvo em `.txt`
- [ ] Commit com tipo semântico

## Perguntas para reflexão

- O que acontece se uma linha tiver um campo não numérico?
- Por que ler com `header=None`? O que muda se você não passar os nomes das colunas?
- `with open(...) as f`: o que o `with` garante?

## Referências

- [Trilha Python](../trilhas/python.md)
- [Exemplo Python](../examples/python-exemplo.md)
- [Slide deck](../slides/semana-01.html)
- [Quiz](../quiz/semana-01.html)
