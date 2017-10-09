---
title: tooresource aaaIntroduction Solucionando problemas do observador de rede do Azure | Microsoft Docs
description: "Esta página fornece uma visão geral dos recursos de solução de problemas do recurso Olá observador de rede"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: c1145cd6-d1cf-4770-b1cc-eaf0464cc315
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: ccbe4c1c2364473aba06e709460d67c773cf25ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooresource-troubleshooting-in-azure-network-watcher"></a>Introdução tooresource Solucionando problemas do observador de rede do Azure

Os Gateways de Rede Virtual fornecem conectividade entre os recursos locais e outras redes virtuais no Azure. Esses gateways e suas conexões de monitoramento é fundamental tooensuring comunicação não é interrompida. Observador de rede fornece Olá recurso tootroubleshoot Gateways de rede Virtual e conexões. Isso pode ser chamado por meio do portal de saudação, o PowerShell, CLI ou API REST. Quando chamado, o observador de rede diagnostica integridade de saudação do gateway de rede virtual hello ou conexão e resultados de retorno Olá apropriado. Essa solicitação é uma transação de longa execução, resultados de saudação são retornados após a conclusão do diagnóstico de saudação.

![portal][2]

## <a name="results"></a>Resultados

resultados de preliminar Olá retornados dão uma visão geral da integridade de saudação do recurso de saudação. Mais informações podem ser fornecidas para recursos, conforme mostrado no hello seção a seguir:

Olá lista a seguir é valores hello retornados com hello solucionar problemas de API:

* **startTime** -este valor é tempo de saudação Olá solucionar chamada à API iniciada.
* **endTime** -esse valor é o tempo de saudação quando a solução de problemas de saudação terminou.
* **cod** - esse valor não é apresentado como UnHealthy (não íntegro), se houver uma única falha de diagnóstico.
* **resultados** -resultados é um conjunto de resultados retornados no gateway de rede virtual de Conexão ou Olá Olá.
    * **ID** -este valor é o tipo de falha de saudação.
    * **Resumo** -esse valor é um resumo das falhas de saudação.
    * **detalhadas** -esse valor fornece uma descrição detalhada da falha de saudação.
    * **recommendedActions** -essa propriedade é uma coleção de ações recomendadas tootake.
      * **actionText** -esse valor contém o texto de saudação que descreve quais tootake de ação.
      * **actionUri** -esse valor fornece Olá URI toodocumentation sobre como tooact.
      * **actionUriText** -esse valor é uma breve descrição de texto de ação de saudação.

Olá seguintes tabelas Mostrar Olá falha diferentes tipos (id em resultados de saudação anterior lista) que estão disponíveis e se a falha de saudação cria logs.

### <a name="gateway"></a>Gateway

| Tipo de Falha | Motivo | Registro|
|---|---|---|
| NoFault | Quando nenhum erro é detectado. |Sim|
| GatewayNotFound | Não é possível localizar o Gateway ou o Gateway não está provisionado. |Não|
| PlannedMaintenance |  A instância do gateway está em manutenção.  |Não|
| UserDrivenUpdate | Uma atualização de um usuário está em andamento. Isso pode ser uma operação de redimensionamento. | Não |
| VipUnResponsive | É possível acessar a instância primária de saudação do hello Gateway. Isso acontece quando ocorre falha na investigação de integridade de saudação. | Não |
| PlatformInActive | Há um problema com a plataforma de saudação. | Não|
| ServiceNotRunning | serviço subjacente Olá não está em execução. | Não|
| NoConnectionsFoundForGateway | Nenhuma conexão existe no gateway hello. Isso é apenas um aviso.| Não|
| ConnectionsNotConnected | As conexões não estão conectadas. Isso é apenas um aviso.| Sim|
| GatewayCPUUsageExceeded | uso de CPU do Gateway atual Olá é > 95%. | Sim |

### <a name="connection"></a>Conexão

