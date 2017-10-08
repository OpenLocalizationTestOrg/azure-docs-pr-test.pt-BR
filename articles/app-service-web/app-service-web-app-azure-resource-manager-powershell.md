---
title: aaaAzure PowerShell com base no Gerenciador de recursos de comandos para o aplicativo Web do Azure | Microsoft Docs
description: "Saiba como toouse Olá toomanage novo de comandos PowerShell do Azure Resource Manager com base em seus aplicativos da Web do Azure."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 4231fbba-61e5-4f92-b958-531c066fb87f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: bbb821e89daa315280436e84e11316217bb644d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-based-powershell-toomanage-azure-web-apps"></a>Usando aplicativos de Web do Azure PowerShell Azure Resource Manager-Based tooManage
> [!div class="op_single_selector"]
> * [CLI do Azure](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [PowerShell do Azure](app-service-web-app-azure-resource-manager-powershell.md)
> 
> 

Com o Microsoft Azure PowerShell versão 1.0.0 foram adicionados novos comandos, que fornecem Olá usuário Olá capacidade toouse com base no Gerenciador de recursos do Azure PowerShell comandos toomanage aplicativos Web.

toolearn sobre o gerenciamento de grupos de recursos, consulte [usando o PowerShell do Azure com o Azure Resource Manager](../powershell-azure-resource-manager.md). 

toolearn sobre a lista completa de saudação de parâmetros e as opções de saudação cmdlets do PowerShell, consulte Olá [completo referência do Cmdlet baseado em Web aplicativo do Azure Resource Manager de Cmdlets do PowerShell](https://msdn.microsoft.com/library/mt619237.aspx)

## <a name="managing-app-service-plans"></a>Gerenciando Planos do Serviço de Aplicativo
### <a name="create-an-app-service-plan"></a>Criar um Plano do Serviço de Aplicativo
toocreate um plano de serviço de aplicativo, use Olá **AzureRmAppServicePlan novo** cmdlet.

Seguem as descrições dos parâmetros diferentes hello:

* **Nome**: nome do plano de serviço de aplicativo hello.
* **Local**: a localização do plano do serviço.
* **ResourceGroupName**: grupo de recursos que inclui o plano de serviço de aplicativo hello recém-criado.
* **Camada**: Olá desejado de preço (o padrão é gratuito, outras opções são compartilhados, Basic, Standard e Premium).
* **WorkerSize**: Olá tamanho de trabalhadores (o padrão é pequeno se o parâmetro de camada de saudação foi especificado como Basic, Standard ou Premium. Outras opções são Médio e Grande.)
* **NumberofWorkers**: Olá número de trabalhadores no plano de serviço de aplicativo hello (o valor padrão é 1). 

Exemplo toouse esse cmdlet:

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -Tier Premium -WorkerSize Large -NumberofWorkers 10

### <a name="create-an-app-service-plan-in-an-app-service-environment"></a>Criar um Plano do Serviço de Aplicativo em um Ambiente de Serviço de Aplicativo
plano de um aplicativo de serviço toocreate em um ambiente de serviço de aplicativo, use Olá mesmo comando **AzureRmAppServicePlan novo** com nome hello toospecify de parâmetros adicionais do ASE e o nome do grupo de recursos do ASE.

Exemplo toouse esse cmdlet:

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -AseName constosoASE -AseResourceGroupName contosoASERG -Tier Premium -WorkerSize Large -NumberofWorkers 10

mais sobre o ambiente de serviço de aplicativo, seleção de toolearn [Introdução tooApp ambiente de serviço](app-service-app-service-environment-intro.md)

### <a name="list-existing-app-service-plans"></a>Listar os Planos do Serviço de Aplicativo existentes
toolist Olá existente aplicativo planos de serviço, use **AzureRmAppServicePlan Get** cmdlet.

toolist todos os planos de serviço de aplicativo em sua assinatura, use: 

    Get-AzureRmAppServicePlan

toolist todos os planos de serviço de aplicativo em um grupo de recursos específico, use:

    Get-AzureRmAppServicePlan -ResourceGroupname ContosoAzureResourceGroup

tooget um plano de serviço de aplicativo específico, use:

    Get-AzureRmAppServicePlan -Name ContosoAppServicePlan


### <a name="configure-an-existing-app-service-plan"></a>Configurar um Plano do Serviço de Aplicativo existente
configurações de saudação toochange para um plano de serviço de aplicativo existente, use Olá **AzureRmAppServicePlan conjunto** cmdlet. Você pode alterar a camada Olá, tamanho do trabalho e número de saudação de trabalhos 

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard -WorkerSize Medium -NumberofWorkers 9

#### <a name="scaling-an-app-service-plan"></a>Dimensionando um Plano do Serviço de Aplicativo
tooscale um aplicativo de serviço de plano existente, use:

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -NumberofWorkers 9

#### <a name="changing-hello-worker-size-of-an-app-service-plan"></a>Alterando o tamanho de trabalhador de saudação de um plano de serviço de aplicativo
tamanho de saudação toochange de trabalhadores em um aplicativo de serviço plano existente, use:

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -WorkerSize Medium

#### <a name="changing-hello-tier-of-an-app-service-plan"></a>Saudação de alteração da camada de um plano de serviço de aplicativo
camada de saudação toochange de um aplicativo de serviço plano existente, use:

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard

### <a name="delete-an-existing-app-service-plan"></a>Excluir um Plano do Serviço de Aplicativo existente
toodelete um plano de serviço de aplicativo existente, todos os atribuídos toobe de necessidade de aplicativos web movido ou excluído primeiro. Usando o hello **AzureRmAppServicePlan remover** cmdlet, você pode excluir o plano de serviço de aplicativo hello.

    Remove-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup

## <a name="managing-app-service-web-apps"></a>Gerenciando Aplicativos Web do Serviço de Aplicativo
### <a name="create-a-web-app"></a>Criar um aplicativo Web
toocreate um aplicativo web, use Olá **AzureRmWebApp novo** cmdlet.

Seguem as descrições dos parâmetros diferentes hello:

* **Nome**: nome do aplicativo web de saudação.
* **AppServicePlan**: nome do plano de serviço Olá usado toohost Olá web app.
* **ResourceGroupName**: grupo de recursos que hospeda o plano de serviço de aplicativo hello.
* **Local**: Olá local do aplicativo web.

Exemplo toouse esse cmdlet:

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"

### <a name="create-a-web-app-in-an-app-service-environment"></a>Criar um aplicativo Web em um Ambiente de Serviço de Aplicativo
toocreate um aplicativo web no ambiente de serviço de um aplicativo (ASE). Use Olá mesmo **AzureRmWebApp novo** com o nome da saudação ASE toospecify parâmetros adicionais e o nome do grupo de recursos de Olá Olá ASE pertence a.

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"  -ASEName ContosoASEName -ASEResourceGroupName ContosoASEResourceGroupName

mais sobre o ambiente de serviço de aplicativo, seleção de toolearn [Introdução tooApp ambiente de serviço](app-service-app-service-environment-intro.md)

### <a name="delete-an-existing-web-app"></a>Excluir um aplicativo Web existente
toodelete um aplicativo web existente, você pode usar o hello **AzureRmWebApp remover** cmdlet, você precisa toospecify nome de saudação do aplicativo web de saudação e o nome do grupo de recursos de saudação.

    Remove-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup


### <a name="list-existing-web-apps"></a>Listar os aplicativos Web
toolist Olá existente os aplicativos web, use Olá **AzureRmWebApp Get** cmdlet.

toolist todos os aplicativos web em sua assinatura, use:

    Get-AzureRmWebApp

toolist todos os aplicativos web em um grupo de recursos específico, use:

    Get-AzureRmWebApp -ResourceGroupname ContosoAzureResourceGroup

tooget um aplicativo web específico, use:

    Get-AzureRmWebApp -Name ContosoWebApp

### <a name="configure-an-existing-web-app"></a>Configurar um aplicativo Web existente
configurações de saudação do toochange e as configurações para um aplicativo web existente, use Olá **AzureRmWebApp conjunto** cmdlet. Para obter uma lista completa de parâmetros, verifique Olá [link de referência de Cmdlet](https://msdn.microsoft.com/library/mt652487.aspx)

Exemplo (1): use essa cadeias de caracteres de conexão do cmdlet toochange

    $connectionstrings = @{ ContosoConn1 = @{ Type = “MySql”; Value = “MySqlConn”}; ContosoConn2 = @{ Type = “SQLAzure”; Value = “SQLAzureConn”} }
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -ConnectionStrings $connectionstrings

Exemplo (2): adicionar ou alterar as configurações do aplicativo

    $appsettings = @{appsetting1 = "appsetting1value"; appsetting2 = "appsetting2value"}
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -AppSettings $appsettings


Exemplo (3): definir Olá web aplicativo toorun no modo de 64 bits

    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -Use32BitWorkerProcess $False

### <a name="change-hello-state-of-an-existing-web-app"></a>Alterar o estado de saudação de um aplicativo Web existente
#### <a name="restart-a-web-app"></a>Reiniciar um aplicativo Web
toorestart um aplicativo web, você deve especificar Olá nome e grupo de recursos do aplicativo web de saudação.

    Restart-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="stop-a-web-app"></a>Parar um aplicativo Web
toostop um aplicativo web, você deve especificar Olá nome e grupo de recursos do aplicativo web de saudação.

    Stop-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="start-a-web-app"></a>Iniciar um aplicativo Web
toostart um aplicativo web, você deve especificar Olá nome e grupo de recursos do aplicativo web de saudação.

    Start-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-publishing-profiles"></a>Gerenciar perfis de publicação de aplicativos Web
Cada aplicativo web tem um perfil de publicação que pode ser usado toopublish seus aplicativos, várias operações podem ser executadas em perfis de publicação.

#### <a name="get-publishing-profile"></a>Obter o perfil de publicação
Olá tooget perfil para um aplicativo web, o uso de publicação:

    Get-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -OutputFile .\publishingprofile.txt

Este comando exibe Olá publicação de linha de comando de toohello perfil também Olá publicando o arquivo de texto tooa perfil de saída.

#### <a name="reset-publishing-profile"></a>Redefinir o perfil de publicação
tooreset ambos Olá a senha de publicação de FTP e implantação da web para um aplicativo web, use:

    Reset-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-certificates"></a>Gerenciar certificados de aplicativo Web
toolearn sobre como toomanage web certificados de aplicativo, consulte [associação de certificados SSL usando o PowerShell](app-service-web-app-powershell-ssl-binding.md)

### <a name="next-steps"></a>Próximas etapas
* toolearn sobre o suporte do PowerShell do Gerenciador de recursos do Azure, consulte [usando o PowerShell do Azure com o Gerenciador de recursos do Azure.](../powershell-azure-resource-manager.md)
* toolearn sobre ambientes de serviço de aplicativo, consulte [Introdução tooApp ambiente de serviço.](app-service-app-service-environment-intro.md)
* toolearn sobre como gerenciar certificados SSL do serviço de aplicativo usando o PowerShell, consulte [associação de certificados SSL usando o PowerShell.](app-service-web-app-powershell-ssl-binding.md)
* toolearn sobre a lista completa de saudação de cmdlets do PowerShell com base no Gerenciador de recursos do Azure para aplicativos da Web do Azure, consulte [referência de Cmdlet do Azure Web aplicativos do Azure Resource Manager de Cmdlets do PowerShell.](https://msdn.microsoft.com/library/mt619237.aspx)
* * toolearn sobre o gerenciamento de serviço de aplicativo usando a CLI, consulte [Using Azure Resource Manager-Based XPlat CLI para o aplicativo Web do Azure.](app-service-web-app-azure-resource-manager-xplat-cli.md)

