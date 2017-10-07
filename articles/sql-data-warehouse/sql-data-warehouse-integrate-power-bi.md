---
title: aaaUse Power BI com o SQL Data Warehouse | Microsoft Docs
description: "Dicas para usar o Power BI com o SQL Data Warehouse do Azure para desenvolvimento de soluções."
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: b12bee87-2268-40c2-81bf-ab27588b32e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: a3a347493d07af6824a561567f05894cfe3c0471
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-power-bi-with-sql-data-warehouse"></a>Usar o Power BI com o SQL Data Warehouse
Como com o banco de dados SQL Azure, a conexão direta do SQL Data Warehouse permite que usuário tooleverage poderoso lógico aplicação juntamente com recursos analíticos de saudação do Power BI.  Com conexão direta, consultas são enviadas tooyour back Azure SQL Data Warehouse em tempo real conforme você explora dados hello.  Isso, combinado com escala de saudação do SQL Data Warehouse, permite que os usuários de relatórios dinâmicos toocreate em minutos em terabytes de dados.  Além disso, a introdução de saudação do hello aberto no botão Power BI permite que os usuários toodirectly conectar o Power BI tootheir SQL Data Warehouse sem coletar informações de outras partes do Azure.

Ao usar a Conexão Direta:

* Especifique o nome totalmente qualificado do servidor de saudação durante a conexão (consulte abaixo para obter mais detalhes)
* Certifique-se de que as regras de firewall para o banco de dados de saudação são configuradas muito "permitem acesso tooAzure serviços".
* Toda ação, como selecionar uma coluna ou adicionar um filtro, consultará diretamente data warehouse de saudação
* Blocos são atualizados aproximadamente a cada 15 minutos (a atualização não é necessário toobe agendado)
* Perguntas e respostas não estão disponíveis para conjuntos de dados de Conexão Direta
* As alterações no esquema não são selecionadas automaticamente
* Todas as consultas de Conexão Direta atingirão o tempo limite após 2 minutos

Essas restrições e observações podem mudar conforme continuamos tooimprove Olá experiências ao mesmo tempo. Olá etapas tooconnect são detalhadas abaixo.  

## <a name="using-hello-open-in-power-bi-button"></a>Usando o botão 'Abrir no Power BI' hello
Olá toomove de maneira mais fácil entre o SQL Data Warehouse e o Power BI é com hello aberto no botão Power BI. Esse botão permite tooseamlessly começar a criar novos painéis no Power BI.  

1. tooget iniciado navegue tooyour instância de SQL Data Warehouse em Olá Portal clássico do Azure.
2. Clique o botão 'Abrir no Power BI' hello.
3. Se não for capaz de toosign no diretamente, ou se você não tiver uma conta do Power BI, você precisará toosign-in.  
4. Você será direcionado pré-preenchidos toohello página de conexão do SQL Data Warehouse, com informações de saudação do Data Warehouse do SQL.
5. Depois de inserir suas credenciais, você será totalmente conectada tooyour SQL Data Warehouse.

## <a name="connecting-through-hello-power-bi-portal"></a>Conectando por meio do portal do Power BI Olá
Saudação de toousing de adição aberto no botão Power BI, os usuários também podem conectar tootheir SQL Data Warehouse por meio de saudação Portal do Power BI.

1. Clique em 'Obter dados' na parte inferior de Olá Olá do painel de navegação.
2. Selecione 'Bancos de dados'.
3. Uma vez na página de bancos de dados hello, selecione 'Azure SQL Data Warehouse' e, em seguida, clique em 'Conectar'.
4. Insira as informações de conexão necessárias hello.  Seu nome de servidor e o nome do banco de dados podem ser encontrados no hello Portal do Azure.
5. Você será direcionado volta toohello o página principal do Power BI e depois que a conexão é feita uma nova entrada em 'Conjuntos de dados' aparecerá com o nome de saudação da sua instância.  
6. Você pode clicar em Olá novo conjunto de dados tooexplore todas as tabelas de saudação e exibições no banco de dados. Selecionando uma coluna enviará uma fonte de back toohello consulta, criando dinamicamente seu visual. Esses elementos visuais podem ser salvas em um novo relatório e fixados de volta tooyour painel.

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop/
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integration/

<!--MSDN references-->

<!--Other Web references-->
