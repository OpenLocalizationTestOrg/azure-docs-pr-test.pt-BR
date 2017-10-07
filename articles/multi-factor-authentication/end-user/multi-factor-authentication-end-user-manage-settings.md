---
title: "aaaManage as configurações de verificação em duas etapas | Microsoft Docs"
description: "Gerencie como usar Autenticação Multifator do Azure incluindo alterar suas informações de contato ou configurar seus dispositivos."
services: multi-factor-authentication
keywords: "cliente do multifactor authentication, problema de autenticação, ID de correlação"
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: d3372d9a-9ad1-4609-bdcf-2c4ca9679a3b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: 2c974b08c584943f3c5a6b9bf16497d1706e8329
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-settings-for-two-step-verification"></a>Gerenciar as configurações de verificação em duas etapas
Este artigo responde às perguntas sobre como as configurações de tooupdate para a autenticação multifator ou de verificação em duas etapas. Se você estiver tendo problemas para entrar no tooyour conta, consulte muito[tendo problemas com a verificação em duas etapas](multi-factor-authentication-end-user-troubleshoot.md) para resolução de problemas.

## <a name="where-toofind-hello-settings-page"></a>Onde toofind Olá página Configurações
Dependendo de como a sua empresa usa a Autenticação Multifator do Azure, há alguns lugares onde você pode alterar as configurações, como o número de seu telefone.

Se o seu administrador de TI enviado uma URL específica ou a verificação de duas etapas toomanage etapas, siga essas instruções. Caso contrário, Olá seguindo instruções deve funcionar para todos os outros. Se você seguir estas etapas, mas não vir Olá opções, que significa que sua empresa ou escola seu próprio portal personalizado. Peça ao administrador do portal de autenticação multifator do Azure Olá link tooyour.

1. Entrar muito[https://myapps.microsoft.com](https://myapps.microsoft.com)  
2. Selecione o nome da conta em Olá superior direito e selecione **perfil**.  
3. Escolha **Verificação de segurança adicional**.  

    ![Myapps](./media/multi-factor-authentication-end-user-manage/myapps1.png)
4. página de verificação de segurança adicionais de saudação carrega com suas configurações.

    ![Prova](./media/multi-factor-authentication-end-user-manage/proofup.png)

## <a name="i-want-toochange-my-phone-number-or-add-a-secondary-number"></a>Eu quiser toochange meu número de telefone ou adicionar um número secundário
É importante tooconfigure um número de telefone de autenticação secundária.  Porque o principal número de telefone e seu aplicativo móvel são provavelmente em Olá mesmo telefone, número de telefone secundário Olá é única forma de saudação será tooget capaz de volta para sua conta, se o seu telefone for perdido ou roubado.

> [!NOTE]
> Se você não tem o número de telefone principal do acesso tooyour e precisar de ajuda para obter tooyour conta, consulte os tópicos de ajuda na [tendo problemas com a verificacao](multi-factor-authentication-end-user-troubleshoot.md).  

**toochange número de telefone principal:**  

1. Na página de verificação de segurança adicional hello, marque a caixa de texto de saudação com seu número de telefone atual e editá-lo com o novo número de telefone.  
2. Selecione **Salvar**.  
3. Se esse for o número de saudação que você usa para a opção de verificação preferencial, você tem novo número de saudação tooverify antes de salvá-lo.  

**tooadd um número de telefone secundário:**  

1. Na página de verificação de segurança adicional hello, caixa de seleção Olá Avançar muito**telefone de autenticação alternativo.**  
2. Insira seu número de telefone secundário na caixa de texto de saudação.  
3. Selecione **Salvar** e suas alterações são concluídas.  

## <a name="require-two-step-verification-again-on-a-device-youve-marked-as-trusted"></a>Exigir verificação em duas etapas novamente em um dispositivo que você marcou como confiável

Dependendo das configurações de sua organização, uma caixa de seleção "Não pergunte novamente por **X** dias" pode ser exibida quando você executa a verificação em duas etapas em seu navegador. Se essa caixa de seleção e, em seguida, perder seu dispositivo ou achar que a conta for comprometida, você deve restaurar tooall de verificação em duas etapas em seus dispositivos. 

1. Na página de verificação de segurança adicional hello, selecione **restauração multi-factor authentication em dispositivos confiáveis**.
2. Hello próxima vez que você entrar em qualquer dispositivo, você será solicitado tooperform verificacao. 

## <a name="how-do-i-clean-up-microsoft-authenticator-from-my-old-device-and-move-tooa-new-one"></a>Como limpar Microsoft Authenticator do meu dispositivo antigo e mover tooa um novo?
Quando você desinstala o aplicativo de saudação do seu dispositivo ou dispositivo de saudação de redefinição, não remove a ativação no back-end Olá Olá. Para saber mais, veja [Microsoft Authenticator](microsoft-authenticator-app-how-to.md).

## <a name="next-steps"></a>Próximas etapas
* Obter dicas de solução de problemas e ajuda em [Tendo problemas com a verificação em duas etapas](multi-factor-authentication-end-user-troubleshoot.md)
* Configure [senhas de aplicativo](multi-factor-authentication-end-user-app-passwords.md) para quaisquer aplicativos que não dão suporte à verificação em duas etapas.
