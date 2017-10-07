---
title: "tamanhos de máquina aaaVirtual para serviços de nuvem do Azure | Microsoft Docs"
description: "Lista tamanhos de máquina virtual diferente da saudação (e IDs) para funções de web e de trabalho do serviço de nuvem do Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 1127c23e-106a-47c1-a2e9-40e6dda640f6
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 93d91a67afc352f3d18c31e0dd5cf976bf46350c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sizes-for-cloud-services"></a>Tamanhos dos serviços de nuvem
Este tópico descreve os tamanhos disponíveis hello e as opções de instâncias de função serviço de nuvem (funções web e funções de trabalho). Ele também fornece toobe de considerações de implantação ciente ao planejar toouse esses recursos. Cada tamanho tem uma ID que você coloca em seu [arquivo de definição de serviço](cloud-services-model-and-package.md#csdef). Os preços para cada tamanho de estão disponíveis em Olá [preços de serviços de nuvem](https://azure.microsoft.com/pricing/details/cloud-services/) página.

> [!NOTE]
> toosee relacionados a limites do Azure, consulte [assinatura do Azure e limites de serviço, cotas e restrições](../azure-subscription-service-limits.md)
>
>

## <a name="sizes-for-web-and-worker-role-instances"></a>Tamanhos de instâncias de função web e de trabalho
Existem várias toochoose de tamanhos padrão do Azure. Entre as considerações sobre algumas dessas dimensões estão:

* VMs série D são projetadas toorun aplicativos que exigem maior capacidade de computação e desempenho de disco temporário. VMs série D fornecem processadores mais rápidos, uma maior taxa de memória por núcleo e uma unidade de estado sólida (SSD) para o disco temporário hello. Para obter detalhes, consulte comunicado Olá no hello blog do Azure, [novos tamanhos de máquina Virtual da série D](https://azure.microsoft.com/blog/2014/09/22/new-d-series-virtual-machine-sizes/).
* Dv2 série, um acompanhamento toohello D-series original, apresenta uma CPU mais eficiente. Olá Dv2 série CPU é cerca de 35% mais rápido do que Olá CPU da série D. Ele se baseia Olá última geração v3 de 2,4 GHz Intel Xeon® E5-2673 processador (Haswell) e com hello Intel Turbo aumento tecnologia 2.0, pode subir too3.1 GHz. Olá Dv2 série tem Olá mesmas configurações de disco e memória conforme Olá série D.
* As VMs da série G oferecem hello mais memória e executadas em hosts que têm processadores da família Intel Xeon E5 V3.
* Olá VMs série pode ser implantado em vários tipos de hardware e processadores. tamanho de saudação é limitado, com base em hardware hello, toooffer o desempenho do processador consistente para Olá executando a instância, independentemente do hardware de saudação em que é implantado. toodetermine Olá hardware físico em que esse tamanho for implantado, consulta Olá hardware virtual de dentro de saudação Máquina Virtual.
* Olá Tamanho A0 for assinada em excesso no hardware físico hello. Para esse tamanho específico apenas, outras implantações de cliente podem afetar o desempenho de saudação da carga de trabalho em execução. desempenho relativo de saudação é descrito a seguir como Olá esperado da linha de base, assunto tooan aproximado a variabilidade de 15%.

tamanho de saudação da máquina virtual de saudação afeta Olá preços. tamanho de saudação também afeta a capacidade de processamento, memória e armazenamento de saudação da máquina virtual de saudação. Os custos de armazenamento são calculados separadamente com base nas páginas usadas na conta de armazenamento hello. Para obter detalhes, confira [Detalhes de preços dos Serviços de Nuvem](https://azure.microsoft.com/pricing/details/cloud-services/) e [Preços do Armazenamento do Azure](https://azure.microsoft.com/pricing/details/storage/).

Olá considerações a seguir pode ajudá-lo a escolher um tamanho:

* Olá tamanhos A8 A11 e H série também são conhecidas como *instâncias de computação intensiva*. hardware de saudação que executa esses tamanhos é projetado e otimizado para computação intensa e aplicativos, modelagem e simulações de cluster de aplicativos com uso intensivo de rede, incluindo a computação de alto desempenho (HPC). Olá A8 A11 série usa Intel Xeon E5-2670 @ 2.6 GHZ e Olá H série v3 Intel Xeon E5-2667 @ 3,2 GHz. Para obter informações detalhadas e considerações sobre o uso desses tamanhos, veja [Tamanhos de VM de computação de alto desempenho](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* As séries Dv2 e D e G são ideais para aplicativos que exigem CPUs mais rápidas, melhor desempenho de disco local ou que têm uma maior demanda de memória. Elas oferecem uma combinação poderosa para vários aplicativos de nível empresarial.
* Alguns dos hosts físicos de saudação em data centers do Azure podem não aceitar tamanhos de máquina virtual maiores, como A5 – A11. Como resultado, você verá a mensagem de erro de saudação **máquina virtual de tooconfigure falha {nome da máquina}** ou **máquina virtual de toocreate falha {nome da máquina}** ao redimensionar uma tooa de máquina virtual existente novo tamanho; Criando uma nova máquina virtual em uma rede virtual criada antes de 16 de abril de 2013; ou adicionando um nova máquina virtual tooan serviço de nuvem existente. Consulte [erro: "Falha na máquina de virtual de tooconfigure"](https://social.msdn.microsoft.com/Forums/9693f56c-fcd3-4d42-850e-5e3b56c7d6be/error-failed-to-configure-virtual-machine-with-a5-a6-or-a7-vm-size?forum=WAVirtualMachinesforWindows) no Fórum de suporte de saudação de soluções alternativas para cada cenário de implantação.
* Sua assinatura também pode limitar o número de saudação de núcleos que podem ser implantados em determinadas famílias de tamanho. tooincrease uma cota, entre em contato com o suporte do Azure.

## <a name="performance-considerations"></a>Considerações sobre o desempenho
Nós criamos conceito de saudação de saudação unidade de computação do Azure (ACU) tooprovide uma maneira de comparar o desempenho de computação (CPU) em SKUs do Azure e tooidentify que SKU é provavelmente toosatisfy o desempenho precisa.  A ACU atualmente é padronizada como uma VM pequena (Standard_A1) sendo 100 e todas as SKUs representam, aproximadamente, o quanto a SKU pode executar um parâmetro de comparação padrão mais rapidamente.

> [!IMPORTANT]
> Olá ACU é apenas uma diretriz. Olá resultados para sua carga de trabalho podem variar.
>
>

<br>

| Família de SKU | ACU/núcleo |
| --- | --- |
| [ExtraSmall](#a-series) |50 |
| [Small-ExtraLarge](#a-series) |100 |
| [A5-7](#a-series) |100 |
| [Standard_A1-8v2](#av2-series) |100 |
| [Standard_A2m-8mv2](#av2-series) |100 |
| [A8-A11](#a-series) |225* |
| [D1-14](#d-series) |160 |
| [D1-15v2](#dv2-series) |210 - 250* |
| [G1-5](#g-series) |180 - 240* |
| [H](#h-series) |290 – 300* |

ACUs marcados com um * usar Intel® Turbo tecnologia tooincrease CPU frequência e fornecer um aumento de desempenho. Olá aumento Olá pode variar com base no tamanho da VM hello, carga de trabalho e outras cargas de trabalho em execução no hello mesmo host.

## <a name="size-tables"></a>Tabelas de tamanho
Hello tabelas a seguir mostram tamanhos hello e capacidades de saudação que eles fornecem.

* A capacidade de armazenamento é mostrada em unidades de GiB ou de 1024^3 bytes. Quando comparar discos medido em GB (1000 ^ 3 bytes) toodisks medido em GiB (1024 ^ 3) lembre-se de que os números de capacidade fornecidos no GiB podem parecer menores. Por exemplo, 1023 GiB = 1098,4 GB
* A taxa de transferência do disco é medida em IOPS (operações de entrada/saída por segundo) e em MBps, em que MBps = 10^6 bytes/s.
* Os discos de dados podem operar nos modos em cache ou não armazenado em cache. Para a operação de disco de dados armazenados em cache, modo de cache do host de saudação é definido muito**ReadOnly** ou **ReadWrite**. Para a operação de disco de dados não armazenados em cache, modo de cache do host de saudação é definido muito**nenhum**.
* Largura de banda de rede máxima é Olá agregados largura de banda máxima alocada e atribuído por tipo VM. a largura de banda máxima Olá fornece orientação para a seleção de Olá direita VM tipo tooensure capacidade adequada de rede está disponível. Ao mover entre baixa, moderada, alta e muito alta, taxa de transferência Olá também aumenta. O desempenho real da rede dependerá de vários fatores, incluindo cargas de rede e aplicativos, bem como configurações de rede do aplicativo.

## <a name="a-series"></a>Séria A
| Tamanho            | Núcleos de CPU | Memória: GiB  | HDD local: GiB       | NICs máximas / largura de banda da rede |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| ExtraSmall      | 1         | 0,768        | 20                   | 1 / baixa |
| Pequena           | 1         | 1,75         | 225                  | 1 / moderada |
| Média          | 2         | 3,5 GB       | 490                  | 1 / moderada |
| Grande           | 4         | 7            | 1000                 | 2 / alta |
| ExtraLarge      | 8         | 14           | 2040                 | 4 / alta |
| A5              | 2         | 14           | 490                  | 1 / moderada |
| A6              | 4         | 28           | 1000                 | 2 / alta |
| A7              | 8         | 56           | 2040                 | 4 / alta |

## <a name="a-series---compute-intensive-instances"></a>Série A – Instâncias de computação intensiva
Para obter informações e considerações sobre o uso desses tamanhos, veja [Tamanhos de VM de computação de alto desempenho](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

| Tamanho            | Núcleos de CPU | Memória: GiB  | HDD local: GiB       | NICs máximas / largura de banda da rede |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| A8*             |8          | 56           | 1817                 | 2 / alta |
| A9*             |16         | 112          | 1817                 | 4 / muito alta |
| A10             |8          | 56           | 1817                 | 2 / alta |
| A11             |16         | 112          | 1817                 | 4 / muito alta |

\*Compatível com RDMA

## <a name="av2-series"></a>Série Av2

| Tamanho            | Núcleos de CPU | Memória: GiB  | SSD local: GiB       | NICs máximas / largura de banda da rede |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standard_A1_v2  | 1         | 2            | 10                   | 1 / moderada                 |
| Standard_A2_v2  | 2         | 4            | 20                   | 2 / moderada                 |
| Standard_A4_v2  | 4         | 8            | 40                   | 4 / alta                     |
| Standard_A8_v2  | 8         | 16           | 80                   | 8 / alta                     |
| Standard_A2m_v2 | 2         | 16           | 20                   | 2 / moderada                 |
| Standard_A4m_v2 | 4         | 32           | 40                   | 4 / alta                     |
| Standard_A8m_v2 | 8         | 64           | 80                   | 8 / alta                     |


## <a name="d-series"></a>Série D
| Tamanho            | Núcleos de CPU | Memória: GiB  | SSD local: GiB       | NICs máximas / largura de banda da rede |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standard_D1     | 1         | 3,5          | 50                   | 1 / moderada |
| Standard_D2     | 2         | 7            | 100                  | 2 / alta |
| Standard_D3     | 4         | 14           | 200                  | 4 / alta |
| Standard_D4     | 8         | 28           | 400                  | 8 / alta |
| Standard_D11    | 2         | 14           | 100                  | 2 / alta |
| Standard_D12    | 4         | 28           | 200                  | 4 / alta |
| Standard_D13    | 8         | 56           | 400                  | 8 / alta |
| Standard_D14    | 16        | 112          | 800                  | 8 / muito alta |

## <a name="dv2-series"></a>Série Dv2
| Tamanho            | Núcleos de CPU | Memória: GiB  | SSD local: GiB       | NICs máximas / largura de banda da rede |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standard_D1_v2  | 1         | 3,5          | 50                   | 1 / moderada |
| Standard_D2_v2  | 2         | 7            | 100                  | 2 / alta |
| Standard_D3_v2  | 4         | 14           | 200                  | 4 / alta |
| Standard_D4_v2  | 8         | 28           | 400                  | 8 / alta |
| Standard_D5_v2  | 16        | 56           | 800                  | 8 / extremamente alta |
| Standard_D11_v2 | 2         | 14           | 100                  | 2 / alta |
| Standard_D12_v2 | 4         | 28           | 200                  | 4 / alta |
| Standard_D13_v2 | 8         | 56           | 400                  | 8 / alta |
| Standard_D14_v2 | 16        | 112          | 800                  | 8 / extremamente alta |
| Standard_D15_v2 | 20        | 140          | 1.000                | 8 / extremamente alta |

## <a name="g-series"></a>Série G
| Tamanho            | Núcleos de CPU | Memória: GiB  | SSD local: GiB       | NICs máximas / largura de banda da rede |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standard_G1     | 2         | 28           | 384                  |1 / alta |
| Standard_G2     | 4         | 56           | 768                  |2 / alta |
| Standard_G3     | 8         | 112          | 1.536                |4 / muito alta |
| Standard_G4     | 16        | 224          | 3.072                |8 / extremamente alta |
| Standard_G5     | 32        | 448          | 6.144                |8 / extremamente alta |

## <a name="h-series"></a>Série H
Máquinas virtuais do Azure H-series são Olá próxima geração computação de alto desempenho que VMs visam necessidades computacionais high-end, como modelagem molecular e dinâmica de fluidos computacional. Esses 8 e 16 núcleos VMs baseiam-se na tecnologia de processador Olá Intel 2667 Haswell E5 V3 apresentando DDR4 memória e armazenamento baseado em SSD local.

Além disso toohello substancial de energia da CPU, Olá H-series oferece diversas opções de rede de RDMA de baixa latência usando FDR InfiniBand e várias configurações toosupport memória intensiva computacional requisitos de memória.

| Tamanho            | Núcleos de CPU | Memória: GiB  | SSD local: GiB       | NICs máximas / largura de banda da rede |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standard_H8     | 8         | 56           | 1000                 | 8 / alta |
| Standard_H16    | 16        | 112          | 2000                 | 8 / muito alta |
| Standard_H8m    | 8         | 112          | 1000                 | 8 / alta |
| Standard_H16m   | 16        | 224          | 2000                 | 8 / muito alta |
| Standard_H16r*  | 16        | 112          | 2000                 | 8 / muito alta |
| Standard_H16mr* | 16        | 224          | 2000                 | 8 / muito alta |

\*Compatível com RDMA

## <a name="configure-sizes-for-cloud-services"></a>Configurar tamanhos para os Serviços de Nuvem
Você pode especificar o tamanho da máquina Virtual de saudação de uma instância de função como parte do modelo de serviço Olá descrito pelo Olá [arquivo de definição de serviço](cloud-services-model-and-package.md#csdef). tamanho de saudação da função hello determina o número de saudação de núcleos de CPU, capacidade de memória hello e tamanho de sistema de arquivo local Olá alocada tooa instância em execução. Escolha o tamanho da função hello com base em requisitos de recursos do aplicativo.

Aqui está um exemplo de configuração toobe de tamanho de função hello [Standard_D2](#general-purpose-d) para uma instância de função Web:

```xml
<WorkerRole name="Worker1" vmsize="Standard_D2">
...
</WorkerRole>
```

## <a name="changing-hello-size-of-an-existing-role"></a>Alterando o tamanho de saudação de uma função existente

Como a natureza Olá as alterações de carga de trabalho ou novos tamanhos VM se tornar disponíveis, talvez você queira toochange tamanho de saudação de sua função. toodo, portanto, você deve alterar o tamanho da VM Olá em seu arquivo de definição de serviço (como mostrado acima), reempacotar seu serviço de nuvem e implantá-lo. Não é possível toochange tamanhos de VM diretamente do portal de saudação ou o PowerShell.

>[!TIP]
> Você talvez queira toouse diferentes tamanhos de VM para sua função em diferentes ambientes (por exemplo. teste versus produção). Uma maneira toodo isso é toocreate vários arquivos de definição (. csdef) do serviço em seu projeto e criar pacotes de serviço por ambiente de nuvem diferente durante a compilação automatizada usando a ferramenta CSPack de saudação. pacote de serviços toolearn mais informações sobre os elementos de saudação de uma nuvem e como toocreate-los, consulte [novidades nuvem Olá serviços modelo e como empacotá-lo?](cloud-services-model-and-package.md)
>
>

## <a name="get-a-list-of-sizes"></a>Obter uma lista de tamanhos
Você pode usar o PowerShell ou hello API REST tooget uma lista de tamanhos. Olá API REST está documentada [aqui](https://msdn.microsoft.com/library/azure/dn469422.aspx). Olá código a seguir é um comando do PowerShell que listará todos os tamanhos de saudação atualmente disponíveis para seu serviço de nuvem.

```powershell
Get-AzureRoleSize | where SupportedByWebWorkerRoles -eq $true | select InstanceSize
```

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre a [assinatura do Azure e limites de serviços, cotas e restrições](../azure-subscription-service-limits.md).
* Saiba mais [sobre tamanhos de VM de computação de alto desempenho](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para cargas de trabalho do HPC.
