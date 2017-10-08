---
title: aaaHow tooconnect toodata fontes | Microsoft Docs
description: "Tooarticle como realce como tooconnect toodata fontes descobertos no catálogo de dados do Azure."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 4e6b27a5-cf75-4012-b88c-333c1fe638e8
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 01d659510c8e67c1238ed488f4eebf511aab7217
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconnect-toodata-sources"></a>Como tooconnect toodata fontes
## <a name="introduction"></a>Introdução
**Catálogo de Dados do Microsoft Azure** é um serviço de nuvem totalmente gerenciado que atua como um sistema de registro e sistema de descoberta em fontes de dados da empresa. Em outras palavras, **Data Catalog do Azure** é tudo sobre pessoas ajudando descobrir, entender e usar fontes de dados e ajudar as organizações tooget mais valor de seus dados existentes. Um aspecto fundamental desse cenário está usando Olá fonte de dados – depois que um usuário descobre um dados e entenda a sua finalidade, Olá próxima etapa é a fonte de dados de toohello tooconnect tooput toouse seus dados.

## <a name="data-source-locations"></a>Locais de origem de dados
Durante o registro da fonte de dados, **Data Catalog do Azure** recebe metadados sobre a fonte de dados de saudação. Esses metadados incluem detalhes de saudação do local da fonte de dados hello. detalhes de saudação do local de saudação variam de fonte de toodata de fonte de dados, mas sempre conterá Olá tooconnect de informações necessárias. Por exemplo, local de saudação para uma tabela do SQL Server inclui nome de saudação do servidor, nome do banco de dados, nome do esquema e nome de tabela, enquanto local Olá para um relatório do SQL Server Reporting Services inclui o nome do servidor de saudação e relatório de toohello caminho Olá. Outros tipos de fonte de dados terá locais que refletem a estrutura de saudação e recursos do sistema de origem de saudação.

## <a name="integrated-client-tools"></a>Ferramentas de cliente integradas
Olá mais simples maneira tooconnect tooa fonte de dados é toouse hello "Abrir em...." menu de saudação **Data Catalog do Azure** portal. Esse menu exibe uma lista de opções de conexão toohello ativos de dados selecionada.
Ao usar o modo de exibição do bloco saudação padrão, este menu está disponível na Olá cada peça.

 ![Abrir uma tabela do SQL Server no Excel do bloco de ativos de dados Olá](./media/data-catalog-how-to-connect/data-catalog-how-to-connect1.png)

Ao usar o modo de exibição de lista hello, menu hello está disponível na barra de pesquisa de saudação na parte superior de saudação da janela portal hello.

 ![Abrir um relatório do SQL Server Reporting Services no Gerenciador de relatórios na barra de pesquisa Olá](./media/data-catalog-how-to-connect/data-catalog-how-to-connect2.png)

## <a name="supported-client-applications"></a>Aplicativos do Cliente com Suporte
Ao usar o hello "Abrir em...." menu para dados de fontes no portal do catálogo de dados do Azure hello, aplicativo de cliente correto hello deve ser instalado no computador do cliente de saudação.

| Abrir no aplicativo | Extensão de arquivo / protocolo | Versões do aplicativo com suporte |
| --- | --- | --- |
| Excel |.odc |Excel 2010 ou posterior |
| Excel (Top 1000) |.odc |Excel 2010 ou posterior |
| Power Query |.xlsx |Excel 2016 ou Excel 2010 ou Excel 2013 com hello Power Query para Excel em instalados |
| Power BI Desktop |.pbix |Power BI Desktop de julho de 2016 ou posterior |
| Ferramentas de dados do SQL Server |vsweb:// |Visual Studio 2013 Atualização 4 ou posterior com ferramentas do SQL Server instaladas |
| Gerenciador de Relatórios |http:// |Consulte [requisitos do navegador para os Serviços de Relatório do SQL Server](https://technet.microsoft.com/en-us/library/ms156511.aspx) |

## <a name="your-data-your-tools"></a>Seus dados, suas ferramentas
Opções de saudação disponíveis no menu de saudação serão dependem de tipo de saudação do ativo de dados selecionado no momento. Obviamente, nem todas as ferramentas possíveis serão incluídas no hello "aberto em...." menu, mas é a fonte de dados de toohello tooconnect ainda fácil usando qualquer ferramenta de cliente. Quando um ativo de dados está selecionado no hello **Data Catalog do Azure** portal, local completa da saudação é exibido no painel de propriedades de saudação.

 ![Informações de conexão para uma tabela do SQL Server](./media/data-catalog-how-to-connect/data-catalog-how-to-connect3.png)

informações de conexão Olá detalhes serão diferentes do tipo de fonte de toodata do tipo de fonte de dados, mas as informações de saudação incluídos no portal de saudação fornecerá tudo o que você precisa tooconnect toohello fonte de dados em qualquer ferramenta de cliente. Os usuários podem copiar detalhes de conexão Olá Olá fontes de dados que eles descobriram usando **Data Catalog do Azure**, permitindo que eles toowork com dados de saudação em sua ferramenta de sua escolha.

## <a name="connecting-and-data-source-permissions"></a>Permissões de conexão e de fonte de dados
Embora **Data Catalog do Azure** torna detectável, acesso a fontes de dados dados toohello em si permanecem sob o controle de saudação do proprietário da fonte de dados hello ou administrador. Descoberta de uma fonte de dados **Data Catalog do Azure** não conceder a um usuário qualquer permissões tooaccess Olá própria fonte de dados.

toomake facilitam para os usuários que descobrir um dados de origem, mas não tem permissão tooaccess seus dados, os usuários podem fornecer informações em Olá propriedade solicitar acesso quando anotar uma fonte de dados. As informações fornecidas aqui – incluindo o processo de toohello links ou ponto de contato para obter acesso à fonte de dados – são apresentadas junto com informações de local de fonte de dados de saudação no portal de saudação.

 ![Informações de conexão com as instruções de acesso de solicitação fornecidas](./media/data-catalog-how-to-connect/data-catalog-how-to-connect4.png)

## <a name="summary"></a>Resumo
Registrar uma fonte de dados com **Data Catalog do Azure** faz com que os dados detectável copiando metadados estruturais e descritivo da fonte de dados Olá para Olá serviço de catálogo. Depois que uma fonte de dados foi registrada e descoberta, usuários podem se conectar a fonte de dados toohello de saudação **Data Catalog do Azure** portal "Abrir em...." " ou usando suas ferramentas de dados à sua escolha.

## <a name="see-also"></a>Consulte também
* [Introdução ao Data Catalog do Azure](data-catalog-get-started.md) tutorial para obter detalhes passo a passo sobre como tooconnect toodata fontes.
