
* Olá série M oferece hello mais alto vCPU contar (too128 vCPUs) e maior memória (para cima too2.0 TiB) de qualquer máquina virtual na nuvem hello.  Ele é ideal para bancos de dados muito grandes ou outros aplicativos que se beneficiam de altas contagens de vCPU e de grandes quantidades de memória.

* Série Dv2, série D, série G, e contrapartes do DS/GS Olá são ideais para aplicativos que exigem mais rápido vCPUs, melhor desempenho de armazenamento temporário, ou têm exigências de memória superior.  Elas oferecem uma combinação poderosa para vários aplicativos de nível empresarial.

* VMs série D são projetadas toorun aplicativos que exigem maior capacidade de computação e desempenho de disco temporário. As VMs da série D fornecem processadores mais rápidos, uma maior taxa de memória por vCPU e uma unidade de estado sólido (SSD) para o armazenamento temporário. Para obter detalhes, consulte comunicado Olá no hello blog do Azure, [novos tamanhos de máquina Virtual da série D](https://azure.microsoft.com/blog/2014/09/22/new-d-series-virtual-machine-sizes/).

* Dv2 série, um acompanhamento toohello D-series original, apresenta uma CPU mais eficiente. Olá Dv2 série CPU é cerca de 35% mais rápido do que Olá CPU da série D. Ele se baseia Olá última geração v3 de 2,4 GHz Intel Xeon® E5-2673 processador (Haswell) e com hello Intel Turbo aumento tecnologia 2.0, pode subir too3.1 GHz. Olá Dv2 série tem Olá mesmas configurações de disco e memória conforme Olá série D.


## <a name="esv3-series"></a>ESv3-series

ACU: 160-190

Instâncias de série ESv3 baseiam-se no hello v4 do 2.3 GHz Intel XEON® E5-2673 processador (Broadwell) e pode obter 3.5GHz com Intel Turbo aumento tecnologia 2.0 e usar o armazenamento premium. As instâncias Ev3-series são ideais para aplicativos empresariais com uso intensivo de memória.


| Tamanho             | vCPU | Memória: GiB | Armazenamento temporário (SSD) GiB | Discos de dados máximos | Taxa de transferência máxima do disco em cache e armazenamento temporário: IOPS / MBps (tamanho do cache em GiB) | Taxa de transferência máxima do disco não armazenado em cache: IOPS / MBps | Máximo de NICs/Desempenho de rede esperado (Mbps) |
|------------------|--------|-------------|----------------|----------------|-----------------------------------------------------------------------|-------------------------------------------|------------------------------------------------|
| Standard_E2s_v3  | 2      | 16          | 32             | 4              | 4,000 / 32 (50)                                                       | 3.200 / 48                                | 2 / moderada                                   |
| Standard_E4s_v3  | 4      | 32          | 64             | 8              | 8,000 / 64 (100)                                                      | 6.400 / 96                                | 2 / moderada                                   |
| Standard_E8s_v3  | 8      | 64          | 128            | 16             | 16,000 / 128 (200)                                                    | 12.800 / 192                              | 4 / alta                                       |
| Standard_E16s_v3 | 16     | 128         | 256            | 32             | 32,000 / 256 (400)                                                    | 25.600 / 384                              | 8 / alta                                       |
| Standard_E32s_v3 | 32     | 256         | 512            | 32             | 64,000 / 512 (800)                                                    | 51.200 / 768                              | 8 / extremamente alta                             |
| Standard_E64s_v3 | 64     | 432         | 864            | 32             | 128,000/1024 (1600)                                                   | 80,000 / 1200                             | 8 / extremamente alta                             |



## <a name="ev3-series"></a>Ev3-series

ACU: 160 - 190 

Instâncias de série Ev3 baseiam-se no hello v4 do 2.3 GHz Intel XEON® E5-2673 processador (Broadwell) e pode obter 3.5GHz com Intel Turbo aumento tecnologia 2.0. As instâncias Ev3-series são ideais para aplicativos empresariais com uso intensivo de memória.

O armazenamento do disco de dados é faturado separadamente das máquinas virtuais. toouse discos de armazenamento premium, use os tamanhos de ESv3 hello. Olá preços e medidores de cobrança para tamanhos de ESv3 são Olá igual Ev3-series. 


| Tamanho            | vCPU | Memória: GiB | Armazenamento temporário (SSD) GiB | Discos de dados máximos | Taxa de transferência máxima de armazenamento temporário: IOPS / MBps de leitura / MBps de gravação | NICs máximas / largura de banda da rede |
|-----------------|-----------|-------------|----------------|----------------|----------------------------------------------------------|------------------------------|
| Standard_E2_v3  | 2         | 16          | 50             | 4              | 3000/46/23                                               | 2 / moderada                 |
| Standard_E4_v3  | 4         | 32          | 100            | 8              | 6000/93/46                                               | 2 / moderada                 |
| Standard_E8_v3  | 8         | 64          | 200            | 16             | 12000/187/93                                             | 4 / alta                     |
| Standard_E16_v3 | 16        | 128         | 400            | 32             | 24000/375/187                                            | 8 / alta                     |
| Standard_E32_v3 | 32        | 256         | 800            | 32             | 48000/750/375                                            | 8 / extremamente alta           |
| Standard_E64_v3 | 64        | 432         | 1600           | 32             | 96000/1000/500                                           | 8 / extremamente alta           |


## <a name="m-series"></a>Série M*

ACU: 160 a 180

| Tamanho            | vCPU | Memória: GiB | Armazenamento temporário (SSD) GiB | Discos de dados máximos | Taxa de transferência máxima do disco em cache e armazenamento temporário: IOPS / MBps (tamanho do cache em GiB) | Taxa de transferência máxima do disco não armazenado em cache: IOPS / MBps | Máximo de NICs/Desempenho de rede esperado (Mbps) |
|-----------------|------|-------------|----------------|----------------|-----------------------------------------------------------------------|-------------------------------------------|------------------------------|
| Standard_M64ms  | 64   | 1792        | 2.048           | 32             | 80,000 / 800 (6348)       | 40.000 / 1.000                            | 8 / 16000          |
| Standard_M128s** | 128  | 2.048        | 4096           | 64             | 160,000 / 1,600 (12,696) | 80.000 / 2.000                            | 8 / 25000          |



*A tecnologia Intel® Hyper-Threading da VM série M

**Mais de 64 vCPUs exigem um destes sistemas operacionais convidados com suporte: Windows Server 2016, Ubuntu 16.04 LTS, SLES 12 SP2 e Red Hat Enterprise Linux ou CentOS 7.3 com LIS 4.2.1 

<br>

## <a name="gs-series"></a>Série GS*

ACU: 180 - 240

| Tamanho | vCPU | Memória: GiB | Armazenamento temporário (SSD) GiB | Discos de dados máximos | Taxa de transferência máxima do disco em cache e armazenamento temporário: IOPS / MBps (tamanho do cache em GiB) | Taxa de transferência máxima do disco não armazenado em cache: IOPS / MBps | Máximo de NICs/Desempenho de rede esperado (Mbps) |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_GS1 |2 |28 |56 |4 |10.000 / 100 (264) |5.000 / 125 |2 / 2000 |
| Standard_GS2 |4 |56 |112 |8 |20.000 / 200 (528) |10.000 / 250 |2 / 4000 |
| Standard_GS3 |8 |112 |224 |16 |40.000 / 400 (1.056) |20.000 / 500 |4 / 8000 |
| Standard_GS4 |16 |224 |448 |32 |80.000 / 800 (2.112) |40.000 / 1.000 |8 / 6000 - 16000 &#8224; |
| Standard_GS5** |32 |448 |896 |64 |160.000 / 1.600 (4.224) |80.000 / 2.000 |8 / 20000 |

* hello máximo em disco taxa de transferência (IOPS ou MBps) possível com uma série GS VM pode ser limitada por número de hello, tamanho e a distribuição de saudação anexada discos. Para obter detalhes, confira [Armazenamento Premium: armazenamento de alto desempenho para cargas de trabalho das máquinas virtuais do Azure](../articles/storage/common/storage-premium-storage.md). 

* * A instância é isolado toohardware tooa dedicado único cliente.


<br>

## <a name="g-series"></a>Série G

ACU: 180 - 240

| Tamanho         | vCPU | Memória: GiB | Armazenamento temporário (SSD) GiB | Taxa de transferência máxima de armazenamento temporário: IOPS / MBps de leitura / MBps de gravação | Discos de dados máximos / taxa de transferência: IOPS | Máximo de NICs/Desempenho de rede esperado (Mbps) |
|--------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standard_G1  | 2         | 28          | 384            | 6000 / 93 / 46                                           | 4 / 4 x 500                       | 2 / 2000                     |
| Standard_G2  | 4         | 56          | 768            | 12000 / 187 / 93                                         | 8 / 8 x 500                       | 2 / 4000                     |
| Standard_G3  | 8         | 112         | 1.536          | 24000 / 375 / 187                                        | 16 / 16 x 500                     | 4 / 8000                |
| Standard_G4  | 16        | 224         | 3.072          | 48000 / 750 / 375                                        | 32 / 32 x 500                     | 8 / 6000 - 16000 &#8224;          |
| Standard_G5* | 32        | 448         | 6.144          | 96000 / 1500 / 750                                       | 64 / 64 x 500                     | 8 / 20000           |

* A instância é isolado toohardware tooa dedicado único cliente.
<br>


## <a name="dsv2-series"></a>Série DSv2*

ACU: 210 - 250

| Tamanho | vCPU | Memória: GiB | Armazenamento temporário (SSD) GiB | Discos de dados máximos | Taxa de transferência máxima do disco em cache e armazenamento temporário: IOPS / MBps (tamanho do cache em GiB) | Taxa de transferência máxima do disco não armazenado em cache: IOPS / MBps | Máximo de NICs/Desempenho de rede esperado (Mbps) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_DS11_v2 |2 |14 |28 |4 |8.000 / 64 (72) |6.400 / 96 |2 / 1500 |
| Standard_DS12_v2 |4 |28 |56 |8 |16.000 / 128 (144) |12.800 / 192 |4 / 3000 |
| Standard_DS13_v2 |8 |56 |112 |16 |32.000 / 256 (288) |25.600 / 384 |8 / 6000 |
| Standard_DS14_v2 |16 |112 |224 |32 |64.000 / 512 (576) |51.200 / 768 |8 / 6000 - 12000 &#8224; |
| Standard_DS15_v2** |20 |140 |280 |40 |80.000 / 640 (720) |64.000 / 960 |8 / 20000***

* hello máximo em disco taxa de transferência (IOPS ou MBps) possível com uma série de série DSv2 VM pode ser limitada por número de hello, tamanho e a distribuição de saudação anexada discos.  Para obter detalhes, confira [Armazenamento Premium: armazenamento de alto desempenho para cargas de trabalho das máquinas virtuais do Azure](../articles/storage/common/storage-premium-storage.md).

* * Instância é um nó isolado que garante que a VM seja Olá apenas uma VM em nosso nó Haswell Intel.

***25000 Mbps com Rede Acelerada.

<br>

## <a name="dv2-series"></a>Série Dv2

ACU: 210 - 250

| Tamanho              | vCPU | Memória: GiB | Armazenamento temporário (SSD) GiB | Taxa de transferência máxima de armazenamento temporário: IOPS / MBps de leitura / MBps de gravação | Discos de dados máximos / taxa de transferência: IOPS | Máximo de NICs/Desempenho de rede esperado (Mbps) |
|-------------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standard_D11_v2   | 2         | 14          | 100            | 6000 / 93 / 46                                           | 4 / 4 x 500                         | 2 / 1500                     |
| Standard_D12_v2   | 4         | 28          | 200            | 12000 / 187 / 93                                         | 8 / 8 x 500                         | 4 / 3000                     |
| Standard_D13_v2   | 8         | 56          | 400            | 24000 / 375 / 187                                        | 16 / 16 x 500                       | 8 / 6000                     |
| Standard_D14_v2   | 16        | 112         | 800            | 48000 / 750 / 375                                        | 32 / 32 x 500                       | 8 / 6000 - 12000 &#8224;          |
| Standard_D15_v2* | 20        | 140         | 1.000          | 60000 / 937 / 468                                        | 40 / 40 x 500                       | 8 / 20000** |

* A instância é um nó de isolado que garante que a VM seja Olá apenas uma VM em nosso nó Haswell Intel.

**25000 Mbps com Rede Acelerada.

<br>

## <a name="ds-series"></a>Série DS*

ACU: 160

| Tamanho | vCPU | Memória: GiB | Armazenamento temporário (SSD) GiB | Discos de dados máximos | Taxa de transferência máxima do disco em cache e armazenamento temporário: IOPS / MBps (tamanho do cache em GiB) | Taxa de transferência máxima do disco não armazenado em cache: IOPS / MBps | Máximo de NICs/Desempenho de rede esperado (Mbps) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_DS11 |2 |14 |28 |4 |8.000 / 64 (72) |6.400 / 64 |2 / 1000 |
| Standard_DS12 |4 |28 |56 |8 |16.000 / 128 (144) |12.800 / 128 |4 / 2000 |
| Standard_DS13 |8 |56 |112 |16 |32.000 / 256 (288) |25.600 / 256 |8 / 4000 |
| Standard_DS14 |16 |112 |224 |32 |64.000 / 512 (576) |51.200 / 512 |8 / 6000 - 8000 &#8224; |

* hello máximo em disco taxa de transferência (IOPS ou MBps) possível com uma VM da série DS pode ser limitada por número de hello, tamanho e a distribuição de saudação anexada discos.  Para obter detalhes, confira [Armazenamento Premium: armazenamento de alto desempenho para cargas de trabalho das máquinas virtuais do Azure](../articles/storage/common/storage-premium-storage.md).


## <a name="d-series"></a>Série D

ACU: 160

| Tamanho         | vCPU | Memória: GiB | Armazenamento temporário (SSD) GiB | Taxa de transferência máxima de armazenamento temporário: IOPS / MBps de leitura / MBps de gravação | Discos de dados máximos / taxa de transferência: IOPS | Máximo de NICs/Desempenho de rede esperado (Mbps) |
|--------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standard_D11 | 2         | 14          | 100            | 6000 / 93 / 46                                           | 4 / 4 x 500                         | 2 / 1000                     |
| Standard_D12 | 4         | 28          | 200            | 12000 / 187 / 93                                         | 8 / 8 x 500                         | 4 / 2000                     |
| Standard_D13 | 8         | 56          | 400            | 24000 / 375 / 187                                        | 16 / 16 x 500                       | 8 / 4000                     |
| Standard_D14 | 16        | 112         | 800            | 48000 / 750 / 375                                        | 32 / 32 x 500                       | 8 / 6000 - 8000 &#8224;                |

<br>

