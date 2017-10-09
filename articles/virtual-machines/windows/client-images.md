---
title: imagens do cliente Windows aaaUse no Azure | Microsoft Docs
description: "Como toouse assinatura do Visual Studio beneficia toodeploy Windows 7, Windows 8 ou Windows 10 no Azure para cenários de desenvolvimento/teste"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 91c3880a-cede-44f1-ae25-f8f9f5b6eaa4
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: 4ac7c3d9872673030f4ea0f0ab38625dd9d9c1b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-client-in-azure-for-devtest-scenarios"></a>Usar o cliente do Windows no Azure para cenários de desenvolvimento/teste
Você pode usar o Windows 7, Windows 8 ou Windows 10 no Azure para cenários de desenvolvimento + teste, desde que você tenha uma assinatura apropriada do Visual Studio (anteriormente conhecido como MSDN). Este artigo descreve os requisitos de qualificação Olá para executar o cliente do Windows no Azure e o uso de saudação imagens da Galeria do Azure.

## <a name="subscription-eligibility"></a>Qualificação de assinatura
Os assinantes ativos do Visual Studio (pessoas que tem adquiriram uma licença de assinatura do Visual Studio) podem usar o cliente do Windows para fins de teste e desenvolvimento. O cliente do Windows pode ser usado em seu próprio hardware e nas máquinas virtuais do Azure em execução em qualquer tipo de assinatura do Azure. Cliente do Windows não pode ser implantado tooor usado no Azure para uso em produção normal ou usados por pessoas que não são assinantes ativos do Visual Studio.

Para sua conveniência, fizemos determinadas imagens do Windows 10 disponíveis da Galeria do Azure Olá em [qualificados de desenvolvimento/teste oferece](#eligible-offers). Assinantes do Visual Studio em qualquer tipo de oferta também podem [adequadamente preparar e criar](prepare-for-upload-vhd-image.md) uma imagem do Windows 7, Windows 8 ou Windows 10 64 bits e, em seguida, [carregar tooAzure](upload-generalized-managed.md). use Olá permanece toodev/teste limitado por assinantes ativos do Visual Studio.

## <a name="eligible-offers"></a>Ofertas qualificadas
Olá Olá de detalhes da tabela a seguir oferece IDs que estão qualificado toodeploy Windows 10 por meio de saudação Galeria do Azure. imagens de saudação Windows 10 só são visível toohello ofertas a seguir. Assinantes do Visual Studio que precisa toorun cliente do Windows em um tipo diferente de oferta exigir muito[adequadamente preparar e criar](prepare-for-upload-vhd-image.md) uma imagem do Windows 7, Windows 8 ou Windows 10 64 bits e [, em seguida, carregar tooAzure](upload-generalized-managed.md).

| Nome da oferta | Número da oferta | Imagens de cliente disponíveis |
|:--- |:---:|:---:|
| [Desenvolvimento/Teste pré-pago](https://azure.microsoft.com/offers/ms-azr-0023p/) |0023P |Windows 10 |
| [Assinantes do Visual Studio Enterprise (MPN)](https://azure.microsoft.com/offers/ms-azr-0029p/) |0029P |Windows 10 |
| [Assinantes do Visual Studio Professional](https://azure.microsoft.com/offers/ms-azr-0059p/) |0059P |Windows 10 |
| [Assinantes do Visual Studio Test Professional](https://azure.microsoft.com/offers/ms-azr-0060p/) |0060P |Windows 10 |
| [Visual Studio Premium com MSDN (benefício)](https://azure.microsoft.com/offers/ms-azr-0061p/) |0061P |Windows 10 |
| [Assinantes do Visual Studio Enterprise](https://azure.microsoft.com/offers/ms-azr-0063p/) |0063P |Windows 10 |
| [Assinantes do Visual Studio Enterprise (BizSpark)](https://azure.microsoft.com/offers/ms-azr-0064p/) |0064P |Windows 10 |
| [Desenvolvimento/Teste Enterprise](https://azure.microsoft.com/ofers/ms-azr-0148p/) |0148P |Windows 10 |

## <a name="check-your-azure-subscription"></a>Verificar sua assinatura do Azure
Se você não souber a ID de oferta, você pode obtê-lo por meio do portal do Azure em uma destas duas maneiras de saudação:  

- Na folha de 'Assinaturas' hello:

  ![Detalhes da ID de oferta de saudação portal do Azure](./media/client-images/offer-id-azure-portal.png) 

- Ou, clique em **Cobrança** e, em seguida, clique em sua ID de assinatura. ID da oferta Olá aparece na folha de cobrança hello.

Você também pode exibir a ID de oferta de saudação do hello [guia 'Assinaturas'](http://account.windowsazure.com/Subscriptions) hello Azure do portal de conta:

![Detalhes de ID da oferta do portal de conta do Azure Olá](./media/client-images/offer-id-azure-account-portal.png) 

## <a name="next-steps"></a>Próximas etapas
Agora você pode implantar suas VMs usando o [PowerShell](quick-create-powershell.md), os [modelos do Resource Manager](ps-template.md) ou o [Visual Studio](../../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).

