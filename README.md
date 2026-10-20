# Projeto_CALMAS

## Dicionário de dados — `dados_municipio_semana_2000-2024.RData`

### 1. Descrição da base

A base `dados_municipio_semana_2000-2024.RData` integra informações epidemiológicas sobre casos prováveis de dengue, Zika e chikungunya, provenientes do Sistema de Informação de Agravos de Notificação (SINAN), e variáveis climáticas obtidas do ERA5 por meio da API do Mosqlimate, além de índices climáticos disponibilizados pela NOAA.

Os dados são organizados por município e semana epidemiológica, permitindo investigar a distribuição temporal e espacial dos casos e sua relação com as condições climáticas.

**Unidade de observação:** município × semana epidemiológica.

**Chave de identificação esperada:** `cod_mun_res` + `epiyear` + `epiweek`.


### 2. Dicionário das variáveis

#### 2.1. Identificação geográfica e temporal

| Variável | Descrição | Tipo de dado | Unidade/formato |
|---|---|---|---|
| `cod_mun_res` | Código de identificação do município de residência utilizado na base epidemiológica. | Inteiro ou texto numérico | Código municipal |
| `date` | Data de referência da observação semanal, conforme a base integrada. | Data | AAAA-MM-DD |
| `epiyear` | Ano epidemiológico correspondente à observação. | Inteiro | Ano |
| `epiweek` | Número da semana epidemiológica correspondente à observação. | Inteiro | Semana epidemiológica |

#### 2.2. Variáveis epidemiológicas

| Variável | Descrição | Tipo de dado | Unidade |
|---|---|---|---|
| `dengue` | Número de casos prováveis de dengue atribuídos ao município e à semana epidemiológica. | Inteiro ou numérico | Casos |
| `zika` | Número de casos prováveis de Zika atribuídos ao município e à semana epidemiológica. | Inteiro ou numérico | Casos |
| `chik` | Número de casos prováveis de chikungunya atribuídos ao município e à semana epidemiológica. | Inteiro ou numérico | Casos |

#### 2.3. Variáveis climáticas 

| Variável | Descrição | Unidade |
|---|---|---|
| `tmin` | Menor temperatura mínima diária observada na semana. | °C |
| `tmin_mean` | Média das temperaturas mínimas diárias da semana. | °C |
| `tmax` | Maior temperatura máxima diária observada na semana. | °C |
| `tmax_mean` | Média das temperaturas máximas diárias da semana. | °C |
| `tmean` | Média da variável de temperatura média diária (`temp_med`) ao longo da semana. | °C |
| `amp_min` | Menor amplitude térmica diária observada na semana. | °C |
| `amp_max` | Maior amplitude térmica diária observada na semana. | °C |
| `amp_mean` | Média das amplitudes térmicas diárias da semana. | °C |
| `hum_min` | Menor umidade relativa mínima diária observada na semana. | % |
| `hum_min_mean` | Média das umidades relativas mínimas diárias da semana. | % |
| `hum_max` | Maior umidade relativa máxima diária observada na semana. | % |
| `hum_max_mean` | Média das umidades relativas máximas diárias da semana. | % |
| `hum_mean` | Média da variável de umidade relativa média diária (`umid_med`) ao longo da semana. | % |
| `pres_min` | Menor valor diário de pressão atmosférica mínima ao nível do mar observado na semana. | atm |
| `pres_min_mean` | Média dos valores diários de pressão atmosférica mínima ao nível do mar durante a semana. | atm |
| `pres_max` | Maior valor diário de pressão atmosférica máxima ao nível do mar observado na semana. | atm |
| `pres_max_mean` | Média dos valores diários de pressão atmosférica máxima ao nível do mar durante a semana. | atm |
| `pres_mean` | Média dos valores diários de pressão atmosférica média ao nível do mar durante a semana, a partir de `pressao_med`. | atm |
| `precip_min` | Menor valor diário de precipitação observado na semana. | mm |
| `precip_mean` | Média dos valores diários de precipitação durante a semana. | mm |
| `precip_max` | Maior valor diário de precipitação observado na semana. | mm |
| `precip_tot` | Soma dos valores diários de precipitação durante a semana. | mm |


A amplitude térmica diária é calculada pela diferença entre a temperatura máxima e a temperatura mínima do dia:

`amplitude = temp_max - temp_min`

