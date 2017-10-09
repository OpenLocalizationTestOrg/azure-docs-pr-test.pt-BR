---
title: "aaaLog recursos de análise para provedores de serviços | Microsoft Docs"
description: "O Log Analytics pode ajudar provedores de serviços gerenciados (MSPs), grandes empresas, fornecedores de software independentes (ISVs) e provedores de serviço de hospedagem a gerenciar e monitorar servidores no local do cliente ou na infraestrutura de nuvem."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: c07f0b9f-ec37-480d-91ec-d9bcf6786464
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/22/2016
ms.author: richrund
ms.openlocfilehash: 3c0a93232293f90385c6c724be436cee1cf855f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-features-for-service-providers"></a>Recursos do Log Analytics para provedores de serviços
O Log Analytics pode ajudar provedores de serviços gerenciados (MSPs), grandes empresas, fornecedores de software independentes (ISVs) e provedores de serviço de hospedagem a gerenciar e monitorar servidores no local do cliente ou na infraestrutura de nuvem. 

Grandes empresas compartilham várias semelhanças com provedores de serviços, especialmente quando há uma equipe de TI centralizada que é responsável por gerenciar a TI para muitas unidades de negócios diferentes. Para simplificar, este documento usa o termo Olá *provedor* mas hello mesma funcionalidade também está disponível para as empresas e outros clientes.

## <a name="cloud-solution-provider"></a>Provedor de soluções de nuvem
Para parceiros e provedores de serviços que fazem parte da saudação [provedor de solução de nuvem (CSP)](https://partner.microsoft.com/Solutions/cloud-reseller-overview) de programa, análise de Log é uma saudação em serviços do Azure disponíveis em uma assinatura do CSP. 

Para análise de Log, Olá recursos a seguir está habilitado no *provedor de soluções de nuvem* assinaturas.

Como um *Provedor de Soluções de Nuvem*, você pode:

* Criar espaços de trabalho do Log Analytics na assinatura de um locatário (do cliente).
* Acessar espaços de trabalho criados por locatários. 
* Adicionar e remover usuário acesso toohello espaço de trabalho usando o gerenciamento de usuário do Azure. Quando página de gerenciamento de usuário Olá portal em configurações não está disponível no espaço de trabalho do locatário Olá OMS
  * Análise de logs não oferece suporte a acesso baseado em função ainda - fornecendo um usuário `reader` permissão no hello portal do Azure permitirá toomake alterações de configuração no portal do OMS Olá

toolog na tooa assinatura de locatário, você precisa de identificador do locatário Olá toospecify. Identificador do locatário Olá costuma essa última parte da saudação email endereço usado toosign no.

* No portal do OMS hello, adicionar `?tenant=contoso.com` Olá URL para o portal de saudação. Por exemplo, `mms.microsoft.com/?tenant=contoso.com`
* No PowerShell, use Olá `-Tenant contoso.com` parâmetro ao usar `Add-AzureRmAccount` cmdlet
* Identificador do locatário Olá é adicionada automaticamente quando você usar o hello `OMS portal` link do hello tooopen portal do Azure e faça logon no portal do OMS toohello de espaço de trabalho de saudação selecionado

Como um *cliente* de um Provedor de soluções de nuvem, você pode:

* Criar espaços de trabalho do Log Analytics em uma assinatura de CSP
* Espaços de trabalho de acesso criados pelo Olá CSP
  * Saudação de uso `OMS portal` link do hello tooopen portal do Azure e faça logon no portal do OMS toohello de espaço de trabalho de saudação selecionado
* Exibir e usar a página de gerenciamento de usuário Olá em configurações no portal do OMS Olá

> [!NOTE]
> Olá incluídos Backup e soluções de recuperação de Site para análise de Log não tooconnect capaz de Cofre de serviços de recuperação de tooa e não podem ser configuradas em uma assinatura do CSP. 
> 
> 

## <a name="managing-multiple-customers-using-log-analytics"></a>Gerenciando vários clientes usando o Log Analytics
É recomendável que você crie um espaço de trabalho do Log Analytics para cada cliente que você gerencia. Um espaço de trabalho do Log Analytics fornece:

* Uma localização geográfica para toobe dados armazenado. 
* Granularidade de cobrança 
* Isolamento dos dados 
* Configuração exclusiva

Ao criar um espaço de trabalho por cliente, você está tookeep capaz de dados de cada cliente separados e também controlar o uso de saudação de cada cliente.

Mais detalhes sobre quando e por que toocreate vários espaços de trabalho descrito [gerenciar acesso toolog análise](log-analytics-manage-access.md#determine-the-number-of-workspaces-you-need).

Criação e configuração de espaços de trabalho do cliente podem ser automatizados usando [PowerShell](log-analytics-powershell-workspace-configuration.md), [modelos do Gerenciador de recursos](log-analytics-template-workspace-configuration.md), ou usando Olá [API REST](https://www.nuget.org/packages/Microsoft.Azure.Management.OperationalInsights/).

uso de saudação de modelos do Gerenciador de recursos para a configuração do espaço de trabalho permite que você toohave uma configuração mestre que pode ser usado toocreate e configurar espaços de trabalho. Você pode ter certeza de que, como espaços de trabalho são criados para os clientes são automaticamente configurado tooyour requisitos. Quando você atualiza seus requisitos, o modelo de saudação é atualizado e reaplicadas, em seguida, espaços de trabalho existentes hello. Esse processo garante que até mesmo os espaços de trabalho existentes atendem aos novos padrões.    

Ao gerenciar vários espaços de trabalho de análise de Log, recomendamos a integração de cada espaço de trabalho com o sistema de emissão de tíquetes existente / console de operações usando Olá [alertas](log-analytics-alerts.md) funcionalidade. Integrando-se aos sistemas existentes, a equipe de suporte pode continuar toofollow seus processos familiares. Análise de log regularmente verifica cada espaço de trabalho com os critérios de alerta de saudação especificado e gera um alerta quando a ação é necessária.

Para exibições personalizadas de dados, use Olá [painel](../azure-portal/azure-portal-dashboards.md) recurso Olá portal do Azure.  

Para os executivos relatórios que resumem os dados em espaços de trabalho que você pode usar Olá integração entre o Log de análise e [PowerBI](log-analytics-powerbi.md). Se você precisar toointegrate com outro sistema de emissão de relatórios, você pode usar o hello API de pesquisa (por meio do PowerShell ou [REST](log-analytics-log-search-api.md)) toorun consultas e exportar resultados da pesquisa.

## <a name="next-steps"></a>Próximas etapas
* Automatizar a criação e configuração de espaços de trabalho usando [modelos do Gerenciador de recursos](log-analytics-template-workspace-configuration.md)
* Automatizar a criação de espaços de trabalho usando o [PowerShell](log-analytics-powershell-workspace-configuration.md) 
* Use [alertas](log-analytics-alerts.md) toointegrate com sistemas existentes
* Gerar relatórios de resumo usando o [Power BI](log-analytics-powerbi.md)

