---
title: "aaaSet um dispositivo Windows 10 com o Azure AD de configurações | Microsoft Docs"
description: "Explica como os usuários podem ingressar tooAzure AD por meio do menu de configurações de saudação."
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: b844e1d9-ad43-4e4a-a398-5c4a43bf2f5c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: d6485228338db571cc01f913c99fbba49e0bb74a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-windows-10-device-with-azure-ad-from-settings"></a>Configurar um dispositivo Windows 10 com o Azure AD nas Configurações
Se você já estiver usar o Windows 7 ou Windows 8 e seu computador ou dispositivo foi atualizado tooWindows 10, você pode ingressar em tooAzure do Active Directory (AD do Azure) por meio do menu de configurações de saudação.

## <a name="toojoin-tooazure-ad-from-hello-settings-menu"></a>toojoin tooAzure AD no menu de configurações de saudação
1. De saudação **iniciar** menu, clique em Olá **configurações** botão.
2. Em **Configurações**, escolha    **Sistema**->**Sobre**->**Ingressar no Azure AD**.
   
   <center>
   ![Ingressar no menu de configurações de saudação do AD do Azure](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png)</center>
3. Clique em **continuar** na janela de mensagem de junção do Azure AD hello.
   
   <center>
   ![Janela de mensagem de ingresso no Azure AD](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png) </center>
4. Forneça suas credenciais de entrada. Essa experiência de logon incluirá todas as etapas de saudação toocomplete necessária autenticação. Se você fizer parte de um locatário federado, o administrador fornecerá experiência de Federação Olá que é hospedada pela sua organização.
   <center>
   ![Fornecer suas credenciais de entrada](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png) </center>
5. Se sua organização tiver configurado o Azure multi-Factor Authentication para ingresso tooAzure AD, forneça o segundo fator Olá antes de continuar.
6. Clique em **aceitar** em Olá **permitir esta toobe dispositivo gerenciado** tela.
7. Você deve ver a mensagem de saudação "o dispositivo agora está unido tooyour organização no AD do Azure".

## <a name="additional-information"></a>Informações adicionais
* [Saiba mais sobre cenários de uso da Junção do Azure AD](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Conecte-se a dispositivos que ingressaram no domínio tooAzure AD para experiências do Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configurar a Junção do Azure AD](active-directory-azureadjoin-setup.md)
* [Autenticando identidades sem senhas com o Microsoft Passport](active-directory-azureadjoin-passport.md)

