---
title: aaaGet iniciado com o PowerShell para o lote do Azure | Microsoft Docs
description: "Uma breve introdução toohello cmdlets do PowerShell do Azure você pode usar recursos de lote toomanage."
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: f9ad62c5-27bf-4e6b-a5bf-c5f5914e6199
ms.service: batch
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: powershell
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3e4d12e9c1e52a5b2db2dd44346edda93b7ef92b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-resources-with-powershell-cmdlets"></a>Gerenciar recursos do Lote com cmdlets do PowerShell

Com hello cmdlets do PowerShell do lote do Azure, você pode executar e script muitas Olá mesmas tarefas que você realizar com hello APIs de lote, Olá portal do Azure e hello Azure Interface de linha de comando (CLI). Isso é cmdlets de toohello uma rápida introdução, você pode usar toomanage as contas de lote e trabalhar com os recursos de lote como pools, trabalhos e tarefas.

Para obter uma lista completa de cmdlets de lote e sintaxe do cmdlet detalhadas, consulte Olá [referência de cmdlet do Azure Batch](/powershell/module/azurerm.batch/#batch).

Este artigo baseia-se nos cmdlets do Azure PowerShell versão 3.0.0. Recomendamos que você atualize o PowerShell do Azure com frequência tootake vantagem do serviço de atualizações e aprimoramentos.

## <a name="prerequisites"></a>Pré-requisitos
Execute Olá após operações toouse Azure PowerShell toomanage seus recursos de lote.

* [Instalar e configurar o PowerShell do Azure](/powershell/azure/overview)
* Executar Olá **AzureRmAccount Login** cmdlet tooconnect tooyour assinatura (Olá ship do lote do Azure cmdlets no módulo do Azure Resource Manager Olá):
  
    `Login-AzureRmAccount`
* **Registrar com o namespace do provedor de lote Olá**. Esta operação só precisa toobe executada **uma vez por assinatura**.
  
    `Register-AzureRMResourceProvider -ProviderNamespace Microsoft.Batch`

## <a name="manage-batch-accounts-and-keys"></a>Gerenciar contas e chaves do Batch
### <a name="create-a-batch-account"></a>Criar uma conta do Batch
**New-AzureRmBatchAccount** cria uma conta do Lote em um grupo de recursos especificado. Se você ainda não tiver um grupo de recursos, crie um executando Olá [AzureRmResourceGroup novo](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet. Especifique um hello Azure regiões no hello **local** parâmetro, como "Central US". Por exemplo:

    New-AzureRmResourceGroup –Name MyBatchResourceGroup –location "Central US"

Em seguida, crie uma conta de lote no grupo de recursos hello, especificando um nome de conta de saudação em <*account_name*> e o local de saudação e o nome do seu grupo de recursos. Criar conta do lote Olá pode levar algum tempo toocomplete. Por exemplo:

    New-AzureRmBatchAccount –AccountName <account_name> –Location "Central US" –ResourceGroupName <res_group_name>

> [!NOTE]
> conta do lote Olá nome deve ser exclusivo toohello região do Azure para o grupo de recursos de saudação conter entre 3 e 24 caracteres e usar somente letras minúsculas e números.
> 
> 

### <a name="get-account-access-keys"></a>Obter chaves de acesso da conta
**Get-AzureRmBatchAccountKeys** mostra Olá chaves de acesso associadas a uma conta de lote do Azure. Por exemplo, execute Olá tooget Olá primários e secundários as chaves da conta Olá criado a seguir.

    $Account = Get-AzureRmBatchAccountKeys –AccountName <account_name>

    $Account.PrimaryAccountKey

    $Account.SecondaryAccountKey

### <a name="generate-a-new-access-key"></a>Gerar uma nova chave de acesso
**New-AzureRmBatchAccountKey** gera uma nova chave de conta primária ou secundária para uma conta do Lote do Azure. Por exemplo, toogenerate uma nova chave primária para sua conta em lotes, digite:

    New-AzureRmBatchAccountKey -AccountName <account_name> -KeyType Primary

> [!NOTE]
> toogenerate uma nova chave secundária, especifique "Secundário" para Olá **KeyType** parâmetro. Você tem chaves de primárias e secundárias Olá tooregenerate separadamente.
> 
> 

### <a name="delete-a-batch-account"></a>Excluir uma conta do Batch
**Remove-AzureRmBatchAccount** exclui uma conta do Lote. Por exemplo:

    Remove-AzureRmBatchAccount -AccountName <account_name>

Quando solicitado, confirme que você deseja tooremove Olá conta. Remoção de conta pode levar algum tempo toocomplete.

## <a name="create-a-batchaccountcontext-object"></a>Criar um objeto BatchAccountContext
usando tooauthenticate Olá cmdlets do PowerShell de lote quando você cria e gerenciar pools de lote, trabalhos, tarefas, e outros recursos, primeiro crie um toostore de objeto BatchAccountContext seu nome de conta e chaves:

    $context = Get-AzureRmBatchAccountKeys -AccountName <account_name>

Você passa o objeto de BatchAccountContext Olá em cmdlets que use Olá **BatchContext** parâmetro.

> [!NOTE]
> Por padrão, a chave primária da conta Olá é usado para autenticação, mas você pode selecionar toouse chave Olá alterando seu objeto de BatchAccountContext **KeyInUse** propriedade: `$context.KeyInUse = "Secondary"`.
> 
> 

## <a name="create-and-modify-batch-resources"></a>Criar e modificar recursos do Lote
Como usar os cmdlets **New-AzureBatchPool**, **New-AzureBatchJob**, e **AzureBatchTask novo** toocreate recursos em uma conta de lote. Há correspondentes **Get -** e **Set -** propriedades de saudação tooupdate cmdlets dos recursos existentes, e **Remove -** cmdlets tooremove recursos em uma conta de lote.

Ao usar muitos desses cmdlets em adição toopassing um objeto BatchContext, você precisa toocreate ou passa objetos que contêm configurações de recursos detalhado, conforme mostrado no exemplo a seguir de saudação. Consulte Olá ajuda detalhada para cada cmdlet para obter exemplos adicionais.

### <a name="create-a-batch-pool"></a>Criar um pool do Lote
Ao criar ou atualizar um pool de lote, selecione a configuração de máquina virtual de hello ou configuração de serviço de nuvem Olá para hello sistema operacional Olá nós de computação (consulte [visão geral do recurso de lote](batch-api-basics.md#pool)). Se você especificar a configuração do serviço de nuvem hello, seus nós de computação são representados com uma saudação [versões do sistema operacional de convidado do Azure](../cloud-services/cloud-services-guestos-update-matrix.md#releases). Se você especificar a configuração de máquina virtual hello, você pode especificar uma saudação suporte para Linux ou imagens de VM do Windows hello listado na [Marketplace de máquinas virtuais do Azure][vm_marketplace], ou forneça um personalizado imagem que você preparou.

Quando você executa **AzureBatchPool novo**, passar um objeto PSCloudServiceConfiguration ou PSVirtualMachineConfiguration configurações do sistema operacional hello. Por exemplo, hello cmdlet a seguir cria um novo pool de lote conosco de computação pequenos de tamanho na configuração de serviço de nuvem hello, criação de uma imagem com a versão do sistema operacional mais recente Olá da família 3 (Windows Server 2012). Aqui, Olá **CloudServiceConfiguration** parâmetro especifica Olá *$configuration* variável como objeto de PSCloudServiceConfiguration hello. Olá **BatchContext** parâmetro especifica uma variável definida anteriormente *$context* como objeto de BatchAccountContext hello.

    $configuration = New-Object -TypeName "Microsoft.Azure.Commands.Batch.Models.PSCloudServiceConfiguration" -ArgumentList @(4,"*")

    New-AzureBatchPool -Id "AutoScalePool" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -AutoScaleFormula '$TargetDedicated=4;' -BatchContext $context

número de destino de saudação de nós de computação no novo pool de saudação é determinado por uma fórmula de dimensionamento automático. Nesse caso, a fórmula de saudação é simplesmente **$TargetDedicated = 4**, indicando que o número de saudação de nós de computação no pool de saudação está 4 no máximo.

## <a name="query-for-pools-jobs-tasks-and-other-details"></a>Consultar pools, trabalhos, tarefas e outros detalhes
Como usar os cmdlets **Get-AzureBatchPool**, **Get-AzureBatchJob**, e **Get-AzureBatchTask** tooquery para entidades criadas em uma conta de lote.

### <a name="query-for-data"></a>Consultar dados
Por exemplo, use **Get-AzureBatchPools** toofind os pools. Por padrão essa consulta para todos os pools na sua conta, supondo que você já armazenado objeto BatchAccountContext Olá *$context*:

    Get-AzureBatchPool -BatchContext $context

### <a name="use-an-odata-filter"></a>Usar um filtro OData
Você pode fornecer um filtro OData usando Olá **filtro** toofind parâmetro hello apenas objetos que você está interessado. Por exemplo, você pode localizar todos os pools com ids que começam com "myPool":

    $filter = "startswith(id,'myPool')"

    Get-AzureBatchPool -Filter $filter -BatchContext $context

Esse método não é tão flexível quanto usar "Where-Object" em um pipeline local. No entanto, consulta Olá é enviada toohello serviço de lote diretamente para que toda a filtragem ocorre no lado do servidor de saudação, economizando largura de banda de Internet.

### <a name="use-hello-id-parameter"></a>Use o parâmetro de Id de saudação
Um filtro de OData tooan alternativo é Olá toouse **Id** parâmetro. tooquery de um determinado pool com id "myPool":

    Get-AzureBatchPool -Id "myPool" -BatchContext $context

Olá **Id** parâmetro oferece suporte a somente pesquisa completo-id, não curingas ou filtros de estilo do OData.

### <a name="use-hello-maxcount-parameter"></a>Use o parâmetro MaxCount de saudação
Por padrão, cada cmdlet retorna no máximo 1.000 objetos. Se você atingir esse limite, refine seu filtro toobring volta menos objetos tanto definir explicitamente um máximo usando Olá **MaxCount** parâmetro. Por exemplo:

    Get-AzureBatchTask -MaxCount 2500 -BatchContext $context

Definir limite superior do tooremove Olá, **MaxCount** too0 ou menos.

### <a name="use-hello-powershell-pipeline"></a>Usar o pipeline do PowerShell Olá
Cmdlets de lote podem utilizar dados toosend de pipeline de PowerShell saudação entre cmdlets. Isso tem o mesmo efeito que especificar um parâmetro, mas torna trabalhar com várias entidades de saudação.

Por exemplo, localize e exiba todas as tarefas em sua conta:

    Get-AzureBatchJob -BatchContext $context | Get-AzureBatchTask -BatchContext $context

Reinicializar todos os nós de computação em um pool:

    Get-AzureBatchComputeNode -PoolId "myPool" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

## <a name="application-package-management"></a>Gerenciamento de pacote de aplicativos
Pacotes de aplicativos fornecem uma maneira de simplificado toodeploy aplicativos toohello nós de computação em seus pools. Com hello cmdlets do PowerShell do lote, carregar e gerenciar pacotes de aplicativos em sua conta de lote e implantar nós de toocompute de versões do pacote.

**Criar** um aplicativo:

    New-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

**Adicionar** um pacote de aplicativos:

    New-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0" -Format zip -FilePath package001.zip

Saudação de conjunto **versão padrão** para o aplicativo hello:

    Set-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -DefaultVersion "1.0"

**Listar** pacotes de um aplicativo

    $application = Get-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

    $application.ApplicationPackages

**Excluir** um pacote de aplicativo

    Remove-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0"

**Excluir** um aplicativo

    Remove-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

> [!NOTE]
> Você deve excluir todas as versões do pacote de aplicativo do aplicativo antes de excluir o aplicativo hello. Se você tentar toodelete um aplicativo que tem atualmente os pacotes de aplicativos, você receberá um erro de 'conflito de '.
> 
> 

### <a name="deploy-an-application-package"></a>Implantar um pacote de aplicativos
Você pode especificar um ou mais pacotes de aplicativos para implantação durante a criação de um pool. Quando você especificar um pacote no momento da criação de pool, é implantado tooeach nó como Olá nó junções pool. Pacotes também são implantados quando um nó é reinicializado ou quando sua imagem é refeita.

Especifique a saudação `-ApplicationPackageReference` opção ao criar um pool toodeploy nós de um pacote toohello do pool de aplicativos ao entrarem pool hello. Primeiro, crie um **PSApplicationPackageReference** de objeto e configurá-lo com hello Id e o pacote de versão do aplicativo deseja que nós de computação do pool de toodeploy toohello:

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "1.0"

Agora criar pool hello e especificar o objeto de referência de pacote hello como Olá argumento toohello `ApplicationPackageReferences` opção:

    New-AzureBatchPool -Id "PoolWithAppPackage" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -BatchContext $context -ApplicationPackageReferences $appPackageReference

Você pode encontrar mais informações sobre pacotes de aplicativos em [implantar aplicativos toocompute nós com pacotes de aplicativos de lote](batch-application-packages.md).

> [!IMPORTANT]
> Você deve [vincular uma conta de armazenamento do Azure](#linked-storage-account-autostorage) tooyour lote conta toouse pacotes de aplicativos.
> 
> 

### <a name="update-a-pools-application-packages"></a>Atualizar pacotes de aplicativos de um pool
aplicativos de saudação tooupdate atribuídos tooan pool existente, primeiro crie um objeto de PSApplicationPackageReference com propriedades de saudação desejada (versão de pacote e a Id de aplicativo):

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "2.0"

Em seguida, obter o pool de saudação do lote, limpar todos os pacotes existentes, adicionar nossa nova referência de pacote e atualizar o serviço de lote de saudação com novas configurações de pool hello:

    $pool = Get-AzureBatchPool -BatchContext $context -Id "PoolWithAppPackage"

    $pool.ApplicationPackageReferences.Clear()

    $pool.ApplicationPackageReferences.Add($appPackageReference)

    Set-AzureBatchPool -BatchContext $context -Pool $pool

Agora que você atualizou os propriedades do pool de saudação no serviço de lote de saudação. tooactually implantar Olá novo aplicativo pacote toocompute nós no pool hello, no entanto, você deve reinicializar ou refazer em nós. Você pode reiniciar todos os nós em um pool com este comando:

    Get-AzureBatchComputeNode -PoolId "PoolWithAppPackage" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

> [!TIP]
> Você pode implantar vários aplicativos pacotes toohello nós de computação em um pool. Se você quiser muito*adicionar* um pacote de aplicativo em vez de substituir os pacotes de saudação atualmente implantado, omita Olá `$pool.ApplicationPackageReferences.Clear()` linha acima.
> 
> 

## <a name="next-steps"></a>Próximas etapas
* Para obter a sintaxe detalhada do cmdlet, veja [Referência de cmdlet do Lote do Azure](/powershell/module/azurerm.batch/#batch).
* Para obter mais informações sobre aplicativos e pacotes de aplicativos em lote, consulte [implantar aplicativos toocompute nós com pacotes de aplicativos de lote](batch-application-packages.md).

[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/