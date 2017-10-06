---
title: "aaaBuild uma solução de gerenciamento do OMS | Microsoft Docs"
description: "Soluções de gerenciamento de estendem a funcionalidade de saudação do Operations Management Suite (OMS), fornecendo os cenários de pacotes de gerenciamento que os clientes podem adicionar tootheir espaço de trabalho do OMS.  Este artigo fornece detalhes sobre como você pode criar toobe de soluções de gerenciamento usados em seu próprio ambiente ou feitas clientes tooyour disponíveis."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1915e204-ba7e-431b-9718-9eb6b4213ad8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/20/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: dea4c0d9e608d9fe4aa41088705958c9fe999372
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="design-and-build-a-management-solution-in-operations-management-suite-oms-preview"></a>Projetar e compilar uma solução de gerenciamento no OMS (Operations Management Suite) (Visualização)
> [!NOTE]
> Esta é uma documentação preliminar para criar soluções de gerenciamento no OMS, que estão atualmente em visualização. Qualquer esquema descrita abaixo é toochange de assunto.

[Soluções de gerenciamento](operations-management-suite-solutions.md) estender a funcionalidade de saudação do OMS Operations Management Suite (), fornecendo os cenários de pacotes de gerenciamento que os clientes podem adicionar tootheir espaço de trabalho do OMS.  Este artigo apresenta um processo básico toodesign e criar uma solução de gerenciamento que é adequada para os requisitos mais comuns.  Se você estiver novas soluções de gerenciamento de toobuilding, você poderá usar esse processo como um ponto de partida e, em seguida, aproveitar conceitos Olá soluções mais complexas, como a evolução das exigências.

## <a name="what-is-a-management-solution"></a>O que é uma solução de gerenciamento?

Soluções de gerenciamento contêm OMS e recursos do Azure que funcionam em conjunto tooachieve um determinado cenário de monitoramento.  Eles são implementados como [modelos de gerenciamento de recursos](../azure-resource-manager/resource-manager-template-walkthrough.md) que contêm detalhes de como tooinstall e configurar os recursos contidos ao Olá solução estiver instalada.

Olá a estratégia básica é a solução de gerenciamento de toostart Criando componentes individuais de saudação no seu ambiente do Azure.  Uma vez que a funcionalidade de saudação funcionando corretamente, é possível começar o empacotamento-los em um [arquivo de solução de gerenciamento](operations-management-suite-solutions-solution-file.md). 


## <a name="design-your-solution"></a>Projetar sua solução
padrão mais comum de saudação para uma solução de gerenciamento é mostrado no diagrama a seguir de saudação.  diferentes componentes Olá nesse padrão são discutidos em Olá abaixo.

![Visão geral da solução OMS](media/operations-management-suite-solutions/solution-overview.png)


### <a name="data-sources"></a>Fontes de dados
Olá primeira etapa na criação de uma solução é determinar dados Olá que exigem do repositório de análise de Log de saudação.  Esses dados podem ser coletados por um [fonte de dados](../log-analytics/log-analytics-data-sources.md) ou [outra solução](operations-management-suite-solutions.md), ou sua solução pode ser necessário tooprovide Olá processo toocollect-lo.

Há várias maneiras de fontes de dados que podem ser coletados no repositório de análise de Log hello, conforme descrito em [fontes de dados de análise de Log](../log-analytics/log-analytics-data-sources.md).  Isso inclui eventos Olá Log de eventos do Windows ou geradas pelo Syslog além tooperformance contadores para clientes Windows e Linux.  Você também pode reunir dados de recursos do Azure coletados pelo Azure Monitor.  

Se você precisar de dados que não está acessíveis por meio de qualquer uma das fontes de dados disponíveis de saudação, você pode usar o hello [API do coletor de dados de HTTP](../log-analytics/log-analytics-data-collector-api.md) que permite o repositório de análise de Log de toohello toowrite dados de qualquer cliente que pode chamar um REST API.  Olá, meio mais comum de coleta de dados personalizadas em uma solução de gerenciamento é toocreate uma [runbook na automação do Azure](../automation/automation-runbook-types.md) que coleta dados de saudação necessária de recursos do Azure ou externos e usa Olá toowrite da API do coletor de dados repositório de toohello.  

