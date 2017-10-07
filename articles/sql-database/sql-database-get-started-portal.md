---
title: 'Portal do Azure: Criar um banco de dados SQL | Microsoft Docs'
description: "Saiba como toocreate um servidor lógico do banco de dados SQL, regra de firewall de nível de servidor e bancos de dados em Olá portal do Azure. Você também aprenderá tooquery em um banco de dados do SQL Azure usando Olá portal do Azure."
keywords: tutorial do banco de dados SQL, criar um banco de dados SQL
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: aeb8c4c3-6ae2-45f7-b2c3-fa13e3752eed
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: portal
ms.devlang: na
ms.topic: hero-article
ms.date: 05/30/2017
ms.author: carlrab
ms.openlocfilehash: d30352d834f2007e0b6b3eabfc3c108c61479b22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-sql-database-in-hello-azure-portal"></a>Criar um banco de dados do SQL Azure no portal do Azure de saudação

Este tutorial de início rápido orienta como toocreate um SQL banco de dados no Azure. Banco de dados do SQL Azure é um "banco de dados-como-um-serviço" que permite a você toorun escala altamente disponíveis do SQL Server bancos de dados e na nuvem de saudação da oferta. Esse início rápido mostra como tooget iniciado com a criação de um banco de dados SQL usando Olá portal do Azure.

