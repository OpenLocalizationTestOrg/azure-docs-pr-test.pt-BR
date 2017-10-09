---
title: "aaaConstructing cadeias de caracteres de filtro para o designer de tabela Olá | Microsoft Docs"
description: "Construindo cadeias de caracteres de filtro para o designer de tabela Olá"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: a1a10ea1-687a-4ee1-a952-6b24c2fe1a22
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 48b38d27b97936064daa875e41881d51546bc11f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="constructing-filter-strings-for-hello-table-designer"></a><span data-ttu-id="70154-103">Construindo cadeias de caracteres de filtro para Olá Designer de tabela</span><span class="sxs-lookup"><span data-stu-id="70154-103">Constructing Filter Strings for hello Table Designer</span></span>
## <a name="overview"></a><span data-ttu-id="70154-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="70154-104">Overview</span></span>
<span data-ttu-id="70154-105">Olá de toofilter dados em uma tabela do Azure que é exibido no Visual Studio **Designer de tabela**, construir uma cadeia de caracteres de filtro e insira-o no campo de filtro de saudação.</span><span class="sxs-lookup"><span data-stu-id="70154-105">toofilter data in an Azure table that is displayed in hello Visual Studio **Table Designer**, you construct a filter string and enter it into hello filter field.</span></span> <span data-ttu-id="70154-106">sintaxe de cadeia de caracteres de filtro de saudação é definido por Olá WCF Data Services e é semelhante tooa cláusula SQL WHERE, mas é enviada toohello serviço tabela por meio de uma solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="70154-106">hello filter string syntax is defined by hello WCF Data Services and is similar tooa SQL WHERE clause, but is sent toohello Table service via an HTTP request.</span></span> <span data-ttu-id="70154-107">Olá **Designer de tabela** identificadores Olá codificação adequada para você, caso toofilter em um valor de propriedade desejada, você só precisa inserir Olá nome de propriedade, o operador de comparação, valor de critérios, e, opcionalmente, o operador booleano no hello filtrar campo.</span><span class="sxs-lookup"><span data-stu-id="70154-107">hello **Table Designer** handles hello proper encoding for you, so toofilter on a desired property value, you need only enter hello property name, comparison operator, criteria value, and optionally, Boolean operator in hello filter field.</span></span> <span data-ttu-id="70154-108">Opção de consulta Olá $filter tooinclude não é necessário como você faria se foram construindo uma tabela de saudação do URL tooquery via Olá [referência de API de REST de serviços de armazenamento](http://go.microsoft.com/fwlink/p/?LinkId=400447).</span><span class="sxs-lookup"><span data-stu-id="70154-108">You do not need tooinclude hello $filter query option as you would if you were constructing a URL tooquery hello table via hello [Storage Services REST API Reference](http://go.microsoft.com/fwlink/p/?LinkId=400447).</span></span>

<span data-ttu-id="70154-109">Olá WCF Data Services se baseiam no hello [Open Data Protocol](http://go.microsoft.com/fwlink/p/?LinkId=214805) (OData).</span><span class="sxs-lookup"><span data-stu-id="70154-109">hello WCF Data Services are based on hello [Open Data Protocol](http://go.microsoft.com/fwlink/p/?LinkId=214805) (OData).</span></span> <span data-ttu-id="70154-110">Para obter detalhes sobre a opção de consulta do sistema de filtro de saudação (**$filter**), consulte Olá [especificação de convenções de URI do OData](http://go.microsoft.com/fwlink/p/?LinkId=214806).</span><span class="sxs-lookup"><span data-stu-id="70154-110">For details on hello filter system query option (**$filter**), see hello [OData URI Conventions specification](http://go.microsoft.com/fwlink/p/?LinkId=214806).</span></span>

## <a name="comparison-operators"></a><span data-ttu-id="70154-111">Operadores de comparação</span><span class="sxs-lookup"><span data-stu-id="70154-111">Comparison Operators</span></span>
<span data-ttu-id="70154-112">Olá seguintes operadores lógicos têm suporte para todos os tipos de propriedade:</span><span class="sxs-lookup"><span data-stu-id="70154-112">hello following logical operators are supported for all property types:</span></span>

| <span data-ttu-id="70154-113">Operador lógico</span><span class="sxs-lookup"><span data-stu-id="70154-113">Logical operator</span></span> | <span data-ttu-id="70154-114">Descrição</span><span class="sxs-lookup"><span data-stu-id="70154-114">Description</span></span> | <span data-ttu-id="70154-115">Cadeia de caracteres de filtro de exemplo</span><span class="sxs-lookup"><span data-stu-id="70154-115">Example filter string</span></span> |
| --- | --- | --- |
| <span data-ttu-id="70154-116">eq</span><span class="sxs-lookup"><span data-stu-id="70154-116">eq</span></span> |<span data-ttu-id="70154-117">Igual a</span><span class="sxs-lookup"><span data-stu-id="70154-117">Equal</span></span> |<span data-ttu-id="70154-118">City eq 'Redmond'</span><span class="sxs-lookup"><span data-stu-id="70154-118">City eq 'Redmond'</span></span> |
| <span data-ttu-id="70154-119">gt</span><span class="sxs-lookup"><span data-stu-id="70154-119">gt</span></span> |<span data-ttu-id="70154-120">Maior que</span><span class="sxs-lookup"><span data-stu-id="70154-120">Greater than</span></span> |<span data-ttu-id="70154-121">Preço gt 20</span><span class="sxs-lookup"><span data-stu-id="70154-121">Price gt 20</span></span> |
| <span data-ttu-id="70154-122">ge</span><span class="sxs-lookup"><span data-stu-id="70154-122">ge</span></span> |<span data-ttu-id="70154-123">Maior que ou igual muito</span><span class="sxs-lookup"><span data-stu-id="70154-123">Greater than or equal too</span></span>|<span data-ttu-id="70154-124">Preço ge 10</span><span class="sxs-lookup"><span data-stu-id="70154-124">Price ge 10</span></span> |
| <span data-ttu-id="70154-125">lt</span><span class="sxs-lookup"><span data-stu-id="70154-125">lt</span></span> |<span data-ttu-id="70154-126">Menor que</span><span class="sxs-lookup"><span data-stu-id="70154-126">Less than</span></span> |<span data-ttu-id="70154-127">Preço lt 20</span><span class="sxs-lookup"><span data-stu-id="70154-127">Price lt 20</span></span> |
| <span data-ttu-id="70154-128">le</span><span class="sxs-lookup"><span data-stu-id="70154-128">le</span></span> |<span data-ttu-id="70154-129">Menor ou igual a</span><span class="sxs-lookup"><span data-stu-id="70154-129">Less than or equal</span></span> |<span data-ttu-id="70154-130">Preço le 100</span><span class="sxs-lookup"><span data-stu-id="70154-130">Price le 100</span></span> |
| <span data-ttu-id="70154-131">ne</span><span class="sxs-lookup"><span data-stu-id="70154-131">ne</span></span> |<span data-ttu-id="70154-132">Diferente de</span><span class="sxs-lookup"><span data-stu-id="70154-132">Not equal</span></span> |<span data-ttu-id="70154-133">City ne 'London'</span><span class="sxs-lookup"><span data-stu-id="70154-133">City ne 'London'</span></span> |
| <span data-ttu-id="70154-134">e</span><span class="sxs-lookup"><span data-stu-id="70154-134">and</span></span> |<span data-ttu-id="70154-135">e</span><span class="sxs-lookup"><span data-stu-id="70154-135">And</span></span> |<span data-ttu-id="70154-136">Preço le 200 e Preço gt 3,5</span><span class="sxs-lookup"><span data-stu-id="70154-136">Price le 200 and Price gt 3.5</span></span> |
| <span data-ttu-id="70154-137">ou o</span><span class="sxs-lookup"><span data-stu-id="70154-137">or</span></span> |<span data-ttu-id="70154-138">ou o</span><span class="sxs-lookup"><span data-stu-id="70154-138">Or</span></span> |<span data-ttu-id="70154-139">Preço le 3,5 ou Preço gt 200</span><span class="sxs-lookup"><span data-stu-id="70154-139">Price le 3.5 or Price gt 200</span></span> |
| <span data-ttu-id="70154-140">não</span><span class="sxs-lookup"><span data-stu-id="70154-140">not</span></span> |<span data-ttu-id="70154-141">não</span><span class="sxs-lookup"><span data-stu-id="70154-141">Not</span></span> |<span data-ttu-id="70154-142">não isAvailable</span><span class="sxs-lookup"><span data-stu-id="70154-142">not isAvailable</span></span> |

<span data-ttu-id="70154-143">Ao construir uma cadeia de caracteres de filtro, hello regras a seguir são importantes:</span><span class="sxs-lookup"><span data-stu-id="70154-143">When constructing a filter string, hello following rules are important:</span></span>

* <span data-ttu-id="70154-144">Use operadores lógicos de saudação toocompare um valor da propriedade tooa.</span><span class="sxs-lookup"><span data-stu-id="70154-144">Use hello logical operators toocompare a property tooa value.</span></span> <span data-ttu-id="70154-145">Observe que não é possível toocompare um valor dinâmico tooa da propriedade; um lado da expressão Olá deve ser uma constante.</span><span class="sxs-lookup"><span data-stu-id="70154-145">Note that it is not possible toocompare a property tooa dynamic value; one side of hello expression must be a constant.</span></span>
* <span data-ttu-id="70154-146">Todas as partes da cadeia de caracteres de filtro Olá diferenciam maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="70154-146">All parts of hello filter string are case-sensitive.</span></span>
* <span data-ttu-id="70154-147">valor constante Olá deve ser de saudação mesmo tipo que propriedade Olá para que os resultados Olá filtro tooreturn válidos.</span><span class="sxs-lookup"><span data-stu-id="70154-147">hello constant value must be of hello same data type as hello property in order for hello filter tooreturn valid results.</span></span> <span data-ttu-id="70154-148">Para obter mais informações sobre os tipos de propriedade com suporte, consulte [Olá Noções básicas sobre modelo de dados do serviço de tabela](http://go.microsoft.com/fwlink/p/?LinkId=400448).</span><span class="sxs-lookup"><span data-stu-id="70154-148">For more information about supported property types, see [Understanding hello Table Service Data Model](http://go.microsoft.com/fwlink/p/?LinkId=400448).</span></span>

## <a name="filtering-on-string-properties"></a><span data-ttu-id="70154-149">Filtrando nas propriedades de cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="70154-149">Filtering on String Properties</span></span>
<span data-ttu-id="70154-150">Quando você filtrar em Propriedades de cadeia de caracteres, coloque constante de cadeia de caracteres de saudação entre aspas.</span><span class="sxs-lookup"><span data-stu-id="70154-150">When you filter on string properties, enclose hello string constant in single quotation marks.</span></span>

<span data-ttu-id="70154-151">Olá filtros de exemplo a seguir no hello **PartitionKey** e **RowKey** propriedades; adicional não-chave propriedades também podem ser adicionadas toohello cadeia de caracteres de filtro:</span><span class="sxs-lookup"><span data-stu-id="70154-151">hello following example filters on hello **PartitionKey** and **RowKey** properties; additional non-key properties could also be added toohello filter string:</span></span>

    PartitionKey eq 'Partition1' and RowKey eq '00001'

<span data-ttu-id="70154-152">Você pode colocar cada expressão de filtro entre parênteses, embora não seja necessário:</span><span class="sxs-lookup"><span data-stu-id="70154-152">You can enclose each filter expression in parentheses, although it is not required:</span></span>

    (PartitionKey eq 'Partition1') and (RowKey eq '00001')

<span data-ttu-id="70154-153">Observe que Olá serviço tabela não oferece suporte a consultas com caractere curinga, e eles não têm suporte no Designer de tabela de saudação ou.</span><span class="sxs-lookup"><span data-stu-id="70154-153">Note that hello Table service does not support wildcard queries, and they are not supported in hello Table Designer either.</span></span> <span data-ttu-id="70154-154">No entanto, você pode executar usando operadores de comparação no prefixo desejado Olá de correspondência de prefixo.</span><span class="sxs-lookup"><span data-stu-id="70154-154">However, you can perform prefix matching by using comparison operators on hello desired prefix.</span></span> <span data-ttu-id="70154-155">Olá, exemplo a seguir retorna entidades com um sobrenome propriedade que começa com a letra de saudação 'A':</span><span class="sxs-lookup"><span data-stu-id="70154-155">hello following example returns entities with a LastName property beginning with hello letter 'A':</span></span>

    LastName ge 'A' and LastName lt 'B'

## <a name="filtering-on-numeric-properties"></a><span data-ttu-id="70154-156">Filtrando em propriedades numéricas</span><span class="sxs-lookup"><span data-stu-id="70154-156">Filtering on Numeric Properties</span></span>
<span data-ttu-id="70154-157">toofilter em um inteiro ou um número de ponto flutuante, especifique o número de saudação sem aspas.</span><span class="sxs-lookup"><span data-stu-id="70154-157">toofilter on an integer or floating-point number, specify hello number without quotation marks.</span></span>

<span data-ttu-id="70154-158">Este exemplo retorna todas as entidades com uma propriedade Idade cujo valor é maior que 30:</span><span class="sxs-lookup"><span data-stu-id="70154-158">This example returns all entities with an Age property whose value is greater than 30:</span></span>

    Age gt 30

<span data-ttu-id="70154-159">Este exemplo retorna todas as entidades com uma propriedade AmountDue cujo valor é menor que ou igual a too100.25:</span><span class="sxs-lookup"><span data-stu-id="70154-159">This example returns all entities with an AmountDue property whose value is less than or equal too100.25:</span></span>

    AmountDue le 100.25

## <a name="filtering-on-boolean-properties"></a><span data-ttu-id="70154-160">Filtrando em Propriedades Boolianas</span><span class="sxs-lookup"><span data-stu-id="70154-160">Filtering on Boolean Properties</span></span>
<span data-ttu-id="70154-161">toofilter em um valor booliano, especifique **true** ou **false** sem aspas.</span><span class="sxs-lookup"><span data-stu-id="70154-161">toofilter on a Boolean value, specify **true** or **false** without quotation marks.</span></span>

<span data-ttu-id="70154-162">Olá exemplo a seguir retorna todas as entidades onde Olá IsActive propriedade foi definido muito**true**:</span><span class="sxs-lookup"><span data-stu-id="70154-162">hello following example returns all entities where hello IsActive property is set too**true**:</span></span>

    IsActive eq true

<span data-ttu-id="70154-163">Você também pode escrever esta expressão de filtro sem um operador lógico hello.</span><span class="sxs-lookup"><span data-stu-id="70154-163">You can also write this filter expression without hello logical operator.</span></span> <span data-ttu-id="70154-164">Em Olá exemplo a seguir, Olá serviço tabela também retornará todas as entidades onde IsActive é **true**:</span><span class="sxs-lookup"><span data-stu-id="70154-164">In hello following example, hello Table service will also return all entities where IsActive is **true**:</span></span>

    IsActive

<span data-ttu-id="70154-165">tooreturn todas as entidades, onde é false, você pode usar o IsActive Olá não operador:</span><span class="sxs-lookup"><span data-stu-id="70154-165">tooreturn all entities where IsActive is false, you can use hello not operator:</span></span>

    not IsActive

## <a name="filtering-on-datetime-properties"></a><span data-ttu-id="70154-166">Filtrando em Propriedades DateTime</span><span class="sxs-lookup"><span data-stu-id="70154-166">Filtering on DateTime Properties</span></span>
<span data-ttu-id="70154-167">toofilter em um valor DateTime, especifique Olá **datetime** palavra-chave, seguido pela constante de data/hora de saudação entre aspas.</span><span class="sxs-lookup"><span data-stu-id="70154-167">toofilter on a DateTime value, specify hello **datetime** keyword, followed by hello date/time constant in single quotation marks.</span></span> <span data-ttu-id="70154-168">constante de data/hora Olá deve estar no formato UTC combinado, conforme descrito em [formatação de valores de propriedade DateTime](http://go.microsoft.com/fwlink/p/?LinkId=400449).</span><span class="sxs-lookup"><span data-stu-id="70154-168">hello date/time constant must be in combined UTC format, as described in [Formatting DateTime Property Values](http://go.microsoft.com/fwlink/p/?LinkId=400449).</span></span>

<span data-ttu-id="70154-169">saudação de exemplo a seguir retorna entidades em que a propriedade de CustomerSince Olá tooJuly igual a 10, 2008:</span><span class="sxs-lookup"><span data-stu-id="70154-169">hello following example returns entities where hello CustomerSince property is equal tooJuly 10, 2008:</span></span>

    CustomerSince eq datetime'2008-07-10T00:00:00Z'
