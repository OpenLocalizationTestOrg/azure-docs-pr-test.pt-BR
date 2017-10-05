---
title: "Atribuir usuários a um domínio personalizado no Azure Active Directory | Microsoft Docs"
description: "Como preencher um domínio personalizado no Active Directory do Azure com contas de usuário."
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
ms.openlocfilehash: 39cb54a6637088c35c6aef864a804c24803f48ba
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="assign-users-to-a-custom-domain"></a>Atribuir usuários a um domínio personalizado
Após ter adicionado seu domínio personalizado ao Active Directory do Azure, você deve adicionar as contas de usuário a esse domínio para que possa começar a autenticá-los.

> [!IMPORTANT]
> A Microsoft recomenda que você gerencie o Azure AD usando o [Centro de administração do AD do Azure](https://aad.portal.azure.com) no portal do Azure em vez de usar o portal clássico do Azure mencionado neste artigo. Para saber como gerenciar seus nomes de domínio no centro de administração do Azure AD, consulte [Gerenciando nomes de domínio personalizados no Azure Active Directory](active-directory-domains-manage-azure-portal.md).

## <a name="users-synced-from-a-on-premises-directory"></a>Usuários sincronizados por meio de um diretório local
Se você já configurou uma conexão entre seu Active Directory local e o Active Directory do Azure, a sincronização poderá preencher as contas. Para obter mais informações sobre como sincronizar o Active Directory do Azure com o Active Directory local, consulte [Integração de suas identidades locais com o Active Directory do Azure](active-directory-aadconnect.md).

## <a name="users-added-and-managed-in-the-cloud"></a>Usuários adicionados e gerenciados na nuvem
Para alterar o domínio para uma conta de usuário:

1. Abra o portal clássico do Azure usando uma conta que seja um administrador global ou administrador de usuário.
2. Abra seu diretório.
3. Clique a guia **Usuários** .
4. Selecione o usuário na lista.
5. Altere o domínio para o usuário e selecione **Salvar**.

Isso também pode ser feito usando o [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) ou a [API do Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).

## <a name="select-a-custom-domain-when-creating-a-new-user"></a>Selecione um domínio personalizado ao criar um novo usuário
1. Abra o portal clássico do Azure usando uma conta que seja um administrador global ou administrador de usuário.
2. Abra seu diretório.
3. Clique a guia **Usuários** .
4. Na barra de comandos, selecione **Adicionar**.
5. Quando adicionar o nome de usuário, escolha o domínio personalizado na lista de domínios.
6. Selecione **Salvar**.

## <a name="next-steps"></a>Próximas etapas
* [Como usar nomes de domínio personalizados para simplificar a experiência de conexão para os usuários](active-directory-add-domain.md)
* [Gerenciar nomes de domínio personalizados](active-directory-add-manage-domain-names.md)
* [Saiba mais sobre os conceitos de gerenciamento de domínio no AD do Azure](active-directory-add-domain-concepts.md)

