📊 Processamento e Consolidação de Dados de Escolas
📌 Visão Geral

Este projeto realiza o tratamento, padronização e consolidação de dados relacionados a escolas, materiais didáticos e subprefeituras.

O objetivo principal é gerar uma base unificada e confiável que permita analisar a distribuição de materiais didáticos por subprefeitura.

📂 Estrutura dos Dados

O projeto utiliza três arquivos CSV como entrada:

data/escolas.csv
Contém informações das escolas (ID, nome, bairro, endereço, latitude e longitude)
data/material_didatico.csv
Contém a quantidade de material didático por escola
data/subprefeituras.csv
Relaciona bairros às respectivas subprefeituras
⚙️ Etapas do Processamento
1. Padronização de Endereços
Expansão de abreviações (ex: R. → Rua)
Remoção de acentos
Conversão para caixa alta
Separação de:
Logradouro
Número
2. Tratamento dos Nomes das Escolas
Padronização de siglas:
E.M. → ESCOLA MUNICIPAL
CIEP → CENTRO INTEGRADO DE EDUCAÇÃO PÚBLICA
Classificação do tipo de escola:
EM
CIEP
Colégio
Desconhecido
3. Limpeza de Bairros
Correções específicas de nomes inconsistentes
Remoção de acentos
Padronização para caixa alta
4. Tratamento dos Dados de Material
Padronização do campo id (com zero à esquerda)
Remoção de caracteres não numéricos da quantidade
Separação de registros inválidos:
Exportados para: invalido/material_invalido.csv
5. Tratamento de Subprefeituras
Padronização dos nomes
Correção de inconsistências (ex: Osvaldo → Oswaldo)
6. Consolidação dos Dados

Merge dos datasets:

Escolas + Subprefeituras (via bairro)
Resultado + Material Didático (via id)

Filtros aplicados:

Remoção de registros sem quantidade de material
📈 Saídas Geradas
Base consolidada
escolas_completo.csv
Contém todas as informações integradas
Agregação por subprefeitura
material_subprefeituras.csv
Soma total de material didático por subprefeitura
Registros inválidos
invalido/material_invalido.csv
Dados com quantidade inválida
🧠 Principais Funções
short_to_full_tag → Padroniza abreviações de endereço
fix_names → Normaliza nomes das escolas
type_school → Classifica o tipo de escola
remove_acentos → Remove acentuação de strings
🚀 Tecnologias Utilizadas
Python
Pandas
Regex (re)
Unidecode / Unicode normalization
⚠️ Pontos de Atenção
Dependência de padronização textual para joins (especialmente bairro)
Possíveis perdas de dados ao remover registros inválidos
Regras de limpeza são parcialmente hardcoded (ex: bairros específicos)
📌 Possíveis Melhorias
Uso de dicionário externo para padronização (menos hardcode)
Validação de dados mais robusta
Pipeline automatizado (ex: Airflow)
Logs de processamento
Testes unitários nas funções de limpeza
