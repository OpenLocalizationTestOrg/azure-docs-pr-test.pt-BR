---
title: "instruções aaaSign-in para hello Azure Toolkit for IntelliJ | Microsoft Docs"
description: Saiba como toosign em tooMicrosoft do Azure usando hello o Kit de ferramentas do Azure para IntelliJ.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 2de781fc19267cce133b1e6456481497e165fce4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-instructions-for-hello-azure-toolkit-for-intellij"></a>Instruções entrar para hello Azure Toolkit for IntelliJ

Olá Kit de ferramentas do Azure para IntelliJ fornece dois métodos para entrar no tooyour conta do Azure:

  * **Interativo**: Insira suas credenciais do Azure cada vez que você entrar no tooyour conta do Azure.
  * **Automatizada**: criar um arquivo de credenciais que você pode usar o logon de tooautomatically em tooyour conta do Azure.

Olá seções a seguir descrevem como toouse cada método.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-tooyour-azure-account-interactively"></a>Entrar tooyour conta do Azure de modo interativo

toosign em tooAzure inserindo manualmente suas credenciais do Azure, Olá a seguir:

1. Abra seu projeto com o IntelliJ IDEA.

2. Clique em **ferramentas**, ponto muito**Azure**e, em seguida, clique em **Azure entrar**.

   ![Olá IntelliJ Azure entrar no comando][I01]

3. Em Olá **Azure entrar** janela, selecione **interativo**e, em seguida, clique em **entrar**.

   ![Hello Azure entrada na janela com interativo selecionado][I02]

4. Em Olá **Log no Azure** caixa de diálogo for exibida, insira suas credenciais do Azure e, em seguida, clique em **entrar**.

   ![janela de diálogo de logon do Azure Olá][I03]

