---
title: aaaMigrate tooResource Manager com o PowerShell | Microsoft Docs
description: "Este artigo o orienta por meio da migração de suporte de plataforma de saudação de recursos de IaaS como máquinas virtuais (VMs), redes virtuais (VNETs) e contas de armazenamento do clássico tooAzure Resource Manager (ARM) usando comandos do PowerShell do Azure"
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 2b3dff9b-2e99-4556-acc5-d75ef234af9c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: b5b2987da292f1c241be71a354b0c2e1a96a07c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-iaas-resources-from-classic-tooazure-resource-manager-by-using-azure-powershell"></a>Migrar recursos de IaaS de tooAzure clássico Gerenciador de recursos usando o PowerShell do Azure
Estas etapas mostram como os toouse do Azure PowerShell comandos toomigrate infraestrutura como um recurso de serviço (IaaS) do modelo de implantação do hello implantação clássica modelo toohello Gerenciador de recursos do Azure.

Se desejar, você também pode migrar recursos usando Olá [Interface de linha de comando (CLI do Azure) do Azure](../linux/migration-classic-resource-manager-cli.md).

* Para obter informações sobre cenários de migração com suporte, consulte [plataforma suportada migração de recursos de IaaS de tooAzure clássico Gerenciador de recursos](migration-classic-resource-manager-overview.md).
* Para obter orientações detalhadas e um passo a passo de migração, consulte [técnico mergulho profundo na plataforma suportada migração de clássico tooAzure Gerenciador de recursos](migration-classic-resource-manager-deep-dive.md).
* [Examinar os erros de migração mais comuns](migration-classic-resource-manager-errors.md)

<br>
Aqui está uma ordem de saudação do fluxograma tooidentify nos quais etapas precisam toobe executado durante o processo de migração

