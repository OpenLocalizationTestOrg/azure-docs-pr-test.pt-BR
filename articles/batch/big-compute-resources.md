---
title: "aaaResources de lote e HPC na nuvem do Azure da saudação | Microsoft Docs"
description: "Lista os recursos técnicos toohelp executar sua paralela em grande escala, lote e cargas de trabalho (HPC) no Azure de computação de alto desempenho."
services: batch, cloud-services, virtual-machines
documentationcenter: 
author: dlepow
manager: timlt
editor: 
ms.assetid: 6f8be911-c841-41ae-88d3-3bcfc029eb7f
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: big-compute
ms.date: 03/17/2017
ms.author: danlep
ms.openlocfilehash: ab8ba24678bd7ec090306b501d29ca63c4fb83ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="big-compute-in-azure-technical-resources-for-batch-and-high-performance-computing"></a>Big Compute no Azure: recursos técnicos para computação em lote e de alto desempenho
Este é um guia tootechnical recursos toohelp que você executar o paralela em grande escala, lote e cargas de trabalho de computação de alto desempenho (HPC) no Azure. Estenda o lote existente ou toohello de cargas de trabalho do HPC nuvem do Azure, ou criar novas soluções de computação intensa usando os serviços de um intervalo do Azure.

## <a name="solutions-options"></a>Opções de soluções
Saiba mais sobre opções de computação intensa no Azure e escolha a abordagem certa Olá para suas necessidades de negócios e a carga de trabalho.

