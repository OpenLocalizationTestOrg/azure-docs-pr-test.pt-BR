---
title: "conceitos de desenvolvedor do catálogo de aaaData | Microsoft Docs"
description: "Introdução toohello principais conceitos do modelo conceitual do catálogo de dados do Azure, como exposto por meio de Olá API REST do catálogo."
services: data-catalog
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
tags: 
ms.assetid: 89de9137-a0a4-40d1-9f8d-625acad31619
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: d0b1628ff6c31458cb650efef852244f0c139b1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-developer-concepts"></a>Conceitos de desenvolvedor do Catálogo de Dados do Azure
O **Catálogo de Dados do Microsoft Azure** é um serviço de nuvem totalmente gerenciado que fornece recursos para descoberta de fonte de dados e metadados de fonte de dados de crowdsourcing. Os desenvolvedores podem usar o serviço de saudação por meio de suas APIs REST. Entender os conceitos de saudação implementados no serviço de saudação é importante para os desenvolvedores toosuccessfully integrar **Data Catalog do Azure**.

## <a name="key-concepts"></a>Principais conceitos
Olá **Data Catalog do Azure** modelo conceitual baseia-se em quatro conceitos principais: Olá **catálogo**, **usuários**, **ativos**e **Anotações**.

![conceito][1]

*Figura 1 - Modelo conceitual simplificado do Catálogo de Dados do Azure*

### <a name="catalog"></a>Catálogo
Um **catálogo** é o contêiner de nível superior Olá para todos Olá metadados armazena uma organização. Há um **Catálogo** alocado por conta do Azure. Catálogos são empatado tooan assinatura do Azure, mas somente um **catálogo** podem ser criados para qualquer conta do Azure determinada, mesmo que uma conta pode ter várias assinaturas.

Um catálogo contém **Usuários** e **Ativos**.

### <a name="users"></a>Usuários
Os usuários são entidades de segurança que têm permissões tooperform ações (Pesquisar catálogo hello, adicionar, editar ou remover itens, etc.) no catálogo de saudação.

Há várias funções de que um usuário pode ter. Para obter informações sobre funções, consulte a seção de saudação funções e autorização.

Usuários individuais e grupos de segurança podem ser adicionados.

O Catálogo de Dados do Azure usa o Active Directory do Azure para gerenciar identidades e acesso. Cada usuário do catálogo deve ser um membro de saudação do Active Directory para a conta de saudação.

### <a name="assets"></a>Ativos
Um **Catálogo** contém ativos de dados. **Ativos** são Olá unidade de granularidade gerenciada pelo catálogo de saudação.

granularidade de saudação de um ativo varia de acordo com a fonte de dados. Para SQL Server ou Banco de Dados Oracle, um ativo pode ser uma Tabela ou Exibição. Para o SQL Server Analysis Services, um ativo pode ser uma Medida, uma Dimensão ou um KPI (Indicador de Chave de Desempenho). Para SQL Server Reporting Services, um ativo é um Relatório.

Um **ativos** é Olá adicionar ou remover de um catálogo. Unidade de saudação do resultado é obtido da **pesquisa**.

Um **Ativo** é composto de seu nome, local e tipo, bem como anotações que o descrevem melhor.

### <a name="annotations"></a>Anotações
As anotações são itens que representam os metadados sobre os Ativos.

Alguns exemplos de anotações são descrição, marcas, esquema, documentação etc. Uma lista completa dos tipos de ativo hello e anotação estão em Olá seção do modelo de objeto ativo.

## <a name="crowdsourcing-annotations-and-user-perspective-multiplicity-of-opinion"></a>Anotações de crowdsourcing e perspectiva do usuário (multiplicidade de opinião)
Um aspecto importante do catálogo de dados do Azure é como ele suporta crowdsourcing Olá de metadados no sistema de saudação. Como tooa contrário wiki abordagem – onde há apenas uma opinião e hello último gravador ganha – Olá Data Catalog do Azure modelo permite que várias opiniões toolive lado a lado no sistema de saudação.

Essa abordagem reflete Olá mundo real dos dados da empresa onde usuários diferentes podem ter perspectivas diferentes em um determinado ativo:

* Um administrador de banco de dados pode fornecer informações sobre contratos de nível de serviço ou janela de processamento disponíveis Olá para operações de ETL em massa
* Um administrador de dados pode fornecer informações sobre o ativo de saudação do hello business processos toowhich aplicam ou classificações Olá Olá business aplicou tooit
* Um Analista financeiro pode fornecer informações sobre como os dados de saudação são usados durante as tarefas de relatório do fim do período

toosupport neste exemplo, cada usuário – Olá DBA, administrador de dados hello e analista hello – pode adicionar uma descrição tooa única tabela que foi registrada no catálogo de saudação. Todas as descrições são mantidas no sistema de saudação e no portal do catálogo de dados do Azure Olá todas as descrições são exibidas.

Esse padrão é aplicada toomost de itens de saudação no modelo de objeto hello, para que tipos de objeto na carga JSON Olá costumam ser matrizes de propriedades em que você esperava um singleton.

