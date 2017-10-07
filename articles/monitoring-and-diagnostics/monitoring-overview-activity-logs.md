---
title: "aaaOverview de saudação Log de atividades do Azure | Microsoft Docs"
description: "Saiba quais hello é do Log de atividades do Azure e como você pode usá-lo toounderstand eventos que ocorrem dentro de sua assinatura do Azure."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c274782f-039d-4c28-9ddb-f89ce21052c7
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: johnkem
ms.openlocfilehash: cba79b7f6dc0833ef588382e763761fd77d43307
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-subscription-activity-with-hello-azure-activity-log"></a>Monitorar a atividade de assinatura com hello Log de atividades do Azure
Olá **o Log de atividades do Azure** é um log de assinatura que fornece informações sobre eventos de nível de assinatura que ocorreram no Azure. Isso inclui um intervalo de dados do Azure Resource Manager dados operacionais tooupdates em eventos de integridade do serviço. Olá Log de atividades era conhecido anteriormente como "Logs de auditoria" ou "Logs operacionais", desde que os eventos de plano de controle de relatórios Olá categoria administrativa para suas assinaturas. Usando hello atividade de Log, você pode determinar Olá ', quem e quando ' para qualquer gravação as operações executadas em recursos de saudação em sua assinatura (PUT, POST, DELETE). Você também pode saber o status de saudação da operação de saudação e outras propriedades relevantes. Olá Log de atividades não inclui operações de leitura (GET) ou de operações para recursos que usam Olá clássico / modelo "RDFE".

![Logs de Atividade X outros tipos de logs ](./media/monitoring-overview-activity-logs/Activity_Log_vs_other_logs_v5.png)

Figura 1: Logs de Atividade X outros tipos de logs

Hello atividade Log difere [Logs de diagnóstico](monitoring-overview-of-diagnostic-logs.md). Logs de atividade fornecem dados sobre operações de saudação em um recurso de saudação fora (hello "plano de controle"). Logs de diagnóstico são emitidos por um recurso e fornecem informações sobre a operação de saudação do recurso (hello "plano de dados").

Você pode recuperar eventos de seu Log de atividade usando Olá portal do Azure, CLI, cmdlets do PowerShell e a API de REST do Monitor do Azure.


> [!WARNING]
> Olá Log de atividades do Azure é principalmente para atividades que ocorrem no Gerenciador de recursos do Azure. Não controla de recursos usando o modelo RDFE/clássico hello. Alguns tipos de recursos Clássicos têm um provedor de recursos de proxy no Azure Resource Manager (por exemplo, Microsoft.ClassicCompute). Se você interage com um tipo de recurso por meio do Azure Resource Manager usando esses provedores de recursos de proxy clássico, operações de saudação aparecem na Olá Log de atividades. Se você interagir com um recurso clássico de tipo no portal clássico do hello ou caso contrário fora de proxies do Azure Resource Manager hello, suas ações são apenas gravar na Olá Log da operação. Olá Log da operação é acessível apenas no portal clássico do hello.
>
>