| Tipo de Falha | Motivo | Registro|
|---|---|---|
| NoFault | Quando nenhum erro é detectado. |Sim|
| GatewayNotFound | Não é possível localizar o Gateway ou o Gateway não está provisionado. |Não|
| PlannedMaintenance | A instância do gateway está em manutenção.  |Não|
| UserDrivenUpdate | Uma atualização de um usuário está em andamento. Isso pode ser uma operação de redimensionamento.  | Não |
| VipUnResponsive | É possível acessar a instância primária de saudação do hello Gateway. Isso acontece quando ocorre falha na investigação de integridade de saudação. | Não |
| ConnectionEntityNotFound | A configuração da Conexão está ausente. | Não |
| ConnectionIsMarkedDisconnected | Olá Conexão está marcado como "desconectada". |Não|
| ConnectionNotConfiguredOnGateway | serviço subjacente Olá não tem Olá que Conexão configurada. | Sim |
| ConnectionMarkedStandy | Olá serviço subjacente é marcado como em espera.| Sim|
| Autenticação | Incompatibilidade de chave pré-compartilhada. | Sim|
| PeerReachability | gateway do Hello correspondente não está acessível. | Sim|
| IkePolicyMismatch | gateway de par de saudação tem políticas de IKE que não são suportadas pelo Azure. | Sim|
| Erro WfpParse | Erro ao analisar logs WFP hello. |Sim|

## <a name="supported-gateway-types"></a>Tipos de gateway com suporte

Olá lista a seguir mostra suporte Olá mostra quais gateways e conexões são compatíveis com a solução de problemas do observador de rede.
|  |  |
|---------|---------|
|**Tipos de gateway**   |         |
|VPN      | Suportado        |
|ExpressRoute | Sem suporte |
|Hypernet | Sem suporte|
|**Tipos de VPN** | |
|Baseada em Rota | Suportado|
|Baseada em Políticas | Sem suporte|
|**Tipos de conexão**||
|IPsec| Suportado|
|VNet2Vnet| Suportado|
|ExpressRoute| Sem suporte|
|Hypernet| Sem suporte|
|VPNClient| Sem suporte|

## <a name="log-files"></a>Arquivos de log

arquivos de log de solução de problemas do Hello recursos são armazenados em uma conta de armazenamento após a conclusão da solução de problemas de recursos. Olá imagem a seguir mostra conteúdo de exemplo hello de uma chamada que resultou em erro.

![arquivo zip][1]

> [!NOTE]
> Em alguns casos, somente um subconjunto dos arquivos de log de saudação é gravado toostorage.

