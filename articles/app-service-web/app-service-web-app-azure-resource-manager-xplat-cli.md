---
title: aaaAzure ferramentas de linha de comando de plataforma cruzada com base no Gerenciador de recursos para o aplicativo Web do Azure | Microsoft Docs
description: "Saiba como toouse Olá toomanage de novas ferramentas de linha de comando de plataforma cruzada com base no Azure Resource Manager seus aplicativos da Web do Azure."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: d415b195-4262-416f-b59f-7e1aef200054
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: 5f5e03edcb01154aef3bd220cd27358f69656ef4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-based-xplat-cli-for-azure-app-service"></a>Como usar a CLI XPlat com base no Azure Resource Manager para o Serviço de Aplicativo do Azure
> [!div class="op_single_selector"]
> * [CLI do Azure](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [PowerShell do Azure](app-service-web-app-azure-resource-manager-powershell.md)

Com o lançamento de saudação da versão de ferramentas de linha de comando de plataforma cruzada do Microsoft Azure 0.10.5, foram adicionados novos comandos. Esses comandos oferecem Olá usuário Olá capacidade toouse com base no Gerenciador de recursos do Azure PowerShell comandos toomanage do serviço de aplicativo.

toolearn sobre o gerenciamento de grupos de recursos, consulte [usar toomanage de CLI do Azure hello Azure recursos e grupos de recursos](../azure-resource-manager/xplat-cli-azure-resource-manager.md). 

> [!NOTE] 
> Além disso, experimente [2.0 do CLI do Azure](https://github.com/Azure/azure-cli), uma CLI de última geração escritos em Python para o modelo de implantação do gerenciamento de recursos de saudação.
>
>

## <a name="managing-app-service-plans"></a>Gerenciando Planos do Serviço de Aplicativo
### <a name="create-an-app-service-plan"></a>Criar um Plano do Serviço de Aplicativo
toocreate um plano de serviço de aplicativo, use Olá **appserviceplan azure criar** comando.

Seguem as descrições dos parâmetros diferentes hello:

* **-grupo de recursos**: grupo de recursos que inclui o plano de serviço de aplicativo hello recém-criado.
* **-nome**: nome do plano de serviço de aplicativo hello.
* **--location**: a localização do plano do serviço de aplicativo.
* **– sku**: Olá desejado preços sku (Olá opções são: F1 (Free). D1 (Compartilhado). B1 (Básico Breve), B2 (Básico Médio) e B3 (Básico Prolongado). S1 (Standard Breve), S2 (Standard Médio) e S3 (Standard Prolongado). P1 (Premium Breve), P2 (Premium Médio) e P3 (Premium Prolongado)).
* **-instâncias**: Olá número de trabalhadores no plano de serviço de aplicativo hello (o valor padrão é 1).

Exemplo toouse esse cmdlet:

    azure appserviceplan create --name ContosoAppServicePlan --location "South Central US" --resource-group ContosoAzureResourceGroup --sku P1 --instances 10

#### <a name="create-a-linux-app-service-plan"></a>Criar um Plano do Serviço de Aplicativo do Linux

Usando Olá mesmo **appserviceplan azure criar** comando com hello parâmetro extra **true - islinux**. Observe as restrições de saudação e regiões descritos no [Introdução tooApp serviço no Linux](app-service-linux-intro.md)

### <a name="list-existing-app-service-plans"></a>Listar os Planos do Serviço de Aplicativo existentes
toolist Olá existente aplicativo planos de serviço, use **appserviceplan do azure lista** comando.

toolist todos os planos de serviço de aplicativo em um grupo de recursos específico, use:

    azure appserviceplan list --resource-group ContosoAzureResourceGroup

tooget um plano de serviço de aplicativo específico, use **appserviceplan azure Mostrar** comando:

    azure appserviceplan show --name ContosoAppServicePlan --resource-group southeastasia

### <a name="configure-an-existing-app-service-plan"></a>Configurar um Plano do Serviço de Aplicativo existente
configurações de saudação toochange para um plano de serviço de aplicativo existente, use Olá **appserviceplan azure config** comando. Você pode alterar Olá sku e o número de trabalhos Olá 

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1 --instances 9

#### <a name="scaling-an-app-service-plan"></a>Dimensionando um Plano do Serviço de Aplicativo
tooscale um aplicativo de serviço de plano existente, use:

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --instances 9

#### <a name="changing-hello-sku-of-an-app-service-plan"></a>Alterando Olá SKU de um plano de serviço de aplicativo
sku de saudação toochange de um aplicativo de serviço plano existente, use:

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1


### <a name="delete-an-existing-app-service-plan"></a>Excluir um Plano do Serviço de Aplicativo existente
toodelete um plano de serviço de aplicativo existente, todos os atribuídos aplicativos necessidade toobe movido ou excluído primeiro. Usando o hello **webapp azure excluir** comando você pode excluir o plano de serviço de aplicativo hello.

    azure appserviceplan delete --name ContosoAppServicePlan --resource-group southeastasia

## <a name="managing-app-service-apps"></a>Gerenciando aplicativos do Serviço de Aplicativo
### <a name="create-a-web-app"></a>Criar um aplicativo Web
toocreate um aplicativo web, use Olá **webapp azure criar** comando.

Seguem as descrições dos parâmetros diferentes hello:

* **-nome**: nome do aplicativo web de saudação.
* **-plano**: nome do plano de serviço Olá usado toohost Olá web app.
* **-grupo de recursos**: grupo de recursos que hospeda o plano de serviço de aplicativo hello.
* **– local**: Olá local do aplicativo web.

Exemplo toouse esse cmdlet:

    azure webapp create --name ContosoWebApp --resource-group ContosoAzureResourceGroup --plan ContosoAppServicePlan --location "South Central US"

### <a name="delete-an-existing-app"></a>Excluir um aplicativo existente
toodelete um aplicativo existente, você pode usar o hello **webapp azure excluir** comando. Você precisará toospecify nome de saudação do aplicativo hello e o nome do grupo de recursos de saudação.

    azure webapp delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="list-existing-apps"></a>Listar aplicativos existentes
toolist Olá os aplicativos existentes, use Olá **webapp do azure lista** comando.

toolist todos os aplicativos em um grupo de recursos específico, use:

    azure webapp list --resource-group ContosoAzureResourceGroup

tooget um aplicativo específico, use Olá **webapp azure Mostrar** comando.

    azure webapp show --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="configure-an-existing-app"></a>Configurar um aplicativo existente
configurações de saudação do toochange e as configurações para um aplicativo existente, use Olá **conjunto de configuração de aplicativo Web do azure** comando.

Exemplo (1): alterar a versão do php Olá de um aplicativo 

    azure webapp config set --name ContosoWebApp --resource-group ContosoAzureResourceGroup --phpversion 5.6

Exemplo (2): adicionar ou alterar as configurações do aplicativo

    webapp config appsettings set --name ContosoWebApp --resource-group ContosoAzureResourceGroup appsetting1=appsetting1value,appsetting2=appsetting2value

tooknow outras configurações que podem ser alteradas, use Olá **-h do conjunto de configuração de aplicativo Web do azure** comando.

### <a name="change-hello-state-of-an-existing-app"></a>Alterar o estado de saudação de um aplicativo existente
#### <a name="restart-an-app"></a>Reiniciar um aplicativo
toorestart um aplicativo, você deve especificar Olá nome e grupo de recursos do aplicativo hello.

    azure webapp restart --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="stop-an-app"></a>Interromper um aplicativo
toostop um aplicativo, você deve especificar Olá nome e grupo de recursos do aplicativo hello.

    azure webapp stop --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="start-an-app"></a>Iniciar um aplicativo
toostart um aplicativo, você deve especificar Olá nome e grupo de recursos do aplicativo hello.

    azure webapp start --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="manage-publishing-profiles-of-an-app"></a>Gerenciar perfis de publicação de um aplicativo
Cada aplicativo tem um perfil de publicação que pode ser usado toopublish seu código.

#### <a name="get-publishing-profile"></a>Obter o perfil de publicação
Olá tooget perfil para um aplicativo, o uso de publicação:

    azure webapp publishingprofile --name ContosoWebApp --resource-group ContosoAzureResourceGroup

Este comando exibe o saudação de linha de comando de toohello de nome de usuário e senha de perfil de publicação.

### <a name="manage-app-hostnames"></a>Gerenciar nomes do host de aplicativo
toomanage associações de nome de host para seu aplicativo, use Olá **nomes de host do aplicativo Web do azure config** comando  

#### <a name="list-hostname-bindings"></a>Listar associações de nome de host
tooget Olá atual associações de nome de host para um aplicativo usar:

    azure webapp config hostnames list --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="add-hostname-bindings"></a>Adicionar associações de nome de host
aplicativo de tooan de associações de hostname tooadd, use:

    azure webapp config hostnames add --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

#### <a name="delete-hostname-bindings"></a>Excluir associações de nome de host
associações de hostname toodelete, use:

    azure webapp config hostnames delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

## <a name="next-steps"></a>Próximas etapas
* toolearn sobre o suporte a CLI do Azure Resource Manager, consulte [usar toomanage de CLI do Azure hello Azure recursos e grupos de recursos.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)
* toolearn sobre o gerenciamento de serviço de aplicativo usando o PowerShell, consulte [tooManage Using Azure Resource Manager-Based PowerShell aplicativos Web do Azure.](app-service-web-app-azure-resource-manager-powershell.md)
* toolearn sobre o serviço de aplicativo do Azure no Linux, consulte [tooApp Introdução serviço no Linux](app-service-linux-intro.md)
