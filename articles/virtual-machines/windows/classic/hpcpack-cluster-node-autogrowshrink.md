---
title: "nós de cluster de HPC Pack aaaAutoscale | Microsoft Docs"
description: "Automaticamente aumentar ou reduzir o número de saudação de nós de computação de cluster de HPC Pack no Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: 
editor: tysonn
ms.assetid: 38762cd1-f917-464c-ae5d-b02b1eb21e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/08/2016
ms.author: danlep
ms.openlocfilehash: 0bdf55625d337a2bbfe05677682d645a584798d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-grow-and-shrink-hello-hpc-pack-cluster-resources-in-azure-according-toohello-cluster-workload"></a>Aumentar e reduzir os recursos de cluster de HPC Pack Olá no Azure de acordo com a carga de trabalho de cluster toohello automaticamente
Se você implantar nós de "Disparo" do Azure em seu cluster de HPC Pack ou criar um cluster de HPC Pack em VMs do Azure, talvez seja uma maneira de aumentar ou reduzir os recursos de cluster hello como nós ou núcleos de acordo com a carga de trabalho Olá no cluster Olá automaticamente. Dimensionamento dos recursos de cluster Olá dessa maneira permite que você toouse os recursos do Azure com mais eficiência e controlar os custos.

Este artigo mostra duas maneiras de HPC Pack fornece recursos de computação tooautoscale:

* saudação de propriedade de cluster de HPC Pack **AutoGrowShrink**

* Olá **AzureAutoGrowShrink.ps1** script do HPC PowerShell

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

No momento somente é possível aumentar ou reduzir automaticamente nós de computação HPC Pack que estão em execução em um sistema operacional Windows Server.


## <a name="set-hello-autogrowshrink-cluster-property"></a>Definir a propriedade de cluster AutoGrowShrink Olá
### <a name="prerequisites"></a>Pré-requisitos