Por exemplo, em ativo Olá raiz é uma matriz de objetos de descrição. propriedade da matriz Olá é chamada "Descrição". Um objeto de descrição tem uma propriedade - descrição. padrão de saudação é que cada usuário que descrição tipos obtém um objeto de descrição é criado para Olá valor fornecido pelo usuário hello.

Olá UX pode escolher como toodisplay Olá combinação. Existem três padrões diferentes para exibição.

* padrão de saudação mais simples é "Mostrar tudo". Nesse padrão, todos os objetos de saudação são mostrados em uma exibição de lista. portal do catálogo de dados do Azure Olá UX usa esse padrão para descrição.
* Outro padrão é "Mesclar". Nesse padrão, todos os valores de saudação de usuários diferentes Olá são mesclados, com duplicata removida. Exemplos desse padrão no portal do catálogo de dados do Azure Olá UX são propriedades de marcas e especialistas de saudação.
* Um terceiro padrão é "último editor vence". Nesse padrão, somente hello mais recente valor digitado é mostrado. friendlyName é um exemplo desse padrão.

## <a name="asset-object-model"></a>Modelo de objeto de ativo
Conforme apresentada na seção de conceitos principais hello, Olá **Data Catalog do Azure** modelo de objeto contém itens que podem ser ativos ou anotações. Itens têm propriedades que podem ser obrigatórias ou opcionais. Algumas propriedades se aplicam a itens de tooall. Algumas propriedades se aplicam a tooall ativos. Algumas propriedades se aplicam somente os tipos de ativo toospecific.

### <a name="system-properties"></a>Propriedades do sistema
<table><tr><td><b>Nome da Propriedade</b></td><td><b>Tipo de dados</b></td><td><b>Comentários</b></td></tr><tr><td>timestamp</td><td>Datetime</td><td>Olá última hora Olá item foi modificado. Esse campo é gerado pelo servidor de saudação quando um item é inserido e sempre que um item é atualizado. Olá valor dessa propriedade é ignorada em entrada de operações de publicação.</td></tr><tr><td>ID</td><td>Uri</td><td>Url absoluta do item de saudação (somente leitura). É Olá URI endereçável exclusivo do item de saudação.  Olá valor dessa propriedade é ignorada em entrada de operações de publicação.</td></tr><tr><td>type</td><td>Cadeia de caracteres</td><td>tipo de saudação do ativo de saudação (somente leitura).</td></tr><tr><td>etag</td><td>Cadeia de caracteres</td><td>Uma cadeia de caracteres correspondente toohello versão Olá item que pode ser usado para controle de simultaneidade otimista ao executar operações que atualizam os itens do catálogo de saudação. "*" pode ser usado toomatch qualquer valor.</td></tr></table>

### <a name="common-properties"></a>Propriedades comuns
Essas propriedades se aplicam a tipos de raiz de tooall ativo e todos os tipos de anotação.

<table>
<tr><td><b>Nome da Propriedade</b></td><td><b>Tipo de dados</b></td><td><b>Comentários</b></td></tr>
<tr><td>fromSourceSystem</td><td>Booliano</td><td>Indica se os dados do item são derivados de um sistema de origem (como o Banco de Dados do SQL Server, Oracle Database) ou criados por um usuário.</td></tr>
</table>

### <a name="common-root-properties"></a>Propriedades comuns de raiz
<p>
Essas propriedades se aplicam a tipos de raiz de tooall ativo.

<table><tr><td><b>Nome da Propriedade</b></td><td><b>Tipo de dados</b></td><td><b>Comentários</b></td></tr><tr><td>name</td><td>Cadeia de caracteres</td><td>Um nome derivado de informações de local de fonte de dados de saudação</td></tr><tr><td>dsl</td><td>DataSourceLocation</td><td>Exclusivamente descreve Olá fonte de dados e é um dos identificadores de saudação para ativo hello. (Consulte a seção de identidade dupla).  estrutura Olá de dsl Olá varia por protocolo hello e tipo de origem.</td></tr><tr><td>dataSource</td><td>DataSourceInfo</td><td>Obter mais detalhes sobre o tipo de saudação do ativo.</td></tr><tr><td>lastRegisteredBy</td><td>SecurityPrincipal</td><td>Descreve o usuário Olá registrado recentemente ativo.  Contém a id exclusiva Olá para usuário hello (Olá upn) e um nome para exibição (lastName e firstName).</td></tr><tr><td>containerId</td><td>Cadeia de caracteres</td><td>ID do ativo de contêiner Olá Olá fonte de dados. Essa propriedade não há suporte para Olá tipo de contêiner.</td></tr></table>

### <a name="common-non-singleton-annotation-properties"></a>Propriedades comuns de anotação não singleton
Essas propriedades se aplicam a tipos de anotação não singleton tooall (anotações, que permitido toobe vários por ativo).