* [Soluções de HPC e Lote](batch-hpc-solutions.md)
* [Vídeo: Computação intensa na nuvem Olá com o Azure e HPC](https://azure.microsoft.com/documentation/videos/teched-europe-2014-big-compute-in-the-cloud-with-high-performance-computing-on-azure/)

## <a name="azure-batch"></a>Lote do Azure
[Lote](https://azure.microsoft.com/services/batch/) é um serviço de plataforma que torna mais fácil toocloud-habilitar seus aplicativos Linux e Windows e executados trabalhos sem configurar e gerenciar um cluster e o trabalho do Agendador. Use aplicativos de cliente Olá SDK toointegrate com lote do Azure por meio de vários idiomas, estágio tooAzure de dados e criar pipelines de execução do trabalho.

* [Documentação](https://azure.microsoft.com/documentation/services/batch/)
* Referência do [.NET](https://msdn.microsoft.com/library/azure/mt348682.aspx), [Python](http://azure-sdk-for-python.readthedocs.io/latest/), [Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/), [Java](http://azure.github.io/azure-sdk-for-java/) e da API [REST](https://msdn.microsoft.com/library/azure/dn820158.aspx)
* [Biblioteca do .NET de gerenciamento do lote](https://msdn.microsoft.com/library/mt463120.aspx) 
* Tutoriais: Introdução à [Biblioteca de lote do Azure para .NET](batch-dotnet-get-started.md) e para o [cliente Python do Lot](batch-python-tutorial.md)
* [Fórum do lote](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurebatch)
* [Vídeos de lote](https://azure.microsoft.com/documentation/videos/index/?services=batch)

## <a name="hpc-cluster-solutions"></a>Soluções de cluster HPC
Implantar ou estenda sua toorun de tooAzure de cluster Windows ou Linux HPC existente suas cargas de trabalho intensivas de computação.  

### <a name="microsoft-hpc-pack"></a>Microsoft HPC Pack
O HPC Pack é a solução de HPC gratuita da Microsoft fundamentada nas tecnologias Microsoft Azure e Windows Server, capaz de executar cargas de trabalho do HPC no Windows e Linux.  

* [Baixe o HPC Pack 2016](https://www.microsoft.com/download/details.aspx?id=54507)
* [Baixe a atualização 3 do HPC Pack 2012 R2](https://www.microsoft.com/download/details.aspx?id=49922)
* [Documentação](https://technet.microsoft.com/library/jj899572.aspx)
* Opções de cluster HPC Pack no Azure: [Linux](../virtual-machines/linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) e [Windows](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 
* [Intermitência tooAzure instâncias de trabalho com o HPC Pack](https://technet.microsoft.com/library/gg481749.aspx)
* [Intermitência tooAzure em lotes com o HPC Pack](https://technet.microsoft.com/library/mt612877.aspx)
* [Fóruns do Windows HPC](https://social.microsoft.com/Forums/home?category=windowshpc)

### <a name="linux-and-oss-cluster-solutions"></a>Soluções de cluster do Linux e OSS
Use esses toodeploy modelos do Azure Linux HPC clusters.

* [Crie um cluster SLURM](https://azure.microsoft.com/documentation/templates/slurm/) e uma [postagem de blog](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx)
* [Crie um cluster de Torque](https://azure.microsoft.com/documentation/templates/torque-cluster/)
* [Modelos de grade de computação com o PBS Professional](https://github.com/xpillons/azure-hpc/tree/master/Compute-Grid-Infra)

## <a name="hpc-storage"></a>Armazenamento HPC
* [Sistemas de arquivos paralelos para o armazenamento HPC no Azure](https://blogs.msdn.microsoft.com/azurecat/2017/03/17/parallel-file-systems-for-hpc-storage-on-azure/)
* [Intel Cloud Edition for Software Lustre - Eval](https://azure.microsoft.com/marketplace/partners/intel/lustre-cloud-edition-evaleval-lustre-2-7/)
* [BeeGFS no modelo do CentOS 7.2](https://github.com/smith1511/hpc/tree/master/beegfs-shared-on-centos7.2)




## <a name="microsoft-mpi"></a>Microsoft MPI
[Microsoft MPI](https://msdn.microsoft.com/library/bb524831.aspx) (MS-MPI) é uma implementação da Microsoft da Message Passing Interface padrão para desenvolver e executar aplicativos paralelos na plataforma do Windows hello de saudação.

* [Baixe o MS-MPI](http://go.microsoft.com/FWLink/p/?LinkID=389556)
* [Referência do MS-MPI](https://msdn.microsoft.com/library/dn473458.aspx)
* [Fórum do MPI](https://social.microsoft.com/Forums/en-us/home?forum=windowshpcmpi)

## <a name="compute-intensive-instances"></a>Instâncias com uso computacional intensivo
Azure oferece uma [tamanhos de intervalo de VM](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), incluindo [H-série de computação intensa](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) instâncias capazes de se conectar rede RDMA tooa back-end, toorun suas cargas de trabalho do Linux e do Windows HPC. 

* [Configurar um aplicativo de MPI toorun Linux RDMA cluster](../virtual-machines/linux/classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Configurar um cluster do Windows RDMA com aplicativos de MPI toorun Microsoft HPC Pack](../virtual-machines/windows/classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

Para cargas de trabalho com uso intensivo de GPU, confira [Tamanhos de NC e NV](https://azure.microsoft.com/blog/azure-n-series-general-availability-on-december-1/).

## <a name="samples-and-demos"></a>Exemplos e scripts
* [Exemplos de código do C# e Python para o Lote do Azure](https://github.com/Azure/azure-batch-samples)
* [Lote Shipyard](https://azure.github.io/batch-shipyard/) Kit de ferramentas para facilitar a implantação de estilo de lote Dockerized cargas de trabalho tooAzure em lotes
* Pacote R [doAzureParallel](http://www.github.com/Azure/doAzureParallel), criado com base no Lote do Azure
* [Testar o SUSE Linux Enterprise Server para HPC](https://azure.microsoft.com/marketplace/partners/suse/suselinuxenterpriseserver12optimizedforhighperformancecompute/)

## <a name="related-azure-services"></a>Serviços do Azure relacionados
* [Fábrica de dados](https://azure.microsoft.com/documentation/services/data-factory/)
* 
            [Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/)
* [HDInsight](https://azure.microsoft.com/documentation/services/hdinsight/)
* [Máquinas virtuais](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [Conjuntos de Escala de Máquina Virtual](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/)
* [Serviços de Nuvem](https://azure.microsoft.com/documentation/services/cloud-services/)
* [Serviço de Aplicativo](https://azure.microsoft.com/documentation/services/app-service/)
* [Serviços de Mídia](https://azure.microsoft.com/documentation/services/media-services/)
* [Funções](https://azure.microsoft.com/documentation/services/functions/)

## <a name="architecture-blueprints"></a>Plano gráfico da arquitetura
* [HPC e orquestração de dados usando o Lote do Azure, o Azure Data Factory](http://go.microsoft.com/fwlink/?linkid=717686) (PDF) e o [artigo](../data-factory/data-factory-data-processing-using-batch.md)

## <a name="industry-solutions"></a>Soluções do setor
* [Bancos e mercados de capitais](https://finance.azure.com/)
* [Simulações de engenharia](https://simulation.azure.com/) 

## <a name="customer-stories"></a>Relatos de clientes
* [ANEO](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=4168) 
* [d3View](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=22088)
* [Ludwig Institute of Cancer Research](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=5830)
* [Microsoft Research](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=15634)
* [Milliman](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=14967)
* [Mitsubishi UFJ Securities International](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=26266)
* [Schlumberger](http://azure.microsoft.com/blog/big-compute-for-large-engineering-simulations)
* [Towers Watson](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18222)
* [UberCloud](https://simulation.azure.com/casestudies/Team-182-ABB-UC-Final.pdf)

## <a name="next-steps"></a>Próximas etapas
* Para lançamentos mais recentes de Olá, consulte Olá [blog da equipe do Microsoft HPC e lote](http://blogs.technet.com/b/windowshpc/) e hello [blog Azure](https://azure.microsoft.com/blog/tag/hpc/).
* Consulte também [o que há de novo no lote](https://azure.microsoft.com/updates/?service=batch) ou assinar toohello [RSS feed](https://azure.microsoft.com/updates/feed/?service=batch).