### <a name="log-searches"></a>Pesquisas de log
[Pesquisas de log](../log-analytics/log-analytics-log-searches.md) são usado tooextract e analisar dados no repositório de análise de Log de saudação.  Eles são usados pelas exibições e alertas em adição tooallowing Olá usuário tooperform análise ad hoc de dados no repositório de saudação.  

Você deve definir as consultas que você acredita serem úteis toohello usuário mesmo se eles não são usados por modos de exibição ou alertas.  Serão toothem disponível como pesquisas salvas no portal de saudação e você também pode incluir em um [parte da visualização de lista de consultas](../log-analytics/log-analytics-view-designer-parts.md#list-of-queries-part) no modo de exibição personalizado.

### <a name="alerts"></a>Alertas
[Alertas de análise de Log](../log-analytics/log-analytics-alerts.md) identificar problemas por meio de [pesquisas de log](#log-searches) em relação aos dados Olá no repositório de saudação.  Eles notificar o usuário hello ou executar automaticamente uma ação em resposta. Identifique as condições de alerta diferentes para seu aplicativo e inclua regras de alerta correspondentes em seu arquivo de solução.

Se o problema de saudação potencialmente pode ser corrigido com um processo automatizado, em seguida, você geralmente criará um runbook na automação do Azure tooperform essa correção.  Os serviços do Azure mais podem ser gerenciados com [cmdlets](/powershell/azure/overview) quais runbook Olá utilizaria tooperform essa funcionalidade.

Se sua solução requer funcionalidade externa no alerta de tooan de resposta, em seguida, você pode usar um [webhook resposta](../log-analytics/log-analytics-alerts-actions.md).  Isso permite que você toocall um serviço web externo enviar informações de alerta de saudação.

### <a name="views"></a>Modos de exibição
Modos de exibição na análise de Log são usados toovisualize dados do repositório de análise de Log de saudação.  Cada solução normalmente conterá uma única exibição com um [bloco](../log-analytics/log-analytics-view-designer-tiles.md) que é exibido no painel principal do usuário hello.  exibição de saudação pode conter qualquer número de [partes de visualização](../log-analytics/log-analytics-view-designer-parts.md) tooprovide de visualizações diferentes do usuário de toohello do hello os dados coletados.

Você [criar exibições personalizadas usando Olá Designer de exibição](../log-analytics/log-analytics-view-designer.md) que mais tarde você pode exportar para inclusão no seu arquivo de solução.  


## <a name="create-solution-file"></a>Criar arquivo de solução
Depois de configurado e testado componentes Olá que farão parte de sua solução, você pode [criar seu arquivo de solução](operations-management-suite-solutions-solution-file.md).  Você implementará componentes da solução Olá em um [modelo do Gerenciador de recursos](../azure-resource-manager/resource-group-authoring-templates.md) que inclui um [recursos de solução](operations-management-suite-solutions-solution-file.md#solution-resource) com relações toohello outros recursos em Olá arquivo.  


## <a name="test-your-solution"></a>Testar sua solução
Enquanto você estiver desenvolvendo sua solução, será necessário tooinstall e testá-lo em seu espaço de trabalho.  Você pode fazer isso usando qualquer um dos métodos disponíveis Olá muito[testar e instalar o Gerenciador de recursos modelos](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="publish-your-solution"></a>Publicar sua solução
Depois de você ter concluído e testado sua solução, você pode fazer toocustomers disponíveis por meio de qualquer Olá as origens a seguir.

- **Modelos de Início Rápido do Azure**.  [Modelos de início rápido do Azure](https://azure.microsoft.com/resources/templates/) é um conjunto de modelos do Gerenciador de recursos contribuído pela comunidade Olá por meio do GitHub.  Você pode disponibilizar sua solução de informações a seguir Olá [guia contribuição](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE).
- **Azure Marketplace**.  Olá [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/) permite toodistribute e vender sua solução tooother desenvolvedores, ISVs e profissionais de TI.  Você pode aprender como toopublish tooAzure sua solução Marketplace em [como toopublish e gerenciar uma oferta em hello Azure Marketplace](../marketplace-publishing/marketplace-publishing-getting-started.md).



## <a name="next-steps"></a>Próximas etapas
* Saiba como muito[criar um arquivo de solução](operations-management-suite-solutions-solution-file.md) para sua solução de gerenciamento.
* Obter detalhes de saudação do [modelos de autoria do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).
* Pesquise entre os [Modelos de Início Rápido do Azure](https://azure.microsoft.com/documentation/templates) para obter exemplos de diferentes modelos do Resource Manager.