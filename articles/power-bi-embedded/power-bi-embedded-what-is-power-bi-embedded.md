---
title: "aaaWhat é o Microsoft Power BI inserido?"
description: "Power BI inserido permite toointegrate relatórios do Power BI em seu web ou aplicativos móveis para que você não precise soluções personalizadas de toobuild."
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 03649b72-b7d7-40ca-b077-12356d72d4f3
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/20/2017
ms.author: asaxton
ms.openlocfilehash: 0353938b6cdd9bb58b123b250f45f76b8cc7abe6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-microsoft-power-bi-embedded"></a>O que é o Microsoft Power BI Embedded?
Com **Power BI Embedded**, você pode integrar relatórios do Power BI diretamente a seus aplicativos móveis ou Web.

![](media/powerbi-embedded-whats-is/what-is.png)

Power BI inserido é um **serviço do Azure** que permite que ISVs e desenvolvedores de aplicativo toosurface dados do Power BI experiências em seus aplicativos. Como desenvolvedor, você criou aplicativos, e esses aplicativos têm seus próprios usuários e um conjunto distinto de recursos. Esses aplicativos também podem acontecer toohave alguns elementos de dados interna, como gráficos e relatórios agora podem ser desligados pelo Microsoft Power BI inserido. Você não precisa um toouse de conta do Power BI em seu aplicativo. Você pode continuar toosign no aplicativo tooyour assim como antes e exibir e interagir com hello experiência de relatórios do Power BI sem a necessidade de qualquer licença adicional.

