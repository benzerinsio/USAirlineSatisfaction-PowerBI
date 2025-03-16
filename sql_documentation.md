# Documentação de Pré-processamento com SQLite

## Contexto
Este documento registra o uso do SQLite para preprocessar o dataset "US Airline Passenger Satisfaction". O objetivo foi reduzir o dataset original, mantendo apenas as colunas necessárias para visualizações no Power BI, otimizando o processo de análise.

---

## Passos e Comandos SQL

### 1. Abertura do Banco de Dados
- **Comando**: `sqlite3 airline.db`  
- **Descrição**: Inicia o SQLite e cria/abre o banco `airline.db` no diretório, onde o CSV original está localizado.

### 2. Configuração do Modo CSV
- **Comando**: `.mode csv`  
- **Descrição**: Define o modo de importação/exportação como CSV, garantindo compatibilidade com o formato do arquivo de entrada e saída.

### 3. Importação do Dataset
- **Comando**: `.import airline_satisfaction.csv satisfacao`  
- **Descrição**: Importa o arquivo `airline_satisfaction.csv` como a tabela "satisfacao" no banco. O SQLite usa os cabeçalhos do CSV como nomes de colunas.

### 4. Verificação das Colunas
- **Comando**: `.schema satisfacao`  
- **Descrição**: Exibe a estrutura da tabela "satisfacao", confirmando os nomes das colunas (ex.: "Gender", "Age") para uso na query.

### 5. Query SQL para Seleção de Colunas
- **Comando**:  
  ```sql
  SELECT "Gender", "Type of Travel", "Customer Type", "Class", "satisfaction_v2", 
         "Flight Distance", "Age", "Cleanliness", "Seat comfort" 
  FROM satisfacao;
- **Descrição**: Seleciona apenas as 9 colunas relevantes para as visualizações planejadas, reduzindo o dataset original.

### 6. Configuração para Exportação
- **Comando**:
  ```sql
  .headers on
  .mode csv
- **Descrição**: Ativa os cabeçalhos no arquivo de saída e mantém o modo CSV para formatação correta.

### 7. Exportação do Resultado
- **Comandos**:
  ```sql
  .output satisfacao_reduzido.csv
  
  SELECT "Gender", "Type of Travel", "Customer Type", "Class", "satisfaction_v2", 
       "Flight Distance", "Age", "Cleanliness", "Seat comfort" 
  FROM satisfacao;

  .output stdout
- **Descrição**: Direciona a saída da query para `most_useful_columns.csv`, grava os dados e retorna a saída ao Terminal.

### 8. Encerramento do Banco
- **Comando**: 
  ```sql
  .exit
- **Descrição**: Fecha o SQLite, finalizando o processo de preprocessamento.

---

## Resultado
O arquivo satisfacao_reduzido.csv foi gerado com as 9 colunas selecionadas, pronto para importação no Power BI. Este processo demonstrou o uso básico de SQL e comandos do SQLite para manipulação de dados via linha de comando.