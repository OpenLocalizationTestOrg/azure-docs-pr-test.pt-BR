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
# <a name="row-level-security-with-power-bi-embedded"></a><span data-ttu-id="7e1ab-103">Segurança de nível de linha com o Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="7e1ab-103">Row level security with Power BI Embedded</span></span>

<span data-ttu-id="7e1ab-104">Segurança em nível de linha (RLS) pode ser usado toorestrict usuário acessar tooparticular dados dentro de um relatório ou conjunto de dados, permitindo para toouse de vários usuários diferentes Olá mesmo relatório ao ver todos os dados de diferentes.</span><span class="sxs-lookup"><span data-stu-id="7e1ab-104">Row level security (RLS) can be used toorestrict user access tooparticular data within a report or dataset, allowing for multiple different users toouse hello same report while all seeing different data.</span></span> <span data-ttu-id="7e1ab-105">O Power BI Embedded agora dá suporte a conjuntos de dados configurados com RLS.</span><span class="sxs-lookup"><span data-stu-id="7e1ab-105">Power BI Embedded now supports datasets configured with RLS.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-flow-1.png)

<span data-ttu-id="7e1ab-106">Em ordem tootake as vantagens do RLS, é importante que compreender os três conceitos principais; Os usuários, funções e regras.</span><span class="sxs-lookup"><span data-stu-id="7e1ab-106">In order tootake advantage of RLS, it’s important you understand three main concepts; Users, Roles, and Rules.</span></span> <span data-ttu-id="7e1ab-107">Vamos examinar cada um com mais detalhes:</span><span class="sxs-lookup"><span data-stu-id="7e1ab-107">Let’s take a closer look at each:</span></span>

<span data-ttu-id="7e1ab-108">**Os usuários** – estes são os usuários finais real de saudação exibir relatórios.</span><span class="sxs-lookup"><span data-stu-id="7e1ab-108">**Users** –  These are hello actual end-users viewing reports.</span></span> <span data-ttu-id="7e1ab-109">No Power BI inserido, os usuários são identificados pela propriedade de nome de usuário de saudação em um Token de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7e1ab-109">In Power BI Embedded, users are identified by hello username property in an App Token.</span></span>

<span data-ttu-id="7e1ab-110">**Funções** – os usuários pertencem tooroles.</span><span class="sxs-lookup"><span data-stu-id="7e1ab-110">**Roles** – Users belong tooroles.</span></span> <span data-ttu-id="7e1ab-111">Uma função é um contêiner de regras e pode ter um nome como "Gerente de vendas" ou "Representante de vendas".</span><span class="sxs-lookup"><span data-stu-id="7e1ab-111">A role is a container for rules and can be named something like “Sales Manager” or “Sales Rep”.</span></span> <span data-ttu-id="7e1ab-112">No Power BI inserido, os usuários são identificados pela propriedade de funções hello em um Token de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7e1ab-112">In Power BI Embedded, users are identified by hello roles property in an App Token.</span></span>

<span data-ttu-id="7e1ab-113">**Regras de** – funções têm regras, e essas regras são filtros Olá real forem toobe aplicada toohello dados.</span><span class="sxs-lookup"><span data-stu-id="7e1ab-113">**Rules** – Roles have rules, and those rules are hello actual filters that are going toobe applied toohello data.</span></span> <span data-ttu-id="7e1ab-114">Isso pode ser tão simples quanto "País = EUA" ou algo muito mais dinâmico.</span><span class="sxs-lookup"><span data-stu-id="7e1ab-114">This could be as simple as “Country = USA” or something much more dynamic.</span></span>

### <a name="example"></a><span data-ttu-id="7e1ab-115">Exemplo</span><span class="sxs-lookup"><span data-stu-id="7e1ab-115">Example</span></span>

