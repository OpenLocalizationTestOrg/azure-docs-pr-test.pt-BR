---
title: "domínio personalizado do aaaAssign usuários tooa no Active Directory do Azure | Microsoft Docs"
description: "Como toopopulate um domínio personalizado no Azure Active Directory com contas de usuário."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 717b5a7c-7bc3-4ab1-98b5-4740b53338fe
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 23c338a361a90fddf42d4df90db94c9774305886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-users-tooa-custom-domain"></a>Atribuir usuários tooa o domínio personalizado
Depois que você adicionou tooAzure seu domínio personalizado do Active Directory, você deve adicionar contas de usuário Olá para esse domínio para que você possa começar a autenticá-los.

> [!IMPORTANT]
> A Microsoft recomenda que você gerencie o AD do Azure usando Olá [Centro de administração do AD do Azure](https://aad.portal.azure.com) em Olá portal do Azure em vez de usar Olá portal clássico do Azure mencionado neste artigo. Para como toomanage seu nomes de domínio no Centro de administração de saudação do AD do Azure, consulte [gerenciar nomes de domínio personalizado no Active Directory do Azure](active-directory-domains-manage-azure-portal.md).

## <a name="users-synced-from-a-on-premises-directory"></a>Usuários sincronizados por meio de um diretório local
Se você já configurou uma conexão entre o local do Active Directory e o Active Directory do Azure, a sincronização pode preencher contas hello. Para obter mais informações sobre como toosynchronize do Active Directory do Azure com seu local no Active Directory, consulte [integrando suas identidades locais ao Active Directory do Azure](active-directory-aadconnect.md).

## <a name="users-added-and-managed-in-hello-cloud"></a>Os usuários adicionados e gerenciados em nuvem Olá
domínio de saudação toochange para uma conta de usuário:

1. Olá Abrir portal clássico do Azure usando uma conta que seja um administrador global ou um administrador do usuário.
2. Abra seu diretório.
3. Selecione Olá **usuários** guia.
4. Selecione usuário Olá Olá lista.
5. Alterar domínio Olá para usuário hello e, em seguida, selecione **salvar**.

Isso também pode ser feito usando [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) ou hello [API do Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).

## <a name="select-a-custom-domain-when-creating-a-new-user"></a>Selecione um domínio personalizado ao criar um novo usuário
1. Olá Abrir portal clássico do Azure usando uma conta que seja um administrador global ou um administrador do usuário.
2. Abra seu diretório.
3. Selecione Olá **usuários** guia.
4. Na barra de comandos hello, selecione **adicionar**.
5. Quando você adiciona um nome de usuário hello, escolha domínio personalizado Olá Olá lista de domínios.
6. Selecione **Salvar**.

## <a name="next-steps"></a>Próximas etapas
* [Usando o domínio personalizado nomes toosimplify Olá experiência de logon para os usuários](active-directory-add-domain.md)
* [Gerenciar nomes de domínio personalizados](active-directory-add-manage-domain-names.md)
* [Saiba mais sobre os conceitos de gerenciamento de domínio no AD do Azure](active-directory-add-domain-concepts.md)

