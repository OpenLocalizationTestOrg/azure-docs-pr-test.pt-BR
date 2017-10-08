---
title: os administradores de servidor aaaManage no Azure Analysis Services | Microsoft Docs
description: Saiba como administradores de servidor toomanage para um servidor do Analysis Services no Azure.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: e04387e48e9b9483c382ee5cc9fd65f8331fb2a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-server-administrators"></a>Gerenciar administradores de servidor
Os administradores de servidor devem ser um usuário ou grupo válido no hello Azure Active Directory (AD do Azure) para o locatário Olá em qual Olá servidor reside. Você pode usar **administradores do Analysis Services** na folha de controle Olá para o servidor no portal do Azure ou os administradores de servidor do SSMS toomanage propriedades de servidor. 

## <a name="tooadd-server-administrators-by-using-azure-portal"></a>administradores de servidor tooadd usando o portal do Azure
1. Na folha de controle de saudação do servidor, clique em **administradores do Analysis Services**.
2. Em Olá  **\<servername >-os administradores de serviços de análise** folha, clique em **adicionar**.
3. Em Olá **adicionar administradores de servidor** folha, selecione as contas de usuário do AD do Azure ou convidar usuários externos por endereço de email.

    ![Administradores de servidor no portal do Azure](./media/analysis-services-server-admins/aas-manage-users-admins.png)

## <a name="tooadd-server-administrators-by-using-ssms"></a>administradores de servidor tooadd usando o SSMS
1. Servidor de saudação atalho > **propriedades**.
2. Em **Propriedades do Analysis Server**, clique em **Segurança**.
3. Clique em **adicionar**e, em seguida, insira o endereço de email de saudação para um usuário ou grupo no AD do Azure.
   
    ![Adicionar administradores do servidor no SSMS](./media/analysis-services-server-admins/aas-manage-users-ssms.png)

## <a name="next-steps"></a>Próximas etapas 
[Autenticação e permissões de usuário](analysis-services-manage-users.md)  
[Gerenciar usuários e funções de banco de dados](analysis-services-database-users.md)  
[Controle de acesso baseado em função](../active-directory/role-based-access-control-what-is.md)  

