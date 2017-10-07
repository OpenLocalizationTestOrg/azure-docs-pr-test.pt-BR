---
title: "aaaTesting seu serviço de dados oferecem para Olá Marketplace | Microsoft Docs"
description: "Entenda como tootest seu serviço de dados oferecem para hello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e861bd11-f74d-4d77-b4b5-23fb463644ad
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 1b9c7027d8e0818b9bdee5cfca971bab25dd1959
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="testing-your-data-service-offer-in-staging"></a>Testando sua oferta do Serviço de Dados no preparo
> [!IMPORTANT]
> **Neste momento, não estamos mais realizando a integração de novos editores de Serviço de Dados. Novos serviços de dados não serão ser aprovados para listagem.** Se você tiver um aplicativo de negócios SaaS você gostaria que toopublish em AppSource, você pode encontrar mais informações [aqui](https://appsource.microsoft.com/partners). Se você tiver aplicativos de IaaS ou desenvolvedor de serviço seria como toopublish no Azure Marketplace, você pode encontrar mais informações [aqui](https://azure.microsoft.com/marketplace/programs/certified/).
> 
> 

Depois de concluir as duas primeiras etapas saudação do [criação de sua conta do Microsoft Developer](marketplace-publishing-accounts-creation-registration.md) e [criando sua oferta de serviço de dados no Portal de publicação](marketplace-publishing-data-service-creation.md) você está pronto para disponibilizar sua oferta no Olá Marketplace do Azure. Este tópico orientará Olá primeiro, intermediário, chamada "preparação" de etapa

Preparo significa Implantando sua oferta em uma "área restrita" onde você pode testar e verificar sua funcionalidade antes de enviar a ele tooproduction particular. oferta Hello serão exibidos no preparo como faria cliente tooa que implantou a ele.

## <a name="step-1-pushing-your-offer-toostaging"></a>Etapa 1. Enviar por push toostaging sua oferta
Enviar por push toostaging sua oferta permite que você tootest oferta de saudação antes de se tornar disponível toofuture assinantes.  Você pode ver como sua oferta aparecerá e funcione para aqueles que se inscreveram tooyour dados.  

  ![desenho](media/marketplace-publishing-data-service-test-in-staging/step-1.1.png)

1. Fazer logon no hello [Portal de publicação](https://publish.windowsazure.com)
2. Selecione **Data Services** na janela de navegação à esquerda da saudação
3. Selecione a oferta desejada toopush toostaging. Você verá Olá acima da tela.
4. Clique em **Push tooStaging** botão.  
5. Se houver problemas com hello oferta que necessário toobe concluída toostaging toopushing anterior, você verá uma lista exibida.  Corrija esses itens clicando em cada item na lista de saudação. Quando todas as correções feitas, clique em **Push tooStaging** novamente.

Se não houver nenhum problema com sua oferta você verá a janela pop-up de saudação abaixo.  

Se você não estiver planejando/não aprovado toosurface sua oferta no Portal do Azure (atualmente tem capacidade limitada), e a janela pop-up Olá apenas fechar.

tootest seus dados de serviço no Portal do Azure (no portal de DataMarket de toohello adição), você precisará tootest uma ID de assinatura do Azure com.  Essa ID de assinatura identificará conta Olá que será permitido tootest sua oferta.  

Recorte e cole sua ID de assinatura e clique em Olá toocontinue de marca de seleção.

  ![desenho](media/marketplace-publishing-data-service-test-in-staging/step-1.2.png)

> [!NOTE]
> Essas identificações de assinaturas do Azure só são necessários para teste e no hello [Portal de gerenciamento](https://manage.windowsazure.com). Eles não são necessário tootest no Azure Marketplace.
> 
> 

Olá próxima tela exibida mostra que a publicação está ocorrendo exibindo hello "em andamento" ícone realçado amarelo abaixo. Enviar por push toostaging leva de 10 minutos too15.  Se levar mais tempo, primeiro atualize seu navegador (pressione F5 no IE).  Olá raros casos em que sua oferta é ainda envio por push toostaging após uma hora, clique em contato Olá nos vincular toolet nos saber se há um problema.

  ![desenho](media/marketplace-publishing-data-service-test-in-staging/step-1.3.png)

Quando Olá Push tooStaging conclui hello "em andamento" ícone irá parar mover e Olá status será atualizado muito "preparação".  Você está agora pronto tootest sua oferta.  

## <a name="step-2-test-your-staged-offer-in-datamarket"></a>Etapa 2. Testar sua oferta preparada no DataMarket
Clique em link Olá depois do texto de saudação **"ver seu serviço oferecem em...."** tela hello toodisplay que Olá assinante será exibida quando a sua oferta fica tooproduction e aparecerá no DataMarket.

  ![desenho](media/marketplace-publishing-data-service-test-in-staging/step-2.2.png)

Teste ou verifique se cada um dos 12 itens de saudação marcado acima tooensure todos os logotipos, preços/transações, texto, imagens, documentação e links estão corretas e funcionando corretamente.  Este é um tooensure bom momento quaisquer valores de teste inseridos durante a criação de sua oferta foram substituídos por valores reais.

1. Logotipo da oferta
2. Nome da oferta
3. Site da empresa das tooyour de link do nome do publicador
4. Pesquisar categorias para a oferta
5. Assinantes de tooassist de link de suporte da oferta
6. Descrição contextual da oferta
7. Plano de oferta que descreve os detalhes de cobrança
8. Código de tooimplementation de link
9. Imagens de exemplo que ilustram o uso dos dados da oferta
10. Metadados de entrada/saída para cada serviço na oferta de saudação
11. Termos de Uso da oferta
12. Visualização dos dados da oferta do hello

Finalmente, verifique o serviço Olá funcionará por meio de saudação do Datamarket clicando o link hello "Explorar este conjunto de dados".  Uma nova janela será aberta na ferramenta Olá chamamos "Gerenciador de serviços" para que você pode visualizar os resultados de saudação de uma consulta em relação a seu serviço.  Nessa janela, você pode inserir Olá parâmetros necessários e ver os resultados de saudação exibidos a partir de uma consulta em relação a seu serviço.   Além disso, exibido é Olá URL para a sua consulta.  

> [!NOTE]
> Ser se tooreview Olá descrição textual Olá serviço exibida na parte superior da saudação.  E se sua oferta consiste em mais de um serviço chamam, clique nas guias de saudação em Olá inferior tooswitch toohello próximo serviço tooreview e teste.
> 
> 

## <a name="next-step"></a>Próxima etapa
Se você estiver tendo problemas e precisar de ajuda para resolvê-los, entre em contato com o [Suporte do Editor do Azure](http://go.microsoft.com/fwlink/?LinkId=272975).

Se você estiver satisfeito e pronto toopublish sua oferta, leia Olá [solicitar aprovação tooPush tooProduction](marketplace-publishing-push-to-production.md) documentação.

## <a name="see-also"></a>Consulte também
* [Guia de Introdução: Como toopublish toohello uma oferta do Azure Marketplace](marketplace-publishing-getting-started.md)

