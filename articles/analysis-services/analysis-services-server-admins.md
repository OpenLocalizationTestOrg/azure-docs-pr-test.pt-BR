---
title: Gerenciar administradores de servidor no Azure Analysis Services | Microsoft Docs
description: Saiba como gerenciar administradores de servidor para um servidor do Analysis Services no Azure.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: kfile
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 11/01/2017
ms.author: owend
ms.openlocfilehash: 6a42baf9fd880264e4130c009f27935a4743de21
ms.sourcegitcommit: d41d9049625a7c9fc186ef721b8df4feeb28215f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/02/2017
---
# <a name="manage-server-administrators"></a>Gerenciar administradores de servidor
Os administradores do servidor devem ser um usuário ou grupo válido no Azure AD (Azure Active Directory) para o locatário no qual o servidor reside. Você pode usar os **Administradores do Analysis Services** na folha de controle de seu servidor no portal do Azure ou nas Propriedades do Servidor no SSMS para gerenciar os administradores de servidor. 

## <a name="to-add-server-administrators-by-using-azure-portal"></a>Para adicionar administradores do servidor usando o Portal do Azure
1. Na folha de controle do seu servidor, clique em **os administradores de serviços de análise de**.
2. Na folha  **\<nomedoservidor >- Administradores de Serviços de Análise**, clique em **Adicionar**.
3. Na folha **Adicionar Administradores de Servidor**, selecione as contas de usuário do Azure AD ou convide usuários externos por meio de endereço de email.

    ![Administradores de servidor no portal do Azure](./media/analysis-services-server-admins/aas-manage-users-admins.png)

## <a name="to-add-server-administrators-by-using-ssms"></a>Para adicionar administradores do servidor usando o SSMS
1. Clique com botão direito do mouse em servidor > **Propriedades**.
2. Em **Propriedades do Analysis Server**, clique em **Segurança**.
3. Clique em **Adicionar** e, em seguida, insira o endereço de email de um usuário ou grupo em seu Azure AD.
   
    ![Adicionar administradores do servidor no SSMS](./media/analysis-services-server-admins/aas-manage-users-ssms.png)

## <a name="next-steps"></a>Próximas etapas 
[Autenticação e permissões de usuário](analysis-services-manage-users.md)  
[Gerenciar usuários e funções de banco de dados](analysis-services-database-users.md)  
[Controle de acesso baseado em função](../active-directory/role-based-access-control-what-is.md)  

