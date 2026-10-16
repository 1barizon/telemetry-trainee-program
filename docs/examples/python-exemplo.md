# Exemplo - Python: Leitura e Análise de Telemetria

## Objetivo

Ler o CSV de telemetria da Semana 1 com `pandas`, calcular estatísticas e gerar um gráfico.

## Código completo

```python
#!/usr/bin/env python3
"""Leitor de telemetria - calcula estatisticas e gera grafico."""

import sys
from pathlib import Path

import pandas as pd

# Ordem dos campos no pacote #51,... (veja a Semana 1)
COLUNAS = [
    "ID", "millis", "pckt", "alt", "temp", "humi", "press",
    "gx", "gy", "gz", "ax", "ay", "az", "vz", "maxalt", "state",
    "hora", "data", "gps_alt", "lat", "lon", "sat", "pqd", "rssi",
]


def ler_csv(caminho: str) -> pd.DataFrame:
    """Le o CSV (sem cabecalho) e limpa o ID."""
    df = pd.read_csv(caminho, header=None, names=COLUNAS)
    df["ID"] = df["ID"].astype(str).str.lstrip("#").astype(int)
    return df


def calcular_estatisticas(df: pd.DataFrame, campo: str) -> dict:
    """Calcula media, max e min de um campo numerico."""
    serie = pd.to_numeric(df[campo], errors="coerce").dropna()
    return {
        "campo": campo,
        "media": serie.mean(),
        "max": serie.max(),
        "min": serie.min(),
        "amostras": len(serie),
    }


def salvar_resumo(estats: list[dict], caminho: str = "resumo.txt") -> None:
    """Salva estatisticas em arquivo."""
    with open(caminho, "w") as f:
        for e in estats:
            f.write(
                f"{e['campo']}: media={e['media']:.2f}, "
                f"max={e['max']:.2f}, min={e['min']:.2f}, "
                f"amostras={e['amostras']}\n"
            )
    print(f"Resumo salvo em {caminho}")


def main() -> None:
    if len(sys.argv) < 2:
        print("Uso: python exemplo.py <arquivo.csv>")
        sys.exit(1)

    caminho = sys.argv[1]
    if not Path(caminho).exists():
        print(f"Erro: arquivo {caminho} nao encontrado")
        sys.exit(1)

    df = ler_csv(caminho)
    print(f"Amostras: {len(df)}")

    campos = ["alt", "temp", "press"]
    estats = [calcular_estatisticas(df, c) for c in campos]

    for e in estats:
        print(f"{e['campo']}: media={e['media']:.2f}, "
              f"max={e['max']:.2f}, min={e['min']:.2f}")

    salvar_resumo(estats)

    # Grafico (opcional)
    try:
        import matplotlib.pyplot as plt

        tempo_s = (df["millis"] - df["millis"].min()) / 1000
        plt.plot(tempo_s, df["alt"])
        plt.xlabel("Tempo (s)")
        plt.ylabel("Altitude (m)")
        plt.title("Perfil de Voo")
        plt.grid(True)
        plt.savefig("perfil_voo.png")
        print("Grafico salvo em perfil_voo.png")
    except ImportError:
        print("matplotlib nao instalado - grafico ignorado")


if __name__ == "__main__":
    main()
```

## Como testar

```bash
# 1. Salve o código acima como exemplo.py na sua pasta da Semana 1
# 2. Instale as dependências:
pip install pandas matplotlib

# 3. Rode apontando para o dataset compartilhado (a partir da raiz do repo):
python exemplo.py entregas/dados/semana-01/cleaned.csv

# 4. Saída esperada:
# Amostras: 38
# alt: media=257.57, max=359.42, min=39.53
# temp: media=42.29, max=42.34, min=42.23
# press: media=932.83, max=957.29, min=921.51
# Resumo salvo em resumo.txt
```
