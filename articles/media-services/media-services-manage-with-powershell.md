---
title: "aaaManage contas de serviços de mídia do Azure com o PowerShell"
description: Saiba como toomanage Azure Media Services contas com cmdlets do PowerShell.
author: Juliako
manager: erikre
editor: 
services: media-services
documentationcenter: 
ms.assetid: 17a10c25-d94f-421c-b6bc-ae0958e2ac96
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/03/2016
ms.author: juliako
ms.openlocfilehash: e8f97bb2393343e45fabf9c437b4fc09f2525dc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-media-services-accounts-with-powershell"></a>Gerenciar contas dos Serviços de Mídia do Azure com o PowerShell
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-create-account.md)
> * [PowerShell](media-services-manage-with-powershell.md)
> * [REST](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> toobe toocreate capaz de uma conta de serviços de mídia do Azure, você deve ter uma conta do Azure. Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Avaliação Gratuita do Azure</a>.
> 
> 

## <a name="overview"></a>Visão geral
Este artigo lista Olá cmdlets do PowerShell do Azure para serviços de mídia do Azure (AMS) na estrutura do Azure Resource Manager hello. Olá cmdlets existe no hello **Microsoft.Azure.Commands.Media** namespace.

## <a name="versions"></a>Versões
**ApiVersion**:   "2015-10-01"

## <a name="new-azurermmediaservice"></a>New-AzureRmMediaService
Cria um serviço de mídia.

### <a name="syntax"></a>Sintaxe
Conjunto de Parâmetros: StorageAccountIdParamSet

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccountId] <string> [-Tags <hashtable>]  [<CommonParameters>]

Conjunto de Parâmetros: StorageAccountsParamSet

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccounts] <PSStorageAccount[]> [-Tags <hashtable>]  [<CommonParameters>]

### <a name="parameters"></a>parâmetros
**-ResourceGroupName &lt;Cadeia de caracteres&gt;**

Especifica o nome de saudação do hello toowhich de grupo de recursos que pertence este serviço de mídia.

| Aliases | nenhum |
| --- | --- |
| Obrigatório? |verdadeiro |
| Position? |0 |
| Valor padrão |nenhum |
| Aceitar entrada do Pipeline? |true(ByPropertyName) |
| Aceitar caracteres curinga? |false |

**-AccountName &lt;Cadeia de caracteres&gt;**

Especifica o nome de saudação do serviço de mídia hello.

| Aliases | Name |
| --- | --- |
| Obrigatório? |verdadeiro |
| Position? |1 |
| Valor padrão |nenhum |
| Aceitar entrada do Pipeline? |false |
| Aceitar caracteres curinga? |false |

**-Location &lt;Cadeia de caracteres&gt;**

Especifica a localização do recurso de saudação do serviço de mídia hello.

| Aliases | nenhum |
| --- | --- |
| Obrigatório? |verdadeiro |
| Position? |2 |
| Valor padrão |nenhum |
| Aceitar entrada do Pipeline? |true(ByPropertyName) |
| Aceitar caracteres curinga? |false |

**-StorageAccountId &lt;Cadeia de caracteres&gt;**

Especifica uma conta de armazenamento primário associado ao serviço de mídia hello.

* Nova conta de armazenamento (criada com hello API do Gerenciador de recursos) somente oferece suportada.
* Olá conta de armazenamento deve existir e tiver Olá mesmo local com o serviço de mídia hello.

| Aliases | nenhum |
| --- | --- |
| Obrigatório? |verdadeiro |
| Position? |3 |
| Valor padrão |nenhum |
| Aceitar entrada do Pipeline? |true(ByPropertyName) |
| Nome do conjunto de parâmetros |StorageAccountIdParamSet |
| Aceitar caracteres curinga? |false |

**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**

Especifica as contas de armazenamento associado ao serviço de mídia hello.

* Nova conta de armazenamento (criada com hello API do Gerenciador de recursos) somente oferece suportada.
* Olá conta de armazenamento deve existir e tiver Olá mesmo local com o serviço de mídia hello.
* Apenas uma conta de armazenamento pode ser especificada como principal.

| Aliases | nenhum |
| --- | --- |
| Obrigatório? |verdadeiro |
| Position? |3 |
| Valor padrão |nenhum |
| Aceitar entrada do Pipeline? |true(ByPropertyName) |
| Nome do conjunto de parâmetros |StorageAccountsParamSet |
| Aceitar caracteres curinga? |false |

