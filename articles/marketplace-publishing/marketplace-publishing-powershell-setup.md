---
title: "aaaSet backup toocreate PowerShell uma VM para Olá Marketplace | Microsoft Docs"
description: "Instruções para configurar o Azure PowerShell e usá-lo como um processo opcional fluem toocreate toodeploy de imagens VM e vendem em, hello Azure Marketplace"
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
ms.openlocfilehash: cd2ebad7472248b8f921706e1a8c82d41f33b9cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-azure-powershell-toocreate-an-offer-for-hello-azure-marketplace"></a><span data-ttu-id="20f72-103">Configurar o Azure PowerShell toocreate uma oferta de saudação do Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="20f72-103">Set up Azure PowerShell toocreate an offer for hello Azure Marketplace</span></span>
<span data-ttu-id="20f72-104">Para obter informações detalhadas sobre como tooset o PowerShell no Azure, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="20f72-104">For detailed information on how tooset up PowerShell in Azure, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="20f72-105">Uma abordagem simples é o método de certificado do toouse hello, que baixa e importa um certificado necessário para autenticação.</span><span class="sxs-lookup"><span data-stu-id="20f72-105">A simple approach is toouse hello certificate method, which downloads and imports a certificate needed for authentication.</span></span> <span data-ttu-id="20f72-106">Olá tooobtain necessário de certificado, use Olá **AzurePublishSettingsFile Get** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="20f72-106">tooobtain hello needed certificate, use hello **Get-AzurePublishSettingsFile** cmdlet.</span></span> <span data-ttu-id="20f72-107">Salve arquivo hello quando você for solicitado.</span><span class="sxs-lookup"><span data-stu-id="20f72-107">Save hello file when you're prompted.</span></span> <span data-ttu-id="20f72-108">certificado de saudação tooimport em uma sessão do PowerShell, use Olá **AzurePublishSettingsFile importação** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="20f72-108">tooimport hello certificate into a PowerShell session, use hello **Import-AzurePublishSettingsFile** cmdlet.</span></span>

<span data-ttu-id="20f72-109">tooconfigure e armazenamento Olá comuns Microsoft Azure assinatura configurações de sessão do PowerShell Olá, use Olá **Set-AzureSubscription** e **Select-AzureSubscription** cmdlets:</span><span class="sxs-lookup"><span data-stu-id="20f72-109">tooconfigure and store hello common Microsoft Azure subscription settings for hello PowerShell session, use hello **Set-AzureSubscription** and **Select-AzureSubscription** cmdlets:</span></span>

        Set-AzureSubscription -SubscriptionName “mySubName” -CurrentStorageAccountName “mystorageaccount”
        Select-AzureSubscription -SubscriptionName "mySubName" –Current

<span data-ttu-id="20f72-110">comando primeiro Olá associa uma conta de armazenamento padrão com assinatura de saudação (necessária para algumas operações de provisionamento de VM).</span><span class="sxs-lookup"><span data-stu-id="20f72-110">hello first command associates a default storage account with hello subscription (needed for some VM provisioning operations).</span></span>  <span data-ttu-id="20f72-111">Olá segundo torna assinatura Olá Olá um atual (reconhecido por outros cmdlets).</span><span class="sxs-lookup"><span data-stu-id="20f72-111">hello second makes hello subscription hello current one (recognized by other cmdlets).</span></span>

## <a name="see-also"></a><span data-ttu-id="20f72-112">Consulte também</span><span class="sxs-lookup"><span data-stu-id="20f72-112">See also</span></span>
* [<span data-ttu-id="20f72-113">Guia de Introdução: como toopublish toohello uma oferta do Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="20f72-113">Getting started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)
* [<span data-ttu-id="20f72-114">Criar uma imagem de máquina virtual para Olá Marketplace</span><span class="sxs-lookup"><span data-stu-id="20f72-114">Creating a virtual machine image for hello Marketplace</span></span>](marketplace-publishing-vm-image-creation.md)

