---
title: "Solução de problemas: O item 'Active Directory' está ausente ou não disponível | Microsoft Docs"
description: "Quais toodo quando o item de menu do Active Directory não aparece no Portal de gerenciamento de saudação."
services: active-directory
documentationcenter: na
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 3383020d-6397-43ea-b7aa-c6a9d6a1e3df
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.openlocfilehash: d7355a4e39141f0b09272dc5615c309b23c8c70f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-active-directory-item-is-missing-or-not-available"></a>Solução de problemas: o item “Active Directory” está ausente ou não está disponível
Muitas das instruções Olá para o uso de recursos do Active Directory do Azure e serviços começam com "Vá toohello Portal de gerenciamento do Azure e clique em **do Active Directory**." Mas o que fazer se o item de menu ou extensão do Active Directory Olá não aparecer ou se ele está marcado como **não disponível**? Este tópico é toohelp projetado. Ele descreve as condições de saudação sob a qual **do Active Directory** não aparece ou não está disponível e explica como tooproceed.

## <a name="active-directory-is-missing"></a>Active Directory ausente
Normalmente, um **do Active Directory** item aparece no menu de navegação à esquerda de saudação. instruções de Olá nos procedimentos do Azure Active Directory pressupõem que este item está no modo de exibição.

![Captura de tela: Active Directory no Azure](./media/active-directory-troubleshooting/typical-view.png)

o item Active Directory Olá aparece no menu de navegação à esquerda do hello quando qualquer Olá seguintes condições for verdadeira. Caso contrário, o item de saudação não aparecerá.

* usuário atual Olá conectado com uma conta da Microsoft (anteriormente conhecida como um Windows Live ID).
  
    OU
* Olá locatário do Azure tem um diretório e conta do hello atual é um administrador de diretório.
  
    OU
* Olá locatário do Azure tem pelo menos um namespace de controle de acesso do AD do Azure (ACS). Para obter mais informações, confira [Namespace de Controle de Acesso](https://msdn.microsoft.com/library/azure/gg185908.aspx).
  
    OU
* Olá locatário do Azure tem pelo menos um provedor de autenticação multifator do Azure. Para obter mais informações, confira [Administrando Provedores do Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).

toocreate um namespace de controle de acesso ou um provedor de autenticação multifator, clique em **+ novo** > **serviços de aplicativos** > **do Active Directory**.

tooget diretório de tooa direitos administrativos, têm um administrador atribua um administrador função tooyour conta. Para obter detalhes, confira [Atribuindo funções de administrador](active-directory-assign-admin-roles.md).

## <a name="active-directory-is-not-available"></a>Active Directory não disponível
Quando você clica em **+Novo** > **Serviços de Aplicativos**, um item do **Active Directory** é exibido. Especificamente, o item Active Directory Olá aparece quando qualquer um dos recursos do Active Directory hello, como diretório, controle de acesso ou provedor de autenticação multifator, são o usuário atual toohello disponíveis.

No entanto, enquanto o carregamento da página hello, item Olá estiver esmaecido e está marcado como **não está disponível**. Este é um estado temporário. Se você esperar alguns segundos, o item de saudação fica disponível. Se Olá atraso for prolongado, atualizar a página da web hello normalmente resolve o problema de saudação.

![Captura de tela: Active Directory não disponível](./media/active-directory-troubleshooting/not-available.png)