<table>
<tr><td><b>Nome da Propriedade</b></td><td><b>Tipo de dados</b></td><td><b>Comentários</b></td></tr>
<tr><td>chave</td><td>Cadeia de caracteres</td><td>Um usuário especificado chave, que identifica exclusivamente a anotação Olá no conjunto atual de saudação. comprimento da chave Olá não pode exceder 256 caracteres.</td></tr>
</table>

### <a name="root-asset-types"></a>Tipos de ativos de raiz
Tipos de raiz de ativos são os tipos que representam Olá vários tipos de ativos de dados que podem ser registrados no catálogo de saudação. Para cada tipo de raiz, há um modo de exibição, que descreve o ativo e anotações incluídas na exibição de saudação. Nome de exibição deve ser usado no segmento de url {view_name} correspondente Olá ao publicar um ativo usando a API REST.

<table><tr><td><b>Tipo de ativo (Exibir nome)</b></td><td><b>Propriedades adicionais</b></td><td><b>Tipo de dados</b></td><td><b>Anotações Permitidas</b></td><td><b>Comentários</b></td></tr><tr><td>Tabela ("tabelas")</td><td></td><td></td><td>Descrição<p>FriendlyName<p>Marca<p>Esquema<p>ColumnDescription<p>ColumnTag<p> Especialista<p>Visualização<p>AccessInstruction<p>TableDataProfile<p>ColumnDataProfile<p>ColumnDataClassification<p>Documentação<p></td><td>Uma Tabela representa quaisquer dados tabulares.  Por exemplo: Tabela SQL, Exibição SQL, Tabela Tabular do Analysis Services, dimensão do multidimensional do Analysis Services, Tabela do Oracle, etc.   </td></tr><tr><td>Medida ("medidas")</td><td></td><td></td><td>Descrição<p>FriendlyName<p>Marca<p>Especialista<p>AccessInstruction<p>Documentação<p></td><td>Esse tipo representa uma medida do Analysis Services.</td></tr><tr><td></td><td>medida</td><td>Coluna</td><td></td><td>Metadados que descrevem medidas de saudação</td></tr><tr><td></td><td>isCalculated </td><td>Booliano</td><td></td><td>Especifica se a medida de saudação é calculada ou não.</td></tr><tr><td></td><td>measureGroup</td><td>Cadeia de caracteres</td><td></td><td>Contêiner físico para medidas</td></tr><td>KPI ("kpis")</td><td></td><td></td><td>Descrição<p>FriendlyName<p>Marca<p>Especialista<p>AccessInstruction<p>Documentação</td><td></td></tr><tr><td></td><td>measureGroup</td><td>Cadeia de caracteres</td><td></td><td>Contêiner físico para medidas</td></tr><tr><td></td><td>goalExpression</td><td>Cadeia de caracteres</td><td></td><td>Uma expressão numérica MDX ou um cálculo que retorna o valor de destino de saudação do hello KPI.</td></tr><tr><td></td><td>valueExpression</td><td>Cadeia de caracteres</td><td></td><td>Uma expressão numérica de MDX que retorna o valor real de saudação do hello KPI.</td></tr><tr><td></td><td>statusExpression</td><td>Cadeia de caracteres</td><td></td><td>Uma expressão MDX que representa o estado de saudação do hello KPI em um momento específico no tempo.</td></tr><tr><td></td><td>trendExpression</td><td>Cadeia de caracteres</td><td></td><td>Uma expressão MDX que avalia o valor de saudação do hello KPI ao longo do tempo. tendência de saudação pode ser qualquer critério baseado no tempo que é útil em um contexto empresarial específico.</td>
<tr><td>Relatório ("relatórios")</td><td></td><td></td><td>Descrição<p>FriendlyName<p>Marca<p>Especialista<p>AccessInstruction<p>Documentação<p></td><td>Esse tipo representa um relatório do SQL Server Reporting Services </td></tr><tr><td></td><td>assetCreatedDate</td><td>Cadeia de caracteres</td><td></td><td></td></tr><tr><td></td><td>assetCreatedBy</td><td>Cadeia de caracteres</td><td></td><td></td></tr><tr><td></td><td>assetModifiedDate</td><td>Cadeia de caracteres</td><td></td><td></td></tr><tr><td></td><td>assetModifiedBy</td><td>Cadeia de caracteres</td><td></td><td></td></tr><tr><td>Contêiner ("contêineres")</td><td></td><td></td><td>Descrição<p>FriendlyName<p>Marca<p>Especialista<p>AccessInstruction<p>Documentação<p></td><td>Esse tipo representa um contêiner de outros ativos, como um banco de dados SQL, um contêiner de Blobs do Azure ou um modelo do Analysis Services.</td></tr></table>

### <a name="annotation-types"></a>Tipos de anotação
Tipos de anotação representam tipos de metadados que podem ser atribuídos a tipos de tooother no catálogo de saudação.

<table>
<tr><td><b>Tipo de Anotação (nome de exibição aninhado)</b></td><td><b>Propriedades adicionais</b></td><td><b>Tipo de dados</b></td><td><b>Comentários</b></td></tr>

