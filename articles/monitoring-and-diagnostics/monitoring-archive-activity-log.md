---
title: "Olá aaaArchive Log de atividades do Azure | Microsoft Docs"
description: "Saiba como tooarchive sua atividade do Azure Log para retenção de longo prazo em uma conta de armazenamento."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2016
ms.author: johnkem
ms.openlocfilehash: 58c6d3a3a31398287f66f76999d48f2942ab5109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="archive-hello-azure-activity-log"></a>Olá arquivar o Log de atividades do Azure
Neste artigo, mostramos como você pode usar o hello portal do Azure, Cmdlets do PowerShell ou CLI de plataforma cruzada tooarchive seu [ **o Log de atividades do Azure** ](monitoring-overview-activity-logs.md) em uma conta de armazenamento. Essa opção é útil se você quiser tooretain mais de 90 dias (com controle total sobre a política de retenção Olá) para o Log de atividades de auditoria, análise estática, ou de backup. Se você precisar somente tooretain seus eventos por 90 dias ou menos que você não é necessário tooset tooa arquivamento conta de armazenamento, desde que os eventos de Log de atividades são mantidos no hello plataforma Windows Azure por 90 dias sem habilitar arquivamento.

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar, é preciso muito[criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account) toowhich poderá arquivar o Log de atividades. É altamente recomendável que você não use uma conta de armazenamento existente que tenha outros monitoramento não dados armazenados nela, para que você pode controlar melhor acesso toomonitoring dados. No entanto, se você também estiver arquivando Logs de diagnóstico e a conta de armazenamento tooa métricas, talvez faça sentido toouse essa conta de armazenamento para a atividade de Log também tookeep todos os dados de monitoramento em um local central. conta de armazenamento Olá usada deve ser uma conta de armazenamento de propósito geral, não uma conta de armazenamento de blob. conta de armazenamento Olá não tem toobe Olá mesma assinatura que Olá emitindo logs como usuário Olá que configura a configuração de saudação tem assinaturas de tooboth de acesso RBAC apropriadas.

## <a name="log-profile"></a>Perfil de Log
Olá tooarchive Log de atividades, usando qualquer um dos métodos de saudação abaixo, você definir Olá **Log perfil** para uma assinatura. Olá Log perfil define o tipo de saudação de eventos que são armazenadas ou transmitidas e Olá saídas — hub de conta e/ou evento de armazenamento. Ele também define a política de retenção de saudação (número de dias tooretain) para eventos armazenados em uma conta de armazenamento. Se toozero é definir a política de retenção de hello, eventos são armazenados indefinidamente. Caso contrário, isso pode ser definido tooany valor entre 1 e 2147483647. Políticas de retenção são aplicadas por dia, para em Olá final de um dia (UTC), logs do dia Olá que agora está além da política de retenção hello serão excluídas. Por exemplo, se você tiver uma política de retenção de um dia, no início de saudação do dia Olá hoje hello logs de anteontem Olá seriam excluídas. [Você pode ler mais sobre perfis de log aqui](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile). 

## <a name="archive-hello-activity-log-using-hello-portal"></a>Arquivo hello usando o portal de saudação do Log de atividades
1. No portal de saudação, clique em Olá **Log de atividades** link de navegação do lado esquerdo de saudação. Se você não vir um link para Olá Log de atividades, clique em Olá **mais serviços** link primeiro.
   
    ![Navegue tooActivity folha de Log](media/monitoring-archive-activity-log/act-log-portal-navigate.png)
2. Na parte superior de saudação da folha de saudação, clique em **exportar**.
   
    ![Botão de exportação Olá](media/monitoring-archive-activity-log/act-log-portal-export-button.png)
3. Na folha de saudação que aparece, marque a caixa de saudação do **exportar a conta de armazenamento tooa** e selecione uma conta de armazenamento.
   
    ![De uma conta de armazenamento](media/monitoring-archive-activity-log/act-log-portal-export-blade.png)
