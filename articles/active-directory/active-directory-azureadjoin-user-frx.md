---
title: "aaaSet um novo dispositivo com o AD do Azure durante a instalação | Microsoft Docs"
description: "Um tópico que explica como os usuários podem configurar a Junção do Azure AD durante sua experiência de primeira execução."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 06a149f7-4aa1-4fb9-a8ec-ac2633b031fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 6afce4be7f084f1956a6f9dbddaa8def0605956d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-new-device-with-azure-ad-during-setup"></a>Configurar um novo dispositivo com o AD do Azure durante a instalação
No Windows 10, os usuários podem ingressar seu dispositivos tooAzure do Active Directory (AD do Azure) na experiência de primeira execução da saudação (FRX). Isso permite que os funcionários do organizações toodistribute dispositivos têm embalagem tootheir ou alunos ou escolherei seus próprios dispositivos (CYOD).
Se o Windows 10 Professional ou Windows 10 Enterprise Edition está instalado em um dispositivo, Olá apresentar o processo de instalação padrão é toohello para dispositivos da empresa.

## <a name="toojoin-a-device-tooazure-ad"></a>toojoin tooAzure um dispositivo AD
1. Quando você ativa o novo dispositivo e iniciar o processo de instalação hello, você deve ver Olá **Preparando-se** mensagem. Siga Olá prompts tooset o seu dispositivo.
2. Inicie personalizando a região e o idioma. Aceite Olá Microsoft Software License Terms.
   ![Personalizar a região](./media/active-directory-azureadjoin/active-directory-azureadjoin-customize-region.png)
3. Selecione a rede de saudação serão toouse para conectar-se toohello da Internet.
4. Selecione se está usando um dispositivo pessoal ou de propriedade da empresa. Se ele estiver sendo da empresa, clique em **este dispositivo pertence organização toomy**. Isso inicia a experiência de junção do Azure AD de saudação. Apresentamos a seguir uma tela que será exibida se estiver usando o Windows 10 Professional.
   <center>
   ![Tela Quem é o proprietário deste computador?](./media/active-directory-azureadjoin/active-directory-azureadjoin-who-owns-pc.png)
5. Insira as credenciais de saudação que foram fornecidas tooyou pela sua organização.
   <center>
   ![Tela de entrada](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)
6. Depois de inserir seu nome de usuário, um locatário correspondente estará localizado no Azure AD. Se você estiver em um domínio federado, será o servidor de Token STS (serviço seguro) no local redirecionado tooyour--por exemplo, Active Directory Federation Services (AD FS).
7. Se você for um usuário em um domínio não federadas, insira suas credenciais diretamente no hello páginas hospedado pelo AD do Azure. Você também verá o logotipo de sua organização e um texto de suporte se a identidade visual da empresa tiver sido configurada.
8. Um desafio da autenticação multifator será apresentado a você. Esse desafio é configurável por um administrador de TI.
9. O Azure AD verifica se esse usuário/dispositivo exige registro no gerenciamento de dispositivo móvel.
10. Windows registra o dispositivo Olá no diretório da organização Olá no AD do Azure e se registra no gerenciamento de dispositivos móveis, se apropriado.
11. Se você for um usuário gerenciado, o Windows usa toohello desktop por meio do processo de entrada automática hello.
12. Se você for um usuário federado, você será direcionado toohello entrar no Windows tela tooenter suas credenciais.

> [!NOTE]
> Não há suporte para a ingressar em um domínio do Windows Server Active Directory local no Windows de saudação do usuário. Portanto, se você planejar toojoin um domínio de tooa do computador, você deve selecionar link Olá **configurar o Windows com uma conta local** em vez disso. Em seguida, você pode adicionar domínio Olá das configurações da saudação em seu computador como fez antes.
> 
> 

## <a name="additional-information"></a>Informações adicionais
* [Windows 10 para a empresa Olá: dispositivos de toouse maneiras de trabalho](active-directory-azureadjoin-windows10-devices-overview.md)
* [Estendendo nuvem dispositivos de tooWindows 10 de recursos por meio de junção do Active Directory do Azure](active-directory-azureadjoin-user-upgrade.md)
* [Autenticando identidades sem senhas com o Microsoft Passport](active-directory-azureadjoin-passport.md)
* [Saiba mais sobre cenários de uso da Junção do Azure AD](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Conecte-se a dispositivos que ingressaram no domínio tooAzure AD para experiências do Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configurar a Junção do Azure AD](active-directory-azureadjoin-setup.md)

