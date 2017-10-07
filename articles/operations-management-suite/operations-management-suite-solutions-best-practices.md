---
title: "práticas recomendadas de solução de aaaOMSManagement | Microsoft Docs"
description: 
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
ms.date: 04/27/2017
ms.author: bwren
ms.openlocfilehash: 08cf1c101e301d24fb5c2bf4bc02a978e508a198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-creating-management-solutions-in-operations-management-suite-oms-preview"></a>Práticas recomendadas para a criação de soluções de gerenciamento no OMS (Operations Management Suite) (Preview)
> [!NOTE]
> Esta é uma documentação preliminar para criar soluções de gerenciamento no OMS, que estão atualmente em visualização. Qualquer esquema descrita abaixo é toochange de assunto.  

Este artigo apresenta as práticas recomendadas para a [criação de um arquivo de solução de gerenciamento](operations-management-suite-solutions-solution-file.md) no OMS (Operations Management Suite).  Essas informações serão atualizadas à medida que práticas recomendadas adicionais forem identificadas.

## <a name="data-sources"></a>Fontes de dados
- As fontes de dados podem ser [configuradas com um modelo do Resource Manager](../log-analytics/log-analytics-template-workspace-configuration.md), mas não devem ser incluídas em um arquivo de solução.  motivo de saudação é que configurar fontes de dados não é atualmente idempotentes, que significa que sua solução pode substituir a configuração existente no espaço de trabalho do usuário hello.<br><br>Por exemplo, sua solução pode exigir que os eventos de aviso e erro do log de eventos do aplicativo hello.  Se você especificar isso como uma fonte de dados em sua solução, você poderá remover eventos de informações se o usuário Olá tinha essa configuração em seu espaço de trabalho.  Se você incluiu todos os eventos, em seguida, você pode coletar eventos excessivos de informações no espaço de trabalho do usuário hello.

- Se sua solução requer dados de uma das fontes de dados padrão de saudação, você deve definir isso como um pré-requisito.  Estado na documentação do cliente Olá deve configurar fonte de dados de saudação por conta própria.  
- Adicionar um [verificação de fluxo de dados](../log-analytics/log-analytics-view-designer-tiles.md) mensagem tooany exibições em sua solução tooinstruct Olá de usuário em fontes de dados que toobe necessidade configurado para os dados necessários toobe coletados.  Esta mensagem é exibida no bloco de saudação do modo de exibição de saudação quando dados necessários não foram encontrados.


## <a name="runbooks"></a>Runbooks
- Adicionar uma [agendamento de automação](../automation/automation-schedules.md) para cada runbook em sua solução que precisa toorun em uma agenda.
- Incluir Olá [IngestionAPI módulo](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) no seu toobe solução usada por runbooks gravando o repositório de análise de Log de toohello de dados.  Configurar a solução de saudação muito[referência](operations-management-suite-solutions-solution-file.md#solution-resource) esse recurso para que ele permaneça se Olá solução é removida.  Isso permite que o módulo de saudação do várias soluções tooshare.
- Use [variáveis de automação](../automation/automation-schedules.md) tooprovide valores toohello solução que o usuário pode querer toochange mais tarde.  Mesmo se houver Olá solução variável de saudação toocontain configurado, seu valor ainda pode ser alterada.

## <a name="views"></a>Modos de exibição
- Todas as soluções devem incluir uma única exibição que é exibida no portal do usuário hello.  Olá exibição pode conter vários [partes visualização](../log-analytics/log-analytics-view-designer-parts.md) tooillustrate diferente conjuntos de dados.
- Adicionar um [verificação de fluxo de dados](../log-analytics/log-analytics-view-designer-tiles.md) mensagem tooany exibições em sua solução tooinstruct Olá de usuário em fontes de dados que toobe necessidade configurado para os dados necessários toobe coletados.
- Configurar a solução de saudação muito[contêm](operations-management-suite-solutions-solution-file.md#solution-resource) Olá exibição para que ele seja removido se Olá solução é removida.

## <a name="alerts"></a>Alertas
- Defina lista de destinatários hello como um parâmetro no arquivo de solução Olá para que usuário Olá pode defini-los ao instalar a solução de saudação.
- Configurar a solução de saudação muito[referência](operations-management-suite-solutions-solution-file.md#solution-resource) para que o usuário pode alterar sua configuração de regras de alerta.  Pode ser toomake alterações como modificar a lista de destinatários hello, alterar o limite de saudação do alerta de saudação ou desabilitar a regra de alerta de saudação. 


## <a name="next-steps"></a>Próximas etapas
* Percorrer o processo básico de saudação do [Projetando e criando uma solução de gerenciamento](operations-management-suite-solutions-creating.md).
* Saiba como muito[criar um arquivo de solução](operations-management-suite-solutions-solution-file.md).
* [Adicionar alertas e pesquisas salvas](operations-management-suite-solutions-resources-searches-alerts.md) tooyour solução de gerenciamento.
* [Adicionar modos de exibição](operations-management-suite-solutions-resources-views.md) tooyour solução de gerenciamento.
* [Adicionar runbooks de automação e outros recursos](operations-management-suite-solutions-resources-automation.md) tooyour solução de gerenciamento.

