# Exemplo - GitHub: Fluxo de PR

## Objetivo

Mostrar o fluxo completo de contribuição: fork, branch pessoal e PR com a entrega dentro de `entregas/`.

## Passo a passo

```bash
# 1. Fazer fork no GitHub e clonar o SEU fork
git clone https://github.com/maria-silva/telemetry-trainee-program.git
cd telemetry-trainee-program

# 2. Registrar o repositório original para sincronizar depois
git remote add upstream https://github.com/Serra-Rocketry/telemetry-trainee-program.git

# 3. Criar a branch pessoal
git checkout -b maria-silva

# 4. Criar a estrutura de entregas da semana
mkdir -p entregas/maria-silva/semana-00/evidencias

echo "# Maria Silva - Trainee Telemetria" > entregas/maria-silva/README.md
echo "Objetivo: aprender Python e Arduino para atuar no Helike" >> entregas/maria-silva/README.md

cat > entregas/maria-silva/semana-00/hello.py <<'EOF'
def main():
    print("Hello from telemetry trainee!")

if __name__ == "__main__":
    main()
EOF

# 5. Commitar (use o prefixo da tecnologia)
git add entregas/maria-silva
git commit -m "docs: adiciona README pessoal e hello world da semana 00"

# 6. Enviar para o GitHub (o seu fork, não o repositório original)
git push -u origin maria-silva

# 7. Abrir PR no GitHub:
#    - Ir até o repositório ORIGINAL (Serra-Rocketry/telemetry-trainee-program)
#    - Clicar em "Pull Request" / "Compare across forks"
#    - Base: main (original) ← Compare: maria-silva (seu fork)
#    - Preencher o template

# 8. Após aprovação, o mentor faz o merge
```

## Nova semana depois de um merge

```bash
# Sincronizar o fork com o repositório original
git checkout main
git pull upstream main
git push origin main

# Trazer o merge para a sua branch
git checkout maria-silva
git merge main

# Criar a pasta da nova semana e trabalhar nela
mkdir -p entregas/maria-silva/semana-01

git add entregas/maria-silva/semana-01
git commit -m "feat: adiciona parser csv da semana 01"
git push origin maria-silva
# Abrir uma NOVA PR com os commits da semana
```

## Template de PR

```markdown
## Semana 0 - Onboarding & GitHub

## O que foi feito
- [x] Fork e branch `maria-silva` criados
- [x] README pessoal em `entregas/maria-silva/README.md`
- [x] `entregas/maria-silva/semana-00/hello.py`

## Como testar
1. `git checkout maria-silva`
2. `python entregas/maria-silva/semana-00/hello.py`

## Critérios de aceite
- [x] Entrega em `entregas/maria-silva/semana-00/`
- [x] PR segue template

## Dificuldades
- Nenhuma - tranquilo!
```

## Referências

- [Padrão de Entregas](../padrao-entregas.md)
- [Trilha GitHub](../trilhas/github.md)
