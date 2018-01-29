---
title: "Portal do Azure: máscara de dados dinâmicos do Banco de Dados SQL | Microsoft Docs"
description: "Como começar a usar a máscara de dados dinâmicos do Banco de Dados SQL no portal do Azure"
services: sql-database
documentationcenter: 
author: ronitr
manager: jhubbard
editor: 
ms.assetid: "2"
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: Inactive
ms.date: 11/22/2016
ms.author: ronitr
ms.openlocfilehash: 20d344bc6ae971012bd181d14d130432263a3b76
ms.sourcegitcommit: fa28ca091317eba4e55cef17766e72475bdd4c96
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="get-started-with-sql-database-dynamic-data-masking-with-the-azure-portal"></a>Introdução à máscara de dados dinâmicos do Banco de Dados SQL com o portal do Azure

Este artigo mostra como implementar a [máscara de dados dinâmicos](sql-database-dynamic-data-masking-get-started.md) com o Portal do Azure. Você também pode implementar a máscara de dados dinâmicos usando [cmdlets de Banco de Dados SQL do Azure](https://msdn.microsoft.com/library/azure/mt574084.aspx) ou a [API REST](https://msdn.microsoft.com/library/dn505719.aspx).


## <a name="set-up-dynamic-data-masking-for-your-database-using-the-azure-portal"></a>Configurar o mascaramento de dados dinâmicos para o banco de dados usando o portal do Azure
1. Inicie o Portal do Azure em [https://portal.azure.com](https://portal.azure.com).
2. Navegue até a página de configurações do banco de dados que contém os dados confidenciais que você deseja mascarar.
3. Clique no bloco **Máscara de Dados Dinâmicos** que inicia a página de configuração **Máscara de Dados Dinâmicos**.
   
   * Como alternativa, role para baixo até a seção **Operações** e clique em **Máscara de Dados Dinâmicos**.
     
     ![Painel de navegação](./media/sql-database-dynamic-data-masking-get-started/4_ddm_settings_tile.png)<br/><br/>
4. Na página de configuração **Máscara de Dados Dinâmicos**, você poderá ver algumas colunas de banco de dados que o mecanismo de recomendações sinalizou para mascaramento. Para aceitar as recomendações, basta clicar em **Adicionar Máscara** para uma ou mais colunas e uma máscara será criada com base no tipo padrão para essa coluna. Você pode alterar a função de mascaramento clicando na regra de mascaramento e editando o formato do campo de mascaramento para um formato diferente à sua escolha. Clique em **Salvar** para salvar suas configurações.
   
    ![Painel de navegação](./media/sql-database-dynamic-data-masking-get-started/5_ddm_recommendations.png)<br/><br/>
5. Para adicionar uma máscara a uma coluna do banco de dados, na parte superior da página de configuração **Máscara de Dados Dinâmicos**, clique em **Adicionar Máscara** para abrir a página de configuração **Adicionar Regra de Mascaramento**.
   
    ![Painel de navegação](./media/sql-database-dynamic-data-masking-get-started/6_ddm_add_mask.png)<br/><br/>
6. Selecione o **Esquema**, a **Tabela** e a **Coluna** para definir o campo designado para o mascaramento.
7. Escolha um **Formato do Campo de Máscara** na lista de categorias de mascaramento dos dados confidenciais.
   
    ![Painel de navegação](./media/sql-database-dynamic-data-masking-get-started/7_ddm_mask_field_format.png)<br/><br/>        
8. Clique em **Salvar** na página da regra de mascaramento de dados para atualizar o conjunto de regras de mascaramento na política de máscara de dados dinâmicos.
9. Digite os usuários do SQL ou as identidades AAD que devem ser excluídos da máscara e têm acesso aos dados confidenciais sem máscara. Deve ser uma lista de usuários separada por vírgulas. Os usuários com privilégios de administrador sempre terão acesso aos dados sem máscara originais.
   
    ![Painel de navegação](./media/sql-database-dynamic-data-masking-get-started/8_ddm_excluded_users.png)
   
   > [!TIP]
   > Para fazer isso de forma que a camada de aplicativo possa exibir dados confidenciais para usuários com privilégios de aplicativo, adicione o usuário do SQL ou a identidade do AAD usados pelo aplicativo para consultar o banco de dados. É altamente recomendável que essa lista contenha um número mínimo de usuários privilegiados para minimizar a exposição de dados confidenciais.
   > 
   > 
10. Clique em **Salvar** na página de configuração de mascaramento de dados para salvar a política de mascaramento nova ou atualizada.


## <a name="next-steps"></a>Próximas etapas

* Para obter uma visão geral da máscara de dados dinâmicos, consulte [máscara de dados dinâmicos](sql-database-dynamic-data-masking-get-started.md).
* Você também pode implementar a máscara de dados dinâmicos usando [cmdlets de Banco de Dados SQL do Azure](https://msdn.microsoft.com/library/azure/mt574084.aspx) ou a [API REST](https://msdn.microsoft.com/library/dn505719.aspx).
