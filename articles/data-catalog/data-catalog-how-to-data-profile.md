---
title: fontes de dados de perfil aaaHow tooData
description: "Tooarticle como realce como perfis de dados no nível de tabela e coluna tooinclude ao registrar fontes de dados no Data Catalog do Azure e como os perfis de dados toouse toounderstand fontes de dados."
services: data-catalog
documentationcenter: 
author: spelluru
manager: NA
editor: 
tags: 
ms.assetid: 94a8274b-5c9c-4962-a4b1-2fed38a3d919
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: 12c9f38501cdaee903d0dcbbdd0b82395f35a187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="data-profile-data-sources"></a>Fontes de dados de perfil de dados
## <a name="introduction"></a>Introdução
**Catálogo de Dados do Microsoft Azure** é um serviço de nuvem totalmente gerenciado que atua como um sistema de registro e sistema de descoberta em fontes de dados da empresa. Em outras palavras, **Data Catalog do Azure** é tudo sobre pessoas ajudando descobrir, entender e usar fontes de dados e ajudar as organizações tooget mais valor de seus dados existentes. Quando uma fonte de dados é registrada com **Data Catalog do Azure**, seus metadados são copiados e indexados pelo serviço de saudação, mas o texto de saudação não termina existe.

Olá **criação de perfil de dados** recurso de **Data Catalog do Azure** examina Olá dados de fontes de dados com suporte no catálogo e coleta de estatísticas e informações sobre esses dados. É fácil tooinclude um perfil de seus ativos de dados. Quando você registra um ativo de dados, escolha **incluir dados de perfil** na ferramenta de registro de fonte de dados de saudação.

## <a name="what-is-data-profiling"></a>O que é a criação de perfil de dados
Perfil de dados examina Olá dados na fonte de dados hello está sendo registrado e coleta de estatísticas e informações sobre esses dados. Durante a descoberta de fonte de dados, essas estatísticas podem ajudar a determinar a adequação de saudação do hello dados toosolve um problema de negócios.

<!-- In [How toodiscover data sources](data-catalog-how-to-discover.md), you learn about **Azure Data Catalog's** extensive search capabilities including searching for data assets that have a profile. See [How tooinclude a data profile when registering a data source](#howto). -->

Olá seguintes fontes de dados oferecem suporte a criação de perfil de dados:

* Tabelas e exibições do SQL Server (incluindo o Banco de Dados SQL do Azure e o Azure SQL Data Warehouse)
* Tabelas e exibições do oracle
* Tabelas e exibições do Teradata
* Tabelas do Hive

A inclusão de perfis de dados ao registrar ativos de dados ajuda os usuários a responder a perguntas sobre fontes de dados, incluindo:

* Pode ser usado toosolve meu problema de negócios?
* Dados de saudação está em conformidade tooparticular padrões ou padrões?
* Quais são alguns dos anomalias Olá Olá da fonte de dados?
* Quais são os possíveis desafios de integração desses dados a meu aplicativo?

> [!NOTE]
> Você também pode adicionar documentação tooan ativo toodescribe como os dados podem ser integrados em um aplicativo. Consulte [como fontes de dados de toodocument](data-catalog-how-to-documentation.md).
>
>

<a name="howto"/>

## <a name="how-tooinclude-a-data-profile-when-registering-a-data-source"></a>Como tooinclude um dado de perfil ao registrar uma fonte de dados
É fácil tooinclude um perfil de sua fonte de dados. Quando você registra uma fonte de dados no hello **toobe objetos registrado** painel do registro da fonte de dados Olá ferramenta, escolher **incluir dados de perfil**.

![](media/data-catalog-data-profile/data-catalog-register-profile.png)

Saiba mais sobre toolearn como tooregister fontes de dados, consulte [como fontes de dados de tooregister](data-catalog-how-to-register.md) e [Introdução ao Data Catalog do Azure](data-catalog-get-started.md).

## <a name="filtering-on-data-assets-that-include-data-profiles"></a>Filtragem de ativos de dados que incluem perfis de dados
toodiscover os ativos de dados que incluem um perfil de dados, você pode incluir `has:tableDataProfiles` ou `has:columnsDataProfiles` como um dos seus termos de pesquisa.

> [!NOTE]
> Selecionando **incluir dados de perfil** nos dados Olá ferramenta de registro de origem inclui a tabela e informações de perfil de nível de coluna. No entanto, hello API de catálogo de dados permite toobe de ativos de dados registrado com apenas um conjunto de informações de perfil incluídas.
>
>

## <a name="viewing-data-profile-information"></a>Exibição de informações de perfil de dados
Depois de encontrar uma fonte de dados adequado com um perfil, você pode exibir detalhes do perfil de dados hello. dados de saudação tooview perfil, selecione um ativo de dados e escolha **perfil de dados** na janela portal do catálogo de dados hello.

![](media/data-catalog-data-profile/data-catalog-view.png)

Um perfil de dados no **Catálogo de Dados do Azure** mostra informações de perfil de tabela e coluna, incluindo:

### <a name="object-data-profile"></a>Perfil de dados de objeto
* Número de linhas
* Tamanho de tabela
* Quando Olá última atualização do objeto

### <a name="column-data-profile"></a>Perfil de dados de coluna
* Tipo de dados de coluna
* Número de valores distintos
* Número de linhas com valores NULL
* Desvio mínimo, máximo, médio e padrão para valores de colunas

## <a name="summary"></a>Resumo
Dados de criação de perfil fornece estatísticas e informações sobre registrados dados ativos toohelp determinar adequação Olá Olá dados toosolve problemas de negócios. Além de anotar e documentar fontes de dados, os perfis de dados podem dar aos usuários uma compreensão mais profunda dos dados.

## <a name="see-also"></a>Consulte também
* [Como tooregister fontes de dados](data-catalog-how-to-register.md)
* [Introdução ao Catálogo de Dados do Azure](data-catalog-get-started.md)
