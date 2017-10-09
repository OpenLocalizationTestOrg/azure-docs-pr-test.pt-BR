<!-- A-series - compute-intensive instances, H-series -->

Olá tamanhos A8 A11 e H série também são conhecidas como *instâncias de computação intensiva*. hardware de saudação que executa esses tamanhos é projetado e otimizado para computação intensa e aplicativos, modelagem e simulações de cluster de aplicativos com uso intensivo de rede, incluindo a computação de alto desempenho (HPC). Olá A8 A11 série usa Intel Xeon E5-2670 @ 2.6 GHZ e Olá H série v3 Intel Xeon E5-2667 @ 3,2 GHz. 

Máquinas virtuais do Azure H-series são Olá próxima geração computação de alto desempenho que VMs visam necessidades computacionais high-end, como modelagem molecular e dinâmica de fluidos computacional. Esses 8 e 16 vCPU VMs baseiam-se na tecnologia de processador Olá Intel 2667 Haswell E5 V3 com DDR4 memória e armazenamento temporário baseada em SSD. 

Além disso toohello substancial de energia da CPU, Olá H-series oferece diversas opções de rede de RDMA de baixa latência usando FDR InfiniBand e várias configurações toosupport memória intensiva computacional requisitos de memória.



## <a name="h-series"></a>Série H

ACU: 290-300

| Tamanho | vCPU | Memória: GiB | Armazenamento temporário (SSD) GiB | Discos de dados máximos | Taxa de transferência máxima do disco: IOPS | Máximo de NICs |
| --- | --- | --- | --- | --- | --- | --- |
| Standard_H8 |8 |56 |1000 |16 |16 x 500 |2  |
| Standard_H16 |16 |112 |2000 |32 |32 x 500 |4 |
| Standard_H8m |8 |112 |1000 |16 |16 x 500 |2  |
| Standard_H16m |16 |224 |2000 |32 |32 x 500 |4  |
| Standard_H16r* |16 |112 |2000 |32 |32 x 500 |4  |
| Standard_H16mr* |16 |224 |2000 |32 |32 x 500 |4 |

*Para os aplicativos MPI, a rede de back-end RDMA dedicada é habilitada pela rede InfiniBand FDR, que fornece latência ultrabaixa e largura de banda alta.

<br>



## <a name="a-series---compute-intensive-instances"></a>Série A – Instâncias de computação intensiva

ACU: 225

| Tamanho | vCPU | Memória: GiB | Armazenamento temporário (HDD): GiB | Discos de dados máximos | Taxa de transferência máxima do disco de dados: IOPS | Máximo de NICs|
| --- | --- | --- | --- | --- | --- | --- |
| Standard_A8* |8 |56 |382 |16 |16 x 500 |2 |
| Standard_A9* |16 |112 |382 |16 |16 x 500 |4 |
| Standard_A10 |8 |56 |382 |16 |16 x 500 |2  |
| Standard_A11 |16 |112 |382 |16 |16 x 500 |4 |

*Para os aplicativos MPI, a rede de back-end RDMA dedicada é habilitada pela rede InfiniBand FDR, que fornece latência ultrabaixa e largura de banda alta.

<br>



