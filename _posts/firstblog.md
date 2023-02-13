---
date: '2022-12-16T11:50:54.000Z'
title: Amazing Blog
tagline: Criação de uma APi simples.
preview: >-
  Este é um exemplo de como é feita a criação de uma API em Flask que faz a conexão diretamente de uma base de dados SQLite .
image: >-
  https://images.unsplash.com/photo-1656188505561-19f1a1b6cda8?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1632&q=80
---

Para criar uma API que conecte a uma base de dados SQLite e grave dados de nome e idade, você precisará primeiro ter o SQLite instalado em sua máquina. Depois, você pode criar um arquivo .py com o seguinte código:

```python

# Importe o modulo do SQLite
import sqlite3

# Conectar ao banco de dados (ou criar um novo banco de dados se ele não existir)
conn = sqlite3.connect('database.db')

# Criar um cursor para executar comandos SQL
cursor = conn.cursor()

# Criar uma tabela para armazenar os dados de nome e idade
cursor.execute('''
    CREATE TABLE IF NOT EXISTS dados (
        nome TEXT,
        idade INTEGER
    )
''')

# Função para inserir um novo dado no banco de dados
def gravar_dado(nome, idade):
    cursor.execute('''
        INSERT INTO dados (nome, idade)
        VALUES (?, ?)
    ''', (nome, idade))
    conn.commit()

# Função para recuperar todos os dados do banco de dados
def obter_dados():
    cursor.execute('''
        SELECT * FROM dados
    ''')
    return cursor.fetchall()

```
Essas funções podem ser usadas para gravar e obter dados da base de dados SQLite. Para criar a API, você pode usar o Flask, uma biblioteca Python para desenvolvimento web. O código abaixo demonstra como criar uma API com duas rotas: uma que permite gravar dados de nome e idade na base de dados e outra que retorna todos os dados gravados.

```python

# Importar o Flask
from flask import Flask

# Criar uma instância da classe Flask
app = Flask(__name__)

# Rota para gravar dados
@app.route('/gravar_dado/<nome>/<idade>')
def gravar_dado_api(nome, idade):
    gravar_dado(nome, idade)
    return 'Dado gravado com sucesso!'

# Rota para obter dados
@app.route('/obter_dados')
def obter_dados_api():
    dados = obter_dados()
    return str(dados)

# Iniciar a aplicação Flask
if __name__ == '__main__':
    app.run()

```
Depois de criar esse código, você pode executá-lo com o seguinte comando:

`python app.py`

A API estará disponível em **http://localhost:5000**,