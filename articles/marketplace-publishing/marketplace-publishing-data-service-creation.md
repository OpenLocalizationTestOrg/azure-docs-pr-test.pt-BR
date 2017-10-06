---
title: "aaaGuide toocreating um serviço de dados para Olá Marketplace | Microsoft Docs"
description: "Instruções detalhadas de como toocreate, certificar e implantar um serviço de dados para compra em hello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 96194198-6991-43b4-918e-ee337e250339
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 0220d357ae0ec89e7d4f6399605850e57c646f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="data-service-publishing-guide-for-hello-azure-marketplace"></a>Guia de publicação de serviço de dados para hello Azure Marketplace
> [!IMPORTANT]
> **Neste momento, não estamos mais realizando a integração de novos editores de Serviço de Dados. Novos serviços de dados não serão ser aprovados para listagem.** Se você tiver um aplicativo de negócios SaaS você gostaria que toopublish em AppSource, você pode encontrar mais informações [aqui](https://appsource.microsoft.com/partners). Se você tiver aplicativos de IaaS ou desenvolvedor de serviço seria como toopublish no Azure Marketplace, você pode encontrar mais informações [aqui](https://azure.microsoft.com/marketplace/programs/certified/).
> 
> 

Depois de concluir a etapa de saudação 1, [criação da conta e o registro](marketplace-publishing-accounts-creation-registration.md), que você é orientado pelos Olá [geral não técnico](marketplace-publishing-pre-requisites.md) e [requisitos técnicos](marketplace-publishing-data-service-creation-prerequisites.md) de um serviço de dados oferta no Azure Marketplace. Agora podemos irá orientá-lo pelas etapas de saudação para criar uma oferta de serviço de dados em Olá [Portal de publicação] [ link-pubportal] para hello Azure Marketplace.

## <a name="1----login-toohello-publishing-portal"></a>1.    Logon toohello Portal de publicação.
Vá muito[https://publish.windowsazure.com](https://publish.windowsazure.com.)

**Para a primeira hora logon tooPublishing Portal, use Olá a mesma conta com a qual o vendedor da sua empresa perfil foi registrada no Centro de desenvolvedores.**  (Mais tarde você pode adicionar qualquer funcionário da sua empresa como um coadministrador no Portal de publicação de saudação).

Clique em Olá **publicar uma Data Services** se esse for o primeiro o logon no portal de publicação Olá Olá lado a lado.

## <a name="2----choose-data-services-in-hello-navigation-menu-on-hello-left-side"></a>2.    Escolha **Data Services** no menu de navegação Olá no lado esquerdo de saudação.
  ![desenho](media/marketplace-publishing-data-service-creation/pubportal-main-nav.png)

## <a name="3----create-a-new-data-service"></a>3.    Crie um novo Serviço de Dados
Preencha título Olá para sua nova oferta de serviço de dados e clique em "+" na saudação à direita.

  ![desenho](media/marketplace-publishing-data-service-creation/step-3.png)

## <a name="4----review-hello-sub-menu-under-hello-newly-created-data-service-in-hello-navigation-menu"></a>4.    Revisão Olá submenu em Olá recém-criados serviço de dados no menu de navegação hello.
Clique em Olá **passo a passo** guia e examinar todas as etapas necessárias necessário toopublish corretamente Olá serviço de dados em hello Azure Marketplace.

> [!TIP]
> Você sempre pode clique nos links de saudação na página de "Passo a passo" hello ou usar guias no submenu da oferta de serviço de dados Olá no lado esquerdo da saudação.
> 
> 

## <a name="5----create-a-new-plan"></a>5.    Crie um novo Plano.
### <a name="offers-plans-transactions"></a>Ofertas, planos, transações.
Cada oferta pode ter vários planos, mas a quantidade mínima de planos é 1 (um). Quando os usuários finais se inscreve tooyour oferta eles se inscrever para uma plano do oferta de saudação. Cada plano define como os usuários finais vai ser capaz de toouse seu serviço.

No momento Azure Marketplace oferece suporte a apenas mensal assinatura transação modelo com base em serviços de dados, ou seja, os usuários finais pagará taxa mensal de acordo com o preço de toohello de plano específico hello, eles inscrito tooand será capaz de tooconsume cada número de mês de transação definida pelo plano de saudação.

Cada transação geralmente definida como o número de registros que o serviço de dados retornará com base em consulta Olá toohello serviço. saudação padrão é 100. Número de transações retornado tooeach consulta será dividido por 100 de número de registros e arredondado até o inteiro mais próximo toohello.

É o Azure Marketplace serviço camada responsabilidade toomonitor (medidor) o número de transações consumida por cada consulta.

> [!IMPORTANT]
> Os usuários finais que atingiu o limite de transação Olá durante o mês de saudação serão impedidos de continuar o serviço de saudação do toouse até o final de seu ciclo de assinatura mensal.
> 
> Olá plano ou um dos planos de saudação pode (mas não deve) incluem um número ilimitado de transações.
> 
> 

### <a name="create-a-plan"></a>Crie um plano.
1. Clique em **"+"** toohello próximo "adicionar um novo plano".
2. Escolha uma das opções de saudação: **Unlimited** ou **limitado** uso para este plano.  Se limitado, em seguida, forneça o número de saudação do plano de saudação transação permitirá tooconsume em um mês.
   
    ![desenho](media/marketplace-publishing-data-service-creation/step-5.1.png)  
   
    Portal de publicação também sugere "Identificador de plano", que será usado toocommunicate toohello os usuários finais Olá nome do plano Olá Olá da interface do usuário e também usada pela Olá tooidentify de serviço do mercado Olá plano. Se desejar, você pode alterar hello "Identificador de plano".
   
   > [!NOTE]
   > Olá "Identificador de plano" deve ser exclusivo no escopo de saudação de cada oferta. Como muitos outros identificadores usado no hello planejar publicação de Portal identificador será bloqueado após hello tooproduction publicação primeiro e você não será capaz de toochange esse identificador.
   > 
   > 
3. Clique em tooaccept sua escolha.
4. Em seguida, você deve responder a algumas perguntas adicionais sobre seu plano recém-criado.
   
    ![desenho](media/marketplace-publishing-data-service-creation/step-5.2.png)

| Pergunta | Significado |
| --- | --- |
| **Este Plano é gratuito e está disponível em todo o mundo?** |Você pode criar um plano totalmente gratuito. Se seu Olá apenas plano para essa oferta – isso significa que você está publicando "Oferecem livre" em Olá Marketplace. Se for somente para um (de alguns) plano, Olá lhe toolearn de usuários finais de toooffer uma opção mais sobre o serviço com um número relativamente pequeno de transações por mês.  Se a resposta de saudação é "Sim", serão solicitadas sem mais perguntas. |

> [!NOTE]
> Os usuários finais podem sempre atualize toohello paga planos.
> 
> 

| Pergunta | Significado |
| --- | --- |
| **Existe uma avaliação gratuita disponível?** |Você pode escolher entre "Sem avaliação" em todos os ou oferecem uma opção toouse seu plano para "Um mês". Editores como toouse esse opção tooprovide os usuários finais Olá possibilidade toounderstand Olá benefícios Olá oferecem gratuitamente por um mês. |

> [!IMPORTANT]
> Os usuários finais só será capaz de toopurchase uma avaliação gratuita se estabelecerem instrumento de pagamento, por exemplo, cartão de crédito, contrato enterprise.
> 
> Depois de um mês de avaliação gratuita hello, Azure Marketplace será iniciado Carregando clientes preço Olá data Olá da assinatura hello, a menos que o cliente Olá iniciou o cancelamento de assinatura de saudação. Nenhuma notificação especial será fornecida toohello os usuários finais.
> 
> 

| Pergunta | Significado |
| --- | --- |
| **Este plano requer um toopurchase de código de promoção?** |Editores têm uma opção toolimit acesso tootheir que planos de serviço, fornecendo um código especial, chamado "A Promocode" toospecific clientes. Somente os usuários finais que terão esse Promocode será capaz de toosubscribe toohello plano. Se você escolher "Não", você concorda que todos da região Olá onde Olá oferecem estão disponível (consulte [guia de conteúdo de Marketing do Marketplace](marketplace-publishing-push-to-staging.md) para obter mais detalhes) será capaz de toosubscribe toothis plano. Não será feita nenhuma outra pergunta. |
| **Ocultar esse plano de qualquer pessoa que não tenha um código de promoção válido?** |Se a pergunta do hello resposta toohello anterior é "Sim" hello publicador tem toocompletely uma opção remover esse plano apareçam nos Olá interface de usuário do Marketplace de saudação. Isso significa que, os clientes não verão este plano na página de detalhes da oferta do hello. Os usuários finais que irá receber um toopurchase promocode, será capaz de toosubscribe tooit usando este promocode. |

## <a name="6----create-your-marketplace-marketing-content"></a>6.    Criar conteúdo de marketing do Marketplace
Para como tooprovide informações necessárias, na **Marketing, preços, suporte e categorias** guias, visite [guia de conteúdo de Marketing do Marketplace](marketplace-publishing-push-to-staging.md) que é comum artefatos tooall publicados em Olá Marketplace do Azure.  

## <a name="7----connect-your-offer-tooyour-service-sql-azure-based-or-web-service-based"></a>7.    Conecte-se tooyour sua oferta de serviço (SQL Azure com base ou serviço da Web com base).
Clique em Olá **Data Services** submenu.

Na metade superior do hello da página Olá deverá da oferta do hello tooprovide **Namespace**.  

  ![desenho](media/marketplace-publishing-data-service-creation/step-7.png)

Olá abaixo pergunta definirá como Olá publicador será tooexpose recém-criado oferta tooAzure Marketplace. (Para obter mais detalhes, consulte Olá [guia pré-requisito técnico de serviços de dados](marketplace-publishing-data-service-creation-prerequisites.md)).

  ![desenho](media/marketplace-publishing-data-service-creation/step-7.2.png)

**Publicando Olá banco de dados com base em serviço**

Clique em **Banco de Dados**. saudação de página a seguir será exibida:

  ![desenho](media/marketplace-publishing-data-service-creation/step-7.3.png)

toocreate um mapeamento de CSDL para Olá conjunto de dados com base em Olá banco de dados do SQL Azure:

  ![desenho](media/marketplace-publishing-data-service-creation/step-7.4.png)

E para cada tabela

  ![desenho](media/marketplace-publishing-data-service-creation/step-7.5.png)

  ![desenho](media/marketplace-publishing-data-service-creation/step-7.6.png)

Se for serviço Web

  ![desenho](media/marketplace-publishing-data-service-creation/step-7.7.png)

> [!IMPORTANT]
> Leitura [mapeamento existente web tooOData de serviço por meio de CSDL](marketplace-publishing-data-service-creation-odata-mapping.md) para obter instruções detalhadas e exemplos para a criação de um serviço Web de CSDL.
> 
> 

## <a name="next-steps"></a>Próximas etapas
Agora que você criou sua oferta de serviço de dados, certifique-se de que você conclua instruções Olá Olá [guia de conteúdo de Marketing do Marketplace](marketplace-publishing-push-to-staging.md) antes de você Avançar muito[Testando seu serviço de dados de preparo](marketplace-publishing-data-service-test-in-staging.md).

## <a name="see-also"></a>Consulte também
* [Guia de Introdução: Como toopublish toohello uma oferta do Azure Marketplace](marketplace-publishing-getting-started.md)
* Se você estiver interessado em entender Olá processo geral de mapeamento de OData e a finalidade, leia este artigo [dados serviço OData mapeamento](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview definições, estruturas e instruções.
* Se você estiver interessado em aprendizado e nós específicos de saudação de compreensão e seus parâmetros, leia este artigo [dados serviço OData mapeamento nós](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) para definições e explicações, exemplos e contexto de casos de uso.
* Se você estiver interessado em examinar os exemplos, leia este artigo [dados serviço OData mapeamento exemplos](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee código de exemplo e entender a sintaxe de código e o contexto.

[link-pubportal]:https://publish.windowsazure.com
