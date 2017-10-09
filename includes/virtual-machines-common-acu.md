



Criamos o conceito de saudação do hello unidade de computação do Azure (ACU) tooprovide uma maneira de comparar o desempenho de computação (CPU) em SKUs do Azure. Isso ajudará você a identificar facilmente quais SKU é provavelmente toosatisfy suas necessidades de desempenho.  A ACU atualmente é padronizada como uma VM pequena (Standard_A1) sendo 100 e todas as SKUs representam, aproximadamente, o quanto a SKU pode executar um parâmetro de comparação padrão mais rapidamente. 

> [!IMPORTANT]
> Olá ACU é apenas uma diretriz.  Olá resultados para sua carga de trabalho podem variar. 
> 
> 

<br>

| Família de SKU | ACU \ vCPU |
| --- | --- |
| [A0](../articles/virtual-machines/windows/sizes-general.md) |50 |
| [A4 A1](../articles/virtual-machines/windows/sizes-general.md) |100 |
| [A7 A5](../articles/virtual-machines/windows/sizes-general.md) |100 |
| [A1_v2 A8_v2](../articles/virtual-machines/windows/sizes-general.md) |100 |
| [A2m_v2 A8m_v2](../articles/virtual-machines/windows/sizes-general.md) |100 |
| [A8-A11](../articles/virtual-machines/windows/sizes-hpc.md) |225* |
| [D1 D14](../articles/virtual-machines/windows/sizes-general.md) |160 |
| [D1_v2 D15_v2](../articles/virtual-machines/windows/sizes-general.md) |210 - 250* |
| [DS14 DS1](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) |160 |
| [DS1_v2 DS15_v2](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) |210-250* |
| [D_v3](../articles/virtual-machines/virtual-machines-windows-sizes-general.md) |160-190* ** |
| [Ds_v3](../articles/virtual-machines/virtual-machines-windows-sizes-general.md) |160-190* ** |
| [E_v3](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) |160-190* ** |
| [Es_v3](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) |160-190* ** |
| [F1-F16](../articles/virtual-machines/windows/sizes-compute.md) |210-250* |
| [F1s-F16s](../articles/virtual-machines/windows/sizes-compute.md) |210-250* |
| [G5 G1](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) |180 - 240* |
| [GS1 GS5](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) |180 - 240* |
| [H](../articles/virtual-machines/windows/sizes-hpc.md) |290 – 300* |
| [L4s-L32s](../articles/virtual-machines/windows/sizes-storage.md) |180 - 240* |
| [M](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) | 160-180** |

ACUs marcados com um * usar Intel® Turbo tecnologia tooincrease CPU frequência e fornecer um aumento de desempenho.  Olá aumento Olá pode variar com base no tamanho da VM hello, carga de trabalho e outras cargas de trabalho em execução no hello mesmo host.

**Hyper-threaded. 