Para obter instruções sobre como baixar os arquivos de contas de armazenamento do azure, consulte muito[Introdução ao armazenamento de BLOBs do Azure usando o .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Outra ferramenta que pode ser usada é o Gerenciador de armazenamento. Para obter mais informações sobre o Gerenciador de armazenamento podem ser encontradas aqui em Olá link a seguir: [Gerenciador de armazenamento](http://storageexplorer.com/)

### <a name="connectionstatstxt"></a>ConnectionStats.txt

Olá **ConnectionStats.txt** arquivo contém estatísticas gerais de saudação Conexão, incluindo bytes de entrada e saída, o status de Conexão e saudação de tempo de saudação Conexão foi estabelecida.

> [!NOTE]
> Se Olá toohello de chamada de API de solução de problemas retorna íntegro, a única coisa que Olá retornada no arquivo zip de saudação é um **ConnectionStats.txt** arquivo.

conteúdo deste arquivo Hello é semelhante toohello exemplo a seguir:

```
Connectivity State : Connected
Remote Tunnel Endpoint :
Ingress Bytes (since last connected) : 288 B
Egress Bytes (Since last connected) : 288 B
Connected Since : 2/1/2017 8:22:06 PM
```

### <a name="cpustatstxt"></a>CPUStats.txt

Olá **CPUStats.txt** arquivo contém o uso da CPU e memória disponível no momento de saudação do teste.  conteúdo deste arquivo Hello é semelhante toohello exemplo a seguir:

```
Current CPU Usage : 0 % Current Memory Available : 641 MBs
```

### <a name="ikeerrorstxt"></a>IKEErrors.txt

Olá **IKEErrors.txt** arquivo contendo quaisquer erros de IKE que foram encontrados durante o monitoramento.

Olá, exemplo a seguir mostra Olá conteúdo de um arquivo de IKEErrors.txt. Os erros podem ser diferentes dependendo do problema de saudação.

```
Error: Authentication failed. Check shared key. Check crypto. Check lifetimes. 
     based on log : Peer failed with Windows error 13801(ERROR_IPSEC_IKE_AUTH_FAIL)
Error: On-prem device sent invalid payload. 
     based on log : IkeFindPayloadInPacket failed with Windows error 13843(ERROR_IPSEC_IKE_INVALID_PAYLOAD)
```

### <a name="scrubbed-wfpdiagtxt"></a>Scrubbed-wfpdiag.txt

Olá **Scrubbed wfpdiag.txt** arquivo de log contém o log de wfp hello. Esse log contém o registro de descarte do pacote e de falhas de IKE/AuthIP.

Olá exemplo a seguir mostra conteúdo de saudação do arquivo de Scrubbed wfpdiag.txt de saudação. Neste exemplo, a chave compartilhada de saudação de uma Conexão não estava correto como pode ser visto na linha de 3ª Olá da parte inferior da saudação. saudação de exemplo a seguir é apenas um trecho de todo o log hello, como log Olá pode ser demorado, dependendo do problema de saudação.

```
...
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Deleted ICookie from hello high priority thread pool list
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|IKE diagnostic event:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Event Header:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Timestamp: 1601-01-01T00:00:00.000Z
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Flags: 0x00000106
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Local address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Remote address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IP version field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP version: IPv4
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP protocol: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local address: 13.78.238.92
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote address: 52.161.24.36
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Application ID:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  User SID: <invalid>
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Failure type: IKE/Authip Main Mode Failure
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Type specific info:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure error code:0x000035e9
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IKE authentication credentials are unacceptable
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure point: Remote
...
```

### <a name="wfpdiagtxtsum"></a>wfpdiag.txt.sum

Olá **wfpdiag.txt.sum** arquivo é um log mostrando buffers hello e eventos processados.

Olá, exemplo a seguir é Olá conteúdo de um arquivo de wfpdiag.txt.sum.
```
Files Processed:
    C:\Resources\directory\924336c47dd045d5a246c349b8ae57f2.GatewayTenantWorker.DiagnosticsStorage\2017-02-02T17-34-23\wfpdiag.etl
Total Buffers Processed 8
Total Events  Processed 2169
Total Events  Lost      0
Total Format  Errors    0
Total Formats Unknown   486
Elapsed Time            330 sec
+-----------------------------------------------------------------------------------+
|EventCount    EventName            EventType   TMF                                 |
+-----------------------------------------------------------------------------------+
|        36    ikeext               ike_addr_utils_c844  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        12    ikeext               ike_addr_utils_c857  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        96    ikeext               ike_addr_utils_c832  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|         6    ikeext               ike_bfe_callbacks_c133  1dc2d67f-8381-6303-e314-6c1452eeb529|
|         6    ikeext               ike_bfe_callbacks_c61  1dc2d67f-8381-6303-e314-6c1452eeb529|
|        12    ikeext               ike_sa_management_c5698  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c8447  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c494  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c642  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c3162  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c3307  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
```

## <a name="next-steps"></a>Próximas etapas

Saiba como Gateways de VPN toodiagnose e conexões por meio de Olá portal visitando [solução de problemas do Gateway - portal do Azure](network-watcher-troubleshoot-manage-portal.md).
<!--Image references-->

[1]: ./media/network-watcher-troubleshoot-overview/GatewayTenantWorkerLogs.png
[2]: ./media/network-watcher-troubleshoot-overview/portal.png
