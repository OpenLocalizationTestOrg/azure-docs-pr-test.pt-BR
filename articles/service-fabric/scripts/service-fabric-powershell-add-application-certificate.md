---
title: aaaAzure exemplo de Script do PowerShell - Adicionar aplicativo cert tooa cluster | Microsoft Docs
description: Script do PowerShell do Azure de exemplo - adicionar um cluster do aplicativo certificado tooa do Service Fabric.
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: aba62598e2e4775012f89b5070bef5e61aec64f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-an-application-certificate-tooa-service-fabric-cluster"></a><span data-ttu-id="c299b-103">Adicionar um cluster de malha do serviço do aplicativo certificado tooa</span><span class="sxs-lookup"><span data-stu-id="c299b-103">Add an application certificate tooa Service Fabric cluster</span></span>

<span data-ttu-id="c299b-104">Esse script de exemplo cria um certificado autoassinado no cofre de chaves do Azure especificado hello e instala tooall nós de cluster do Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="c299b-104">This sample script creates a self-signed certificate in hello specified Azure key vault and installs it tooall nodes of hello Service Fabric cluster.</span></span> <span data-ttu-id="c299b-105">certificado Olá baixa também a pasta local tooa.</span><span class="sxs-lookup"><span data-stu-id="c299b-105">hello certificate also downloads tooa local folder.</span></span> <span data-ttu-id="c299b-106">nome de saudação do certificado de saudação baixado é Olá igual ao nome de saudação do certificado Olá no cofre de chaves hello.</span><span class="sxs-lookup"><span data-stu-id="c299b-106">hello name of hello downloaded certificate is hello same as hello name of hello certificate in hello key vault.</span></span> <span data-ttu-id="c299b-107">Personalize parâmetros Olá conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="c299b-107">Customize hello parameters as needed.</span></span>

<span data-ttu-id="c299b-108">Se necessário, instale Olá PowerShell do Azure usando a instrução Olá encontrado no hello [guia do PowerShell do Azure](/powershell/azure/overview) e, em seguida, execute `Login-AzureRmAccount` toocreate uma conexão com o Azure.</span><span class="sxs-lookup"><span data-stu-id="c299b-108">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview) and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="c299b-109">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="c299b-109">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/add-application-certificate/add-new-application-certificate.ps1 "Add an application certificate tooa cluster")]

## <a name="script-explanation"></a><span data-ttu-id="c299b-110">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="c299b-110">Script explanation</span></span>

<span data-ttu-id="c299b-111">Esse script usa Olá comandos a seguir: cada comando na tabela Olá vincula a documentação específica do toocommand.</span><span class="sxs-lookup"><span data-stu-id="c299b-111">This script uses hello following commands: Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c299b-112">Command</span><span class="sxs-lookup"><span data-stu-id="c299b-112">Command</span></span> | <span data-ttu-id="c299b-113">Observações</span><span class="sxs-lookup"><span data-stu-id="c299b-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c299b-114">Add-AzureRmServiceFabricApplicationCertificate</span><span class="sxs-lookup"><span data-stu-id="c299b-114">Add-AzureRmServiceFabricApplicationCertificate</span></span>](/powershell/module/azurerm.servicefabric/Add-AzureRmServiceFabricApplicationCertificate) | <span data-ttu-id="c299b-115">Adicione que uma escala de máquina virtual toohello de certificado novo aplicativo definido que formam o cluster hello.</span><span class="sxs-lookup"><span data-stu-id="c299b-115">Add a new application certificate toohello virtual machine scale set that make up hello cluster.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="c299b-116">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c299b-116">Next steps</span></span>

<span data-ttu-id="c299b-117">Para obter mais informações sobre o módulo do PowerShell do Azure hello, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c299b-117">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="c299b-118">Exemplos adicionais do Azure Powershell para Azure Service Fabric podem ser encontrados no hello [exemplos do PowerShell do Azure](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c299b-118">Additional Azure Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
