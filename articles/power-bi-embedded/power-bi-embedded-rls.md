---
title: "Segurança de nível de linha com o Power BI Embedded"
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
ms.openlocfilehash: 1cde5b9ee4c716af07d427d4d0eb3f0775d456ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="row-level-security-with-power-bi-embedded"></a><span data-ttu-id="6c8d6-103">Segurança de nível de linha com o Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="6c8d6-103">Row level security with Power BI Embedded</span></span>

<span data-ttu-id="6c8d6-104">A RLS (segurança em nível de linha) pode ser usada para restringir o acesso do usuário a dados específicos em um relatório ou conjunto de dados, permitindo que vários usuários diferentes usem o mesmo relatório, mas vendo dados diferentes.</span><span class="sxs-lookup"><span data-stu-id="6c8d6-104">Row level security (RLS) can be used to restrict user access to particular data within a report or dataset, allowing for multiple different users to use the same report while all seeing different data.</span></span> <span data-ttu-id="6c8d6-105">O Power BI Embedded agora dá suporte a conjuntos de dados configurados com RLS.</span><span class="sxs-lookup"><span data-stu-id="6c8d6-105">Power BI Embedded now supports datasets configured with RLS.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-flow-1.png)

<span data-ttu-id="6c8d6-106">Para tirar proveito da RLS, é importante compreender os três conceitos principais: usuários, funções e regras.</span><span class="sxs-lookup"><span data-stu-id="6c8d6-106">In order to take advantage of RLS, it’s important you understand three main concepts; Users, Roles, and Rules.</span></span> <span data-ttu-id="6c8d6-107">Vamos examinar cada um com mais detalhes:</span><span class="sxs-lookup"><span data-stu-id="6c8d6-107">Let’s take a closer look at each:</span></span>

<span data-ttu-id="6c8d6-108">**Usuários** – são os usuários finais reais que exibem os relatórios.</span><span class="sxs-lookup"><span data-stu-id="6c8d6-108">**Users** –  These are the actual end-users viewing reports.</span></span> <span data-ttu-id="6c8d6-109">No Power BI Embedded, os usuários são identificados pela propriedade Nome de usuário em um Token de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6c8d6-109">In Power BI Embedded, users are identified by the username property in an App Token.</span></span>

<span data-ttu-id="6c8d6-110">**Funções** – os usuários pertencem a funções.</span><span class="sxs-lookup"><span data-stu-id="6c8d6-110">**Roles** – Users belong to roles.</span></span> <span data-ttu-id="6c8d6-111">Uma função é um contêiner de regras e pode ter um nome como "Gerente de vendas" ou "Representante de vendas".</span><span class="sxs-lookup"><span data-stu-id="6c8d6-111">A role is a container for rules and can be named something like “Sales Manager” or “Sales Rep”.</span></span> <span data-ttu-id="6c8d6-112">No Power BI Embedded, os usuários são identificados pela propriedade Funções em um Token de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6c8d6-112">In Power BI Embedded, users are identified by the roles property in an App Token.</span></span>

<span data-ttu-id="6c8d6-113">**Regras** – funções têm regras e essas regras são os filtros reais aplicados aos dados.</span><span class="sxs-lookup"><span data-stu-id="6c8d6-113">**Rules** – Roles have rules, and those rules are the actual filters that are going to be applied to the data.</span></span> <span data-ttu-id="6c8d6-114">Isso pode ser tão simples quanto "País = EUA" ou algo muito mais dinâmico.</span><span class="sxs-lookup"><span data-stu-id="6c8d6-114">This could be as simple as “Country = USA” or something much more dynamic.</span></span>

### <a name="example"></a><span data-ttu-id="6c8d6-115">Exemplo</span><span class="sxs-lookup"><span data-stu-id="6c8d6-115">Example</span></span>

