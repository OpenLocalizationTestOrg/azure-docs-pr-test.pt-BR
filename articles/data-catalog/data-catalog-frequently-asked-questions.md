---
title: "Perguntas frequentes do catálogo de dados de aaaAzure | Microsoft Docs"
description: "Perguntas frequentes sobre o Catálogo de Dados do Azure, incluindo recursos para descoberta de fontes de dados, anotação e gerenciamento."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 5c7e209a-458c-4bb4-96bb-7ed178f9528a
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 03f9f4b801640b2e14232c62c8fc168e42e2c393
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-frequently-asked-questions"></a>Perguntas frequentes sobre o Catálogo de Dados do Azure
Este artigo fornece respostas toofrequently frequentes perguntas relacionadas toohello serviço de catálogo de dados do Azure.

## <a name="what-is-azure-data-catalog"></a>O que é o Catálogo de Dados do Azure?
O Catálogo de Dados é um serviço totalmente gerenciado hospedado no Microsoft Azure que atua como um sistema de registro e descoberta para fontes de dados da empresa. Com o catálogo de dados, qualquer usuário, os cientistas de toodata analistas e desenvolvedores, pode registrar, descobrir, entender e consumir fontes de dados.

## <a name="what-customer-challenges-does-it-solve"></a>Quais desafios do cliente ele resolve?
Endereços do catálogo de dados Olá desafios de descoberta de fonte de dados e "dados escuros" para que os usuários podem descobrir e entender as fontes de dados empresariais.

## <a name="what-are-its-target-audiences"></a>Quais são seus públicos-alvo?
O Catálogo de Dados é desenvolvido para usuários técnicos e não técnicos, incluindo:

* Os desenvolvedores de dados e profissionais de BI e análise: quem é responsável por produzir dados e análise de conteúdo para outros tooconsume.
* Administradores de dados: as pessoas que têm conhecimento Olá Olá dados, o que significa e como ele é pretendido toobe usado.
* Os consumidores de dados: pessoas que precisa tooeasily de toobe capaz de descobrir, entender e conectar dados toohello precisam toodo seu trabalho, usando a ferramenta Olá de sua escolha.
* Central IT: pessoas que precisam de toomake centenas de fontes de dados podem ser descobertos por usuários de negócios e que precisam de supervisão toomaintain sobre como os dados estão sendo usados e por quem.

## <a name="what-is-its-availability-by-region"></a>Qual é a disponibilidade por região?
Serviços de catálogo de dados estão disponíveis atualmente no hello centros de dados a seguir:

* Oeste dos EUA
* Leste dos EUA
* Europa Ocidental
* Norte da Europa
* Leste da Austrália
* Sudeste Asiático

## <a name="what-are-its-limits-on-hello-number-of-data-assets"></a>Quais são seus limites no número de saudação de ativos de dados?
Olá, edição gratuita do catálogo de dados é limitado too5, ativos de dados registrado, 000.

Olá edição Standard do catálogo de dados oferece suporte ao backup too100, 000 ativos de dados registrados.

## <a name="what-are-its-supported-data-source-and-asset-types"></a>Quais são os tipos de ativos e fonte de dados com suporte?
Para obter uma lista de fontes de dados com suporte no momento, consulte [DSR do Catálogo de Dados](data-catalog-dsr.md).

## <a name="how-do-i-request-support-for-another-data-source"></a>Como fazer para solicitar suporte para outra fonte de dados?
toosubmit recurso solicitações e outros comentários, vá toohello [Fórum do catálogo de dados do Azure](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).

## <a name="how-do-i-get-started-with-data-catalog"></a>Como fazer para usar o Catálogo de Dados?
Olá tooget de maneira melhor de Introdução está indo muito[guia de Introdução ao catálogo de dados](data-catalog-get-started.md). Este artigo é uma visão geral dos recursos de saudação do serviço hello.

## <a name="how-do-i-register-my-data"></a>Como fazer para registrar meus dados?
tooregister seus dados no catálogo de dados:
1. No portal do catálogo de dados do Azure de hello, na Olá **publicar** área, a ferramenta de registro do início Olá Data Catalog do Azure. 
2. Em Olá catálogo de dados a publicação de aplicativo, entrar com hello mesmo credenciais que você use tooaccess Olá portal do catálogo de dados.
3. Selecione a fonte de dados de saudação e ativos específicos de saudação que você deseja tooregister.

