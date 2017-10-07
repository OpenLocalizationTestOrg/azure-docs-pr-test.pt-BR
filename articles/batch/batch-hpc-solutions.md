---
title: "aaaBatch e soluções na nuvem Olá - Azure | Microsoft Docs"
description: "Saiba mais sobre opções de cenários e de soluções de computação em lote e de alto desempenho (HPC e Big Compute) no Azure"
services: batch, virtual-machines, cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
ms.assetid: aab5401d-2baf-4cf2-bf20-ad224de33888
ms.service: batch
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c5a3c8859d1f95040bcdad15942a815d71eb4486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="batch-and-hpc-solutions-for-large-scale-computing-workloads"></a>Soluções HPC e Lote para cargas de trabalho de computação em larga escala

O Azure oferece soluções em nuvem eficientes, escalonáveis para lote e HPC (computação de alto desempenho), também chamado de *Big Compute*. Saiba mais aqui sobre cargas de trabalho de computação intensa e toosupport de serviços do Azure-los ou ir diretamente muito[cenários de solução](#scenarios) posteriormente neste artigo. Este artigo é principalmente para fornecedores independentes de software, os gerentes de TI e responsáveis por decisões técnicas, mas outros desenvolvedores e profissionais de TI podem usar it toofamiliarize-se com essas soluções.

As organizações têm problemas de computação em larga escala: design de engenharia e análise, renderização de imagem, modelagem complexa, simulações de Monte Carlo, cálculos de riscos financeiros, entre outros. Azure ajuda as organizações a resolver esses problemas com recursos hello, escala e agenda necessários. Com o Azure, as organizações podem:

* Criar soluções híbridas, estendendo uma nuvem de toohello local HPC cluster toooffload pico cargas de trabalho
* Executar cargas de trabalho e ferramentas de cluster HPC totalmente no Azure
* Usar os serviços do Azure gerenciados e escalonáveis, como [lote](https://azure.microsoft.com/documentation/services/batch/) toorun cargas de trabalho de computação intensa sem ter que toodeploy e gerenciar infraestrutura de computação

Embora além do escopo Olá deste artigo, Azure também fornece aos desenvolvedores e parceiros um conjunto completo de recursos, opções de arquitetura e desenvolvimento ferramentas toobuild em larga escala, personalizados de computação intensa fluxos de trabalho. E um ecossistema de parceiros crescente toohelp pronto, você faz suas cargas de trabalho de computação intensa produtivo Olá nuvem do Azure.

## <a name="batch-and-hpc-applications"></a>Aplicativos de lote e HPC
Diferentemente dos aplicativos web e muitos aplicativos de linha de negócios, aplicativos Lote e HPC têm um início e fim definido e podem ser executados de acordo com um planejamento ou sob demanda, às vezes, por horas ou mais tempo. A maioria se enquadram em duas categorias principais: *intrinsecamente paralelos* (chamados de "embaraçosamente paralelo", porque eles solucionar de problemas de saudação se prestam toorunning em paralelo em vários computadores ou processadores) e *firmemente acopladas*. Consulte a tabela a seguir para obter mais informações sobre esses tipos de aplicativos de saudação. Algumas soluções do Azure se aproximar funcionam melhor para um tipo ou Olá outros.

> [!NOTE]
> Em soluções do Lote e HPC, uma instância em execução de um aplicativo normalmente é chamada de *trabalho* e cada trabalho pode ser dividido em *tarefas*. E hello recursos de computação em cluster para o aplicativo hello são chamados de *nós de computação*.
> 
> 

| Tipo | Características | Exemplos |
| --- | --- | --- |
| **Intrinsecamente paralelo**<br/><br/>![Intrinsecamente paralelo][parallel] |• Computadores individuais executam lógica de aplicativo independentemente<br/><br/> Computadores adicionando • permite que o tempo de computação Olá aplicativo tooscale e diminuir<br/><br/>• O aplicativo é formado por executáveis separados ou é dividido em um grupo de serviços chamados por um cliente (um aplicativo de arquitetura orientada a serviços, ou SOA) |• Modelagem de riscos financeiros<br/><br/>• Renderização e processamento de imagens<br/><br/>• Codificação e transcodificação de mídia<br/><br/>• Simulações de Monte Carlo<br/><br/>• Testes de software |
| **Tightly coupled**<br/><br/>![Tightly coupled][coupled] |• O aplicativo requer computação nós toointeract ou exchange resultados intermediários<br/><br/>• Computação nós podem se comunicar usando Olá Interface MPI (Message Passing), um protocolo de comunicação comum para a computação paralela<br/><br/>• hello está largura de banda e latência toonetwork confidenciais<br/><br/>• O desempenho do aplicativo pode ser melhorado com o uso de tecnologias de rede de alta velocidade, como InfiniBand e RDMA (acesso remoto direto à memória) |• Modelagem do reservatório de petróleo e gás<br/><br/>• Design de engenharia e análise, como dinâmica de fluidos computacional<br/><br/>• Simulações físicas como colisões de carro e reações nucleares<br/><br/>• Previsão do tempo |

### <a name="considerations-for-running-batch-and-hpc-applications-in-hello-cloud"></a>Considerações sobre a execução de lote e os aplicativos de HPC na nuvem Olá
Você pode migrar facilmente muitos aplicativos que são projetado toorun no ambiente de híbrida (entre locais) tooa ou tooAzure de clusters do HPC no local. No entanto, pode haver algumas restrições ou considerações, incluindo:

* **Disponibilidade de recursos de nuvem** -dependendo do tipo de saudação de recursos de computação de nuvem, você usar, talvez não seja capaz de toorely disponibilidade contínua do computador enquanto um trabalho é executado. Progresso e tratamento de estado Verifique apontando é comuns técnicas toohandle possíveis falhas transitórias e mais necessário ao usar recursos de nuvem.
* **Acesso a dados** -técnicas de acesso a dados geralmente disponíveis em clusters de empresa, como NFS, podem exigir configuração especial na nuvem hello. Ou, talvez seja necessário padrões e práticas recomendadas de acesso de dados diferentes de tooadopt para nuvem hello.
* **Movimentação de dados** - para aplicativos de processo grandes quantidades de dados, estratégias são necessários toomove Olá dados em armazenamento e toocompute recursos de nuvem. Talvez você precise de redes entre locais de alta velocidade, como [ExpressRoute do Azure](https://azure.microsoft.com/services/expressroute/). Também considere as limitações legais, regulatórias ou de políticas para armazenar e acessar esses dados.
* **Licenciamento** - entre em contato com o fornecedor de saudação de qualquer aplicativo comercial para licenciamento ou outras restrições de execução na nuvem de hello. Nem todos os fornecedores oferecem licenciamento pré-pago. Talvez você precise tooplan para um servidor de licenciamento na nuvem Olá para sua solução, ou conecte-se o servidor de licença local tooan.

### <a name="big-compute-or-big-data"></a>Big Compute ou Big Data?
Olá, dividindo a linha entre os aplicativos de computação intensa e Big Data nem sempre é criptografado e alguns aplicativos podem ter características de ambos. Os dois envolvem a execução de cálculos em larga escala, geralmente em clusters de computadores. Mas Olá solução abordagens e ferramentas de suporte podem ser diferentes.

• **Computação intensa** tende tooinvolve aplicativos que se baseiam na capacidade da CPU e memória, como simulações de engenharia, modelagem de riscos financeiros e renderização digital. infraestrutura de saudação para uma solução de computação intensa pode incluir computadores com processadores multicore especializados tooperform bruto computação, especializada, de alta velocidade rede hardware tooconnect hello.

• **Big Data** resolve problemas de análise de dados que envolvem grandes quantidades de dados que não podem ser gerenciados por um único computador ou sistema de gerenciamento de banco de dados. Os exemplos incluem grandes volumes de logs da Web ou outros dados de business intelligence. O Big Data tende toorely mais informações sobre a capacidade do disco e desempenho de e/s do que a capacidade da CPU. Também há ferramentas especializadas de dados grande, como Apache Hadoop toomanage Olá cluster e particionar dados saudação. (Para obter informações sobre o Azure HDInsight e outras soluções do Azure Hadoop, consulte [Hadoop](https://azure.microsoft.com/solutions/hadoop/).)

## <a name="compute-management-and-job-scheduling"></a>Gerenciamento de computação e agendamento de trabalho
Executando aplicativos de lote e HPC geralmente inclui um *Gerenciador de cluster* e um *Agendador de trabalhos* toohelp gerenciar recursos de computação em cluster e alocá-los toohello aplicativos que executam trabalhos hello. Essas funções podem ser feitas por ferramentas separadas ou por uma ferramenta ou serviço integrado.

* **Gerenciador de cluster** - Provisiona, libera e administra recursos de computação (ou nós de computação). Um Gerenciador de cluster pode automatizar a instalação de imagens do sistema operacional e aplicativos em nós de computação, dimensionar os recursos de computação, de acordo com o toodemands e monitorar o desempenho de saudação de nós de saudação.
* **Agendador de trabalhos** -Especifica os recursos de saudação (como processadores ou memória) um aplicativo precisa e hello condições quando ele é executado. Um agendador de trabalho mantém uma fila de trabalhos e aloca recursos toothem com base em uma prioridade atribuída ou outras características.

Clustering e ferramentas para clusters baseados em Linux e Windows de agendamento de trabalho podem migrar tooAzure bem. Por exemplo, o [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029), a solução de cluster de computação gratuita da Microsoft para cargas de trabalho de HPC do Windows e Linux, oferece diversas opções para execução no Azure. Você também pode criar clusters Linux toorun ferramentas de código-fonte aberto como Torque e SLURM. Você também pode abrir tooAzure de soluções comerciais de grade, tais como [TIBCO DataSynapse GridServer](https://azure.microsoft.com/blog/tibco-datasynapse-comes-to-the-azure-marketplace/), [IBM espectro Sinfonia e Sinfonia LSF](https://azure.microsoft.com/blog/ibm-and-microsoft-azure-support-spectrum-symphony-and-spectrum-lsf/), e [Univa grade mecanismo](http://www.univa.com/products/grid-engine).

Conforme mostrado na Olá seções a seguir, você pode tirar proveito dos serviços do Azure toomanage recursos de computação e agendar as ferramentas de gerenciamento de cluster tradicionais trabalhos sem (ou além).

## <a name="scenarios"></a>Cenários
Aqui estão três cenários comuns toorun cargas de trabalho de computação intensa no Azure usando soluções de cluster HPC existentes, os serviços do Azure ou uma combinação de saudação dois. As considerações importantes para a escolha de cada cenário estão listadas, mas não é uma lista completa. Mais sobre os serviços do Azure disponíveis Olá que você pode usar em sua solução é posteriormente Olá artigo.

| Cenário | Por que escolher isso? |
| --- | --- | --- |
| **Disparar um tooAzure de cluster HPC**<br/><br/>[![Cluster burst][burst_cluster]](./media/batch-hpc-solutions/burst_cluster.png) <br/><br/> Saiba mais:<br/>• [Disparar tooAzure instâncias de trabalho com o HPC Pack](https://technet.microsoft.com/library/gg481749.aspx)<br/><br/>• [Configurar um cluster de cálculo híbrido com o HPC Pack](../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)<br/><br/>• [Disparar tooAzure em lotes com o HPC Pack](https://technet.microsoft.com/library/mt612877.aspx)<br/><br/> |• Combinar o [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) ou outro cluster local com recursos adicionais do Azure em uma solução híbrida.<br/><br/>• Estender sua toorun de cargas de trabalho de computação intensa na plataforma como um instâncias de máquina virtual de serviço (PaaS) (atualmente somente Windows Server).<br/><br/>• Acesse um servidor de licenças local ou repositório de dados usando uma rede virtual do Azure opcional |
| **Criar um cluster de HPC inteiramente no Azure**<br/><br/>[![Cluster in IaaS][iaas_cluster]](./media/batch-hpc-solutions/iaas_cluster.png)<br/><br/>Saiba mais:<br/>• [Soluções de cluster HPC no Azure](big-compute-resources.md)<br/><br/> |• Implante de forma rápida e consistente seus aplicativos e ferramentas de cluster em máquinas virtuais de IaaS (Infraestrutura como serviço) do Windows ou Linux padrão ou personalizadas.<br/><br/>• Executar várias cargas de trabalho de computação intensa usando a solução de sua escolha de agendamento de trabalhos de saudação.<br/><br/>• Usar serviços adicionais do Azure, incluindo armazenamento e rede toocreate baseado em nuvem soluções completas. |
| **Dimensionar um aplicativo paralelo tooAzure**<br/><br/>[![Azure Batch][batch_proc]](./media/batch-hpc-solutions/batch_proc.png)<br/><br/>Saiba mais:<br/>• [Noções básicas de Lote do Azure](batch-technical-overview.md)<br/><br/>• [Introdução à biblioteca do lote do Azure de saudação para .NET](batch-dotnet-get-started.md) |• Desenvolver com [do Azure Batch](https://azure.microsoft.com/documentation/services/batch/) tooscale out várias toorun cargas de trabalho de computação intensa em pools de máquinas virtuais Windows ou Linux.<br/><br/>• Usar uma implantação de toomanage de serviço de plataforma Windows Azure e o dimensionamento automático de máquinas virtuais, agendamento de trabalho, recuperação de desastres, movimentação de dados, gerenciamento de dependência e implantação do aplicativo. |

## <a name="azure-services-for-big-compute"></a>Serviços do Azure para Big Compute
Eis aqui mais informações sobre computação hello, dados, rede e serviços relacionados que pode combinar para soluções de computação intensa e fluxos de trabalho. Para obter orientação detalhada sobre os serviços do Azure, consulte Olá serviços do Azure [documentação](https://azure.microsoft.com/documentation/). Olá [cenários](#scenarios) neste artigo Mostrar apenas algumas maneiras de usar esses serviços.

> [!NOTE]
> O Azure apresenta regularmente novos serviços que podem ser úteis para seu cenário. Se você tiver dúvidas, entre em contato com um [parceiro do Azure](https://pinpoint.microsoft.com/en-US/search?keyword=azure) ou envie um email para *bigcompute@microsoft.com*.
> 
> 

### <a name="compute-services"></a>Serviços de computação
Serviços de computação do Azure são core saudação de uma solução de computação intensa e Olá computação diferentes serviços oferecem vantagens para cenários diferentes. Em um nível básico, esses serviços oferecem modos diferentes para aplicativos toorun em instâncias de computação baseadas em máquina virtual que o Azure fornece usando a tecnologia Hyper-V do Windows Server. Essas instâncias podem executar sistemas operacionais e ferramentas padrão e personalizadas para Linux e Windows. O Azure fornece várias opções de [tamanhos de instância](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) com diferentes configurações de núcleos de CPU, de memória, de capacidade do disco e outras características. Dependendo de suas necessidades, você pode dimensionar Olá instâncias toothousands de núcleos e reduzir, em seguida, quando você precisa de menos recursos.

> [!NOTE]
> Aproveitar hello Azure [instâncias de computação intensiva como Olá H-series](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooimprove Olá desempenho e escalabilidade de cargas de trabalho do HPC. Essas instâncias também dão suporte a aplicativos MPI paralelos que exigem uma rede do aplicativo de baixa latência e alta taxa de transferência. Também estão disponíveis no [série N](../virtual-machines/windows/sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) VMs com GPUs NVIDIA tooexpand Olá inúmeros cenários de computação e de visualização no Azure.  
> 
> 

| O Barramento de | Descrição |
| --- | --- |
| **[Máquinas virtuais](https://azure.microsoft.com/documentation/services/virtual-machines/)**<br/><br/> |• Fornecem infraestrutura de computação como serviço (IaaS) usando a tecnologia Microsoft Hyper-V<br/><br/>• Permitem que você tooflexibly provisionar e gerenciar computadores de nuvem persistentes de imagens padrão do Windows Server ou Linux da saudação [Azure Marketplace](https://azure.microsoft.com/marketplace/), ou imagens e discos de dados fornecido<br/><br/>• Podem ser implantados e gerenciados como [conjuntos de escala de VM](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/) toobuild em larga escala serviços de máquinas virtuais idênticas, com capacidade de dimensionamento automático tooincrease ou reduzir automaticamente<br/><br/>• Executados no local aplicativos totalmente na nuvem hello e ferramentas de cluster de computação<br/><br/> |
| **[Serviços de nuvem](https://azure.microsoft.com/documentation/services/cloud-services/)**<br/><br/> |• Pode executar aplicativos de Big Compute em instâncias de função de trabalho, que são máquinas virtuais que executam uma versão do Windows Server e são totalmente gerenciadas pelo Azure<br/><br/>• Permite aplicativos escalonáveis e confiáveis com pouca sobrecarga administrativa, executando em um modelo PaaS (plataforma como serviço)<br/><br/>• Podem exigir ferramentas adicionais ou toointegrate de desenvolvimento com soluções de cluster HPC no local |
| **[Lote](https://azure.microsoft.com/documentation/services/batch/)**<br/><br/> |• Executa cargas de trabalho de larga escala paralelas e em lote em um serviço completamente gerenciado<br/><br/>• Fornece o plano de trabalho e o dimensionamento automático de um pool de máquinas virtuais gerenciado<br/><br/>• Permite que os desenvolvedores toobuild e executar aplicativos como um serviço ou aplicativos existentes habilitados para nuvem<br/> |

### <a name="storage-services"></a>Serviços de armazenamento
Uma solução de Big Compute geralmente opera em um conjunto de dados de entrada e gera dados para seus resultados. Alguns dos serviços de armazenamento do Azure Olá usados em soluções de computação intensa incluem:

* [Blob, tabela e armazenamento de fila](https://azure.microsoft.com/documentation/services/storage/) - gerencie grandes quantidades de dados não estruturados, dados NoSQL e mensagens para fluxo de trabalho e comunicação, respectivamente. Por exemplo, você pode usar o armazenamento de blob para grandes conjuntos de dados técnicos ou imagens de entrada hello ou arquivos de mídia seus processos de aplicativo. Você pode usar filas para comunicação assíncrona em uma solução. Consulte [tooMicrosoft Introdução armazenamento do Azure](../storage/common/storage-introduction.md).
* [Armazenamento de arquivo do Azure](https://azure.microsoft.com/services/storage/files/) -Olá a arquivos comuns de compartilhamentos e os dados no Azure usando protocolo SMB padrão, o que é necessário para algumas soluções de cluster HPC.
* [Repositório data Lake](https://azure.microsoft.com/services/data-lake-store/) -fornece uma sistema de arquivos distribuído do Apache Hadoop hiperescala para nuvem hello, útil para o lote, em tempo real e análises interativas.

### <a name="data-and-analysis-services"></a>Serviços de dados e análise
Alguns cenários de Big Compute envolvem fluxos de dados em grande escala ou geram dados que precisam de mais análise ou processamento. O Azure oferece vários serviços de dados e de análise, incluindo:

* [Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) - cria fluxos de trabalho orientados a dados (pipelines) que unem, agregam e transformam dados de repositórios de dados locais, em nuvem e na Internet.
* [Banco de dados SQL](https://azure.microsoft.com/documentation/services/sql-database/) -fornece os principais recursos de saudação de um sistema de gerenciamento de banco de dados relacional do Microsoft SQL Server em um serviço gerenciado.
* [HDInsight](https://azure.microsoft.com/documentation/services/hdinsight/) - implanta e provisiona clusters do Windows Server ou com base em Linux Apache Hadoop no hello nuvem toomanage, analisar e relatar grandes dados.
* 
            [Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) - ajuda a criar, testar, operar e gerenciar soluções analíticas de previsão em um serviço totalmente gerenciado.

### <a name="additional-services"></a>Serviços adicionais
Sua solução de computação intensa, talvez seja necessário outros serviços do Azure tooconnect tooresources no local ou em outros ambientes. Os exemplos incluem:

* [Rede virtual](https://azure.microsoft.com/documentation/services/virtual-network/) -cria uma seção logicamente isolada no Azure de recursos do Azure tooconnect tooeach outros ou tooyour local data center. Com uma rede virtual entre locais, os aplicativos de Big Compute podem acessar dados locais, serviços do Active Directory e servidores de licença
* [ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/) - cria conexões privadas entre os datacenters da Microsoft e a infraestrutura no local ou em um ambiente de colocalização. Rota expressa fornece maior segurança, mais confiabilidade, velocidades mais rápidas e latências menores que as conexões típicas pela Internet da saudação.
* [Barramento de serviço](https://azure.microsoft.com/documentation/services/service-bus/) -fornece vários mecanismos para aplicativos de dados do exchange ou toocommunicate, se eles estão localizados no Azure, em outra plataforma de nuvem ou em um data center.

## <a name="next-steps"></a>Próximas etapas
* Consulte [recursos técnicos para o lote e HPC](big-compute-resources.md) toofind orientação técnica toobuild sua solução.
* Discuta as opções do Azure com parceiros, incluindo Cycle Computing, Rescale e UberCloud.
* Leia sobre as soluções de Big Compute do Azure fornecidas por [Towers Watson](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18222), [Altair](https://azure.microsoft.com/blog/availability-of-altair-radioss-rdma-on-microsoft-azure/), [ANSYS](https://azure.microsoft.com/blog/ansys-cfd-and-microsoft-azure-perform-the-best-hpc-scalability-in-the-cloud/) e [d3VIEW](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=22088).
* Para lançamentos mais recentes de Olá, consulte Olá [blog da equipe do Microsoft HPC e lote](http://blogs.technet.com/b/windowshpc/) e hello [blog Azure](https://azure.microsoft.com/blog/tag/hpc/).

<!--Image references-->
[parallel]: ./media/batch-hpc-solutions/parallel.png
[coupled]: ./media/batch-hpc-solutions/coupled.png
[iaas_cluster]: ./media/batch-hpc-solutions/iaas_cluster.png
[burst_cluster]: ./media/batch-hpc-solutions/burst_cluster.png
[batch_proc]: ./media/batch-hpc-solutions/batch_proc.png
