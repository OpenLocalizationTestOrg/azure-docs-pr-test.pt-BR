---
title: "transferência segura de aaaRequire no armazenamento do Azure | Microsoft Docs"
description: "Saiba mais sobre o recurso de \"Exigir a transferência segura\" Olá para armazenamento do Azure e como tooenable-lo."
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
ms.openlocfilehash: 27f745c5e771b50213c1dbb39dee081947be1f39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="require-secure-transfer"></a><span data-ttu-id="8e721-103">Requer transferência segura</span><span class="sxs-lookup"><span data-stu-id="8e721-103">Require secure transfer</span></span>

<span data-ttu-id="8e721-104">opção Hello "transferência segura necessária" aumenta a segurança de saudação da sua conta de armazenamento, permitindo que apenas solicitações toohello conta de armazenamento de conexões seguras.</span><span class="sxs-lookup"><span data-stu-id="8e721-104">hello "Secure transfer required" option enhances hello security of your storage account by only allowing requests toohello storage account from secure connections.</span></span> <span data-ttu-id="8e721-105">Por exemplo, ao chamar APIs REST tooaccess sua conta de armazenamento, você deve se conectar usando HTTPS.</span><span class="sxs-lookup"><span data-stu-id="8e721-105">For example, when calling REST APIs tooaccess your storage account, you must connect using HTTPS.</span></span> <span data-ttu-id="8e721-106">Todas as solicitações utilizando HTTP serão rejeitadas quando a "Transferência segura obrigatória" estiver habilitada.</span><span class="sxs-lookup"><span data-stu-id="8e721-106">Any requests using HTTP are rejected when "Secure transfer required" is enabled.</span></span>

<span data-ttu-id="8e721-107">Quando você estiver usando o serviço de arquivos do Azure Olá, qualquer conexão sem criptografia falhará ao "Seguro transferência necessária" está habilitado.</span><span class="sxs-lookup"><span data-stu-id="8e721-107">When you are using hello Azure Files service, any connection without encryption fails when "Secure transfer required" is enabled.</span></span> <span data-ttu-id="8e721-108">Isso inclui cenários de uso de SMB 2.1, SMB 3.0 sem criptografia e alguns tipos de saudação cliente Linux SMB.</span><span class="sxs-lookup"><span data-stu-id="8e721-108">This includes scenarios using SMB 2.1, SMB 3.0 without encryption, and some flavors of hello Linux SMB client.</span></span> 

<span data-ttu-id="8e721-109">Por padrão, a opção de hello "transferência segura necessária" está desabilitada.</span><span class="sxs-lookup"><span data-stu-id="8e721-109">By default, hello "Secure transfer required" option is disabled.</span></span>

> [!NOTE]
> <span data-ttu-id="8e721-110">Como o armazenamento do Azure não dá suporte a HTTPS para nomes de domínio personalizado, essa opção não será aplicada ao usar um nome de domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="8e721-110">Because Azure Storage doesn't support HTTPS for custom domain names, this option is not applied when using a custom domain name.</span></span>

## <a name="enable-secure-transfer-required-in-hello-azure-portal"></a><span data-ttu-id="8e721-111">Habilitar o "Transferência segura necessária" hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8e721-111">Enable "Secure transfer required" in hello Azure portal</span></span>

