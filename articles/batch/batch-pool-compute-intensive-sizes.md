---
title: "computação intensa aaaUse VMs do Azure com o lote | Microsoft Docs"
description: "Como os tamanhos de tootake vantagem de VM compatíveis com RDMA ou GPU habilitado nos pools de lote do Azure"
services: batch
documentationcenter: 
author: dlepow
manager: timlt
editor: 
ms.assetid: 
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: danlep
ms.openlocfilehash: 6a462a5f2a44ddcec8bf4e5c200d444cac8fafe6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-rdma-capable-or-gpu-enabled-instances-in-batch-pools"></a>Usar instâncias compatíveis com RDMA ou habilitadas para GPU em pools do Lote

toorun determinados trabalhos de lote, talvez você queira tootake vantagem dos tamanhos de VM do Azure criado para a computação em larga escala. Por exemplo, toorun várias instâncias [cargas de trabalho MPI](batch-mpi.md), você pode escolher A8, A9, ou tamanhos H-series que tem uma rede de interface para direto memória RDMA (acesso remoto). Esses tamanhos de se conectar a rede InfiniBand de tooan para comunicação entre nós, o que pode acelerar aplicativos MPI. Ou, para aplicativos CUDA, você pode escolher tamanhos da série N que incluem cartões de GPU (unidade de processamento gráfico) da NVIDIA Tesla.

Este artigo fornece diretrizes e exemplos toouse alguns dos tamanhos de especializada do Azure nos pools de lote. Para obter especificações e contexto, consulte:

* Tamanhos de VM de computação de alto desempenho ([Linux](../virtual-machines/linux/sizes-hpc.md), [Windows](../virtual-machines/windows/sizes-hpc.md)) 

* Tamanhos de VM habilitados para GPU ([Linux](../virtual-machines/linux/sizes-gpu.md), [Windows](../virtual-machines/windows/sizes-gpu.md)) 


## <a name="subscription-and-account-limits"></a>Limites de assinatura e de conta

