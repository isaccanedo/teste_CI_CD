# Estrutura do projeto:
#### /meu_projeto
#### ├── .github/workflows/ci_cd.yml  (Workflow do GitHub Actions)
#### ├── meu_projeto/
#### │   ├── __init__.py
#### │   ├── main.py  (Código principal)
#### │   └── test_main.py  (Testes automatizados)
#### ├── requirements.txt  (Dependências)
#### ├── .flake8  (Configuração do flake8)
#### └── README.md  (Descrição do projeto)

# 1. Criando o código principal
# Arquivo: meu_projeto/main.py
```
def hello_world():
    return "Hello, World!"

if __name__ == "__main__":
    print(hello_world())
```

# 2. Criando os testes automatizados
# Arquivo: meu_projeto/test_main.py
import pytest
from main import hello_world

def test_hello_world():
    assert hello_world() == "Hello, World!"

# 3. Criando um arquivo de dependências
# Arquivo: requirements.txt
pytest
flake8

# 4. Configurando flake8
# Arquivo: .flake8
[flake8]
max-line-length = 88
exclude = .git,__pycache__,.venv

# 5. Criando o workflow CI/CD no GitHub Actions
# Arquivo: .github/workflows/ci_cd.yml
name: CI/CD Python

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout do código
        uses: actions/checkout@v3
      
      - name: Configurar Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.10'
      
      - name: Instalar dependências
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements.txt
      
      - name: Rodar flake8 (verificação de estilo)
        run: flake8 meu_projeto/
      
      - name: Rodar testes
        run: pytest meu_projeto/test_main.py

      - name: Simulação de Deploy
        run: echo "Deploy realizado com sucesso!"

