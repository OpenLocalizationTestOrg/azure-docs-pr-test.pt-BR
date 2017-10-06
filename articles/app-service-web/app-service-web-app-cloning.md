---
title: aaaWeb aplicativo clonagem usando o PowerShell
description: Saiba como tooclone seus aplicativos Web de toonew de aplicativos Web usando o PowerShell.
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: f9a5cfa1-fbb0-41e6-95d1-75d457347a35
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: aelnably
ms.openlocfilehash: b8882370d6db6939f8e4473ccc1414091bdcb8f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-app-cloning-using-powershell"></a>Clonagem de aplicativo do Serviço de Aplicativo do Azure usando o Azure PowerShell
Com a versão de saudação do Microsoft Azure PowerShell versão 1.1.0 uma nova opção foi adicionada AzureRMWebApp tooNew que daria Olá usuário Olá capacidade tooclone um aplicativo existente do aplicativo Web tooa recentemente criado em uma região diferente ou em Olá mesma região. Isso permitirá que os clientes toodeploy um número de aplicativos em regiões diferentes rapidamente e facilmente.

A clonagem de aplicativo atualmente só tem suporte para planos de serviço de aplicativos de camada Premium. novos usos de recurso Olá Olá mesmo limitações de recurso de Backup de aplicativos da Web, consulte [backup de um aplicativo web no serviço de aplicativo do Azure](web-sites-backup.md).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

toolearn sobre como usar o Gerenciador de recursos do Azure com base em toomanage de cmdlets do PowerShell do Azure sua seleção de aplicativos Web [Gerenciador de recursos do Azure com base em comandos do PowerShell para o aplicativo Web do Azure](app-service-web-app-azure-resource-manager-powershell.md)

## <a name="cloning-an-existing-app"></a>Clonagem de um aplicativo existente
Cenário: Um aplicativo web existente na região Centro Sul dos EUA, usuário Olá gostariam tooclone Olá conteúdo tooa novo aplicativo web na região Norte Central dos EUA. Isso pode ser feito com a versão de Gerenciador de recursos do Azure de saudação do hello PowerShell cmdlet toocreate um novo aplicativo web com a opção de SourceWebApp - Olá.

Conhecer os recursos de saudação nome do grupo que contém o aplicativo de web de origem hello, podemos usar Olá informações PowerShell comando tooget Olá fonte do aplicativo web (nesse caso chamadas webapp fonte) a seguir:

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

toocreate um novo plano de serviço de aplicativo, podemos usar o comando New-AzureRmAppServicePlan como no exemplo a seguir de saudação

    New-AzureRmAppServicePlan -Location "South Central US" -ResourceGroupName DestinationAzureResourceGroup -Name NewAppServicePlan -Tier Premium

Usando o comando Olá AzureRmWebApp novo, podemos criar novo aplicativo web e Olá na região do hello Centro Norte dos EUA e anexá-la de camada premium existente tooan plano do serviço de aplicativo, além disso, podemos usar Olá mesmo recurso de grupo como o aplicativo de web de origem hello ou definir um novo grupo de recursos , a seguir Olá demonstra que:

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp

tooclone um aplicativo web existente, incluindo todos os slots de implantação associado, o usuário Olá precisará toouse Olá parâmetro IncludeSourceWebAppSlots, Olá comando PowerShell a seguir demonstra o uso de saudação desse parâmetro com hello AzureRmWebApp novo comando:

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -IncludeSourceWebAppSlots

tooclone um aplicativo web existente no hello mesma região, Olá usuário deverá toocreate plano de um novo grupo de recursos e um novo serviço de aplicativo no Olá Olá a mesma região e, em seguida, usando seguinte aplicativo web do PowerShell comando tooclone Olá

    $destapp = New-AzureRmWebApp -ResourceGroupName NewAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan NewAppServicePlan -SourceWebApp $srcap

## <a name="cloning-an-existing-app-tooan-app-service-environment"></a>Clonagem de um tooan de aplicativo ambiente de serviço de aplicativo existente
Cenário: Um aplicativo web existente na região Centro Sul dos EUA, Olá usuário quer tooclone Olá conteúdo tooa nova web aplicativo tooan existente do ambiente de serviço de aplicativo (ASE).

Conhecer os recursos de saudação nome do grupo que contém o aplicativo de web de origem hello, podemos usar Olá informações PowerShell comando tooget Olá fonte do aplicativo web (nesse caso chamadas webapp fonte) a seguir:

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

Saber o nome e nome do grupo de recursos de Olá Olá ASE pertence a saudação do ASE, usuário Olá pode usar o comando Olá novo AzureRmWebApp toocreate Olá novo aplicativo web de saudação existente ASE, Olá a seguir demonstra que:

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -ASEName DestinationASE -ASEResourceGroupName DestinationASEResourceGroupName -SourceWebApp $srcapp

