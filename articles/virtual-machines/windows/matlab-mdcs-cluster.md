---
title: "aaaMATLAB clusters em máquinas virtuais | Microsoft Docs"
description: "Usar toocreate de máquinas virtuais do Microsoft Azure toorun de clusters de servidor de computação distribuída MATLAB suas cargas de trabalho MATLAB paralelas com computação intensiva"
services: virtual-machines-windows
documentationcenter: 
author: mscurrell
manager: timlt
editor: 
ms.assetid: e9980ce9-124a-41f1-b9ec-f444c8ea5c72
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Windows
ms.workload: infrastructure-services
ms.date: 05/09/2016
ms.author: markscu
ms.openlocfilehash: 266749dbdcfefac42c94b74aa612bfee18075a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-matlab-distributed-computing-server-clusters-on-azure-vms"></a>Criar clusters de Servidor de Computação Distribuída MATLAB em VMs do Azure
Use Microsoft Azure virtual máquinas toocreate um ou mais MATLAB servidor de computação distribuída clusters toorun suas cargas de trabalho MATLAB paralelas com computação intensiva. Instalar o software de servidor de computação distribuída MATLAB em toouse uma VM como uma imagem de base e usar um modelo de início rápido do Azure ou um script do PowerShell do Azure (disponível em [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/matlab-cluster)) toodeploy e gerenciar o cluster hello. Após a implantação, conecte-se toohello cluster toorun suas cargas de trabalho.

## <a name="about-matlab-and-matlab-distributed-computing-server"></a>Sobre a MATLAB e o Servidor de Computação Distribuída MATLAB
Olá [MATLAB](http://www.mathworks.com/products/matlab/) plataforma é otimizada para solução de problemas científicos e de engenharia. Usuários do MATLAB com simulações em grande escala e tarefas de processamento de dados podem usar paralelo MathWorks computação toospeed produtos suas cargas de trabalho de computação intensa, aproveitando os clusters de computadores e serviços de grade. [Caixa de Ferramentas de Computação Paralela](http://www.mathworks.com/products/parallel-computing/) permite que os usuários da MATLAB paralelizem aplicativos e aproveitem os processadores de vários núcleos, GPUs e clusters de cálculo. [Servidor de computação distribuída MATLAB](http://www.mathworks.com/products/distriben/) permite MATLAB usuários tooutilize vários computadores em um cluster de computação.

Usando máquinas virtuais do Azure, você pode criar clusters de servidor de computação distribuída MATLAB com todos os Olá mesmo mecanismos disponíveis toosubmit paralelas de trabalho em clusters locais, como trabalhos interativos, trabalhos de lote, tarefas independentes, e tarefas de comunicação. Usando o Azure em conjunto com a plataforma do MATLAB Olá tem tooprovisioning de muitas vantagens em comparação usando tradicionais locais e hardware: tamanhos de um intervalo de máquina virtual, criação de clusters sob demanda para que você paga somente pelos recursos de computação Olá usar, e modelos de tootest de capacidade de saudação em escala.  

## <a name="prerequisites"></a>Pré-requisitos
* **Computador cliente** -você precisará de um toocommunicate do computador cliente com Windows com o Azure e Olá cluster de servidor de computação distribuída MATLAB após a implantação.
* **O Azure PowerShell** -consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) tooinstall-lo no computador cliente.
* **Assinatura do Azure** : se você não tiver uma assinatura, poderá criar uma [conta gratuita](https://azure.microsoft.com/free/) em apenas alguns minutos. Para clusters maiores, considere uma assinatura pré-paga ou outras opções de compra.
* **Cota de núcleos** -tooincrease Olá core cota toodeploy talvez seja necessário um cluster grande ou mais de um cluster de servidor de computação distribuída MATLAB. uma cota de tooincrease [abrir uma solicitação de suporte do cliente online](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) sem custo adicional.
* **Licenças MATLAB, computação paralela de ferramentas e servidor de computação distribuída MATLAB** -scripts de saudação presumem que Olá [MathWorks Gerenciador de licenças hospedado](http://www.mathworks.com/products/parallel-computing/mathworks-hosted-license-manager/) é usado para todas as licenças.  
* **Software de servidor de computação distribuída MATLAB** -serão instalados em uma máquina virtual que será usada como imagem VM base Olá para máquinas virtuais do cluster hello.

## <a name="high-level-steps"></a>Etapas de alto nível
toouse máquinas virtuais do Azure para os clusters de servidor de computação distribuída MATLAB, hello seguintes etapas de alto nível são necessárias. As instruções detalhadas estão na documentação de saudação que acompanha o modelo de início rápido do hello e scripts em [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/matlab-cluster).

1. **Criar uma imagem de VM de base**  

   * Baixe e instale o software de Servidor de Computação Distribuída MATLAB nessa VM.

     > [!NOTE]
     > Esse processo pode levar algumas horas, mas tiver apenas toodo-lo depois de cada versão do MATLAB em que você usar.   
     >
     >
2. **Criar um ou mais clusters**  

   * Use script do PowerShell Olá fornecido ou Olá quickstart modelo toocreate um cluster de imagem VM de base de saudação.   
   * Gerencie clusters hello usando script do PowerShell Olá fornecido que permite que você toolist, pausar, retomar e clusters de exclusão.

## <a name="cluster-configurations"></a>Configurações de cluster
Atualmente, modelo e script de criação de cluster Olá permitem toocreate uma topologia de servidor de computação distribuída MATLAB único. Se desejar, crie um ou mais clusters adicionais, com cada cluster com um número diferente de VMs de trabalho, usando diferentes tamanhos de VM e assim por diante.

### <a name="matlab-client-and-cluster-in-azure"></a>Cluster e cliente MATLAB no Azure
nó do cliente MATLAB Hello, nó do Agendador de trabalhos do MATLAB e servidor distribuída MATLAB computação "trabalho" nós são todos configurados como VMs do Azure em uma rede virtual, conforme mostrado na seguinte Olá figura.


* Olá toouse de cluster, conecte-se ao nó do cliente toohello da área de trabalho remota. nó de saudação do cliente executa o cliente do MATLAB Olá.
* nó de saudação do cliente tem um compartilhamento de arquivos que pode ser acessado por todos os funcionários.
* MathWorks hospedado Gerenciador de licenças é usado para verificações de licença Olá para todos os softwares do MATLAB.
* Por padrão, um trabalho de servidor de computação distribuída MATLAB por núcleo é criado no trabalho Olá VMs, mas você pode especificar qualquer número.

## <a name="use-an-azure-based-cluster"></a>Usar um Cluster baseado no Azure
Assim como acontece com outros tipos de clusters de servidor de computação distribuída MATLAB, você precisa toouse Olá Gerenciador de Cluster de perfil no hello MATLAB cliente (no cliente de saudação VM) toocreate um perfil de cluster do Agendador de trabalhos do MATLAB.

![Gerenciador de perfis de cluster](./media/matlab-mdcs-cluster/cluster_profile_manager.png)

## <a name="next-steps"></a>Próximas etapas
* Para obter instruções detalhadas toodeploy e gerenciar clusters de servidor de computação distribuída MATLAB no Azure, consulte Olá [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/matlab-cluster) repositório que contém modelos de saudação e scripts.
* Vá toohello [MathWorks site](http://www.mathworks.com/) para documentação detalhada de MATLAB e servidor de computação distribuída MATLAB.
