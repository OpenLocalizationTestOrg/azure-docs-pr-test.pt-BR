---
title: aaaAzure MFA entrar com a verificacao | Microsoft Docs
description: "Esta página fornece orientação sobre onde toogo toosee Olá vários métodos de entrada disponíveis com o Azure MFA."
keywords: "autenticação do usuário, experiência de conexão, conectar com telefone celular, conectar com telefone do escritório"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b310b762-471b-4b26-887a-a321c9e81d46
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/02/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: end-user
ms.openlocfilehash: fcd5eb5e8426eda537db9e099bf247bde29c195b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-sign-in-experience-with-azure-multi-factor-authentication"></a>Olá experiência de entrada com o Azure multi-Factor Authentication
> [!NOTE]
> Olá finalidade deste artigo é toowalk por meio de uma experiência de conexão típica. Para obter ajuda com entrar ou tootroubleshoot problemas, consulte [tendo problemas com o Azure multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).

## <a name="what-will-your-sign-in-experience-be"></a>Qual será sua experiência de conexão?
Sua experiência de entrada é diferente dependendo do que você escolhe toouse como o segundo fator: uma chamada telefônica, um aplicativo de autenticação ou textos. Escolha a opção de saudação que melhor descreve o que está fazendo:

| Como entrar no Azure? | 
| --- |
| [Com um telefone de chamada telefônica toomy móvel ou comercial](#signing-in-with-a-phone-call) |
| [Com um celular toomy do texto](#signing-in-with-a-text-message)
| [Com notificações do aplicativo do Microsoft Authenticator Olá](#signing-in-with-the-microsoft-authenticator-app-using-notification) |
| [Com códigos de verificação de aplicativo do Microsoft Authenticator Olá](#signing-in-with-the-microsoft-authenticator-app-using-verification-code) |
| [Com um método alternativo, porque não consigo usar meu método preferido agora](#signing-in-with-an-alternate-method) |

## <a name="signing-in-with-a-phone-call"></a>Conectando com uma chamada telefônica
Olá informações a seguir descreve a experiência de verificação em duas etapas Olá com chamada tooyour móveis ou telefone comercial.

1. Entrar no aplicativo de tooan ou serviço, como o Office 365 usando o nome de usuário e senha.  
2. A Microsoft liga para você.  
3. Atenda phone hello e pressione a tecla # de saudação.  

## <a name="signing-in-with-a-text-message"></a>Conectando com uma mensagem de texto
Olá informações a seguir descreve a experiência de verificação de duas etapas Olá com um telefone celular de tooyour de mensagem de texto:

1. Entrar no aplicativo de tooan ou serviço, como o Office 365 usando o nome de usuário e senha. 
2. A Microsoft envia para você uma mensagem de texto com um código numérico. 
3. Insira código Olá Olá caixa fornecida na página de entrada hello. 

## <a name="signing-in-with-hello-microsoft-authenticator-app"></a>Entrar com o aplicativo do Microsoft Authenticator Olá 
Olá informações a seguir descrevem a experiência de saudação do aplicativo do Microsoft Authenticator Olá para verificações de duas etapas. Há duas maneiras diferentes toouse Olá aplicativo. Você pode receber notificações por push em seu dispositivo ou você pode abrir Olá aplicativo tooget um código de verificação.

### <a name="toosign-in-with-a-notification-from-hello-microsoft-authenticator-app"></a>toosign com uma notificação de aplicativo do Microsoft Authenticator Olá
1. Entrar no aplicativo de tooan ou serviço, como o Office 365 usando o nome de usuário e senha.
2. A Microsoft envia um aplicativo de Microsoft Authenticator toohello notificação em seu dispositivo.

  ![A Microsoft envia notificação](./media/multi-factor-authentication-end-user-signin/notify.png)

3. Notificação de saudação aberta no seu telefone e selecione Olá **verificar** chave. Se sua empresa exigir um PIN, digite-o aqui.
4. Agora você deve estar conectado.

### <a name="toosign-in-using-a-verification-code-with-hello-microsoft-authenticator-app"></a>toosign usando um código de verificação com o aplicativo do Microsoft Authenticator Olá

Se você usar códigos de verificação Olá Microsoft Authenticator aplicativo tooget, em seguida, quando você abre o aplicativo hello você vir um número em seu nome de conta. Esse número é alterado a cada 30 segundos para que você não use Olá mesmo número duas vezes. Quando for solicitado um código de verificação, abra o aplicativo hello e usar qualquer número que está sendo exibido. 

1. Entrar no aplicativo de tooan ou serviço, como o Office 365 usando o nome de usuário e senha.
2. A Microsoft solicita que você insira um código de verificação.

  ![Inserir código de verificação](./media/multi-factor-authentication-end-user-signin/verify3.png)

3. Abra Olá Microsoft Authenticator aplicativo em seu telefone e insira o código de saudação na caixa Olá onde você está tentando entrar.

## <a name="signing-in-with-an-alternate-method"></a>Conectando-se com um método alternativo
Às vezes, você não tem o telefone hello ou dispositivo que você deseja configurar como seu método preferido de verificação. É por isso que recomendamos que faça o backup da conta. Olá seção a seguir mostra como toosign com um método alternativo para o método principal pode não estar disponível.

1. Entrar no aplicativo de tooan ou serviço, como o Office 365 usando o nome de usuário e senha.
2. Selecione **Usar uma opção de verificação diferente**. Você verá opções de verificação diferentes, de acordo com a quantidade configurada.
3. Escolha um método alternativo e conecte-se.

  ![Usar método alternativo](./media/multi-factor-authentication-end-user-signin/alt.png)

## <a name="next-steps"></a>Próximas etapas

Se você tiver problemas para entrar usando a verificação em duas etapas, consulte [Problemas com a Autenticação Multifator do Microsoft Azure](multi-factor-authentication-end-user-troubleshoot.md) para obter mais informações.

Saiba como muito[gerenciar as configurações de verificação em duas etapas](multi-factor-authentication-end-user-manage-settings.md).

Descubra como muito[Introdução ao aplicativo do Microsoft Authenticator Olá](microsoft-authenticator-app-how-to.md) para que você possa usar notificações toosign, em vez de chamadas telefônicas e de textos. 
