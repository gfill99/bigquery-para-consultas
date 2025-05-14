# BigQuery para Consultar Dados

## 🛠️ Configurando o Ambiente no Google BigQuery

### 1. Criando uma Conta no Google Cloud

Se ainda não possui, crie uma conta no Google:
- Acesse: [https://accounts.google.com/signup](https://accounts.google.com/signup)

Recomenda-se criar uma conta separada apenas para projetos, mas você pode usar sua conta Gmail pessoal.

### 2. Ativando o Google Cloud Platform (GCP)

- Vá até o console do Google Cloud: [https://console.cloud.google.com/](https://console.cloud.google.com/)
- Faça login com sua conta Google.
- Aceite os **termos de uso** e ative o serviço.

### 3. Criando um Projeto no GCP

- No topo da tela, clique em **“Selecionar projeto”** > **“Novo projeto”**.
- Dê um nome para o projeto (por exemplo: `profissoes-brasil`).
- Clique em **“Criar”** e selecione o projeto criado.

### 4. Acessando o BigQuery

- No menu lateral do GCP, procure por **BigQuery** ou vá diretamente para: [https://console.cloud.google.com/bigquery](https://console.cloud.google.com/bigquery)
- Clique para abrir o ambiente do BigQuery Studio. Esse será o espaço onde você irá carregar dados e executar consultas SQL.

---

## 📊 Criando Datasets e Carregando Dados

Agora que você já configurou seu ambiente no Google Cloud, o próximo passo é importar os dados para o BigQuery.

### 1. Criando Conjunto de Dados (Dataset)

- No painel do BigQuery, localize seu projeto e clique nos três pontinhos ao lado do nome do projeto.
- Selecione **Criar conjunto de dados**.
- Nomeie o conjunto de dados (por exemplo: `profissoes`).
- Em **Tipo de Local**, selecione **Região** e escolha: **southamerica-east1** (São Paulo).
- Clique em **Criar conjunto de dados**.

### 2. Criando Tabelas e Carregando os Arquivos CSV

Os dados necessários para o projeto estão disponíveis no GitHub. Siga os passos abaixo para obter os arquivos:

1. Acesse o repositório [profissoes_brasil](https://github.com/gfill99/profissoes_brasil).
2. Dentro do repositório, vá para a pasta **[data](https://github.com/gfill99/profissoes_brasil/tree/main/data)**.
3. Nas subpastas (como `advogados`, `contadores`, etc.), clique no arquivo CSV desejado.
4. No canto superior direito de cada arquivo, clique em **Download** para baixá-lo para o seu computador.

```plaintext
profissoes_brasil/
├── data/
│ ├── Advogados.csv
│ ├── Contadores.csv
│ ├── Engenheiros.csv
│ ├── Estados_brasil.csv
│ └── Psicologos.csv
```

Depois de baixar os arquivos, faça o upload deles para o BigQuery, conforme explicado abaixo.

### 3. Fazendo o Upload para o BigQuery

- No BigQuery, selecione o conjunto de dados que você criou anteriormente.
- Clique nos três pontinhos ao lado e selecione **Criar tabela**.
- Em **Origem**, selecione **Fazer upload** e faça o upload do arquivo CSV.
- Em **Nome da tabela**, insira um nome **simples e descritivo** (ex: `advogados`, `contadores`, `engenheiros`, `estados_brasil`, `psicologos`).
- Em **Esquema**, selecione **Detectar automaticamente**.
- Clique em **Criar tabela**.

---

## 📝 Realizando Consultas SQL no BigQuery

Agora que seus dados estão carregados no BigQuery, você pode começar a consultar as tabelas usando SQL. Abaixo está um exemplo de consulta para combinar dados de diferentes tabelas usando `JOINs`:

### Exemplo de Consulta SQL

```sql
SELECT
  a.id,
  TRIM(a.` nome_estado`) AS nome_estado,
  b.masculino,
  b.feminino
FROM `seu-projeto.profissoes.estados_brasil` AS a
LEFT JOIN `seu-projeto.profissoes.advogados` AS b
ON UPPER(TRIM(a.` uf`)) = UPPER(b.estado)
