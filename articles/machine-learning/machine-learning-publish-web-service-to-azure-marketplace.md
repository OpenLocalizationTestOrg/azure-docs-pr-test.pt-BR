---
title: "tooAzure de serviço web Marketplace de aprendizado de máquina de publicação de AAA(deprecated) | Microsoft Docs"
description: "(preterido) Como toopublish toohello seu serviço de Web de aprendizado de máquina do Azure Marketplace do Azure"
services: machine-learning
documentationcenter: 
author: BharathS
manager: jhubbard
editor: cgronlun
ms.assetid: 68e908be-3a99-4cd7-9517-e2b5f2f341b8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: bharaths
ROBOTS: NOINDEX
redirect_url: machine-learning-gallery-experiments
redirect_document_id: True
ms.openlocfilehash: 149abc3df9b79c1b37d233d5e85e803592ff1020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-publish-azure-machine-learning-web-service-toohello-azure-marketplace"></a>(preterido) Publicar o serviço de Web de aprendizado de máquina do Azure toohello Azure Marketplace

> [!NOTE]
> O DataMarket e os Serviços de Dados estão sendo desativados e as assinaturas existentes serão desativadas e canceladas a partir de 31/3/2017. Como resultado, este artigo está sendo preterido. 
> 
> Como alternativa, você pode publicar seu toohello experiências de aprendizado de máquina [Cortana Intelligence galeria](https://gallery.cortanaintelligence.com/) para o benefício de saudação da comunidade de ciência de dados hello. Para obter mais informações, consulte [compartilhamento e descobrir recursos na Olá Cortana Intelligence galeria](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).

Olá Marketplace do Azure fornece a capacidade de saudação toopublish dos serviços web de aprendizado de máquina do Azure como paga ou libere serviços para consumo por clientes externos. Este artigo fornece uma visão geral do processo com links tooguidelines tooget que é iniciado. Usando esse processo, você pode tornar seus serviços web disponíveis para outros desenvolvedores tooconsume em seus aplicativos.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview-of-hello-publishing-process"></a>Visão geral do processo de publicação de saudação
Olá seguem etapas Olá para publicar um tooAzure de serviço web do aprendizado de máquina do Azure Marketplace:

1. Criar e publicar um RRS (serviço de Solicitação-Resposta) do Machine Learning
2. Implantar Olá tooproduction de serviço e obter Olá informações de ponto de extremidade OData e chave de API.
3. URL de saudação de uso de saudação publicada toopublish de serviço web muito[Azure Marketplace (Data Market)](https://publish.windowsazure.com/workspace/) 
4. Quando enviado, a sua oferta é analisada e precisa toobe aprovada antes dos clientes pode começar a compra-lo. o processo de publicação Olá pode levar alguns dias. 

## <a name="walk-through"></a>Passo a passo
### <a name="step-1-create-and-publish-a-machine-learning-request-response-service-rrs"></a>Etapa 1: criar e publicar um RRS (serviço de Solicitação-Resposta) do Machine Learning
 Se você ainda não fez isso, consulte o [passo a passo](machine-learning-walkthrough-5-publish-web-service.md).

### <a name="step-2-deploy-hello-service-tooproduction-and-obtain-hello-api-key-and-odata-endpoint-information"></a>Etapa 2: Implantar Olá tooproduction de serviço e obter Olá informações de ponto de extremidade OData e chave de API
1. De saudação [Portal clássico do Azure](http://manage.windowsazure.com), selecione Olá **APRENDIZADO de máquina** opção da barra de navegação à esquerda do hello e selecione seu espaço de trabalho. 
2. Clique em Olá **serviços WEB** guia e selecione Olá web serviço toopublish toohello marketplace.
   
    ![Azure Marketplace][workspace]
3. Selecione o ponto de extremidade de saudação você como toohave Olá marketplace consumiria. Se você não criou nenhum ponto de extremidade adicionais, você pode selecionar Olá **padrão** ponto de extremidade.
4. Depois de clicar no ponto de extremidade hello, será capaz de toosee Olá **chave API**. Você precisará dessa informação posteriormente na Etapa 3, então, faça uma cópia dela.
   
    ![Azure Marketplace][apikey]
5. Clique em Olá **solicitação/resposta** toohello marketplace de serviços do método, neste momento, não há suporte para execução de lote de publicação. Isso o levará toohello API a página de ajuda para o método de solicitação/resposta de saudação.
6. Saudação de cópia **endereço de ponto de extremidade OData**, você precisará dessas informações posteriormente na etapa 3.
   
    ![Azure Marketplace][odata]

Implante o serviço de saudação em produção.

### <a name="step-3-use-hello-url-of-hello-published-web-service-toopublish-tooazure-marketplace-datamarket"></a>Etapa 3: Use URL Olá Olá publicado web serviço toopublish tooAzure Marketplace (DataMarket)
1. Navegue muito[Azure Marketplace (Data Market)](http://datamarket.azure.com/home) 
2. Clique em Olá **publicar** link na parte superior de saudação da página de saudação. Isso o levará toohello [Portal de publicação do Microsoft Azure](https://publish.windowsazure.com)
3. Clique em Olá **editores** tooregister seção como um publicador.
4. Quando criar uma nova oferta, selecione **Serviços de Dados**, em seguida, clique em **Criar um novo serviço de dados**. 
   
   ![Azure Marketplace][image1]
   
   <br />
5. Em **Planos** , forneça informações sobre sua oferta, incluindo um plano de preços. Decida se você oferecerá um serviço gratuito ou pago. tooget pago, fornecer informações de pagamento, como as informações do banco e imposto.
6. Em **Marketing** fornecem informações sobre sua oferta, como título hello e uma descrição para sua oferta.
7. Em **preços** você pode definir preços Olá para seus planos para países específicos ou permitir que o sistema hello "autoprice" sua oferta.
8. Em Olá **serviço de dados** , clique em **Web Service** como Olá **fonte de dados**.
   
    ![Azure Marketplace][image2]
9. Obter chave de API e a URL de serviço de web do hello de saudação Portal clássico do Azure, conforme explicado na etapa 2 acima.
10. Na caixa de diálogo Instalação do serviço de dados do Marketplace hello, cole endereço de ponto de extremidade OData Olá Olá **URL do serviço** caixa de texto.
11. Para **autenticação**, escolha **cabeçalho** como Olá **esquema de autenticação**.
    
    * Digite "Autorização" hello **nome de cabeçalho**.
    * Para Olá **o valor do cabeçalho**, digite "Portador" (sem aspas Olá), clique em Olá **espaço** barra e, em seguida, cole a chave de API de saudação.
    * Selecione Olá **este serviço é OData** caixa de seleção.
    * Clique em **Conexão de teste** tootest conexão de saudação.
12. Em **Categorias**, verifique se **Machine Learning** está selecionado.
13. Quando você terminar de inserir todas Olá metadados sobre sua oferta, clique em **publicar**e, em seguida, **Push tooStaging**. Neste ponto, você será notificado de outros problemas que você precisa toofix.
14. Após ter assegurado conclusão de todos os problemas pendentes de saudação, clique em **solicitar aprovação toopush tooProduction**. o processo de publicação Olá pode levar alguns dias. 

[image1]:./media/machine-learning-publish-web-service-to-azure-marketplace/image1.png
[image2]:./media/machine-learning-publish-web-service-to-azure-marketplace/image2.png
[workspace]:./media/machine-learning-publish-web-service-to-azure-marketplace/selectworkspace.png
[apikey]:./media/machine-learning-publish-web-service-to-azure-marketplace/apikey.png
[odata]:./media/machine-learning-publish-web-service-to-azure-marketplace/odata.png

