---
title: "aaaProblem a adição de um aplicativo não Galeria | Microsoft Docs"
description: "Entender a face de pessoas problemas comuns Olá durante a adição de aplicativos não-Galeria personalizados"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: cfe9b657ae18cbacaddbd85658471a2c57c9cf95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-adding-a-non-gallery-application"></a>Problema ao adicionar um aplicativo inexistente na galeria

Este artigo ajuda face de pessoas de problemas comuns do toounderstand Olá ao adicionar **aplicativos personalizados de galeria não** e que você pode fazer tooresolve-los. 

## <a name="i-clicked-hello-add-button-and-my-application-took-a-long-time-tooappear"></a>Clique em hello "Adicionar" botão e meu aplicativo levaram um tempo longo tooappear

Em algumas circunstâncias, pode levar de 1 a 2 minutos (e às vezes, mais) para tooappear um aplicativo após adicioná-lo tooyour directory. Embora isso não seja normais de desempenho esperado hello, você pode ver a adição de aplicativo hello está em andamento clicando no hello **notificações** ícone (bell Olá) no superior de saudação à direita da saudação [Portal do Azure](https://portal.azure.com/)e procurando um **em andamento** ou **concluído** notificação rotulada **criar aplicativo**.

Se seu aplicativo nunca é adicionado ou se você encontrar um erro ao clicar Olá **adicionar** botão, você verá um **notificação** em uma **erro** estado. Se você quiser obter mais detalhes sobre Olá erro toolearn tooor mais compartilhar com um engingeer de suporte, você pode ver mais informações sobre erro hello, seguindo as etapas de Olá Olá [como detalhes de saudação toosee de uma notificação de portal](#how-to-see-the-details-of-a-portal-notification) seção.

## <a name="i-clicked-hello-add-button-and-my-application-didnt-appear"></a>Clique em botão de "Adicionar" hello e meu aplicativo não apareceu

Às vezes, devido a problemas de tootransient, problemas de rede ou um erro, adicionando uma falha de aplicativo. Você pode ver isso acontece quando você clica em Olá **notificações** ícone (bell Olá) no canto superior direito Olá Olá Portal do Azure e ver um vermelho (!) tooyour próximo ícone **criar aplicativo** notificação. Isso indica que houve um erro ao criar o aplicativo hello.

Se você encontrar um erro ao clicar Olá **adicionar** botão, você verá um **notificação** em uma **erro** estado. Se você quiser obter mais detalhes sobre Olá erro toolearn tooor mais compartilhar com um engingeer de suporte, você pode ver mais informações sobre erro hello, seguindo as etapas de Olá Olá [como detalhes de saudação toosee de uma notificação de portal](#how-to-see-the-details-of-a-portal-notification) seção.

## <a name="i-dont-know-how-tooset-up-my-application-once-ive-added-it"></a>Não sei como tooset meu aplicativo uma vez adicioná-lo

Se precisar de ajuda para aprender sobre aplicativos personalizados, Olá [biblioteca de documentos de aplicativos do AD do Azure](https://docs.microsoft.com/azure/active-directory/active-directory-apps-index) ajudá-lo a toolearn mais sobre logon único com o Azure AD e como ele funciona.

## <a name="how-toosee-hello-details-of-a-portal-notification"></a>Como detalhes de saudação toosee de uma notificação de portal

Você pode ver os detalhes de saudação de qualquer notificação de portal, seguindo as etapas de saudação abaixo:

1.  Clique em Olá **notificações** ícone (bell Olá) no canto superior direito de saudação do hello Portal do Azure

2.  Selecione qualquer notificação em um **erro** estado (aquelas com um toothem de Avançar vermelho (!)).

   >[!NOTE]
   >Não é possível clicar em notificações com estado de **Êxito** ou **Em Andamento**.
   >
   >

3.  Este Olá abrir **detalhes da notificação** folha.

4.  Use essas informações por conta própria toounderstand mais detalhes sobre o problema de saudação.

5.  Se você ainda precisar de Ajuda, você também pode compartilhar essas informações com um suporte engenheiro ou hello grupo tooget Ajuda do produto com o problema.

6.  Clique em Olá **ícone para copiar** toohello direito da saudação **copiar erro** textbox toocopy todos os Olá tooshare de detalhes de notificação com um engenheiro de suporte ou produto de grupo.

## <a name="how-tooget-help-by-sending-notification-details-tooa-support-engineer"></a>Como ajudar a tooget enviando o engenheiro de suporte de tooa de detalhes de notificação

É muito importante que você compartilhe **todos os detalhes abaixo de Olá** com um engenheiro de suporte se você precisar de Ajuda, para que eles podem ajudá-lo rapidamente. Você pode fazer isso facilmente por **tirar uma captura de tela,** ou clicando Olá **ícone de erro de cópia**, encontrado toohello direito da saudação **copiar erro** caixa de texto.

## <a name="notification-details-explained"></a>Detalhes da notificação explicados

Olá abaixo explica mais que cada um dos itens de notificação Olá significa e fornece exemplos de cada um deles.

### <a name="essential-notification-items"></a>Itens de notificação essenciais

-   **Título** – Olá título descritivo da notificação de saudação
   *  Exemplo – **Configurações do proxy do aplicativo**

-   **Descrição** – Olá descrição do que ocorreu como resultado da operação de saudação

   *  Exemplo – **A URL interna inserida já está sendo usada por outro aplicativo**

-   **Id de notificação** – a id exclusiva Olá da notificação de saudação

   *  Exemplo – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**

-   **Id de solicitação do cliente** – id de solicitação específica de saudação feita pelo seu navegador

   *  Exemplo – **302fd775-3329-4670-a9f3-bea37004f0bc**

-   **Hora UTC de carimbo de data /** – Olá timestamp durante o qual ocorreu notificação hello, em UTC

   *  Exemplo – **2017-03-23T19:50:43.7583681Z**

-   **Id de transação interna** – Olá ID interna, podemos usar erro de saudação toolook em nossos sistemas

   *  Exemplo – **71a2f329-ca29-402f-aa72-bc00a7aca603**

-   **UPN** – usuário Olá que realizou a operação de saudação

   *  Exemplo – **tperkins@f128.info**

-   **Id do locatário** – ID exclusiva de saudação do locatário Olá Olá usuário que realizou a operação de saudação era um membro de

   *  Exemplo – **7918d4b5-0442-4a97-be2d-36f9f9962ece**

-   **Id do objeto de usuário** – Olá ID exclusiva do usuário Olá que realizou a operação de saudação

 *  Exemplo – **17f84be4-51f8-483a-b533-383791227a99**

### <a name="detailed-notification-items"></a>Itens de notificação detalhados

-   **Nome de exibição** – **(pode estar vazia)** um nome para exibição mais detalhado para o erro Olá

  *  Exemplo – **Configurações do proxy do aplicativo**

-   **Status** – Olá status específicos de notificação de saudação

   *  Exemplo – **Falha**

-   **Id de objeto** – **(pode estar vazia)** Olá ID de objeto em relação a quais Olá a operação foi executada

   *  Exemplo – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**

-   **Detalhes** – Olá descrição detalhada do que ocorreu como resultado da operação de saudação

   *  Exemplo – **A URL interna 'http://bing.com/' é inválida, uma vez que está sendo utilizada**

-   **Erro de cópia** – clique Olá **ícone para copiar** toohello direito da saudação **copiar erro** textbox toocopy todos os Olá tooshare de detalhes de notificação com um engenheiro de suporte ou produto de grupo

   *  Exemplo ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```

## <a name="next-steps"></a>Próximas etapas
[Gerenciando aplicativos com o Azure Active Directory](active-directory-enable-sso-scenario.md)