* **HPC Pack 2012 R2 atualização 2 ou posterior cluster** -nó principal do cluster Olá pode ser implantado no local ou em uma VM do Azure. Consulte [configurar um cluster híbrido com o HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget iniciado conosco de "Disparo" do Azure e um nó principal local. Consulte Olá [script de implantação IaaS do HPC Pack](hpcpack-cluster-powershell-script.md) tooquickly implantar um cluster de HPC Pack em VMs do Azure.

* **Para um cluster com um nó de cabeçalho no Azure (modelo de implantação do Resource Manager)** – No HPC Pack 2016, a autenticação de certificado em um aplicativo do Azure Active Directory é usada para expandir e reduzir automaticamente as VMs de cluster implantado usando o Azure Resource Manager. Configure um certificado da seguinte maneira:

  1. Após a implantação de cluster, conecte-se ao nó principal do tooone de área de trabalho remota.

  2. Carregar o nó principal do tooeach Olá certificado (formato PFX com chave privada) e instale tooCert:\LocalMachine\My e Cert: \LocalMachine\Root.

  3. Inicie o PowerShell do Azure como administrador e execute Olá comandos a seguir em um nó principal:

    ```powershell
        cd $env:CCP_HOME\bin

        Login-AzureRmAccount
    ```
        
    Se sua conta estiver em mais de um locatário do Active Directory do Azure ou assinatura do Azure, você pode executar o seguinte Olá comando locatário correto do tooselect hello e assinatura:
  
    ```powershell
        Login-AzureRMAccount -TenantId <TenantId> -SubscriptionId <subscriptionId>
    ```     
       
    Executar Olá tooview de comando a seguir Olá selecionada locatário e assinatura:
    
    ```powershell
        Get-AzureRMContext
    ```

  4. Executar Olá script a seguir

    ```powershell
        .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -CertificateThumbprint "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX" -TenantId xxxxxxxx-xxxxx-xxxxx-xxxxx-xxxxxxxxxxxx
    ```

    onde

    **DisplayName** – nome de exibição do aplicativo ativo do Azure. Se o aplicativo hello não existir, ele é criado no Active Directory do Azure.

    **Home page** -Olá home page do aplicativo hello. Você pode configurar uma URL fictícia, como saudação anterior de exemplo.

    **IdentifierUri** -identificador de aplicativo hello. Você pode configurar uma URL fictícia, como saudação anterior de exemplo.

    **CertificateThumbprint** -impressão digital do certificado Olá instalado no nó de cabeçalho Olá na etapa 1.

    **TenantId** – ID de locatário do Azure Active Directory. Você pode obter Olá ID de locatário no portal do Azure Active Directory Olá **propriedades** página.

    Para obter mais detalhes sobre **ConfigARMAutoGrowShrinkCert.ps1**, execute `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.


* **Para um cluster com um nó principal no Azure (modelo de implantação clássico)** - se você usar o cluster de Olá Olá HPC Pack IaaS implantação script toocreate no modelo de implantação clássico hello, habilitar Olá **AutoGrowShrink** cluster propriedade definindo a opção de AutoGrowShrink Olá no arquivo de configuração de cluster de saudação. Para obter detalhes, consulte a documentação de saudação que acompanha Olá [download do script](https://www.microsoft.com/download/details.aspx?id=44949).

    Como alternativa, habilitar Olá **AutoGrowShrink** comandos de propriedade de cluster depois de implantar o cluster hello usando o PowerShell HPC descrito em Olá seção a seguir. tooprepare para isso, primeiro Olá completo seguindo as etapas:

  1. Configure um certificado de gerenciamento do Azure no nó de cabeçalho hello e no hello assinatura do Azure. Para uma implantação de teste, você pode usar saudação padrão do Microsoft HPC Azure certificado autoassinado que instala o HPC Pack no nó principal hello e carregue tooyour esse certificado assinatura do Azure. Para opções e etapas, consulte Olá [orientação de biblioteca do TechNet](https://technet.microsoft.com/library/gg481759.aspx).

  2. Executar **regedit** no nó principal do hello, vá tooHKLM\SOFTWARE\Micorsoft\HPC\IaasInfo e adicione um valor de cadeia de caracteres. Defina o nome do valor Olá muito "Impressão digital" e a impressão digital toohello de dados do valor do certificado Olá na etapa 1.

### <a name="hpc-powershell-commands-tooset-hello-autogrowshrink-property"></a>Propriedade AutoGrowShrink do HPC PowerShell comandos tooset Olá
A seguir é tooset de comandos do exemplo do HPC PowerShell **AutoGrowShrink** e tootune seu comportamento com parâmetros adicionais. Consulte [AutoGrowShrink parâmetros](#AutoGrowShrink-parameters) posteriormente neste artigo para obter a lista completa Olá das configurações.

toorun esses comandos, inicie o PowerShell do HPC no nó principal do cluster Olá como um administrador.

**Olá tooenable propriedade AutoGrowShrink**

```powershell
Set-HpcClusterProperty –EnableGrowShrink 1
```

**Olá toodisable propriedade AutoGrowShrink**

```powershell
Set-HpcClusterProperty –EnableGrowShrink 0
```

**Olá toochange aumentar o intervalo em minutos**

```powershell
Set-HpcClusterProperty –GrowInterval <interval>
```

**Olá toochange reduzir o intervalo em minutos**

```powershell
Set-HpcClusterProperty –ShrinkInterval <interval>
```

**configuração atual do hello tooview de AutoGrowShrink**

```powershell
Get-HpcClusterProperty –AutoGrowShrink
```

**grupos de nó de tooexclude de AutoGrowShrink**

```powershell
Set-HpcClusterProperty –ExcludeNodeGroups <group1,group2,group3>
```

>[!NOTE] 
> Esse parâmetro tem suporte do HPC Pack 2016
>

### <a name="autogrowshrink-parameters"></a>parâmetros de AutoGrowShrink
Olá seguem AutoGrowShrink parâmetros que podem ser modificados usando Olá **HpcClusterProperty conjunto** comando.

* **EnableGrowShrink** - alternar tooenable ou desabilitar Olá **AutoGrowShrink** propriedade.
* **ParamSweepTasksPerCore** -número de limpeza paramétrica tarefas toogrow um núcleo. padrão de saudação é um núcleo toogrow por tarefa.

  > [!NOTE]
  > Alterações de HPC Pack QFE KB3134307 **ParamSweepTasksPerCore** muito**TasksPerResourceUnit**. Ele se baseia no tipo de recurso de trabalho hello e pode ser nó, soquete ou core.
  >
  >
* **GrowThreshold** -limite de crescimento automático de tootrigger de tarefas na fila. padrão de saudação é 1, o que significa que, se há 1 ou mais tarefas Olá estado na fila, aumentar automaticamente nós.
* **GrowInterval** -intervalo de aumento automático de tootrigger minutos. intervalo padrão de saudação é de 5 minutos.
* **ShrinkInterval** -intervalo em minutos tootrigger redução automática. intervalo padrão de saudação é de 5 minutos. |
* **ShrinkIdleTimes** -número de verificações contínua tooshrink tooindicate Olá nós está ocioso. padrão de saudação é 3 vezes. Por exemplo, se hello **ShrinkInterval** é de 5 minutos, HPC Pack verifica se o nó de saudação está ocioso a cada 5 minutos. Se nós Olá estiverem em estado ocioso Olá após 3 contínua verifica (15 minutos), o HPC Pack reduz nesse nó.
* **ExtraNodesGrowRatio** -porcentagem adicional de nós toogrow para trabalhos de Interface MPI (Message Passing). valor padrão de saudação é 1, o que significa que o HPC Pack cresce nós % 1 para trabalhos MPI.
* **GrowByMin** -alternar tooindicate se a política de aumento automático de saudação baseia-se no mínimo de recursos necessário para o trabalho de saudação do hello. padrão de saudação é false, o que significa que o HPC Pack cresce nós para trabalhos com base nos recursos de máximo de saudação necessários para trabalhos de saudação.
* **SoaJobGrowThreshold** -processo de aumento de limite de entrada SOA solicitações tootrigger Olá automática. valor padrão de saudação é 50000.

  > [!NOTE]
  > Esse parâmetro tem suporte a partir do HPC Pack 2012 R2 Atualização 3.
  >
  >
* **SoaRequestsPerCore** -número de entrada SOA solicitações toogrow um núcleo. valor padrão de saudação é 20.000.

  > [!NOTE]
  > Esse parâmetro tem suporte a partir do HPC Pack 2012 R2 Atualização 3.
  >
* **ExcludeNodeGroups** – nós Olá especificado grupos de nó automaticamente aumentar ou encolher.
  
  > [!NOTE]
  > Esse parâmetro tem suporte do HPC Pack 2016.
  >

### <a name="mpi-example"></a>Exemplo de MPI
Por padrão o HPC Pack cresce % 1 nós extras para trabalhos MPI (**ExtraNodesGrowRatio** está definida too1). motivo da saudação é que MPI pode exigir vários nós e trabalho Olá pode ser executada somente quando todos os nós estão prontos. Quando o Azure inicia nós, ocasionalmente, um nó talvez seja necessário mais toostart de tempo que outras pessoas, fazendo com que outros toobe nós ocioso enquanto aguarda que tooget nó pronto. Ao aumentar nós extras, o HPC Pack reduz o tempo de espera desse recurso e potencialmente reduz os custos. Porcentagem de saudação tooincrease de nós extras para trabalhos MPI (por exemplo, % too10), execute um comando semelhante a

    Set-HpcClusterProperty -ExtraNodesGrowRatio 10

### <a name="soa-example"></a>Exemplo de SOA
Por padrão, **SoaJobGrowThreshold** é definir too50000 e **SoaRequestsPerCore** está definida too200000. Se você enviar um trabalho SOA com 70000 solicitações, há uma tarefa na fila e as solicitações de entrada serão 70000. Nesse caso o HPC Pack cresce 1 núcleo para hello na fila de tarefas e solicitações de entrada, cresce (50000 70000) / 20000 = 1 núcleo, no total cresce 2 núcleos para este trabalho SOA.

## <a name="run-hello-azureautogrowshrinkps1-script"></a>Executar script de AzureAutoGrowShrink.ps1 Olá
### <a name="prerequisites"></a>Pré-requisitos

* **HPC Pack 2012 R2 Update 1 ou posterior cluster** - Olá **AzureAutoGrowShrink.ps1** script está instalado na pasta % CCP_HOME % bin hello. nó principal do cluster Olá pode ser implantado no local ou em uma VM do Azure. Consulte [configurar um cluster híbrido com o HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget iniciado conosco de "Disparo" do Azure e um nó principal local. Consulte Olá [script de implantação IaaS do HPC Pack](hpcpack-cluster-powershell-script.md) tooquickly implantar um cluster de HPC Pack em VMs do Azure ou use um [modelo de início rápido do Azure](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/).
* **O Azure PowerShell 1.4.0** -script hello depende atualmente essa versão específica do PowerShell do Azure.
* **Para um cluster com o Azure burst nós** -executar script hello em um computador cliente onde o HPC Pack está instalado, ou no nó de cabeçalho hello. Se em execução em um computador cliente, certifique-se de que você defina Olá variável $env: nó de cabeçalho CCP_SCHEDULER toopoint toohello. Hello Azure "disparar" nós devem ser adicionados toohello cluster, mas elas podem estar no estado não implantado de saudação.
* **Para um cluster implantado em VMs do Azure (modelo de implantação do Gerenciador de recursos)** -para um cluster de máquinas virtuais do Azure implantados no modelo de implantação do Gerenciador de recursos de saudação, o script hello dá suporte a dois métodos de autenticação do Azure: entrar tooyour conta do Azure script de saudação toorun sempre (executando `Login-AzureRmAccount`, ou configurar um tooauthenticate principal do serviço com um certificado. HPC Pack fornece o script hello **ConfigARMAutoGrowShrinkCert.ps** toocreate uma entidade de serviço com o certificado. script Hello cria um aplicativo do Azure Active Directory (AD do Azure) e uma entidade de serviço e atribui a entidade de serviço Olá Colaborador função toohello. script de saudação toorun, inicie o PowerShell do Azure como administrador e execute Olá comandos a seguir:

    ```powershell
    cd $env:CCP_HOME\bin

    Login-AzureRmAccount

    .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -PfxFile "d:\yourcertificate.pfx"
    ```

    Para obter mais detalhes sobre **ConfigARMAutoGrowShrinkCert.ps1**, execute `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`,

* **Para um cluster implantado em VMs do Azure (modelo de implantação clássico)** -executar script hello no nó de cabeçalho Olá VM, porque depende de saudação **Start-hpciaasnode.ps1** e **Stop-hpciaasnode.ps1**scripts que estão instalados lá. Além disso, esses scripts exigem um certificado de gerenciamento ou um arquivo de configurações de publicação do Azure (veja [Gerenciar nós de computação em um cluster HPC Pack no Azure](hpcpack-cluster-node-manage.md)). Certifique-se de saudação todas as VMs, você precisa do nó já foram adicionadas toohello cluster de computação. Elas podem estar no estado parado de saudação.



### <a name="syntax"></a>Sintaxe
```powershell
AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfActiveQueuedTasksPerNodeToGrow <Single> [-NumOfActiveQueuedTasksToGrowThreshold <Int32>]
    [-NumOfInitialNodesToGrow <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>]
    [-ShrinkCheckIdleTimes <Int32>] [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>]
    [<CommonParameters>]

AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfQueuedJobsPerNodeToGrow <Single> [-NumOfQueuedJobsToGrowThreshold <Int32>] [-NumOfInitialNodesToGrow
    <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>] [-ShrinkCheckIdleTimes <Int32>]
    [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]

AzureAutoGrowShrink.ps1 -UseLastConfigurations [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]
```
### <a name="parameters"></a>parâmetros
* **NodeTemplates** -nomes de toodefine de modelos de nó Olá Olá Olá nós toogrow escopo e reduzir. Se não for especificado (valor padrão de saudação é @()), todos os nós no hello **AzureNodes** grupo de nó estão no escopo quando **NodeType** tem um valor de AzureNodes e todos os nós na Olá **ComputeNodes** grupo de nó estão no escopo quando **NodeType** tem um valor de ComputeNodes.
* **Os JobTemplates** -nomes de saudação modelos toodefine Olá escopo Olá toogrow de nós de trabalho.
* **NodeType** - Olá tipo de nó toogrow e reduzir. Os valores para os quais há suporte são:

  * **AzureNodes** – para os nós (de disparo contínuo) de PaaS do Azure em cluster local ou de IaaS do Azure.
  * **ComputeNodes** - para VMs de nó de computação apenas em um cluster de IaaS do Azure.

* **NumOfQueuedJobsPerNodeToGrow** -número de trabalhos em fila necessário toogrow um nó.
* **NumOfQueuedJobsToGrowThreshold** -número de limite de saudação de saudação de toostart trabalhos em fila cresça processo.
* **NumOfActiveQueuedTasksPerNodeToGrow** -número de saudação de tarefas ativas em fila necessário toogrow um nó. Se **NumOfQueuedJobsPerNodeToGrow** for especificado com um valor maior que 0, esse parâmetro será ignorado.
* **NumOfActiveQueuedTasksToGrowThreshold** -número de limite de saudação de saudação do toostart tarefas ativas em fila cresça processo.
* **NumOfInitialNodesToGrow** - Olá inicial número mínimo de nós toogrow se todos os nós de saudação no escopo são **não implantado** ou **parado (desalocado)**.
* **GrowCheckIntervalMins** -intervalo de saudação em minutos entre verifica toogrow.
* **ShrinkCheckIntervalMins** -intervalo de saudação em minutos entre verifica tooshrink.
* **ShrinkCheckIdleTimes** -Olá número de verificações de redução contínuas (separadas por **ShrinkCheckIntervalMins**) tooindicate Olá nós estão ociosos.
* **UseLastConfigurations** -Olá configurações anteriores salvas no arquivo de argumento de saudação.
* **ArgFile**- Olá nome da saudação argumento arquivo usado toosave e Olá configurações toorun Olá script de atualização.
* **LogFilePrefix** -nome do prefixo Olá Olá do arquivo de log. Você pode especificar um caminho. Por padrão o log de saudação é escrito toohello diretório de trabalho atual.

### <a name="example-1"></a>Exemplo 1
Olá, exemplo a seguir configura hello Azure intermitente nós implantados com o modelo AzureNode padrão toogrow e reduzir automaticamente. Se todos os nós estão inicialmente em Olá **não implantado** estado, pelo menos 3 nós serão iniciados. Se o número de saudação de trabalhos em fila exceder 8, o script hello inicia nós até seu número excede a taxa de saudação de trabalhos em fila para **NumOfQueuedJobsPerNodeToGrow**. Se um nó for encontrado toobe ocioso por 3 vezes consecutivas, ele será interrompido.

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates @('Default AzureNode
 Template') -NodeType AzureNodes -NumOfQueuedJobsPerNodeToGrow 5
 -NumOfQueuedJobsToGrowThreshold 8 -NumOfInitialNodesToGrow 3
 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 3
```

### <a name="example-2"></a>Exemplo 2
Olá, exemplo a seguir configura hello Azure implantadas com hello modelo ComputeNode padrão toogrow VMs do nó de computação e reduzir automaticamente.
trabalhos Olá configurados pelo modelo de trabalho padrão Olá definem escopo de saudação da carga de trabalho no cluster hello. Se todos os nós de saudação forem interrompidos inicialmente, pelo menos 5 nós serão iniciados. Se o número de saudação de tarefas ativas em fila exceder 15, o script hello inicia nós até seu número excede a taxa de saudação de tarefas ativas em fila muito**NumOfActiveQueuedTasksPerNodeToGrow**. Se um nó for encontrado toobe ocioso em 10 vezes consecutivas, ele será interrompido.

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates 'Default ComputeNode Template' -JobTemplates 'Default' -NodeType ComputeNodes -NumOfActiveQueuedTasksPerNodeToGrow 10 -NumOfActiveQueuedTasksToGrowThreshold 15 -NumOfInitialNodesToGrow 5 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 10 -ArgFile 'IaaSVMComputeNodes_Arg.xml' -LogFilePrefix 'IaaSVMComputeNodes_log'
```
