---
title: aaaMicrosoft autenticador phone entrar - contas do Azure e Microsoft | Microsoft Docs
description: Use seu telefone toosign tooyour conta da Microsoft em vez de digitar sua senha. Este artigo responde a Perguntas Frequentes sobre esse recurso.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/12/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: end-user
ms.openlocfilehash: a4911ff580b3ffa078299ad706d099330b75a2e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-with-your-phone-not-your-password"></a>Entre com seu telefone, não com sua senha

Olá Microsoft Authenticator aplicativo ajuda a proteger suas contas, executando a verificação em duas etapas depois de inserir sua senha. Mas você sabia que ele pode substituir totalmente senha Olá para sua conta pessoal da Microsoft? 

Esse recurso está disponível em dispositivos iOS e Android e funciona com contas pessoais da Microsoft. 

## <a name="how-it-works"></a>Como ele funciona

Muitos de vocês usam Olá Authenticator Microsoft app para verificação em duas etapas quando você entrar no tooyour conta da Microsoft. Digite sua senha, então vá toohello aplicativo tooeither aprovar uma notificação ou obter um código de verificação. Com a entrada no telefone, você ignorar senha hello e faça a verificação de identidade em seu telefone. Porque a entrada do telefone é um tipo de verificação em duas etapas, você ainda precisa tooprovide algo que você sabe e algo que você tem tooverify sua identidade. telefone Olá ainda é passo hello e PIN ou a chave biométrico seu telefone é Olá que você sabe. 

## <a name="how-tooget-started"></a>A inicialização de tooget

toosign em tooyour conta pessoal da Microsoft com seu telefone, siga estas etapas: 

1. Habilitar entrada pelo telefone para sua conta. 

  - Se você não terá um aplicativo do Microsoft Authenticator Olá ainda, instalar e adicionar sua conta pessoal da Microsoft de acordo com as etapas de toohello em hello [página Microsoft Authenticator](microsoft-authenticator-app-how-to.md). Contas recém-adicionado são habilitadas automaticamente, então você está toogo BOM.

  - Se você já usa o Microsoft Authenticator para verificação em duas etapas, selecione a conta na home page do aplicativo de saudação e selecione **habilitar phone entrada** do menu suspenso de saudação.

  >[!NOTE] 
  >tooprotect sua conta, é necessário um PIN ou a biométrico bloqueio em seu dispositivo. Se você mantiver o seu telefone desbloqueado, o aplicativo hello surge uma solicitação para que você tooset o bloqueio de um antes de habilitar a entrada do telefone. 

3. A maioria das páginas em que você normalmente digitaria sua senha de conta da Microsoft tem um link que diz **Usar um aplicativo**. Selecione este toosign de link com o seu telefone. 

4. A Microsoft envia um telefone de tooyour de notificação. Aprove Olá notificação toosign tooyour conta.   

## <a name="faq"></a>Perguntas frequentes 

### <a name="how-is-signing-in-with-my-phone-more-secure-than-typing-a-password"></a>Como a entrada com meu telefone é mais segura do que digitar uma senha?  

Hoje, a maioria das pessoas entrar tooweb sites ou aplicativos que usam um nome de usuário e senha.  Infelizmente, as senhas são geralmente perdidas, roubadas ou adivinhadas por hackers. Quando você configura Olá Microsoft Authenticator aplicativo toosign no, podemos gerar uma chave no telefone que pode desbloquear sua conta. Protegemos essa chave com hello PIN ou a biométrica que você já usa no seu telefone.  Quando você entrar com seu telefone, essa chave é usada tooprove sua identidade com segurança com dois fatores – hello telefone em si e sua capacidade toounlock-lo. 

chave Olá usada é semelhante toohello as chaves usadas no Windows Hello e especificações de FIDO Alliance UAF hello. Sua biografia dados só são usado como tooprotect Olá chave localmente e é nunca enviada para ou armazenada na nuvem hello. 
 
### <a name="where-can-i-use-my-phone-tooreplace-my-password-and-where-would-i-still-need-hello-password"></a>Onde posso usar meu telefone tooreplace minha senha, e em que eu ainda precisaria senha Olá?  