<span data-ttu-id="6c8d6-116">Para o restante deste artigo, forneceremos um exemplo de criação de RLS e o usaremos em um aplicativo incorporado.</span><span class="sxs-lookup"><span data-stu-id="6c8d6-116">For the rest of this article, we’ll provide an example of authoring RLS, and then consuming that within an embedded application.</span></span> <span data-ttu-id="6c8d6-117">Nosso exemplo usa o arquivo PBIX [exemplo de análise de varejo](http://go.microsoft.com/fwlink/?LinkID=780547) .</span><span class="sxs-lookup"><span data-stu-id="6c8d6-117">Our example uses the [Retail Analysis Sample](http://go.microsoft.com/fwlink/?LinkID=780547) PBIX file.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-scenario-2.png)

<span data-ttu-id="6c8d6-118">Nosso exemplo de análise de varejo mostra as vendas para todas as lojas em uma cadeia de varejo específica.</span><span class="sxs-lookup"><span data-stu-id="6c8d6-118">Our Retail Analysis sample shows sales for all the stores in a particular retail chain.</span></span> <span data-ttu-id="6c8d6-119">Sem RLS, não importa que gerente regional entra e exibe o relatório; eles veem os mesmos dados.</span><span class="sxs-lookup"><span data-stu-id="6c8d6-119">Without RLS, no matter which district manager signs in and views the report, they’ll see the same data.</span></span> <span data-ttu-id="6c8d6-120">A cúpula sênior determinou que cada gerente regional veja apenas as vendas das lojas que eles gerenciam e, para fazer isso, podemos usar RLS.</span><span class="sxs-lookup"><span data-stu-id="6c8d6-120">Senior management has determined each district manager should only see the sales for the stores they manage, and to do this, we can use RLS.</span></span>

<span data-ttu-id="6c8d6-121">A RLS é criada no Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="6c8d6-121">RLS is authored in Power BI Desktop.</span></span> <span data-ttu-id="6c8d6-122">Quando o conjunto de dados e o relatório são abertos, podemos alternar para modo de exibição de diagrama a fim de ver o esquema:</span><span class="sxs-lookup"><span data-stu-id="6c8d6-122">When the dataset and report are opened, we can switch to diagram view to see the schema:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-3.png)

<span data-ttu-id="6c8d6-123">Eis algumas observações em relação a esse esquema:</span><span class="sxs-lookup"><span data-stu-id="6c8d6-123">Here are a few things to notice with this schema:</span></span>

* <span data-ttu-id="6c8d6-124">Todas as medidas, como **Total de vendas**, são armazenadas na tabela de fatos **Vendas**.</span><span class="sxs-lookup"><span data-stu-id="6c8d6-124">All measures, like **Total Sales**, are stored in the **Sales** fact table.</span></span>
* <span data-ttu-id="6c8d6-125">Há quatro tabelas de dimensões adicionais relacionadas: **Item**, **Hora**, **Loja** e **Região**.</span><span class="sxs-lookup"><span data-stu-id="6c8d6-125">There are four additional related dimension tables: **Item**, **Time**, **Store**, and **District**.</span></span>
* <span data-ttu-id="6c8d6-126">As setas nas linhas de relação indicam como os filtros podem fluir de uma tabela para outra.</span><span class="sxs-lookup"><span data-stu-id="6c8d6-126">The arrows on the relationship lines indicate which way filters can flow from one table to another.</span></span> <span data-ttu-id="6c8d6-127">Por exemplo, se um filtro é colocado em **Hora[Data]**, no esquema atual ele filtraria somente valores na tabela **Vendas**.</span><span class="sxs-lookup"><span data-stu-id="6c8d6-127">For example, if a filter is placed on **Time[Date]**, in the current schema it would only filter down values in the **Sales** table.</span></span> <span data-ttu-id="6c8d6-128">Nenhuma outra tabela seria afetada por esse filtro, já que todas as setas nas linhas de relação apontam em direção à tabela de vendas, e não para fora dela.</span><span class="sxs-lookup"><span data-stu-id="6c8d6-128">No other tables would be affected by this filter since all of the arrows on the relationship lines point to the sales table and not away.</span></span>
* <span data-ttu-id="6c8d6-129">A tabela **Região** indica quem é o gerente de cada região:</span><span class="sxs-lookup"><span data-stu-id="6c8d6-129">The **District** table indicates who the manager is for each district:</span></span>
  
  ![](media/power-bi-embedded-rls/pbi-embedded-rls-district-table-4.png)

