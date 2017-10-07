---
title: "Serviços de mídia aaaUpdate depois de implantar o armazenamento de chaves de acesso | Microsoft Docs"
description: "Este artigo oferece orientação sobre como tooupdate Media Services depois de implantar o armazenamento de chaves de acesso."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a892ebb0-0ea0-4fc8-b715-60347cc5c95b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: milanga;cenkdin;juliako
ms.openlocfilehash: 26fa7a75a73397842aaebda59516a00f68ab97f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="update-media-services-after-rolling-storage-access-keys"></a>Atualizar os Serviços de Mídia após implantar chaves de acesso de armazenamento

Quando você cria uma nova conta de serviços de mídia do Azure (AMS), você será solicitado tooselect um armazenamento do Azure da conta que é usada toostore seu conteúdo de mídia. Você pode adicionar tooyour de contas de armazenamento mais de uma conta de serviços de mídia. Este tópico mostra como toorotate chaves de armazenamento. Ele também mostra como as contas de armazenamento tooadd tooa conta de mídia. 

ações de saudação tooperform descritas neste tópico, você deve usar [ARM APIs](https://docs.microsoft.com/rest/api/media/mediaservice) e [Powershell](https://docs.microsoft.com/powershell/resourcemanager/azurerm.media/v0.3.2/azurerm.media).  Para obter mais informações, consulte [como toomanage Azure recursos com o PowerShell e o Gerenciador de recursos](../azure-resource-manager/powershell-azure-resource-manager.md).

## <a name="overview"></a>Visão geral

Quando uma nova conta de armazenamento é criada, o Azure gera duas chaves de acesso de armazenamento de 512 bits, que são usado tooauthenticate acessar tooyour conta de armazenamento. tookeep suas conexões de armazenamento mais seguros, é recomendável tooperiodically regenerar e girar sua chave de acesso de armazenamento. Duas chaves de acesso (primárias e secundárias) são fornecidos na ordem tooenable você toomaintain conexões toohello conta de armazenamento usando um acesso chave enquanto você regenera Olá outra chave de acesso. Esse procedimento também é chamado de "implantação de chaves de acesso".

Serviços de mídia depende de uma chave de armazenamento fornecida tooit. Especificamente, localizadores Olá toostream usado ou baixar seus ativos dependem de chave de acesso de armazenamento especificado hello. Quando uma conta de AMS é criada que leva uma dependência na chave de acesso de armazenamento primário Olá por padrão, mas como um usuário, você pode atualizar a chave de armazenamento de saudação AMS tem. Você deve se certificar de que os serviços de mídia toolet saber quais toouse chave seguindo as etapas descritas neste tópico.  

>[!NOTE]
> Se tiver várias contas de armazenamento, você deverá executar esse procedimento com cada conta de armazenamento. ordem de saudação na qual você rotação de chaves de armazenamento não é fixo. Você pode girar a chave secundária Olá primeiro e, em seguida, Olá primário chave ou vice-versa.
>
> Antes de executar as etapas descritas neste tópico em uma conta de produção, tootest se torná-los em uma conta de pré-produção.
>

## <a name="steps-toorotate-storage-keys"></a>Chaves de armazenamento toorotate etapas 
 
 1. Alteração Olá armazenamento chave primária da conta por meio do cmdlet do powershell hello ou [Azure](https://portal.azure.com/) portal.
 2. Chamar o cmdlet de sincronização AzureRmMediaServiceStorageKeys com os parâmetros apropriados tooforce mídia conta toopick backup das chaves de conta de armazenamento
 
    saudação de exemplo a seguir mostra como toosync chaves toostorage contas.
  
         Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId
  
 3. Aguarde uma hora mais ou menos. Verificar os cenários de streaming Olá estão funcionando.
 4. Alterar a chave secundária de conta de armazenamento por meio do cmdlet do powershell hello ou o portal do Azure.
 5. Chame powershell AzureRmMediaServiceStorageKeys de sincronização com os parâmetros apropriados tooforce mídia conta toopick backup novas chaves de conta de armazenamento. 
 6. Aguarde uma hora mais ou menos. Verificar os cenários de streaming Olá estão funcionando.
 
### <a name="a-powershell-cmdlet-example"></a>Um exemplo de cmdlet do powershell 

Olá exemplo a seguir demonstra como tooget Olá conta de armazenamento e sincronizá-lo com conta Olá AMS.

    $regionName = "West US"
    $resourceGroupName = "SkyMedia-USWest-App"
    $mediaAccountName = "sky"
    $storageAccountName = "skystorage"
    $storageAccountId = "/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Storage/storageAccounts/$storageAccountName"

    Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId

 
## <a name="steps-tooadd-storage-accounts-tooyour-ams-account"></a>Contas de armazenamento de tooadd etapas tooyour AMS conta

Olá tópico a seguir mostra como as contas de armazenamento tooadd tooyour AMS conta: [anexar várias tooa de contas de armazenamento conta do Media Services](meda-services-managing-multiple-storage-accounts.md).

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a>Agradecimentos
Gostaríamos Olá tooacknowledge pessoas que contribuíram para a criação deste documento a seguir: Cenk Dingiloglu, Gada Milão, Seva Titov.
