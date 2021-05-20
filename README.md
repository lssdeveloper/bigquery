# bigquery

#### LISTANDO O ID DO PROJETO

gcloud config list project

#### EXIBE O SCHEMA da tabela Shakespeare no conjunto de dados de amostra, execute:
bq show bigquery-public-data:samples.shakespeare

#### REALIZANDO UMA CONSULTA

bq query --use_legacy_sql=false \
'SELECT
   word,
   SUM(word_count) AS count
 FROM
   `bigquery-public-data`.samples.shakespeare
 WHERE
   word LIKE "%raisin%"
 GROUP BY
   word'


#### CRIANDO UMA NOVA TABELA
lista se há um conjunto de dados no seu projeto padrão
bq ls


#### LISTANDO O CONJUNTO DE DADOS DE UM PROJETO ESPECÍFICO INCLUINDO O ID DO PROJETO SEGUIDO POR (:)
bq ls bigquery-public-data:

#### CRIANDO UM CONJUNTO DE DADOS
bq mk babynames

#### FAZENDO UPLOAD PARA CARGA NA TABELA
wget http://www.ssa.gov/OACT/babynames/names.zip

#### EM SEGUIDA LISTANDO OS ARQUIVOS
ls

#### NO CASO DE UM ARQUIVO .ZIP, DESCOMPACTO
unzip names.zip

####CRIAR, ATUALIZAR E CARREGAR OS DADOS DE UMA TABELA EM UMA ÚNICA ETAPA (comando bq load)
##### CRIANDO A TABELA
bq load babynames.names2010 yob2010.txt name:string,gender:string,count:integer

#### ARGUMENTOS
datasetID: babynames
tableID: names2010
source: yob2010.txt
schema: name:string,gender:string,count:integer

#### VERIFICANDO A TABELA CRIADA NO CONJUNTO DE DADOS
bq ls babynames

#### SAÍDA
  tableId  |  Type

  names2010 |  TABLE

#### VISUALIZANDO O SCHEMA DA TABELA
bq show babynames.names2010


#### EXECUTANDO CONSULTAS
##### RETORNANDO OS CINCOS NOMES FEMININOS MAIS COMUNS
bq query "SELECT name,count FROM babynames.names2010 WHERE gender = 'F' ORDER BY count DESC LIMIT 5"

#### RETORNANDO OS 5 NOMES MASCULINOS MENOS COMUNS
bq query "SELECT name,count FROM babynames.names2010 WHERE gender = 'M' ORDER BY count ASC LIMIT 5"

#### LIMPAR, EXCLUIR O CONJUNTO DE DADOS CRIADO COM TODAS AS TABELAS RRESPECTIVAS
bq rm -r babynames
