---
title: aaaHow toouse senhas de aplicativo no Azure MFA? | Microsoft Docs
description: "Esta página ajuda os usuários a entender quais são as senhas de aplicativo e o que são usados para com relação tooAzure MFA."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 345b757b-5a2b-48eb-953f-d363313be9e5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: bf2c11edc0ca81f2950eff0f7a3a24c8a5b34623
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-app-passwords-in-azure-multi-factor-authentication"></a>O que são as senhas de aplicativo no Azure Multi-Factor Authentication?
Determinados aplicativos sem navegador, como o cliente de email nativo do hello Apple que usa o Exchange Active Sync, atualmente não dão suporte a autenticação multifator. O Multi-Factor Authentication é habilitado por usuário. Isso significa que se um usuário tiver sido habilitado para autenticação multifator e eles estão tentando toouse não são navegadores, eles serão toodo não é possível então. Uma senha de aplicativo permite que este toooccur.

Quando tiver uma senha de aplicativo, você poderá usá-la no lugar da senha original com esses aplicativos que não usam navegador. Isso ocorre porque quando você registrar para verificação em duas etapas, você está dizendo Microsoft não toolet qualquer pessoa entrar com sua senha se elas também não é possível executar a verificação segundo hello. cliente de email nativo Olá Apple em seu telefone não pode entrar como você porque ele não é possível solicitar a verificação em duas etapas. Olá, a solução para isso é toocreate uma senha mais segura do aplicativo que você não use diárias, mas apenas para os aplicativos que não oferece suporte a verificação em duas etapas. Use senha de aplicativo hello para que os aplicativos podem ignorar a autenticação multifator e continuar toowork.

> [!NOTE]
> Os clientes do Office 2013 (incluindo Outlook) são compatíveis com novos protocolos de autenticação e podem ser usados com a verificação em duas etapas.  Isso significa que, uma vez habilitadas, as senhas de aplicativo não são necessárias para usar com os clientes do Office 2013.  Para saber mais, veja [Anúncio da visualização pública da autenticação moderna do Office 2013](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).


## <a name="how-toouse-app-passwords"></a>Como as senhas de aplicativo toouse
Olá, estes são alguns tooremember coisas sobre como as senhas de aplicativo toouse.

* Você não cria suas próprias senhas de aplicativo. Em vez disso, elas são geradas automaticamente. Como você só tiver a senha de aplicativo hello tooenter uma vez por aplicativo, é mais seguro toouse uma senha mais complexa, gerada automaticamente em vez de fazer um que você possa se lembrar.
* Atualmente, há um limite de 40 senhas por usuário. Se você tentar toocreate um depois que você atingiu o limite de hello, será solicitada toodelete uma das senhas de aplicativo existente antes de criar um novo.
* Você deve usar uma senha de aplicativo por dispositivo, não por aplicativo. Por exemplo, você pode criar uma senha de aplicativo para seu laptop e usá-la para todos os aplicativos nesse laptop. Em seguida, crie uma segunda toouse de senha de aplicativo para todos os seus aplicativos em sua área de trabalho. 
* Você terá uma saudação de senha de aplicativo primeira vez que você se registrar para verificação em duas etapas.  Se precisar de mais, é possível criá-las.



## <a name="creating-and-deleting-app-passwords"></a>Criação e exclusão de senhas de aplicativo
Durante a conexão inicial, você recebe uma senha de aplicativo que pode usar.  Além disso, você também pode criar e excluir senhas de aplicativo posteriormente.  Como fazer isso depende de como você usa a autenticação multifator. Saudação de resposta a seguir perguntas toodetermine onde você deve ficar toomanage senhas de aplicativo: 

1. Você usa a verificação em duas etapas em sua conta pessoal da Microsoft? Se Sim, consulte toohello [senhas de aplicativo e verificação em duas etapas](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) artigo para obter ajuda. Se não, continue tooquestion dois.

2. Certo, você usa a verificação de duas etapas em sua conta corporativa ou de estudante. Você usa ele toosign em tooOffice 365 aplicativos? Se Sim, você deve referir-se muito[criar uma senha de aplicativo para o Office 365](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183) para obter ajuda. Se não, continue tooquestion três. 