## <a name="licensing-for-microsoft-power-bi-embedded"></a>Licenciamento do Microsoft Power BI Embedded
Em Olá **Microsoft Power BI inserido** modelo de uso para o Power BI não é responsabilidade de saudação do usuário final de saudação de licenciamento.  Em vez disso, **sessões** são comprados pelo desenvolvedor de saudação do aplicativo hello que está consumindo visuais hello e são cobrados toohello assinatura que possui os recursos. Informações adicionais podem ser encontradas em Olá [página de preços](https://azure.microsoft.com/en-us/pricing/details/power-bi-embedded/).

## <a name="microsoft-power-bi-embedded-conceptual-model"></a>Modelo conceitual do Microsoft Power BI Embedded

![](media/powerbi-embedded-whats-is/model.png)

Como qualquer outro serviço no Azure, os recursos para o Power BI inserido são provisionados através de Olá [APIs do Gerenciador de recursos do Azure](https://msdn.microsoft.com/library/mt712306.aspx). Nesse caso, o recurso de saudação provisionado é um **coleta de espaço de trabalho do Power BI**.

## <a name="workspace-collection"></a>Coleção de espaços de trabalho
Um **coleta de espaço de trabalho** é hello Azure contêiner de nível superior para recursos que contém 0 ou mais **espaços de trabalho**.  Um **espaço de trabalho** **coleção** possui todas as propriedades padrão do Azure hello, bem como a seguir hello:

* **Chaves de acesso** – as chaves usadas ao chamar com segurança Olá APIs do Power BI (descrita adiante).
* **Os usuários** – os usuários do Azure Active Directory (AAD) que têm toomanage de direitos de administrador Olá coleta de espaço de trabalho do Power BI por meio de saudação portal do Azure ou a API do Gerenciador de recursos do Azure.
* **Região** – como parte do provisionamento de um **coleta de espaço de trabalho**, você pode selecionar um toobe região provisionado no. Para obter mais informações, consulte [Regiões do Azure](https://azure.microsoft.com/regions/).

## <a name="workspace"></a>Espaço de trabalho
Um **Espaço de Trabalho** é um contêiner de conteúdo do Power BI, que pode incluir conjuntos de dados e relatórios. Um **Espaço de Trabalho** fica vazio logo após ser criado pela primeira vez. Você vai criar conteúdo usando o Power BI Desktop e você implantará programaticamente Olá PBIX no espaço de trabalho usando Olá [API do Power BI importar](https://msdn.microsoft.com/library/mt711504.aspx). Você pode criar também programaticamente o conjunto de dados e então criar relatórios de dentro de seu aplicativo em vez de usar o Power BI Desktop.

## <a name="using-workspace-collections-and-workspaces"></a>Usando espaços de trabalhos e coleções de espaços de trabalho
**Coleções de espaço de trabalho** e **espaços de trabalho** são contêineres de conteúdo que são usados e organizados em melhor forma adequada de design de saudação do aplicativo hello que você está criando. Haverá várias maneiras diferentes que você pode organizar o conteúdo do hello dentro deles. Você pode escolher tooput todo o conteúdo dentro de um espaço de trabalho e posterior toofurther de tokens do aplicativo use subdividir conteúdo Olá entre seus clientes. Você também pode optar tooput todos os seus clientes em espaços de trabalho separados para que haja alguma separação entre eles. Ou, você pode optar por usuários tooorganize por região em vez de cliente. Esse design flexível permite que você toochoose Olá melhor maneira tooorganize conteúdo.

## <a name="cached-datasets"></a>Conjuntos de dados em cache
Conjuntos de dados em cache podem ser usados.  No entanto, você não pode atualizar os dados armazenados em cache após eles serem carregados no **Microsoft Power BI Embedded**. Um conjunto de dados armazenados em cache significa que você importou dados saudação no Power BI Desktop em vez de usar o DirectQuery.

## <a name="authentication-and-authorization-with-app-tokens"></a>Autenticação e autorização com tokens de aplicativo
**Microsoft Power BI inserido** adia tooyour aplicativo tooperform todos os Olá necessário autenticação e autorização. Não há nenhum requisito explícito de que os usuários finais sejam os clientes do Azure Active Directory (Azure AD).  Em vez disso, seu aplicativo expressa muito**Microsoft Power BI inserido** toorender autorização um relatório do Power BI usando **Tokens de autenticação de aplicativo (App Tokens)**.  Essas **aplicativo Tokens** são criados conforme necessário ao seu aplicativo deseja toorender um relatório.

![](media/powerbi-embedded-whats-is/app-tokens.png)

**Tokens de autenticação de aplicativo (App Tokens)** são tooauthenticate usado contra **Microsoft Power BI inserido**.  Há três tipos de **Tokens de Aplicativo**:

1. Tokens de Provisionamento – usados ao provisionar um novo **Espaço de Trabalho** em uma **Coleção de Espaços de Trabalho**
2. Tokens de desenvolvimento - usados ao fazer chamadas diretamente toohello **APIs REST do Power BI**
3. Inserindo Tokens - usados ao fazer chamadas toorender incorporado de um relatório no hello iframe

Esses tokens são usados para Olá várias fases de suas interações com **Microsoft Power BI inserido**.  tokens de saudação são projetados para que você pode delegar permissões do seu aplicativo tooPower BI. Para obter mais informações, consulte o [Fluxo de Tokens de Aplicativo](power-bi-embedded-app-token-flow.md).

## <a name="create-or-edit-reports-within-your-application"></a>Criar ou editar relatórios dentro de seu aplicativo

Você pode editar existe relatórios ou criar novos relatórios diretamente em seu aplicativo sem ter que toouse Power BI Desktop. Isso requer a existência de um conjunto de dados dentro de seu espaço de trabalho.

## <a name="see-also"></a>Consulte também

[Cenários comuns do Microsoft Power BI Embedded](power-bi-embedded-scenarios.md)  
[Introdução ao Microsoft Power BI Embedded](power-bi-embedded-get-started.md)  
[Introdução a exemplos](power-bi-embedded-get-started-sample.md)  
[Inserir um relatório](power-bi-embedded-embed-report.md)  
[Autenticando e autorizando com o Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Amostra de inserção de JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[Repositório de Git PowerBI-CSharp](https://github.com/Microsoft/PowerBI-CSharp)  
[Repositório de Git PowerBI-Node](https://github.com/Microsoft/PowerBI-Node)  
Mais perguntas? [Tente Olá comunidade do Power BI](http://community.powerbi.com/)