**-Tags &lt;Hashtable&gt;**

Especifica uma tabela de hash de marcas de saudação que estão associados com o serviço de mídia hello.

* Exemplo: @{"tag1"="value1";" tag2 "=: valor2"}

| Aliases | nenhum |
| --- | --- |
| Obrigatório? |false |
| Position? |nomeado |
| Valor padrão |nenhum |
| Aceitar entrada do Pipeline? |false |
| Aceitar caracteres curinga? |false |

**&lt;CommandParameters&gt;**

Esse cmdlet oferece suporte a parâmetros comuns de saudação:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction e - WarningVariable.

### <a name="inputs"></a>Entradas
tipo de entrada Hello é tipo de saudação do hello objetos que você pode transmitir toohello cmdlet.

### <a name="outputs"></a>outputs
tipo de saída de Hello é o tipo de saudação de objetos Olá Olá cmdlet emite.

## <a name="set-azurermmediaservice"></a>Set-AzureRmMediaService
Atualiza um serviço de mídia.

### <a name="syntax"></a>Sintaxe
    Set-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Tags <hashtable>] [-StorageAccounts <PSStorageAccount[]>]  [<CommonParameters>]

### <a name="parameters"></a>parâmetros
**-ResourceGroupName &lt;Cadeia de caracteres&gt;**

Especifica o nome de saudação do hello toowhich de grupo de recursos que pertence este serviço de mídia.

| Aliases | nenhum |
| --- | --- |
| Obrigatório? |verdadeiro |
| Position? |0 |
| Valor padrão |nenhum |
| Aceitar entrada do Pipeline? |true(ByPropertyName) |
| Aceitar caracteres curinga? |false |

**-AccountName &lt;Cadeia de caracteres&gt;**

Especifica o nome de saudação do serviço de mídia hello.

| Aliases | Name |
| --- | --- |
| Obrigatório? |verdadeiro |
| Position? |1 |
| Valor padrão |nenhum |
| Aceitar entrada do Pipeline? |true(ByPropertyName) |
| Aceitar caracteres curinga? |Falso |

**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**

Especifica as contas de armazenamento associado ao serviço de mídia hello.

* Nova conta de armazenamento (criada com hello API do Gerenciador de recursos) somente oferece suportada.
* Olá conta de armazenamento deve existir e tiver Olá mesmo local com o serviço de mídia hello.
* Apenas uma conta de armazenamento pode ser especificada como principal.

| Aliases | nenhum |
| --- | --- |
| Obrigatório? |false |
| Position? |nomeado |
| Valor padrão |nenhum |
| Aceitar entrada do Pipeline? |true(ByPropertyName) |
| Nome do conjunto de parâmetros |StorageAccountsParamSet |
| Aceitar caracteres curinga? |false |

**-Tags &lt;Hashtable&gt;**

Especifica uma tabela de hash de marcas de saudação que estão associados esse serviço de mídia.

* marcas de saudação que estão associadas com o serviço de mídia Olá são substituídas com o valor especificado pelo cliente de saudação.

| Aliases | nenhum |
| --- | --- |
| Obrigatório? |false |
| Position? |nomeado |
| Valor padrão |nenhum |
| Aceitar entrada do Pipeline? |true(ByPropertyName) |
| Aceitar caracteres curinga? |false |

**&lt;CommandParameters&gt;**

Esse cmdlet oferece suporte a parâmetros comuns de saudação:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction e - WarningVariable.

### <a name="inputs"></a>Entradas
tipo de entrada Hello é tipo de saudação do hello objetos que você pode transmitir toohello cmdlet.

### <a name="outputs"></a>outputs
tipo de saída de Hello é o tipo de saudação de objetos Olá Olá cmdlet emite.

## <a name="remove-azurermmediaservice"></a>Remove-AzureRmMediaService
Remove um serviço de mídia.

### <a name="syntax"></a>Sintaxe
    Remove-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a>parâmetros
**-ResourceGroupName &lt;Cadeia de caracteres&gt;**

Especifica o nome de saudação do hello toowhich de grupo de recursos que pertence este serviço de mídia.

| Aliases | nenhum |
| --- | --- |
| Obrigatório? |verdadeiro |
| Position? |0 |
| Valor padrão |nenhum |
| Aceitar entrada do Pipeline? |true(ByPropertyName) |
| Aceitar caracteres curinga? |false |

