---
title: "aaaCreate um grupo de usuários no Active Directory do Azure | Microsoft Docs"
description: Como toocreate um grupo no Active Directory do Azure e adicionar membros toohello grupo
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fc583a7f02ce50e7f3b2c8f97a9c032a3e2dc33a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-group-and-add-members-in-azure-active-directory"></a>Criar um grupo e adicionar membros no Azure Active Directory
> [!div class="op_single_selector"]
> * [Portal do Azure](active-directory-groups-create-azure-portal.md)
> * [Portal clássico do Azure](active-directory-accessmanagement-manage-groups.md)
> * [PowerShell](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

Este artigo explica como toocreate e popular um novo grupo no Active Directory do Azure. Use as tarefas de gerenciamento de tooperform um grupo como a atribuição de permissões ou licenças tooa o número de usuários ou dispositivos de uma vez.

## <a name="how-do-i-create-a-group"></a>Como faço para criar um grupo?
1. Entrar toohello [portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global para o diretório de saudação.
2. Selecione **mais serviços**, digite **usuários e grupos** Olá caixa de texto e, em seguida, selecione **Enter**.

   ![Abrir o gerenciamento de usuários](./media/active-directory-groups-create-azure-portal/search-user-management.png)
3. Em Olá **usuários e grupos** folha, selecione **todos os grupos de**.

   ![Folha de grupos de saudação de abertura](./media/active-directory-groups-create-azure-portal/view-groups-blade.png)
4. Em Olá **usuários e grupos - todos os grupos de** folha, selecione Olá **adicionar** comando.

   ![Selecionando o comando Add a saudação](./media/active-directory-groups-create-azure-portal/add-group-command.png)
5. Em Olá **grupo** folha, adicionar um nome e uma descrição para o grupo de saudação.
6. tooselect membros tooadd toohello grupo, selecione **atribuído** em Olá **tipo de associação** caixa e, em seguida, selecione **membros**. Para obter mais informações sobre como toomanage Olá associação de um grupo dinamicamente, consulte [usar atributos toocreate avançado regras de associação de grupo](active-directory-groups-dynamic-membership-azure-portal.md).

   ![Selecionando membros tooadd](./media/active-directory-groups-create-azure-portal/select-members.png)
7. Em Olá **membros** folha, selecione um ou mais usuários ou dispositivos de grupo de toohello de tooadd e selecione Olá **selecione** botão na parte inferior de saudação do hello folha tooadd-los toohello grupo. Olá **usuário** caixa filtra Olá com base na correspondência de sua parte de tooany de entrada de um nome de usuário ou dispositivo de exibição. Caracteres curinga não são aceitos nessa caixa.
8. Quando terminar de adicionar o grupo de membros do toohello, selecione **criar** em Olá **grupo** folha.    

   ![Criar a confirmação do grupo](./media/active-directory-groups-create-azure-portal/create-group-confirmation.png)


## <a name="next-steps"></a>Próximas etapas
Esses artigos fornecem mais informações sobre o Active Directory do Azure.

* [Consultar grupos existentes](active-directory-groups-view-azure-portal.md)
* [Gerenciar configurações de um grupo](active-directory-groups-settings-azure-portal.md)
* [Gerenciar membros de um grupo](active-directory-groups-members-azure-portal.md)
* [Gerenciar associações de um grupo](active-directory-groups-membership-azure-portal.md)
* [Gerenciar regras dinâmicas para usuários em um grupo](active-directory-groups-dynamic-membership-azure-portal.md)
