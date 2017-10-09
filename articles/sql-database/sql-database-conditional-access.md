---
title: aaaConditional acesso - banco de dados do SQL Azure e o Data Warehouse | Documento do Microsoft
description: Saiba como tooconfigure de acesso condicional para o banco de dados do SQL Azure e o Data Warehouse.
services: sql-database
author: BYHAM
manager: jhubbard
ms.custom: security
ms.service: sql-database
ms.topic: article
ms.date: 06/07/2017
ms.author: rickbyh
ms.openlocfilehash: f49f4708c0f1b3cad1539d630c2efd919f8ece68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-mfa-with-azure-sql-database-and-data-warehouse"></a>Acesso Condicional (MFA) com o Banco de Dados SQL do Azure e o Data Warehouse  

O Banco de Dados SQL e o SQL Data Warehouse dão suporte ao Acesso Condicional da Microsoft. Olá mostram as etapas a seguir como tooenforce de banco de dados SQL tooconfigure uma política de acesso condicional.  

## <a name="prerequisites"></a>Pré-requisitos  
- Você deve configurar a autenticação do Active Directory do Azure de toosupport banco de dados SQL ou SQL Data Warehouse. Para obter etapas específicas, consulte [Configurar e gerenciar a autenticação do Azure Active Directory com o Banco de Dados SQL ou o SQL Data Warehouse](sql-database-aad-authentication-configure.md).  
- Quando a autenticação multifator é habilitada, você deve se conectar com a ferramenta com suporte, como Olá SSMS mais recentes. Para obter mais informações, consulte [Configurar a autenticação multifator do Banco de Dados SQL do Azure para o SQL Server Management Studio](sql-database-ssms-mfa-authentication-configure.md).  

## <a name="configure-ca-for-azure-sql-dbdw"></a>Configurar a AC para o BD SQL do Azure/DW  
1.  Entrar toohello Portal, selecione **Active Directory do Azure**e, em seguida, selecione **acesso condicional**. Para obter mais informações, consulte [Referência técnica do Acesso Condicional ao Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-conditional-access-technical-reference).  
  ![folha do acesso condicional](./media/sql-database-conditional-access/conditional-access-blade.png) 
     
2.  Em Olá **políticas de acesso condicional** folha, clique em **nova política**, forneça um nome e, em seguida, clique em **configurar regras de**.  
3.  Em **atribuições**, selecione **usuários e grupos**, verifique **selecionar usuários e grupos**e, em seguida, selecione usuário hello ou um grupo de acesso condicional. Clique em **selecione**e, em seguida, clique em **feito** tooaccept sua seleção.  
  ![selecionar usuários e grupos](./media/sql-database-conditional-access/select-users-and-groups.png)  

4.  Selecione **Aplicativos na nuvem** e clique em **Selecionar aplicativos**. Você verá todos os aplicativos disponíveis para o acesso condicional. Selecione **banco de dados do SQL Azure**, na parte inferior da saudação clique **selecione**e, em seguida, clique em **feito**.  
  ![selecionar Banco de Dados SQL](./media/sql-database-conditional-access/select-sql-database.png)  
  Se você não encontrar **banco de dados do SQL Azure** listado no hello terceira captura de tela a seguir, conclua Olá etapas a seguir:   
  - Entrar na instância do Azure SQL DB/DW tooyour usando o SSMS com uma conta de administrador do AAD.  
  - Execute `CREATE USER [user@yourtenant.com] FROM EXTERNAL PROVIDER`.  
  - Entre no tooAAD e verifique se o banco de dados do SQL Azure e o Data Warehouse estão listados em aplicativos de saudação em seu AAD.  

5.  Selecione **controles de acesso**, selecione **Grant**e, em seguida, verificar a diretiva de saudação tooapply desejado. Para este exemplo, selecionamos **Exigir autenticação multifator**.  
  ![selecionar conceder acesso](./media/sql-database-conditional-access/grant-access.png)  

## <a name="summary"></a>Resumo  
aplicativo Hello selecionada (banco de dados do SQL Azure) permitindo tooconnect tooAzure DB/DW do SQL usando o Azure AD Premium, agora impõe a política de acesso condicional Olá selecionado, **necessária a autenticação multifator.**  
Em caso de dúvidas sobre o Banco de Dados SQL do Azure e o Data Warehouse com relação à autenticação multifator, contate MFAforSQLDB@microsoft.com.  

## <a name="next-steps"></a>Próximas etapas  

Para obter um tutorial, consulte [Proteger o Banco de Dados SQL do Azure](sql-database-security-tutorial.md).
