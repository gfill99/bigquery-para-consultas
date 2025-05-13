# 📊 Profissões no Brasil com BigQuery

Este projeto tem como objetivo **ensinar passo a passo como usar o Google BigQuery**, utilizando dados reais sobre profissões no Brasil (como advogados, contadores, engenheiros e psicólogos).

---

## 🧠 O que você vai aprender

- Como criar um projeto no Google Cloud e usar o BigQuery
- Como importar dados CSV do seu computador para o BigQuery
- Como fazer consultas SQL com `JOIN`, `TRIM`, `UPPER`, `REPLACE` e outros comandos úteis
- Como resolver problemas comuns de limpeza e padronização de dados

---

## 📁 Arquivos de dados

Todos os arquivos `.csv` usados neste projeto estão na pasta [`/data`](data). Você pode baixá-los diretamente por aqui:

- [advogados.csv](https://github.com/gfill99/profissoes_brasil/blob/main/data/advogados.csv)
- [contadores.csv](https://github.com/gfill99/profissoes_brasil/blob/main/data/contadores.csv)
- [engenheiros.csv](https://github.com/gfill99/profissoes_brasil/blob/main/data/engenheiros.csv)
- [estados_brasil.csv](https://github.com/gfill99/profissoes_brasil/blob/main/data/estados_brasil.csv)
- [psicologos.csv](https://github.com/gfill99/profissoes_brasil/blob/main/data/psicologos.csv)

---

## 🛠️ Passo a passo no BigQuery

### 1. Crie um projeto no Google Cloud
1. Acesse: [console.cloud.google.com](https://console.cloud.google.com)
2. Crie um novo projeto
3. Ative a API do BigQuery (se necessário)

### 2. Crie um Dataset
No painel do BigQuery:
- Vá em seu projeto → clique em **"Criar conjunto de dados"**
- Nomeie como `profissoes`

### 3. Faça o upload dos arquivos CSV
Para cada arquivo `.csv`:
- Clique com o botão direito no dataset → **"Criar tabela"**
- Fonte: Upload de arquivo
- Tipo: CSV
- Esquema: Autodetectar ou informar manualmente
- Nomeie a tabela de forma correspondente (ex: `advogados`, `engenheiros` etc.)

### 4. Faça as consultas SQL
Use as funções `TRIM()`, `UPPER()` e `REPLACE()` para padronizar os dados e realizar os `JOINs`.  
Exemplo:

```sql
SELECT
  a.id,
  TRIM(a.` nome_estado`) AS nome_estado,
  b.masculino,
  b.feminino
FROM `seu-projeto.profissoes.estados_brasil` AS a
LEFT JOIN `seu-projeto.profissoes.advogados` AS b
ON UPPER(TRIM(a.` uf`)) = UPPER(b.estado)