**-AccountName &lt;Cadeia de caracteres&gt;**

Especifica o nome de saudação do serviço de mídia hello.

| Aliases | nenhum |
| --- | --- |
| Obrigatório? |verdadeiro |
| Position? |2 |
| Valor padrão |nenhum |
| Aceitar entrada do Pipeline? |true(ByPropertyName) |
| Aceitar caracteres curinga? |Falso |

**&lt;CommandParameters&gt;**

Esse cmdlet oferece suporte a parâmetros comuns de saudação:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction e - WarningVariable.

### <a name="inputs"></a>Entradas
tipo de entrada Hello é tipo de saudação do hello objetos que você pode transmitir toohello cmdlet.

### <a name="outputs"></a>outputs
tipo de saída de Hello é o tipo de saudação de objetos Olá Olá cmdlet emite.

## <a name="get-azurermmediaservice"></a>Get-AzureRmMediaService
Obtém todos os serviços de mídia em um grupo de recursos ou um serviço de mídia com um determinado nome.

### <a name="syntax"></a>Sintaxe
ParameterSet: ResourceGroupParameterSet

    Get-AzureRmMediaService [-ResourceGroupName] <string>  [<CommonParameters>]    

ParameterSet: AccountNameParameterSet

    Get-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a>parâmetros
**-ResourceGroupName &lt;Cadeia de caracteres&gt;**

Especifica o nome de saudação do hello toowhich de grupo de recursos que pertence este serviço de mídia.

| Aliases | nenhum |
| --- | --- |
| Obrigatório? |verdadeiro |
| Position? |0 |
| Valor padrão |nenhum |
| Aceitar entrada do Pipeline? |true(ByPropertyName) |
| Nome do conjunto de parâmetros |ResourceGroupParameterSet, AccountNameParameterSet |

Aceitar caracteres curinga?   false

**-AccountName &lt;Cadeia de caracteres&gt;**

Especifica o nome de saudação do serviço de mídia hello.

| Aliases | nenhum |
| --- | --- |
| Obrigatório? |verdadeiro |
| Position? |1 |
| Valor padrão |nenhum |
| Aceitar entrada do Pipeline? |true(ByPropertyName) |
| Nome do conjunto de parâmetros |AccountNameParameterSet |
| Aceitar caracteres curinga? |false |

**&lt;CommandParameters&gt;**

Esse cmdlet oferece suporte a parâmetros comuns de saudação:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction e - WarningVariable.

### <a name="inputs"></a>Entradas
tipo de entrada Hello é tipo de saudação do hello objetos que você pode transmitir toohello cmdlet.

### <a name="outputs"></a>outputs
tipo de saída de Hello é o tipo de saudação de objetos Olá Olá cmdlet emite.

## <a name="get-azurermmediaservicekeys"></a>Get-AzureRmMediaServiceKeys
Obtém as chaves de um serviço de mídia.