* **Cotas** -um ou mais cotas do Azure podem limitar Olá número ou tipo de nós, você pode adicionar pool de lote tooa. Você é mais provável toobe limitada quando você escolher compatíveis com RDMA, GPU habilitado, ou outros tamanhos de VM com vários núcleos. Dependendo do tipo de saudação da conta de lote criado, as cotas de Olá podem se aplicam a própria conta toohello ou tooyour assinatura.

    * Se você criou sua conta de lote no hello **serviço de lote** configuração, você está limitado pela Olá [cota de núcleos dedicados por conta do lote](batch-quota-limit.md#resource-quotas). Por padrão, essa cota é de 20 núcleos. Uma cota separada aplica-se muito[VMs de baixa prioridade](batch-low-pri-vms.md), se você usá-los. 

    * Se você criou a conta de saudação em Olá **assinatura de usuário** configuração, sua assinatura limita o número de saudação de núcleos VM por região. Veja [Assinatura do Azure e limites, cotas e restrições de serviço](../azure-subscription-service-limits.md). Sua assinatura também se aplica a um tamanhos de VM toocertain cota regional, incluindo as instâncias HPC e GPU. Na configuração de assinatura de usuário hello, sem cotas adicionais se aplicam a conta do lote toohello. 

  Talvez seja necessário tooincrease um ou mais cotas ao usar um tamanho VM especializado em lote. toorequest um aumento de cota, abra um [solicitação de suporte do cliente online](../azure-supportability/how-to-create-azure-support-request.md) sem custo adicional.

* **Disponibilidade de região** - computação intensa VMs podem não estar disponíveis em regiões Olá onde você pode criar suas contas do Batch. toocheck que um tamanho estiver disponível, consulte [produtos disponíveis por região](https://azure.microsoft.com/regions/services/).


## <a name="dependencies"></a>Dependências

Olá RDMA e os recursos GPU de tamanhos de computação intensa têm suporte apenas em determinados sistemas operacionais. Dependendo do seu sistema operacional, talvez você precise tooinstall ou configurar o driver adicional ou outros softwares. Olá tabelas a seguir resume essas dependências. Consulte os artigos vinculados para obter detalhes. Para pools de lote de tooconfigure de opções, consulte mais adiante neste artigo.


### <a name="linux-pools---virtual-machine-configuration"></a>Pools do Linux – configuração de máquina virtual

| Tamanho | Recurso | Sistemas operacionais | Software necessário | Configurações do pool |
| -------- | -------- | ----- |  -------- | ----- |
| [H16r, H16mr, A8, A9](../virtual-machines/linux/sizes-hpc.md#rdma-capable-instances) | RDMA | SUSE Linux Enterprise Server 12 HPC ou<br/>HPC baseado em CentOS<br/>(Azure Marketplace) | Intel MPI 5 | Habilitar a comunicação entre nós, desabilitar a execução de tarefas simultâneas |
| [Série NC*](../virtual-machines/linux/n-series-driver-setup.md#install-cuda-drivers-for-nc-vms) | GPU NVIDIA Tesla K80 | Ubuntu 16.04 LTS.<br/>Red Hat Enterprise Linux 7.3 ou<br/>CentOS 7.3<br/>(Azure Marketplace) | Drivers NVIDIA CUDA Toolkit 8.0 | N/D | 
| [Série NV](../virtual-machines/linux/n-series-driver-setup.md#install-grid-drivers-for-nv-vms) | GPU NVIDIA Tesla M60 | Ubuntu 16.04 LTS<br/>Red Hat Enterprise Linux 7.3<br/>CentOS 7.3<br/>(Azure Marketplace) | Drivers NVIDIA GRID 4.3 | N/D |

* A conectividade RDMA em VMs NC24r tem suporte em HPC baseado em CentOS 7.3 com Intel MPI.



### <a name="windows-pools---virtual-machine-configuration"></a>Pools do Windows – configuração de máquina virtual

| Tamanho | Recurso | Sistemas operacionais | Software necessário | Configurações do pool |
| -------- | ------ | -------- | -------- | ----- |
| [H16r, H16mr, A8, A9](../virtual-machines/windows/sizes-hpc.md#rdma-capable-instances) | RDMA | Windows Server 2012 R2 ou<br/>Windows Server 2012 (Azure Marketplace) | Microsoft MPI 2012 R2 ou posterior, ou<br/> Intel MPI 5<br/><br/>Extensão de VM do Azure HpcVMDrivers | Habilitar a comunicação entre nós, desabilitar a execução de tarefas simultâneas |
| [Série NC*](../virtual-machines/windows/n-series-driver-setup.md) | GPU NVIDIA Tesla K80 | Windows Server 2016 ou <br/>Windows Server 2012 R2 (Azure Marketplace) | Drivers NVIDIA Tesla ou drivers CUDA Toolkit 8.0| N/D | 
| [Série NV](../virtual-machines/windows/n-series-driver-setup.md) | GPU NVIDIA Tesla M60 | Windows Server 2016 ou<br/>Windows Server 2012 R2 (Azure Marketplace) | Drivers NVIDIA GRID 4.3 | N/D |

* A conectividade RDMA em VMs NC24r tem suporte no Windows Server 2012 R2 com a extensão HpcVMDrivers e Microsoft MPI ou Intel MPI.

### <a name="windows-pools---cloud-services-configuration"></a>Pools do Windows – configuração de serviços de nuvem

> [!NOTE]
> Não há suporte para tamanhos de N-series em pools de lote com a configuração de serviços de nuvem hello.
>

| Tamanho | Recurso | Sistemas operacionais | Software necessário | Configurações do pool |
| -------- | ------- | -------- | -------- | ----- |
| [H16r, H16mr, A8, A9](../virtual-machines/windows/sizes-hpc.md#rdma-capable-instances) | RDMA | Windows Server 2012 R2,<br/>Windows Server 2012 ou<br/>Windows Server 2008 R2 (família do SO convidado) | Microsoft MPI 2012 R2 ou posterior, ou<br/>Intel MPI 5<br/><br/>Extensão de VM do Azure HpcVMDrivers | Habilitar a comunicação entre nós,<br/> desabilitar a execução de tarefas simultâneas |





## <a name="pool-configuration-options"></a>Opções de configuração do pool

tooconfigure um tamanho VM especializado para seu pool de lote, Olá APIs de lote e ferramentas fornecem vários software de tooinstall necessário de opções ou drivers, incluindo:

* [Iniciar tarefa](batch-api-basics.md#start-task) -carregar um pacote de instalação como um arquivo de recurso tooan conta de armazenamento do Azure Olá mesma região Olá conta do lote. Crie um arquivo de recurso Iniciar tarefa linha de comando tooinstall Olá silenciosamente ao pool Olá inicia. Para obter mais informações, consulte Olá [documentação da API REST](/rest/api/batchservice/add-a-pool-to-an-account#bk_starttask).

  > [!NOTE] 
  > Olá Iniciar tarefa deve ser executada com permissões com privilégios elevados (administrador) e ele deve esperar para o sucesso.
  >

* [Pacote de aplicativo](batch-application-packages.md) - adicionar um pacote de instalação compactado tooyour conta em lotes e configurar uma referência de pacote no pool de saudação. Essa configuração carrega e descompacta o pacote de saudação em todos os nós no pool de saudação. Se o pacote de saudação é um instalador, crie um aplicativo hello Iniciar tarefa linha de comando toosilently instalar em todos os nós de pool. Opcionalmente, instale o pacote de saudação quando uma tarefa está agendada toorun em um nó.

* [Imagem de pool personalizado](batch-api-basics.md#pool) - criar uma personalizada do Windows ou imagem de VM do Linux que contém os drivers, software ou outras configurações necessárias para Olá tamanho da VM. Se você criou sua conta em lotes na configuração de assinatura de usuário hello, especifique a imagem personalizada Olá para o pool de lote. (Imagens personalizadas não têm suporte nas contas na configuração de serviço de lote hello.) Imagens personalizadas podem ser usadas somente com os pools na configuração de máquina virtual de saudação.

  > [!IMPORTANT]
  > Nos pools do Lote, não possível usar uma imagem personalizada criada com discos gerenciados ou com o armazenamento Premium no momento.
  >



* [Lote Shipyard](https://github.com/Azure/batch-shipyard) configura automaticamente toowork GPU e RDMA Olá transparentemente com cargas de trabalho em contêineres em lote do Azure. O Batch Shipyard é totalmente controlado por arquivos de configuração. Há muitos exemplos receita de configurações disponíveis que permitem a cargas de trabalho GPU e RDMA como Olá [CNTK GPU receita](https://github.com/Azure/batch-shipyard/tree/master/recipes/CNTK-GPU-OpenMPI) que pré-configura usando drivers de GPU em VMs série N e carrega o software Microsoft cognitivas Toolkit como uma imagem do Docker.


## <a name="example-microsoft-mpi-on-an-a8-vm-pool"></a>Exemplo: Microsoft MPI em um pool de VM A8

aplicativos de MPI Windows toorun em um conjunto de nós do Azure A8, é necessário tooinstall uma implementação de MPI com suporte. Aqui estão exemplo etapas tooinstall [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) em um Windows pool usando um pacote de aplicativo do lote.

1. Baixar Olá [o pacote de instalação](http://go.microsoft.com/FWLink/p/?LinkID=389556) (MSMpiSetup.exe) para a versão mais recente de saudação do Microsoft MPI.
2. Crie um arquivo zip do pacote de saudação.
3. Carregar a conta do lote Olá pacote tooyour. Para obter as etapas, consulte Olá [pacotes de aplicativos](batch-application-packages.md) orientação. Especifique uma ID de aplicativo, como *MSMPI*e uma versão, como *8.1*. 
4. Usando Olá APIs de lote ou o portal do Azure, crie um pool na configuração de serviços de nuvem Olá com número de saudação desejado de nós e a escala. Olá tabela a seguir mostra exemplo configurações tooset backup MPI no modo autônomo usando uma tarefa de início:

| Configuração | Valor |
| ---- | ----- | 
| **Tipo de imagem** | Serviços de Nuvem |
| **Família de sistema operacional** | Windows Server 2012 R2 (família de SO 4) |
| **Tamanho do nó** | A8 Standard |
| **Comunicação entre nós habilitada** | True  |
| **Máx. de tarefas por nó** | 1 |
| **Referências do pacote de aplicativos** | MSMPI |
| **Tarefa inicial habilitada** | True <br>**Linha de comando** - `"cmd /c %AZ_BATCH_APP_PACKAGE_MSMPI#8.1%\\MSMpiSetup.exe -unattend -force"`<br/>**Identidade de usuário** – Pool autouser, administrador<br/>**Aguardar o êxito** – True

## <a name="example-nvidia-tesla-drivers-on-nc-vm-pool"></a>Exemplo: drivers NVIDIA Tesla em pool de VM NC

aplicativos de CUDA toorun em um conjunto de nós do Linux NC, é necessário tooinstall CUDA Toolkit 8.0 em nós de saudação. Olá Toolkit instala drivers de NVIDIA Tesla GPU necessário hello. Aqui estão as etapas de exemplo toodeploy uma imagem personalizada do Ubuntu 16.04 LTS com drivers de GPU Olá:

1. Implante uma VM do Azure NC6 que execute o Ubuntu 16.04 LTS. Por exemplo, crie hello VM na região nos Sul Central hello. Certifique-se de que você crie Olá VM com o armazenamento padrão, e *sem* discos gerenciado.
2. Siga Olá etapas tooconnect toohello VM e [instalar drivers CUDA](../virtual-machines/linux/n-series-driver-setup.md#install-cuda-drivers-for-nc-vms).
3. Desprovisionar o agente do Linux hello e, em seguida, capturar a imagem de VM do Linux usando comandos Olá 1.0 da CLI do Azure. Para obter as etapas, consulte [Capturar uma máquina virtual do Linux em execução no Azure](../virtual-machines/linux/capture-image-nodejs.md). Tome nota do URI da imagem hello.
  > [!IMPORTANT]
  > Não use imagem de saudação do Azure 2.0 do CLI comandos toocapture de lote do Azure. No momento comandos Olá 2.0 do CLI capturam somente máquinas virtuais criadas usando discos gerenciados.
  >
4. Crie uma conta de lote, com a configuração de assinatura de usuário hello, em uma região que dá suporte a VMs NC.
5. Usando Olá APIs de lote ou o portal do Azure, crie um pool usando a imagem personalizada hello e com hello desejado no número de nós e a escala. Olá tabela a seguir mostra as configurações do pool de exemplo para imagem hello:

| Configuração | Valor |
| ---- | ---- |
| **Tipo de imagem** | Imagem personalizada |
| **Imagem personalizada** | URI do formulário de saudação da imagem`https://yourstorageaccountdisks.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd` |
| **SKU do agente do nó** | batch.node.ubuntu 16.04 |
| **Tamanho do nó** | NC6 Standard |



## <a name="next-steps"></a>Próximas etapas

* toorun de trabalhos MPI em um pool de lote do Azure, consulte Olá [Windows](batch-mpi.md) ou [Linux](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/) exemplos.

* Para obter exemplos de cargas de trabalho GPU em lote, consulte Olá [Shipyard lote](https://github.com/Azure/batch-shipyard/) receitas.