<span data-ttu-id="6c8d6-130">Com base nesse esquema, se aplicamos um filtro na coluna**Gerente regional** e esse filtro corresponder ao usuário que exibe o relatório, ele também filtrará as tabelas **Loja** e **Vendas**, a fim de mostrar somente os dados relacionados ao gerente regional em questão.</span><span class="sxs-lookup"><span data-stu-id="6c8d6-130">Based on this schema, if we apply a filter to the **District Manager** column in the District table, and if that filter matches the user viewing the report, that filter will also filter down the **Store** and **Sales** tables to only show data for that particular district manager.</span></span>

<span data-ttu-id="6c8d6-131">Veja como fazer isso:</span><span class="sxs-lookup"><span data-stu-id="6c8d6-131">Here’s how:</span></span>

1. <span data-ttu-id="6c8d6-132">Na guia Modelagem, clique em **Gerenciar Funções**.</span><span class="sxs-lookup"><span data-stu-id="6c8d6-132">On the Modeling tab, click **Manage Roles**.</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-modeling-tab-5.png)
2. <span data-ttu-id="6c8d6-133">Criar uma nova função chamada **Gerente**.</span><span class="sxs-lookup"><span data-stu-id="6c8d6-133">Create a new role called **Manager**.</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-6.png)
3. <span data-ttu-id="6c8d6-134">Na tabela **Região**, insira a seguinte expressão DAX: **[District Manager] = Username()**</span><span class="sxs-lookup"><span data-stu-id="6c8d6-134">In the **District** table enter the following DAX expression: **[District Manager] = USERNAME()**</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-7.png)
4. <span data-ttu-id="6c8d6-135">Para verificar se as regras estão funcionando, na guia **Modelagem**, clique em **Exibir como Funções** e digite o seguinte:</span><span class="sxs-lookup"><span data-stu-id="6c8d6-135">To make sure the rules are working, on the **Modeling** tab, click **View as Roles**, and then enter the following:</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-view-as-roles-8.png)
   
   <span data-ttu-id="6c8d6-136">Os relatórios agora mostrarão dados como se você estivesse conectado como **Paulo Araújo**.</span><span class="sxs-lookup"><span data-stu-id="6c8d6-136">The reports will now show data as if you were signed in as **Andrew Ma**.</span></span>

<span data-ttu-id="6c8d6-137">A aplicação do filtro como fizemos aqui filtrará todos os registros nas tabelas **Região**, **Loja** e **Vendas**.</span><span class="sxs-lookup"><span data-stu-id="6c8d6-137">Applying the filter, the way we did here, will filter down all records in the **District**, **Store**, and **Sales** tables.</span></span> <span data-ttu-id="6c8d6-138">No entanto, devido à direção do filtro nas relações entre **Vendas** e **Hora**, as tabelas **Vendas** e **Item** e **Item** e **Hora** não serão filtradas.</span><span class="sxs-lookup"><span data-stu-id="6c8d6-138">However, because of the filter direction on the relationships between **Sales** and **Time**, **Sales** and **Item**, and **Item** and **Time** tables will not be filtered down.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-9.png)