<tr><td>Descrição ("descrições")</td><td></td><td></td><td>Esta propriedade contém uma descrição de um ativo. Cada usuário do sistema Olá pode adicionar seu próprios descrição.  Somente esse usuário pode editar o objeto de descrição de saudação.  (Proprietários de ativos e administradores podem excluir o objeto de descrição de saudação mas não editá-lo). sistema de saudação mantém descrições dos usuários separadamente.  Assim, há uma matriz de descrições de cada ativo (um para cada usuário que contribuiu seus conhecimentos sobre ativo hello, na inclusão toopossibly que contém informações derivado da fonte de dados de saudação).</td></tr>
<tr><td></td><td>description</td><td>string</td><td>Uma breve descrição (2-3 linhas) do ativo Olá</td></tr>

<tr><td>Marca ("marcas")</td><td></td><td></td><td>Esta propriedade define uma marca de um ativo. Cada usuário do sistema Olá pode adicionar várias marcas para um ativo.  Somente usuário Olá que criou objetos de marca pode editá-los.  (Proprietários de ativos e administradores podem excluir objeto de marca Olá mas não editá-lo). sistema de saudação mantém as marcas dos usuários separadamente.  Portanto, há uma matriz de objetos de Marca em cada ativo.</td></tr>
<tr><td></td><td>marca</td><td>string</td><td>Um ativo de saudação descrevendo marca.</td></tr>

<tr><td>FriendlyName ("friendlyName")</td><td></td><td></td><td>Esta propriedade contém um nome amigável de um ativo. FriendlyName é uma anotação de singleton - FriendlyName apenas uma pode ser adicionado tooan ativo.  Somente usuário Olá que criou o objeto FriendlyName pode editá-lo. (Proprietários de ativos e administradores podem excluir Olá FriendlyName objeto mas não editá-lo). sistema Olá mantém os nomes amigáveis dos usuários separadamente.</td></tr>
<tr><td></td><td>friendlyName</td><td>string</td><td>Um nome amigável do ativo de saudação.</td></tr>

<tr><td>Esquema ("esquema")</td><td></td><td></td><td>Olá esquema descreve a estrutura de saudação de dados saudação.  Ele lista Olá nomes de atributo (coluna, atributo, campo, etc.), os tipos também outros metadados.  Essas informações são derivadas da fonte de dados de saudação.  Esquema é uma anotação singleton: somente um esquema pode ser adicionado a um ativo.</td></tr>
<tr><td></td><td>colunas</td><td>Column[]</td><td>Uma matriz de objetos de coluna. Eles descrevem coluna Olá com informações derivadas Olá da fonte de dados.</td></tr>

<tr><td>ColumnDescription ("columnDescriptions")</td><td></td><td></td><td>Esta propriedade contém uma descrição de uma coluna.  Cada usuário do sistema Olá pode adicionar suas próprias descrições de várias colunas (no máximo uma por coluna). Somente usuário Olá que criou objetos ColumnDescription pode editá-los.  (Proprietários de ativos e administradores podem excluir Olá ColumnDescription objeto mas não editá-lo). sistema de saudação mantém as descrições da coluna do usuário esses separadamente.  Portanto, há uma matriz de objetos ColumnDescription em cada ativo (uma por coluna para cada usuário que contribuiu seu conhecimento sobre a coluna de saudação Além disso toopossibly que contém informações derivadas Olá da fonte de dados).  Olá ColumnDescription é toohello livremente acoplada esquema para que ele possa obter fora de sincronia. Olá ColumnDescription pode descrever uma coluna que não existe no esquema de saudação.  É a descrição do toohello gravador tookeep e esquema em sincronia.  fonte de dados Olá também pode ter informações de descrição de colunas e eles são objetos ColumnDescription adicionais que pode ser criados ao executar a ferramenta de saudação.</td></tr>
<tr><td></td><td>columnName</td><td>Cadeia de caracteres</td><td>nome de saudação da coluna de saudação a que essa descrição refere-se.</td></tr>
<tr><td></td><td>description</td><td>Cadeia de caracteres</td><td>uma breve descrição (2-3 linhas) da coluna de saudação.</td></tr>

<tr><td>ColumnTag ("columnTags")</td><td></td><td></td><td>Esta propriedade contém uma marca de uma coluna. Cada usuário do sistema Olá pode adicionar várias marcas para uma determinada coluna e pode adicionar marcas de várias colunas. Somente usuário Olá que criou objetos ColumnTag pode editá-los. (Proprietários de ativos e administradores podem excluir Olá ColumnTag objeto mas não editá-lo). sistema de saudação mantém marcas de coluna esses usuários separadamente.  Portanto, há uma matriz de objetos ColumnTag em cada ativo.  Olá ColumnTag é toohello livremente acoplada esquema para que ele possa obter fora de sincronia. Olá ColumnTag pode descrever uma coluna que não existe no esquema de saudação.  É a marca de coluna toohello gravador tookeep e esquema em sincronia.</td></tr>
<tr><td></td><td>columnName</td><td>Cadeia de caracteres</td><td>nome de saudação da coluna de saudação a que essa marca refere-se.</td></tr>
<tr><td></td><td>marca</td><td>Cadeia de caracteres</td><td>Uma coluna Olá descrevendo marca.</td></tr>