Hoje, Olá phone entrar recurso só funciona com aplicativos web e serviços que são ativados pelas contas da Microsoft pessoais, iOS ou Android aplicativos que usam uma conta pessoal da Microsoft e aplicativos no Windows 10 que usam uma conta pessoal da Microsoft. Quando você entrar no tooone desses sites da web ou aplicativos, na página de saudação em que você digite sua senha normalmente há um link que diz **usar um aplicativo**. 

Entrada do telefone não pode ser usado toounlock um computador Windows, XBOX ou todas as versões da área de trabalho de aplicativos da Microsoft, como aplicativos do Office no momento. 
 
### <a name="does-this-replace-two-step-verification-should-i-turn-it-off"></a>Isso substitui a verificação em duas etapas? Devo desativá-la?   

Às vezes. Estamos trabalhando para expandir o escopo de saudação do telefone entrar, mas por enquanto ainda há locais no ecossistema do Microsoft hello que não dão suporte a ele. Nesses locais, ainda estamos usando a verificação em duas etapas para entrada segura. Por esse motivo, não, você não deve desativar a verificação em duas etapas para a sua conta. 
 
### <a name="okay-if-i-keep-two-step-verification-turned-on-for-my-account-do-i-have-tooapprove-two-notifications"></a>Okey, se mantiver o verificação em duas etapas para minha conta, é necessário tooapprove duas notificações?

Não, não será necessário. Entrar tooyour conta da Microsoft com seu telefone será considerada verificação em duas etapas. Em vez de digitar sua senha, em seguida, aprovando uma notificação provar sua identidade sabendo como toounlock seu telefone e, em seguida, aprovar uma notificação. Não enviaremos um segundo tooapprove de notificação.

### <a name="what-if-i-lose-my-phone-or-dont-have-it-with-me-how-can-i-access-my-account"></a>E se eu perder meu telefone ou não o tiver comigo, como posso acessar minha conta?  

Você sempre pode clicar em **usar uma senha de** em tooswitch de página de entrada hello faça toousing sua senha. Tenha em mente que se você usar a verificação em duas etapas, ainda precisará de um segundo tooverify de método sua entrada. É por isso que recomendamos que você toomake se você tem informações de segurança extra e atualizadas em sua conta. Você pode gerenciar suas informações de segurança em https://account.live.com/proofs/manage. 
 
### <a name="how-do-i-stop-using-this-feature-and-go-back-tooentering-my-password"></a>Como parar de usar esse recurso e voltar tooentering minha senha?

Clique em **Usar uma senha** quando você entrar. Nós Lembre-se de sua escolha mais recente e oferecer que por saudação padrão próxima vez que entrar. Se você quiser toosigning back toogo com seu telefone, clique em **usar um aplicativo**. 
 
### <a name="can-i-use-hello-app-toosign-in-tooall-my-accounts-with-microsoft"></a>Posso usar o hello aplicativo toosign em tooall minhas contas com a Microsoft?   
No momento, essa funcionalidade só está disponível para contas pessoais da Microsoft. 
 
### <a name="can-i-sign-into-my-pc-with-my-phone"></a>Posso entrar no meu computador com o meu telefone?  
Para o seu computador, é recomendável entrar com o Windows Hello no Windows 10 usando o rosto, impressão digital ou um PIN.   
 
### <a name="can-i-sign-in-with-my-windows-phone"></a>Posso entrar com meu Windows Phone?  
Neste momento, não estamos desenvolvendo essa funcionalidade para Olá Microsoft Authenticator no Windows Phone. 

## <a name="next-steps"></a>Próximas etapas
Se você não tiver baixado o aplicativo do Microsoft Authenticator hello, check-out. aplicativo Hello está disponível para [do Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), e entrar no telefone está disponível no aplicativo do Microsoft Authenticator Olá para [Android](http://go.microsoft.com/fwlink/?Linkid=825072) e [IOS](http://go.microsoft.com/fwlink/?Linkid=825073).

Se você tiver dúvidas sobre o aplicativo hello em geral, dê uma olhada Olá [perguntas frequentes do Microsoft autenticador](microsoft-authenticator-app-faq.md)