5. Em Olá **selecione assinaturas** caixa de diálogo, assinaturas de saudação selecione que você deseja toouse e, em seguida, clique em **Okey**.

   ![caixa de diálogo Selecionar assinaturas Olá][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a>Sair de sua conta do Azure depois de entrar interativamente

Depois que você configurou sua conta usando Olá etapas anteriores, você será conectado automaticamente fora da sua conta do Azure cada vez que você reiniciar IntelliJ IDEIA. No entanto, se você quiser toosign fora da sua conta do Azure *sem* reiniciar IntelliJ IDEIA, Olá a seguir.

1. Em IntelliJ IDEIA, em hello **ferramentas** menus, aponte muito**Azure**e, em seguida, clique em **Azure sair**.

   ![Olá comando IntelliJ Azure sair][L01]

2. Em Olá **Azure sair** janela de confirmação, clique em **Sim**.

   ![janela de Hello Azure sair confirmação][L02]

## <a name="sign-in-tooyour-azure-account-automatically"></a>Conectar automaticamente tooyour conta do Azure

Esta seção fornece uma orientarão pela criação de um arquivo de credenciais contendo os dados de sua entidade de serviço. Depois de concluir esse processo, tooautomatically Eclipse usa Olá credenciais arquivo de entrada que no tooAzure cada vez que você abra seu projeto.

1. Abra seu projeto com o IntelliJ IDEA.

2. Em Olá **ferramentas** menu ponto muito**Azure**e, em seguida, clique em **Azure entrar**.

   ![Olá IntelliJ Azure entrar no comando][A01]

3. Em Olá **Azure entrar** janela, selecione **automatizada**e, em seguida, clique em **novo**.

   ![Hello Azure entrada na janela com automatizado selecionada][A02]

4. Em Olá **caixa de diálogo de logon do Azure** janela, insira suas credenciais do Azure e, em seguida, clique em **entrar**.

   ![janela de diálogo de logon do Azure Olá][A03]

5. Em Olá **criar arquivos de autenticação** janela, assinaturas de saudação selecione deseja toouse, escolha o diretório de destino e, em seguida, clique em **iniciar**.

   ![janela de criar arquivos de autenticação Olá][A04]

6. Em Olá **Status de criação da entidade de serviço** caixa de diálogo, depois que os arquivos foram criados com êxito, clique em **Okey**.

   ![Olá caixa de diálogo Status de criação da entidade de serviço][A05]

7. Em Olá **Azure entrar** janela, clique em **entrar**.

   ![Caixa de Diálogo de Logon do Azure][A06]

8. Em Olá **selecione assinaturas** caixa de diálogo, assinaturas de saudação selecione que você deseja toouse e, em seguida, clique em **Okey**.

   ![caixa de diálogo Selecionar assinaturas Olá][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a>Sair de sua conta do Azure depois de entrar automaticamente

Depois que você configurou sua conta usando Olá etapas anteriores, Olá Kit de ferramentas do Azure automaticamente faz com que você no tooyour cada vez que você reiniciar IntelliJ IDEIA de conta do Azure. No entanto, toosign fora da sua conta do Azure e evitar Olá Kit de ferramentas do Azure de conectá-lo automaticamente, Olá a seguir:

1. Em IntelliJ IDEIA, em hello **ferramentas** menus, aponte muito**Azure**e, em seguida, clique em **Azure sair**.

   ![Olá comando IntelliJ Azure sair][L01]

2. Em Olá **Azure sair** janela de confirmação, clique em **Sim**.

   ![janela de Hello Azure sair confirmação][L03]

## <a name="sign-in-tooyour-azure-account-automatically-by-using-an-existing-credentials-file"></a>Entre no tooyour conta do Azure automaticamente usando um arquivo existente de credenciais

Se você assinar fora da sua conta do Azure, quando você estiver usando IntelliJ IDEIA, você deve usar um sinal de tooautomatically de arquivo de credenciais existentes em toohello conta. Olá tooconfigure Kit de ferramentas do Azure para Eclipse toouse um arquivo existente de credenciais, Olá a seguir:

1. Abra seu projeto com o IntelliJ IDEA.

2. Em Olá **ferramentas** menu ponto muito**Azure**e, em seguida, clique em **Azure entrar**.

   ![Olá IntelliJ Azure entrar no comando][A01]

3. Em Olá **Azure entrar** janela, selecione **automatizada**e, em seguida, clique em **procurar**.

   ![Hello Azure entrada na janela com automatizado selecionada][A02]

4. Em Olá **Selecionar arquivo de autenticação** caixa de diálogo, selecione um arquivo de credenciais criado anteriormente e, em seguida, clique em **selecione**.

   ![caixa de diálogo Selecionar arquivo de autenticação Olá][A08]

5. Em Olá **Azure entrar** janela, clique em **entrar**.

   ![Hello Azure entrada na janela com automatizado selecionada][A06]

6. Em Olá **selecione assinaturas** caixa de diálogo, assinaturas de saudação selecione que você deseja toouse e, em seguida, clique em **Okey**.

   ![caixa de diálogo Selecionar assinaturas Olá][A07]

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre Olá kits de ferramentas do Azure para Java IDEs, consulte Olá links a seguir:

* [Kit de ferramentas do Azure para Eclipse]
  * [O que há de novo no hello Kit de ferramentas do Azure para Eclipse]
  * [Saudação de instalar o Kit de ferramentas do Azure para Eclipse]
  * [Instruções de entrada para Olá Kit de ferramentas do Azure para Eclipse]
  * [Criar um aplicativo Web Olá, Mundo para o Azure no Eclipse]
* [Kit de Ferramentas do Azure para IntelliJ]
  * [O que há de novo no hello Azure Toolkit for IntelliJ]
  * [Saudação de instalar o Kit de ferramentas do Azure para IntelliJ]
  * *Instruções entrar para hello Azure Toolkit for IntelliJ* (Este artigo)
  * [Criar um aplicativo Web Olá, Mundo para o Azure no IntelliJ]

Para obter mais informações sobre como usar o Azure com Java, consulte Olá [Centro de desenvolvedores de Java do Azure] e hello [ferramentas Java para o Visual Studio Team Services].

<!-- URL List -->

[Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse.md
[Kit de Ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij.md
[Criar um aplicativo Web Hello World para o Azure no Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Criar um aplicativo Web Olá, Mundo para o Azure no IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Saudação de instalar o Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Saudação de instalar o Kit de ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Instruções de entrada para Olá Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Sign-in instructions for hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[O que há de novo no hello Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[O que há de novo no hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Centro de desenvolvedores de Java do Azure]: https://azure.microsoft.com/develop/java/
[ferramentas Java para o Visual Studio Team Services]: https://java.visualstudio.com/

<!-- IMG List -->

[I01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I01.png
[I02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I02.png
[I03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I03.png
[I04]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I04.png

[A01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A01.png
[A02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A02.png
[A03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A03.png
[A04]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A04.png
[A05]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A05.png
[A06]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A06.png
[A07]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A07.png
[A08]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A08.png

[L01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L01.png
[L02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L02.png
[L03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L03.png
