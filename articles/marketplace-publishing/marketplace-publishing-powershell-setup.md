---
title: Configurar o PowerShell para criar uma VM para o Marketplace | Microsoft Docs
description: "Instruções para configurar o Azure PowerShell e usar como um fluxo de processo opcional para criar imagens VM para implantar e vender no Azure Marketplace"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e19d6cda-76df-4e42-be84-c9fe47a636db
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/04/2016
ms.author: hascipio
ms.openlocfilehash: bbcce5093d2bbd5326523063db7d0e565fe4de6d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-azure-powershell-to-create-an-offer-for-the-azure-marketplace"></a><span data-ttu-id="6b492-103">Configurar o Azure PowerShell para criar a oferta para o Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="6b492-103">Set up Azure PowerShell to create an offer for the Azure Marketplace</span></span>
<span data-ttu-id="6b492-104">Para obter informações detalhadas sobre como configurar o PowerShell no Azure, consulte, [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6b492-104">For detailed information on how to set up PowerShell in Azure, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="6b492-105">Uma abordagem simples é usar o método de certificado que baixa e importa um certificado necessário para autenticar.</span><span class="sxs-lookup"><span data-stu-id="6b492-105">A simple approach is to use the certificate method, which downloads and imports a certificate needed for authentication.</span></span> <span data-ttu-id="6b492-106">Para obter o certificado necessário, use o cmdlet **Get-AzurePublishSettingsFile** .</span><span class="sxs-lookup"><span data-stu-id="6b492-106">To obtain the needed certificate, use the **Get-AzurePublishSettingsFile** cmdlet.</span></span> <span data-ttu-id="6b492-107">Quando for solicitado, salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="6b492-107">Save the file when you're prompted.</span></span> <span data-ttu-id="6b492-108">Para importar o certificado em uma sessão do PowerShell, use o cmdlet **Import-AzurePublishSettingsFile** .</span><span class="sxs-lookup"><span data-stu-id="6b492-108">To import the certificate into a PowerShell session, use the **Import-AzurePublishSettingsFile** cmdlet.</span></span>

<span data-ttu-id="6b492-109">Para configurar e armazenar as configurações de assinatura do Microsoft Azure comuns para a sessão do PowerShell, use os cmdlets **Set-AzureSubscription** e **Select-AzureSubscription**:</span><span class="sxs-lookup"><span data-stu-id="6b492-109">To configure and store the common Microsoft Azure subscription settings for the PowerShell session, use the **Set-AzureSubscription** and **Select-AzureSubscription** cmdlets:</span></span>

        Set-AzureSubscription -SubscriptionName “mySubName” -CurrentStorageAccountName “mystorageaccount”
        Select-AzureSubscription -SubscriptionName "mySubName" –Current

<span data-ttu-id="6b492-110">O primeiro comando associa uma conta de armazenamento padrão com a assinatura (necessária para algumas operações de provisionamento da VM).</span><span class="sxs-lookup"><span data-stu-id="6b492-110">The first command associates a default storage account with the subscription (needed for some VM provisioning operations).</span></span>  <span data-ttu-id="6b492-111">O segundo faz a assinatura do ano atual (reconhecido por outros cmdlets).</span><span class="sxs-lookup"><span data-stu-id="6b492-111">The second makes the subscription the current one (recognized by other cmdlets).</span></span>

## <a name="see-also"></a><span data-ttu-id="6b492-112">Consulte também</span><span class="sxs-lookup"><span data-stu-id="6b492-112">See also</span></span>
* [<span data-ttu-id="6b492-113">Introdução: como publicar uma oferta no Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="6b492-113">Getting started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)
* [<span data-ttu-id="6b492-114">Criar uma imagem de máquina virtual para o Marketplace</span><span class="sxs-lookup"><span data-stu-id="6b492-114">Creating a virtual machine image for the Marketplace</span></span>](marketplace-publishing-vm-image-creation.md)