<span data-ttu-id="7e1ab-116">Para rest Olá deste artigo, forneceremos um exemplo de RLS de criação e, em seguida, consumindo que dentro de um aplicativo incorporado.</span><span class="sxs-lookup"><span data-stu-id="7e1ab-116">For hello rest of this article, we’ll provide an example of authoring RLS, and then consuming that within an embedded application.</span></span> <span data-ttu-id="7e1ab-117">Usa o nosso exemplo hello [exemplo de análise de varejo](http://go.microsoft.com/fwlink/?LinkID=780547) arquivo PBIX.</span><span class="sxs-lookup"><span data-stu-id="7e1ab-117">Our example uses hello [Retail Analysis Sample](http://go.microsoft.com/fwlink/?LinkID=780547) PBIX file.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-scenario-2.png)

<span data-ttu-id="7e1ab-118">Nosso exemplo de análise de varejo mostra as vendas de todos os repositórios de saudação em uma cadeia de varejo específico.</span><span class="sxs-lookup"><span data-stu-id="7e1ab-118">Our Retail Analysis sample shows sales for all hello stores in a particular retail chain.</span></span> <span data-ttu-id="7e1ab-119">Sem RLS, não importa qual Distrito manager entra e exibições hello relatório, ele verá Olá os mesmos dados.</span><span class="sxs-lookup"><span data-stu-id="7e1ab-119">Without RLS, no matter which district manager signs in and views hello report, they’ll see hello same data.</span></span> <span data-ttu-id="7e1ab-120">Gerenciamento sênior determinou que cada gerente regional deverão ver apenas Olá vendas para lojas Olá gerenciam e toodo isso, podemos usar RLS.</span><span class="sxs-lookup"><span data-stu-id="7e1ab-120">Senior management has determined each district manager should only see hello sales for hello stores they manage, and toodo this, we can use RLS.</span></span>

<span data-ttu-id="7e1ab-121">A RLS é criada no Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="7e1ab-121">RLS is authored in Power BI Desktop.</span></span> <span data-ttu-id="7e1ab-122">Quando a saudação de conjunto de dados e relatórios são abertos, é possível alternar toosee toodiagram exibir o esquema de saudação:</span><span class="sxs-lookup"><span data-stu-id="7e1ab-122">When hello dataset and report are opened, we can switch toodiagram view toosee hello schema:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-3.png)

<span data-ttu-id="7e1ab-123">Aqui estão alguns toonotice coisas com esse esquema:</span><span class="sxs-lookup"><span data-stu-id="7e1ab-123">Here are a few things toonotice with this schema:</span></span>

* <span data-ttu-id="7e1ab-124">Todas as medidas, como **Total de vendas**, são armazenados no hello **vendas** tabela de fatos.</span><span class="sxs-lookup"><span data-stu-id="7e1ab-124">All measures, like **Total Sales**, are stored in hello **Sales** fact table.</span></span>
* <span data-ttu-id="7e1ab-125">Há quatro tabelas de dimensões adicionais relacionadas: **Item**, **Hora**, **Loja** e **Região**.</span><span class="sxs-lookup"><span data-stu-id="7e1ab-125">There are four additional related dimension tables: **Item**, **Time**, **Store**, and **District**.</span></span>
* <span data-ttu-id="7e1ab-126">setas de saudação nas linhas de relação Olá indicam como filtros podem fluir de tooanother de uma tabela.</span><span class="sxs-lookup"><span data-stu-id="7e1ab-126">hello arrows on hello relationship lines indicate which way filters can flow from one table tooanother.</span></span> <span data-ttu-id="7e1ab-127">Por exemplo, se um filtro for colocado em **hora [Data]**, no esquema atual Olá ele seria apenas filtrar valores em Olá **vendas** tabela.</span><span class="sxs-lookup"><span data-stu-id="7e1ab-127">For example, if a filter is placed on **Time[Date]**, in hello current schema it would only filter down values in hello **Sales** table.</span></span> <span data-ttu-id="7e1ab-128">Nenhuma outra tabela seria afetada por esse filtro desde que todas as setas Olá na tabela de vendas do hello relação linhas toohello ponto e não ausente.</span><span class="sxs-lookup"><span data-stu-id="7e1ab-128">No other tables would be affected by this filter since all of hello arrows on hello relationship lines point toohello sales table and not away.</span></span>
* <span data-ttu-id="7e1ab-129">Olá **Distrito** tabela indica quem é o gerente de saudação para cada Distrito:</span><span class="sxs-lookup"><span data-stu-id="7e1ab-129">hello **District** table indicates who hello manager is for each district:</span></span>
  
  ![](media/power-bi-embedded-rls/pbi-embedded-rls-district-table-4.png)

