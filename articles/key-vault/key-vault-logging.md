---
title: aaaAzure log de Cofre de chave | Microsoft Docs
description: "Use este tutorial toohelp começar com o Cofre de chaves do Azure log."
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 43f96a2b-3af8-4adc-9344-bc6041fface8
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: cabailey
ms.openlocfilehash: 38a173297948748bef45e3d857c06b50b3e21e74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-logging"></a>Logs do Cofre da Chave do Azure
O Cofre da Chave do Azure está disponível na maioria das regiões. Para obter mais informações, consulte Olá [página de preços do Cofre de chaves](https://azure.microsoft.com/pricing/details/key-vault/).

## <a name="introduction"></a>Introdução
Depois de criar um ou mais cofres de chaves, provavelmente você desejará toomonitor como e quando sua chave de cofres são acessados e por quem. Você pode fazer isso ao habilitar o log para o Cofre da Chave, que salva as informações em uma conta de armazenamento do Azure fornecida por você. Um novo contêiner chamado **insights-logs-auditevent** é automaticamente criado para a conta de armazenamento especificada e você poderá usar essa mesma conta de armazenamento para a coleta de logs de vários cofres da chave.

Você pode acessar suas informações de registro em log no máximo, 10 minutos após a chave de saudação cofre a operação. Na maioria dos casos, será mais rápido do que isso.  É o tooyou toomanage seus logs de sua conta de armazenamento:

* Use seus logs de toosecure de métodos de controle de acesso do Azure standard ao restringir quem pode acessá-los.
* Exclua logs que você não deseja mais tookeep na sua conta de armazenamento.

Use este tutorial toohelp começar com o Azure Key Vault log toocreate sua conta de armazenamento, habilitar o log e interpretar as informações de log Olá coletadas.  

> [!NOTE]
> Este tutorial não inclui instruções sobre como toocreate chave cofres, chaves ou segredos. Para obter essas informações, confira [Introdução ao Cofre da Chave do Azure](key-vault-get-started.md). Ou, para obter instruções de Interface de linha de comando entre diferentes plataformas, consulte [este tutorial equivalente](key-vault-manage-with-cli2.md).
>
> No momento, você não pode configurar o Cofre de chaves do Azure no portal do Azure de saudação. Em vez disso, use estas instruções do PowerShell do Azure.
>
>

Para obter informações gerais sobre o Cofre da Chave do Azure, consulte [O que é o Cofre da Chave do Azure?](key-vault-whatis.md)

## <a name="prerequisites"></a>Pré-requisitos
toocomplete neste tutorial, você deve ter Olá a seguir:

* Um cofre da chave existente que você esteja usando.  
* Azure PowerShell, **versão mínima: 1.0.1**. tooinstall PowerShell do Azure e associá-lo a sua assinatura do Azure, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview). Se você já tiver instalado o PowerShell do Azure e não souber a versão de hello, no console do Azure PowerShell hello, digite `(Get-Module azure -ListAvailable).Version`.  
* Armazenamento suficiente no Azure para seus logs do Cofre da Chave.

## <a id="connect"></a>Conecte-se tooyour assinaturas
Iniciar uma sessão do PowerShell do Azure e entrar tooyour conta do Azure com hello comando a seguir:  

    Login-AzureRmAccount

Na janela de pop-up do navegador hello, insira seu nome de usuário da conta do Azure e a senha. O Azure PowerShell obterá todas as assinaturas de saudação que estão associadas com essa conta e, por padrão, usa Olá primeiro.

Se você tiver várias assinaturas, talvez seja necessário toospecify um específico que foi usado toocreate seu Cofre de chaves do Azure. Digite hello assinaturas de saudação toosee para sua conta a seguir:

    Get-AzureRmSubscription

Em seguida, toospecify Olá assinatura associada com o Cofre de chaves que fizerem logon, tipo:

    Set-AzureRmContext -SubscriptionId <subscription ID>

> [!NOTE]
> Esta é uma etapa importante e será especialmente útil se você tiver várias assinaturas associadas à sua conta. Você pode receber um erro tooregister Insights se esta etapa será ignorada.
>   
>

