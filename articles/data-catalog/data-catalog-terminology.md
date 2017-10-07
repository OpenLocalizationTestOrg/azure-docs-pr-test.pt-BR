---
title: "terminologia do catálogo de dados de aaaAzure | Microsoft Docs"
description: "Este artigo fornece uma introdução tooconcepts e termos usados na documentação do Data Catalog do Azure."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 6fec74d9-4a3c-4b4b-88ba-cad5ad143331
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: b5f071db4f62c914d2c1cdef9aa686b18d5297d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-terminology"></a>Terminologia do Catálogo de Dados do Azure
## <a name="catalog"></a>Catálogo
Olá Data Catalog do Azure é um repositório de metadados com base em nuvem na qual os dados e fontes de dados pode ser registrados. Catálogo de saudação serve como um local de armazenamento central para metadados estruturais extraídos de fontes de dados e metadados descritivos adicionada por usuários.

## <a name="data-source"></a>Fonte de dados
Uma fonte de dados é um sistema ou um contêiner que gerencia ativos de dados. Exemplos incluem bancos de dados do SQL Server, bancos de dados Oracle, bancos de dados do SQL Server Analysis Services (tabela ou multidimensionais) e servidores do SQL Server Reporting Services.

## <a name="data-asset"></a>Ativos de dados
Ativos de dados são objetos contidos em fontes de dados que podem ser registrados com o catálogo de saudação. Exemplos incluem tabelas e exibições do SQL Server, tabelas e exibições do Oracle, medidas, dimensões e KPIs do SQL Server Analysis Services e relatórios do SQL Server Reporting Services.

## <a name="data-asset-location"></a>Local do ativo de dados
Olá, catálogo armazena Olá local de uma fonte de dados ou dados ativos, que podem ser usado tooconnect toohello usando um aplicativo cliente de origem. formato de saudação e os detalhes do local de saudação variam com base no tipo de fonte de dados de saudação. Por exemplo, uma tabela do SQL Server pode ser identificada por seu nome de quatro partes – nome do servidor, nome do banco de dados, nome do esquema, nome do objeto – enquanto um relatório do SQL Server Reporting Services pode ser identificado por sua URL.

## <a name="structural-metadata"></a>Metadados estruturais
Os metadados estruturais são extraídos de uma fonte de dados que descreve a estrutura de saudação de um ativo de dados de metadados de saudação. Isso inclui o local de ativos de saudação, seu nome de objeto e tipo e características adicionais de um tipo específico. Por exemplo, metadados estruturais de saudação para tabelas e modos de exibição incluem nomes de hello e tipos de dados colunas do objeto Olá.

