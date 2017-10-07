---
title: "grupos de saudação aaaManage seu grupo pertence tooin Active Directory do Azure | Microsoft Docs"
description: "Os grupos podem conter outros grupos no Azure Active Directory. Aqui está como toomanage essas associações."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e785c2d0-7724-47d4-a56e-c58280c08a14
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0a0a1967084de0968e1e802559f9cdfd7ca6ae4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-toowhich-groups-a-group-belongs-in-your-azure-active-directory-tenant"></a>Gerenciar grupos de toowhich que pertence a um grupo no seu locatário do Active Directory do Azure
Os grupos podem conter outros grupos no Azure Active Directory. Aqui está como toomanage essas associações.

## <a name="how-do-i-find-hello-groups-my-group-is-a-member-of"></a>Como localizar grupos Olá que meu grupo é membro?
1. Entrar toohello [portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global para o diretório de saudação.
2. Selecione **mais serviços**, digite **usuários e grupos** Olá caixa de texto e, em seguida, selecione **Enter**.

   ![Abrir o gerenciamento de usuários](./media/active-directory-groups-membership-azure-portal/search-user-management.png)
3. Em Olá **usuários e grupos** folha, selecione **todos os grupos de**.

   ![Folha de grupos de saudação de abertura](./media/active-directory-groups-membership-azure-portal/view-groups-blade.png)
4. Em Olá **usuários e grupos - todos os grupos** folha, selecione um grupo.
5. Em Olá **grupo - *groupname***  folha, selecione **as associações de grupo**.

   ![Folha de associações de grupo abertura Olá](./media/active-directory-groups-membership-azure-portal/group-membership-blade.png)
6. tooadd seu grupo como membro de outro grupo, em Olá **grupo - as associações de grupo** folha, selecione Olá **adicionar** comando.
7. Selecione um grupo de saudação **Selecionar grupo** folha e, em seguida, selecione Olá **selecione** botão na parte inferior da saudação da folha de saudação. Você pode adicionar o grupo tooonly um grupo por vez. Olá **usuário** caixa filtra Olá com base na correspondência de sua parte de tooany de entrada de um nome de usuário ou dispositivo de exibição. Caracteres curinga não são aceitos nessa caixa.

   ![Adicionar uma associação de grupo](./media/active-directory-groups-membership-azure-portal/add-group-membership.png)
8. tooremove seu grupo como membro de outro grupo, em Olá **grupo - as associações de grupo** folha, selecione um grupo.
9. Em Olá ***groupname*** folha, selecione Olá **remover** de comando e confirme sua escolha no prompt de saudação.

   ![comando remover associação](./media/active-directory-groups-membership-azure-portal/remove-group-membership.png)
10. Quando terminar de alterar as associações de grupo para o grupo, escolha **Salvar**.

## <a name="additional-information"></a>Informações adicionais
Esses artigos fornecem mais informações sobre o Active Directory do Azure.

* [Ver grupos existentes](active-directory-groups-view-azure-portal.md)
* [Criar um novo grupo e adicionando membros](active-directory-groups-create-azure-portal.md)
* [Gerenciar configurações de um grupo](active-directory-groups-settings-azure-portal.md)
* [Gerenciar membros de um grupo](active-directory-groups-members-azure-portal.md)
* [Gerenciar regras dinâmicas para usuários em um grupo](active-directory-groups-dynamic-membership-azure-portal.md)
