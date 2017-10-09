
## <a name="size-table-definitions"></a>Definições da tabela de tamanhos

- A capacidade de armazenamento é mostrada em unidades de GiB ou de 1024^3 bytes. Quando comparar discos medido em GB (1000 ^ 3 bytes) toodisks medido em GiB (1024 ^ 3) lembre-se de que os números de capacidade fornecidos no GiB podem parecer menores. Por exemplo, 1023 GiB = 1098,4 GB
- A taxa de transferência do disco é medida em IOPS (operações de entrada/saída por segundo) e em MBps, em que MBps = 10^6 bytes/s.
- Os discos de dados podem operar nos modos em cache ou não armazenado em cache. Para a operação de disco de dados armazenados em cache, modo de cache do host de saudação é definido muito**ReadOnly** ou **ReadWrite**.  Para a operação de disco de dados não armazenados em cache, modo de cache do host de saudação é definido muito**nenhum**.
- **Esperado o desempenho da rede** é Olá agregados largura de banda máxima alocada por tipo VM em todas as NICs para todos os destinos. Limites superiores não são garantidos, mas são tooprovide pretendido diretrizes para selecionar o tipo correto de VM Olá para o aplicativo hello que se destina. O desempenho real da rede dependerá de uma variedade de fatores, incluindo cargas de rede e aplicativos, bem como configurações de rede. Para saber mais sobre como otimizar a taxa de transferência de rede, veja [Otimização da taxa de transferência de rede para Windows e Linux](../articles/virtual-network/virtual-network-optimize-network-bandwidth.md). Olá tooachieve esperado de desempenho de rede em Linux ou Windows, pode ser necessário tooselect uma versão específica ou otimizar sua VM. Para obter mais informações, consulte [como tooreliably testar para taxa de transferência da máquina virtual](../articles/virtual-network/virtual-network-bandwidth-testing.md).

- &#8224; desempenho de 16 vCPU consistentemente alcançará o limite superior de saudação em uma versão futura.