Para obter mais informações sobre como configurar o Azure PowerShell, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).

## <a id="storage"></a>Criar uma nova conta de armazenamento para seus logs
Embora você possa usar uma conta de armazenamento existente para seus logs, vamos criar uma nova conta de armazenamento será dedicado tooKey cofre logs. Para sua conveniência para quando temos toospecify isso mais tarde, armazenamos detalhes de saudação em uma variável chamada **sa**.

Para facilidade de gerenciamento, também usaremos Olá mesmo grupo de recursos como Olá que contenha o nosso Cofre de chaves. De saudação [tutorial de Introdução](key-vault-get-started.md), esse grupo de recursos é denominado **ContosoResourceGroup** e continuaremos a localização do toouse Olá Ásia Oriental. Substitua esses valores pelos seus, conforme aplicável:

    $sa = New-AzureRmStorageAccount -ResourceGroupName ContosoResourceGroup -Name contosokeyvaultlogs -Type Standard_LRS -Location 'East Asia'


> [!NOTE]
> Se você decidir toouse uma conta de armazenamento existente, ele deve usar Olá a mesma assinatura conforme seu Cofre de chaves e ele devem usar modelo de implantação do Gerenciador de recursos de hello, em vez de modelo de implantação clássico hello.
>
>

## <a id="identify"></a>Identificar o Cofre de chaves Olá para seus logs
Em nosso tutorial de Introdução, o nome do Cofre de chaves foi **ContosoKeyVault**, portanto, continuaremos toouse que nomear e armazenar os detalhes de saudação em uma variável chamada **kv**:

    $kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'


## <a id="enable"></a>Habilitar o registro em log
tooenable registro em log para o Cofre de chaves, usaremos Olá conjunto AzureRmDiagnosticSetting cmdlet, juntamente com variáveis Olá criada para a nova conta de armazenamento e nosso cofre da chave. Também vamos definir Olá **-habilitado** sinalizador muito**$true** e defina Olá categoria tooAuditEvent (Olá somente categoria para registro de Cofre de chaves):

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent

saída de Hello para isso inclui:

    StorageAccountId   : /subscriptions/<subscription-GUID>/resourceGroups/ContosoResourceGroup/providers/Microsoft.Storage/storageAccounts/ContosoKeyVaultLogs
    ServiceBusRuleId   :
    StorageAccountName :
        Logs
        Enabled           : True
        Category          : AuditEvent
        RetentionPolicy
        Enabled : False
        Days    : 0


Isso confirma que o log está ativado para seu Cofre de chaves, salvar a conta de armazenamento tooyour informações.

Opcionalmente, você também pode definir a política de retenção para os logs, de modo que os logs mais antigos sejam automaticamente excluídos. Por exemplo, definir a política de retenção usando **- RetentionEnabled** sinalizador muito**$true** e defina **- RetentionInDays** parâmetro muito**90** para Se mais de 90 dias de logs serão excluídas automaticamente.

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent -RetentionEnabled $true -RetentionInDays 90

O que é registrado em log:

* Todas as solicitações de API REST autenticadas são registradas, o que inclui as solicitações que falharam devido a permissões de acesso, erros do sistema ou solicitações inválidas.
* Operações em chave Olá cofre em si, que inclui a criação, exclusão, políticas de acesso do Cofre de chaves de configuração, e atualizar os atributos de Cofre de chaves, como marcas.
* Operações em chaves e segredos no cofre de chaves hello, que inclui criar, modificar ou excluir essas chaves ou segredos; operações como entrada, verifique se, criptografar, descriptografar, encapsular e descodificar chaves, obter segredos, listar chaves e segredos e suas versões.
* Solicitações não autenticadas que resultam em uma resposta 401. Por exemplo, solicitações que não têm um token de portador, estão malformadas ou expiradas ou têm um token inválido.  

## <a id="access"></a>Acessar seus logs
Logs de Cofre de chaves são armazenados em Olá **insights-logs-auditevent** contêiner na conta de armazenamento Olá fornecida. toolist todos os blobs Olá nesse contêiner, digite:

