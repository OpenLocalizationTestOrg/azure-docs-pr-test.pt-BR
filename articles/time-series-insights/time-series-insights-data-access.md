---
title: "políticas de acesso aaaData no Azure Insights de série de tempo | Microsoft Docs"
description: "Neste tutorial, você aprenderá toomanage políticas de acesso de dados em informações da série de tempo"
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/01/2017
ms.author: omravi
ms.openlocfilehash: f286d26c8c5c851c523e9384760dc4b10711fa3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="grant-data-access-tooa-time-series-insights-environment-using-azure-portal"></a>Ambiente Grant dados access tooa Insights de série de tempo usando o portal do Azure

Os ambientes de Análise de Séries Temporais possuem dois tipos independentes de políticas de acesso:

* Políticas de acesso de gerenciamento
* Políticas de acesso de dados

Os dois tipos de políticas concedem às entidades de segurança (usuários e aplicativos) do Azure Active Directory várias permissões em um ambiente específico. Olá entidades (usuários e aplicativos) devem pertencer toohello active directory (ou "Locatário do Azure") associado à assinatura Olá que contém o ambiente de saudação.

Políticas de gerenciamento de acesso concederem a configuração de permissões de toohello relacionados de ambiente hello, como
*   Conjuntos de dados de referência de criação e exclusão de ambiente hello, fontes de evento, e
*   Gerenciamento de políticas de acesso de dados hello.

Políticas de acesso de dados conceder permissões em consultas de dados tooissue, manipulam dados de referência de ambiente hello e compartilham consultas salvas e perspectivas associadas ambiente hello.

dois tipos de saudação de políticas permitem separação clara entre gerenciamento de acesso à toohello do ambiente de saudação e acessar os dados toohello no ambiente de saudação. Por exemplo, é possível toosetup um ambiente que Olá proprietário/criador do ambiente de saudação é removido do acesso a dados hello. Bem como usuários e serviços que são permitidos dados tooread do ambiente Olá não pode ser concedido nenhuma configuração de toohello de acesso do ambiente de saudação.

## <a name="grant-data-access"></a>Conceder acesso a dados
Olá etapas a seguir mostram como acesso a dados de toogrant para uma entidade de segurança do usuário:

1.  Entrar toohello [portal do Azure](https://portal.azure.com).
2.  Clique em "Todos os recursos" no menu de saudação no lado esquerdo de saudação do hello portal do Azure.
3.  Selecione o seu ambiente de Análise de Séries Temporais.

  ![Gerenciar Olá fonte de informações da série de tempo - ambiente](media/data-access/getstarted-grant-data-access1.png)

4.  Selecione "Acesso ao plano de dados", clique em "Adicionar"

  ![Gerenciar a fonte de informações da série de tempo de saudação - adicionar](media/data-access/getstarted-grant-data-access2.png)

5.  Clique em “Selecionar usuário”.
6.  A pesquisa e selecione o usuário por email hello.
7.  Clique em "Selecionar" na folha "Selecionar usuário".

  ![Gerenciar Olá fonte de informações da série de tempo - selecione o usuário](media/data-access/getstarted-grant-data-access3.png)

8.  Clique em “Selecionar função”.
9.  Selecione "Colaborador" Se você deseja que os dados de referência do tooallow usuário toochange e compartilha consultas salvas e perspectivas com outros usuários do ambiente de saudação. Caso contrário, selecione dados de consulta de usuário "Leitor" tooallow no ambiente de saudação e salve pessoais consultas (não compartilhadas) no ambiente de saudação.
10. Clique em "Okey" na folha do hello "Selecionar função".

  ![Gerenciar Olá fonte de informações da série de tempo - função select](media/data-access/getstarted-grant-data-access4.png)

11. Clique em "Okey" na folha do hello "Selecionar a função de usuário".
12. Você deverá ver:

  ![Gerenciar Olá fonte de informações da série de tempo - resultados](media/data-access/getstarted-grant-data-access5.png)

## <a name="next-steps"></a>Próximas etapas

* [Criar uma fonte de eventos](time-series-insights-add-event-source.md)
* [Enviar eventos](time-series-insights-send-events.md) toohello origem do evento
* Exibir seu ambiente no [Portal de Análise de Séries Temporais](https://insights.timeseries.azure.com)
