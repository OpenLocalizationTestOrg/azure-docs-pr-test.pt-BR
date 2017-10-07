---
title: "fontes de dados aaaRegister no catálogo de dados do Azure | Microsoft Docs"
description: "Este artigo destaca como tooregister fontes de dados no catálogo de dados do Azure, inclusive campos de metadados Olá extraído durante o registro."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: bab89906-186f-4d35-9ffd-61b1d903905d
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: efc8a852ddc9fb4bbacc7b0280477bd47814936f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="register-data-sources-in-azure-data-catalog"></a>Registrar fontes de dados no Catálogo de Dados do Azure
## <a name="introduction"></a>Introdução
O Catálogo de Dados do Azure é um serviço de nuvem totalmente gerenciado que atua como um sistema de registro e descoberta para fontes de dados da empresa. Em outras palavras, o Catálogo de Dados ajuda as pessoas a descobrir, entender e usar fontes de dados, além de ajudar as organizações a obterem mais valor dos seus dados existentes. Olá a primeira etapa toomaking uma fonte de dados podem ser descobertos por meio do catálogo de dados tooregister de é essa fonte de dados.

## <a name="register-data-sources"></a>Registrar fontes de dados
Registro é o processo de saudação de extração de metadados de fonte de dados de saudação e copiar esse toohello dados serviço Catálogo de dados. Olá dados permanecem em que ela reside atualmente e permanece em controle de saudação de administradores de saudação e políticas do sistema atual hello.

uma fonte de dados de tooregister Olá a seguir:
1. No portal do catálogo de dados do Azure hello, inicie a ferramenta de registro de fonte de dados do hello catálogo de dados. 
2. Entrar com sua conta corporativa ou de Estudante com hello mesmo credenciais do Active Directory do Azure que você use toosign no portal de toohello.
3. Selecione a fonte de dados de saudação tooregister desejado.

Para obter mais detalhes passo a passo, consulte Olá [Introdução ao Data Catalog do Azure](data-catalog-get-started.md) tutorial.

Após ter registrado a fonte de dados hello, catálogo Olá rastreia o local e seus metadados de índices. Os usuários podem pesquisar, procurar, descobrir a fonte de dados de saudação e, em seguida, usar tooit de tooconnect seu local usando o aplicativo hello ou ferramenta de sua escolha.

## <a name="supported-data-sources"></a>Fontes de dados com suporte
Para obter uma lista de fontes de dados com suporte no momento, consulte [DSR do Catálogo de Dados](data-catalog-dsr.md).

## <a name="structural-metadata"></a>Metadados estruturais
Ao registrar uma fonte de dados, ferramenta de registro de saudação extrai informações sobre estrutura de saudação dos objetos Olá selecionados. Essas informações são metadados estruturais tooas referenciada.

Para todos os objetos, esses metadados estruturais incluem o local do objeto hello, para que os usuários descobrir Olá dados podem usar esse objeto de informações de toohello tooconnect em ferramentas de cliente de saudação de sua escolha. Outros metadados estruturais incluem o tipo e o nome do objeto e o nome de coluna/atributo e tipo de dados.

## <a name="descriptive-metadata"></a>Metadados descritivos
Além disso toohello core metadados estruturais que são extraídos da fonte de dados Olá, ferramenta de registro de fonte de dados Olá extrai metadados descritivos. Para SQL Server Analysis Services e SQL Server Reporting Services, esses metadados são obtidos do propriedades da descrição Olá expostas por esses serviços. Para o SQL Server, os valores fornecidos usando Olá ms\_descrição de propriedade estendida é extraída. Banco de dados Oracle, Olá fonte de dados registro ferramenta extrai Olá coluna COMMENTS da Olá todos\_guia\_exibir comentários.

Em adição toohello descritivo metadados são extraídos da fonte de dados hello, os usuários podem inserir metadados descritivos usando a ferramenta de registro de fonte de dados de saudação. Os usuários podem adicionar marcas, e eles podem identificar especialistas para objetos hello está sendo registrados. Todos esses metadados descritivos são copiados toohello serviço de catálogo de dados junto com os metadados estruturais hello.

## <a name="include-previews"></a>Incluir versões prévias
Por padrão, apenas os metadados são extraídos de fontes de dados e copiado toohello serviço Catálogo de dados, mas Noções básicas sobre que uma fonte de dados geralmente é mais fácil quando você pode exibir um exemplo dos dados Olá contém.

Usando a ferramenta de registro de saudação fonte de dados do catálogo de dados, você pode incluir uma visualização de instantâneo de dados de saudação em cada tabela e o modo de exibição que está registrado. Se você escolher tooinclude visualizações durante o registro, a ferramenta de registro de saudação inclui too20 registros de cada tabela e exibição. Esse instantâneo é copiado, em seguida, catálogo de toohello junto com os metadados estruturais e descritivo hello.

> [!NOTE]
> Tabelas largas com um grande número de colunas podem ter menos de 20 registros incluídos na sua versão prévia.
>
>

## <a name="include-data-profiles"></a>Incluir perfis de dados
Assim como visualizações incluindo podem fornecer contexto importante para os usuários que pesquisar fontes de dados no catálogo de dados, incluindo um perfil de dados pode tornar mais fácil fontes de dados toounderstand descoberto.

Usando a ferramenta de registro de saudação fonte de dados do catálogo de dados, você pode incluir um perfil de dados para cada tabela e o modo de exibição que está registrado. Se você escolher um perfil de dados tooinclude durante o registro, a ferramenta de registro de Olá inclui estatísticas agregadas sobre dados de saudação em cada tabela e exibição, incluindo:

* número de saudação de linhas e o tamanho dos dados de saudação no objeto de saudação.
* Data de saudação atualização mais recente de saudação de dados saudação e esquema de objeto Olá.
* número de saudação de registros nulo e valores distintos para colunas.
* valores Hello de mínimo, máximo, média e desvio padrão para colunas.

Essas estatísticas são copiadas catálogo toohello junto com os metadados estruturais e descritivo hello.

> [!NOTE]
> As colunas de data e texto não incluem estatísticas de desvio padrão ou média no seu perfil de dados.
>
>

## <a name="update-registrations"></a>Atualizar os registros
Registrar uma fonte de dados torna possível descobri-los no catálogo de dados quando você usa metadados hello e visualização opcional extraído durante o registro. Se precisar de fonte de dados Olá toobe atualizado no catálogo de saudação (por exemplo, se Olá esquema de um objeto foi alterado, originalmente excluídas de tabelas devem ser incluídas ou tooupdate Olá dados que está incluído na visualização de saudação), ferramenta de registro de fonte de dados de saudação pode ser executado novamente.

O novo registro de uma fonte de dados já registrada executa uma operação "upsert" de mesclagem: objetos existentes são atualizados e os novos objetos são criados. Todos os metadados fornecidos por usuários através do portal do catálogo de dados de saudação são mantidas.

## <a name="summary"></a>Resumo
Pois ele copia os metadados estruturais e descritivo de um serviço de catálogo de toohello de fonte de dados, registrar a fonte de dados de saudação no catálogo de dados torna Olá dados mais fácil toodiscover e entender. Depois de registrar a fonte de dados hello, você pode anotar, gerenciar e descobri-lo usando o portal do catálogo de dados de saudação.

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre o registro de fontes de dados, consulte Olá [Introdução ao Data Catalog do Azure](data-catalog-get-started.md) tutorial.
