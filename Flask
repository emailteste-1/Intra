from flask import Flask, request
import sqlite3

app = Flask(__name__)

def connect_db():
    conn = sqlite3.connect("dados_cnpj_filtrados.sqlite")
    return conn

@app.route('/')
def home():
    return """
    <h1>Intranet - Busca por CNAE</h1>
    <form action='/buscar' method='post'>
        <label>Digite o Código do CNAE:</label>
        <input type='text' name='cnae'>
        <input type='submit' value='Buscar'>
    </form>
    """

@app.route('/buscar', methods=['POST'])
def buscar():
    cnae_codigo = request.form['cnae']
    conn = connect_db()
    cursor = conn.cursor()
    
    cursor.execute("SELECT * FROM estabelecimento WHERE cnae_fiscal_principal=?", (cnae_codigo,))
    dados = cursor.fetchall()
    conn.close()

    return f"<h2>Resultados</h2><p>{dados}</p>"

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=8080)
