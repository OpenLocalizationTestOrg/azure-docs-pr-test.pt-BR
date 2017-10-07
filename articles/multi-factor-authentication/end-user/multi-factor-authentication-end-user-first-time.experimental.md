---
title: "aaaSet uma verificação de duas etapas para minha conta corporativa ou de estudante | Microsoft Docs"
description: "Quando sua empresa configura autenticação multifator do Azure, será solicitado toosign para verificação em duas etapas. Saiba como tooset-o. "
services: multi-factor-authentication
keywords: "como diretório de toouse do azure, active directory na nuvem hello, tutorial do active directory"
documentationcenter: 
author: kgremban
manager: femila
editor: pblachar
ms.assetid: 46f83a6a-dbdd-4375-8dc4-e7ea77c16357
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: 2d0348081eefa42c23de2047044688879dcb5966
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-my-account-for-two-step-verification"></a>Configurar minha conta para verificação em duas etapas
Verificação em duas etapas é uma etapa de segurança adicional que ajuda a proteger sua conta, dificultando toobreak outras pessoas no. Se você está lendo este artigo, é provável que tenha um email de seu administrador do trabalho ou escola sobre Autenticação Multifator. Ou talvez você tentou toosign no e recebeu uma mensagem solicitando que você tooset uma verificação de segurança adicional. Se esse for o caso de Olá, **você não pode entrar até concluir o processo de registro automático Olá**.

Este artigo ajuda você a configurar sua **conta corporativa ou de estudante**. Se você quiser tooenable verificacao para sua própria conta pessoal da Microsoft, consulte [sobre verificação em duas etapas](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification).

## <a name="set-up-your-account"></a>Configurar sua conta

Quando o departamento de TI exige que você toostart usando a verificação em duas etapas, dizer uma tela **seu administrador exigiu que você configure esta conta para verificação de segurança adicional** aparece:

![Configuração](./media/multi-factor-authentication-end-user-first-time/first.png)

tooget iniciado, selecione **configurá-lo agora.**

Se você não vir uma tela assim, quando você entrar, siga as instruções de saudação na [gerenciar as configurações de verificação em duas etapas](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page) toofind página de configurações de saudação onde você pode gerenciar suas opções de verificação. 

## <a name="decide-how-you-want-tooverify-your-sign-ins"></a>Decida como deseja tooverify suas entradas

Olá primeira pergunta no processo de registro de saudação é como você deseja nos toocontact você. Examine as opções de saudação na tabela de saudação e use etapas de instalação do hello links toogo toohello para cada método.

