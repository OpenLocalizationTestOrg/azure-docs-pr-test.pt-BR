---
title: "AAA(deprecated) perguntas Frequentes – publicar e usar aplicativos de aprendizado de máquina no Azure Marketplace | Microsoft Docs"
description: "(preterido) Perguntas frequentes sobre publicação aplicativos de aprendizado de máquina no hello Azure Marketplace"
services: machine-learning
documentationcenter: 
author: bharaths
manager: jhubbard
editor: cgronlun
ms.assetid: 26b3a1e7-8b9a-4004-98bc-17456d4c25e8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: bharaths
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: b3ae45dfff211fe9baccaf54faaf360a8309c780
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-publishing-and-using-machine-learning-apps-in-hello-azure-marketplace-faq"></a>(preterido) Publicar e usar aplicativos de aprendizado de máquina no hello Azure Marketplace: perguntas Frequentes

> [!NOTE]
> O DataMarket e os Serviços de Dados estão sendo desativados e as assinaturas existentes serão desativadas e canceladas a partir de 31/3/2017. Como resultado, este artigo está sendo preterido. 
> 
> Como alternativa, você pode publicar seu toohello experiências de aprendizado de máquina [Cortana Intelligence galeria](https://gallery.cortanaintelligence.com/) para o benefício de saudação da comunidade de ciência de dados hello. Para obter mais informações, consulte [compartilhamento e descobrir recursos na Olá Cortana Intelligence galeria](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).


## <a name="questions-about-consuming-from-marketplace"></a>Perguntas sobre o consumo do Marketplace
**1. Por que recebo Olá a seguinte mensagem de erro depois que forneça entradas para o serviço web de saudação:**

**solicitação de saudação resultou em um erro de back-end ou back-end de tempo limite. equipe de saudação está investigando o problema de saudação. Lamentamos pela inconveniência hello. (500)**

Parâmetros de entrada não podem estar em conformidade toohello o formato necessário para Olá determinado serviço web. Consulte toohello correspondente documentação link toofind Olá formato correto para parâmetros de entrada e as limitações de saudação do serviço web.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

**2. Se copiar link Olá API de serviço da web de saudação que vejo hello "Explorar este conjunto de dados" página e cole-o em outra janela do navegador, as credenciais que devem, use tooaccess Olá resultados e como fazer, vê-los?**

Você deve usar sua conta do Marketplace como saudação de nome de usuário e a chave de conta primária hello como senha hello. chave da conta primária Olá pode ser encontrada no hello **explorar este conjunto de dados** página em descrição Olá Olá web service (clique Olá **Mostrar** botão). resultado Olá pode exibir no navegador de saudação ou talvez esteja disponível muito download, dependendo de qual navegador você está usando.

**3. Por que recebo Olá a seguinte mensagem de erro depois que eu inserir entrada hello para serviço web de saudação na página de "Explorar este conjunto de dados" hello:** 

**Ocorreu um erro inesperado ao processar a sua solicitação. Tente novamente.**

Um ou mais parâmetros de entrada do serviço web podem ter excedido o limite de comprimento de saudação ao consumir o serviço web de saudação no marketplace de saudação **explorar este conjunto de dados** página. Serviços de saudação podem ser chamados com um comprimento de entrada mais usando métodos de HTTP POST. Para obter exemplos, consulte [exemplo soluções que usam R no aprendizado de máquina e publicado tooMarketplace](machine-learning-r-csharp-web-service-examples.md).

**4. Por que eu não vejo qualquer coisa hello "Gerenciador de API" guia int Olá repositório no hello Portal clássico do Azure?** 

Este é um problema conhecido com hello Marketplace de Portal clássico do Azure. Olá equipe trabalha tooresolve esse problema. 

## <a name="questions-about-publishing-from-azure-machine-learning-on-marketplace"></a>Perguntas sobre a publicação de Azure Machine Learning no Marketplace
**1. Por que as minhas transações de logotipos ou imagens não são atualizadas para o meu serviço Web?** 

Logotipos e imagens são armazenadas em cache no portal de publicação hello e pode levar até too10 dias para logotipo novo hello ou tooupdate de imagem no portal de saudação.

**2. Por que é o guia de "Detalhes" hello do meu serviço da web no Marketplace mostrando uma mensagem de erro?**

Há um problema conhecido do Marketplace durante a conexão tooAzure aprendizado de máquina para obter detalhes do serviço. Olá equipe trabalha tooresolve esse problema.

**3. Por que Olá código de exemplo R nos serviços de web do aprendizado de máquina do Azure Olá não funciona para consumir serviços web de saudação no mercado?**

sistemas de autenticação de saudação são diferentes ao se conectar a serviços de web de aprendizado de máquina tooAzure diretamente em comparação com serviços de web toothese tooconnecting por meio de saudação Marketplace. Serviços de saudação no Marketplace são serviços OData, e eles podem ser chamados com os métodos GET ou POST. 

**4. Por que são links de suporte de saudação do meu serviço web oferece não atualizar corretamente para algumas das minhas ofertas?**

links de suporte de saudação são globais por publicador, não por oferta. 

**5. Como eu publico um serviço Web com o modo de entrada em lote no Marketplace?**

modo de entrada de lote Olá atualmente não há suporte nos serviços web do Marketplace.

**6. Quem devo contatar tooget ajuda se tiver perguntas sobre como se tornar um editor de dados, ou se tiver problemas durante a publicação?**

Contate a equipe do Azure Marketplace Olá em < mailto:datamarketbd@microsoft.com > para obter mais informações.