Saudação de exibição Olá vídeo de Introdução ao Log de atividades a seguir.
> [!VIDEO https://channel9.msdn.com/Blogs/Seth-Juarez/Logs-John-Kemnetz/player]
> 
>

## <a name="categories-in-hello-activity-log"></a>Categorias de saudação Log de atividades
Hello atividade de Log contém várias categorias de dados. Para obter detalhes completos sobre esquemas de saudação dessas categorias, [consulte este artigo](monitoring-activity-log-schema.md). Estão incluídos:
* **Administrativos** -nesta categoria contém o registro de saudação de todos os criar, operações de atualização, exclusão e a ação executada por meio do Gerenciador de recursos. Exemplos de saudação tipos de eventos que você vê nessa categoria incluem "criar a máquina virtual" e "Excluir grupo de segurança de rede" cada ação tomada por um usuário ou aplicativo usando o Gerenciador de recursos é modelado como uma operação em um tipo de recurso específico. Se o tipo de operação de saudação é gravar, Delete ou ação, registros de saudação do início de saudação e o sucesso ou falha da operação são registradas na categoria administrativa hello. categoria administrativa Olá também inclui qualquer controle de acesso baseado em toorole alterações em uma assinatura.
* **Integridade do serviço** -nesta categoria contém o registro de saudação de qualquer incidente de integridade do serviço que ocorreram no Azure. Um exemplo de tipo de saudação do evento que você vê nessa categoria é "SQL Azure no Leste dos EUA está passando por tempo de inatividade." Eventos de serviço de integridade são fornecidos em cinco variedades: ação necessária, recuperação assistida, incidente, manutenção, informações ou segurança e só aparecerá se você tiver um recurso na assinatura de saudação que será afetada pelo evento hello.
* **Alerta** -nesta categoria contém o registro de saudação de todas as ativações de alertas do Azure. Um exemplo desse tipo de saudação do evento que você vê nessa categoria é "% da CPU em myVM 80 para hello nos últimos 5 minutos." Uma variedade de sistemas do Azure têm um conceito de alerta – você pode definir uma regra de algum tipo e receber uma notificação quando as condições corresponderem a essa regra. Cada vez que um tipo de alerta com suporte do Azure 'ativa,' ou condições hello são atendido toogenerate uma notificação, um registro de ativação de saudação também é enviada por push toothis categoria de saudação Log de atividades.
* **Dimensionamento automático** -nesta categoria contém o registro de saudação de qualquer operação de toohello relacionados de eventos do mecanismo de dimensionamento automático de saudação com base em quaisquer configurações de dimensionamento automático que você definiu na sua assinatura. Um exemplo desse tipo de saudação do evento que você vê nessa categoria é "Escala de dimensionamento automático das ações de falha". Usar o dimensionamento automático, você pode automaticamente expansão ou escala em Olá o número de instâncias em um tipo de recurso com suporte com base na hora do dia e/ou carregar dados (métricas) usando uma configuração de AutoEscala. Quando Olá condições tooscale para cima ou para baixo, início hello e eventos de êxito ou com falhas são registrados nesta categoria.
* **Recomendação** - essa categoria contém eventos de recomendação de certos tipos de recursos, como sites e servidores SQL. Esses eventos recomendações para como toobetter utilizam os seus recursos. Você só receberá eventos desse tipo se tiver recursos que emitam recomendações.
* **Política de segurança e integridade de recursos** -essas categorias não contêm eventos; elas estão reservadas para uso futuro.

## <a name="event-schema-per-category"></a>Esquema de eventos por categoria
[Consulte esse esquema de evento de Log de atividades do artigo toounderstand Olá por categoria.](monitoring-activity-log-schema.md)

## <a name="what-you-can-do-with-hello-activity-log"></a>O que você pode fazer com hello Log de atividades
Aqui estão algumas das coisas Olá que você pode fazer com hello Log de atividades:

![Log de Atividades do Azure](./media/monitoring-overview-activity-logs/Activity_Log_Overview_v3.png)


* Consultar e exibi-lo no hello **portal do Azure**.
* [Criar um alerta em um evento do Log de Atividades.](monitoring-activity-log-alerts.md)
* [Fluxo de tooan **Hub de eventos** ](monitoring-stream-activity-logs-event-hubs.md) para ingestão por um serviço de terceiros ou a solução de análise personalizado, como o Power BI.
* Analisá-los no Power BI usando Olá [ **pacote de conteúdo do PowerBI**](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs/).
* [Salvá-lo tooa **conta de armazenamento** para fins de arquivamento ou manual inspeção](monitoring-archive-activity-log.md). Você pode especificar o tempo de retenção de saudação (em dias) usando Olá **Log perfil**.
* Consultar por meio de Cmdlet do PowerShell, da CLI ou da API REST.

## <a name="query-hello-activity-log-in-hello-azure-portal"></a>Saudação de consulta Log de atividades no hello portal do Azure
Dentro de saudação portal do Azure, você pode exibir o Log de atividades em vários locais:
* Olá **folha do Log de atividades**, que você pode acessar pesquisando Olá Log de atividades em "Mais serviços" no painel de navegação do lado esquerdo de saudação.
* Olá **folha Monitor**, que é exibido por padrão no painel de navegação do lado esquerdo de saudação. Hello atividade de Log é uma seção desta folha de Monitor do Azure.
* Qualquer recurso **folha de recursos**, por exemplo, folha de configuração Olá para uma máquina Virtual. Olá Log de atividades é ser uma das seções de saudação na maioria dos blades recursos e clicando nele automaticamente filtra eventos de saudação toothose relacionados ao recurso de toothat específico.

Em Olá portal do Azure, você pode filtrar o Log de atividades por estes campos:
* Tempo de TimeSpan - Olá início e término para eventos.
* Categoria - Olá categoria de evento conforme descrito acima.
* Assinatura – Um ou mais nomes de assinatura do Azure.
* Grupo de recursos – Um ou mais grupos de recursos nessas assinaturas.
* Recurso (nome) - Olá nome de um recurso específico.
* Tipo de recurso - Olá tipo de recurso, por exemplo, Microsoft.Compute/virtualmachines.
* Nome da operação - nome de saudação de uma operação do Gerenciador de recursos do Azure, por exemplo, Microsoft.SQL/servers/Write.
* Severidade - nível de severidade de saudação do evento hello (informação, aviso, erro, crítico).
* Evento iniciado por - Olá 'chamador' ou o usuário que realizou a operação de saudação.
* Pesquisa aberta – Isso é uma caixa de pesquisa de texto aberto que procura essa cadeia de caracteres em todos os campos de todos os eventos.

Quando você definiu um conjunto de filtros, você pode salvá-lo como uma consulta que é persistente entre as sessões, se você alguma vez precisar tooperform Olá mesma consulta com os filtros aplicados novamente no futuro de saudação. Você também pode fixar uma manutenção de tooalways do painel do Azure consulta tooyour olho em eventos específicos.

Clicar em "Aplicar" executa sua consulta e mostrar todos os eventos correspondentes. Clicar em qualquer evento na lista de saudação mostra Olá resumo do evento, bem como Olá JSON completo bruto de evento.

Até mesmo mais energia, você pode clicar em Olá **pesquisa de Log** ícone, que exibe os dados de Log de atividades em Olá [solução de análise de Log de atividade de análise de Log](../log-analytics/log-analytics-activity.md). folha de Log de atividades de saudação oferece uma experiência de filtro básico/procurar nos logs, mas habilita a análise de Log toopivot, consultar e visualizar seus dados de forma mais eficiente.

## <a name="export-hello-activity-log-with-a-log-profile"></a>Exportar hello atividade de Log com um perfil de registro
Um **Perfil de Log** controla o modo de exportação de seu Log de Atividades. Com um Perfil de Log, você pode configurar:

* Onde Olá Log de atividades deve ser enviada (conta de armazenamento ou Hubs de eventos)
* Quais categorias de evento (Gravação, Exclusão, Ação) devem ser enviadas. *significado Hello "category" em perfis de Log e eventos de Log de atividades é diferente. Olá perfil do Log, "Category" representa o tipo de operação de saudação (ação de gravação, exclusão,). Em um evento de Log de atividades, propriedade de 'categoria' hello representa fonte hello ou tipo de evento (por exemplo, administração, ServiceHealth, alerta e muito mais).*
* Quais regiões (locais) devem ser exportados. Verifique se tooinclude "global", como muitos eventos Olá Log de atividades são eventos globais.
* Quanto tempo hello atividade de Log deve ser mantido em uma conta de armazenamento.
    - Uma retenção de zero dias significa que os registros serão mantidos indefinidamente. Caso contrário, o valor de saudação pode ser qualquer número de dias entre 1 e 2147483647.
    - Se as políticas de retenção são definidas, mas o armazenamento de logs em uma conta de armazenamento está desabilitado (por exemplo, se apenas as opções de Hubs de eventos ou do OMS são selecionadas), políticas de retenção de saudação não têm efeito.
    - Políticas de retenção são aplicadas por dia, para em Olá final de um dia (UTC), logs de dia de saudação que agora está além da política de retenção de saudação são excluídos. Por exemplo, se você tiver uma política de retenção de um dia, no início de saudação do dia Olá hoje hello logs de anteontem Olá seriam excluídas.

Você pode usar uma conta de armazenamento ou o namespace de hub de eventos que não está em Olá mesma assinatura conforme Olá um emissor logs. usuário de saudação que configura a configuração de saudação deve ter assinaturas do hello apropriadas RBAC acesso tooboth.

Essas configurações podem ser definidas usando a opção "Export" hello na folha de Log de atividades de saudação no portal de saudação. Também pode ser configurados por meio de programação [usando Olá API REST do Azure Monitor](https://msdn.microsoft.com/library/azure/dn931927.aspx), cmdlets do PowerShell ou CLI. Uma assinatura pode ter somente um perfil de log.

### <a name="configure-log-profiles-using-hello-azure-portal"></a>Configurar perfis de log usando Olá portal do Azure
Você pode tooan do Log de atividades de saudação Hub de eventos de fluxo ou armazená-las em uma conta de armazenamento usando a opção de "Exportar" de saudação em Olá portal do Azure.

1. Navegue toohello **Log de atividades** folha usando o menu de saudação em Olá esquerda do portal de saudação.

    ![Navegue tooActivity Log no portal](./media/monitoring-overview-activity-logs/activity-logs-portal-navigate.png)
2. Clique em Olá **exportar** botão na parte superior de saudação da folha de saudação.

    ![Botão Exportar no portal](./media/monitoring-overview-activity-logs/activity-logs-portal-export.png)
3. Na folha de saudação que aparece, você pode selecionar:  
  * regiões para os quais você gostaria que os eventos de tooexport
  * Olá toowhich de conta de armazenamento que você gostaria que os eventos de toosave
  * Olá quantos dias que você deseja tooretain esses eventos no armazenamento. Uma configuração de 0 dias retém logs Olá para sempre.
  * Olá Namespace de barramento de serviço em que você gostaria que um toobe de Hub de eventos criado para esses eventos de fluxo contínuo.

     ![Folha Exportar Log de Atividades](./media/monitoring-overview-activity-logs/activity-logs-portal-export-blade.png)
4. Clique em **salvar** toosave essas configurações. configurações de saudação imediatamente são ser aplicada tooyour assinatura.

### <a name="configure-log-profiles-using-hello-azure-powershell-cmdlets"></a>Configurar perfis de log usando Olá Cmdlets do PowerShell do Azure
#### <a name="get-existing-log-profile"></a>Obter o perfil de log existente
```
Get-AzureRmLogProfile
```

#### <a name="add-a-log-profile"></a>Adicionar um perfil de log
```
Add-AzureRmLogProfile -Name my_log_profile -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus -RetentionInDays 90 -Categories Write,Delete,Action
```

| Propriedade | Obrigatório | Descrição |
| --- | --- | --- |
| Nome |Sim |Nome de seu perfil de log. |
| StorageAccountId |Não |ID do recurso da saudação toowhich da conta de armazenamento hello atividade de Log deve ser salvo. |
| serviceBusRuleId |Não |ID da regra barramento de serviço para o namespace de barramento de serviço Olá você gostaria que toohave hubs de eventos criados no. É uma cadeia de caracteres com este formato: `{service bus resource ID}/authorizationrules/{key name}`. |
| Locais |Sim |Lista separada por vírgulas de regiões para o qual você gostaria que os eventos de Log de atividades de toocollect. |
| RetentionInDays |Sim |Número de dias durante os quais os eventos devem ser mantidos, entre 1 e 2147483647. Um valor de zero armazena logs Olá indefinidamente (sempre). |
| Categorias |Não |Lista separada por vírgulas de categorias de eventos que devem ser coletados. Os valores possíveis são Gravação, Exclusão e Ação. |

#### <a name="remove-a-log-profile"></a>Remover um perfil de log
```
Remove-AzureRmLogProfile -name my_log_profile
```

### <a name="configure-log-profiles-using-hello-azure-cross-platform-cli"></a>Configurar perfis de log usando Olá CLI de plataforma cruzada do Azure
#### <a name="get-existing-log-profile"></a>Obter o perfil de log existente
```
azure insights logprofile list
```
```
azure insights logprofile get --name my_log_profile
```
Olá `name` propriedade deve ser o nome de saudação do seu perfil do log.

#### <a name="add-a-log-profile"></a>Adicionar um perfil de log
```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope --retentionInDays 90 –categories Write,Delete,Action
```

| Propriedade | Obrigatório | Descrição |
| --- | --- | --- |
| name |Sim |Nome de seu perfil de log. |
| storageId |Não |ID do recurso da saudação toowhich da conta de armazenamento hello atividade de Log deve ser salvo. |
| serviceBusRuleId |Não |ID da regra barramento de serviço para o namespace de barramento de serviço Olá você gostaria que toohave hubs de eventos criados no. É uma cadeia de caracteres com este formato: `{service bus resource ID}/authorizationrules/{key name}`. |
| locais |Sim |Lista separada por vírgulas de regiões para o qual você gostaria que os eventos de Log de atividades de toocollect. |
| RetentionInDays |Sim |Número de dias durante os quais os eventos devem ser mantidos, entre 1 e 2147483647. Um valor de zero armazena logs Olá indefinidamente (sempre). |
| Categorias |Não |Lista separada por vírgulas de categorias de eventos que devem ser coletados. Os valores possíveis são Gravação, Exclusão e Ação. |

#### <a name="remove-a-log-profile"></a>Remover um perfil de log
```
azure insights logprofile delete --name my_log_profile
```

## <a name="next-steps"></a>Próximas etapas
* [Saiba mais sobre hello (anteriormente conhecida como Logs de auditoria) do Log de atividades](../azure-resource-manager/resource-group-audit.md)
* [Fluxo de tooEvent de Log de atividades do Azure Olá Hubs](monitoring-stream-activity-logs-event-hubs.md)