<tr><td>Especialista ("especialistas")</td><td></td><td></td><td>Esta propriedade contém um usuário que é considerado um especialista no conjunto de dados de saudação. opinions(descriptions) bolhas toohello superior especialistas em da saudação da saudação UX ao listar as descrições. Cada usuário pode especificar seus próprios especialistas. Somente esse usuário pode editar o objeto de especialistas de saudação. (Proprietários de ativos e administradores podem excluir objetos especialista Olá mas não editá-lo).</td></tr>
<tr><td></td><td>especialista</td><td>SecurityPrincipal</td><td></td></tr>

<tr><td>Visualização ("visualizações")</td><td></td><td></td><td>visualização de saudação contém um instantâneo de saudação principais 20 linhas de dados para o ativo de saudação. A Visualização só faz sentido para alguns tipos de ativos (faz sentido para Tabela, mas não para Medida).</td></tr>
<tr><td></td><td>preview</td><td>object[]</td><td>A matriz de objetos que representa uma coluna.  Cada objeto tem uma propriedade de mapeamento de coluna tooa com um valor para essa coluna para a linha de saudação.</td></tr>

<tr><td>AccessInstruction ("accessInstructions")</td><td></td><td></td><td></td></tr>
<tr><td></td><td>Tipo MIME</td><td>string</td><td>tipo de mime de saudação do conteúdo hello.</td></tr>
<tr><td></td><td>conteúdo</td><td>string</td><td>instruções de saudação para como tooget acessar toothis dados ativos. conteúdo de saudação pode ser uma URL, um endereço de email ou um conjunto de instruções.</td></tr>

<tr><td>TableDataProfile ("tableDataProfiles")</td><td></td><td></td><td></td></tr>
<tr><td></td><td>numberOfRows</td></td><td>int</td><td>número de saudação de linhas no conjunto de dados de saudação</td></tr>
<tr><td></td><td>tamanho</td><td>longo</td><td>tamanho de saudação em bytes saudação do conjunto de dados.  </td></tr>
<tr><td></td><td>schemaModifiedTime</td><td>string</td><td>modificação do esquema em Olá Olá último tempo</td></tr>
<tr><td></td><td>dataModifiedTime</td><td>string</td><td>Olá último tempo Olá conjunto de dados foi modificado (dados foi adicionados, modificada ou excluir)</td></tr>

<tr><td>ColumnsDataProfile ("columnsDataProfiles")</td><td></td><td></td><td></td></tr>
<tr><td></td><td>colunas</td></td><td>ColumnDataProfile[]</td><td>Uma matriz de perfis de dados da coluna.</td></tr>

<tr><td>ColumnDataClassification ("columnDataClassifications")</td><td></td><td></td><td></td></tr>
<tr><td></td><td>columnName</td><td>Cadeia de caracteres</td><td>nome de saudação da coluna de saudação que essa classificação se refere ao.</td></tr>
<tr><td></td><td>classificação</td><td>Cadeia de caracteres</td><td>classificação de saudação de dados Olá nesta coluna.</td></tr>

<tr><td>Documentação ("documentação")</td><td></td><td></td><td>Um determinado ativo pode ter apenas uma documentação associada a ele.</td></tr>
<tr><td></td><td>Tipo MIME</td><td>string</td><td>tipo de mime de saudação do conteúdo hello.</td></tr>
<tr><td></td><td>conteúdo</td><td>string</td><td>conteúdo de documentation Hello.</td></tr>

</table>

### <a name="common-types"></a>Tipos comuns
Tipos comuns podem ser usados como tipos de saudação para propriedades, mas não são itens.

<table>
<tr><td><b>Tipo comum</b></td><td><b>Propriedades</b></td><td><b>Tipo de dados</b></td><td><b>Comentários</b></td></tr>
<tr><td>DataSourceInfo</td><td></td><td></td><td></td></tr>
<tr><td></td><td>sourceType</td><td>string</td><td>Descreve o tipo de saudação da fonte de dados.  Por exemplo: SQL Server, banco de dados Oracle etc.  </td></tr>
<tr><td></td><td>objectType</td><td>string</td><td>Descreve o tipo de saudação do objeto de fonte de dados de saudação. Por exemplo: Tabela, Exibição do SQL Server.</td></tr>

<tr><td>DataSourceLocation</td><td></td><td></td><td></td></tr>
<tr><td></td><td>protocol</td><td>string</td><td>Obrigatório. Descreve um toocommunicate de protocolo usado com a fonte de dados de saudação. Por exemplo: "tds" para o SQl Server, "oracle" para Oracle etc. Consulte também[especificações de referência - estrutura de DSL da fonte de dados](data-catalog-dsr.md) para lista de saudação de protocolos com suporte no momento.</td></tr>
<tr><td></td><td>endereço</td><td>Dicionário<string, object></td><td>Obrigatório. Endereço é um conjunto de protocolo específico toohello dados de fonte de dados de saudação tooidentify usado que está sendo referenciado. dados de endereço Olá escopo determinado protocolo tooa, que significa que não faz sentido sem conhecer o protocolo de saudação.</td></tr>
<tr><td></td><td>Autenticação</td><td>string</td><td>Opcional. esquema de autenticação de saudação usado toocommunicate com fonte de dados de saudação. Por exemplo: windows, oauth etc.</td></tr>
<tr><td></td><td>connectionProperties</td><td>Dicionário<string, object></td><td>Opcional. Informações adicionais sobre como fonte de dados de tooa tooconnect.</td></tr>

