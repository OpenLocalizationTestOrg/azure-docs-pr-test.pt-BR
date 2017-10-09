---
title: "aaaJoin uma organização de tooyour dispositivo pessoal | Microsoft Docs"
description: "Explica como os usuários podem registrar suas redes corporativas pessoal do Windows 10 dispositivos tootheir e fornece as etapas de implantação para um cenário de BYOD."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 9f3d38f5-1cfd-43d4-97da-4fed1255a1ff
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 979e2461dd9ad0438aa402a0a3223cc84c4c625c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-personal-device-tooyour-organization"></a>Ingressar em uma organização de tooyour dispositivo pessoal
## <a name="toojoin-a-windows-10-device-tooyour-organization"></a>organização de tooyour dispositivo toojoin um Windows 10
1. De saudação **iniciar** menu, selecione **configurações**.
2. Selecione **Contas** e, em seguida, clique em **Sua conta**.
3. Clique em **Adicionar conta corporativa ou de estudante**e, em seguida, digite sua conta organizacional.
4. Na saudação página de entrada para a sua organização, insira seu nome de usuário e senha e, em seguida, clique em **Okey**.
5. Um desafio de Multi-Factor Authentication será apresentado a você. (Esse desafio é configurável por um administrador de TI.)
6. Azure Active Directory (AD do Azure) verifica se o dispositivo Olá requer registro de gerenciamento de dispositivo móvel.
7. Windows registra o dispositivo Olá no diretório da organização Olá no AD do Azure e se registra no gerenciamento de dispositivos móveis, se apropriado.
8. Se você for um usuário gerenciado, o Windows usa toohello desktop por meio de entrada automática hello.
9. Se você for um usuário federado, você será levado tooa entrar no Windows tela tooenter suas credenciais.

## <a name="additional-information"></a>Informações adicionais
* [Windows 10 para a empresa Olá: dispositivos de toouse maneiras de trabalho](active-directory-azureadjoin-windows10-devices-overview.md)
* [Estendendo nuvem dispositivos de tooWindows 10 de recursos por meio de junção do Active Directory do Azure](active-directory-azureadjoin-user-upgrade.md)
* [Autenticando identidades sem senhas com o Microsoft Passport](active-directory-azureadjoin-passport.md)
* [Saiba mais sobre cenários de uso da Junção do Azure AD](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Conecte-se a dispositivos que ingressaram no domínio tooAzure AD para experiências do Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configurar a Junção do Azure AD](active-directory-azureadjoin-setup.md)

