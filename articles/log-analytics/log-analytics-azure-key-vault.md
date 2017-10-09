---
title: "aaaAzure solução de Cofre de chaves em análise de Log | Microsoft Docs"
description: "Você pode usar a solução do Azure Key Vault Olá em tooreview de análise de logs, que logs do Azure Key Vault."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: 5e25e6d6-dd20-4528-9820-6e2958a40dae
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: richrund
ms.openlocfilehash: 1c6eae26ded7ad55b0159a3be09cdc9901596298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-analytics-solution-in-log-analytics"></a>Solução do Azure Key Vault Analytics no Log Analytics

![Símbolo do Cofre de Chaves](./media/log-analytics-azure-keyvault/key-vault-analytics-symbol.png)

Você pode usar a solução de Cofre de chaves do Azure de saudação em tooreview de análise de logs do Azure Key Vault AuditEvent logs.

solução de saudação toouse, você precisa tooenable log diagnóstico do Azure Key Vault e o espaço de trabalho do hello direto diagnóstico tooa análise de Log. Não é necessário toowrite Olá logs tooAzure o armazenamento de Blob.

> [!NOTE]
> Em janeiro de 2017, Olá suporte para a forma de envio de logs do Cofre de chaves tooLog alterada de análise. Mostra se solução do hello Cofre de chaves que você estiver usando *(preterido)* no título hello, consulte muito[migrando de solução de Cofre de chaves antiga Olá](#migrating-from-the-old-key-vault-solution) para obter as etapas que você precisa toofollow.
>
>

## <a name="install-and-configure-hello-solution"></a>Instalar e configurar a solução de saudação
Use Olá tooinstall instruções a seguir e configurar a solução do Azure Key Vault hello:

1. Habilitar a solução do Azure Key Vault saudação do [do Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview) ou usando o processo de saudação descrito em [soluções de análise de Log adicionar da Galeria de soluções de saudação](log-analytics-add-solutions.md).
2. Habilitar o diagnóstico de registro em log para Olá toomonitor de recursos de Cofre de chaves, usando qualquer Olá [portal](#enable-key-vault-diagnostics-in-the-portal) ou [PowerShell](#enable-key-vault-diagnostics-using-powershell)

### <a name="enable-key-vault-diagnostics-in-hello-portal"></a>Habilitar o diagnóstico de Cofre de chaves no portal de saudação

1. No portal do Azure de Olá, navegar toohello toomonitor de recurso de Cofre de chaves
2. Selecione *logs de diagnóstico* tooopen Olá página a seguir

   ![imagem do bloco Cofre de Chaves do Azure](./media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics01.png)
3. Clique em *Ativar diagnóstico* tooopen Olá página a seguir

   ![imagem do bloco Cofre de Chaves do Azure](./media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics02.png)
4. tooturn em diagnóstico, clique em *na* em *Status*
5. Clique em Olá caixa de seleção *enviar tooLog análise*
6. Selecione um espaço de trabalho existente do Log Analytics ou crie um espaço de trabalho
7. tooenable *AuditEvent* logs, clique em caixa de seleção de saudação em Log
8. Clique em *salvar* tooenable log de saudação do diagnóstico tooLog análise

### <a name="enable-key-vault-diagnostics-using-powershell"></a>Habilitar o diagnóstico do Key Vault usando o PowerShell
saudação de script do PowerShell a seguir fornece um exemplo de como toouse `Set-AzureRmDiagnosticSetting` tooenable log de diagnóstico para o Cofre de chaves:
```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'

Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```



## <a name="review-azure-key-vault-data-collection-details"></a>Veja os detalhes da coleta de dados do Cofre de Chaves do Azure
Solução de Cofre de chaves do Azure coleta logs de diagnóstico diretamente da saudação Cofre de chaves.
Não é necessário toowrite Olá logs tooAzure armazenamento de Blob e nenhum agente é necessária para a coleta de dados.

Olá tabela a seguir mostra os métodos de coleta de dados e outros detalhes sobre como os dados são coletados para o Cofre de chaves do Azure.

| Plataforma | Agente direto | Agente do Systems Center Operations Manager | As tabelas | Operations Manager necessário? | Dados de agente do Operations Manager enviados por meio do grupo de gerenciamento | Frequência de coleta |
| --- | --- | --- | --- | --- | --- | --- |
| As tabelas |  |  |&#8226; |  |  | na chegada |

## <a name="use-azure-key-vault"></a>Usar o Cofre de Chaves do Azure
Depois que você [instalar Olá solução](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview), exibir dados de Cofre de chaves de saudação clicando Olá **Azure Key Vault** lado a lado de saudação **visão geral** página da análise de Log.

![imagem do bloco Cofre de Chaves do Azure](./media/log-analytics-azure-keyvault/log-analytics-keyvault-tile.png)

Depois de clicar em Olá **visão geral** lado a lado, você pode exibir resumos dos seus logs e, em seguida, detalhada em toodetails para Olá categorias a seguir:

* Volume de todas as operações do Cofre de Chaves ao longo do tempo
* Volumes de operação com falha ao longo do tempo
* Latência operacional média por operação
* Qualidade de serviço para operações com o número de saudação de operações que levam mais de 1000 ms e uma lista de operações que levam mais de 1000 ms

![imagem do painel Cofre de Chaves do Azure](./media/log-analytics-azure-keyvault/log-analytics-keyvault01.png)

![imagem do painel Cofre de Chaves do Azure](./media/log-analytics-azure-keyvault/log-analytics-keyvault02.png)

### <a name="tooview-details-for-any-operation"></a>detalhes de tooview para qualquer operação
1. Em Olá **visão geral** , clique em Olá **Azure Key Vault** lado a lado.
2. Em Olá **Azure Key Vault** painel, examine as informações de resumo de saudação em uma das folhas de saudação e, em seguida, clique em uma tooview informações detalhadas sobre ele na página de pesquisa de log de saudação.

    Em qualquer uma das páginas de pesquisa de log hello, você pode exibir os resultados por tempo, resultados detalhados e o histórico de pesquisa de log. Você também pode filtrar pelos resultados de saudação toonarrow facetas.

## <a name="log-analytics-records"></a>Registros do Log Analytics
Olá solução Cofre de chaves do Azure analisa os registros que têm um tipo de **KeyVaults** que são coletados de [AuditEvent logs](../key-vault/key-vault-logging.md) no diagnóstico do Azure.  Propriedades para esses registros são em Olá a tabela a seguir:  

| Propriedade | Descrição |
|:--- |:--- |
| Tipo |*AzureDiagnostics* |
| SourceSystem |*As tabelas* |
| CallerIpAddress |Endereço IP do cliente de saudação que fez a solicitação de saudação |
| Categoria | *AuditEvent* |
| CorrelationId |Um GUID opcional que Olá cliente pode passar toocorrelate logs do lado do cliente com os logs do lado do serviço (Cofre de chaves). |
| DurationMs |Tempo de solicitação de API REST do tooservice hello, em milissegundos. Neste momento não inclui a latência de rede, para que o tempo de saudação que medem no lado do cliente Olá pode não corresponder neste momento. |
| httpStatusCode_d |Código de status HTTP retornado pela solicitação de saudação (por exemplo, *200*) |
| id_s |ID exclusiva da solicitação de saudação |
| identity_claim_appid_g | GUID para a id de aplicativo hello |
| OperationName |Nome da operação hello, conforme documentado no [log de Cofre de chave do Azure](../key-vault/key-vault-logging.md) |
| OperationVersion |Versão da API REST solicitada pelo cliente hello (por exemplo *2015-06-01*) |
| requestUri_s |URI de solicitação de saudação |
| Recurso |Nome do Cofre de chaves Olá |
| ResourceGroup |Grupo de recursos do Cofre de chaves Olá |
| ResourceId |ID do Recurso do Gerenciador de Recursos do Azure. Para logs de Cofre de chaves, esse é o ID de recurso de Cofre de chaves do hello. |
| ResourceProvider |*MICROSOFT.KEYVAULT* |
| ResourceType | *VAULTS* |
| ResultSignature |Status do HTTP (por exemplo, *OK*) |
| ResultType |Resultado da solicitação da API REST (por exemplo, *Êxito*) |
| SubscriptionId |ID de assinatura do Azure da assinatura de saudação contendo Olá Cofre de chaves |

## <a name="migrating-from-hello-old-key-vault-solution"></a>Migrando de solução de Cofre de chaves antiga Olá
Em janeiro de 2017, Olá suporte para a forma de envio de logs do Cofre de chaves tooLog alterada de análise. Essas alterações fornecem Olá vantagens a seguir:
+ Os logs são gravados diretamente tooLog análise sem Olá necessário toouse uma conta de armazenamento
+ Menor latência de tempo de saudação quando os logs são gerados toothem disponíveis na análise de Log
+ Menos etapas de configuração
+ Um formato comum para todos os tipos de diagnóstico do Azure

Olá toouse atualizado Solução:

1. [Configurar o diagnóstico toobe enviado diretamente tooLog análise do Cofre de chaves](#enable-key-vault-diagnostics-in-the-portal)  
2. Habilitar a solução de Cofre de chaves do Azure hello usando Olá processo descrito em [soluções de análise de Log adicionar da saudação Galeria de soluções](log-analytics-add-solutions.md)
3. Atualizar todos os painéis, as consultas salvas ou alertas toouse Olá novo tipo de dados
  + O tipo é a alteração do: KeyVaults tooAzureDiagnostics. Você pode usar o hello ResourceType toofilter tooKey Logs do cofre.
  - Em vez de: `Type=KeyVaults`, use`Type=AzureDiagnostics ResourceType=VAULTS`
  + Campos: (os nomes de campo diferenciam maiúsculas de minúsculas)
  - Para qualquer campo que tenha um sufixo de \_s, \_d, ou \_g em nome do hello, alteração Olá primeiro caractere toolower caso
  - Para qualquer campo que tenha um sufixo de \_o nome, dados de saudação é dividido em campos individuais com base nos nomes de campo Olá aninhado. Por exemplo, Olá UPN do chamador Olá é armazenado em um campo`identity_claim_http_schemas_xmlsoap_org_ws_2005_05_identity_claims_upn_s`
   - TooCallerIPAddress CallerIpAddress de campo alterado
   - O campo RemoteIPCountry não está mais presente
4. Remover Olá *análise de Cofre de chave (preterido)* solução. Se você estiver usando o PowerShell, use `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "KeyVault" -Enabled $false`

Os dados coletados antes de alterar Olá não estiver visível na nova solução de saudação. Você pode continuar tooquery para esse dados usando Olá tipo antigo e nomes de campo.

## <a name="troubleshooting"></a>Solucionar problemas
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a>Próximas etapas
* Use [pesquisas de Log na análise de Log](log-analytics-log-searches.md) tooview informações detalhadas e o Cofre de chaves do Azure.
