# 📊 Profissões no Brasil com BigQuery

Este projeto tem como objetivo analisar a distribuição de profissionais por estado no Brasil usando o Google BigQuery. Foram integradas diferentes bases de dados contendo informações sobre advogados, contadores, engenheiros, psicólogos e os estados brasileiros.

---

# 🧱 Estrutura do Projeto

- Projeto no BigQuery: `profissoes_brasil`

- Dataset: `profissoes`

- Tabelas:

  - `estados_brasil` – Contém os nomes e siglas dos estados

  - `advogados` – Quantidade de advogados por estado, separados por gênero

  - `contadores` – Quantidade de contadores por estado, separados por gênero

  - `engenheiros` – Quantidade de engenheiros, com alguns estados prefixados com "CREA-"

  - `psicologos` – Quantidade de psicólogos por estado, separados por gênero
 
---

# 🧠 Objetivo

Consolidar todas as informações em uma única tabela para análise cruzada de profissionais por estado, com separação por gênero.

---

# ✅ Passo a passo

## 1. Importação e verificação dos dados
- Carreguei as tabelas no BigQuery.
- Verifiquei o conteúdo com SELECT * FROM ... LIMIT 10 para entender a estrutura de cada uma.

## 2. Identificação de inconsistências
- A tabela estados_brasil tinha colunas com espaços invisíveis no nome ( uf e nome_estado).
- Foi necessário utilizar backticks e aplicar TRIM() para remover espaços ao referenciar essas colunas.

## 3. Padronização de formatos
- Alguns nomes de estado nas tabelas estavam em letras minúsculas.
- Foi aplicado UPPER() nas colunas de JOIN para garantir uniformidade.
- A tabela engenheiros tinha o prefixo "CREA-" nos nomes dos estados, removido com REPLACE().

## 4. Construção dos JOINs
- Utilizei LEFT JOINs para combinar as tabelas de profissões com a tabela estados_brasil, garantindo que todos os estados aparecessem mesmo se alguma profissão estivesse ausente.
- O JOIN com psicólogos foi feito com nome_estado, enquanto os demais usaram uf.

---

# 🧪 Resultados

O resultado final é uma tabela consolidada contendo a quantidade de profissionais por gênero e por estado, o que permite realizar análises comparativas e criar visualizações.

---

# 🛠️ Ferramentas utilizadas
- Google BigQuery
- SQL padrão ANSI
- Google Cloud Console

---

# 🚧 Desafios enfrentados
- Colunas com espaços invisíveis exigiram atenção especial com TRIM() e backticks.
- Diferentes padrões de nomenclatura (uf vs estado, "CREA-") exigiram transformações com UPPER() e REPLACE().