<tr><td>SecurityPrincipal</td><td></td><td></td><td>Olá back-end não executará nenhuma validação de propriedades fornecidas no AAD durante a publicação.</td></tr>
<tr><td></td><td>upn</td><td>string</td><td>Endereço de email exclusivo do usuário. Deve ser especificado se objectId não for fornecido, ou no contexto de saudação da propriedade "lastRegisteredBy", caso contrário, opcional.</td></tr>
<tr><td></td><td>ID do objeto</td><td>Guid</td><td>Identidade do AAD do usuário ou grupo de segurança. Opcional. Deverá ser especificado se o upn não for fornecido; caso contrário, será opcional.</td></tr>
<tr><td></td><td>firstName</td><td>string</td><td>Nome do usuário (para fins de exibição). Opcional. Só é válida no contexto de saudação da propriedade "lastRegisteredBy". Não pode ser especificado ao fornecer a entidade de segurança para "funções", "permissões" e "especialistas".</td></tr>
<tr><td></td><td>lastName</td><td>string</td><td>Sobrenome do usuário (para fins de exibição). Opcional. Só é válida no contexto de saudação da propriedade "lastRegisteredBy". Não pode ser especificado ao fornecer a entidade de segurança para "funções", "permissões" e "especialistas".</td></tr>

<tr><td>Coluna</td><td></td><td></td><td></td></tr>
<tr><td></td><td>name</td><td>string</td><td>Nome da coluna de saudação ou atributo.</td></tr>
<tr><td></td><td>type</td><td>string</td><td>tipo de dados da coluna de saudação ou atributo. tipos permitidos Olá dependem de tipo de origem de dados de ativo de saudação.  Há suporte apenas para um subconjunto de tipos.</td></tr>
<tr><td></td><td>maxLength</td><td>int</td><td>Olá máximo permitido para a coluna hello ou atributo. Derivado da fonte de dados. Somente os tipos de fonte toosome aplicável.</td></tr>
<tr><td></td><td>precisão</td><td>byte</td><td>precisão Olá Olá coluna ou atributo. Derivado da fonte de dados. Somente os tipos de fonte toosome aplicável.</td></tr>
<tr><td></td><td>isNullable</td><td>Booliano</td><td>Se a coluna de saudação é permitido toohave um valor nulo ou não. Derivado da fonte de dados. Somente os tipos de fonte toosome aplicável.</td></tr>
<tr><td></td><td>expressão</td><td>string</td><td>Se o valor de saudação é uma coluna calculada, este campo contém a expressão Olá que expressa valor hello. Derivado da fonte de dados. Somente os tipos de fonte toosome aplicável.</td></tr>

<tr><td>ColumnDataProfile</td><td></td><td></td><td></td></tr>
<tr><td></td><td>columnName </td><td>string</td><td>nome de saudação da coluna de saudação</td></tr>
<tr><td></td><td>type </td><td>string</td><td>tipo de saudação da coluna de saudação</td></tr>
<tr><td></td><td>Min </td><td>string</td><td>valor mínimo de Olá Olá conjunto de dados</td></tr>
<tr><td></td><td>max </td><td>string</td><td>valor máximo de Olá Olá conjunto de dados</td></tr>
<tr><td></td><td>avg </td><td>double</td><td>valor médio de Olá Olá conjunto de dados</td></tr>
<tr><td></td><td>stdev </td><td>double</td><td>desvio padrão de Olá Olá conjunto de dados</td></tr>
<tr><td></td><td>nullCount </td><td>int</td><td>Contagem de saudação de valores nulos no conjunto de dados Olá</td></tr>
<tr><td></td><td>distinctCount  </td><td>int</td><td>Contagem de saudação de valores distintos no conjunto de dados Olá</td></tr>


</table>

## <a name="asset-identity"></a>Identidade do ativo
Catálogo de dados do Azure usa "protocol" e as propriedades de identidade de recipiente de propriedades "address" hello da identidade de toogenerate de propriedade Olá DataSourceLocation "dsl" do ativo hello, que é usado tooaddress Olá ativo dentro Olá catálogo.
Por exemplo, o protocolo de "tds" hello tem propriedades de identidade "server", "banco de dados", "esquema" e "objeto". combinações de saudação do protocolo de saudação e propriedades de identidade de saudação são toogenerate usada identidade Olá Olá ativo de tabela do SQL Server.
O Catálogo de Dados do Azure fornece vários protocolos de fonte de dados internos que são listados em [Especificação de referência da fonte de dados - Estrutura de DSL](data-catalog-dsr.md).
Olá conjunto de protocolos com suporte pode ser estendido por meio de programação (consulte a referência da API de REST de catálogo tooData). Os administradores de saudação catálogo podem registrar protocolos de fonte de dados personalizados. Olá tabela a seguir descreve Olá propriedades necessárias tooregister um protocolo personalizado.

