---
title: "aaaCreate um nó principal do HPC Pack em uma VM do Azure | Microsoft Docs"
description: "Saiba como toouse Olá implantação do Azure do Gerenciador de recursos de portal e hello modelo toocreate um nó principal do Microsoft HPC Pack 2012 R2 em uma VM do Azure."
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,hpc-pack
ms.assetid: e6a13eaf-9124-47b4-8d75-2bc4672b8f21
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 3ddefb74b053a48a15f1ba1ca8edbc0192da51a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hello-head-node-of-an-hpc-pack-cluster-in-an-azure-vm-with-a-marketplace-image"></a>Criar o nó de cabeçalho de saudação de um cluster de HPC Pack em uma VM do Azure com uma imagem do Marketplace
Use um [imagem de máquina virtual do Microsoft HPC Pack 2012 R2](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) de saudação do Azure Marketplace e hello toocreate portal do Azure Olá nó principal de um cluster HPC. Esta imagem da VM do Pacote HPC baseia-se no Windows Server 2012 R2 Datacenter com Pacote HPC 2012 R2 Atualização 3 pré-instalado. Use esse nó principal para uma implantação de prova de conceito do Pacote HPC no Azure. Em seguida, você pode adicionar computação nós toohello cluster toorun HPC cargas de trabalho.

> [!TIP]
> toodeploy um cluster de HPC Pack 2012 R2 completo no Azure que inclui o nó principal hello e nós de computação, recomendamos que você use um método automatizado. As opções incluem hello [script de implantação IaaS do HPC Pack](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) e modelos do Gerenciador de recursos, como Olá [cluster HPC Pack para cargas de trabalho do Windows](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/). Os modelos do Resource Manager também estão disponíveis para [clusters Microsoft HPC Pack 2016](https://github.com/MsHpcPack/HPCPack2016/tree/master/newcluster-templates). 
> 
> 

## <a name="planning-considerations"></a>Considerações sobre planejamento
Conforme mostrado na figura a seguir de saudação, você implantar o nó principal do HPC Pack Olá em um domínio do Active Directory em uma rede virtual do Azure.

![Nó principal do Pacote HPC][headnode]

* **Domínio do Active Directory**: hello HPC Pack 2012 R2 nó principal deve ser unida tooan domínio do Active Directory do Azure antes de iniciar os serviços HPC Olá no hello VM. Conforme mostrado neste artigo, para uma implantação de verificação de conceito, você pode promover Olá VM que você criou para o nó principal hello como um controlador de domínio antes de iniciar os serviços do HPC hello. Outra opção é toodeploy um controlador de domínio separadas e floresta no Azure toowhich ingressar Olá VM do nó principal.

* **Modelo de implantação**: na maioria das implantações de novo, a Microsoft recomenda que você use o modelo de implantação do Gerenciador de recursos de saudação. Este artigo pressupõe que você use esse modelo de implantação.

* **Rede virtual do Azure**: quando você usa Olá Gerenciador de recursos implantação modelo toodeploy Olá nó principal, você especificar ou criar uma rede virtual do Azure. Você usar a rede virtual Olá se você precisar toojoin Olá nó principal tooan domínio existente do Active Directory. Também precisar do nó de computação posterior tooadd VMs toohello cluster.

## <a name="steps-toocreate-hello-head-node"></a>Nó de cabeçalho etapas toocreate Olá
A seguir é etapas de alto nível toouse Olá toocreate portal do Azure uma VM do Azure para o nó principal do HPC Pack hello usando o modelo de implantação do Gerenciador de recursos de saudação. 

1. Se você quiser toocreate uma nova floresta do Active Directory no Azure com máquinas virtuais do controlador de domínio separadas, uma opção é toouse uma [modelo do Gerenciador de recursos](https://github.com/Azure/azure-quickstart-templates/tree/master/active-directory-new-domain-ha-2-dc). Para obter uma verificação simple da implantação do conceito, ele tem problema tooomit esta etapa e configurar o nó principal do hello própria máquina virtual como um controlador de domínio. Essa opções será descrita posteriormente neste artigo.
2. Em Olá [HPC Pack 2012 R2 na página do Windows Server 2012 R2](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) no hello Azure Marketplace, clique em **criar Máquina Virtual**. 
3. No portal Olá Olá **HPC Pack 2012 R2 no Windows Server 2012 R2** página, selecione Olá **Gerenciador de recursos de** modelo de implantação e clique **criar**.
   
    ![Imagem do Pacote HPC][marketplace]
4. Usar as configurações de portal tooconfigure Olá Olá e criar hello VM. Se você for novo tooAzure, siga o tutorial Olá [criar uma máquina virtual do Windows no portal do Azure de saudação](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Para uma implantação de verificação de conceito, você geralmente pode aceitar o padrão de saudação ou as configurações recomendadas.
   
   > [!NOTE]
   > Se você quiser toojoin Olá nó principal tooan existentes de domínio do Active Directory no Azure, certifique-se de que especificar a rede virtual Olá para esse domínio ao criar hello VM.
   > 
   > 
5. Depois de criar hello VM e hello VM estiver em execução, [conectar toohello VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) por área de trabalho remota. 
6. Associe a floresta de domínio do Active Directory do hello VM tooan escolhendo uma saudação as opções a seguir:
   
   * Se você criou Olá VM em uma rede virtual do Azure com uma floresta de domínio existente, una floresta de toohello VM hello usando ferramentas padrão do Gerenciador do servidor ou o Windows PowerShell. Em seguida, reinicie.
   * Se você criou Olá VM em uma nova rede virtual (sem uma floresta de domínio existente), em seguida, promova Olá VM como um controlador de domínio. Use as etapas padrão tooinstall e configurar a função de serviços de domínio do Active Directory de saudação no nó de cabeçalho de saudação. Para obter etapas detalhadas, consulte [Instalar uma nova floresta do Active Directory no Windows Server 2012](https://technet.microsoft.com/library/jj574166.aspx).
7. Após Olá VM está em execução e unida tooan floresta do Active Directory, inicie serviços do HPC Pack Olá da seguinte maneira:
   
    a. Conecte-se usando uma conta de domínio que seja membro do grupo de administradores local Olá VM com nó principal toohello. Por exemplo, use a conta de administrador Olá configurada quando você criou a VM do nó principal hello.
   
    b. Para uma configuração de nó principal do padrão, inicie o Windows PowerShell como administrador e digite Olá a seguir:
   
    ```PowerShell
    & $env:CCP_HOME\bin\HPCHNPrepare.ps1 –DBServerInstance ".\ComputeCluster"
    ```
   
    Pode levar vários minutos para toostart de serviços do HPC Pack hello.
   
    Para opções de configuração adicionais de nó principal, digite `get-help HPCHNPrepare.ps1`.

## <a name="next-steps"></a>Próximas etapas
* Agora você pode trabalhar com o nó principal de saudação do seu cluster de HPC Pack. Por exemplo, inicie o Gerenciador de Cluster de HPC e Olá completa [lista de tarefas de implantação](https://technet.microsoft.com/library/jj884141.aspx).
* Se você quiser tooincrease Olá cluster de computação capacidade sob demanda, adicione [nós de disparo do Azure](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) em um serviço de nuvem. 
* Tente executar uma carga de trabalho de teste no cluster hello. Para obter um exemplo, consulte Olá HPC Pack [guia de Introdução](https://technet.microsoft.com/library/jj884144).

<!--Image references-->
[headnode]: ./media/hpcpack-cluster-headnode/headnode.png
[marketplace]: ./media/hpcpack-cluster-headnode/marketplace.png
