---
title: aaaSupported tipos de recursos por meio de integridade de recursos do Azure | Microsoft Docs
description: Tipos de recurso com suporte por meio do Azure Resource Health
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 03/19/2017
ms.author: BernardoAMunoz
ms.openlocfilehash: fc7bef214702f8ba6954b5aca62236b38023d27a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-types-and-health-checks-in-azure-resource-health"></a>Tipos de recursos e verificações de integridade no Azure Resource Health
Abaixo está uma lista completa de todas as verificações de saudação executados por meio de integridade de recursos por tipos de recursos.

## <a name="microsoftcacheredisredis"></a>Microsoft.CacheRedis/Redis
|Verificações executadas|
|---|
|<ul><li>Todos os nós de Cache Olá backup e executando?</li><li>Olá Cache pode ser acessado de dentro do datacenter Olá?</li><li>Tem Olá que cache atingiu o número máximo de conexões do Olá?</li><li> Cache de saudação esgotou a memória disponível? </li><li>Olá Cache está apresentando um alto número de falhas de página?</li><li>É Olá Cache sob carga pesada?</li></ul>|

## <a name="microsoftcdnprofile"></a>Microsoft.CDN/profile
|Verificações executadas|
|---|
|<ul> <li>Qualquer um dos pontos de extremidade de saudação foi interrompido, removido ou configurado incorretamente?</li><li>Portal suplementar da saudação é acessível para operações de configuração de CDN?</li><li>Há problemas de entrega em andamento com hello pontos de extremidade CDN?</li><li>Usuários podem alterar configuração Olá seus recursos de CDN?</li><li>Alterações de configuração estão propagando a taxa de saudação esperada?</li><li>Os usuários podem gerenciar usando Olá portal do Azure, PowerShell ou Olá API de configuração de CDN Olá?</li> </ul>|

## <a name="microsoftclassiccomputevirtualmachines"></a>Microsoft.classiccompute/virtualmachines
|Verificações executadas|
|---|
|<ul><li>É o servidor de host de saudação para cima e em execução?</li><li>Inicialização de sistema operacional de host Olá concluída?</li><li>Contêiner de máquina virtual Olá provisionado e ligado?</li><li>Há conectividade de rede entre o host de saudação e conta de armazenamento Olá?</li><li>Olá inicialização do sistema operacional convidado de saudação concluída?</li><li>Há manutenção planejada contínua?</li></ul>|

## <a name="microsoftcognitiveservicesaccounts"></a>Microsoft.cognitiveservices/accounts
|Verificações executadas|
|---|
|<ul><li>Conta de saudação pode ser acessada de dentro do datacenter Olá?</li><li>É Olá cognitivas provedor de recursos de serviços disponíveis?</li><li>É Olá cognitivas serviço disponível na região apropriada Olá?</li><li>Pode ler operações ser executada na conta de armazenamento Olá contém metadados do recurso Olá?</li><li>Cota de chamada Olá API foi atingida?</li><li>Limite de leitura Olá API chamada foi atingido?</li></ul>|

## <a name="microsoftcomputevirtualmachines"></a>Microsoft.compute/virtualmachines
|Verificações executadas|
|---|
|<ul><li>É servidor Olá hospeda esta máquina virtual para cima e em execução?</li><li>Inicialização de sistema operacional de host Olá concluída?</li><li>Contêiner de máquina virtual Olá provisionado e ligado?</li><li>Há conectividade de rede entre o host de saudação e conta de armazenamento Olá?</li><li>Olá inicialização do sistema operacional convidado de saudação concluída?</li><li>Há manutenção planejada contínua?</li></ul>|

## <a name="microsoftdatalakeanalyticsaccounts"></a>Microsoft.datalakeanalytics/accounts
|Verificações executadas|
|---|
|<ul><li>Os usuários enviar trabalhos tooData Lake análise em podem Olá região?</li><li>Região de saudação de execução e concluída com êxito em trabalhos básica de fazer?</li><li>Os usuários podem listar os itens de catálogo na região Olá?</li>|


## <a name="microsoftdatalakestoreaccounts"></a>Microsoft.datalakestore/accounts
|Verificações executadas|
|---|
|<ul><li>Os usuários podem carregar repositório data Lake de tooData na região Olá?</li><li>Os usuários podem baixar dados do repositório Data Lake na região Olá?</li></ul>|

## <a name="microsoftdocumentdbdatabaseaccounts"></a>Microsoft.documentdb/databaseAccounts
|Verificações executadas|
|---|
|<ul><li>Houve quaisquer solicitações de banco de dados ou uma coleção não atendidas devido a indisponibilidade de serviço do DocumentDB tooa?</li><li>Houve nenhuma solicitação de documento não atendida devido a indisponibilidade de serviço do DocumentDB tooa?</li></ul>|

