---
title: "aaaAdmins gerenciar usuários e dispositivos – o Azure MFA | Microsoft Docs"
description: "Descreve como toochange configurações do usuário, como forçar Olá usuários toodo Olá processo de verificação novamente."
documentationcenter: 
services: multi-factor-authentication
author: kgremban
manager: femila
ms.assetid: aac3b922-7cc1-428c-9044-273579aa7b5a
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 8c35435e4f6504014d9a4f6f1b837639c3b53481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-user-settings-with-azure-multi-factor-authentication-in-hello-cloud"></a>Gerenciar configurações de usuário com o Azure multi-Factor Authentication na nuvem Olá
Como administrador, você pode gerenciar Olá configurações de usuário e dispositivo a seguir:

* Exigir métodos de contato usuários tooprovide novamente
* Excluir senhas de aplicativo
* Exigir a MFA em todos os dispositivos confiáveis 

## <a name="require-users-tooprovide-contact-methods-again"></a>Exigir métodos de contato usuários tooprovide novamente
Essa configuração força o processo de registro de saudação do hello usuário toocomplete novamente. Aplicativos sem navegador continuam toowork se usuário Olá tiver senhas de aplicativo para eles.  Você pode excluir as senhas de usuários aplicativo hello selecionando **excluir todas as senhas de aplicativo existentes geradas pelos usuários Olá selecionado**.

### <a name="how-toorequire-users-tooprovide-contact-methods-again"></a>Como toorequire usuários tooprovide métodos de contato novamente
1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Olá esquerda, selecione **Active Directory do Azure** > **usuários e grupos** > **todos os usuários**.
3. Selecione **Autenticação Multifator**. Abre a página de autenticação multifator Hello. 
4. Verifique Olá caixa próxima toohello ou usuários que você deseja toomanage. Uma lista de opções de etapa rápida aparecem na saudação à direita. 
5. Selecione **Gerenciar configurações de usuário**.
6. Marque a caixa Olá para **exigir que os usuários selecionados tooprovide métodos de contato novamente**.
   ![Fornecer métodos de contato](./media/multi-factor-authentication-manage-users-and-devices/reproofup.png)
7. Clique em **Salvar**.
8. Clique em **Fechar**.

## <a name="delete-users-existing-app-passwords"></a>Excluir senhas de aplicativo de usuários existentes
Essa configuração exclui todas as senhas de aplicativo hello que um usuário tenha criado. Aplicativos sem navegador que estavam associados a essas senhas de aplicativo deixam de funcionar até que uma nova senha de aplicativo seja criada.

### <a name="how-toodelete-users-existing-app-passwords"></a>Como os usuários de toodelete existente senhas de aplicativo
1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Olá esquerda, selecione **Active Directory do Azure** > **usuários e grupos** > **todos os usuários**.
3. Selecione **Autenticação Multifator**. Abre a página de autenticação multifator Hello. 
6. Verifique Olá caixa próxima toohello ou usuários que você deseja toomanage. Uma lista de opções de etapa rápida aparecem na saudação à direita. 
7. Selecione **Gerenciar configurações de usuário**.
8. Marque a caixa Olá para **excluir todas as senhas de aplicativo existentes geradas pelos usuários Olá selecionado**.
   ![Excluir senhas de aplicativo](./media/multi-factor-authentication-manage-users-and-devices/deleteapppasswords.png)
9. Clique em **Salvar**.
10. Clique em **Fechar**.

## <a name="restore-mfa-on-all-remembered-devices-for-a-user"></a>Restaurar o MFA em todos os dispositivos lembrados de um usuário
Um dos recursos configurável de saudação do Azure multi-Factor Authentication está dando a seus usuários Olá opção toomark dispositivos confiáveis. Para saber mais, confira [Definir as configurações da Autenticação Multifator do Azure](multi-factor-authentication-whats-next.md#remember-multi-factor-authentication-for-devices-that-users-trust).

Os usuários podem ignorar a verificação em duas etapas durante um período configurável em seus dispositivos regulares. Se uma conta for comprometida ou um dispositivo confiável é perdido, você precisa toobe tooremove capaz de saudação confiável status e exige verificação de duas etapas novamente.

Olá **restauração multi-factor authentication em todos os dispositivos lembrados** configuração significa que esse usuário Olá será Olá de verificação em duas etapas desafiados tooperform próxima vez que entrar, independentemente se eles decidiram toomark seus dispositivo como confiável. 

### <a name="how-toorestore-mfa-on-all-suspended-devices-for-a-user"></a>Como toorestore MFA em todos os dispositivos suspensos para um usuário
1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Olá esquerda, selecione **Active Directory do Azure** > **usuários e grupos** > **todos os usuários**.
3. Selecione **Autenticação Multifator**. Abre a página de autenticação multifator Hello. 
6. Verifique Olá caixa próxima toohello ou usuários que você deseja toomanage. Uma lista de opções de etapa rápida aparecem na saudação à direita. 
7. Selecione **Gerenciar configurações de usuário**.
8. Marque a caixa Olá para **restauração multi-factor authentication em todos os dispositivos lembrados**
   ![excluir senhas de aplicativo](./media/multi-factor-authentication-manage-users-and-devices/rememberdevices.png)
9. Clique em **Salvar**.
10. Clique em **Fechar**.

## <a name="next-steps"></a>Próximas etapas

- Obter mais informações sobre como muito[configurações de configurar o Azure multi-Factor Authentication](multi-factor-authentication-whats-next.md)

- Se os usuários precisarem de Ajuda, apontá-los em direção à saudação [guia do usuário para verificação em duas etapas](./end-user/multi-factor-authentication-end-user.md)