<span data-ttu-id="6c8d6-139">Que podem ser adequadas para esse requisito; no entanto, se não quisermos que os gerentes vejam itens para os quais não têm vendas, poderíamos ativar a filtragem cruzada bidirecional a relação e fluir o filtro de segurança em ambos os sentidos.</span><span class="sxs-lookup"><span data-stu-id="6c8d6-139">That may be ok for this requirement, however, if we don’t want managers to see items for which they don’t have any sales, we could turn on bidirectional cross-filtering for the relationship and flow the security filter in both directions.</span></span> <span data-ttu-id="6c8d6-140">Isso pode ser feito editando a relação entre **Vendas** e **Item**, assim:</span><span class="sxs-lookup"><span data-stu-id="6c8d6-140">This can be done by editing the relationship between **Sales** and **Item**, like this:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-edit-relationship-10.png)

<span data-ttu-id="6c8d6-141">Agora, os filtros também podem fluir da tabela Vendas para a tabela **Item** :</span><span class="sxs-lookup"><span data-stu-id="6c8d6-141">Now, filters can also flow from the Sales table to the **Item** table:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-11.png)

> [!NOTE]
> <span data-ttu-id="6c8d6-142">Se você estiver usando o modo DirectQuery para seus dados, precisará habilitar a filtragem bidirecional selecionando estas duas opções:</span><span class="sxs-lookup"><span data-stu-id="6c8d6-142">If you're using DirectQuery mode for your data, you will need to enable bidirectional-cross filtering by selecting these two options:</span></span>

1. <span data-ttu-id="6c8d6-143">**Arquivo** -> **Opções e Configurações** -> **Recursos de Visualização** -> **Habilitar filtragem cruzada em ambas as direções para DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="6c8d6-143">**File** -> **Options and Settings** -> **Preview Features** -> **Enable cross filtering in both directions for DirectQuery**.</span></span>
2. <span data-ttu-id="6c8d6-144">**Arquivo** -> **Opções e Configurações** -> **DirectQuery** -> **Permitir medidas irrestritas no modo DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="6c8d6-144">**File** -> **Options and Settings** -> **DirectQuery** -> **Allow unrestricted measure in DirectQuery mode**.</span></span>

<span data-ttu-id="6c8d6-145">Para saber mais sobre filtragem cruzada bidirecional, baixe o whitepaper [Filtragem cruzada bidirecional no SQL Server Analysis Services 2016 e no Power BI Desktop](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx).</span><span class="sxs-lookup"><span data-stu-id="6c8d6-145">To learn more about bidirectional cross-filtering, download the [Bidirectional cross-filtering in SQL Server Analysis Services 2016 and Power BI Desktop](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx) whitepaper.</span></span>

<span data-ttu-id="6c8d6-146">Isso conclui todo o trabalho que precisa ser feito no Power BI Desktop, mas há um mais trabalho que precisa ser feito para tornar as regras de RLS definidas funcionarem no Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="6c8d6-146">This wraps up all the work that needs to be done in Power BI Desktop, but there’s one more piece of work that needs to be done to make the RLS rules we defined work in Power BI Embedded.</span></span> <span data-ttu-id="6c8d6-147">Os usuários são autenticados e autorizados pelo seu aplicativo e Tokens de Aplicativo são usados para conceder acesso de usuário a um relatório de Power BI Embedded específico.</span><span class="sxs-lookup"><span data-stu-id="6c8d6-147">Users are authenticated and authorized by your application and App tokens are used to grant that user access to a specific Power BI Embedded report.</span></span> <span data-ttu-id="6c8d6-148">O Power BI Embedded não tem nenhuma informação específica sobre quem é o usuário.</span><span class="sxs-lookup"><span data-stu-id="6c8d6-148">Power BI Embedded doesn’t have any specific information on who your user is.</span></span> <span data-ttu-id="6c8d6-149">Para que a RLS funcione, você precisará passar algum contexto adicional como parte de seu token do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="6c8d6-149">For RLS to work, you’ll need to pass some additional context as part of your app token:</span></span>

