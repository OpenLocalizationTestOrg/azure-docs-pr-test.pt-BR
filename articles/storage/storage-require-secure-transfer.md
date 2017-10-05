---
title: "Requer transferência segura no Armazenamento do Microsoft Azure | Microsoft Docs"
description: "Saiba mais sobre o recurso \"Requer transferência segura\" para o Armazenamento do Microsoft Azure e como habilitá-lo."
services: storage
documentationcenter: na
author: fhryo-msft
manager: Jason.Hogg
editor: fhryo-msft
ms.assetid: 
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 06/20/2017
ms.author: fryu
ms.openlocfilehash: bc5b7fc79869c632db96958f17aaf953a5fd3b19
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="require-secure-transfer"></a><span data-ttu-id="1071f-103">Requer transferência segura</span><span class="sxs-lookup"><span data-stu-id="1071f-103">Require secure transfer</span></span>

<span data-ttu-id="1071f-104">A opção "Transferência segura obrigatória" melhora a segurança da sua conta de armazenamento, permitindo apenas solicitações para a conta de armazenamento de conexões seguras.</span><span class="sxs-lookup"><span data-stu-id="1071f-104">The "Secure transfer required" option enhances the security of your storage account by only allowing requests to the storage account from secure connections.</span></span> <span data-ttu-id="1071f-105">Por exemplo, ao chamar APIs REST para acessar sua conta de armazenamento, será necessário estar conectado utilizando o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="1071f-105">For example, when calling REST APIs to access your storage account, you must connect using HTTPS.</span></span> <span data-ttu-id="1071f-106">Todas as solicitações utilizando HTTP serão rejeitadas quando a "Transferência segura obrigatória" estiver habilitada.</span><span class="sxs-lookup"><span data-stu-id="1071f-106">Any requests using HTTP are rejected when "Secure transfer required" is enabled.</span></span>

<span data-ttu-id="1071f-107">Quando você estiver usando o serviço de Arquivos do Azure, qualquer conexão sem criptografia falhará quando "Transferência segura obrigatória" estiver habilitada.</span><span class="sxs-lookup"><span data-stu-id="1071f-107">When you are using the Azure Files service, any connection without encryption fails when "Secure transfer required" is enabled.</span></span> <span data-ttu-id="1071f-108">Isso inclui cenários usando SMB 2.1, SMB 3.0 sem criptografia e alguns tipos do cliente Linux SMB.</span><span class="sxs-lookup"><span data-stu-id="1071f-108">This includes scenarios using SMB 2.1, SMB 3.0 without encryption, and some flavors of the Linux SMB client.</span></span> 

<span data-ttu-id="1071f-109">Por padrão, a opção "Transferência segura obrigatória" está desabilitada.</span><span class="sxs-lookup"><span data-stu-id="1071f-109">By default, the "Secure transfer required" option is disabled.</span></span>

> [!NOTE]
> <span data-ttu-id="1071f-110">Como o armazenamento do Azure não dá suporte a HTTPS para nomes de domínio personalizado, essa opção não será aplicada ao usar um nome de domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="1071f-110">Because Azure Storage doesn't support HTTPS for custom domain names, this option is not applied when using a custom domain name.</span></span>

## <a name="enable-secure-transfer-required-in-the-azure-portal"></a><span data-ttu-id="1071f-111">Habilitar "Transferência segura obrigatória" no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="1071f-111">Enable "Secure transfer required" in the Azure portal</span></span>