| Método de contato | Descrição |
| --- | --- |
| [Aplicativo móvel](#use-a-mobile-app-as-the-contact-method) |- **Receba notificações para verificação.** Essa opção envia um aplicativo do autenticador toohello notificação no seu smartphone ou tablet. Exibir notificação hello e, se for legítima, selecionar **autenticar** no aplicativo hello. Seu trabalho ou escola pode exigir que você insira um PIN antes de se autenticar.<br>- **Use o código de verificação.** Nesse modo, o aplicativo do autenticador de hello gera um código de verificação de atualizações a cada 30 segundos. Insira o código de verificação mais recente da saudação na interface de entrada hello.<br>Olá Microsoft Authenticator aplicativo está disponível para [do Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), e [IOS](http://go.microsoft.com/fwlink/?Linkid=825073). |
| [Chamada telefônica ou SMS de celular](#use-your-mobile-phone-as-the-contact-method) |- **Chamada telefônica** coloca um número de telefone voz automática chamada toohello você fornecer. Responder a chamada hello e pressione # em tooauthenticate de teclado do telefone hello.<br>- **SMS** envia para o usuário uma mensagem de texto contendo um código de verificação. Após Olá prompt no texto de saudação, responder a mensagem de texto toohello ou inserir código de verificação de saudação fornecido Olá logon na interface. |
| [Ligação Para Telefone Comercial](#use-your-office-phone-as-the-contact-method) |Coloca um número de telefone voz automática chamada toohello que você fornecer. Saudação de resposta chamada e pressiona # no tooauthenticate de teclado do telefone hello. |

## <a name="use-a-mobile-app-as-hello-contact-method"></a>Usar um aplicativo móvel como método de contato Olá
Usar esse método requer que você instale um aplicativo autenticador em seu telefone ou tablet. Olá etapas neste artigo se baseiam no aplicativo do Microsoft Authenticator hello, que está disponível para [do Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), e [IOS](http://go.microsoft.com/fwlink/?Linkid=825073).

1. Selecione **aplicativo móvel** da lista suspensa de saudação.
2. Selecione **Receber notificações para verificação** ou **Usar código de verificação**, então selecione **Configurar**.

   ![Tela de verificação de segurança adicional](./media/multi-factor-authentication-end-user-first-time/mobileapp.png)

3. No seu telefone ou tablet, abra o aplicativo hello e selecione  **+**  tooadd uma conta. (Em dispositivos Android, selecione Olá três pontos, em seguida, **adicionar conta**.)
4. Especifique que você deseja tooadd uma conta corporativa ou escolar. scanner de código QR Olá em seu telefone será aberta. Se a câmera não está funcionando corretamente, você pode selecionar tooenter informações da sua empresa manualmente. Para obter mais informações, consulte [Adicionar uma conta manualmente](#add-an-account-manually).  
5. Digitalize Olá QR código imagem exibida com tela hello para configurar o aplicativo móvel hello.  Selecione **feito** tela de código QR de saudação tooclose.  

   ![Tela do código QR](./media/multi-factor-authentication-end-user-first-time/scan2.png)

6. Quando termina de ativação no telefone hello, selecione **contato me**.  Esta etapa envia uma notificação ou um telefone de tooyour do código de verificação. Selecione **Verificar**.  
7. Se sua empresa exigir um PIN para aprovar a verificação de entrada, digite-o.

   ![Caixa para inserir um PIN](./media/multi-factor-authentication-end-user-first-time/scan3.png)

8. Após digitar o PIN, selecione **Fechar**. Nesse ponto, sua verificação deve ter sido bem-sucedida.
9. É recomendável que você insira seu número de telefone celular em caso de perda de aplicativo móvel do acesso tooyour. Especifique seu país na lista suspensa de saudação e insira o número de telefone celular no hello caixa próxima toohello nome do país. Selecione **Avançar**.
10. Neste ponto, você está tooset solicitada as senhas de aplicativo para aplicativos sem navegador, como o Outlook 2010 ou anterior ou aplicativo de email nativo Olá em dispositivos da Apple. Esta ação ocorre porque alguns aplicativos não dão suporte à verificação em duas etapas. Se você não usar esses aplicativos, clique em **feito** e ignore Olá restante dessas etapas.
11. Se você estiver usando esses aplicativos, copiar senha de aplicativo hello fornecido e cole-o em seu aplicativo em vez de sua senha regular. Você pode usar o hello mesma senha de aplicativo para vários aplicativos. Para obter mais informações, [ajuda com senhas de aplicativo].
12. Clique em **Concluído**.

### <a name="add-an-account-manually"></a>Adicionar uma conta manualmente
Se você quiser tooadd um aplicativo móvel de toohello conta manualmente, em vez de usar o leitor de saudação QR, siga estas etapas.

1. Selecione Olá **insira a conta manualmente** botão.  
2. Insira código hello e a URL de Olá fornecidos em Olá na mesma página que mostra Olá código de barras. Essas informações vai Olá **código** e **URL** caixas no aplicativo móvel hello.

    ![Configuração](./media/multi-factor-authentication-end-user-first-time/barcode2.png)
3. Quando termina a ativação hello, selecione **contato me**. Esta etapa envia uma notificação ou um telefone de tooyour do código de verificação. Selecione **Verificar**.

## <a name="use-your-mobile-phone-as-hello-contact-method"></a>Usar o telefone celular como método de contato Olá
1. Selecione **telefone de autenticação** da lista suspensa de saudação.  

    ![Configuração](./media/multi-factor-authentication-end-user-first-time/phone.png)  
2. Escolha seu país na lista suspensa de saudação e insira seu número de telefone celular.
3. Selecione método hello preferir toouse com seu celular - texto ou chamada.
4. Selecione **contato me** tooverify seu número de telefone. Dependendo do modo de saudação selecionado, podemos enviar um texto ou ligar para você. Siga as instruções de saudação fornecidas na tela hello, em seguida, selecione **verificar**.
5. Neste ponto, você está tooset solicitada as senhas de aplicativo para aplicativos sem navegador, como o Outlook 2010 ou anterior ou aplicativo de email nativo Olá em dispositivos da Apple. Esta ação ocorre porque alguns aplicativos não dão suporte à verificação em duas etapas. Se você não usar esses aplicativos, clique em **feito** e ignore Olá restante das etapas de saudação.
6. Se você estiver usando esses aplicativos, copiar senha de aplicativo hello fornecido e cole-o em seu aplicativo em vez de sua senha regular. Você pode usar o hello mesma senha de aplicativo para vários aplicativos. Para obter mais informações, [ajuda com senhas de aplicativo].
7. Clique em **Concluído**.

## <a name="use-your-office-phone-as-hello-contact-method"></a>Usar o telefone comercial como método de contato Olá
1. Selecione **telefone comercial** Olá suspenso  

    ![Configuração](./media/multi-factor-authentication-end-user-first-time/office.png)  
2. caixa de número de telefone de saudação é preenchida automaticamente com as informações de contato da empresa. Se o número de saudação está incorreto ou ausente, peça ao seu administrador toomake alterações.
3. Selecione **contato me** tooverify seu número de telefone e nós chamará seu número. Siga as instruções de saudação fornecidas na tela hello, em seguida, selecione **verificar**.
4. Neste ponto, você está tooset solicitada as senhas de aplicativo para aplicativos sem navegador, como o Outlook 2010 ou anterior ou aplicativo de email nativo Olá em dispositivos da Apple. Esta ação ocorre porque alguns aplicativos não dão suporte à verificação em duas etapas. Se você não usar esses aplicativos, clique em **feito** e ignore Olá restante das etapas de saudação.
5. Se você estiver usando esses aplicativos, copiar senha de aplicativo hello fornecido e cole-o em seu aplicativo em vez de sua senha regular. Você pode usar o hello mesma senha de aplicativo para vários aplicativos. Para obter mais informações, consulte [O que são senhas de aplicativo](multi-factor-authentication-end-user-app-passwords.md).
6. Clique em **Concluído**.

## <a name="next-steps"></a>Próximas etapas
* Altere suas opções preferenciais e [gerencie suas configurações de verificação em duas etapas](multi-factor-authentication-end-user-manage-settings.md)
* Configure [senhas de aplicativo](multi-factor-authentication-end-user-app-passwords.md) para aplicativos de dispositivo nativo que não dão suporte à verificação em duas etapas.
* Check-out Olá [aplicativo Microsoft Authenticator](microsoft-authenticator-app-how-to.md) para fast, autenticação de segurança mesmo quando você não tem serviços de célula.

