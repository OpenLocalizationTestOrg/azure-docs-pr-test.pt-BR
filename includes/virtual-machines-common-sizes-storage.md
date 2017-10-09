
Olá Ls série é otimizado para cargas de trabalho que exigem o armazenamento temporário de baixa latência, como bancos de dados NoSQL incluindo Cassandra, MongoDB, Cloudera e Redis. Olá Ls-series oferece até vCPUs too32 usando Olá [processador Intel® Xeon® E5 v3 família](http://www.intel.com/content/www/us/en/processors/xeon/xeon-e5-solutions.html). Olá Ls série obtém Olá mesmo desempenho de CPU como Olá série G/GS e vem com 8 GiB de memória por vCPU.  

## <a name="ls-series"></a>Série Ls

ACU: 180-240
 
| Tamanho          | vCPU | Memória: GiB | Armazenamento temporário (SSD) GiB | Discos de dados máximos | Taxa de transferência máxima do disco em cache e armazenamento temporário: IOPS / MBps (tamanho do cache em GiB) | Taxa de transferência máxima do disco não armazenado em cache: IOPS / MBps | Máximo de NICs/Desempenho de rede esperado (Mbps) | 
|---------------|-----------|-------------|--------------------------|----------------|-------------------------------------------------------------|-------------------------------------------|------------------------------| 
| Standard_L4s  | 4    | 32   | 678   | 8              | NA / NA (0)          | 5.000 / 125                               | 2 / 4000       | 
| Standard_L8s  | 8    | 64   | 1.388 | 16             | NA / NA (0)          | 10.000 / 250                              | 4 / 8000  | 
| Standard_L16s | 16   | 128  | 2.807 | 32             | NA / NA (0)          | 20.000 / 500                              | 8 / 6000 - 16000 &#8224; | 
| Standard_L32s* | 32 | 256  | 5.630 | 64             | NA / NA (0)          | 40.000 / 1.000                            | 8 / 20000 | 
 

taxa de transferência de disco máximo do Hello possível com VMs série Ls pode ser limitado pelo número de hello, tamanho e a distribuição de qualquer anexou discos. Para obter detalhes, confira [Armazenamento Premium: armazenamento de alto desempenho para cargas de trabalho das máquinas virtuais do Azure](../articles/storage/common/storage-premium-storage.md). 

* A instância é isolado toohardware tooa dedicado único cliente.

