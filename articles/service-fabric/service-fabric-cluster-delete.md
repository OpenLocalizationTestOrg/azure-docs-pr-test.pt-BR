---
title: aaaDelete um Azure cluster e seus recursos | Microsoft Docs
description: "Saiba como delete toocompletely uma malha de serviço de cluster ou excluir grupo de recursos de saudação contendo cluster hello ou excluindo seletivamente recursos."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: de422950-2d22-4ddb-ac47-dd663a946a7e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/24/2017
ms.author: chackdan
ms.openlocfilehash: 5c15a4184644da715cd69397f2150de86ab433ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="delete-a-service-fabric-cluster-on-azure-and-hello-resources-it-uses"></a>Excluir um cluster do Service Fabric nos recursos do Azure e hello usa
Um cluster do Service Fabric é composto por muitos outros recursos do Azure além de recurso de cluster toohello propriamente dito. Para toocompletely exclua um cluster do Service Fabric também é necessário toodelete que todos Olá recursos que é formado.
Você tem duas opções: grupo de recursos ou excluir Olá Olá cluster está em (que exclui o recurso de cluster hello e todos os outros recursos no grupo de recursos de saudação) ou excluir especificamente o recurso de cluster de saudação e associado recursos (mas não outras recursos no grupo de recursos de saudação).

> [!NOTE]
> Excluindo o recurso de cluster Olá **não** excluir todos os Olá outros recursos que o cluster do Service Fabric é composto de.
> 
> 

## <a name="delete-hello-entire-resource-group-rg-that-hello-service-fabric-cluster-is-in"></a>Excluir grupo de recursos inteiro da saudação (RG) que Olá malha do serviço de cluster está em
Isso é Olá tooensure de maneira mais fácil que você exclua todos os recursos de saudação associados ao cluster, incluindo o grupo de recursos de saudação. Você pode excluir o grupo de recursos de saudação usando o PowerShell ou por meio de saudação portal do Azure. Se seu grupo de recursos tiver recursos que não estão relacionadas tooService cluster de malha, você pode excluir recursos específicos.

### <a name="delete-hello-resource-group-using-azure-powershell"></a>Excluir grupo de recursos de saudação usando o PowerShell do Azure
Você também pode excluir o grupo de recursos de saudação executando Olá seguintes cmdlets do PowerShell do Azure. Certifique-se de que o Azure PowerShell 1.0 ou superior está instalado em seu computador. Se você não tiver feito isso antes, execute as etapas de saudação descritas em [como tooinstall e configurar o Azure PowerShell.](/powershell/azure/overview)

Abra uma janela do PowerShell e execute Olá PS cmdlets a seguir:

```powershell
Login-AzureRmAccount

Remove-AzureRmResourceGroup -Name <name of ResouceGroup> -Force
```

Você obterá uma exclusão de saudação do prompt tooconfirm se você não usou Olá *-Force* opção. Em confirmação Olá RG e todos os recursos de saudação que ele contém são excluídos.

### <a name="delete-a-resource-group-in-hello-azure-portal"></a>Excluir um grupo de recursos em Olá portal do Azure
1. Logon toohello [portal do Azure](https://portal.azure.com).
2. Navegue cluster do Service Fabric toohello toodelete desejado.
3. Clique em Olá nome do grupo de recursos na página do essentials cluster hello.
4. Isso traz Olá **princípios básicos de grupo de recursos** página.
5. Clique em **Excluir**.
6. Siga as instruções de saudação em que página toocomplete Olá a exclusão do grupo de recursos de saudação.

![Exclusão do Grupo de Recursos][ResourceGroupDelete]

## <a name="delete-hello-cluster-resource-and-hello-resources-it-uses-but-not-other-resources-in-hello-resource-group"></a>Excluir o recurso de cluster hello e Olá recursos usados por ele, mas não outros recursos no grupo de recursos de saudação
Se seu grupo de recursos tem apenas os recursos relacionados toohello malha do serviço de cluster deseja toodelete, ele é mais fácil toodelete Olá todo recurso grupo. Se você desejar que recursos de saudação do tooselectively excluir um por um no seu grupo de recursos, em seguida, siga estas etapas.

Se você implantou o cluster usando o portal de saudação ou usando um dos modelos de serviço Gerenciador de recursos de malha Olá Olá da Galeria de modelos, todos os recursos de Olá Olá cluster usará são marcados com hello duas marcas a seguir. Você pode usar toodecide quais recursos você deseja toodelete.

***Marca n º 1:*** chave = clusterName, valor = 'nome do cluster de saudação'

***Marcação n º 2:*** Chave = resourceName, Valor = ServiceFabric

### <a name="delete-specific-resources-in-hello-azure-portal"></a>Excluir recursos específicos no hello portal do Azure
1. Logon toohello [portal do Azure](https://portal.azure.com).
2. Navegue cluster do Service Fabric toohello toodelete desejado.
3. Vá muito**todas as configurações de** na folha do essentials hello.
4. Clique em **marcas** em **gerenciamento de recursos** na folha de configurações de saudação.
5. Clique em uma saudação **marcas** em Olá marcas folha tooget uma lista de todos os recursos de saudação com essa marca.
   
    ![Marcações de recursos][ResourceTags]
6. Uma vez que a lista de saudação de recursos marcados, clique em cada um dos recursos de saudação e excluí-los.
   
    ![Recursos marcados][TaggedResources]

### <a name="delete-hello-resources-using-azure-powershell"></a>Excluir recursos hello usando o PowerShell do Azure
Você pode excluir recursos Olá um por um executando Olá seguintes cmdlets do PowerShell do Azure. Certifique-se de que o Azure PowerShell 1.0 ou superior está instalado em seu computador. Se você não tiver feito isso antes, execute as etapas de saudação descritas em [como tooinstall e configurar o Azure PowerShell.](/powershell/azure/overview)

Abra uma janela do PowerShell e execute Olá PS cmdlets a seguir:

```powershell
Login-AzureRmAccount
```
Para cada um dos recursos de saudação você deseja toodelete, execute o seguinte hello:

```powershell
Remove-AzureRmResource -ResourceName "<name of hello Resource>" -ResourceType "<Resource Type>" -ResourceGroupName "<name of hello resource group>" -Force
```

recurso de cluster em Olá toodelete, execute Olá seguinte:

```powershell
Remove-AzureRmResource -ResourceName "<name of hello Resource>" -ResourceType "Microsoft.ServiceFabric/clusters" -ResourceGroupName "<name of hello resource group>" -Force
```

## <a name="next-steps"></a>Próximas etapas
Saudação de leitura após tooalso Saiba mais sobre particionamento serviços e atualizar um cluster:

* [Saiba mais sobre atualizações de cluster](service-fabric-cluster-upgrade.md)
* [Saiba mais sobre os serviços com estado de particionamento para escala máxima](service-fabric-concepts-partitioning.md)

<!--Image references-->
[ResourceGroupDelete]: ./media/service-fabric-cluster-delete/ResourceGroupDelete.PNG

[ResourceTags]: ./media/service-fabric-cluster-delete/ResourceTags.png

[TaggedResources]: ./media/service-fabric-cluster-delete/TaggedResources.PNG