Fonte dos dados diários: [MOSQLIMATE — Climate API](https://api.mosqlimate.org/docs/datastore/GET/climate/).


#### 2.4. Indicadores semanais de precipitação e temperatura derivados

Os indicadores são inicialmente calculados para cada dia e, posteriormente, somados dentro de cada semana epidemiológica.

| Variável | Descrição | Critério diário | Unidade |
|---|---|---|---|
| `dias_sem_chuva` | Número de dias com precipitação igual ou inferior a 0,03 mm. | `precip_tot <= 0.03` | Dias/semana |
| `dias_chuvosos` | Número de dias com precipitação superior a 0,03 mm. | `precip_tot > 0.03` | Dias/semana |
| `dias_chuva_1` | Número de dias com precipitação igual ou superior a 1 mm. | `precip_tot >= 1` | Dias/semana |
| `dias_chuva_5` | Número de dias com precipitação igual ou superior a 5 mm. | `precip_tot >= 5` | Dias/semana |
| `dias_chuva_10` | Número de dias com precipitação igual ou superior a 10 mm. | `precip_tot >= 10` | Dias/semana |
| `dias_chuva_50` | Número de dias com precipitação igual ou superior a 50 mm. | `precip_tot >= 50` | Dias/semana |
| `dias_chuva_100` | Número de dias com precipitação igual ou superior a 100 mm. | `precip_tot >= 100` | Dias/semana |
| `dias_tmax_25` | Número de dias em que a temperatura máxima foi igual ou superior a 25 °C. | `temp_max >= 25` | Dias/semana |
| `dias_tmax_30` | Número de dias em que a temperatura máxima foi igual ou superior a 30 °C. | `temp_max >= 30` | Dias/semana |
| `dias_tmax_35` | Número de dias em que a temperatura máxima foi igual ou superior a 35 °C. | `temp_max >= 35` | Dias/semana |
| `dias_tmax_40` | Número de dias em que a temperatura máxima foi igual ou superior a 40 °C. | `temp_max >= 40` | Dias/semana |
| `dias_tmin_10` | Número de dias em que a temperatura mínima foi igual ou inferior a 10 °C. | `temp_min <= 10` | Dias/semana |

#### 2.5. Variáveis complementares

| Variável | Descrição | Tipo de dado | Unidade/formato |
|---|---|---|---|
| `pop` | População de referência do município, conforme a fonte utilizada na preparação da base. | Numérico | Habitantes |
| `SEAS` | Identificador da estação climática de três meses consecutivos, conforme a nomenclatura utilizada pela NOAA para os períodos de cálculo do Oceanic Niño Index (ONI). Exemplos: `DJF` (dezembro–janeiro–fevereiro), `JFM` (janeiro–fevereiro–março) e `FMA` (fevereiro–março–abril). | Texto (`chr`) | Sigla de três meses |
| `ONI` | Oceanic Niño Index: anomalia da temperatura da superfície do mar, calculada como média móvel de três meses na região Niño 3.4 do Pacífico equatorial. | Numérico | °C |

**Fonte do ONI:** NOAA Climate Prediction Center (CPC).  
Documentação: [https://www.cpc.ncep.noaa.gov/data/](https://www.cpc.ncep.noaa.gov/data/)


### 3. Fontes de dados

- **Dados epidemiológicos:** Sistema de Informação de Agravos de Notificação (SINAN). A base utilizada no projeto contém contagens de casos prováveis de dengue, Zika e chikungunya, conforme os critérios de seleção, tratamento e agregação adotados. Dados podem estar sujeitos a alterações no SINAN. Os aqui disponibilizados foram obtidos em 12-Fev-2025.
- **Dados climáticos:** ERA5, obtidos por meio da API do Mosqlimate. Os dados incluem variáveis meteorológicas diárias utilizadas no cálculo de indicadores climáticos e na agregação por semana epidemiológica e município.  
  Documentação: https://api.mosqlimate.org/docs/datastore/GET/climate/
- **Índices Oceânico Niño:** National Oceanic and Atmospheric Administration (NOAA), fonte dos dados do Oceanic Niño Index (ONI) e das respectivas estações móveis de três meses (`SEAS`), utilizados para caracterizar condições associadas ao fenômeno El Niño–Oscilação Sul (ENSO).  
  Documentação: https://www.cpc.ncep.noaa.gov/data/