### <a name="custom-data-source-protocol-specification"></a>Especificação de protocolo de fonte de dados personalizados
<table>
<tr><td><b>Tipo</b></td><td><b>Propriedades</b></td><td><b>Tipo de dados</b></td><td><b>Comentários</b></td></tr>

<tr><td>DataSourceProtocol</td><td></td><td></td><td></td></tr>
<tr><td></td><td>namespace</td><td>string</td><td>namespace de saudação do protocolo de saudação. Namespace deve ser de 1 too255 caracteres, conter uma ou mais partes não vazias separadas por ponto (.). Cada parte deve ser de 1 too255 caracteres, começar com uma letra e conter somente letras e números.</td></tr>
<tr><td></td><td>name</td><td>string</td><td>nome de saudação do protocolo de saudação. Nome deve ser de 1 too255 caracteres, começar com uma letra e conter apenas letras, números e caracteres de traço (-) hello.</td></tr>
<tr><td></td><td>identityProperties</td><td>DataSourceProtocolIdentityProperty[]</td><td>Lista de propriedades de identidade, deve conter pelo menos uma, mas no máximo 20 propriedades. Por exemplo: "server", "banco de dados", "esquema", "objeto" é propriedades de identidade de protocolo de "tds" hello.</td></tr>
<tr><td></td><td>identitySets</td><td>DataSourceProtocolIdentitySet[]</td><td>Lista de conjuntos de identidade. Define conjuntos de propriedades de identidade que representam a identidade do ativo válido. Deve conter pelo menos um, mas no máximo 20 conjuntos. Por exemplo: {"server", "database", "schema" e "object"} é um conjunto de identidade para o protocolo "tds", que define a identidade do ativo de Tabela do SQL Server.</td></tr>

<tr><td>DataSourceProtocolIdentityProperty</td><td></td><td></td><td></td></tr>
<tr><td></td><td>name</td><td>string</td><td>nome de saudação da propriedade de saudação. Nome deve ser de 1 too100 caracteres, começar com uma letra e pode conter apenas letras e números.</td></tr>
<tr><td></td><td>type</td><td>string</td><td>tipo de saudação da propriedade hello. Os valores com suporte são: “bool”, “boolean”, “byte”, “guid”, “int”, “integer”, “long”, “string” e “url”</td></tr>
<tr><td></td><td>ignoreCase</td><td>bool</td><td>Indica se o caso deve ser ignorado ao usar o valor da propriedade. Só pode ser especificado para propriedades com o tipo "string". O valor padrão é falso.</td></tr>
<tr><td></td><td>urlPathSegmentsIgnoreCase</td><td>bool[]</td><td>Indica se caso deve ser ignorado para cada segmento do caminho da url de saudação. Só pode ser especificado para propriedades com o tipo "url". O valor padrão é [falso].</td></tr>

<tr><td>DataSourceProtocolIdentitySet</td><td></td><td></td><td></td></tr>
<tr><td></td><td>name</td><td>string</td><td>nome de saudação do conjunto de identidade hello.</td></tr>
<tr><td></td><td>propriedades</td><td>string[]</td><td>Olá lista de propriedades de identidade incluído nessa identidade definida. Ele não pode conter duplicatas. Cada propriedade referenciada pelo conjunto de identidade deve ser definida na lista de saudação do "identityProperties" do protocolo de saudação.</td></tr>

</table>

## <a name="roles-and-authorization"></a>Funções e autorização
O Catálogo de Dados do Microsoft Azure fornece recursos de autorização para operações CRUD de ativos e anotações.

## <a name="key-concepts"></a>Principais conceitos
Olá Data Catalog do Azure usa dois mecanismos de autorização:

* Autorização baseada em função
* Autorização baseada em permissão

### <a name="roles"></a>Funções
Há três funções: **Administrador**, **Proprietário** e **Colaborador**.  Cada função tem seu escopo e direitos, que são resumidos na Olá a tabela a seguir.

<table><tr><td><b>Função</b></td><td><b>Escopo</b></td><td><b>Direitos</b></td></tr><tr><td>Administrador</td><td>Catálogo (todos os ativos/anotações no hello catálogo)</td><td>Read Delete ViewRoles

ChangeOwnership ChangeVisibility ViewPermissions</td></tr><tr><td>Proprietário</td><td>Cada ativo (item raiz)</td><td>Read Delete ViewRoles

ChangeOwnership ChangeVisibility ViewPermissions</td></tr><tr><td>Colaborador</td><td>Cada ativo e anotação individuais</td><td>Atualização de leitura excluir ViewRoles Observação: todos os direitos de saudação são revogados se Olá de leitura no item Olá é revogada de saudação Colaborador</td></tr></table>

