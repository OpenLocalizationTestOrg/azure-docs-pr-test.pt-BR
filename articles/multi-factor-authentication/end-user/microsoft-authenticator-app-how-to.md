---
title: aplicativo do autenticador aaaMicrosoft para telefones celulares | Microsoft Docs
description: "Saiba como tooupgrade toohello última versão do autenticador do Azure."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3065a1ee-f253-41f0-a68d-2bd84af5ffba
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: H1Hack27Feb2017, end-user
ms.openlocfilehash: d895d92d89613cbafd9fc09d4ff4810cbf25652e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-microsoft-authenticator-app"></a>Introdução ao aplicativo do Microsoft Authenticator Olá
aplicativo Microsoft Authenticator Hello fornece um nível adicional de segurança em sua conta corporativa ou escolar (por exemplo, bsimon@contoso.com) ou sua conta da Microsoft (por exemplo, bsimon@outlook.com).

aplicativo Hello funciona em uma das seguintes maneiras:

* **Notificação**. aplicativo Hello pode ajudar a evitar acesso não autorizado tooaccounts e interromper transações fraudulentas enviando uma notificação tooyour smartphone ou tablet. Simplesmente exibir notificação hello e, se for legítima, selecione **verificar**. Caso contrário, você pode selecionar **Negar**. 
* **Código de verificação**. saudação de aplicativo pode ser usado como um software token toogenerate um código de verificação de OAuth. Depois de inserir seu nome de usuário e senha, você inserir código Olá fornecido pelo aplicativo hello na tela de entrada hello. código de verificação de saudação oferece uma segunda forma de autenticação.

Olá Microsoft Authenticator aplicativo substitui o aplicativo do Azure Authenticator hello. aplicativo do Azure Authenticator Olá ainda funciona, mas se você decidir toomove toohello novo aplicativo Microsoft Authenticator, este artigo pode ajudá-lo.  

## <a name="opt-in-for-two-step-verification"></a>Aceitar a verificação em duas etapas

aplicativo do Microsoft Authenticator Olá não funciona por si só. Configure cada um dos seu tooprompt contas por um segundo método de verificação depois de você entra com seu nome de usuário e senha. 

Para uma conta corporativa ou de estudante, você não geralmente obtém toochoose esse recurso por conta própria. Em vez disso, um administrador de segurança aceita em seu nome e o notifica tooregister métodos de verificação para sua conta. Se esta situação se aplica a tooyou, saiba mais em [o Azure multi-Factor Authentication significa para mim](multi-factor-authentication-end-user.md).

Para uma conta pessoal, você precisa tooset uma verificação de duas etapas para si mesmo. Se você tem uma conta da Microsoft, essas etapas estão disponíveis em [Sobre a verificação em duas etapas](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification). 

Você também pode usar o hello Microsoft Authenticator com contas não Microsoft. Eles podem chamar o recurso de saudação algo diferente de verificação em duas etapas, mas você deve ser capaz de toofind-o em configurações de segurança ou de entrada. 

