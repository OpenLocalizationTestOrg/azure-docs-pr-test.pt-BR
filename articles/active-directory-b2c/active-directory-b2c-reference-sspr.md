---
title: "Azure Active Directory B2C: autoatendimento de redefinição de senha | Microsoft Docs"
description: "Um tópico demonstra como a redefinição de tooset a senha de autoatendimento para seus consumidores no Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: curtand
ms.assetid: c87ed86e-1520-42b1-8c31-46cd44ed5310
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: ff87eea42259b610702da73af35d0a38eb7dd33d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-set-up-self-service-password-reset-for-your-consumers"></a>Azure Active Directory B2C: configurar a redefinição de senha por autoatendimento para seus consumidores
Olá com o recurso de redefinição de senha de autoatendimento, seus consumidores (que se inscreveram para contas locais) podem redefinir suas senhas em seus próprios. Isso reduz significativamente carga Olá em sua equipe de suporte, especialmente se seu aplicativo tiver milhões de consumidores usá-lo regularmente. Atualmente, só há suporte para usar um endereço de email verificado como um método de recuperação. Vamos adicionar métodos de recuperação adicionais (número de telefone verificado, perguntas de segurança, etc.) em um futuro hello.

> [!NOTE]
> Este artigo se aplica a senha de serviço tooself usada no contexto de saudação de uma política de redefinição. Se precisar de políticas de redefinição de senha totalmente personalizáveis invocadas por meio de seu aplicativo, veja [este artigo](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).
> 
> 

Por padrão, o diretório não terá a redefinição de senha por autoatendimento ativada. Use Olá seguindo as etapas tooturn-lo em:

1. Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com/) como Olá administrador da assinatura. Isso é hello mesmo trabalho ou conta escolar ou Olá a mesma conta da Microsoft que você usou toocreate seu diretório.
2. Navegue a extensão do Active Directory toohello na barra de navegação Olá no lado esquerdo da saudação.
3. Localizar seu diretório de saudação **diretório** guia e clique nele.
4. Clique em Olá **configurar** guia.
5. Role para baixo toohello **política de redefinição de senha do usuário** seção e alternar Olá **usuários habilitados para redefinição de senha** opção muito**Sim**. Observe que Olá **endereço de Email alternativo** opção estiver marcada; deixe-o como está.
   
    ![Redefinição de senha de autoatendimento](./media/active-directory-b2c-reference-sspr/sspr.png)
6. Clique em **salvar** final Olá Olá página. Pronto!

tootest, o recurso de "Executar agora" hello use em qualquer política de entrada que tem as contas locais como um provedor de identidade. Na saudação conta local entrar página (em que você inserir um endereço de email e senha, ou um nome de usuário e senha), clique em **não é possível acessar sua conta?** experiência do consumidor Olá tooverify.

> [!NOTE]
> Olá páginas de redefinição de senha de autoatendimento podem ser personalizadas usando Olá [marca do recurso da empresa](../active-directory/active-directory-add-company-branding.md).
> 
> 

