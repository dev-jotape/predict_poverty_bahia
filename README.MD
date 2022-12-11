# Imagens de Satélite e Machine Learning para Previsão de Indicadores Socioeconômicos no Brasil

## Introdução

Repositório com o código para replicação dos resultados obtidos no projeto de mestrado "Imagens de Satélite e Machine Learning para Previsão de Indicadores Socioeconômicos no Brasil", que esta sendo realizado no Instituto de Ciências Matemáticas e de Computação - Universidade de São Paulo (ICMC - USP) pelo aluno João Pedro da Silva (jp.silva@usp.br).

Este trabalho tem como objetivo combinar imagens diurnas e noturnas de satélite, e aplicar a técnica de Transfer Learning para previsão de indicadores socioeconômicos ainda não cobertos pela literatura.

O projeto se baseia no artigo [Predicting socioeconomic indicators using transfer learning on imagery data: an application in Brazil](https://link.springer.com/article/10.1007/s10708-022-10618-3) e esta em andamento.

A princípio a rede esta sendo criada utilizando o modelo VGG16, aplicada apenas para as cidades do estado da Bahia e com o objetivo de prever PIB e Renda média da região.

Os passos a seguir mostram como repoduzir os resultados preliminares.
  
## Download data

+ Donwload da imagem noturna (NTL): https://ngdc.noaa.gov/eog/viirs/download_dnb_composites.html

Os demais arquivos de entrada já estão presentes no repositório, mas podem ser acessados através dos seguintes links:

+ Indicadores:
	+ PIB: https://sidra.ibge.gov.br/Tabela/5938
	+ População: https://sidra.ibge.gov.br/Tabela/6579
	+ Renda média: https://sidra.ibge.gov.br/tabela/3548
+ Shapefiles do Brasil e Bahia: https://portaldemapas.ibge.gov.br/ (clicando em "Organização do Território" -> "Malhas territoriais" -> "Malha de municípios")
+ Coordenadas de cada município do Brazil (centros de cidades): ftp://geoftp.ibge.gov.br/estrutura_territorial/localidades/Shapefile_SHP/BR_Localidades_2010_v1.shp

## Scripts de Pré processamento de dados

+ Na pasta "scripts", executar na seguinte ordem: 
	+ todos que começam com "prepare_data_*"
	+ "get_nighttime_lights": Extrair caracteristicas da imagem de luz noturna (radiancia e geolocalização)
	+ "associate_cities_nightlights": associar os pontos de luz noturna com cada município
	+ "get_all_cities_coordinates": gerar um arquivo com a geolocalização de todos os centros de cidades da Bahia.
	+ "nightlights_distances_per_city": calcular a distancia euclidiana entre os pontos de luz noturna e o centro da cidade.
	+ "nearest_nightlights_per_city": filtrar apenas os 100 pontos mais próximos do centro da cidade.

## Obter Google Maps Static images

Após executar os scripts anteriores é necessário fazer o download das imagens diurnas de satélite no  Google Maps Static images:

+ Criar uma conta (ou utilizar um já existente) no Google Cloud
+ Adicionar uma chave de API para o "Maps API Key"
+ Em "scripts", executar o arquivo "download_google_images.py" substituindo a Key do Google Maps obtido no console.

## Extrair features

Para extrair features das imagens diurnas de satélite, com o modelo de rede VGG16 e aplicando transfer learning, executar o arquivo "scripts/extract_cnn_transfer_learning_features"

## Visualização de dados

Em "scripts/visualization" é possível executar o arquivo "visualization_ba" para se obter visualizações da base de dados.