![Captura de tela que mostra as etapas de migração de saudação](media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-plan-for-migration"></a>Etapa 1: Planejar a migração
Aqui estão algumas práticas recomendadas que recomendamos durante a avaliação de migração de recursos de IaaS do clássico tooResource Manager:

* Leia Olá [com e sem suporte a recursos e configurações](migration-classic-resource-manager-overview.md). Se você tiver máquinas virtuais que usam recursos ou configurações sem suporte, é recomendável que você aguarde Olá configuração/recurso suporte toobe anunciada. Como alternativa, se ele atende às suas necessidades, remover esse recurso ou mover para fora da migração tooenable configuração.
* Se você tiver automatizado scripts que implantar a infraestrutura e os aplicativos de hoje, tente toocreate uma configuração de teste semelhante usando esses scripts para a migração. Como alternativa, você pode configurar ambientes de exemplo usando Olá portal do Azure.

> [!IMPORTANT]
> Os Gateways de aplicativos não têm suporte atualmente para a migração de clássico tooResource Manager. toomigrate uma rede virtual clássica com um gateway de aplicativo, remova gateway Olá antes de executar uma rede Olá de toomove de operação de preparação. Depois de concluir a migração de hello, reconecte gateway Olá no Gerenciador de recursos do Azure.
>
>Gateways de rota expressa conectando tooExpressRoute circuitos em outra assinatura não podem ser migrados automaticamente. Nesses casos, remover o gateway de rota expressa hello, migrar a rede virtual hello e recrie o gateway hello. Consulte [ExpressRoute migrar circuitos e associadas a redes virtuais do modelo de implantação do Gerenciador de recursos de toohello clássico de Olá](../../expressroute/expressroute-migration-classic-resource-manager.md) para obter mais informações.
>
>

## <a name="step-2-install-hello-latest-version-of-azure-powershell"></a>Etapa 2: Instalar a versão mais recente de saudação do PowerShell do Azure
Há duas opções principais tooinstall PowerShell do Azure: [Galeria do PowerShell](https://www.powershellgallery.com/profiles/azure-sdk/) ou [Web Platform Installer (WebPI)](http://aka.ms/webpi-azps). WebPI recebe atualizações mensais. A Galeria do PowerShell receberá atualizações continuamente. Este artigo tem base no Azure PowerShell versão 2.1.0.

Para obter instruções de instalação, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).

<br>

## <a name="step-3-ensure-that-you-are-an-administrator-for-hello-subscription-in-azure-portal"></a>Etapa 3: Verifique se você for um administrador de assinatura de saudação no portal do Azure
tooperform a migração, você deve ser adicionado como coadministrador da assinatura Olá Olá [portal do Azure](https://portal.azure.com).

1. O logon no hello [portal do Azure](https://portal.azure.com).
2. No menu de Hub hello, selecione **assinatura**. Caso não visualize essa opção, selecione **Mais serviços**.
3. Localizar a entrada de assinatura apropriada hello, examinar Olá **minha função** campo. Para um coadministrador, o valor de saudação deve ser _administrador da conta_.

Se você não for capaz de tooadd um coadministrador, contate um administrador de serviço ou coadministrador para Olá assinatura tooget por conta própria adicionado.   

## <a name="step-4-set-your-subscription-and-sign-up-for-migration"></a>Etapa 4: Definir a assinatura e se inscrever para a migração
Primeiro, inicie um prompt do PowerShell. Para a migração, você precisa tooset seu ambiente para ambos os clássico e o Gerenciador de recursos.

Entre na conta de tooyour para o modelo do Gerenciador de recursos de saudação.

```powershell
    Login-AzureRmAccount
```

Obter assinaturas disponíveis hello usando Olá comando a seguir:

```powershell
    Get-AzureRMSubscription | Sort Name | Select Name
```

Defina sua assinatura do Azure para Olá a sessão atual. Este exemplo define Olá nome da assinatura padrão muito**minha assinatura do Azure**. Substitua o nome de inscrição do exemplo hello com seus próprios.

```powershell
    Select-AzureRmSubscription –SubscriptionName "My Azure Subscription"
```

> [!NOTE]
> O registro é uma etapa única, mas é preciso executá-lo uma vez antes de tentar a migração. Sem registrar, você verá Olá a seguinte mensagem de erro:
>
> *BadRequest: a assinatura não está registrada para migração.*
>
>

Registrar com o provedor de recursos de migração de saudação usando Olá comando a seguir:

```powershell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

Aguarde cinco minutos para Olá toofinish de registro. Você pode verificar o status de saudação de aprovação de saudação usando Olá comando a seguir:

```powershell
    Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

Verifique se RegistrationState é `Registered` antes de continuar.

Agora, entre na conta de tooyour para o modelo clássico hello.

```powershell
    Add-AzureAccount
```

Obter assinaturas disponíveis hello usando Olá comando a seguir:

```powershell
    Get-AzureSubscription | Sort SubscriptionName | Select SubscriptionName
```

Defina sua assinatura do Azure para Olá a sessão atual. Este exemplo define a assinatura de padrão de saudação muito**minha assinatura do Azure**. Substitua o nome de inscrição do exemplo hello com seus próprios.

```powershell
    Select-AzureSubscription –SubscriptionName "My Azure Subscription"
```

<br>

## <a name="step-5-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-hello-azure-region-of-your-current-deployment-or-vnet"></a>Etapa 5: Verifique se que você tem suficiente núcleos de máquina Virtual do Azure Resource Manager no hello região do Azure de sua implantação atual ou a rede virtual
Você pode usar o hello PowerShell comando toocheck Olá número atual de núcleos que você tem no Gerenciador de recursos do Azure a seguir. toolearn mais sobre cotas de core, consulte [limites e hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager).

Este exemplo verifica a disponibilidade Olá Olá **Oeste dos EUA** região. Substitua o nome da região exemplo hello com seus próprios.

```powershell
Get-AzureRmVMUsage -Location "West US"
```

## <a name="step-6-run-commands-toomigrate-your-iaas-resources"></a>Etapa 6: Executar comandos toomigrate seus recursos de IaaS
> [!NOTE]
> Todas as operações de saudação descritas aqui são idempotentes. Se você tiver um problema que não seja um recurso sem suporte ou um erro de configuração, é recomendável que você repita Olá preparar, anular ou confirmar a operação. plataforma de saudação tentará novamente a ação de saudação.
>
>

## <a name="step-61-option-1---migrate-virtual-machines-in-a-cloud-service-not-in-a-virtual-network"></a>Etapa 6.1: Opção 1 - Migrar máquinas virtuais em um serviço de nuvem (não em uma rede virtual)
Obter uma lista de serviços de nuvem usando o comando a seguir de saudação e, em seguida, escolha Olá serviço em nuvem que você deseja toomigrate hello. Se Olá VMs no serviço de nuvem Olá está em uma rede virtual ou se eles têm funções web ou de trabalho, o comando Olá retorna uma mensagem de erro.

```powershell
    Get-AzureService | ft Servicename
```

Obter o nome de implantação Olá Olá serviço de nuvem. Neste exemplo, o nome do serviço de saudação é **meu serviço**. Substitua o nome do serviço de exemplo hello com seu próprio nome de serviço.

```powershell
    $serviceName = "My Service"
    $deployment = Get-AzureDeployment -ServiceName $serviceName
    $deploymentName = $deployment.DeploymentName
```

Prepare Olá VMs no serviço de nuvem Olá para migração. Você tem dois toochoose de opções do.

* **Opção 1. Migrar Olá VMs tooa criado plataforma rede virtual**

    Primeiro, valide se você pode migrar o serviço de nuvem hello usando Olá comandos a seguir:

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    $validate.ValidationMessages
    ```

    Olá comando anterior exibe avisos e erros que bloqueiam a migração. Se a validação for bem-sucedida, você pode mover toohello **preparar** etapa:

    ```powershell
    Move-AzureService -Prepare -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    ```
* **Opção 2. Migrar a rede virtual existente do tooan no modelo de implantação do Gerenciador de recursos de saudação**

    Este exemplo define Olá nome do grupo de recursos muito**myResourceGroup**, Olá muito o nome de rede virtual**myVirtualNetwork** e Olá nome da sub-rede muito**mySubNet**. Substitua os nomes de saudação no exemplo hello com nomes de saudação de seus próprios recursos.

    ```powershell
    $existingVnetRGName = "myResourceGroup"
    $vnetName = "myVirtualNetwork"
    $subnetName = "mySubNet"
    ```

    Primeiro, valide se migrar Olá rede virtual usando o comando a seguir de saudação:

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName -VirtualNetworkName $vnetName -SubnetName $subnetName
    $validate.ValidationMessages
    ```

    Olá comando anterior exibe avisos e erros que bloqueiam a migração. Se a validação for bem-sucedida, você pode prosseguir com hello etapa de preparação a seguir:

    ```powershell
        Move-AzureService -Prepare -ServiceName $serviceName -DeploymentName $deploymentName `
        -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName `
        -VirtualNetworkName $vnetName -SubnetName $subnetName
    ```

Depois de Olá operação preparar for bem-sucedida com o hello anterior opções, consulte o estado de migração de saudação do hello VMs. Certifique-se de que eles estejam em Olá `Prepared` estado.

Este exemplo define Olá nome da VM muito**myVM**. Substitua o nome do exemplo hello com seu próprio nome VM.

```powershell
    $vmName = "myVM"
    $vm = Get-AzureVM -ServiceName $serviceName -Name $vmName
    $vm.VM.MigrationState
```

Verifique a configuração de saudação para Olá preparado recursos usando o PowerShell ou Olá portal do Azure. Se você não está pronto para migração e desejar toogo toohello back antigo estado, use Olá comando a seguir:

```powershell
    Move-AzureService -Abort -ServiceName $serviceName -DeploymentName $deploymentName
```

Se configuração preparada Olá parece bom, você pode Avançar e confirmar recursos hello usando o comando a seguir de saudação:

```powershell
    Move-AzureService -Commit -ServiceName $serviceName -DeploymentName $deploymentName
```

## <a name="step-61-option-2---migrate-virtual-machines-in-a-virtual-network"></a>Etapa 6.1: Opção 2 - Migrar máquinas virtuais em uma rede virtual

máquinas virtuais de toomigrate em uma rede virtual, você migrar a rede virtual hello. máquinas virtuais de saudação migrar automaticamente com a rede virtual hello. Escolha Olá rede virtual que você deseja toomigrate.
> [!NOTE]
> [Migrar máquina virtual clássica](migrate-single-classic-to-resource-manager.md) criando uma nova máquina virtual Gerenciador de recursos com discos gerenciados usando os arquivos hello (sistema operacional e dados) de VHD de máquina virtual de saudação.
<br>

> [!NOTE]
> nome da rede virtual Olá pode ser diferente do que é exibido no hello novo Portal. Olá, novo Portal do Azure exibe nome hello como `[vnet-name]` mas o nome de rede virtual real Olá é do tipo `Group [resource-group-name] [vnet-name]`. Antes de migrar, nome da pesquisa Olá real de rede virtual usando o comando Olá `Get-AzureVnetSite | Select -Property Name` ou exibi-lo no hello antigo Portal do Azure. 

Este exemplo define Olá nome de rede virtual muito**myVnet**. Substitua o nome de rede virtual do exemplo hello com seus próprios.

```powershell
    $vnetName = "myVnet"
```

> [!NOTE]
> Se a rede virtual Olá contém web ou funções de trabalho ou máquinas virtuais com configurações sem suporte, você receberá uma mensagem de erro de validação.
>
>

Primeiro, valide se você pode migrar a rede virtual Olá usando Olá comando a seguir:

```powershell
    Move-AzureVirtualNetwork -Validate -VirtualNetworkName $vnetName
```

Olá comando anterior exibe avisos e erros que bloqueiam a migração. Se a validação for bem-sucedida, você pode prosseguir com hello etapa de preparação a seguir:

```powershell
    Move-AzureVirtualNetwork -Prepare -VirtualNetworkName $vnetName
```

Verifique a configuração de saudação para Olá preparado máquinas virtuais usando o Azure PowerShell ou Olá portal do Azure. Se você não está pronto para migração e desejar toogo toohello back antigo estado, use Olá comando a seguir:

```powershell
    Move-AzureVirtualNetwork -Abort -VirtualNetworkName $vnetName
```

Se configuração preparada Olá parece bom, você pode Avançar e confirmar recursos hello usando o comando a seguir de saudação:

```powershell
    Move-AzureVirtualNetwork -Commit -VirtualNetworkName $vnetName
```

## <a name="step-62-migrate-a-storage-account"></a>Etapa 6.2 Migrar uma conta de armazenamento
Quando terminar de migração de máquinas virtuais Olá, é recomendável que migrar as contas de armazenamento hello.

Antes de migrar uma conta de armazenamento hello, execute anterior verificações de pré-requisitos:

* **Migrar máquinas virtuais clássicas cujos discos são armazenados na conta de armazenamento Olá**

    Precede o comando retorna propriedades de RoleName e DiskName de todos os discos VM clássicos Olá na conta de armazenamento hello. RoleName é o nome de saudação do hello toowhich de máquina virtual em um disco está anexado. Se precede o comando retorna discos, em seguida, certifique-se de que toowhich de máquinas virtuais que esses discos anexados são migrados antes de migrar Olá conta de armazenamento.
    ```powershell
     $storageAccountName = 'yourStorageAccountName'
      Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Select-Object -ExpandProperty AttachedTo -Property `
      DiskName | Format-List -Property RoleName, DiskName

    ```
* **Excluir desanexada clássicos discos VM armazenados na conta de armazenamento Olá**

    Localize desanexada clássicos discos de VM no armazenamento de saudação de conta usando a seguinte comando:

    ```powershell
        $storageAccountName = 'yourStorageAccountName'
        Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Where-Object -Property AttachedTo -EQ $null | Format-List -Property DiskName  

    ```
    Se o comando acima retornar discos, exclua-os usando o seguinte comando:

    ```powershell
       Remove-AzureDisk -DiskName 'yourDiskName'
    ```
* **Excluir imagens da VM armazenadas na conta de armazenamento Olá**

    Precede o comando retorna todas as imagens VM Olá com armazenados na conta de armazenamento de saudação de disco do sistema operacional.
     ```powershell
        Get-AzureVmImage | Where-Object { $_.OSDiskConfiguration.MediaLink -ne $null -and $_.OSDiskConfiguration.MediaLink.Host.Contains($storageAccountName)`
                                } | Select-Object -Property ImageName, ImageLabel
     ```
     Precede o comando retorna todas as imagens VM Olá com discos de dados armazenados na conta de armazenamento hello.
     ```powershell

        Get-AzureVmImage | Where-Object {$_.DataDiskConfigurations -ne $null `
                                         -and ($_.DataDiskConfigurations | Where-Object {$_.MediaLink -ne $null -and $_.MediaLink.Host.Contains($storageAccountName)}).Count -gt 0 `
                                        } | Select-Object -Property ImageName, ImageLabel
     ```
    Exclua todas as imagens VM Olá retornadas por acima comandos usando o comando anterior:
    ```powershell
    Remove-AzureVMImage -ImageName 'yourImageName'
    ```

Valide cada conta de armazenamento para a migração usando o comando a seguir de saudação. Neste exemplo, é o nome de conta de armazenamento Olá **myStorageAccount**. Substitua o nome do exemplo hello com nome de saudação do sua própria conta de armazenamento.

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Validate -StorageAccountName $storageAccountName
```

Próxima etapa é a conta de armazenamento tooPrepare Olá para migração

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Prepare -StorageAccountName $storageAccountName
```

Verifique a configuração de saudação para Olá preparada a conta de armazenamento usando o Azure PowerShell ou Olá portal do Azure. Se você não está pronto para migração e desejar toogo toohello back antigo estado, use Olá comando a seguir:

```powershell
    Move-AzureStorageAccount -Abort -StorageAccountName $storageAccountName
```

Se configuração preparada Olá parece bom, você pode Avançar e confirmar recursos hello usando o comando a seguir de saudação:

```powershell
    Move-AzureStorageAccount -Commit -StorageAccountName $storageAccountName
```

## <a name="next-steps"></a>Próximas etapas
* [Visão geral da plataforma suportada migração de recursos de IaaS de tooAzure clássico Gerenciador de recursos](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Técnico mergulho profundo na plataforma suportada migração de clássico tooAzure Gerenciador de recursos](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Planejando a migração de recursos de IaaS de tooAzure clássico Gerenciador de recursos](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Usar recursos de IaaS toomigrate CLI do clássico tooAzure Gerenciador de recursos](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Ferramentas de comunidade para ajudar com a migração de recursos de IaaS de tooAzure clássico Gerenciador de recursos](migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Examinar os erros de migração mais comuns](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Saudação de revisão mais perguntas frequentes sobre migração de recursos de IaaS do clássico tooAzure Gerenciador de recursos](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