<span data-ttu-id="7e1ab-130">Com base neste esquema, se conseguimos aplicar um filtro toohello **gerente regional** coluna Olá tabela regional e se esse filtro corresponder usuário Olá exibindo relatório hello, esse filtro também filtrará inativo saudação **repositório**e **vendas** tooonly tabelas mostram dados de que determinado Distrito manager.</span><span class="sxs-lookup"><span data-stu-id="7e1ab-130">Based on this schema, if we apply a filter toohello **District Manager** column in hello District table, and if that filter matches hello user viewing hello report, that filter will also filter down hello **Store** and **Sales** tables tooonly show data for that particular district manager.</span></span>

<span data-ttu-id="7e1ab-131">Veja como fazer isso:</span><span class="sxs-lookup"><span data-stu-id="7e1ab-131">Here’s how:</span></span>

1. <span data-ttu-id="7e1ab-132">Na guia de modelagem hello, clique em **gerenciar funções**.</span><span class="sxs-lookup"><span data-stu-id="7e1ab-132">On hello Modeling tab, click **Manage Roles**.</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-modeling-tab-5.png)
2. <span data-ttu-id="7e1ab-133">Criar uma nova função chamada **Gerente**.</span><span class="sxs-lookup"><span data-stu-id="7e1ab-133">Create a new role called **Manager**.</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-6.png)
3. <span data-ttu-id="7e1ab-134">Em Olá **Distrito** tabela insira Olá expressão DAX a seguir: **[gerente regional] = username)**</span><span class="sxs-lookup"><span data-stu-id="7e1ab-134">In hello **District** table enter hello following DAX expression: **[District Manager] = USERNAME()**</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-7.png)
4. <span data-ttu-id="7e1ab-135">regras de saudação se toomake estão trabalhando, Olá **modelagem** , clique em **exibir como funções**e digite Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="7e1ab-135">toomake sure hello rules are working, on hello **Modeling** tab, click **View as Roles**, and then enter hello following:</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-view-as-roles-8.png)
   
   <span data-ttu-id="7e1ab-136">Olá relatórios agora mostrará dados como se você entrou como **Andrew Ma**.</span><span class="sxs-lookup"><span data-stu-id="7e1ab-136">hello reports will now show data as if you were signed in as **Andrew Ma**.</span></span>

<span data-ttu-id="7e1ab-137">Aplicar filtro hello, forma Olá fizemos aqui, filtre para baixo de todos os registros no hello **Distrito**, **repositório**, e **vendas** tabelas.</span><span class="sxs-lookup"><span data-stu-id="7e1ab-137">Applying hello filter, hello way we did here, will filter down all records in hello **District**, **Store**, and **Sales** tables.</span></span> <span data-ttu-id="7e1ab-138">No entanto, devido a direção do filtro Olá em relações de saudação entre **vendas** e **tempo**, **vendas** e **Item**e **Item** e **tempo** tabelas não serão filtradas para baixo.</span><span class="sxs-lookup"><span data-stu-id="7e1ab-138">However, because of hello filter direction on hello relationships between **Sales** and **Time**, **Sales** and **Item**, and **Item** and **Time** tables will not be filtered down.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-9.png)

