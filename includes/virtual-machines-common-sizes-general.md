
<!-- A-series, Av2-series, D-series, Dv2-series, DS-series*, DSv2-series* -->

- Olá série e as VMs da série Av2 podem ser implantadas em uma variedade de tipos de hardware e os processadores. tamanho de saudação é limitado, com base em hardware hello, toooffer o desempenho do processador consistente para Olá executando a instância, independentemente do hardware de saudação em que é implantado. toodetermine Olá hardware físico em que esse tamanho for implantado, consulta Olá hardware virtual de dentro de saudação Máquina Virtual.

- VMs série D são projetadas toorun aplicativos que exigem maior capacidade de computação e desempenho de disco temporário. VMs série D fornecem processadores mais rápidos, uma maior taxa de memória para vCPU e uma unidade de estado sólida (SSD) para o disco temporário hello. Para obter detalhes, consulte comunicado Olá no hello blog do Azure, [novos tamanhos de máquina Virtual da série D](https://azure.microsoft.com/blog/2014/09/22/new-d-series-virtual-machine-sizes/).

- Dv2 série, um acompanhamento toohello D-series original, apresenta uma CPU mais eficiente. Olá Dv2 série CPU é cerca de 35% mais rápido do que Olá CPU da série D. Ele se baseia Olá última geração v3 de 2,4 GHz Intel Xeon® E5-2673 processador (Haswell) e com hello Intel Turbo aumento tecnologia 2.0, pode subir too3.1 GHz. Olá Dv2 série tem Olá mesmas configurações de disco e memória conforme Olá série D.

- tamanhos de camada básica Olá são principalmente para cargas de trabalho de desenvolvimento e outros aplicativos que não exigem balanceamento de carga, dimensionamento automático ou com uso intensivo de memória máquinas virtuais. Para obter informações sobre os tamanhos da VM mais adequados para os aplicativos de produção, consulte (Tamanhos das máquinas virtuais) [virtual-machines-size-specs.md] e para obter informações sobre os preços da VM, consulte [Preços das Máquinas Virtuais](https://azure.microsoft.com/pricing/details/virtual-machines/).

## <a name="dsv3-series"></a>Dsv3-series

ACU: 160-190

Tamanhos de série Dsv3 baseiam-se em Olá v4 do 2.3 GHz Intel XEON® E5-2673 processador (Broadwell) e pode obter 3.5GHz com Intel Turbo aumento tecnologia 2.0 e usar o armazenamento premium. tamanhos de série Dsv3 Olá oferecem uma combinação de vCPU, memória e armazenamento temporário para a maioria das cargas de trabalho de produção.


| Tamanho             | vCPU | Memória: GiB | Armazenamento temporário (SSD) GiB | Discos de dados máximos | Taxa de transferência máxima do disco em cache e armazenamento temporário: IOPS / MBps (tamanho do cache em GiB) | Taxa de transferência máxima do disco não armazenado em cache: IOPS / MBps | Máximo de NICs/Desempenho de rede esperado (Mbps) |
|------------------|--------|-------------|----------------|----------------|-----------------------------------------------------------------------|-------------------------------------------|------------------------------------------------|
| Standard_D2s_v3  | 2      | 8           | 16             | 4              | 4,000 / 32 (50)                                                       | 3.200 / 48                                | 2 / moderada                                   |
| Standard_D4s_v3  | 4      | 16          | 32             | 8              | 8,000 / 64 (100)                                                      | 6.400 / 96                                | 2 / moderada                                   |
| Standard_D8s_v3  | 8      | 32          | 64             | 16             | 16,000 / 128 (200)                                                    | 12.800 / 192                              | 4 / alta                                       |
| Standard_D16s_v3 | 16     | 64          | 128            | 32             | 32,000 / 256 (400)                                                    | 25.600 / 384                              | 8 / alta                                       |


## <a name="dv3-series"></a>Dv3-series

ACU: 160-190

Tamanhos de série Dv3 baseiam-se em Olá v4 do 2.3 GHz Intel XEON® E5-2673 processador (Broadwell) e pode obter 3.5GHz com Intel Turbo aumento tecnologia 2.0. tamanhos de série Dv3 Olá oferecem uma combinação de vCPU, memória e armazenamento temporário para a maioria das cargas de trabalho de produção.

O armazenamento do disco de dados é faturado separadamente das máquinas virtuais. toouse discos de armazenamento premium, use os tamanhos de Dsv3 hello. Olá preços e medidores de cobrança para tamanhos de Dsv3 são Olá igual Dv3-series. 


| Tamanho            | vCPU | Memória: GiB | Armazenamento temporário (SSD) GiB | Discos de dados máximos | Taxa de transferência máxima de armazenamento temporário: IOPS / MBps de leitura / MBps de gravação | NICs máximas / largura de banda da rede |
|-----------------|-----------|-------------|----------------|----------------|----------------------------------------------------------|------------------------------|
| Standard_D2_v3  | 2         | 8           | 50             | 4              | 3000/46/23                                               | 2 / moderada                 |
| Standard_D4_v3  | 4         | 16          | 100            | 8              | 6000/93/46                                               | 2 / moderada                 |
| Standard_D8_v3  | 8         | 32          | 200            | 16             | 12000/187/93                                             | 4 / alta                     |
| Standard_D16_v3 | 16        | 64          | 400            | 32             | 24000/375/187                                            | 8 / alta                     |


## <a name="dsv2-series"></a>Série DSv2

ACU: 210-250

| Tamanho | vCPU | Memória: GiB | Armazenamento temporário (SSD) GiB | Discos de dados máximos | Taxa de transferência máxima do disco em cache e armazenamento temporário: IOPS / MBps (tamanho do cache em GiB) | Taxa de transferência máxima do disco não armazenado em cache: IOPS / MBps | Máximo de NICs/Desempenho de rede esperado (Mbps) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_DS1_v2 |1 |3,5 |7 |2 |4.000 / 32 (43) |3.200 / 48 |2 / 750 |
| Standard_DS2_v2 |2 |7 |14 |4 |8.000 / 64 (86) |6.400 / 96 |2 / 1500 |
| Standard_DS3_v2 |4 |14 |28 |8 |16.000 / 128 (172) |12.800 / 192 |4 / 3000 |
| Standard_DS4_v2 |8 |28 |56 |16 |32.000 / 256 (344) |25.600 / 384 |8 / 6000 |
| Standard_DS5_v2 |16 |56 |112 |32 |64.000 / 512 (688) |51.200 / 768 |8 / 6000 - 12000 &#8224;|



## <a name="dv2-series"></a>Série Dv2

ACU: 210-250

| Tamanho              | vCPU | Memória: GiB | Armazenamento temporário (SSD) GiB | Taxa de transferência máxima de armazenamento temporário: IOPS / MBps de leitura / MBps de gravação | Discos de dados máximos / taxa de transferência: IOPS | Máximo de NICs/Desempenho de rede esperado (Mbps) |
|-------------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standard_D1_v2    | 1         | 3,5         | 50             | 3000 / 46 / 23                                           | 2 / 2 x 500                         | 2 / 750                 |
| Standard_D2_v2    | 2         | 7           | 100            | 6000 / 93 / 46                                           | 4 / 4 x 500                         | 2 / 1500                     |
| Standard_D3_v2    | 4         | 14          | 200            | 12000 / 187 / 93                                         | 8 / 8 x 500                         | 4 / 3000                     |
| Standard_D4_v2    | 8         | 28          | 400            | 24000 / 375 / 187                                        | 16 / 16 x 500                       | 8 / 6000                     |
| Standard_D5_v2    | 16        | 56          | 800            | 48000 / 750 / 375                                        | 32 / 32 x 500                       | 8 / 6000 - 12000 &#8224;          |


<br>

## <a name="ds-series"></a>Série DS

ACU: 160

| Tamanho | vCPU | Memória: GiB | Armazenamento temporário (SSD) GiB | Discos de dados máximos | Taxa de transferência máxima do disco em cache e armazenamento temporário: IOPS / MBps (tamanho do cache em GiB) | Taxa de transferência máxima do disco não armazenado em cache: IOPS / MBps | Máximo de NICs/Desempenho de rede esperado (Mbps) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_DS1 |1 |3,5 |7 |2 |4.000 / 32 (43) |3.200 / 32 |2 / 500 |
| Standard_DS2 |2 |7 |14 |4 |8.000 / 64 (86) |6.400 / 64 |2 / 1000 |
| Standard_DS3 |4 |14 |28 |8 |16.000 / 128 (172) |12.800 / 128 |4 / 2000 |
| Standard_DS4 |8 |28 |56 |16 |32.000 / 256 (344) |25.600 / 256 |8 / 4000 |

<br>

## <a name="d-series"></a>Série D 

ACU: 160

| Tamanho         | vCPU | Memória: GiB | Armazenamento temporário (SSD) GiB | Taxa de transferência máxima de armazenamento temporário: IOPS / MBps de leitura / MBps de gravação | Discos de dados máximos / taxa de transferência: IOPS | Máximo de NICs/Desempenho de rede esperado (Mbps) |
|--------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standard_D1  | 1         | 3,5         | 50             | 3000 / 46 / 23                                           | 2 / 2 x 500                         | 2 / 500                 |
| Standard_D2  | 2         | 7           | 100            | 6000 / 93 / 46                                           | 4 / 4 x 500                         | 2 / 1000                     |
| Standard_D3  | 4         | 14          | 200            | 12000 / 187 / 93                                         | 8 / 8 x 500                         | 4 / 2000                     |
| Standard_D4  | 8         | 28          | 400            | 24000 / 375 / 187                                        | 16 / 16 x 500                       | 8 / 4000                     |

<br>


## <a name="av2-series"></a>Série Av2

ACU: 100

| Tamanho            | vCPU | Memória: GiB | Armazenamento temporário (SSD) GiB | Taxa de transferência máxima de armazenamento temporário: IOPS / MBps de leitura / MBps de gravação | Discos de dados máximos / taxa de transferência: IOPS | Máximo de NICs/Desempenho de rede esperado (Mbps) | 
|-----------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standard_A1_v2  | 1         | 2           | 10             | 1000 / 20 / 10                                           | 2 / 2 x 500               | 2 / 250                 |
| Standard_A2_v2  | 2         | 4           | 20             | 2000 / 40 / 20                                           | 4 / 4 x 500               | 2 / 500                 |
| Standard_A4_v2  | 4         | 8           | 40             | 4000 / 80 / 40                                           | 8 / 8 x 500               | 4 / 1000                     |
| Standard_A8_v2  | 8         | 16          | 80             | 8000 / 160 / 80                                          | 16 / 16 x 500             | 8 / 2000                     |
| Standard_A2m_v2 | 2         | 16          | 20             | 2000 / 40 / 20                                           | 4 / 4 x 500               | 2 / 500                 |
| Standard_A4m_v2 | 4         | 32          | 40             | 4000 / 80 / 40                                           | 8 / 8 x 500               | 4 / 1000                     |
| Standard_A8m_v2 | 8         | 64          | 80             | 8000 / 160 / 80                                          | 16 / 16 x 500             | 8 / 2000                     |

<br>

## <a name="a-series"></a>Séria A

ACU: 50-100

| Tamanho | vCPU | Memória: GiB | Armazenamento temporário (HDD): GiB | Discos de dados máximos | Taxa de transferência máxima do disco de dados: IOPS | Máximo de NICs/Desempenho de rede esperado (Mbps)  |
| --- | --- | --- | --- | --- | --- | --- |
| Standard_A0* |1 |0,768 |20 |1 |1 x 500 |2 / 100 |
| Standard_A1 |1 |1,75 |70 |2 |2x500 |2 / 500  |
| Standard_A2 |2 |3,5 |135 |4 |4x500 |2 / 500 |
| Standard_A3 |4 |7 |285 |8 |8 x 500 |2 / 1000 |
| Standard_A4 |8 |14 |605 |16 |16 x 500 |4 / 2000 |
| Standard_A5 |2 |14 |135 |4 |4x500 |2 / 500 |
| Standard_A6 |4 |28 |285 |8 |8 x 500 |2 / 1000 |
| Standard_A7 |8 |56 |605 |16 |16 x 500 |4 / 2000 |
<br>

* hello Tamanho A0 for assinada em excesso no hardware físico hello. Para esse tamanho específico apenas, outras implantações de cliente podem afetar o desempenho de saudação da carga de trabalho em execução. desempenho relativo de saudação é descrito a seguir como Olá esperado da linha de base, assunto tooan aproximado a variabilidade de 15%.

### <a name="standard-a0---a4-using-cli-and-powershell"></a>Standard A0 - A4 usando CLI e PowerShell
No modelo de implantação clássico Olá, alguns nomes de tamanho VM são um pouco diferentes no CLI e do PowerShell:

* Standard_A0 é ExtraSmall 
* Standard_A1 é pequeno
* Standard_A2 é médio
* Standard_A3 é grande
* Standard_A4 é ExtraLarge

## <a name="basic-a"></a>A Básico

|Tamanho – Tamanho\Nome | vCPU |Memória|NICs (Máx.)|Tamanho máximo do disco temporário |Máx. discos de dados (1.023 GB cada)|Máx. IOPS (300 por disco)|
|---|---|---|---|---|---|---|
|A0\Basic_A0|1|768 MB|2| 20 GB|1|1 x 300|
|A1\Basic_A1|1|1,75 GB|2| 40 GB |2|2 x 300|
|A2\Basic_A2|2|3,5 GB|2| 60 GB|4|4 x 300|
|A3\Basic_A3|4|7 GB|2| 120 GB |8|8 x 300|
|A4\Basic_A4|8|14 GB|2| 240 GB |16|16 x 300|