Primeiro, crie uma variável para o nome do contêiner de saudação. Isso será usado restante Olá Olá passo a passo.

    $container = 'insights-logs-auditevent'

toolist todos os blobs Olá nesse contêiner, digite:

    Get-AzureStorageBlob -Container $container -Context $sa.Context
saída de Hello ficará toothis algo semelhante:

**URI de contêiner: https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**

**Nome**

- - -
**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**

**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**

**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json****

Como você pode ver nessa saída, blobs Olá seguem uma convenção de nomenclatura: **resourceId =<ARM resource ID>/y =<year>/m =<month>/d =<day of month>/h =<hour>/m =<minute>/filename.json**

os valores de data e hora Olá usam UTC.

Como hello mesma conta de armazenamento pode ser logs toocollect usado para vários recursos, hello ID de recurso completo no nome do blob Olá é muito útil tooaccess ou blobs Olá apenas de download que você precisa. Mas antes de fazer isso, primeiro abordaremos como toodownload todos Olá blobs.

Primeiro, crie uma saudação de toodownload pasta blobs. Por exemplo:

    New-Item -Path 'C:\Users\username\ContosoKeyVaultLogs' -ItemType Directory -Force

Em seguida, obtenha uma lista de todos os blobs:  

    $blobs = Get-AzureStorageBlob -Container $container -Context $sa.Context

Direcionar essa lista por meio de blobs de saudação do 'Get-AzureStorageBlobContent' toodownload em nossa pasta de destino:

    $blobs | Get-AzureStorageBlobContent -Destination 'C:\Users\username\ContosoKeyVaultLogs'

