<!-- F-series, Fs-series* -->

F-série é baseada em Olá v3 de 2,4 GHz Intel Xeon® E5-2673 processador (Haswell), que pode proporcionar velocidade de clock mais alto 3,1 GHz com hello Intel Turbo aumento tecnologia 2.0. Isso é Olá mesmo desempenho de CPU como Olá Dv2-série de máquinas virtuais.  A um preço de lista por hora inferior, Olá F série é melhor o valor de preço-desempenho em hello Azure portfólio com base em Olá unidade de computação do Azure (ACU) por vCPU hello. 

As VMs da série F são uma ótima opção para as cargas de trabalho que exigem CPUs mais rápidas, mas não precisam de tanta memória ou armazenamento temporário por vCPU.  Cargas de trabalho como analytics, servidores de jogos, servidores web e o processamento em lotes se beneficiará do valor Olá Olá F-series.

Olá Fs-series fornece todas as vantagens de saudação do Olá F-series, no armazenamento de tooPremium de adição.

## <a name="fs-series"></a>Série Fs*

ACU: 210 - 250

| Tamanho | vCPU | Memória: GiB | Armazenamento temporário (SSD) GiB | Discos de dados máximos | Taxa de transferência máxima do disco em cache e armazenamento temporário: IOPS / MBps (tamanho do cache em GiB) | Taxa de transferência máxima do disco não armazenado em cache: IOPS / MBps | Máximo de NICs/Desempenho de rede esperado (Mbps) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_F1s |1 |2 |4 |2 |4.000 / 32 (12) |3.200 / 48 |2 / 750 |
| Standard_F2s |2 |4 |8 |4 |8.000 / 64 (24) |6.400 / 96 |2 / 1500 |
| Standard_F4s |4 |8 |16 |8 |16.000 / 128 (48) |12.800 / 192 |4 / 3000 |
| Standard_F8s |8 |16 |32 |16 |32.000 / 256 (96) |25.600 / 384 |8 / 6000 |
| Standard_F16s |16 |32 |64 |32 |64.000 / 512 (192) |51.200 / 768 |8 / 6000-12000 &#8224; |

MBps = 10^6 bytes por segundo e GiB = 1024^3 bytes.

* hello máximo em disco taxa de transferência (IOPS ou MBps) possível com uma série de Fs VM pode ser limitada por número de hello, tamanho e a distribuição de saudação anexada discos.  Para obter detalhes, confira [Armazenamento Premium: armazenamento de alto desempenho para cargas de trabalho das máquinas virtuais do Azure](../articles/storage/common/storage-premium-storage.md).


<br>

## <a name="f-series"></a>Série F

ACU: 210 - 250

| Tamanho         | vCPU | Memória: GiB | Armazenamento temporário (SSD) GiB | Taxa de transferência máxima de armazenamento temporário: IOPS / MBps de leitura / MBps de gravação | Discos de dados máximos / taxa de transferência: IOPS | Máximo de NICs/Desempenho de rede esperado (Mbps) |
|--------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standard_F1  | 1         | 2           | 16             | 3000 / 46 / 23                                           | 2 / 2 x 500                         | 2 / 750                 |
| Standard_F2  | 2         | 4           | 32             | 6000 / 93 / 46                                           | 4 / 4 x 500                         | 2 / 1500                     |
| Standard_F4  | 4         | 8           | 64             | 12000 / 187 / 93                                         | 8 / 8 x 500                         | 4 / 3000                     |
| Standard_F8  | 8         | 16          | 128            | 24000 / 375 / 187                                        | 16 / 16 x 500                       | 8 / 6000                     |
| Standard_F16 | 16        | 32          | 256            | 48000 / 750 / 375                                        | 32 / 32 x 500                       | 8 / 6000 - 12000 &#8224;           |


<br>


