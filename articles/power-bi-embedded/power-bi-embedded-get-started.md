---
title: aaaGet iniciado com o Microsoft Power BI Embedded
description: "Power BI Embedded, adicione relatórios interativos do Power BI a seu aplicativo de business intelligence"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 4787cf44-5d1c-4bc3-b3fd-bf396e5c1176
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: ebb550cb4eba761dde3c23e4dd0314fc885817e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-microsoft-power-bi-embedded"></a>Introdução ao Microsoft Power BI Embedded

**Power BI inserido** é um serviço do Azure que tooadd de desenvolvedores de aplicativos permite que relatórios interativos do Power BI em seus próprios aplicativos. **Power BI inserido** funciona com aplicativos existentes sem necessidade reestruturação ou alterar a maneira como os usuários-Olá entrar.

Recursos para **Microsoft Power BI inserido** provisionados usando Olá [Azure ARM APIs](https://msdn.microsoft.com/library/mt712306.aspx). Nesse caso, o recurso de saudação provisionar é um **coleta de espaço de trabalho do Power BI**.

![](media/power-bi-embedded-get-started/introduction.png)

## <a name="create-a-workspace-collection"></a>Criar uma coleção de espaços de trabalho

Um **coleta de espaço de trabalho** é o recurso do Azure do nível superior hello e um contêiner para conteúdo de saudação que será inserido em seu aplicativo. Uma **Coleção de espaços de trabalho** pode ser criada de duas maneiras:

* Manualmente usando Olá Portal do Azure
* Programaticamente, usando Olá APIs de Manager(ARM) de recursos do Azure

Vamos percorrer Olá etapas toobuild um **coleta de espaço de trabalho** usando Olá Portal do Azure.

1. Abra e entre no **Portal do Azure**: [http://portal.azure.com](http://portal.azure.com).
2. Clique em **+ novo** no painel superior hello.
   
   ![](media/power-bi-embedded-get-started/create-workspace-1.png)
3. Em **Dados + Análise**, clique em **Power BI Embedded**.
4. Em Olá **folha de coleta de espaço de trabalho**, insira informações Olá necessário. Para ver **Preços**, confira [Preço do Power BI Embedded](http://go.microsoft.com/fwlink/?LinkID=760527).
   
   ![](media/power-bi-embedded-get-started/create-workspace-2.png)
5. Clique em **Criar**.

Olá **coleta de espaço de trabalho** levará tooprovision de alguns instantes. Quando concluído, você será levado toohello **folha de coleta de espaço de trabalho**.

   ![](media/power-bi-embedded-get-started/create-workspace-3.png)

Olá **criação folha** contém informações de saudação necessárias toocall Olá APIs que criar espaços de trabalho e implantar conteúdo toothem.

<a name="view-access-keys"/>

## <a name="view-power-bi-api-access-keys"></a>Exibir chaves de acesso da API do Power BI

Um dos mais importantes de partes de informações necessárias toocall Olá APIs REST do Power BI de saudação são Olá **chaves de acesso**. Estes são usados toogenerate Olá **tokens do aplicativo** que são usada tooauthenticate suas solicitações de API. tooview seu **chaves de acesso**, clique em **chaves de acesso** em Olá **folha configurações**. Para saber mais sobre **tokens de aplicativo**, confira [Autenticando e autorizando com o Power BI Embedded](power-bi-embedded-app-token-flow.md).

   ![](media/power-bi-embedded-get-started/access-keys.png)

Você notará que tem duas chaves.

   ![](media/power-bi-embedded-get-started/access-keys-2.png)

Copie essas chaves e armazene-as com segurança em seu aplicativo. É muito importante tratar essas chaves como você faria com uma senha, pois será fornecem acesso tooall Olá conteúdo no seu **coleta de espaço de trabalho**.

Embora duas chaves estejam listadas, somente uma chave é usada de cada vez. segunda chave de saudação é fornecido para que você periodicamente pode regenerar chaves sem interromper o serviço de toohello de acesso.

Agora que você tem uma instância do Power BI para seu aplicativo e as **Chaves de Acesso**, pode importar um relatório em seu próprio aplicativo. Antes, você aprenderá como tooimport um relatório, a próxima seção de saudação descreve criando tooembed de conjuntos de dados e relatórios do Power BI em um aplicativo.

## <a name="working-with-workspaces"></a>Trabalhando com espaços de trabalho

Depois de criar sua coleção do espaço de trabalho, você precisará toocreate um espaço de trabalho que conterá os relatórios e conjuntos de dados. toocreate um espaço de trabalho, você precisará Olá toouse [API de REST do espaço de trabalho de Post](https://msdn.microsoft.com/library/azure/mt711503.aspx).

## <a name="create-power-bi-datasets-and-reports-tooembed-into-an-app-using-power-bi-desktop"></a>Criar tooembed de conjuntos de dados e relatórios do Power BI em um aplicativo usando o Power BI Desktop

Agora que você criou uma instância do Power BI para seu aplicativo e ter **chaves de acesso**, você precisará toocreate Olá Power BI conjuntos de dados e relatórios que você deseja tooembed. Conjuntos de dados e relatórios podem ser criados usando o **Power BI Desktop**. Você pode baixar o [Power BI Desktop gratuitamente](https://go.microsoft.com/fwlink/?LinkId=521662). Ou, tooquickly começar, você pode baixar Olá [PBIX de exemplo de análise de varejo](http://go.microsoft.com/fwlink/?LinkID=780547).

> [!NOTE]
> toolearn mais informações sobre como toouse **Power BI Desktop**, consulte [guia de Introdução ao Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop).

Com **Power BI Desktop**, você se conectar tooyour fonte de dados importando uma cópia dos dados de saudação em **Power BI Desktop** ou conectar-se diretamente dados toohello fonte usando **DirectQuery**.

Aqui estão Olá diferenças entre usar **importação** e **DirectQuery**.

| Importar | DirectQuery |
| --- | --- |
| Tabelas, colunas, *e dados* são importados ou copiados para o **Power BI Desktop**. Ao trabalhar com visualizações, **Power BI Desktop** consultas uma cópia dos dados de saudação. toosee todas as alterações de dados subjacente toohello ocorreu, você deve atualizar ou importar novamente um dataset completo e atual. |Somente *tabelas e colunas* são importadas ou copiadas para o **Power BI Desktop**. Ao trabalhar com visualizações, **Power BI Desktop** consultas Olá a fonte de dados subjacente, que significa que você sempre está exibindo dados atuais. |

Para obter mais informações sobre a fonte de dados tooa conexão, consulte [conectar fonte de dados de tooa](power-bi-embedded-connect-datasource.md).

Depois de salvar seu trabalho no **Power BI Desktop**, um arquivo PBIX será criado. Esse arquivo contém o relatório. Além disso, se você importar Olá dados PBIX contém Olá conjunto de dados completo, ou se você usar **DirectQuery**, Olá PBIX contém apenas um esquema de conjunto de dados. Implantar programaticamente Olá PBIX no espaço de trabalho usando Olá [API do Power BI importar](https://msdn.microsoft.com/library/mt711504.aspx).

> [!NOTE]
> **Power BI inserido** tem adicionais APIs toochange saudação do servidor e banco de dados que o conjunto de dados está apontando conjunto tooand uma credencial de conta de serviço que Olá conjunto de dados usará o banco de dados do tooconnect tooyour. Confira [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) e [Correção de fonte de dados do gateway](https://msdn.microsoft.com/library/mt711498.aspx).

## <a name="create-power-bi-datasets-and-reports-using-apis"></a>Criar relatórios e conjuntos de dados do Power BI usando APIs

### <a name="datsets"></a>Conjuntos de dados

Você pode criar conjuntos de dados no Power BI inserido usando Olá API REST. Em seguida, você pode enviar dados por push para seu conjunto de dados. Isso permite que você toowork com dados sem a necessidade de saudação do Power BI Desktop. Para saber mais, veja [Postar conjuntos de dados](https://msdn.microsoft.com/library/azure/mt778875.aspx).

### <a name="reports"></a>Relatórios

Você pode criar um relatório de um conjunto de dados diretamente em seu aplicativo usando Olá API JavaScript. Para saber mais, veja [Criar um novo relatório de um conjunto de dados no Power BI Embedded](power-bi-embedded-create-report-from-dataset.md).

## <a name="see-also"></a>Consulte também

[Introdução a exemplos](power-bi-embedded-get-started-sample.md)  
[Autenticando e autorizando com o Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Inserir um relatório](power-bi-embedded-embed-report.md)  
[Criar um novo relatório de um conjunto de dados no Power BI Embedded](power-bi-embedded-create-report-from-dataset.md)
[Salvar relatórios](power-bi-embedded-save-reports.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[Amostra de inserção de JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
Mais perguntas? [Tente Olá comunidade do Power BI](http://community.powerbi.com/)