### <a name="syntax"></a>Sintaxe
    Get-AzureRmMediaServiceKeys [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a>parâmetros
**-ResourceGroupName &lt;Cadeia de caracteres&gt;**

Especifica o nome de saudação do hello toowhich de grupo de recursos que pertence este serviço de mídia.

| Aliases | nenhum |
| --- | --- |
| Obrigatório? |verdadeiro |
| Position? |0 |
| Valor padrão |nenhum |
| Aceitar entrada do Pipeline? |true(ByPropertyName) |
| Aceitar caracteres curinga? |false |

**-AccountName &lt;Cadeia de caracteres&gt;**

Especifica o nome de saudação do serviço de mídia hello.

| Aliases | nenhum |
| --- | --- |
| Obrigatório? |verdadeiro |
| Position? |1 |
| Valor padrão |nenhum |
| Aceitar entrada do Pipeline? |true(ByPropertyName) |
| Aceitar caracteres curinga? |false |

**&lt;CommandParameters&gt;**

Esse cmdlet oferece suporte a parâmetros comuns de saudação:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction e - WarningVariable.

### <a name="inputs"></a>Entradas
tipo de entrada Hello é tipo de saudação do hello objetos que você pode transmitir toohello cmdlet.

### <a name="outputs"></a>outputs
tipo de saída de Hello é o tipo de saudação de objetos Olá Olá cmdlet emite.

## <a name="set-azurermmediaservicekey"></a>Set-AzureRmMediaServiceKey
Regenera uma chave primária ou secundária de um serviço de mídia.

### <a name="syntax"></a>Sintaxe
    Set-AzureRmMediaServiceKey [-ResourceGroupName] <string> [-AccountName] <string> [-KeyType] <KeyType> {Primary | Secondary}  [<CommonParameters>]

### <a name="parameters"></a>parâmetros
**-ResourceGroupName &lt;Cadeia de caracteres&gt;**

Especifica o nome de saudação do hello toowhich de grupo de recursos que pertence este serviço de mídia.

| Aliases | nenhum |
| --- | --- |
| Obrigatório? |verdadeiro |
| Position? |0 |
| Valor padrão |nenhum |
| Aceitar entrada do Pipeline? |true(ByPropertyName) |
| Aceitar caracteres curinga? |false |

**-AccountName &lt;Cadeia de caracteres&gt;**

Especifica o nome de saudação do serviço de mídia hello.

| Aliases | nenhum |
| --- | --- |
| Obrigatório? |verdadeiro |
| Position? |1 |
| Valor padrão |nenhum |
| Aceitar entrada do Pipeline? |true(ByPropertyName) |
| Aceitar caracteres curinga? |false |

**-KeyType &lt;KeyType&gt;**

Especifica o tipo de serviço de mídia Olá chave hello.

* Primária ou Secundária

| Aliases | nenhum |
| --- | --- |
| Obrigatório? |verdadeiro |
| Position? |2 |
| Valor padrão |nenhum |
| Aceitar entrada do Pipeline? |false |
| Aceitar caracteres curinga? |false |

**&lt;CommandParameters&gt;**

Esse cmdlet oferece suporte a parâmetros comuns de saudação:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction e - WarningVariable.

### <a name="inputs"></a>Entradas
tipo de entrada Hello é tipo de saudação do hello objetos que você pode transmitir toothe cmdlet.

### <a name="outputs"></a>outputs
tipo de saída de Hello é o tipo de saudação de objetos Olá Olá cmdlet emite.

## <a name="sync-azurermmediaservicestoragekeys"></a>Sync-AzureRmMediaServiceStorageKeys
Sincroniza as chaves de conta de armazenamento para uma conta de armazenamento associado ao serviço de mídia hello.

### <a name="syntax"></a>Sintaxe
    Sync-AzureRmMediaServiceStorageKeys [-ResourceGroupName] <string> [-MediaServiceAccountName] <string>    [-StorageAccountId] <string>  [<CommonParameters>]

### <a name="parameters"></a>parâmetros
**-ResourceGroupName &lt;Cadeia de caracteres&gt;**

Especifica o nome de saudação do hello toowhich de grupo de recursos que pertence este serviço de mídia.

| Aliases | nenhum |
| --- | --- |
| Obrigatório? |verdadeiro |
| Position? |0 |
| Valor padrão |nenhum |
| Aceitar entrada do Pipeline? |true(ByPropertyName) |
| Aceitar caracteres curinga? |false |

**-AccountName &lt;Cadeia de caracteres&gt;**

Especifica o nome de saudação do serviço de mídia hello.

| Aliases | nenhum |
| --- | --- |
| Obrigatório? |verdadeiro |
| Position? |1 |
| Valor padrão |nenhum |
| Aceitar entrada do Pipeline? |true(ByPropertyName) |
| Aceitar caracteres curinga? |false |

**-StorageAccountId &lt;Cadeia de caracteres&gt;**

Especifica a conta de armazenamento de saudação associada ao serviço de mídia hello.

| Aliases | ID |
| --- | --- |
| Obrigatório? |verdadeiro |
| Position? |2 |
| Valor padrão |nenhum |
| Aceitar entrada do Pipeline? |true(ByPropertyName) |
| Aceitar caracteres curinga? |false |

**&lt;CommandParameters&gt;**

Esse cmdlet oferece suporte a parâmetros comuns de saudação:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction e - WarningVariable.

### <a name="inputs"></a>Entradas
tipo de entrada Hello é tipo de saudação do hello objetos que você pode transmitir toohello cmdlet.

### <a name="outputs"></a>outputs
tipo de saída de Hello é o tipo de saudação de objetos Olá Olá cmdlet emite.

## <a name="next-step"></a>Próxima etapa
Confira os roteiros de aprendizagem dos Serviços de Mídia.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

