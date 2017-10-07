---
title: "aaaSetting a junção do Azure AD para seus usuários | Microsoft Docs"
description: "Explica como os administradores podem configurar a Junção do Azure AD para o diretório local e o registro de dispositivos."
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: bfc5d415-c918-4d8b-afee-b3f41cc28469
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 60a5aeb11292cb6057ab1065c3ab77e5981d0cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-azure-ad-join-in-your-organization"></a>Configuração da Junção do Azure AD na sua organização
Antes de configurar a junção do Azure Active Directory (junção do Azure AD), você precisar de sincronização de tooeither até seu diretório local da nuvem de toohello de usuários ou criar manualmente as contas gerenciadas no AD do Azure.

Instruções detalhadas para sincronizar seu tooAzure de usuários local AD é abordado em [integrando suas identidades locais ao Active Directory do Azure](active-directory-aadconnect.md).

toomanually criar e gerenciar os usuários no AD do Azure, consulte muito[gerenciamento de usuário no AD do Azure](https://msdn.microsoft.com/library/azure/hh967609.aspx).

## <a name="set-up-device-registration"></a>Configure o registro de dispositivos
1. Faça logon no toohello portal do Azure como administrador.
2. No painel esquerdo do hello, selecione **do Active Directory**.
3. Em Olá **diretório** , selecione seu diretório.
4. Selecione Olá **configurar** guia.
5. Vá toohello **dispositivos** seção.
6. Em Olá **dispositivos** guia, defina Olá seguinte:  
   * **MÁXIMO número de dispositivos por usuário**: selecione Olá o número máximo de dispositivos que um usuário pode ter no AD do Azure.  Se um usuário atingir essa cota, eles não estarão dispositivos adicionais capaz de tooadd até que um ou mais dos seus dispositivos existentes são removidos.
   * **EXIGIR autenticação MULTIFATOR tooJOIN dispositivos**: definir se os usuários são necessária tooprovide uma autenticação de segundo fator toojoin tooAzure seu dispositivo AD. Para obter mais informações sobre o Azure multi-Factor Authentication, consulte [guia de Introdução ao Azure multi-Factor Authentication na nuvem Olá](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).
   * **Os usuários podem dispositivos de junção do AZURE AD**: selecione Olá usuários e grupos são permitidos toojoin dispositivos tooAzure AD.
   * **DISPOSITIVOS que ingressaram no AD do AZURE ON de administradores adicionais**: com o Azure AD Premium ou Olá Enterprise Mobility Suite (EMS), você pode escolher quais usuários são concedidos direitos de administrador local toohello dispositivo. Os administradores globais e os proprietários do dispositivo recebem direitos de administrador local por padrão.

<center>![Configure o registro de dispositivos](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center>

Depois de configurar junção do Azure AD para seus usuários, eles podem se conectar dispositivos pessoais ou tooAzure AD por meio de sua empresa.

A seguir estão os três cenários de saudação você pode usar tooenable tooset seus usuários a junção do Azure AD:

* Os usuários se associar a um dispositivo da empresa diretamente tooAzure AD.
* Usuários toohello de dispositivo de uma empresa de associação de domínio do Active Directory local e estende Olá dispositivo tooAzure AD.
* Adicionarem usuários ou contas de estudante tooWindows em um dispositivo pessoal

## <a name="additional-information"></a>Informações adicionais
* [Windows 10 para a empresa Olá: dispositivos de toouse maneiras de trabalho](active-directory-azureadjoin-windows10-devices-overview.md)
* [Estendendo nuvem dispositivos de tooWindows 10 de recursos por meio de junção do Active Directory do Azure](active-directory-azureadjoin-user-upgrade.md)
* [Saiba mais sobre cenários de uso da Junção do Azure AD](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Conecte-se a dispositivos que ingressaram no domínio tooAzure AD para experiências do Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configurar a Junção do Azure AD](active-directory-azureadjoin-setup.md)