<span data-ttu-id="1071f-112">Você pode habilitar a "Transferência segura obrigatória" configurando ambos ao criar uma conta de armazenamento no [Portal do Azure](https://portal.azure.com)e para contas de armazenamento existentes.</span><span class="sxs-lookup"><span data-stu-id="1071f-112">You can enable the "Secure transfer required" setting both when you create a storage account in the [Azure portal](https://portal.azure.com), and for existing storage accounts.</span></span>

### <a name="require-secure-transfer-when-you-create-a-storage-account"></a><span data-ttu-id="1071f-113">Requerer transferência segura ao criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="1071f-113">Require secure transfer when you create a storage account</span></span>

1. <span data-ttu-id="1071f-114">Abra a folha **Criar conta de armazenamento** no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1071f-114">Open the **Create storage account** blade in the Azure portal.</span></span>
1. <span data-ttu-id="1071f-115">Em **Transferência segura obrigatória**, selecione **habilitado**.</span><span class="sxs-lookup"><span data-stu-id="1071f-115">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![captura de tela](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_1.png)

### <a name="require-secure-transfer-for-an-existing-storage-account"></a><span data-ttu-id="1071f-117">Requer transferência segura de uma conta de armazenamento existente</span><span class="sxs-lookup"><span data-stu-id="1071f-117">Require secure transfer for an existing storage account</span></span>

1. <span data-ttu-id="1071f-118">Selecionar uma conta de armazenamento existente no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1071f-118">Select an existing storage account in the Azure portal.</span></span>
1. <span data-ttu-id="1071f-119">Selecione **Configuração** em **CONFIGURAÇÕES** na folha do menu da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1071f-119">Select **Configuration** under **SETTINGS** in the storage account menu blade.</span></span>
1. <span data-ttu-id="1071f-120">Em **Transferência segura obrigatória**, selecione **habilitado**.</span><span class="sxs-lookup"><span data-stu-id="1071f-120">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![captura de tela](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_2.png)

## <a name="enable-secure-transfer-required-programmatically"></a><span data-ttu-id="1071f-122">Habilitar "Transferência segura obrigatória" Programaticamente</span><span class="sxs-lookup"><span data-stu-id="1071f-122">Enable "Secure transfer required" programmatically</span></span>

<span data-ttu-id="1071f-123">O nome da configuração é _supportsHttpsTrafficOnly_ nas propriedades da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1071f-123">The setting name is _supportsHttpsTrafficOnly_ in storage account properties.</span></span> <span data-ttu-id="1071f-124">Você pode habilitar a configuração "Transferência segura obrigatória" com a API REST, ferramentas ou bibliotecas:</span><span class="sxs-lookup"><span data-stu-id="1071f-124">You can enable "Secure transfer required" setting with REST API, tools or libraries:</span></span>

* <span data-ttu-id="1071f-125">**API REST** (Versão: 2016-12-01): [pacote de lançamento](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)</span><span class="sxs-lookup"><span data-stu-id="1071f-125">**REST API** (Version: 2016-12-01): [release package](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)</span></span>
* <span data-ttu-id="1071f-126">**PowerShell** (Versão: 4.1.0): [pacote de lançamento](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)</span><span class="sxs-lookup"><span data-stu-id="1071f-126">**PowerShell** (Version: 4.1.0): [release package](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)</span></span>
* <span data-ttu-id="1071f-127">**CLI** (Versão: 2.0.11): [pacote de lançamento](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)</span><span class="sxs-lookup"><span data-stu-id="1071f-127">**CLI** (Version: 2.0.11): [release package](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)</span></span>
* <span data-ttu-id="1071f-128">**NodeJS** (Versão: 1.1.0): [pacote de lançamento](https://www.npmjs.com/package/azure-arm-storage/)</span><span class="sxs-lookup"><span data-stu-id="1071f-128">**NodeJS** (Version: 1.1.0): [release package](https://www.npmjs.com/package/azure-arm-storage/)</span></span>
* <span data-ttu-id="1071f-129">**SDK do .NET SDK** (Versão: 6.3.0): [pacote de lançamento](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)</span><span class="sxs-lookup"><span data-stu-id="1071f-129">**.NET SDK** (Version: 6.3.0): [release package](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)</span></span>
* <span data-ttu-id="1071f-130">**SDK do Python** (Versão: 1.1.0): [pacote de lançamento](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)</span><span class="sxs-lookup"><span data-stu-id="1071f-130">**Python SDK** (Version: 1.1.0): [release package](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)</span></span>
* <span data-ttu-id="1071f-131">**SDK do Ruby** (Versão: 0.11.0): [pacote de lançamento](https://rubygems.org/gems/azure_mgmt_storage)</span><span class="sxs-lookup"><span data-stu-id="1071f-131">**Ruby SDK** (Version: 0.11.0): [release package](https://rubygems.org/gems/azure_mgmt_storage)</span></span>

### <a name="enable-secure-transfer-required-setting-with-rest-api"></a><span data-ttu-id="1071f-132">Habilitar a configuração "Transferência segura obrigatória" com a API REST</span><span class="sxs-lookup"><span data-stu-id="1071f-132">Enable "Secure transfer required" setting with REST API</span></span>

<span data-ttu-id="1071f-133">Para simplificar o teste com a API REST, você pode usar [ArmClient](https://github.com/projectkudu/ARMClient) para chamar a partir de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="1071f-133">To simplify testing with REST API, you can use [ArmClient](https://github.com/projectkudu/ARMClient) to call from command line.</span></span>

 <span data-ttu-id="1071f-134">Você pode usar a linha de comando abaixo para verificar a configuração com a API REST:</span><span class="sxs-lookup"><span data-stu-id="1071f-134">You can use below command line to check the setting with the REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient GET  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01
```

<span data-ttu-id="1071f-135">Em resposta, você pode encontrar a configuração _supportsHttpsTrafficOnly_.</span><span class="sxs-lookup"><span data-stu-id="1071f-135">In the response, you can find _supportsHttpsTrafficOnly_ setting.</span></span> <span data-ttu-id="1071f-136">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="1071f-136">Sample:</span></span>

```Json
{
  "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}",
  "kind": "Storage",
  ...
  "properties": {
    ...
    "supportsHttpsTrafficOnly": false
  },
  "type": "Microsoft.Storage/storageAccounts"
}
```

<span data-ttu-id="1071f-137">Você pode usar a linha de comando abaixo para habilitar a configuração com a API REST:</span><span class="sxs-lookup"><span data-stu-id="1071f-137">You can use below command line to enable the setting with the REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01 < Input.json
```
<span data-ttu-id="1071f-138">Exemplo de Input.json:</span><span class="sxs-lookup"><span data-stu-id="1071f-138">Sample of Input.json:</span></span>
```Json
{
  "location": "westus",
  "properties": {
    "supportsHttpsTrafficOnly": true
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="1071f-139">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1071f-139">Next steps</span></span>
<span data-ttu-id="1071f-140">O Armazenamento do Azure fornece um conjunto abrangente de recursos de segurança que, juntos, permitem aos desenvolvedores criar aplicativos seguros.</span><span class="sxs-lookup"><span data-stu-id="1071f-140">Azure Storage provides a comprehensive set of security capabilities, which together enable developers to build secure applications.</span></span> <span data-ttu-id="1071f-141">Para obter mais detalhes, visite o [Guia de segurança do armazenamento](storage-security-guide.md).</span><span class="sxs-lookup"><span data-stu-id="1071f-141">For more details, visit the [Storage Security Guide](storage-security-guide.md).</span></span>
