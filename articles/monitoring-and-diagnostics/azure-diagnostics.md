---
title: "aaaOverview do diagnóstico do Azure | Microsoft Docs"
description: "Usar o diagnóstico do Azure para depurar, medir o desempenho, monitorar e analisar o tráfego em serviços de nuvem, em máquinas virtuais e no Service Fabric"
services: multiple
documentationcenter: .net
author: rboucher
manager: 
editor: 
ms.assetid: baad40d8-c915-4f93-b486-8b160bf33463
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/18/2017
ms.author: robb
ms.openlocfilehash: 2a03a96a37091894d7ab16120c125116e4bf462a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-diagnostics"></a>O que é o Diagnóstico do Azure
Diagnóstico do Azure é a capacidade de saudação dentro do Azure que habilita a coleta de saudação de dados de diagnóstico em um aplicativo implantado. Você pode usar a extensão de diagnóstico de saudação de um número de fontes diferentes. As que têm suporte no momento são as Funções de Trabalho ou Web do Serviço de Nuvem, as Máquinas Virtuais do Azure que executam o Microsoft Windows e o Service Fabric. Outros serviços do Azure têm seu próprios diagnósticos separados.

## <a name="data-you-can-collect"></a>Dados que você pode coletar
Diagnóstico do Azure pode coletar Olá tipos de dados a seguir:

| Fonte de dados | Descrição |
| --- | --- |
| Contadores de desempenho |Contadores de desempenho personalizados e do Sistema Operacional |
| Logs de aplicativo |Rastreio de mensagens gravadas pelo seu aplicativo |
| Logs de Eventos do Windows |Informações enviadas do sistema de log de eventos do Windows toohello |
| Fonte de evento do .NET |Código de gravação de eventos usando o .NET Olá [EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) classe |
| Logs IIS |Informações sobre sites do IIS |
| Manifesto com base no ETW |Rastreamento de Eventos para eventos do Windows gerados por qualquer processo |
| Despejos de falhas |Informações sobre o estado de saudação do processo de saudação no evento de saudação de uma falha de aplicativo |
| Logs de erros personalizados |Logs criados por seu aplicativo ou serviço |
| Logs de infraestrutura do Diagnóstico do Azure |Informações sobre o próprio Diagnóstico |

Olá extensão de diagnóstico do Azure pode transferir esse tooan dados conta de armazenamento do Azure ou enviá-lo tooservices como [Application Insights](../application-insights/app-insights-cloudservices.md). Você pode usar dados de saudação para depuração e solução de problemas, medir o desempenho, o uso de recursos, análise de tráfego e planejamento de capacidade de monitoramento e auditoria.

## <a name="versioning"></a>Controle de versão
Veja [Histórico de versão do Diagnóstico do Azure](azure-diagnostics-versioning-history.md).

## <a name="next-steps"></a>Próximas etapas
Escolha quais serviços você está tentando toocollect diagnóstico e use Olá artigos tooget iniciado a seguir. Use links de diagnóstico do Azure gerais Olá para referência para tarefas específicas.

## <a name="web-apps"></a>Aplicativos Web
Observe que os aplicativos Web não usam o Diagnóstico do Azure. Encontrar informações de saudação equivalente em [aplicativos Web](../app-service-web/web-sites-enable-diagnostic-log.md)

## <a name="cloud-services-using-azure-diagnostics"></a>Serviços de Nuvem que usam o Diagnóstico do Azure
* Se usar o Visual Studio, consulte [tootrace Use o Visual Studio um aplicativo de serviços de nuvem](../vs-azure-tools-debug-cloud-services-virtual-machines.md) tooget iniciado. Caso contrário, veja
* [Como toomonitor nuvem services usando o diagnóstico do Azure](../cloud-services/cloud-services-how-to-monitor.md)
* [Configurar o Diagnóstico do Azure em um Aplicativo dos Serviços de Nuvem](../cloud-services/cloud-services-dotnet-diagnostics.md)

Para tópicos mais avançados, veja

* [Uso dos Diagnósticos do Azure com o Application Insights para Serviços de Nuvem](../application-insights/app-insights-cloudservices.md)
* [Fluxo de saudação do rastreamento de um aplicativo de serviços de nuvem com o diagnóstico do Azure](../cloud-services/cloud-services-dotnet-diagnostics-trace-flow.md)
* [Use o PowerShell tooset o diagnóstico nos serviços de nuvem](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="virtual-machines-using-azure-diagnostics"></a>Máquinas Virtuais que usam o Diagnóstico do Azure
* Se usar o Visual Studio, consulte [tootrace Use o Visual Studio máquinas virtuais do Azure](../vs-azure-tools-debug-cloud-services-virtual-machines.md) tooget iniciado. Caso contrário, veja
* [Configurar o Diagnóstico do Azure em uma Máquina Virtual do Azure](../virtual-machines-dotnet-diagnostics.md)

Para tópicos mais avançados, veja

* [Use o PowerShell tooset o diagnóstico em máquinas virtuais do Azure](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Criar uma máquina virtual do Windows com monitoramento e diagnóstico usando o modelo do Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="service-fabric-using-azure-diagnostics"></a>Service Fabric que usa o Diagnóstico do Azure
Comece em [Monitorar um aplicativo do Service Fabric](../service-fabric/service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md). Muitos outros artigos de diagnóstico do Service Fabric estão disponíveis na árvore de navegação Olá Olá restantes depois de obter toothis artigo.

## <a name="general-azure-diagnostics-articles"></a>Artigos gerais sobre o Diagnóstico do Azure
* [Configuração de esquema de diagnóstico do Azure](https://msdn.microsoft.com/library/azure/mt634524.aspx) - Saiba como toochange Olá toocollect do arquivo de esquema e dados de diagnóstico de rota. Observe que você também pode usar o arquivo de esquema do Visual Studio toochange hello.
* [Como os dados de diagnóstico do Azure são armazenados no armazenamento do Azure](../cloud-services/cloud-services-dotnet-diagnostics-storage.md) -conhecer os nomes de saudação de tabelas de saudação e blobs em que os dados de diagnóstico de saudação são gravados.
* Aprender muito[usar contadores de desempenho no diagnóstico do Azure](../cloud-services/cloud-services-dotnet-diagnostics-performance-counters.md).
* Aprender muito[tooApplication informações de diagnóstico do Azure de rota Insights](azure-diagnostics-configure-application-insights.md)
* Se você tiver problemas com o início do diagnóstico ou com a localização de seus dados nas tabelas do Armazenamento do Azure, veja [Solução de Problemas do Diagnóstico do Azure](azure-diagnostics-troubleshooting.md)
