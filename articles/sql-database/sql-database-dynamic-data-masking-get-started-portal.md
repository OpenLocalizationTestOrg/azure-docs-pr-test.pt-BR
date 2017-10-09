---
title: "Portal do Azure: máscara de dados dinâmicos do Banco de Dados SQL | Microsoft Docs"
description: "Como tooget iniciada com hello Portal do Azure de mascaramento de dados dinâmicos do banco de dados SQL"
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
ms.workload: data-services
ms.date: 11/22/2016
ms.author: ronitr; ronmat
ms.openlocfilehash: 5c5f74682a15d42eceb78c3ca0705401e1ac0ae7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-database-dynamic-data-masking-with-hello-azure-portal"></a>Introdução ao mascaramento com hello Azure Portal de dados dinâmicos do banco de dados SQL

Este tópico mostra como tooimplement [mascaramento de dados dinâmicos](sql-database-dynamic-data-masking-get-started.md) com hello portal do Azure. Você também pode implementar o mascaramento de dados dinâmicos usando [cmdlets do Azure SQL Database](https://msdn.microsoft.com/library/azure/mt574084.aspx) ou hello [API REST](https://msdn.microsoft.com/library/dn505719.aspx).


## <a name="set-up-dynamic-data-masking-for-your-database-using-hello-azure-portal"></a>Configurar o mascaramento de dados dinâmicos para seu banco de dados usando Olá Portal do Azure
1. Iniciar Olá Portal do Azure em [https://portal.azure.com](https://portal.azure.com).
2. Navegue toohello folha de configurações de banco de dados de saudação que inclui dados confidenciais hello, você deseja toomask.
3. Clique em Olá **mascaramento de dados dinâmicos** lado a lado que inicia Olá **mascaramento de dados dinâmicos** folha de configuração.
   
   * Como alternativa, você pode rolar para baixo toohello **operações** seção e clique em **mascaramento de dados dinâmicos**.
     
     ![Painel de navegação](./media/sql-database-dynamic-data-masking-get-started/4_ddm_settings_tile.png)<br/><br/>
4. Em Olá **mascaramento de dados dinâmicos** folha de configuração, você pode ver algumas colunas de banco de dados esse mecanismo de recomendações Olá foi sinalizada para mascaramento. Em ordem tooaccept recomendações hello, basta clicar em **Adicionar máscara** para uma ou mais colunas e uma máscara serão criados com base no tipo de padrão de saudação para essa coluna. Você pode alterar Olá função de máscara clicando na regra de mascaramento hello e editando Olá mascaramento campo tooa outro formato de sua escolha. Ser tooclick se **salvar** toosave suas configurações.
   
    ![Painel de navegação](./media/sql-database-dynamic-data-masking-get-started/5_ddm_recommendations.png)<br/><br/>
5. tooadd uma máscara para qualquer coluna em seu banco de dados, na parte superior de saudação do hello **mascaramento de dados dinâmicos** configuração folha, clique em **Adicionar máscara** tooopen Olá **Adicionar regra de mascaramento** folha de configuração
   
    ![Painel de navegação](./media/sql-database-dynamic-data-masking-get-started/6_ddm_add_mask.png)<br/><br/>
6. Selecione Olá **esquema**, **tabela** e **coluna** toodefine Olá designado campo será mascarado.
7. Escolha um **máscara de formato de campo** de lista de saudação de categorias de mascaramento de dados confidenciais.
   
    ![Painel de navegação](./media/sql-database-dynamic-data-masking-get-started/7_ddm_mask_field_format.png)<br/><br/>        
8. Clique em **salvar** nos dados Olá regra folha tooupdate Olá conjunto de regras de política de mascaramento de dados dinâmico Olá de mascaramento de mascaramento.
9. Os usuários do tipo hello SQL ou identidades do AAD que devem ser excluídas do mascaramento e possui dados confidenciais de toohello sem máscara de acesso. Deve ser uma lista de usuários separada por vírgulas. Observe que os usuários com privilégios de administrador sempre têm acesso toohello dados não mascarados original.
   
    ![Painel de navegação](./media/sql-database-dynamic-data-masking-get-started/8_ddm_excluded_users.png)
   
   > [!TIP]
   > toomake-Olá para camada de aplicativo pode exibir dados confidenciais para os usuários com privilégios de aplicativo, adicione Olá usuário do SQL ou o aplicativo de saudação do AAD identidade usa o banco de dados do tooquery hello. É altamente recomendável que essa lista contém um número mínimo de exposição a usuários privilegiados toominimize dados confidenciais hello.
   > 
   > 
10. Clique em **salvar** nos dados Olá configuração folha toosave Olá mascaramento novos ou atualizados política de mascaramento.


## <a name="next-steps"></a>Próximas etapas

* Para obter uma visão geral da máscara de dados dinâmicos, consulte [máscara de dados dinâmicos](sql-database-dynamic-data-masking-get-started.md).
* Você também pode implementar o mascaramento de dados dinâmicos usando [cmdlets do Azure SQL Database](https://msdn.microsoft.com/library/azure/mt574084.aspx) ou hello [API REST](https://msdn.microsoft.com/library/dn505719.aspx).