> [!NOTE]
> **Leitura**, **atualização**, **excluir**, **ViewRoles** direitos são aplicáveis tooany item (ativo ou anotação) ao **TakeOwnership**, **ChangeOwnership**, **ChangeVisibility**, **ViewPermissions** são apenas os ativos de raiz toohello aplicável.
> 
> **Excluir** direito aplica-se tooan itens e subitems ou único item abaixo dele. Por exemplo, excluir um ativo também exclui todas as anotações desse ativo.
> 
> 

### <a name="permissions"></a>Permissões
A permissão funciona como uma lista de entradas de controle de acesso. Cada entrada de controle de acesso atribui o conjunto de entidade de segurança tooa de direitos. As permissões só podem ser especificadas em um ativo (ou seja, o item de raiz) e aplicam toohello ativo e qualquer subitens.

Durante a saudação **Data Catalog do Azure** visualizar apenas **leitura** direita tem suporte no hello permissões lista tooenable cenário toorestrict visibilidade de um ativo.

Por padrão qualquer usuário autenticado tem **leitura** direito para qualquer item no catálogo hello, a menos que a visibilidade é restrita toohello conjunto de entidades de segurança nas permissões de saudação.

## <a name="rest-api"></a>API REST
**COLOCAR** e **POST** solicitações de item de exibição pode ser usado toocontrol funções e permissões: na carga de tooitem adição, duas propriedades de sistema podem ser especificadas **funções** e  **permissões**.

> [!NOTE]
> **permissões** somente item de raiz tooa aplicável.
> 
> **Proprietário** item raiz da função tooa somente aplicável.
> 
> Por padrão, quando um item é criado no catálogo de saudação seu **Colaborador** é definir o usuário autenticado atualmente toohello. Se o item deve ser atualizável por todos os usuários **Colaborador** deve ser definido muito&lt;todos&gt; entidade de segurança especial no hello **funções** propriedade quando o item for publicado pela primeira vez ( Consulte toohello exemplo a seguir). **Colaborador** não pode ser alterado e permanece Olá mesmo durante o tempo de vida de um item (mesmo **administrador** ou **proprietário** não tem Olá toochange direita Olá  **Colaborador**). Olá somente valor com suporte para a configuração explícita de saudação do hello **Colaborador** é &lt;todos&gt;: **Colaborador** só pode ser um usuário que criou um item ou &lt; Todos&gt;.
> 
> 

### <a name="examples"></a>Exemplos
**Definir o colaborador muito&lt;todos&gt; ao publicar um item.**
A entidade de segurança especial &lt;Everyone&gt; tem a objectId "00000000-0000-0000-0000-000000000201".
  **POST** https://api.azuredatacatalog.com/catalogs/default/views/tables/?api-version=2016-03-30

> [!NOTE]
> Algumas implementações de cliente HTTP podem automaticamente emita novamente solicitações tooa de resposta 302 do servidor de saudação, mas normalmente cabeçalhos de autorização da solicitação de saudação da faixa. Como o cabeçalho de autorização de saudação é necessário toomake solicitações tooAzure catálogo de dados, certifique-se de cabeçalho de autorização Olá ainda é fornecido quando reemissão de um local de redirecionamento de tooa de solicitação especificado pelo catálogo de dados do Azure. Olá seguinte código de exemplo demonstra usando o objeto do .NET HttpWebRequest hello.
> 
> 

**Corpo**

    {
        "roles": [
            {
                "role": "Contributor",
                "members": [
                    {
                        "objectId": "00000000-0000-0000-0000-000000000201"
                    }
                ]
            }
        ]
    }

  **Atribuir proprietários e restringir a visibilidade de um item raiz existente**: **PUT** https://api.azuredatacatalog.com/catalogs/default/views/tables/042297b0...1be45ecd462a?api-version=2016-03-30

    {
        "roles": [
            {
                "role": "Owner",
                "members": [
                    {
                        "objectId": "c4159539-846a-45af-bdfb-58efd3772b43",
                        "upn": "user1@contoso.com"
                    },
                    {
                        "objectId": "fdabd95b-7c56-47d6-a6ba-a7c5f264533f",
                        "upn": "user2@contoso.com"
                    }
                ]
            }
        ],
        "permissions": [
            {
                "principal": {
                    "objectId": "27b9a0eb-bb71-4297-9f1f-c462dab7192a",
                    "upn": "user3@contoso.com"
                },
                "rights": [
                    {
                        "right": "Read"
                    }
                ]
            },
            {
                "principal": {
                    "objectId": "4c8bc8ce-225c-4fcf-b09a-047030baab31",
                    "upn": "user4@contoso.com"
                },
                "rights": [
                    {
                        "right": "Read"
                    }
                ]
            }
        ]
    }

> [!NOTE]
> Em PUT, não é necessário toospecify uma carga de item no corpo da saudação: PUT pode ser funções apenas tooupdate usado e/ou permissões.
> 
> 

<!--Image references-->
[1]: ./media/data-catalog-developer-concepts/concept2.png