## <a name="descriptive-metadata"></a>Metadados descritivos
Metadados descritivos são metadados que descreve a finalidade de saudação ou intenção de um ativo de dados. Normalmente metadados descritivos é adicionado por usuários do catálogo usando o portal do catálogo de dados do Azure hello, mas também podem ser extraído da fonte de dados Olá durante o registro. Por exemplo, ferramenta de registro do Data Catalog do Azure Olá extrairá as descrições da saudação propriedade Description no SQL Server Analysis Services e SQL Server Reporting Services e da saudação [ms_descriptiondapropriedadeestendida](https://technet.microsoft.com/library/ms190243.aspx)em bancos de dados do SQL Server, se essas propriedades foram populadas com valores.

## <a name="request-access"></a>Solicitar acesso
Metadados descritivo de um ativo de dados podem incluir informações sobre como toorequest acessar toohello dados ativos ou fonte de dados. Essas informações são apresentadas com o local de ativos de dados hello e podem incluir um ou mais dos Olá as opções a seguir:

* endereço de email de saudação do usuário hello ou equipe responsável por conceder a fonte de dados do access toohello.
* URL de saudação do hello documentado processo que os usuários devem seguir a fonte de dados de toohello toogain acesso.
* Olá URL de uma ferramenta de gerenciamento de identidade e acesso (como o Microsoft Identity Manager) que pode ser a fonte de dados usada toogain acesso toohello.
* Uma entrada de texto livre que descreve como os usuários podem obter a fonte de dados do access toohello.

## <a name="preview"></a>Visualização
Uma visualização no catálogo de dados do Azure é um instantâneo dos registros de too20 que podem ser extraídos da fonte de dados Olá durante o registro e armazenados no catálogo de saudação com hello metadados de ativo de dados. visualização Olá pode ajudar os usuários que descobrir um ativo de dados entender melhor a sua função e a finalidade. Em outras palavras, vejam os dados de exemplo pode ser mais valioso do que ver apenas nomes de coluna hello e tipos de dados.
Visualizações têm suporte apenas para tabelas e exibições e devem ser explicitamente selecionadas pelo usuário Olá durante o registro.

## <a name="data-profile"></a>Perfil de dados
Um perfil de dados no catálogo de dados do Azure é um instantâneo do nível de tabela e o nível de coluna de metadados sobre um ativo de dados registrados que pode ser extraído da fonte de dados Olá durante o registro e armazenado no catálogo de saudação com hello metadados de ativo de dados. Olá dados perfil pode ajudar os usuários que descobrir um ativo de dados entender melhor a sua função e a finalidade. Toopreviews semelhante, perfis de dados deve ser explicitamente selecionado pelo usuário Olá durante o registro.

> [!NOTE]
> Extrair um perfil de dados pode ser uma operação dispendiosa para grandes tabelas e exibições, e pode significativamente aumento Olá tooregister tempo necessário uma fonte de dados.
>
>

## <a name="user-perspective"></a>Perspectiva do usuário
No Catálogo de Dados do Azure, qualquer usuário pode fornecer metadados descritivos para um ativo de dados registrado. Cada usuário tem uma perspectiva distinta dados saudação e seu uso. Por exemplo, o administrador de saudação responsável por um servidor pode fornecer detalhes de saudação do seu contrato de nível de serviço (SLA) ou o backup do windows; um administrador de dados pode fornecer links toodocumentation para empresas Olá processa dá suporte a dados de saudação; e um analista pode fornecer uma descrição em termos de saudação que são mais relevantes analistas de tooother e que pode ser mais valiosos usuários toothose que precisam de toodiscover e entender dados saudação.

Todas essas perspectivas são inerentemente valiosos e no catálogo de dados do Azure cada usuário pode fornecer informações de saudação que é significativo toothem, embora todos os usuários podem usar dados informações toounderstand hello e sua finalidade.

## <a name="expert"></a>Especialista
Especialista é um usuário que foi identificado como tendo uma perspectiva de "especialista" informada para um ativo de dados. Qualquer usuário pode adicionar a si mesmo ou outro usuário como um especialista para um ativo. Sendo listado como um especialista não concede privilégios adicionais no catálogo de dados do Azure; Ele permite que os usuários tooeasily localizar essas perspectivas que são provavelmente toobe útil ao examinar metadados descritivos um ativo.

## <a name="owner"></a>Proprietário
Um proprietário é um usuário que tem privilégios adicionais para gerenciar um ativo de dados no Catálogo de Dados do Azure. Os usuários podem se apropriar de ativos de dados registrados e os proprietários podem adicionar outros usuários como co-proprietários. Para obter mais informações, consulte [como toomanage ativos de dados](data-catalog-how-to-manage.md)  

> [!NOTE]
> Propriedade e gerenciamento estão disponíveis apenas em Olá Standard Edition do Data Catalog do Azure.
>
>

## <a name="registration"></a>Registro
Registro é o ato de saudação de extrair metadados de ativo de dados de uma fonte de dados e copiando-o serviço de catálogo de dados do Azure toohello. Ativos de dados que foram registrados podem ser anotados e descobertos.

## <a name="see-also"></a>Confira também
* [O que é o Catálogo de Dados do Azure?](data-catalog-what-is-data-catalog.md) -Este artigo fornece uma visão geral do serviço de catálogo de dados do Azure hello, valor Olá fornece e cenários de saudação oferece suporte.
* [Introdução ao Data Catalog do Azure](data-catalog-get-started.md) -este artigo fornece um tutorial de ponta a ponta que mostra como toouse do Azure do catálogo de dados de descoberta de fonte de dados.  
