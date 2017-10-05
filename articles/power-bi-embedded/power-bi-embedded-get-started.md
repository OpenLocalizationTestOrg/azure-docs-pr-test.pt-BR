---
title: "Introdução ao Microsoft Power BI Embedded"
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
ms.openlocfilehash: 4afa8d2c7f8ec1942521ba5fa131967dfd581c91
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-microsoft-power-bi-embedded"></a>Introdução ao Microsoft Power BI Embedded

**Power BI Embedded** é um serviço do Azure que permite que os desenvolvedores de aplicativos adicionem relatórios interativos do Power BI a seus próprios aplicativos. **Power BI Embedded** funciona com aplicativos existentes sem precisar reprojetar ou alterar os maneira como os usuários entram.

Os recursos para o **Microsoft Power BI Embedded** são provisionados por meio de [APIs do ARM do Azure](https://msdn.microsoft.com/library/mt712306.aspx). Nesse caso, o recurso que você provisiona é uma **Coleção de Espaços de Trabalho do Power BI**.

![](media/power-bi-embedded-get-started/introduction.png)

## <a name="create-a-workspace-collection"></a>Criar uma coleção de espaços de trabalho

Uma **coleção de espaços de trabalho** é o recurso mais avançado do Azure e um contêiner para o conteúdo que será inserido em seu aplicativo. Uma **Coleção de espaços de trabalho** pode ser criada de duas maneiras:

* Usando o Portal do Azure manualmente
* Programaticamente, usando as APIs do ARM (Azure Resource Manager)

Vamos percorrer as etapas para criar uma **Coleção de espaços de trabalho** usando o Portal do Azure.

1. Abra e entre no **Portal do Azure**: [http://portal.azure.com](http://portal.azure.com).
2. Clique em **+ Novo** no painel superior.
   
   ![](media/power-bi-embedded-get-started/create-workspace-1.png)
3. Em **Dados + Análise**, clique em **Power BI Embedded**.
4. Na **Folha da Coleção de Espaços de Trabalho**, insira as informações necessárias. Para ver **Preços**, confira [Preço do Power BI Embedded](http://go.microsoft.com/fwlink/?LinkID=760527).
   
   ![](media/power-bi-embedded-get-started/create-workspace-2.png)
5. Clique em **Criar**.

A **Coleção de espaços de trabalho** levará alguns minutos para provisionar. Quando ela for concluída, você será levado para a **Folha de Coleção de espaços de trabalho**.

   ![](media/power-bi-embedded-get-started/create-workspace-3.png)

A **Folha de Criação** contém as informações necessárias para chamar as APIs que criam espaços de trabalho e implanta conteúdo nelas.

<a name="view-access-keys"/>

## <a name="view-power-bi-api-access-keys"></a>Exibir chaves de acesso da API do Power BI

Uma das informações mais importantes necessárias para chamar as APIs REST do Power BI são as **Chaves de Acesso**. Elas são usadas para gerar os **tokens do aplicativo** que são usados na autenticação das solicitações de API. Para exibir suas **Chaves de Acesso**, clique em **Chaves de Acesso** na **Folha de Configurações**. Para saber mais sobre **tokens de aplicativo**, confira [Autenticando e autorizando com o Power BI Embedded](power-bi-embedded-app-token-flow.md).

   ![](media/power-bi-embedded-get-started/access-keys.png)

Você notará que tem duas chaves.

   ![](media/power-bi-embedded-get-started/access-keys-2.png)

Copie essas chaves e armazene-as com segurança em seu aplicativo. É muito importante tratar essas chaves como faria com uma senha, pois elas darão acesso a todo o conteúdo em sua **Coleção de espaços de trabalho**.

Embora duas chaves estejam listadas, somente uma chave é usada de cada vez. A segunda chave é fornecida para regenerar as chaves periodicamente sem interromper o acesso ao serviço.

Agora que você tem uma instância do Power BI para seu aplicativo e as **Chaves de Acesso**, pode importar um relatório em seu próprio aplicativo. Antes de aprender como importar um relatório, a próxima seção descreve a criação de relatórios e conjuntos de dados do Power BI para inserir em um aplicativo.

## <a name="working-with-workspaces"></a>Trabalhando com espaços de trabalho

Depois que você criou sua coleção de espaço de trabalho, você precisará criar um espaço de trabalho que conterá seus relatórios e conjuntos de dados. Para criar um espaço de trabalho, você precisará usar o [API de REST do espaço de trabalho de Post](https://msdn.microsoft.com/library/azure/mt711503.aspx).

## <a name="create-power-bi-datasets-and-reports-to-embed-into-an-app-using-power-bi-desktop"></a>Criar relatórios e conjuntos de dados do Power BI para inserir em um aplicativo usando o Power BI Desktop

Agora que você criou uma instância do Power BI para seu aplicativo e tem **Chaves de Acesso**, precisa criar os relatórios e conjuntos de dados do Power BI que deseja inserir. Conjuntos de dados e relatórios podem ser criados usando o **Power BI Desktop**. Você pode baixar o [Power BI Desktop gratuitamente](https://go.microsoft.com/fwlink/?LinkId=521662). Ou, para começar rapidamente, você pode baixar o [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547)(PBIX de exemplo de análise de varejo).

> [!NOTE]
> Para saber mais sobre como usar o **Power BI Desktop**, confira [Introdução ao Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop).

Com o **Power BI Desktop**, você se conecta à fonte de dados importando uma cópia dos dados para o **Power BI Desktop** ou se conectando diretamente à fonte de dados usando o **DirectQuery**.

Estas são as diferenças entre o uso de **Importar** e **DirectQuery**.

| Importar | DirectQuery |
| --- | --- |
| Tabelas, colunas, *e dados* são importados ou copiados para o **Power BI Desktop**. Ao trabalhar com visualizações, o **Power BI Desktop** consulta uma cópia dos dados. Para ver as alterações ocorridas nos dados subjacentes, você deve atualizar ou importar novamente um conjunto de dados completo e atual. |Somente *tabelas e colunas* são importadas ou copiadas para o **Power BI Desktop**. Ao trabalhar com as visualizações, o **Power BI Desktop** consulta a fonte de dados subjacente, o que significa que você sempre estará exibindo os dados atuais. |

Para saber mais sobre como se conectar a uma fonte de dados, confira [Conectar-se a uma fonte de dados](power-bi-embedded-connect-datasource.md).

Depois de salvar seu trabalho no **Power BI Desktop**, um arquivo PBIX será criado. Esse arquivo contém o relatório. Além disso, se você importar dados, o PBIX conterá o conjunto de dados completo, mas se usar o **DirectQuery**, o PBIX conterá apenas um esquema de conjunto de dados. Implante o PBIX em seu espaço de trabalho programaticamente usando a [API de importação do Power BI](https://msdn.microsoft.com/library/mt711504.aspx).

> [!NOTE]
> **Power BI Embedded** tem APIs adicionais para alterar o servidor e o banco de dados para onde seu conjunto de dados está apontando e para definir uma credencial da conta de serviço que o conjunto de dados usará a fim de se conectar ao banco de dados. Confira [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) e [Correção de fonte de dados do gateway](https://msdn.microsoft.com/library/mt711498.aspx).

## <a name="create-power-bi-datasets-and-reports-using-apis"></a>Criar relatórios e conjuntos de dados do Power BI usando APIs

### <a name="datsets"></a>Conjuntos de dados

Você pode criar conjuntos de dados no Power BI Embedded usando a API REST. Em seguida, você pode enviar dados por push para seu conjunto de dados. Isso permite que você trabalhe com dados sem a necessidade do Power BI Desktop. Para saber mais, veja [Postar conjuntos de dados](https://msdn.microsoft.com/library/azure/mt778875.aspx).

### <a name="reports"></a>Relatórios

Você pode criar um relatório de um conjunto de dados diretamente em seu aplicativo usando a API de JavaScript. Para saber mais, veja [Criar um novo relatório de um conjunto de dados no Power BI Embedded](power-bi-embedded-create-report-from-dataset.md).

## <a name="see-also"></a>Consulte também

[Introdução a exemplos](power-bi-embedded-get-started-sample.md)  
[Autenticando e autorizando com o Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Inserir um relatório](power-bi-embedded-embed-report.md)  
[Criar um novo relatório de um conjunto de dados no Power BI Embedded](power-bi-embedded-create-report-from-dataset.md)
[Salvar relatórios](power-bi-embedded-save-reports.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[Amostra de inserção de JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
Mais perguntas? [Experimentar a comunidade do Power BI](http://community.powerbi.com/)