## <a name="install-hello-app"></a>Instalar o aplicativo hello
Olá Microsoft Authenticator aplicativo está disponível para [do Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), e [iOS](http://go.microsoft.com/fwlink/?Linkid=825073).

## <a name="add-accounts-toohello-app"></a>Adicionar contas toohello aplicativo
Para cada conta que você deseja que o aplicativo do tooadd toohello Microsoft Authenticator, use um dos Olá procedimentos a seguir:

### <a name="add-a-personal-microsoft-account-toohello-app"></a>Adicionar um aplicativo toohello da conta da Microsoft pessoal

Para uma conta pessoal da Microsoft (um que você use toosign em tooOutlook.com, Xbox, Skype, etc.), toodo se entrar na conta de tooyour no aplicativo do Microsoft Authenticator hello.

### <a name="add-a-work-or-school-account-toohello-app-using-hello-qr-code-scanner"></a>Adicionar um trabalho ou escolar conta toohello aplicativo usando o scanner de código QR de saudação
1. Vá toohello tela de configurações de verificação de segurança.  Para obter informações sobre como tooget toothis tela, consulte [alterar suas configurações de segurança](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page).
2. Caixa de seleção Olá Avançar muito**aplicativo autenticador** , em seguida, selecione **configurar**.

    ![botão de configurar Olá na tela de configurações de verificação de segurança Olá](./media/authenticator-app-how-to/azureauthe.png)

    Isso abre uma tela com um código QR.

    ![Tela que fornece o código QR de saudação](./media/authenticator-app-how-to/barcode2.png)
3. Aplicativo do Microsoft Authenticator Olá aberto. Em Olá **contas** tela, selecione  **+** e, em seguida, especifique que você deseja tooadd uma conta corporativa ou escolar.
4. Use Olá câmera tooscan Olá QR código e, em seguida, selecione **feito** tela de código QR de saudação tooclose.

    Se a câmera não está funcionando corretamente, você pode [inserir código Olá QR e a URL manualmente](#add-an-account-to-the-app-manually).

5. Quando o aplicativo hello mostra o nome da conta com um código de seis dígitos abaixo dela, terminar. 

    ![Tela de contas](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-toohello-app-manually"></a>Adicionar um aplicativo de toohello conta manualmente
1. Vá toohello tela de configurações de verificação de segurança.  Para obter informações sobre como tooget toothis tela, consulte [alterar suas configurações de segurança](multi-factor-authentication-end-user-manage-settings.md).
2. Selecione **Configurar**.

    ![botão de configurar Olá na tela de configurações de verificação de segurança Olá](./media/authenticator-app-how-to/azureauthe.png)

    Isso abre uma tela com um código QR.  Observe o código de saudação e a URL.

    ![Tela que fornece o código QR de saudação e a URL](./media/authenticator-app-how-to/barcode2.png)
3. Aplicativo do Microsoft Authenticator Olá aberto. Em Olá **contas** tela, selecione  **+** e, em seguida, especifique que você deseja tooadd uma conta corporativa ou escolar.

4. No scanner hello, selecione **inserir código manualmente**.

    ![Tela para verificar um código QR](./media/multi-factor-authentication-end-user-first-time/scan2.png)
5. Insira o código de saudação e URL Olá nas caixas de saudação apropriadas no aplicativo hello, selecione **concluir**.

    ![Tela para inserir código e a URL](./media/authenticator-app-how-to/manual.png)

6. Quando o aplicativo hello mostra o nome da conta com um código de seis dígitos abaixo dela, terminar.

    ![Tela de contas](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-toohello-app-using-touch-id"></a>Adicionar um aplicativo de toohello de conta usando a ID de toque
aplicativo do Microsoft Authenticator Olá no iOS dá suporte à ID de toque.  Autenticação multifator do Azure permite que as organizações toorequire um PIN para dispositivos. Com a ID de toque, usuários do iOS não precisam tooenter um PIN. Em vez disso, eles podem digitalizar sua impressão digital e selecionar **Aprovar**.

A configuração do Touch ID com o Microsoft Authenticator é simples. Você conclui um desafio de verificação normal com um PIN. Se seu dispositivo der suporte ao o Touch ID, o Microsoft Authenticator irá configurá-lo automaticamente para essa conta.

![Verificação da configuração do Touch ID](./media/authenticator-app-how-to/touchid1.png)

Partir desse ponto, quando você estiver necessário tooverify a entrar, selecione Olá recebida notificação de push e verificar sua impressão digital em vez de digitar seu PIN.

![Notificação por push](./media/authenticator-app-how-to/touchid2.png)

## <a name="use-hello-app-when-you-sign-in"></a>Usar o aplicativo hello quando você entrar no

Depois que sua conta é adicionada toohello aplicativo, pode ser solicitado toodo um toomake de verificação de teste se que tudo foi configurado corretamente. Depois disso, você terminou! Você não precisa toodo nada até hello próxima vez que entrar.

Se você escolher toouse códigos de verificação no aplicativo hello, iniciar toosee-los na home page do hello. Eles são alterados a cada 30 segundos para que você sempre tenha um novo código quando precisar de um. Mas você não precisa toodo nada com eles até que você entrar e tooenter solicitado um código de verificação.  
