---
title: "membros de saudação aaaManage para um grupo no Active Directory do Azure | Microsoft Docs"
description: "Como tooadd ou remover usuários e dispositivos de um grupo no Active Directory do Azure"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d399a97d-fd2a-4b2d-b73d-0975db83f41b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4cb16ee63828003da251423a04736f7174dd4896
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-group-membership-for-users-in-your-azure-active-directory-tenant"></a>Gerenciar associação de grupo de usuários em seu locatário do Azure Active Directory
Este artigo explica como toomanage Olá membros de um grupo no Azure Active Directory (AD do Azure).

## <a name="how-do-i-find-hello-members-and-manage-them"></a>Como localizar membros hello e gerenciá-los?
1. Entrar toohello [portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global para o diretório de saudação.
2. Selecione **mais serviços**, digite **usuários e grupos** Olá caixa de texto e, em seguida, selecione **Enter**.

   ![Abrir o gerenciamento de usuários](./media/active-directory-groups-members-azure-portal/search-user-management.png)
3. Em Olá **usuários e grupos** folha, selecione **todos os grupos de**.

   ![Folha de grupos de saudação de abertura](./media/active-directory-groups-members-azure-portal/view-groups-blade.png)
4. Em Olá **usuários e grupos - todos os grupos** folha, selecione um grupo.
5. Em Olá **grupo - *groupname***  folha, selecione **membros**.

   ![Folha de membros de saudação de abertura](./media/active-directory-groups-members-azure-portal/view-group-members.png)
6. tooadd membros toohello grupo Olá **grupo - membros** folha, selecione **adicionar membros**.

   ![Comando Adicionar Membros](./media/active-directory-groups-members-azure-portal/add-group-members-command.png)
7. Em Olá **membros** folha, selecione um ou mais usuários ou dispositivos de grupo de toohello de tooadd e selecione Olá **selecione** botão na parte inferior de saudação do hello folha tooadd-los toohello grupo. Olá **usuário** caixa filtra Olá com base na correspondência de sua parte de tooany de entrada de um nome de usuário ou dispositivo de exibição. Caracteres curinga não são aceitos nessa caixa.
8. os membros do grupo Olá Olá tooremove **grupo - membros** folha, selecione um membro.
9. Em Olá ***membername*** folha, selecione Olá **remover** de comando e confirme sua escolha no prompt de saudação.

   ![Comando Remover Membros](./media/active-directory-groups-members-azure-portal/remove-group-members-command.png)
10. Quando terminar de alterar os membros do grupo de saudação, selecione **salvar**.

## <a name="additional-information"></a>Informações adicionais
Esses artigos fornecem mais informações sobre o Active Directory do Azure.

* [Ver grupos existentes](active-directory-groups-view-azure-portal.md)
* [Criar um novo grupo e adicionando membros](active-directory-groups-create-azure-portal.md)
* [Gerenciar configurações de um grupo](active-directory-groups-settings-azure-portal.md)
* [Gerenciar associações de um grupo](active-directory-groups-membership-azure-portal.md)
* [Gerenciar regras dinâmicas para usuários em um grupo](active-directory-groups-dynamic-membership-azure-portal.md)