## <a name="microsoftnetworkconnections"></a>Microsoft.network/connections
|Verificações executadas|
|---|
|<ul><li>Túnel VPN hello está conectado?</li><li>Há conflitos de configuração na conexão Olá?</li><li>Chaves pré-compartilhadas Olá estão configuradas corretamente?</li><li>Está Olá VPN local acessível?</li><li>Há diferenças na política de segurança do IPSec/IKE Olá?</li><li>É a conexão de VPN S2S Olá provisionado corretamente ou em um estado com falha?</li><li>É a conexão Olá VNET para VNET provisionado corretamente ou em um estado com falha?</li></ul>|

## <a name="microsoftnetworkvirtualnetworkgateways"></a>Microsoft.network/virtualNetworkGateways
|Verificações executadas|
|---|
|<ul><li>É o gateway VPN Olá acessível a partir do hello internet?</li><li>É Olá Gateway VPN no modo de espera?</li><li>Olá serviço VPN está em execução no gateway Olá?</li></ul>|

## <a name="microsoftnotificationhubsnamespace"></a>Microsoft.NotificationHubs/namespace
|Verificações executadas|
|---|
|<ul><li> Operações de tempo de execução como o registro, a instalação ou enviar podem ser executadas no namespace Olá?</li></ul>|

## <a name="microsoftpowerbiworkspacecollections"></a>Microsoft.PowerBI/workspaceCollections
|Verificações executadas|
|---|
|<ul><li>Depende do sistema operacional do host hello e em execução?</li><li>Olá workspaceCollection é acessível de fora do datacenter Olá?</li><li>É Olá provedor de recursos do Power BI disponíveis?</li><li>É Olá PowerBI Service disponível na região apropriada Olá?</li></ul>|

## <a name="microsoftsearchsearchservices"></a>Microsoft.search/searchServices
|Verificações executadas|
|---|
|<ul><li>Operações de diagnóstico podem ser executadas no cluster Olá?</li></ul>|

## <a name="microsoftsqlserverdatabase"></a>Microsoft.SQL/Server/database
|Verificações executadas|
|---|
|<ul><li> Houve banco de dados de toohello logons?</li></ul>|

## <a name="microsoftstreamanalyticsstreamingjobs"></a>Microsoft.StreamAnalytics/streamingjobs
|Verificações executadas|
|---|
|<ul><li>São todos os hosts de saudação onde trabalho hello está executando o e em execução?</li><li>Foi Olá trabalho não é possível toostart?</li><li>Há atualizações de tempo de execução em andamento?</li><li>Saudação de trabalho em um estado esperado (por exemplo em execução ou parado pelo cliente)?</li><li>Olá trabalho encontrou o limite de exceções de memória?</li><li>Há atualizações de computação agendadas em andamento?</li><li>É Olá Gerenciador de execução (plano de controle) disponível?</li></ul>|

## <a name="microsoftwebserverfarms"></a>Microsoft.web/serverFarms
|Verificações executadas|
|---|
|<ul><li>É o servidor de host de saudação para cima e em execução?</li><li>Os Serviços de Informações da Internet estão em execução?</li><li>O balanceador de carga hello está em execução?</li><li>Olá o plano do serviço Web pode ser acessado de dentro do datacenter Olá?</li><li>Olá armazenamento hospedagem Olá sites conteúdo da conta para o farm de servidores hello está disponível?</li></ul>|

## <a name="microsoftwebsites"></a>Microsoft.web/sites
|Verificações executadas|
|---|
|<ul><li>É o servidor de host de saudação para cima e em execução?</li><li>Os servidor de Informações da Internet está em execução?</li><li>O balanceador de carga hello está em execução?</li><li>Olá aplicativo Web pode ser acessado de dentro do datacenter Olá?</li><li>Conta de armazenamento Olá está hospedando o conteúdo do site Olá disponível?</li></ul>|

# <a name="next-steps"></a>Próximas etapas
-  Consulte [tooAzure Introdução a integridade do serviço](service-health-overview.md) e [tooAzure Introdução integridade de recursos](resource-health-overview.md) toounderstand mais sobre eles. 
-  [Perguntas frequentes sobre o Azure Resource Health](resource-health-faq.md)
- Configure alertas para receber notificações de problemas de integridade. Para obter mais informações, consulte [Configurar alertas do Service Health](../monitoring-and-diagnostics/monitoring-activity-log-alerts-on-service-notifications.md). 