## <a name="what-properties-does-it-extract-for-data-assets-that-are-registered"></a>Quais propriedades ele extrai para ativos de dados que são registrados?
propriedades específicas de saudação diferem da fonte de toodata de fonte de dados, mas, em geral, a saudação serviço de publicação do catálogo de dados extrai Olá informações a seguir:

* Nome do ativo
* Tipo de Ativo
* Descrição do ativo
* Nomes do atributo/coluna
* Tipos de dados do atributo/coluna
* Descrição do atributo/coluna

> [!IMPORTANT]
> Registrando ativos de dados com o catálogo de dados não mova ou copie toohello seus dados na nuvem. Registro de recursos de uma fonte de dados cópias Olá tooAzure de metadados de ativos, mas dados saudação permanecem no local de fonte de dados existente do hello. regra de toothis Olá exceção é se você escolher registros de visualização de tooupload ou um perfil de dados quando você registrar ativos hello. Quando você inclui uma visualização, o too20 registros são copiados de cada ativo e armazenados como um instantâneo no catálogo de dados. Quando você incluir um perfil de dados, informações agregadas são calculadas e incluídas nos metadados de saudação que são armazenados no catálogo de saudação. Agregar informações pode incluir Olá tamanho das tabelas, Olá a porcentagem de valores nulos por coluna ou Olá mínimo, máximo e médio valores para colunas. 
>
>

