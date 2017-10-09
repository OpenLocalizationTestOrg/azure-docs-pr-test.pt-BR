---
title: "exemplos de início rápido aaaAzure Monitor CLI 1.0. | Microsoft Docs"
description: "Comandos de exemplo da CLI 1.0 para recursos do Azure Monitor. Monitor do Azure é um serviço do Microsoft Azure que permite que as notificações de alerta de toosend, chamada web URLs com base nos valores de dados de telemetria configurado e os serviços de nuvem de dimensionamento automático, máquinas virtuais e aplicativos Web."
author: kamathashwin
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 1653aa81-0ee6-4622-9c65-d4801ed9006f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: ashwink
ms.openlocfilehash: 6cd9cd62b3a1977276563f5e43f5384ccca66247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor--cross-platform-cli-10-quick-start-samples"></a>Exemplos de início rápido da CLI 1.0 de plataforma cruzada do Azure Monitor
Este mostra artigo exemplo toohelp de comandos de interface de linha de comando (CLI) você acessar os recursos do Monitor do Azure. Monitor do Azure permite que notificações de alerta serviços de nuvem, máquinas virtuais e aplicativos Web e toosend tooAutoScale ou chamada web URLs com base nos valores de dados de telemetria configurado.

> [!NOTE]
> Monitor do Azure é Olá novo nome para o que era chamado de "Azure Insights" até 25 de setembro de 2016. No entanto, Olá namespaces e, portanto, comandos de saudação abaixo ainda contêm insights"Olá".
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
Se você ainda não instalou Olá CLI do Azure, consulte [instalação Olá CLI do Azure](../cli-install-nodejs.md). Se você estiver familiarizado com a CLI do Azure, você pode ler mais sobre ele no [Olá Use CLI do Azure para Mac, Linux e Windows com o Azure Resource Manager](../xplat-cli-azure-resource-manager.md).

No Windows, instale o npm de saudação [site Node.js](https://nodejs.org/). Depois de concluir a instalação Olá, usando CMD.exe com privilégios de executar como administrador, execute o seguinte Olá da pasta Olá onde npm está instalado:

```console
npm install azure-cli --global
```

Em seguida, navegue até os local da pasta tooany e digite a saudação de linha de comando:

```console
azure help
```

## <a name="log-in-tooazure"></a>Faça logon no tooAzure
Olá primeira etapa é toologin tooyour conta do Azure.

```console
azure login
```

Depois de executar esse comando, você tem toosign via instruções Olá na tela hello. Posteriormente, você verá sua Conta, sua TenantId e sua ID da Assinatura padrão. Todos os comandos funcionam no contexto de saudação da sua assinatura padrão.

detalhes de saudação toolist de sua assinatura atual, use Olá comando a seguir.

```console
azure account show
```

toochange trabalho contexto tooa assinatura diferente, use Olá comando a seguir.

```console
azure account set "subscription ID or subscription name"
```

toouse Gerenciador de recursos do Azure e o Monitor do Azure os comandos, você precisa toobe no modo do Gerenciador de recursos do Azure.

```console
azure config mode arm
```

tooview uma lista de todos os comandos com suporte do Monitor do Azure, execute o seguinte hello.

```console
azure insights
```

## <a name="view-activity-log-for-a-subscription"></a>Exibir o log de atividade para uma assinatura
tooview uma lista de eventos do log de atividade, execute o seguinte Olá.

```console
azure insights logs list [options]
```

Tente Olá tooview a seguir todas as opções disponíveis.

```console
azure insights logs list -help
```

Aqui está um exemplo logs toolist por um grupo de recursos

```console
azure insights logs list --resourceGroup "myrg1"
```

Logs do exemplo toolist pelo chamador

```console
azure insights logs list --caller "myname@company.com"
```

Logs do exemplo toolist pelo chamador em um tipo de recurso, dentro de uma data de início e término

```console
azure insights logs list --resourceProvider "Microsoft.Web" --caller "myname@company.com" --startTime 2016-03-08T00:00:00Z --endTime 2016-03-16T00:00:00Z
```

## <a name="work-with-alerts"></a>Trabalhar com alertas
Você pode usar informações de Olá Olá seção toowork com alertas.

### <a name="get-alert-rules-in-a-resource-group"></a>Obter regras de alerta em um grupo de recursos
```console
azure insights alerts rule list abhingrgtest123
azure insights alerts rule list abhingrgtest123 --ruleName andy0323
```

### <a name="create-a-metric-alert-rule"></a>Criar uma regra de alerta de métrica
```console
azure insights alerts actions email create --customEmails foo@microsoft.com
azure insights alerts actions webhook create https://someuri.com
azure insights alerts rule metric set andy0323 eastus abhingrgtest123 PT5M GreaterThan 2 /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Web-EastUS/providers/Microsoft.Web/serverfarms/Default1 BytesReceived Total
```

### <a name="create-webtest-alert-rule"></a>Criar uma regra de alerta de teste na Web
```console
azure insights alerts rule webtest set leowebtestr1-webtestr1 eastus Default-Web-WestUS PT5M 1 GSMT_AvRaw /subscriptions/b67f7fec-69fc-4974-9099-a26bd6ffeda3/resourcegroups/Default-Web-WestUS/providers/microsoft.insights/webtests/leowebtestr1-webtestr1
```

### <a name="delete-an-alert-rule"></a>Excluir uma regra de alerta
```console
azure insights alerts rule delete abhingrgtest123 andy0323
```

## <a name="log-profiles"></a>Perfis de log
Use as informações de saudação toowork essa seção com perfis de log.

### <a name="get-a-log-profile"></a>Obter um perfil de log
```console
azure insights logprofile list
azure insights logprofile get -n default
```


### <a name="add-a-log-profile-without-retention"></a>Adicionar um perfil de log sem retenção
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a>Remover um perfil de log
```console
azure insights logprofile delete --name default
```

### <a name="add-a-log-profile-with-retention"></a>Adicionar um perfil de log com retenção
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```

### <a name="add-a-log-profile-with-retention-and-eventhub"></a>Adicionar um perfil de log com retenção e Hub de Eventos
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --serviceBusRuleId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/testshoeboxeastus/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```


## <a name="diagnostics"></a>Diagnostics
Use as informações de saudação toowork essa seção com as configurações de diagnóstico.

### <a name="get-a-diagnostic-setting"></a>Obter uma configuração de diagnóstico
```console
azure insights diagnostic get --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp
```

### <a name="disable-a-diagnostic-setting"></a>Desabilitar uma configuração de diagnóstico
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled false
```

### <a name="enable-a-diagnostic-setting-without-retention"></a>Habilitar uma configuração de diagnóstico sem retenção
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled true
```


## <a name="autoscale"></a>Autoscale
Use as informações de saudação toowork essa seção com configurações de dimensionamento automático. É necessário toomodify esses exemplos.

### <a name="get-autoscale-settings-for-a-resource-group"></a>Obter configurações de dimensionamento automático para um grupo de recursos
```console
azure insights autoscale setting list montest2
```

### <a name="get-autoscale-settings-by-name-in-a-resource-group"></a>Obter configurações de dimensionamento automático por nome em um grupo de recursos
```console
azure insights autoscale setting list montest2 -n setting2
```


### <a name="set-auotoscale-settings"></a>Definir as configurações de dimensionamento automático
```console
azure insights autoscale setting set montest2 -n setting2 --settingSpec
```
