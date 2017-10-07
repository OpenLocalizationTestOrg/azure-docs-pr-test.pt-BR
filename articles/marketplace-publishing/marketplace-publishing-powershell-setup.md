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
# <a name="set-up-azure-powershell-toocreate-an-offer-for-hello-azure-marketplace"></a>Configurar o Azure PowerShell toocreate uma oferta de saudação do Azure Marketplace
Para obter informações detalhadas sobre como tooset o PowerShell no Azure, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview). Uma abordagem simples é o método de certificado do toouse hello, que baixa e importa um certificado necessário para autenticação. Olá tooobtain necessário de certificado, use Olá **AzurePublishSettingsFile Get** cmdlet. Salve arquivo hello quando você for solicitado. certificado de saudação tooimport em uma sessão do PowerShell, use Olá **AzurePublishSettingsFile importação** cmdlet.

tooconfigure e armazenamento Olá comuns Microsoft Azure assinatura configurações de sessão do PowerShell Olá, use Olá **Set-AzureSubscription** e **Select-AzureSubscription** cmdlets:

        Set-AzureSubscription -SubscriptionName “mySubName” -CurrentStorageAccountName “mystorageaccount”
        Select-AzureSubscription -SubscriptionName "mySubName" –Current

comando primeiro Olá associa uma conta de armazenamento padrão com assinatura de saudação (necessária para algumas operações de provisionamento de VM).  Olá segundo torna assinatura Olá Olá um atual (reconhecido por outros cmdlets).

## <a name="see-also"></a>Consulte também
* [Guia de Introdução: como toopublish toohello uma oferta do Azure Marketplace](marketplace-publishing-getting-started.md)
* [Criar uma imagem de máquina virtual para Olá Marketplace](marketplace-publishing-vm-image-creation.md)

