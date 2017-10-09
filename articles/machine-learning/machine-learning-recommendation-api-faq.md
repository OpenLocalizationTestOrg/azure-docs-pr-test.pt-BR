---
title: "Olá aaaSet backup e use a API de recomendações de aprendizado de máquina | Microsoft Docs"
description: "API de RECOMENDAÇÕES da Microsoft criada com as perguntas Frequentes do Azure Machine Learning"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 1ffc3c16-e040-4225-9d72-105129938dfa
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: 980bf1a36f3291275d9ef0fee9b4446f7e0cbecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-and-using-machine-learning-recommendations-api-faq"></a>Perguntas frequentes sobre configuração e uso da API de Recomendações do Machine Learning
**O que são as RECOMENDAÇÕES?**

> [!NOTE]
> Deve começar a usar o hello recomendações API cognitivas serviço em vez de nesta versão. Olá serviço cognitivas recomendações será substituído por esse serviço e todos os novos recursos de saudação serão desenvolvidos existe. Ele possui novos recursos como suporte ao processamento em lotes, um Gerenciador de API aprimorado, uma superfície de API mais limpa, uma experiência de inscrição/cobrança mais consistente etc.
> Saiba mais sobre [toohello migrando novo serviço cognitivas](http://aka.ms/recomigrate)
> 
> 

Para organizações e empresas que dependem de venda toocross recomendações e a venda produtos e clientes de tootheir de serviços, as recomendações no aprendizado de máquina do Azure fornece um mecanismo de recomendações de autoatendimento. É uma implementação de filtragem  colaborativa que usa a fatoração de matriz como seu algoritmo central. Os desenvolvedores de aplicativos podem acessar RECOMENDAÇÕES usando APIs REST. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

**O que posso fazer com as RECOMENDAÇÕES?**

RECOMENDAÇÕES utiliza como entrada um item ou um conjunto de itens e retorna uma lista de recomendações relevantes. Por exemplo: um cliente de uma loja online clica em um produto. loja online Olá envia esse produto como entrada tooRECOMMENDATIONS, obtém uma lista de produtos de retorno e decide qual desses produtos serão mostradas toohello cliente. Você pode desejar toouse recomendações toooptimize sua loja online ou até mesmo tooinform seu interior center chamada ou o departamento de vendas.

**Há limitações de uso?**

Recomendações tem Olá limitações de uso a seguir:

* Número máximo de modelos por assinatura: 10
* Número máximo de itens que um catálogo pode conter: 100.000
* número máximo de saudação de pontos de uso que são mantidos é ~ 5.000.000. Olá mais antigo será excluído se novas serão carregadas ou relatadas.
* O volume máximo de dados que podem ser enviados no email (por exemplo, importar dados de catálogo e importar dados de uso) é de 200 MB.
* O número de TPS (transações por segundo) para um build de modelo da Recomendação que não está ativo é de cerca de 2 TPS. Uma compilação de modelo de recomendações está ativa pode conter backup too20 TPS.

## <a name="purchase-and-billing"></a>Compra e cobrança
**Quanto custa recomendações durante o período de início Olá?**

As Recomendações são um serviço por assinatura. A cobrança é feita com base no volume de transações por mês. Você pode verificar Olá [oferecem página](https://datamarket.azure.com/dataset/amla/recommendations) no Microsoft Azure Marketplace para obter informações sobre preços.

**Existem custos associados a fazer as Recomendações acompanharem e armazenarem a atividade do usuário para mim?**

Não no momento da saudação.

**As Recomendações têm uma avaliação gratuita?**

Há uma trilha livre que é restrita too10, 000 transações por mês.

**Quando serei cobrado por Recomendações?**

Uma assinatura paga é qualquer assinatura para a qual há uma taxa mensal. Quando você compra uma assinatura paga, você é cobrado imediatamente para Olá primeiro uso do mês. Você é cobrado quantidade Olá associado a oferta de saudação na página de assinatura da saudação (mais impostos aplicáveis). A cobrança mensal é feita por mês em Olá mesmo calendário data da sua primeira compra até cancelar a assinatura de saudação. 

**Como atualizar o serviço de camada superior tooa?**

Você pode comprar ou atualizar sua assinatura do hello [oferecem página](https://datamarket.azure.com/dataset/amla/recommendations) página no Microsoft Azure Marketplace.

Quando você atualiza uma assinatura:

* As transações que permanecem em sua antiga assinatura não serão adicionadas tooyour nova assinatura. 
* Você paga o preço total para nova assinatura de hello, mesmo que haja transações não utilizadas em sua antiga assinatura.

Processo tooupgrade uma assinatura:

* Nevigate toohello [oferecem página](https://datamarket.azure.com/dataset/amla/recommendations).
* Entrar no Marketplace de toohello se você ainda não tiver entrado.
* No painel direito da saudação, todos os planos de saudação disponíveis são listados. Clique o botão de opção de saudação plano Olá para que deseja tooupgrade.
* Se você quiser tooupgrade, clique em **Okey**. Se você não quiser tooupgrade, clique em **Cancelar**.

**Importante** caixa de diálogo Olá leia com atenção antes de atualizar porque há implicações de cobrança e uso.

**Quando terminará tooRecommendations minha assinatura?**

Sua assinatura será encerrada quando você a cancelar. Se você quiser toocancel suas assinaturas, consulte Olá instruções a seguir.

**Como cancelo minha assinatura de Recomendações?**

toocancel sua assinatura, use Olá seguindo as etapas. Se sua assinatura atual for uma assinatura paga, sua assinatura continua em vigor até o final de saudação do hello atual período de cobrança. Se você precisar hello cancelamento toobe efetiva imediatamente, entre em contato conosco em [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).

**Observação** nenhum reembolso é concedido se você cancelar antes do final de saudação de um período de cobrança ou por transações não utilizadas em um período de cobrança.

* Navegue toohello [oferecem página](https://datamarket.azure.com/dataset/amla/recommendations).
* Entrar no Marketplace de toohello se você ainda não tiver entrado.
* Clique em **Cancelar** toohello direita do nome do conjunto de dados hello e status. Você pode usar essa assinatura até o final de saudação do hello atual de seu limite de transação ou de período de cobrança é atingido (o que ocorrer primeiro).

Se você quiser toocancel sua assinatura imediatamente assim que você pode adquirir uma nova assinatura, uma permissão no arquivo [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).

## <a name="getting-started-with-recommendations"></a>Introdução às Recomendações
**As Recomendações são para mim?** 

As recomendações no aprendizado de máquina é para organizações e empresas que dependem de recomendações toocross venda e vendas produtos ou serviços tootheir clientes. Se você tiver um site voltado para o cliente, uma equipe de vendas, uma equipe de vendas interna ou um call center e se oferecer um catálogo de mais de algumas dezenas de produtos ou serviços, seu resultado final poderá se beneficiar do uso de Recomendações. 

Experimentar recomendações é projetado toobe bastante simples. Olá atual API versão exige habilidades básicas de programação. Se você precisar de assistência, contate o fornecedor de saudação que desenvolveu o seu site. Se você tiver um departamento de TI interno ou desenvolvedor interno, eles devem ser capazes de tooget toowork de recomendações para você. 

**Quais são os pré-requisitos de saudação para configuração de recomendações?**

Recomendações exige que você tenha um log de opções de usuário relacionado tooyour catálogo. Se você não tiver um log e tiver um site voltado para o cliente, as Recomendações poderão coletar a atividade de usuário para você. 

As Recomendações também exigem um catálogo de produtos ou serviços. Se você não tiver o catálogo Olá, recomendações podem dados de uso do cliente real hello e criar um catálogo. Um catálogo implícito não incluirá itens que não tenham sido relatados como parte das transações de usuário.

**Como configurar as recomendações para Olá primeira vez?**

Depois de [assinatura](https://datamarket.azure.com/dataset/amla/recommendations) tooRecommendations, você deve usar a documentação da API de saudação em Olá [recomendações de aprendizado de máquina do Azure - guia de início rápido](machine-learning-recommendation-api-quick-start-guide.md) tooset o serviço de saudação.

**Onde posso encontrar a documentação da API?** 

Olá documentação da API é [recomendações de aprendizado de máquina do Azure-guia de início rápido](machine-learning-recommendation-api-quick-start-guide.md).

**O que fazem opções tenho tooRecommendations de dados de catálogo e o uso de tooupload?**

Você tem duas opções para carregar os dados de catálogo e de uso: você pode exportar os dados de saudação do seu sistema CRM ou outros logs e carregá-lo tooRecommendations, ou você pode adicionar marcas tooyour site controlar atividades de usuário. Se você usar o método último hello, Olá dados serão armazenados no Azure.

## <a name="maintenance-and-support"></a>Manutenção e suporte
**Que tamanho meu conjunto de dados pode ter?**

Cada conjunto de dados pode conter too100, 000 itens de catálogo e too2048 MB de dados de uso.
Além disso, uma assinatura pode conter os conjuntos de dados de too10 (modelos).

**Onde posso obter suporte técnico para Recomendações?**

O suporte técnico está disponível no hello [suporte do Microsoft Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=MachineLearning) site.

**Onde encontrar os termos de uso do Olá?**

[Termos de Serviço da API de Recomendações do Microsoft Azure Machine Learning](https://datamarket.azure.com/dataset/amla/recommendations#terms).

