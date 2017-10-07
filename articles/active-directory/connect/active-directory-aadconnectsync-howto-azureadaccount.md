---
title: "Sincronização do Azure AD Connect: como conta de serviço toomanage Olá AD do Azure | Microsoft Docs"
description: "Este tópico documenta como conta de serviço toorestore Olá AD do Azure."
services: active-directory
keywords: "AADSTS70002, AADSTS50054, como tooreset Olá senha Olá sincronização do Azure AD Connect conta de serviço do conector"
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 6077043a-27f1-4304-a44b-81dc46620f24
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: e563518eae173de42a1d40bb5a76e63f29f9da42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-how-toomanage-hello-azure-ad-service-account"></a>Sincronização do Azure AD Connect: como conta de serviço toomanage Olá AD do Azure
conta de serviço de saudação usada por Olá conector AD do Azure deve toobe serviço gratuito. Se você precisar tooreset suas credenciais, este tópico é para você. Por exemplo, se um Administrador Global tem por engano redefinir Olá senha na conta de serviço hello usando o PowerShell.

## <a name="reset-hello-credentials"></a>Redefinir credenciais de saudação
Se a conta de serviço de Olá definida no hello conector AD do Azure não pode entrar em contato com o AD do Azure devido a problemas de tooauthentication, Olá poderá ser redefinida.

1. Entre no servidor de sincronização do Azure AD Connect toohello e inicie o PowerShell.
2. Execute `Add-ADSyncAADServiceAccount`.  
   ![Cmdlet addadsyncaadserviceaccount do PowerShell](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)
3. Forneça credenciais de Administrador Global do Azure AD.

Esse cmdlet redefine a senha Olá Olá conta de serviço e atualizá-lo no AD do Azure e no mecanismo de sincronização de saudação.

## <a name="known-issues-these-steps-can-solve"></a>Problemas conhecidos que essas etapas podem resolver
Esta seção é uma lista de erros relatados por clientes que foram corrigidos por um credenciais redefinir Olá conta de serviço do AD do Azure.

- - -
Evento 6900  
servidor de saudação encontrou um erro inesperado ao processar uma notificação de alteração de senha:  
AADSTS70002: erro ao validar as credenciais. AADSTS50054: A senha antiga é usada para autenticação.

- - -
Evento 659  
Erro ao recuperar a configuração de sincronização de política de senha. Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:  
AADSTS70002: erro ao validar as credenciais. AADSTS50054: A senha antiga é usada para autenticação.

## <a name="next-steps"></a>Próximas etapas
**Tópicos de visão geral**

* [Sincronização do Azure AD Connect: compreender e personalizar a sincronização](active-directory-aadconnectsync-whatis.md)
* [Integração de suas identidades locais com o Active Directory do Azure](active-directory-aadconnect.md)