4. Usando o controle deslizante de saudação ou caixa de texto, defina um número de dias que os eventos de Log de atividades devem ser mantidos na conta de armazenamento. Se você preferir toohave seus dados persistentes na conta de armazenamento Olá indefinidamente, defina este número toozero.
5. Clique em **Salvar**.

## <a name="archive-hello-activity-log-via-powershell"></a>Olá arquivar o Log de atividades por meio do PowerShell
```
Add-AzureRmLogProfile -Name my_log_profile -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus -RetentionInDays 180 -Categories Write,Delete,Action
```

| Propriedade | Obrigatório | Descrição |
| --- | --- | --- |
| StorageAccountId |Não |ID do recurso de toowhich de conta de armazenamento Olá Logs de atividade deve ser salvo. |
| Locais |Sim |Lista separada por vírgulas de regiões para o qual você gostaria que os eventos de Log de atividades de toocollect. Você pode exibir uma lista de todas as regiões [visitando esta página](https://azure.microsoft.com/en-us/regions) ou usando [Olá API de REST de gerenciamento do Azure](https://msdn.microsoft.com/library/azure/gg441293.aspx). |
| RetentionInDays |Sim |Número de dias durante os quais os eventos devem ser mantidos, entre 1 e 2147483647. Um valor de zero armazena logs Olá indefinidamente (sempre). |
| Categorias |Sim |Lista separada por vírgulas de categorias de eventos que devem ser coletados. Os valores possíveis são Gravação, Exclusão e Ação. |

## <a name="archive-hello-activity-log-via-cli"></a>Olá arquivar o Log de atividade via CLI
```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --locations global,westus,eastus,northeurope --retentionInDays 180 –categories Write,Delete,Action
```

| Propriedade | Obrigatório | Descrição |
| --- | --- | --- |
| name |Sim |Nome de seu perfil de log. |
| storageId |Não |ID do recurso de toowhich de conta de armazenamento Olá Logs de atividade deve ser salvo. |
| locais |Sim |Lista separada por vírgulas de regiões para o qual você gostaria que os eventos de Log de atividades de toocollect. Você pode exibir uma lista de todas as regiões [visitando esta página](https://azure.microsoft.com/en-us/regions) ou usando [Olá API de REST de gerenciamento do Azure](https://msdn.microsoft.com/library/azure/gg441293.aspx). |
| RetentionInDays |Sim |Número de dias durante os quais os eventos devem ser mantidos, entre 1 e 2147483647. Um valor de zero armazenará logs Olá indefinidamente (sempre). |
| Categorias |Sim |Lista separada por vírgulas de categorias de eventos que devem ser coletados. Os valores possíveis são Gravação, Exclusão e Ação. |

## <a name="storage-schema-of-hello-activity-log"></a>Esquema de armazenamento de Log de atividades de hello
Depois que você configurar arquivamento, um contêiner de armazenamento será criado na conta de armazenamento hello, assim como ocorre um evento de Log de atividades. blobs Hello dentro do contêiner de saudação siga Olá mesmo formato em hello atividade de Log e Logs de diagnóstico. estrutura Olá esses blobs é:

> insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{ID da assinatura}/y={ano de quatro dígitos}/m={mês numérico de dois dígitos}/d={dia numérico de dois dígitos}/h={hora de relógio de 24 horas de dois dígitos}/m=00/PT1H.json
> 
> 

Por exemplo, um nome de blob poderia ser:

> insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.json
> 
> 

Cada blob PT1H.json contém um blob JSON de eventos que ocorreram na hora de saudação especificada na URL de blob de saudação (por exemplo, h = 12). Durante a saudação hora presente, os eventos são acrescentadas toohello PT1H.json arquivo conforme elas ocorrem. Olá valor de minuto (m = 00) é sempre 00, desde que os eventos de Log de atividades são divididos em blobs individuais por hora.

No arquivo de PT1H.json hello, cada evento é armazenado na matriz de registros"hello", neste formato a seguir:

```
{
    "records": [
        {
            "time": "2015-01-21T22:14:26.9792776Z",
            "resourceId": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
            "operationName": "microsoft.support/supporttickets/write",
            "category": "Write",
            "resultType": "Success",
            "resultSignature": "Succeeded.Created",
            "durationMs": 2826,
            "callerIpAddress": "111.111.111.11",
            "correlationId": "c776f9f4-36e5-4e0e-809b-c9b3c3fb62a8",
            "identity": {
                "authorization": {
                    "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
                    "action": "microsoft.support/supporttickets/write",
                    "evidence": {
                        "role": "Subscription Admin"
                    }
                },
                "claims": {
                    "aud": "https://management.core.windows.net/",
                    "iss": "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",
                    "iat": "1421876371",
                    "nbf": "1421876371",
                    "exp": "1421880271",
                    "ver": "1.0",
                    "http://schemas.microsoft.com/identity/claims/tenantid": "1e8d8218-c5e7-4578-9acc-9abbd5d23315 ",
                    "http://schemas.microsoft.com/claims/authnmethodsreferences": "pwd",
                    "http://schemas.microsoft.com/identity/claims/objectidentifier": "2468adf0-8211-44e3-95xq-85137af64708",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "admin@contoso.com",
                    "puid": "20030000801A118C",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "9vckmEGF7zDKk1YzIY8k0t1_EAPaXoeHyPRn6f413zM",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "John",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Smith",
                    "name": "John Smith",
                    "groups": "cacfe77c-e058-4712-83qw-f9b08849fd60,7f71d11d-4c41-4b23-99d2-d32ce7aa621c,31522864-0578-4ea0-9gdc-e66cc564d18c",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": " admin@contoso.com",
                    "appid": "c44b4083-3bq0-49c1-b47d-974e53cbdf3c",
                    "appidacr": "2",
                    "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
                    "http://schemas.microsoft.com/claims/authnclassreference": "1"
                }
            },
            "level": "Information",
            "location": "global",
            "properties": {
                "statusCode": "Created",
                "serviceRequestId": "50d5cddb-8ca0-47ad-9b80-6cde2207f97c"
            }
        }
    ]
}
```


| Nome do elemento | Descrição |
| --- | --- |
| tempo real |Evento Olá correspondente de solicitação de carimbo de hora do evento Olá foi gerado pelo Olá Olá de processamento de serviço do Azure. |
| resourceId |ID do recurso da saudação afetados recursos. |
| operationName |Nome da operação de saudação. |
| categoria |Categoria de ação hello, por exemplo. Gravação, Leitura e Ação. |
| resultType |Olá tipo de resultado hello, por exemplo. Êxito, Falha e Início |
| resultSignature |Depende do tipo de recurso de saudação. |
| durationMs |Duração da operação de saudação em milissegundos |
| callerIpAddress |Endereço IP do usuário de saudação que executou a operação de hello, declaração UPN ou declaração SPN com base na disponibilidade. |
| correlationId |Normalmente um GUID no formato de cadeia de caracteres de saudação. Os eventos que compartilham um correlationId pertencem toohello mesma ação uber. |
| identidade |Blob JSON que descreve a declarações e autorização hello. |
| autorização |Blob de propriedades RBAC do evento hello. Geralmente inclui propriedades de "ação", "função" e "escopo" hello. |
| level |Nível de evento hello. Uma saudação valores a seguir: "Crítico", "Error", "Aviso", "Informativo" e "Detalhado" |
| location |Região na qual local Olá ocorreu (ou global). |
| propriedades |Conjunto de `<Key, Value>` pares (ou seja, o dicionário) que descreve os detalhes de saudação do evento hello. |

> [!NOTE]
> Propriedades de saudação e o uso dessas propriedades podem variar dependendo de recurso hello.
> 
> 

## <a name="next-steps"></a>Próximas etapas
* [Baixar blobs para análise](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)
* [Fluxo de tooEvent do Log de atividades de saudação Hubs](monitoring-stream-activity-logs-event-hubs.md)
* [Leia mais sobre Olá Log de atividades](monitoring-overview-activity-logs.md)