Se você não tiver uma assinatura do Azure, crie uma conta [gratuita](https://azure.microsoft.com/free/) antes de começar.

## <a name="log-in-toohello-azure-portal"></a>Faça logon no toohello portal do Azure

Faça logon no toohello [portal do Azure](https://portal.azure.com/).

## <a name="create-a-sql-database"></a>Criar um banco de dados SQL

Um banco de dados SQL do Azure é criado com um conjunto definido de [recursos de computação e armazenamento](sql-database-service-tiers.md). banco de dados de saudação é criado em um [grupo de recursos do Azure](../azure-resource-manager/resource-group-overview.md) e, em um [servidor lógico do banco de dados do Azure SQL](sql-database-features.md). 

Siga estas etapas toocreate um banco de dados SQL que contém dados de exemplo Adventure Works LT hello. 

1. Clique em Olá **novo** botão localizado no canto superior esquerdo de saudação do hello portal do Azure.

2. Selecione **bancos de dados** de saudação **novo** página e selecione **banco de dados SQL** de saudação **bancos de dados** página.

   ![criar database-1](./media/sql-database-get-started-portal/create-database-1.png)

3. Preencha formulário de banco de dados SQL Olá com hello seguintes informações, conforme mostrado na saudação anterior imagem:   

   | Configuração       | Valor sugerido | Descrição | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nome do banco de dados** | mySampleDatabase | Para ver os nomes do banco de dados válidos, consulte [Identificadores do Banco de Dados](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers). | 
   | **Assinatura** | Sua assinatura  | Para obter detalhes sobre suas assinaturas, consulte [Assinaturas](https://account.windowsazure.com/Subscriptions). |
   | **Grupo de recursos**  | myResourceGroup | Para ver os nomes do grupo de recursos válidos, consulte [Regras e restrições de nomenclatura](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions). |
   | **Fonte da origem** | Exemplo (AdventureWorksLT) | Carrega Olá AdventureWorksLT esquema e os dados no novo banco de dados |

   > [!IMPORTANT]
   > Você deve selecionar o banco de dados de exemplo de hello neste formulário porque ela é usada no restante da saudação deste início rápido.
   > 

4. Em **servidor**, clique em **definir as configurações necessárias** e preencha Olá formulário do SQL server (servidor lógico) com hello seguintes informações, conforme mostrado na Olá a imagem a seguir:   

   | Configuração       | Valor sugerido | Descrição | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nome do servidor** | Qualquer nome exclusivo globalmente | Para ver os nomes do servidor válidos, consulte [Regras e restrições de nomenclatura](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions). | 
   | **Logon de administrador do servidor** | Qualquer nome válido | Para ver os nomes de logon válidos, consulte [Identificadores do Banco de Dados](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers). |
   | **Senha** | Qualquer senha válida | Sua senha deve ter pelo menos 8 caracteres e deve conter caracteres de três das Olá categorias a seguir: caracteres em letras maiusculas, letras minúsculas, números e caracteres não alfanuméricos e. |
   | **Assinatura** | Sua assinatura | Para obter detalhes sobre suas assinaturas, consulte [Assinaturas](https://account.windowsazure.com/Subscriptions). |
   | **Grupo de recursos** | myResourceGroup | Para ver os nomes do grupo de recursos válidos, consulte [Regras e restrições de nomenclatura](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions). |
   | **Localidade** | Qualquer local válido | Para obter mais informações sobre as regiões, consulte [Regiões do Azure](https://azure.microsoft.com/regions/). |

   > [!IMPORTANT]
   > Olá administrador logon e senha que você especificar aqui são toolog necessária no servidor de toohello e seus bancos de dados mais tarde nesse início rápido. Lembre-se ou registre essas informações para o uso posterior. 
   >  

   ![criar database-server](./media/sql-database-get-started-portal/create-database-server.png)

5. Quando tiver preenchido o formulário de saudação, clique em **selecione**.

6. Clique em **preço** toospecify Olá desempenho e da camada de nível de serviço para o novo banco de dados. Use Olá controle deslizante tooselect **20 DTUs** e **250** GB de armazenamento. Para obter mais informações sobre as DTUs, consulte [O que é DTU?](sql-database-what-is-a-dtu.md).

   ![Criar database-s1](./media/sql-database-get-started-portal/create-database-s1.png)

7. Depois de quantidade de saudação selecionado de DTUs, clique em **aplicar**.  

8. Agora que você concluiu o formulário de banco de dados SQL hello, clique em **criar** banco de dados do tooprovision hello. O provisionamento demora alguns minutos. 

9. Na barra de ferramentas hello, clique em **notificações** toomonitor processo de implantação de saudação.

   ![notificação](./media/sql-database-get-started-portal/notification.png)

## <a name="create-a-server-level-firewall-rule"></a>Criar uma regra de firewall no nível de servidor

Olá serviço de banco de dados SQL cria um firewall em Olá nível de servidor que impede que aplicativos externos e ferramentas de conexão de servidor toohello ou bancos de dados no servidor de saudação, a menos que uma regra de firewall é criada um firewall de saudação tooopen para endereços IP específicos. Siga estas etapas toocreate um [regra de firewall de nível de servidor de banco de dados SQL](sql-database-firewall-configure.md) para o endereço IP do cliente e habilitar a conectividade externa através do firewall do banco de dados SQL Olá para seu endereço de IP. 

> [!NOTE]
> O Banco de Dados SQL se comunica pela porta 1433. Se você estiver tentando tooconnect de dentro de uma rede corporativa, o tráfego de saída pela porta 1433 talvez não consigam pelo firewall da rede. Nesse caso, você não pode conectar o servidor de banco de dados do Azure SQL tooyour, a menos que o departamento de TI abre a porta 1433.
>

1. Após a conclusão da implantação hello, clique em **bancos de dados SQL** no menu esquerdo hello e clique **mySampleDatabase** em Olá **bancos de dados SQL** página. Olá, página de visão geral para o banco de dados abre, mostrando a você Olá totalmente qualificado nome do servidor (como **mynewserver20170313.database.windows.net**) e fornece opções de configuração adicional. Copie esse nome totalmente qualificado do servidor para um uso posterior.

   > [!IMPORTANT]
   > É necessário que este servidor de tooyour de tooconnect de nome totalmente qualificado do servidor e seus bancos de dados em início rápido subsequente.
   > 

   ![nome do servidor](./media/sql-database-connect-query-dotnet/server-name.png) 

2. Clique em **definir o firewall do servidor** na barra de ferramentas Olá conforme mostrado na imagem anterior hello. Olá **configurações de Firewall** página para o servidor de banco de dados SQL Olá é aberta. 

   ![regra de firewall do servidor](./media/sql-database-get-started-portal/server-firewall-rule.png) 

3. Clique em **Adicionar IP do cliente** em Olá barra de ferramentas tooadd seu atual endereço IP tooa nova regra de firewall. Uma regra de firewall pode abrir a porta 1433 para um único endereço IP ou um intervalo de endereços IP.

4. Clique em **Salvar**. Uma regra de firewall de nível de servidor é criada para seu endereço IP atual, abrir a porta 1433 no servidor lógico hello.

   ![definir regra de firewall do servidor](./media/sql-database-get-started-portal/server-firewall-rule-set.png) 

4. Clique em **Okey** e, em seguida, feche Olá **configurações de Firewall** página.

Agora você pode conectar o servidor de banco de dados SQL toohello e seus bancos de dados usando o SQL Server Management Studio ou outra ferramenta de sua escolha usando esse endereço IP usando a conta de administrador de servidor de saudação criada anteriormente.

> [!IMPORTANT]
> Por padrão, o acesso através do firewall do banco de dados SQL hello está habilitado para todos os serviços do Azure. Clique em **OFF** em toodisable essa página para todos os serviços do Azure.
>

## <a name="query-hello-sql-database"></a>Banco de dados do SQL consulta Olá

Agora que você criou um banco de dados de exemplo no Azure, vamos usar a ferramenta de consulta interna hello dentro Olá tooconfirm portal do Azure que você pode se conectar a dados de saudação de banco de dados e consulta toohello. 

1. Na página de banco de dados SQL Olá para seu banco de dados, clique em **ferramentas** na barra de ferramentas de saudação. Olá **ferramentas** página será aberta.

   ![menu ferramentas](./media/sql-database-get-started-portal/tools-menu.png) 

2. Clique em **editor de consultas (visualização)**, clique em Olá **visualizar termos** caixa de seleção e, em seguida, clique em **Okey**. Abre a página do editor de consulta de saudação.

3. Clique em **Login** e, em seguida, quando solicitado, selecione **autenticação do SQL server** e forneça logon de administrador do servidor de saudação e a senha que você criou anteriormente.

   ![logon](./media/sql-database-get-started-portal/login.png) 

4. Clique em **Okey** toolog no.

5. Depois que você está autenticado, digite o seguinte Olá consulta no painel do editor de consultas de saudação.

   ```sql
   SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
   FROM SalesLT.ProductCategory pc
   JOIN SalesLT.Product p
   ON pc.productcategoryid = p.productcategoryid;
   ```

6. Clique em **executar** e analise os resultados da consulta Olá em Olá **resultados** painel.

   ![resultados do editor de consultas](./media/sql-database-get-started-portal/query-editor-results.png)

7. Olá fechar **editor de consultas** página e hello **ferramentas** página.

## <a name="clean-up-resources"></a>Limpar recursos

Se você não precisa desses recursos para outro/tutorial de início rápido (consulte [próximas etapas](#next-steps)), você pode excluí-los, Olá seguinte:


1. No menu esquerdo de saudação do hello portal do Azure, clique em **grupos de recursos** e, em seguida, clique em **myResourceGroup**. 
2. Na sua página de grupo de recursos, clique em **excluir**, tipo **myResourceGroup** Olá caixa de texto e, em seguida, clique em **excluir**.

## <a name="next-steps"></a>Próximas etapas

Agora que você tem um banco de dados, você pode se conectar e consultar usando suas ferramentas favoritas. Saiba mais escolhendo sua ferramenta abaixo:

- [SQL Server Management Studio](sql-database-connect-query-ssms.md)
- [Visual Studio Code](sql-database-connect-query-vscode.md)
- [.NET](sql-database-connect-query-dotnet.md)
- [PHP](sql-database-connect-query-php.md)
- [Node.js](sql-database-connect-query-nodejs.md)
- [Java](sql-database-connect-query-java.md)
- [Python](sql-database-connect-query-python.md)
- [Ruby](sql-database-connect-query-ruby.md)
