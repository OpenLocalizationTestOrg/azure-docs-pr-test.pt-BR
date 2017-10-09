---
title: "aaaScale cotas e limites de seu laboratório no Azure DevTest Labs | Microsoft Docs"
description: "Saiba como tooscale um laboratório no Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: ae624155-9181-45fa-bd2b-1983339b7e0e
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: tarcher
ms.openlocfilehash: 7fb429c0aabdfbce3a4a5aa6d9259daa2ee270d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-quotas-and-limits-in-devtest-labs"></a>Dimensionar cotas e limites no DevTest Labs
Enquanto você trabalha no DevTest Labs, talvez Observe que há certa toosome de limites padrão recursos do Azure, o que podem afetar o serviço do DevTest Labs hello. Esses limites são chamados tooas **cotas**.

> [!NOTE]
> Olá serviço DevTest Labs não impor cotas. As cotas que podem ser encontrados são restrições de padrão de saudação assinatura geral do Azure.

Você pode usar cada recurso do Azure até atingir sua cota. Cada assinatura tem cotas separadas e seu uso é controlado por assinatura.

Por exemplo, cada assinatura tem uma cota padrão de 20 núcleos. Portanto, se você estiver criando VMs em seu laboratório com quatro núcleos cada, você poderá criar apenas cinco VMs. 

[Azure assinatura e limites de serviço](https://docs.microsoft.com/azure/azure-subscription-service-limits) lista algumas das cotas de hello mais comuns para recursos do Azure. Olá recursos mais comumente usados em um laboratório e para que você pode encontrar cotas, incluir núcleos VM, endereços IP públicos, interface de rede, discos gerenciados, atribuição de função RBAC e circuitos do ExpressRoute.

## <a name="view-your-usage-and-quotas"></a>Exibir seu uso e cotas
Estas etapas mostram como tooview Olá cotas atuais em sua assinatura para recursos específicos do Azure e toosee o percentual de cada cota que você usou.

1. Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Selecione **mais serviços**e, em seguida, selecione **cobrança** da lista de saudação.
1. Na folha de cobrança hello, selecione uma assinatura.
4. Selecione **Uso + cotas**.

   ![Botão Uso e cotas](./media/devtest-lab-scale-lab/devtestlab-usage-and-quotas.png)

   Olá uso + cotas folha é exibida, listando os diferentes recursos disponíveis nessa porcentagem de assinatura e hello da cota de saudação que está sendo usada por recurso.

   ![Cotas e uso](./media/devtest-lab-scale-lab/devtestlab-view-quotas.png)

## <a name="requesting-more-resources-in-your-subscription"></a>Solicitar mais recursos na sua assinatura
Se você atingir um limite de cota, o limite padrão de saudação de um recurso em uma assinatura pode ser aumentado o limite máximo de tooa, conforme descrito em [assinatura do Azure e limites de serviço](https://docs.microsoft.com/azure/azure-subscription-service-limits).

Estas etapas mostram como toorequest uma cota de aumentar a saudação [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Selecione **Mais Serviços**, selecione **Cobrança** e, em seguida, selecione **Uso + cotas**.
1. No uso de saudação + folha de cotas, selecione Olá **solicitar aumentar** botão.

   ![Botão Solicitar aumento](./media/devtest-lab-scale-lab/devtestlab-request-increase.png)

1. toocomplete e enviar solicitação de hello, preencha as informações de saudação necessária em todas as três guias de saudação **nova solicitação de suporte** formulário.

   ![Formulário de solicitação de aumento](./media/devtest-lab-scale-lab/devtestlab-support-form.png)

[Noções básicas sobre os limites do Azure e aumenta](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) fornece mais informações sobre como entrar em contato com o suporte do Azure toorequest uma cota de aumento.



[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a>Próximas etapas
* Explorar Olá [Galeria de modelos do DevTest Labs Azure Resource Manager QuickStart](https://github.com/Azure/azure-devtestlab/tree/master/Samples).