parâmetro de local de saudação é necessário devido a motivo toolegacy, mas no caso de saudação de criação de um aplicativo em uma ASE será ignorado. 

## <a name="cloning-an-existing-app-slot"></a>Clonagem de um slot de aplicativo existente
Cenário: usuário Olá deseja tooclone um tooeither de Slot do aplicativo Web um novo aplicativo Web existente ou um novo slot do aplicativo Web. Olá novo aplicativo Web pode estar em Olá mesma região, como o slot de aplicativo Web original hello, ou em uma região diferente.

Conhecer os recursos de saudação nome do grupo que contém o aplicativo de web de origem hello, podemos usar Olá informações do slot do aplicativo web fonte tooget hello (nesse caso denominadas fonte webappslot) vinculado tooWeb aplicativo origem-webapp de comando do PowerShell a seguir:

    $srcappslot = Get-AzureRmWebAppSlot -ResourceGroupName SourceAzureResourceGroup -Name source-webapp -Slot source-webappslot

a seguir Olá demonstra como criar um clone de Olá web aplicativo tooa novo aplicativo web de origem:

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcappslot

## <a name="configuring-traffic-manager-while-cloning-a-app"></a>Configuração do Gerenciador de Tráfego durante a clonagem de um aplicativo
Criar aplicativos web de várias regiões e configurar o Azure Traffic Manager tooroute tráfego tooall esses aplicativos web, é um tooinsure n cenário importante que aplicativos clientes são altamente disponíveis, quando um aplicativo web existente, você tem a clonagem Olá opção tooconnect ambas as web aplicativos tooeither um perfil do Gerenciador de tráfego novo ou existente - Observe essa versão do Azure Resource Manager somente há suporte ao Gerenciador de tráfego.

### <a name="creating-a-new-traffic-manager-profile-while-cloning-a-app"></a>Criando um novo perfil do Gerenciador de Tráfego durante a clonagem de um aplicativo
Cenário: usuário Olá que tooclone uma região de tooanother do aplicativo web, ao configurar um perfil do Gerenciador de tráfego do Azure Resource Manager que incluem os dois aplicativos da web. a seguir Olá demonstra como criar um clone de Olá web aplicativo tooa novo aplicativo web de origem ao configurar um novo perfil do Gerenciador de tráfego:

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileName newTrafficManagerProfile

### <a name="adding-new-cloned-web-app-tooan-existing-traffic-manager-profile"></a>Adicionando novo clonado aplicativo Web tooan existente perfil do Traffic Manager
Cenário: usuário Olá já tiver um perfil do Gerenciador de tráfego do Azure Resource Manager que ele quer tooadd web apps como pontos de extremidade. toodo assim, é preciso primeiro tooassemble Olá id de perfil de Gerenciador de tráfego existente, precisaremos id da assinatura Olá, nome do grupo de recursos e Olá traffic manager nome do perfil existente.

    $TMProfileID = "/subscriptions/<Your subscription ID goes here>/resourceGroups/<Your resource group name goes here>/providers/Microsoft.TrafficManagerProfiles/ExistingTrafficManagerProfileName"

Depois de ter o id do Gerenciador de tráfego hello, seguinte Olá demonstra como criar um clone de Olá web aplicativo tooa novo aplicativo web de origem ao adicioná-los tooan perfil existente do Gerenciador de tráfego:

    $destapp = New-AzureRmWebApp -ResourceGroupName <Resource group name> -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileId $TMProfileID

## <a name="current-restrictions"></a>Restrições atuais
Este recurso está atualmente em visualização, estamos trabalhando tooadd novos recursos ao longo do tempo, Olá lista a seguir são Olá restrições conhecidas na versão atual de saudação de clonagem do aplicativo:

* As configurações de escala automática não são clonadas
* As configurações de agendamento de backup não são clonadas.
* As configurações da rede virtual não são clonadas
* Ideias de aplicativo não são automaticamente definidas no aplicativo de web de destino Olá
* As configurações de Autenticação Fácil não são clonadas
* A extensão Kudu não é clonada
* As regras de TiP não são clonadas
* O conteúdo do banco de dados não é clonado

### <a name="references"></a>Referências
* [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)
* [Clonagem de Aplicativo Web usando o Portal do Azure](app-service-web-app-cloning-portal.md)
* [Fazer backup de um aplicativo Web no Serviço de Aplicativo do Azure](web-sites-backup.md)
* [Suporte do Azure Resource Manager para Visualização do Gerenciador de Tráfego do Azure](../traffic-manager/traffic-manager-powershell-arm.md)
* [Introdução tooApp ambiente de serviço](app-service-app-service-environment-intro.md)
* [Usando o Azure PowerShell com o Gerenciador de Recursos do Azure](../powershell-azure-resource-manager.md)