<span data-ttu-id="8e721-112">Você pode habilitar hello "transferência segura necessária" configurar ambos ao criar uma conta de armazenamento no hello [portal do Azure](https://portal.azure.com)e para contas de armazenamento existente.</span><span class="sxs-lookup"><span data-stu-id="8e721-112">You can enable hello "Secure transfer required" setting both when you create a storage account in hello [Azure portal](https://portal.azure.com), and for existing storage accounts.</span></span>

### <a name="require-secure-transfer-when-you-create-a-storage-account"></a><span data-ttu-id="8e721-113">Requerer transferência segura ao criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="8e721-113">Require secure transfer when you create a storage account</span></span>

1. <span data-ttu-id="8e721-114">Olá abrir **criar conta de armazenamento** folha em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8e721-114">Open hello **Create storage account** blade in hello Azure portal.</span></span>
1. <span data-ttu-id="8e721-115">Em **Transferência segura obrigatória**, selecione **habilitado**.</span><span class="sxs-lookup"><span data-stu-id="8e721-115">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![captura de tela](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_1.png)

### <a name="require-secure-transfer-for-an-existing-storage-account"></a><span data-ttu-id="8e721-117">Requer transferência segura de uma conta de armazenamento existente</span><span class="sxs-lookup"><span data-stu-id="8e721-117">Require secure transfer for an existing storage account</span></span>

1. <span data-ttu-id="8e721-118">Selecione uma conta de armazenamento existente na Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8e721-118">Select an existing storage account in hello Azure portal.</span></span>
1. <span data-ttu-id="8e721-119">Selecione **configuração** em **configurações** na folha de menu de conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="8e721-119">Select **Configuration** under **SETTINGS** in hello storage account menu blade.</span></span>
1. <span data-ttu-id="8e721-120">Em **Transferência segura obrigatória**, selecione **habilitado**.</span><span class="sxs-lookup"><span data-stu-id="8e721-120">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![captura de tela](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_2.png)

## <a name="enable-secure-transfer-required-programmatically"></a><span data-ttu-id="8e721-122">Habilitar "Transferência segura obrigatória" Programaticamente</span><span class="sxs-lookup"><span data-stu-id="8e721-122">Enable "Secure transfer required" programmatically</span></span>

<span data-ttu-id="8e721-123">nome da configuração Olá é _supportsHttpsTrafficOnly_ nas propriedades da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8e721-123">hello setting name is _supportsHttpsTrafficOnly_ in storage account properties.</span></span> <span data-ttu-id="8e721-124">Você pode habilitar a configuração "Transferência segura obrigatória" com a API REST, ferramentas ou bibliotecas:</span><span class="sxs-lookup"><span data-stu-id="8e721-124">You can enable "Secure transfer required" setting with REST API, tools or libraries:</span></span>

* <span data-ttu-id="8e721-125">**API REST** (Versão: 2016-12-01): [pacote de lançamento](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)</span><span class="sxs-lookup"><span data-stu-id="8e721-125">**REST API** (Version: 2016-12-01): [release package](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)</span></span>
* <span data-ttu-id="8e721-126">**PowerShell** (Versão: 4.1.0): [pacote de lançamento](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)</span><span class="sxs-lookup"><span data-stu-id="8e721-126">**PowerShell** (Version: 4.1.0): [release package](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)</span></span>
* <span data-ttu-id="8e721-127">**CLI** (Versão: 2.0.11): [pacote de lançamento](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)</span><span class="sxs-lookup"><span data-stu-id="8e721-127">**CLI** (Version: 2.0.11): [release package](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)</span></span>
* <span data-ttu-id="8e721-128">**NodeJS** (Versão: 1.1.0): [pacote de lançamento](https://www.npmjs.com/package/azure-arm-storage/)</span><span class="sxs-lookup"><span data-stu-id="8e721-128">**NodeJS** (Version: 1.1.0): [release package](https://www.npmjs.com/package/azure-arm-storage/)</span></span>
* <span data-ttu-id="8e721-129">**SDK do .NET SDK** (Versão: 6.3.0): [pacote de lançamento](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)</span><span class="sxs-lookup"><span data-stu-id="8e721-129">**.NET SDK** (Version: 6.3.0): [release package](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)</span></span>
* <span data-ttu-id="8e721-130">**SDK do Python** (Versão: 1.1.0): [pacote de lançamento](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)</span><span class="sxs-lookup"><span data-stu-id="8e721-130">**Python SDK** (Version: 1.1.0): [release package](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)</span></span>
* <span data-ttu-id="8e721-131">**SDK do Ruby** (Versão: 0.11.0): [pacote de lançamento](https://rubygems.org/gems/azure_mgmt_storage)</span><span class="sxs-lookup"><span data-stu-id="8e721-131">**Ruby SDK** (Version: 0.11.0): [release package](https://rubygems.org/gems/azure_mgmt_storage)</span></span>

### <a name="enable-secure-transfer-required-setting-with-rest-api"></a><span data-ttu-id="8e721-132">Habilitar a configuração "Transferência segura obrigatória" com a API REST</span><span class="sxs-lookup"><span data-stu-id="8e721-132">Enable "Secure transfer required" setting with REST API</span></span>

<span data-ttu-id="8e721-133">toosimplify testes com API REST, você pode usar [ArmClient](https://github.com/projectkudu/ARMClient) toocall de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="8e721-133">toosimplify testing with REST API, you can use [ArmClient](https://github.com/projectkudu/ARMClient) toocall from command line.</span></span>

 <span data-ttu-id="8e721-134">Você pode usar abaixo da configuração de saudação de toocheck de linha de comando com hello API REST:</span><span class="sxs-lookup"><span data-stu-id="8e721-134">You can use below command line toocheck hello setting with hello REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient GET  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01
```

<span data-ttu-id="8e721-135">Em resposta hello, você pode encontrar _supportsHttpsTrafficOnly_ configuração.</span><span class="sxs-lookup"><span data-stu-id="8e721-135">In hello response, you can find _supportsHttpsTrafficOnly_ setting.</span></span> <span data-ttu-id="8e721-136">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="8e721-136">Sample:</span></span>

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

<span data-ttu-id="8e721-137">Você pode usar abaixo da configuração de saudação de tooenable de linha de comando com hello API REST:</span><span class="sxs-lookup"><span data-stu-id="8e721-137">You can use below command line tooenable hello setting with hello REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01 < Input.json
```
<span data-ttu-id="8e721-138">Exemplo de Input.json:</span><span class="sxs-lookup"><span data-stu-id="8e721-138">Sample of Input.json:</span></span>
```Json
{
  "location": "westus",
  "properties": {
    "supportsHttpsTrafficOnly": true
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="8e721-139">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8e721-139">Next steps</span></span>
<span data-ttu-id="8e721-140">Armazenamento do Azure fornece um conjunto abrangente de recursos de segurança, que juntos permitem que os desenvolvedores de aplicativos seguros toobuild.</span><span class="sxs-lookup"><span data-stu-id="8e721-140">Azure Storage provides a comprehensive set of security capabilities, which together enable developers toobuild secure applications.</span></span> <span data-ttu-id="8e721-141">Para obter mais detalhes, visite Olá [guia de segurança do armazenamento](storage-security-guide.md).</span><span class="sxs-lookup"><span data-stu-id="8e721-141">For more details, visit hello [Storage Security Guide](storage-security-guide.md).</span></span>
