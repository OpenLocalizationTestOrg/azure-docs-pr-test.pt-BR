---
title: "aaaCreate um servidor de serviços de análise do Azure usando o PowerShell | Microsoft Docs"
description: Saiba como toocreate um Azure Analysis Services server usando o PowerShell
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 08/01/2017
ms.author: owend
ms.custom: mvc
ms.openlocfilehash: 269b78983410f773d47c4cea34d6d353b19f9e91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-analysis-services-server-by-using-powershell"></a>Criar a um servidor do Azure Analysis Services usando PowerShell

Este guia de início rápido descreve como usar o PowerShell do hello toocreate de linha de comando um servidor do Azure Analysis Services em um [grupo de recursos do Azure](../azure-resource-manager/resource-group-overview.md) na sua assinatura do Azure.

Esta tarefa exige o módulo do Azure PowerShell, versão 4.0 ou posterior. versão de hello toofind, execute ` Get-Module -ListAvailable AzureRM`. tooinstall ou atualização, consulte [instalar o módulo PowerShell Azure](/powershell/azure/install-azurerm-ps). 

> [!NOTE]
> Criar um servidor pode resultar em um novo serviço faturável. mais, consulte toolearn [preços do Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).

## <a name="prerequisites"></a>Pré-requisitos
toocomplete este guia de início rápido, você precisa:

* **Assinatura do Azure**: visite [avaliação gratuita do Azure](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate uma conta.
* **Azure Active Directory**: sua assinatura deve estar associada a um locatário do Azure Active Directory, e você precisa ter uma conta nesse diretório. mais, consulte toolearn [permissões de usuário e autenticação](analysis-services-manage-users.md).

## <a name="import-azurermanalysisservices-module"></a>Importar o módulo AzureRm.AnalysisServices
toocreate um servidor em sua assinatura, você usar Olá [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices) módulo de componente. Carregar o módulo de AzureRm.AnalysisServices de saudação em sua sessão do PowerShell.

```powershell
Import-Module AzureRM.AnalysisServices
```

## <a name="sign-in-tooazure"></a>Entrar tooAzure

Entrar tooyour assinatura do Azure usando Olá [AzureRmAccount adicionar](/powershell/module/azurerm.profile/add-azurermaccount) comando. Siga Olá na tela instruções.

```powershell
Add-AzureRmAccount
```

## <a name="create-a-resource-group"></a>Criar um grupo de recursos
 
Um [grupo de recursos do Azure](../azure-resource-manager/resource-group-overview.md) é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados em grupo. Quando você cria o servidor, precisa especificar um grupo de recursos em sua assinatura. Se você não tiver um grupo de recursos, você pode criar um novo usando Olá [AzureRmResourceGroup novo](/powershell/module/azurerm.resources/new-azurermresourcegroup) comando. Olá, exemplo a seguir cria um grupo de recursos denominado `myResourceGroup` na região Oeste dos EUA de saudação.

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
```

## <a name="create-a-server"></a>Criar um servidor

Criar um novo servidor usando Olá [AzureRmAnalysisServicesServer novo](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) comando. Olá exemplo a seguir cria um servidor chamado myServer na myResourceGroup, na região do Oeste dos EUA hello, na camada de saudação D1 e especifica philipc@adventureworks.com como um administrador de servidor.

```powershell
New-AzureRmAnalysisServicesServer -ResourceGroupName "myResourceGroup" -Name "myServer" -Location West US -Sku D1 -Administrator "philipc@adventure-works.com"
```

## <a name="clean-up-resources"></a>Limpar recursos

Você pode remover o servidor de saudação da sua assinatura usando Olá [AzureRmAnalysisServicesServer remover](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) comando. Se você ainda for seguir outros guias de início rápido e tutoriais desta coleção, não remova o servidor. Olá, exemplo a seguir remove o servidor de saudação criado na etapa anterior Olá.


```powershell
Remove-AzureRmAnalysisServicesServer -Name "myServer" -ResourceGroupName "myResourceGroup"
```

## <a name="next-steps"></a>Próximas etapas
[Gerenciar o Azure Analysis Services com PowerShell](analysis-services-powershell.md)   
[Implantar um modelo a partir do SSDT](analysis-services-deploy.md)   
[Criar um modelo no portal do Azure](analysis-services-create-model-portal.md)