<span data-ttu-id="7e1ab-139">Que pode ser okey para este requisito, no entanto, se não queremos gerenciadores toosee itens para os quais não têm nenhuma venda, foi possível ativar a filtragem cruzada para Olá relação e fluxo Olá filtro de segurança em ambas as direções bidirecional.</span><span class="sxs-lookup"><span data-stu-id="7e1ab-139">That may be ok for this requirement, however, if we don’t want managers toosee items for which they don’t have any sales, we could turn on bidirectional cross-filtering for hello relationship and flow hello security filter in both directions.</span></span> <span data-ttu-id="7e1ab-140">Isso pode ser feito editando relação Olá entre **vendas** e **Item**, assim:</span><span class="sxs-lookup"><span data-stu-id="7e1ab-140">This can be done by editing hello relationship between **Sales** and **Item**, like this:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-edit-relationship-10.png)

<span data-ttu-id="7e1ab-141">Agora, os filtros também podem fluir de Olá vendas tabela toohello **Item** tabela:</span><span class="sxs-lookup"><span data-stu-id="7e1ab-141">Now, filters can also flow from hello Sales table toohello **Item** table:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-11.png)

> [!NOTE]
> <span data-ttu-id="7e1ab-142">Se você estiver usando o modo DirectQuery para seus dados, você precisará tooenable bidirecional cruz filtragem selecionando essas duas opções:</span><span class="sxs-lookup"><span data-stu-id="7e1ab-142">If you're using DirectQuery mode for your data, you will need tooenable bidirectional-cross filtering by selecting these two options:</span></span>

1. <span data-ttu-id="7e1ab-143">**Arquivo** -> **Opções e Configurações** -> **Recursos de Visualização** -> **Habilitar filtragem cruzada em ambas as direções para DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="7e1ab-143">**File** -> **Options and Settings** -> **Preview Features** -> **Enable cross filtering in both directions for DirectQuery**.</span></span>
2. <span data-ttu-id="7e1ab-144">**Arquivo** -> **Opções e Configurações** -> **DirectQuery** -> **Permitir medidas irrestritas no modo DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="7e1ab-144">**File** -> **Options and Settings** -> **DirectQuery** -> **Allow unrestricted measure in DirectQuery mode**.</span></span>

<span data-ttu-id="7e1ab-145">toolearn mais informações sobre filtragem cruzada bidirecional, download Olá [a filtragem cruzada bidirecional no SQL Server Analysis Services 2016 e Power BI Desktop](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx) white paper.</span><span class="sxs-lookup"><span data-stu-id="7e1ab-145">toolearn more about bidirectional cross-filtering, download hello [Bidirectional cross-filtering in SQL Server Analysis Services 2016 and Power BI Desktop](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx) whitepaper.</span></span>

<span data-ttu-id="7e1ab-146">Isso conclui todo o trabalho Olá que precisa toobe feito no Power BI Desktop, mas não há um mais trabalho que precisa toomake toobe feito Olá RLS regras definimos o trabalho no Power BI inserido.</span><span class="sxs-lookup"><span data-stu-id="7e1ab-146">This wraps up all hello work that needs toobe done in Power BI Desktop, but there’s one more piece of work that needs toobe done toomake hello RLS rules we defined work in Power BI Embedded.</span></span> <span data-ttu-id="7e1ab-147">Os usuários são autenticados e autorizados por seu aplicativo e tokens de aplicativo são usado toogrant usuário acesso tooa Power BI inserido relatório específico.</span><span class="sxs-lookup"><span data-stu-id="7e1ab-147">Users are authenticated and authorized by your application and App tokens are used toogrant that user access tooa specific Power BI Embedded report.</span></span> <span data-ttu-id="7e1ab-148">O Power BI Embedded não tem nenhuma informação específica sobre quem é o usuário.</span><span class="sxs-lookup"><span data-stu-id="7e1ab-148">Power BI Embedded doesn’t have any specific information on who your user is.</span></span> <span data-ttu-id="7e1ab-149">Para toowork RLS, você precisará toopass algum contexto adicional como parte de seu token de aplicativo:</span><span class="sxs-lookup"><span data-stu-id="7e1ab-149">For RLS toowork, you’ll need toopass some additional context as part of your app token:</span></span>