* <span data-ttu-id="6c8d6-150">**nome de usuário** (opcional) – usado com RLS, é uma cadeia de caracteres que pode ser usada para ajudar a identificar o usuário ao aplicar regras RLS.</span><span class="sxs-lookup"><span data-stu-id="6c8d6-150">**username** (optional) – Used with RLS this is a string that can be used to help identify the user when applying RLS rules.</span></span> <span data-ttu-id="6c8d6-151">Confira Usando segurança de nível de linha com o Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="6c8d6-151">See Using Row Level Security with Power BI Embedded</span></span>
* <span data-ttu-id="6c8d6-152">**funções** – uma cadeia de caracteres que contém as funções a selecionar ao aplicar regras de segurança em nível de linha.</span><span class="sxs-lookup"><span data-stu-id="6c8d6-152">**roles** – A string containing the roles to select when applying Row Level Security rules.</span></span> <span data-ttu-id="6c8d6-153">Ao transmitir mais de uma função, elas deverão ser transmitidas como uma matriz de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="6c8d6-153">If passing more than one role, they should be passed as a string array.</span></span>

<span data-ttu-id="6c8d6-154">Crie o token usando o método [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__).</span><span class="sxs-lookup"><span data-stu-id="6c8d6-154">You create the token by using the [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__) method.</span></span> <span data-ttu-id="6c8d6-155">Se a propriedade de nome de usuário estiver presente, você também deverá passar pelo menos um valor como funções.</span><span class="sxs-lookup"><span data-stu-id="6c8d6-155">If the username property is present, you must also pass at least one value in roles.</span></span>

<span data-ttu-id="6c8d6-156">Por exemplo, você pode alterar EmbedSample.</span><span class="sxs-lookup"><span data-stu-id="6c8d6-156">For example, you could change the EmbedSample.</span></span> <span data-ttu-id="6c8d6-157">A linha 55 DashboardController pode ser atualizada de</span><span class="sxs-lookup"><span data-stu-id="6c8d6-157">DashboardController line 55 could be updated from</span></span>

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id);

<span data-ttu-id="6c8d6-158">para</span><span class="sxs-lookup"><span data-stu-id="6c8d6-158">to</span></span>

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id, "Andrew Ma", ["Manager"]);'

<span data-ttu-id="6c8d6-159">O token do aplicativo completo será algo parecido com isto:</span><span class="sxs-lookup"><span data-stu-id="6c8d6-159">The full app token will look something like this:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-app-token-string-12.png)

<span data-ttu-id="6c8d6-160">Agora, com todas as partes juntas, quando alguém entrar em nosso aplicativo para exibir esse relatório, só poderá ver os dados que tiver permissão para ver, conforme definido pela nossa segurança em nível de linha.</span><span class="sxs-lookup"><span data-stu-id="6c8d6-160">Now, with all the pieces together, when someone logs into our application to view this report, they’ll only be able to see the data that they are allowed to see, as defined by our row-level security.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-dashboard-13.png)

## <a name="see-also"></a><span data-ttu-id="6c8d6-161">Confira também</span><span class="sxs-lookup"><span data-stu-id="6c8d6-161">See also</span></span>

[<span data-ttu-id="6c8d6-162">RLS (segurança no nível da linha) com Power</span><span class="sxs-lookup"><span data-stu-id="6c8d6-162">Row-level security (RLS) with Power</span></span>](https://powerbi.microsoft.com/en-us/documentation/powerbi-admin-rls/)  
[<span data-ttu-id="6c8d6-163">Autenticando e autorizando com o Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="6c8d6-163">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="6c8d6-164">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="6c8d6-164">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="6c8d6-165">Amostra de inserção de JavaScript</span><span class="sxs-lookup"><span data-stu-id="6c8d6-165">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="6c8d6-166">Mais perguntas?</span><span class="sxs-lookup"><span data-stu-id="6c8d6-166">More questions?</span></span> [<span data-ttu-id="6c8d6-167">Experimentar a comunidade do Power BI</span><span class="sxs-lookup"><span data-stu-id="6c8d6-167">Try the Power BI Community</span></span>](http://community.powerbi.com/)

