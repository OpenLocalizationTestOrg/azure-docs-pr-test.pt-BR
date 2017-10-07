---
title: "aaaView Olá mensal laboratório estimado tendência de custos no Azure DevTest Labs | Microsoft Docs"
description: "Saiba mais sobre o gráfico de tendências de custo estimado mensal do hello Azure DevTest Labs."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 1f46fdc5-d917-46e3-a1ea-f6dd41212ba4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: 47c7dd4cf91b76de74b502c50f05e79cd501ee35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="view-hello-monthly-estimated-lab-cost-trend-in-azure-devtest-labs"></a>Exibição Olá mensal laboratório estimado tendência de custos no Azure DevTest Labs
recurso de gerenciamento de custos de saudação do DevTest Labs ajuda a acompanhar o custo de saudação do seu laboratório. Este artigo ilustra como Olá toouse **mensal tendências de custo estimado** tooview gráfico Olá estimado custo acumulado do mês do calendário atual e Olá custo final do mês projetado para Olá mês do calendário atual. Neste artigo, você aprenderá como tooview Olá mensal gráfico de tendências de custo estimado em Olá portal do Azure.

## <a name="viewing-hello-monthly-estimated-cost-trend-chart"></a>Exibir gráfico de tendência mensal de custo estimado de saudação
Olá tooview gráfico de tendência mensal de custo estimado, siga estas etapas: 

1. Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de saudação.
3. Saudação de laboratórios, selecione lista laboratório desejado hello.   
4. Na folha do laboratório hello, selecione **configurações de custo**.
5. No laboratório de saudação **configurações de custo** folha, selecione **tendências de custo de laboratório**.
6. Olá, captura de tela a seguir mostra um exemplo de um gráfico de custo. 
   
    ![Gráfico de custo](./media/devtest-lab-configure-cost-management/graph.png)

Olá **custo estimado** valor é bom dia estimado custo acumulado do mês do calendário atual. Olá **custo projetado** hello custo estimado de saudação todo mês do calendário atual, calculado usando custo de laboratório Olá para Olá cinco dias anteriores.

os valores de custo Olá são arredondados toohello próximo número de inteiro. Por exemplo: 

* Arredonda 5.01 too6 
* Arredonda 5.50 too6
* Arredonda 5.99 too6

Como ele declara acima gráfico hello, custos Olá exibidos no gráfico de saudação são *estimado* custos usando [pré-pago](https://azure.microsoft.com/offers/ms-azr-0003p/) oferecem taxas.
Além disso, Olá seguem *não* incluído no cálculo do custo de saudação:

* As assinaturas do Dreamspark e o CSP não há suporte atualmente como Azure DevTest Labs usa Olá [APIs de cobrança do Azure](../billing/billing-usage-rate-card-overview.md) toocalculate laboratório de saudação de custo, que não dá suporte a assinaturas do Dreamspark ou de CSP.
* Suas tarifas da oferta. No momento, não estamos toouse capaz de suas taxas de oferta (mostradas em sua assinatura) que você tenha negociado com a Microsoft ou Microsoft parceiros. Estamos usando as tarifas pré-pagas.
* Seus impostos
* Seus descontos
* Sua moeda de cobrança. No momento, o custo de laboratório Olá é exibido apenas na moeda USD.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Postagens de blogs relacionadas
* [Dois tookeep coisas mais seu custo na faixa de DevTest Labs](https://blogs.msdn.microsoft.com/devtestlab/2016/06/21/keep-your-cost-on-track/)
* [Por que os limites de custo?](https://blogs.msdn.microsoft.com/devtestlab/2016/04/11/why-cost-thresholds/)

## <a name="next-steps"></a>Próximas etapas
Aqui estão algumas coisas tootry lado:

* [Definir políticas de laboratório](devtest-lab-set-lab-policy.md) -Saiba como tooset Olá várias políticas usadas toogovern como seu laboratório e suas VMs são usados. 
* [Criar imagem personalizada](devtest-lab-create-template.md) – durante a criação de uma VM, você especifica uma base, que pode ser uma imagem personalizada ou uma imagem do Marketplace. Este artigo ilustra como toocreate um personalizado da imagem de um arquivo VHD.
* [Configurar imagens do Marketplace](devtest-lab-configure-marketplace-images.md) — os DevTest Labs dão suporte à criação de VMs com base em imagens do Azure Marketplace. Este artigo ilustra como toospecify que, se houver, imagens do Azure Marketplace podem ser usado ao criar máquinas virtuais em um laboratório.
* [Criar uma máquina virtual em um laboratório](devtest-lab-add-vm-with-artifacts.md) -ilustra como toocreate uma VM por meio de uma imagem de base (ou personalizadas ou Marketplace) e como toowork com artefatos em sua VM.