3. Você usa a verificação em duas etapas com o Microsoft Azure? Se Sim, continuar toohello [gerenciar senhas de aplicativo no portal do Azure de saudação](#manage-app-passwords-in-the-Azure-portal) deste artigo. Se não, continue tooquestion quatro.

4. Você não sabe onde utiliza a verificação em duas etapas? Continuar toohello [gerenciar senhas de aplicativo com o portal de MyApps Olá](#manage-app-passwords-with-the-myapps-portal) deste artigo. 


## <a name="manage-app-passwords-in-hello-azure-portal"></a>Gerenciar senhas de aplicativo no portal do Azure de saudação
Se você usar a verificação em duas etapas com o Azure, você deseja toocreate senhas de aplicativo por meio de saudação portal do Azure.

### <a name="toocreate-app-passwords-in-hello-azure-portal"></a>senhas de aplicativo toocreate em Olá portal do Azure
1. Entrar toohello portal clássico do Azure.
2. Na parte superior do hello, clique em seu nome de usuário e selecione verificação de segurança adicional.
3. Na página de proofup de saudação, na parte superior do hello, selecione as senhas de aplicativo
4. Clique em **Criar**.
5. Insira um nome para a senha de aplicativo hello e clique em **Avançar**
6. Copie Olá aplicativo senha toohello da área de transferência e cole-o em seu aplicativo.
   
   ![Nuvem](./media/multi-factor-authentication-end-user-app-passwords/app2.png)


### <a name="toodelete-app-passwords-in-hello-azure-portal"></a>senhas de aplicativo toodelete em Olá portal do Azure
1. Entrar toohello portal clássico do Azure.
2. Na parte superior do hello, clique em seu nome de usuário e selecione verificação de segurança adicional.
3. Na parte superior do hello, próxima verificação de segurança tooadditional, selecione **senhas de aplicativo.**
4. Senha do aplicativo toohello próxima deseja toodelete, selecione **excluir**.
5. Confirmar exclusão de saudação clicando **Sim**.
6. Depois que a senha de aplicativo hello for excluída, você pode clicar em **fechar**.


## <a name="manage-app-passwords-with-hello-myapps-portal"></a>Gerencie senhas de aplicativo com o portal de MyApps hello.
Se você não tiver certeza de como você pode usar a autenticação multifator, em seguida, você pode sempre criar e excluir as senhas de aplicativo por meio do portal myapps hello.

### <a name="toocreate-an-app-password-using-hello-myapps-portal"></a>toocreate uma senha de aplicativo usando Olá Myapps portal
1. Entrar muito[https://myapps.microsoft.com](https://myapps.microsoft.com)
2. Clique no nome na parte superior de saudação à direita e escolha **perfil**.
3. Escolha **Verificação de Segurança Adicional**.
   ![Selecione Verificação de Segurança Adicional – captura de tela](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. Selecione **senhas de aplicativo**.
   ![Selecione senhas de aplicativo – captura de tela](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. Clique em **Criar**.
6. Insira um nome para a senha de aplicativo hello e clique em **próximo**.
7. Copie Olá aplicativo senha toohello da área de transferência e cole-o em seu aplicativo.
   ![Criar uma senha de aplicativo](./media/multi-factor-authentication-end-user-app-passwords/create2.png)

### <a name="toodelete-an-app-password-using-hello-myapps-portal"></a>toodelete uma senha de aplicativo usando Olá Myapps portal
1. Entrar muito[https://myapps.microsoft.com](https://myapps.microsoft.com)
2. Na parte superior do hello, selecione o perfil.
3. Escolha **Verificação de Segurança Adicional**.

   ![Selecione Verificação de Segurança Adicional – captura de tela](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. Selecione **senhas de aplicativo**.

   ![Selecione senhas de aplicativo – captura de tela](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. Clique em Avançar senha de aplicativo toohello deseja toodelete, **excluir**.

   ![Excluir uma senha de aplicativo](./media/multi-factor-authentication-end-user-app-passwords/delete1.png)

6. Confirme que você deseja toodelete essa senha, clicando em **Sim**.
7. Depois que a senha de aplicativo hello for excluída, você pode clicar em **fechar**.

## <a name="next-steps"></a>Próximas etapas

- [Gerenciar suas configurações de verificação em duas etapas](multi-factor-authentication-end-user-manage-settings.md)

- Experimente Olá [aplicativo Microsoft Authenticator](microsoft-authenticator-app-how-to.md) tooverify suas entradas com as notificações do aplicativo, em vez de recebimento de textos ou chamadas. 