* <span data-ttu-id="7e1ab-150">**nome de usuário** (opcional) – este usado com a RLS é uma cadeia de caracteres que pode ser usada toohelp identificar usuário Olá ao aplicar regras RLS.</span><span class="sxs-lookup"><span data-stu-id="7e1ab-150">**username** (optional) – Used with RLS this is a string that can be used toohelp identify hello user when applying RLS rules.</span></span> <span data-ttu-id="7e1ab-151">Confira Usando segurança de nível de linha com o Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="7e1ab-151">See Using Row Level Security with Power BI Embedded</span></span>
* <span data-ttu-id="7e1ab-152">**funções** – uma cadeia de caracteres que contém a saudação funções tooselect ao aplicar regras de segurança em nível de linha.</span><span class="sxs-lookup"><span data-stu-id="7e1ab-152">**roles** – A string containing hello roles tooselect when applying Row Level Security rules.</span></span> <span data-ttu-id="7e1ab-153">Ao transmitir mais de uma função, elas deverão ser transmitidas como uma matriz de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="7e1ab-153">If passing more than one role, they should be passed as a string array.</span></span>

<span data-ttu-id="7e1ab-154">Criar o token hello usando Olá [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__) método.</span><span class="sxs-lookup"><span data-stu-id="7e1ab-154">You create hello token by using hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__) method.</span></span> <span data-ttu-id="7e1ab-155">Se a propriedade de nome de usuário Olá estiver presente, você também deve passar pelo menos um valor em funções.</span><span class="sxs-lookup"><span data-stu-id="7e1ab-155">If hello username property is present, you must also pass at least one value in roles.</span></span>

<span data-ttu-id="7e1ab-156">Por exemplo, você pode alterar Olá EmbedSample.</span><span class="sxs-lookup"><span data-stu-id="7e1ab-156">For example, you could change hello EmbedSample.</span></span> <span data-ttu-id="7e1ab-157">A linha 55 DashboardController pode ser atualizada de</span><span class="sxs-lookup"><span data-stu-id="7e1ab-157">DashboardController line 55 could be updated from</span></span>

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id);

<span data-ttu-id="7e1ab-158">para</span><span class="sxs-lookup"><span data-stu-id="7e1ab-158">to</span></span>

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id, "Andrew Ma", ["Manager"]);'

<span data-ttu-id="7e1ab-159">token de aplicativo completo Olá será parecida com isto:</span><span class="sxs-lookup"><span data-stu-id="7e1ab-159">hello full app token will look something like this:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-app-token-string-12.png)

<span data-ttu-id="7e1ab-160">Agora, com todas as partes da saudação juntas, quando alguém fizer em nosso aplicativo tooview neste relatório, eles só serão toosee capaz de dados de saudação que eles são permitidos toosee, conforme definido pela nossa segurança em nível de linha.</span><span class="sxs-lookup"><span data-stu-id="7e1ab-160">Now, with all hello pieces together, when someone logs into our application tooview this report, they’ll only be able toosee hello data that they are allowed toosee, as defined by our row-level security.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-dashboard-13.png)

## <a name="see-also"></a><span data-ttu-id="7e1ab-161">Consulte também</span><span class="sxs-lookup"><span data-stu-id="7e1ab-161">See also</span></span>

[<span data-ttu-id="7e1ab-162">RLS (segurança no nível da linha) com Power</span><span class="sxs-lookup"><span data-stu-id="7e1ab-162">Row-level security (RLS) with Power</span></span>](https://powerbi.microsoft.com/en-us/documentation/powerbi-admin-rls/)  
[<span data-ttu-id="7e1ab-163">Autenticando e autorizando com o Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="7e1ab-163">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="7e1ab-164">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="7e1ab-164">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="7e1ab-165">Amostra de inserção de JavaScript</span><span class="sxs-lookup"><span data-stu-id="7e1ab-165">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="7e1ab-166">Mais perguntas?</span><span class="sxs-lookup"><span data-stu-id="7e1ab-166">More questions?</span></span> [<span data-ttu-id="7e1ab-167">Tente Olá comunidade do Power BI</span><span class="sxs-lookup"><span data-stu-id="7e1ab-167">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

