---
title: "Azure Active Directory B2C: Desabilitar a verificação de email durante a inscrição do consumidor | Microsoft Docs"
description: "Um tópico demonstra como toodisable email verificação durante a inscrição no Azure Active Directory B2C do consumidor"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 433f32b8-96d2-4113-aa82-efcf42fa9827
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/06/2017
ms.author: parakhj
ms.openlocfilehash: a8a42eddcb577725f04d70e1b1ebbebf10b5937c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-disable-email-verification-during-consumer-sign-up"></a>Azure Active Directory B2C: Desabilitar a verificação de email durante a inscrição do consumidor
Quando habilitada, B2C do Azure Active Directory (AD do Azure) fornece um consumidor Olá toosign de capacidade para aplicativos fornecendo um endereço de email e criar uma conta local. B2C do AD do Azure garante endereços de email válidos exigindo que os consumidores tooverify-los durante o processo de inscrição hello. Ele também impede que um processo automatizado mal-intencionado gerar falsas contas para aplicativos de saudação.

Alguns desenvolvedores de aplicativo preferem tooskip verificação de email durante o processo de inscrição hello e em vez disso, tem consumidores verificar o endereço de email hello mais tarde. toosupport, B2C do Azure AD pode ser configurado toodisable de verificação do email. Isso cria um processo de inscrição mais suave e oferece aos desenvolvedores Olá flexibilidade toodifferentiate Olá os consumidores que verificaram seu endereço de email de que esses clientes que não tenham.

Por padrão, as políticas de inscrição têm a verificação de email ativada. Use Olá seguindo as etapas tooturn-desativar:

1. [Siga essas folha de recursos etapas toonavigate toohello B2C Olá portal do Azure](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. Clique em **Políticas de inscrição** ou em **Políticas de inscrição ou entrada** dependendo do que você configurou para inscrição.
3. Clique em sua política (por exemplo, "B2C_1_SiUp") tooopen-lo. Clique em **editar** na parte superior de saudação da folha de saudação.
4. Clique em **Personalização da interface do usuário da página**.
5. Clique em **Página de inscrição da conta local**.
6. Clique em **endereço de Email** em Olá **nome** coluna sob Olá **inscrição atributos** seção.
7. Saudação de alternância **Exigir verificação** opção muito**não**.
8. Clique em **Okey** na parte inferior da saudação até chegar Olá **Editar política** folha.
9. Clique em **salvar** na parte superior de saudação da folha de saudação. Pronto!

> [!NOTE]
> Desabilitar a verificação de email no processo de inscrição Olá pode levar toospam. Se você desabilitar o saudação padrão, é recomendável adicionar seu próprio sistema de verificação.
> 
> 

Estamos sempre abrir toofeedback e sugestões! Se você tiver dificuldade com este tópico ou ter recomendações para melhorar este conteúdo, Apreciamos seus comentários na parte inferior da saudação da página de saudação. Para solicitações de recurso, adicioná-los muito[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).