> [!NOTE]
> Para fontes de dados, como SQL Server Analysis Services que têm uma primeira classe **descrição** propriedade Olá publicar o aplicativo extrai valor da propriedade do catálogo de dados. Para bancos de dados relacionais do SQL Server, que não têm uma primeira classe **descrição** propriedade Olá aplicativo de publicação do catálogo de dados extrai o valor de saudação de saudação **ms_description** propriedade estendida para objetos e colunas. Para saber mais, confira [Como usar propriedades estendidas em objetos de banco de dados](https://technet.microsoft.com/library/ms190243%28v=sql.105%29.aspx).
>
>

## <a name="how-long-should-it-take-for-newly-registered-assets-tooappear-in-hello-catalog"></a>Quanto tempo deve leva para tooappear ativos registrados recentemente no catálogo Olá?
Depois de registrar ativos no catálogo de dados, pode haver um período de 5 segundos too10 antes de aparecerem no portal do catálogo de dados de saudação.

## <a name="how-do-i-annotate-and-enrich-hello-metadata-for-my-registered-data-assets"></a>Como anotar e enriquecer Olá metadados para Meus ativos de dados registrados?
tooprovide metadados de maneira mais simples Olá para ativos registrados tooselect Olá ativo no portal do catálogo de dados hello e digite os valores de Olá no painel de propriedades de saudação ou esquema para o objeto selecionado hello.

Você também pode fornecer alguns metadados, como marcas e os especialistas durante o processo de registro de saudação. valores de Olá que você fornecer em Olá serviço de publicação do catálogo de dados se aplicam a ativos de tooall que está sendo registrados no momento. Olá tooview objetos registrado recentemente no portal de saudação para anotação adicional, selecione Olá **exibição Portal** botão na tela final de saudação do hello aplicativo de publicação do catálogo de dados.

## <a name="how-do-i-delete-my-registered-data-objects"></a>Como fazer para excluir meus objetos de dados registrados?
Você pode excluir um objeto do catálogo de dados selecionando o objeto Olá no portal de saudação e, em seguida, clicando em Olá **excluir** botão. Remover objeto de saudação remove os metadados de catálogo de dados, mas não afeta a fonte de dados subjacente hello.

## <a name="what-is-an-expert"></a>O que é um especialista?
Especialista é uma pessoa que tem uma perspectiva bem informada sobre um objeto de dados. Um objeto pode ter muitos especialistas. Um especialista não precisa toobe hello "proprietário" de um objeto, mas é simplesmente uma pessoa que sabe como dados saudação podem e deve ser usado.

## <a name="how-do-i-share-information-with-hello-data-catalog-team-if-i-encounter-problems"></a>Como faço para compartilhar informações com a equipe do catálogo de dados Olá se encontrar problemas?
problemas de tooreport, compartilhar informações e fazer perguntas, vá toohello [Fórum do catálogo de dados do Azure](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).

## <a name="does-hello-catalog-work-with-another-data-source-that-im-interested-in"></a>Olá trabalho de catálogo com outra fonte de dados que tenho interesse em?
Estamos trabalhando ativamente na adição de mais tooData de fontes de dados catálogo. Se você quiser toosee uma fonte de dados específico com suporte, sugere (ou o suporte de voz, se ele já foi sugerido) por vai toohello [Fórum do catálogo de dados do Azure](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).

## <a name="how-is-azure-data-catalog-related-toohello-data-catalog-in-power-bi-for-office-365"></a>Como é o catálogo de dados do Azure relacionados toohello catálogo de dados no Power BI para Office 365?
Você pode pensar no catálogo de dados do Azure como uma evolução do hello catálogo de dados no Power BI. A partir da primavera de 2017, o Data Catalog do Azure é usado tooenable Olá compartilhamento e descoberta de consultas no Excel 2016 e Power Query para Excel. Recursos do catálogo de dados no Excel são toousers disponíveis com licenças do Power BI Pro.

## <a name="what-permissions-do-i-need-tooregister-assets-with-data-catalog"></a>O que fazem permissões preciso tooregister ativos no catálogo de dados?
ferramenta de registro do toorun Olá catálogo de dados, você precisa de permissões na fonte de dados de saudação que permite que você tooread Olá metadados da fonte de saudação. tooalso incluem uma visualização, você deve ter permissões que permitem que você tooread em dados de saudação de objetos de saudação que está sendo registrados.

## <a name="will-data-catalog-be-made-available-for-on-premises-deployment-as-well"></a>O Catálogo de Dados será disponibilizado para implantação local também?
Catálogo de dados é um serviço de nuvem que possa funcionar com toodeliver de fontes de dados de nuvem e local de uma solução de descoberta de fonte de dados. Atualmente, não há nenhum plano para uma versão do hello serviço Catálogo de dados que é executado no local.

## <a name="can-i-extract-more-or-richer-metadata-from-hello-data-sources-i-register"></a>Pode extrair metadados mais ou mais avançados de fontes de dados Olá que registrar?
Estamos trabalhando ativamente tooexpand recursos de saudação do catálogo de dados. Se você quiser toohave metadados adicionais extraídos da fonte de dados Olá durante o registro, sugerir (ou voto para ele, se ele já foi sugerido) Olá [Fórum do catálogo de dados do Azure](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409). Olá futuras, podemos permitirá terceira partes tooadd novos tipos de dados por meio de uma API de extensibilidade.

## <a name="how-do-i-restrict-hello-visibility-of-registered-data-assets-so-that-only-certain-people-can-discover-them"></a>Como restringir a visibilidade de saudação de ativos de dados registrado, para que somente algumas pessoas podem descobri-los?
Selecione os ativos de dados Olá no hello catálogo de dados e clique em Olá **Take Ownership** botão. Os proprietários de ativos de dados no catálogo de dados podem alterar a visibilidade de saudação configurações tooeither permitir Olá de toodiscover todos os usuários ativos de propriedade ou impedir que os usuários toospecific de visibilidade.

## <a name="how-do-i-update-hello-registration-for-a-data-asset-so-that-changes-in-hello-data-source-are-reflected-in-hello-catalog"></a>Como atualizar registro Olá para um ativo de dados para que as alterações na fonte de dados de saudação são refletidas no catálogo de saudação?
tooupdate Olá metadados para os ativos de dados que já estão registrados no catálogo hello, simplesmente registrar novamente o fonte de dados de saudação que contém ativos de saudação. Todas as alterações na fonte de dados hello, como colunas que estão sendo adicionadas ou removidas de tabelas ou exibições, são atualizadas no catálogo hello, mas qualquer anotações fornecidas por usuários são mantidas.

## <a name="my-question-isnt-answered-here-where-can-i-go-for-answers"></a>Minha dúvida não é respondida aqui. Como posso obter respostas?
Vá toohello [Fórum do catálogo de dados do Azure](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409). As perguntas feitas serão posteriormente incluídas aqui.
