---
title: "segurança em nível de aaaRow com o Power BI Embedded"
description: "Detalhes sobre segurança de nível de linha com o Power BI Embedded"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 7936ade5-2c75-435b-8314-ea7ca815867a
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 384f78826ecc710cf8f101b251ae68b074f3e98b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="row-level-security-with-power-bi-embedded"></a>Segurança de nível de linha com o Power BI Embedded

Segurança em nível de linha (RLS) pode ser usado toorestrict usuário acessar tooparticular dados dentro de um relatório ou conjunto de dados, permitindo para toouse de vários usuários diferentes Olá mesmo relatório ao ver todos os dados de diferentes. O Power BI Embedded agora dá suporte a conjuntos de dados configurados com RLS.

![](media/power-bi-embedded-rls/pbi-embedded-rls-flow-1.png)

Em ordem tootake as vantagens do RLS, é importante que compreender os três conceitos principais; Os usuários, funções e regras. Vamos examinar cada um com mais detalhes:

**Os usuários** – estes são os usuários finais real de saudação exibir relatórios. No Power BI inserido, os usuários são identificados pela propriedade de nome de usuário de saudação em um Token de aplicativo.

**Funções** – os usuários pertencem tooroles. Uma função é um contêiner de regras e pode ter um nome como "Gerente de vendas" ou "Representante de vendas". No Power BI inserido, os usuários são identificados pela propriedade de funções hello em um Token de aplicativo.

**Regras de** – funções têm regras, e essas regras são filtros Olá real forem toobe aplicada toohello dados. Isso pode ser tão simples quanto "País = EUA" ou algo muito mais dinâmico.

### <a name="example"></a>Exemplo

Para rest Olá deste artigo, forneceremos um exemplo de RLS de criação e, em seguida, consumindo que dentro de um aplicativo incorporado. Usa o nosso exemplo hello [exemplo de análise de varejo](http://go.microsoft.com/fwlink/?LinkID=780547) arquivo PBIX.

![](media/power-bi-embedded-rls/pbi-embedded-rls-scenario-2.png)

Nosso exemplo de análise de varejo mostra as vendas de todos os repositórios de saudação em uma cadeia de varejo específico. Sem RLS, não importa qual Distrito manager entra e exibições hello relatório, ele verá Olá os mesmos dados. Gerenciamento sênior determinou que cada gerente regional deverão ver apenas Olá vendas para lojas Olá gerenciam e toodo isso, podemos usar RLS.

A RLS é criada no Power BI Desktop. Quando a saudação de conjunto de dados e relatórios são abertos, é possível alternar toosee toodiagram exibir o esquema de saudação:

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-3.png)

Aqui estão alguns toonotice coisas com esse esquema:

* Todas as medidas, como **Total de vendas**, são armazenados no hello **vendas** tabela de fatos.
* Há quatro tabelas de dimensões adicionais relacionadas: **Item**, **Hora**, **Loja** e **Região**.
* setas de saudação nas linhas de relação Olá indicam como filtros podem fluir de tooanother de uma tabela. Por exemplo, se um filtro for colocado em **hora [Data]**, no esquema atual Olá ele seria apenas filtrar valores em Olá **vendas** tabela. Nenhuma outra tabela seria afetada por esse filtro desde que todas as setas Olá na tabela de vendas do hello relação linhas toohello ponto e não ausente.
* Olá **Distrito** tabela indica quem é o gerente de saudação para cada Distrito:
  
  ![](media/power-bi-embedded-rls/pbi-embedded-rls-district-table-4.png)

Com base neste esquema, se conseguimos aplicar um filtro toohello **gerente regional** coluna Olá tabela regional e se esse filtro corresponder usuário Olá exibindo relatório hello, esse filtro também filtrará inativo saudação **repositório**e **vendas** tooonly tabelas mostram dados de que determinado Distrito manager.

Veja como fazer isso:

1. Na guia de modelagem hello, clique em **gerenciar funções**.  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-modeling-tab-5.png)
2. Criar uma nova função chamada **Gerente**.  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-6.png)
3. Em Olá **Distrito** tabela insira Olá expressão DAX a seguir: **[gerente regional] = username)**  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-7.png)
4. regras de saudação se toomake estão trabalhando, Olá **modelagem** , clique em **exibir como funções**e digite Olá seguinte:  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-view-as-roles-8.png)
   
   Olá relatórios agora mostrará dados como se você entrou como **Andrew Ma**.

Aplicar filtro hello, forma Olá fizemos aqui, filtre para baixo de todos os registros no hello **Distrito**, **repositório**, e **vendas** tabelas. No entanto, devido a direção do filtro Olá em relações de saudação entre **vendas** e **tempo**, **vendas** e **Item**e **Item** e **tempo** tabelas não serão filtradas para baixo.

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-9.png)

Que pode ser okey para este requisito, no entanto, se não queremos gerenciadores toosee itens para os quais não têm nenhuma venda, foi possível ativar a filtragem cruzada para Olá relação e fluxo Olá filtro de segurança em ambas as direções bidirecional. Isso pode ser feito editando relação Olá entre **vendas** e **Item**, assim:

![](media/power-bi-embedded-rls/pbi-embedded-rls-edit-relationship-10.png)

Agora, os filtros também podem fluir de Olá vendas tabela toohello **Item** tabela:

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-11.png)

> [!NOTE]
> Se você estiver usando o modo DirectQuery para seus dados, você precisará tooenable bidirecional cruz filtragem selecionando essas duas opções:

1. **Arquivo** -> **Opções e Configurações** -> **Recursos de Visualização** -> **Habilitar filtragem cruzada em ambas as direções para DirectQuery**.
2. **Arquivo** -> **Opções e Configurações** -> **DirectQuery** -> **Permitir medidas irrestritas no modo DirectQuery**.

toolearn mais informações sobre filtragem cruzada bidirecional, download Olá [a filtragem cruzada bidirecional no SQL Server Analysis Services 2016 e Power BI Desktop](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx) white paper.

Isso conclui todo o trabalho Olá que precisa toobe feito no Power BI Desktop, mas não há um mais trabalho que precisa toomake toobe feito Olá RLS regras definimos o trabalho no Power BI inserido. Os usuários são autenticados e autorizados por seu aplicativo e tokens de aplicativo são usado toogrant usuário acesso tooa Power BI inserido relatório específico. O Power BI Embedded não tem nenhuma informação específica sobre quem é o usuário. Para toowork RLS, você precisará toopass algum contexto adicional como parte de seu token de aplicativo:

* **nome de usuário** (opcional) – este usado com a RLS é uma cadeia de caracteres que pode ser usada toohelp identificar usuário Olá ao aplicar regras RLS. Confira Usando segurança de nível de linha com o Power BI Embedded
* **funções** – uma cadeia de caracteres que contém a saudação funções tooselect ao aplicar regras de segurança em nível de linha. Ao transmitir mais de uma função, elas deverão ser transmitidas como uma matriz de cadeia de caracteres.

Criar o token hello usando Olá [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__) método. Se a propriedade de nome de usuário Olá estiver presente, você também deve passar pelo menos um valor em funções.

Por exemplo, você pode alterar Olá EmbedSample. A linha 55 DashboardController pode ser atualizada de

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id);

para

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id, "Andrew Ma", ["Manager"]);'

token de aplicativo completo Olá será parecida com isto:

![](media/power-bi-embedded-rls/pbi-embedded-rls-app-token-string-12.png)

Agora, com todas as partes da saudação juntas, quando alguém fizer em nosso aplicativo tooview neste relatório, eles só serão toosee capaz de dados de saudação que eles são permitidos toosee, conforme definido pela nossa segurança em nível de linha.

![](media/power-bi-embedded-rls/pbi-embedded-rls-dashboard-13.png)

## <a name="see-also"></a>Consulte também

[RLS (segurança no nível da linha) com Power](https://powerbi.microsoft.com/en-us/documentation/powerbi-admin-rls/)  
[Autenticando e autorizando com o Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[Amostra de inserção de JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
Mais perguntas? [Tente Olá comunidade do Power BI](http://community.powerbi.com/)