Quando você executa esse comando segundo, Olá  **/**  delimitador em nomes de blob Olá criar uma estrutura de pasta completo na pasta de destino Olá, e essa estrutura será usados toodownload e repositório Olá blobs como arquivos.

tooselectively baixar blobs, use caracteres curinga. Por exemplo:

* Se você tiver vários cofres de chaves e deseja logs toodownload para apenas um cofre de chaves, chamado CONTOSOKEYVAULT3:

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/VAULTS/CONTOSOKEYVAULT3
* Se você tiver vários grupos de recursos e quiser logs toodownload para apenas um grupo de recursos, use `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/RESOURCEGROUPS/CONTOSORESOURCEGROUP3/*'
* Se você quiser toodownload todos os logs de saudação mês de saudação de janeiro de 2016, use `-Blob '*/year=2016/m=01/*'`:

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/year=2016/m=01/*'

Você está agora pronto toostart observando o que há no hello logs. Mas antes de passar para que, dois parâmetros mais para Get-AzureRmDiagnosticSetting que talvez você precise tooknow:

* status de saudação tooquery de configurações de diagnóstico para o recurso de Cofre de chaves:`Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`
* log de toodisable para o recurso de Cofre de chaves:`Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`

## <a id="interpret"></a>Interpretar os logs do Cofre de Chave
Os blobs individuais são armazenados como texto, formatados como um blob JSON. Este é um exemplo de entrada de log a partir da execução de `Get-AzureRmKeyVault -VaultName 'contosokeyvault'`:

    {
        "records":
        [
            {
                "time": "2016-01-05T01:32:01.2691226Z",
                "resourceId": "/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSOGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT",
                "operationName": "VaultGet",
                "operationVersion": "2015-06-01",
                "category": "AuditEvent",
                "resultType": "Success",
                "resultSignature": "OK",
                "resultDescription": "",
                "durationMs": "78",
                "callerIpAddress": "104.40.82.76",
                "correlationId": "",
                "identity": {"claim":{"http://schemas.microsoft.com/identity/claims/objectidentifier":"d9da5048-2737-4770-bd64-XXXXXXXXXXXX","http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn":"live.com#username@outlook.com","appid":"1950a258-227b-4e31-a9cf-XXXXXXXXXXXX"}},
                "properties": {"clientInfo":"azure-resource-manager/2.0","requestUri":"https://control-prod-wus.vaultcore.azure.net/subscriptions/361da5d4-a47a-4c79-afdd-XXXXXXXXXXXX/resourcegroups/contosoresourcegroup/providers/Microsoft.KeyVault/vaults/contosokeyvault?api-version=2015-06-01","id":"https://contosokeyvault.vault.azure.net/","httpStatusCode":200}
            }
        ]
    }


Olá tabela a seguir lista nomes de campo hello e descrições.

| Nome do campo | Descrição |
| --- | --- |
| tempo real |Data e hora (UTC). |
| resourceId |ID do Recurso do Gerenciador de Recursos do Azure. Para logs de Cofre de chaves, é sempre ID de recurso de Cofre de chaves do hello. |
| operationName |Nome da operação hello, conforme documentado na tabela a seguir hello. |
| operationVersion |Esta é a versão de API REST de saudação solicitada pelo cliente hello. |
| categoria |Para logs de Cofre de chaves, AuditEvent é um valor único e disponível hello. |
| resultType |Resultado da solicitação da API REST. |
| resultSignature |Código de status HTTP. |
| resultDescription |Descrição adicional sobre o resultado de hello, quando disponível. |
| durationMs |Tempo de solicitação de API REST do tooservice hello, em milissegundos. Isso não inclui a latência de rede Olá, para que medir no lado do cliente de saudação do tempo de saudação pode não corresponder neste momento. |
| callerIpAddress |Endereço IP do cliente de saudação que fez a solicitação de saudação. |
| correlationId |Um GUID opcional que Olá cliente pode passar toocorrelate logs do lado do cliente com os logs do lado do serviço (Cofre de chaves). |
| identidade |Identidade do token Olá apresentado ao fazer a solicitação de API REST de saudação. Isso geralmente é um "usuário", uma "entidade de serviço" ou uma combinação "usuário+appId", como no caso de uma solicitação, resultado de um cmdlet do Azure PowerShell. |
| propriedades |Este campo contém informações diferentes com base na operação de saudação (operationName). Na maioria dos casos, contém informações de cliente (Olá useragent cadeia de caracteres passada pelo cliente Olá), Olá exata URI de solicitação de API REST e o código de status HTTP. Além disso, quando um objeto é retornado como resultado de uma solicitação (por exemplo, KeyCreate ou VaultGet) também conterá Olá URI de chave (como "id"), o URI do cofre ou o URI do segredo. |

Olá **operationName** valores de campo estão no formato de ObjectVerb. Por exemplo:

* Todas as operações do Cofre de chaves têm Olá ' cofre`<action>`' formato, como `VaultGet` e `VaultCreate`.
* Todas as operações de chave têm Olá ' chave`<action>`' formato, como `KeySign` e `KeyList`.
* Todas as operações de segredo têm Olá ' segredo`<action>`' formato, como `SecretGet` e `SecretListVersions`.

Olá, a tabela a seguir lista operationName hello e comando correspondente de API REST.

| operationName | Comando da API REST |
| --- | --- |
| Autenticação |Via ponto de extremidade do Active Directory do Azure |
| VaultGet |[Obter informações sobre um cofre de chaves](https://msdn.microsoft.com/en-us/library/azure/mt620026.aspx) |
| VaultPut |[Criar ou atualizar um cofre de chaves](https://msdn.microsoft.com/en-us/library/azure/mt620025.aspx) |
| VaultDelete |[Excluir um cofre de chaves](https://msdn.microsoft.com/en-us/library/azure/mt620022.aspx) |
| VaultPatch |[Atualizar um cofre da chave](https://msdn.microsoft.com/library/azure/mt620025.aspx) |
| VaultList |[Listar todos os cofres de chaves em um grupo de recursos](https://msdn.microsoft.com/en-us/library/azure/mt620027.aspx) |
| KeyCreate |[Criar uma chave](https://msdn.microsoft.com/en-us/library/azure/dn903634.aspx) |
| KeyGet |[Obter informações sobre uma chave](https://msdn.microsoft.com/en-us/library/azure/dn878080.aspx) |
| KeyImport |[Importar uma chave para um cofre](https://msdn.microsoft.com/en-us/library/azure/dn903626.aspx) |
| KeyBackup |[Fazer backup de uma chave](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx). |
| KeyDelete |[Excluir uma chave](https://msdn.microsoft.com/en-us/library/azure/dn903611.aspx) |
| KeyRestore |[Restaurar uma chave](https://msdn.microsoft.com/en-us/library/azure/dn878106.aspx) |
| KeySign |[Assinar com uma chave](https://msdn.microsoft.com/en-us/library/azure/dn878096.aspx) |
| KeyVerify |[Verificar com uma chave](https://msdn.microsoft.com/en-us/library/azure/dn878082.aspx) |
| KeyWrap |[Encapsular uma chave](https://msdn.microsoft.com/en-us/library/azure/dn878066.aspx) |
| KeyUnwrap |[Desencapsular uma chave](https://msdn.microsoft.com/en-us/library/azure/dn878079.aspx) |
| KeyEncrypt |[Criptografar com uma chave](https://msdn.microsoft.com/en-us/library/azure/dn878060.aspx) |
| KeyDecrypt |[Descriptografar com uma chave](https://msdn.microsoft.com/en-us/library/azure/dn878097.aspx) |
| KeyUpdate |[Atualizar uma chave](https://msdn.microsoft.com/en-us/library/azure/dn903616.aspx) |
| KeyList |[Lista Olá chaves em um cofre](https://msdn.microsoft.com/en-us/library/azure/dn903629.aspx) |
| KeyListVersions |[Listar versões da saudação de uma chave](https://msdn.microsoft.com/en-us/library/azure/dn986822.aspx) |
| SecretSet |[Criar um segredo](https://msdn.microsoft.com/en-us/library/azure/dn903618.aspx) |
| SecretGet |[Obter um segredo](https://msdn.microsoft.com/en-us/library/azure/dn903633.aspx) |
| SecretUpdate |[Atualizar um segredo](https://msdn.microsoft.com/en-us/library/azure/dn986818.aspx) |
| SecretDelete |[Excluir um segredo](https://msdn.microsoft.com/en-us/library/azure/dn903613.aspx) |
| SecretList |[Listar segredos em um cofre](https://msdn.microsoft.com/en-us/library/azure/dn903614.aspx) |
| SecretListVersions |[Listar versões de um segredo](https://msdn.microsoft.com/en-us/library/azure/dn986824.aspx) |

## <a id="loganalytics"></a>Usar Log Analytics

Você pode usar a solução de Cofre de chaves do Azure de saudação em tooreview de análise de logs do Azure Key Vault AuditEvent logs. Para obter mais informações, incluindo como tooset isso, consulte [solução de Cofre de chaves do Azure na análise de Log](../log-analytics/log-analytics-azure-key-vault.md). Este artigo também contém instruções se você precisar toomigrate da solução Cofre de chaves antiga Olá que foi fornecida durante a visualização de análise de Log hello, em que você primeiro roteado tooan seus logs conta de armazenamento do Azure e configurado tooread de análise de Log a partir daí.

## <a id="next"></a>Próximas etapas
Para obter um tutorial que usa o Cofre de Chaves do Azure em um aplicativo Web, confira [Usar o Cofre de Chaves do Azure em um Aplicativo Web](key-vault-use-from-web-application.md).

Para referências de programação, consulte [Olá guia do desenvolvedor do Azure Key Vault](key-vault-developers-guide.md).

Para obter uma lista dos cmdlets do Azure PowerShell 1.0 para o Cofre de Chaves do Azure, confira [Cmdlets do Cofre de Chaves do Azure](/powershell/module/azurerm.keyvault/#key_vault).

Para obter um tutorial sobre rotação de chaves e o log de auditoria com o Cofre de chaves do Azure, consulte [como toosetup Cofre de chaves com final tooend chave rotação e auditoria](key-vault-key-rotation-log-monitoring.md).
