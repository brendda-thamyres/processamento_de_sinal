## Separando faixa de dados

```pid_count``` $\rightarrow$ É o id do paciente, isso é, o rótulo atribuído ao alvo que queremos processar. O prefixo "o" refere-se à tecnica de pressão que deriva os dados do dataset ("o" para oscilométrico e "a" para auscultatório);

```osci_count``` $\rightarrow$ É o índice que leva uma medição oscilométrica durante fase exprimental em ```measurement```;

```sampling_rate```$\rightarrow$ É a quantidade de amostras coletadas por segundo, i.e., o número de vezes que o valor é medido e armazenado;

```ppt_osci_df```$\rightarrow$ É a combinação do dataset de dados do teste oscilométrico com o dataset dos pacientes, a fim de alinhar valores fisiológicos (input) com valoresreais derivados da pressão (target).

## Osci_series
```pid``` $\rightarrow$ id do paciente; <p>
```phase``` $\rightarrow$ É a fase do protocolo para medição: _initial_ é a visita inicial, _ambulatory_ é a etapa de ambulatório para o protocolo oscilométrico, _return_ é a fase de retorno, _synthetic_ harmonização sintética dos dados da visita que serão usados como uma linha base de medição; <p>
```measurement``` $\rightarrow$ Identificador da fase de exercício que o paciente é submetido; <p>
```date_time``` $\rightarrow$ Data e hora em que o teste foi submetido; <p>
```sbp``` $\rightarrow$ pressão sanguínea sistólica; <p>
```dbp``` $\rightarrow$ pressão sanguínea diastólica; <p>
```duration``` $\rightarrow$ duração do teste (em segundos) <p>
```pressure_quality``` $\rightarrow$ Qualidade do exame tonométrico, medida de 0 a 1; <p>
```optical_quality``` $\rightarrow$ Qualidade do exame óptico, medido de 0 a 1; <p>
```waveform_file_path```, ```waveforms_generated``` $\rightarrow$ Caminho para o arquivo da onda; quantidade de ondas geradas.

## Análise visual

```t``` $\rightarrow$ É o tempo medido em segundos relativo ao valor date_time

```ekg``` $\rightarrow$ Amplitude do sinal do ECG, em milivolts (mV). Filtro aplicado: 
    
  * DC Block $\rightarrow$ Remove componentes de baixa frequência (<0.1Hz).
  
  * Lowpass elíptico $\rightarrow$ remove ruído de alta frequência (passa até 40, corta a partir de 45Hz)
  
  * Notch Chebyshev tipo I $\rightarrow$ Elimina os ruídos da rede elétrica: Frequência central em 60Hz, ondulação de 0,1 dB na banda de passagem

  * dispositivo $\rightarrow$ [ADS1292](https://www.ti.com/product/ADS1292)

<<<<<<< HEAD
```Lowpass elíptico``` $\rightarrow$ remove ruído de alta frequência (passa até 40, corta a partir de 45Hz)

```Notch Chebyshev tipo I``` $\rightarrow$ Elimina os ruídos da rede elétrica

```dispositivo ``` $\rightarrow$ [ADS1292](https://www.ti.com/product/ADS1292)

=======
>>>>>>> 20cfc6b9bd30cebff998dc23eafa31fdecd570c1
--------

```optical``` $\rightarrow$ Amplitude do sinal óptico (PPG) capturado no momento da medição oscilométrica, expressa em unidade arbitrárias do amplificador, isso é, valores relativos (sem calibração). Dependendo de como a voltagem foi passada para o amplificador, sabe-se que a voltagem é convertida para um número que a depender da configuração eletronica, pode ser como positivo ou negativo. Filtros aplicados:

* Highpass butterworth $\rightarrow$  remove ruído de movimento e variações lentas de luz: Passa frequências acima de 0.25 Hz;

* Lowpass equiripple $\rightarrow$ remove ruídos de alta frequência e outras interferências; minimiza o erro máximo, gerando ondulações uniformes (iguais) nas bandas: Banda de passagem até 10 Hz, banda de rejeição a partir de 12 Hz

```dispositivo ``` $\rightarrow$ [MAX30101](https://www.maximintegrated.com/en/products/interface/signal-integrity/MAX30101.html)

--------

```acelerômetro``` $\rightarrow$ Os acelerômetros de 3 eixos presentes no dispositivo medem a aceleração em três direções ortogonais (eixos X, Y e Z), 
permitindo a detecção de movimento e inclinação em 3D de acordo com a força da gravidade, monitorando a postura do braço e o nível de atividade. 

```x``` $\rightarrow$ movimento horizontal

```y``` $\rightarrow$ movimento vertical

```z``` $\rightarrow$ movimentos na direção perpendicular aos eixos x e y

_filtros:_ filtro elíptico de alta frequência,  filtro elíptico de baixa frequência de 7ª ordem

```dispositivo``` $\rightarrow$ [LSM6DS3](https://www.st.com/en/mems-and-sensors/lsm6ds3tr-c.html)

--------

```pressão``` $\rightarrow$ Mede a amplitude do sinal tonométrico em milibars (mbar)

_filtros:_ 

  * filtro elíptico de alta frequência (deixa passar apenas as frequências acima de um determinado valor): 0.2 Hz de banda de rejeição, 0.3 Hz de banda de passagem, atenuação de 60 dB na banda de rejeição, ondulação de 1 dB na banda de passagem;
  * filtro elíptico de baixa frequência de 7ª ordem (Passa as frequências abaixo de um determinado valor): 22 Hz de banda de passagem, 6 Hz de banda de rejeição, ondulação de 0,1 dB na banda de passagem;

```dispositivo``` $\rightarrow$ [MS5803-02BA](https://www.te.com/commerce/DocumentDelivery/DDEController?Action=srchrtrv&DocNm=MS5803-02BA&DocType=Data+Sheet&DocLang=English)

---------

#### Referências: 
Rebecca Mieloszyk et al., “A Comparison of Wearable Tonometry, Photoplethysmography, and Electrocardiography for Cuffless Measurement of Blood Pressure in an Ambulatory Setting,” IEEE Transactions on Biomedical Engineering,

repositótio do AURORA: 
