---
title: "Guia para a criação de um Serviço de Dados para o Marketplace | Microsoft Docs"
description: "Instruções detalhadas sobre como criar, certificar e implantar um Serviço de Dados para compra no Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 148f8638-ee80-4100-8d63-5afa4167ca1b
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 2ab624941fc385f14b62bb5d743927f157955845
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="examples-of-mapping-an-existing-web-service-to-odata-through-csdls"></a><span data-ttu-id="f6dc2-103">Exemplos de mapeamento de um serviço Web existente para OData por meio de CSDL</span><span class="sxs-lookup"><span data-stu-id="f6dc2-103">Examples of mapping an existing web service to OData through CSDLs</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f6dc2-104">**Neste momento, não estamos mais realizando a integração de novos editores de Serviço de Dados. Novos serviços de dados não serão ser aprovados para listagem.**</span><span class="sxs-lookup"><span data-stu-id="f6dc2-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="f6dc2-105">Se você tiver um aplicativo de negócios de SaaS que quer publicar no AppSource, encontre mais informações [aqui](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="f6dc2-105">If you have a SaaS business application you would like to publish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="f6dc2-106">Se você tiver aplicativos de IaaS ou serviços de desenvolvedor para publicar no Azure Marketplace, saiba mais [aqui](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="f6dc2-106">If you have an IaaS applications or developer service you would like to publish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

## <a name="example-functionimport-for-raw-data-returned-using-post"></a><span data-ttu-id="f6dc2-107">Exemplo: FunctionImport para dados “Brutos” retornados usando "POST"</span><span class="sxs-lookup"><span data-stu-id="f6dc2-107">Example: FunctionImport for "Raw" data returned using "POST"</span></span>
<span data-ttu-id="f6dc2-108">Use Dados brutos de POST para criar uma nova subordinada e retornar sua URL(local) definida de servidor ou atualizar parte da subordinada na URL definida do servidor.</span><span class="sxs-lookup"><span data-stu-id="f6dc2-108">Use POST Raw data to create a new subordinate and return its server defined URL(location) or to update part of the subordinate at the server defined URL.</span></span>  <span data-ttu-id="f6dc2-109">Onde a subordinada é uma transmissão, por exemplo,</span><span class="sxs-lookup"><span data-stu-id="f6dc2-109">Where the subordinate is a stream, i.e.</span></span> <span data-ttu-id="f6dc2-110">não estruturada, por exemplo,</span><span class="sxs-lookup"><span data-stu-id="f6dc2-110">unstructured, ex.</span></span> <span data-ttu-id="f6dc2-111">um arquivo de texto.</span><span class="sxs-lookup"><span data-stu-id="f6dc2-111">a text file.</span></span>  <span data-ttu-id="f6dc2-112">Esteja ciente de que POST não é idempotente sem um local.</span><span class="sxs-lookup"><span data-stu-id="f6dc2-112">Beware POST in not idempotent without a location.</span></span>

        <!--  No EntitySet or EntityType nodes required for Raw output-->
        <FunctionImport Name="AddUsageEvent" ReturnType="Raw(text/plain)" d:EncodeParameterValues="true" d:AllowedHttpMethods="POST" d:BaseUri="http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Add usage event (data acquisition)</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>

## <a name="example-functionimport-using-delete"></a><span data-ttu-id="f6dc2-113">Exemplo: FunctionImport usando "EXCLUIR"</span><span class="sxs-lookup"><span data-stu-id="f6dc2-113">Example: FunctionImport using "DELETE"</span></span>
<span data-ttu-id="f6dc2-114">Use EXCLUIR para remover um URI especificado.</span><span class="sxs-lookup"><span data-stu-id="f6dc2-114">Use DELETE to remove a specified URI.</span></span>

        <EntitySet Name="DeleteUsageFileEntitySet" EntityType="MyOffer.DeleteUsageFileEntity" />
        <FunctionImport Name="DeleteUsageFile" EntitySet="DeleteUsageFileEntitySet" ReturnType="Collection(MyOffer.DeleteUsageFileEntity)"  d:AllowedHttpMethods="DELETE" d:EncodeParameterValues="true” d:BaseUri=”http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643" >
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Delete usage File</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>
        <EntityType Name="DeleteUsageFileEntity" d:Map="//boolean">
        <Property Name="boolean" Type="String" Nullable="true" d:Map="./boolean" />
        </EntityType>

## <a name="example-functionimport-using-post"></a><span data-ttu-id="f6dc2-115">Exemplo: FunctionImport usando "POST"</span><span class="sxs-lookup"><span data-stu-id="f6dc2-115">Example: FunctionImport using "POST"</span></span>
<span data-ttu-id="f6dc2-116">Use Dados brutos de POST para criar uma nova subordinada e retornar sua URL(local) definida de servidor ou atualizar parte da subordinada na URL definida do servidor.</span><span class="sxs-lookup"><span data-stu-id="f6dc2-116">Use POST Raw data to create a new subordinate and return its server defined URL(location) or to update part of the subordinate at the server defined URL.</span></span>  <span data-ttu-id="f6dc2-117">Onde a subordinada é uma estrutura.</span><span class="sxs-lookup"><span data-stu-id="f6dc2-117">Where the subordinate is a structure.</span></span> <span data-ttu-id="f6dc2-118">Esteja ciente de que POST não é idempotente sem um local.</span><span class="sxs-lookup"><span data-stu-id="f6dc2-118">Beware POST is not idempotent without a location.</span></span>

        <EntitySet Name="CreateANewModelEntitySet2" EntityType=" MyOffer.CreateANewModelEntity2" />
        <FunctionImport Name="CreateModel" EntitySet="CreateANewModelEntitySet2" ReturnType="Collection(MyOffer.CreateANewModelEntity2)" d:EncodeParameterValues="true" d:AllowedHttpMethods="POST" d:BaseUri=”http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Create A New Model</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>

## <a name="example-functionimport-using-put"></a><span data-ttu-id="f6dc2-119">Exemplo: FunctionImport usando "PUT"</span><span class="sxs-lookup"><span data-stu-id="f6dc2-119">Example: FunctionImport using "PUT"</span></span>
<span data-ttu-id="f6dc2-120">Use PUT para criar uma nova subordinada ou atualizar a subordinada por completo em uma URL definida do servidor.</span><span class="sxs-lookup"><span data-stu-id="f6dc2-120">Use PUT to create a new subordinate or to update the entire subordinate at a server defined URL.</span></span>  <span data-ttu-id="f6dc2-121">Onde o subordinado é uma estrutura, PUT é idempotente para várias ocorrências resultando no mesmo estado, ou seja,</span><span class="sxs-lookup"><span data-stu-id="f6dc2-121">Where the subordinate is a structure, PUT is idempotent so multiple occurrences will result in the same state, i.e</span></span> <span data-ttu-id="f6dc2-122">x = 5.</span><span class="sxs-lookup"><span data-stu-id="f6dc2-122">x=5.</span></span>  <span data-ttu-id="f6dc2-123">PUT deve ser usado com o conteúdo completo do recurso especificado.</span><span class="sxs-lookup"><span data-stu-id="f6dc2-123">Put should be used with the full content of the specified resource.</span></span>

        <EntitySet Name="UpdateAnExistingModelEntitySet" EntityType="MyOffer.UpdateAnExistingModelEntity" />
        <FunctionImport Name="UpdateModel" EntitySet="UpdateAnExistingModelEntitySet" ReturnType="Collection(MyOffer.UpdateAnExistingModelEntity)" d:EncodeParameterValues="true" d:AllowedHttpMethods="PUT" d:BaseUri=”http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Update an Existing Model</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>
        <EntityType Name="UpdateAnExistingModelEntity" d:Map="//string">
        <Property Name="string"     Type="String" Nullable="true" d:Map="./string" />
        </EntityType>


## <a name="example-functionimport-for-raw-data-returned-using-put"></a><span data-ttu-id="f6dc2-124">Exemplo: FunctionImport para dados “Brutos” retornados usando "PUT"</span><span class="sxs-lookup"><span data-stu-id="f6dc2-124">Example: FunctionImport for "Raw" data returned using "PUT"</span></span>
<span data-ttu-id="f6dc2-125">Use Dados brutos PUT para criar uma nova subordinada ou atualizar a subordinada por completo em uma URL definida do servidor.</span><span class="sxs-lookup"><span data-stu-id="f6dc2-125">Use PUT Raw data to create a new subordinate or to update the entire subordinate at a server defined URL.</span></span>  <span data-ttu-id="f6dc2-126">Onde a subordinada é uma transmissão, por exemplo,</span><span class="sxs-lookup"><span data-stu-id="f6dc2-126">Where the subordinate is a stream, i.e.</span></span> <span data-ttu-id="f6dc2-127">não estruturada, por exemplo,</span><span class="sxs-lookup"><span data-stu-id="f6dc2-127">unstructured, ex.</span></span> <span data-ttu-id="f6dc2-128">um arquivo de texto.</span><span class="sxs-lookup"><span data-stu-id="f6dc2-128">a text file.</span></span>  <span data-ttu-id="f6dc2-129">PUT é idempotente para várias ocorrências resultando no mesmo estado, ou seja,</span><span class="sxs-lookup"><span data-stu-id="f6dc2-129">PUT is idempotent so multiple occurrences will result in the same state, i.e</span></span> <span data-ttu-id="f6dc2-130">x = 5.</span><span class="sxs-lookup"><span data-stu-id="f6dc2-130">x=5.</span></span>  <span data-ttu-id="f6dc2-131">PUT deve ser usado com o conteúdo completo do recurso especificado.</span><span class="sxs-lookup"><span data-stu-id="f6dc2-131">Put should be used with the full content of the specified resource.</span></span>

        <!--  No EntitySet or EntityType nodes required for Raw output-->
        <FunctionImport Name="CancelBuild” ReturnType="Raw(text/plain)" d:AllowedHttpMethods="PUT" d:EncodeParameterValues="true" d:BaseUri=” http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Cancel Build</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>


## <a name="example-functionimport-for-raw-data-returned-using-get"></a><span data-ttu-id="f6dc2-132">Exemplo: FunctionImport para dados “Brutos” retornados usando "GET"</span><span class="sxs-lookup"><span data-stu-id="f6dc2-132">Example: FunctionImport for "Raw" data returned using "GET"</span></span>
<span data-ttu-id="f6dc2-133">Use Dados brutos GET para retornar uma subordinada não estruturada, ou seja, texto.</span><span class="sxs-lookup"><span data-stu-id="f6dc2-133">Use GET Raw data to return a subordinate that is unstructured, i.e. text.</span></span>

        <!--  No EntitySet or EntityType nodes required for Raw output-->
        <FunctionImport Name="GetModelUsageFile" ReturnType="Raw(text/plain)" d:EncodeParameterValues="true" d:AllowedHttpMethods="GET" d:BaseUri="https://cmla.cloudapp.net/api2/model/builder/build?buildId={buildId}&amp;apiVersion={apiVersion}">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Download A Models Usage File</d:Description>
        <d:Headers>
        <d:Header d:Name="Accept" d:Value="application/xml,application/xhtml+xml,text/html;" />
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>

## <a name="example-functionimport-for-paging-through-returned-data"></a><span data-ttu-id="f6dc2-134">Exemplo: FunctionImport para "Paginação" através de dados retornados</span><span class="sxs-lookup"><span data-stu-id="f6dc2-134">Example: FunctionImport for "Paging" through returned data</span></span>
<span data-ttu-id="f6dc2-135">Use implementar paginação RESTful atraves de seus dados com GET.</span><span class="sxs-lookup"><span data-stu-id="f6dc2-135">Use implement RESTful paging through your data with GET.</span></span>  <span data-ttu-id="f6dc2-136">Paginação padrão é definida como 100 linhas por página de dados.</span><span class="sxs-lookup"><span data-stu-id="f6dc2-136">Default paging is set to 100 row per page of data.</span></span>

        <EntitySet Name=”CropEntitySet" EntityType="MyOffer.CropEntity" />
        <FunctionImport    Name="GetCropReport" EntitySet="CropEntitySet” ReturnType="Collection(MyOffer.CropEntity)" d:EmitSelfLink="false" d:EncodeParameterValues="true" d:Paging="SkipTake" d:MaxPageSize="100" d:BaseUri="http://api.mydata.org/Crop? report={report}&amp;series={series}&amp;start={$skip}&amp;size=100">
        <Parameter Name="report" Type="Int32" Mode="In" Nullable="false" d:SampleValues="4"  d:enum="1|2|3|4|5|6|7|8|9|10|11|12|13|14|15|16|17|18|19"  />
        <Parameter Name="series"    Type="String"    Mode="In" Nullable="false" d:SampleValues="FARM" />
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="text/xml;charset=UTF-8" />
        </d:Headers>
        <d:Namespaces>
        <d:Namespace d:Prefix="diffgr" d:Uri="urn:schemas-microsoft-com:xml-diffgram-v1" />
        </d:Namespaces>
        </FunctionImport>

## <a name="see-also"></a><span data-ttu-id="f6dc2-137">Consulte também</span><span class="sxs-lookup"><span data-stu-id="f6dc2-137">See Also</span></span>
* <span data-ttu-id="f6dc2-138">Se estiver interessado em entender o processo e a finalidade geral do mapeamento de OData, leia este artigo [Mapeamento OData de Serviço de Dados](marketplace-publishing-data-service-creation-odata-mapping.md) para examinar as definições, as estruturas e as instruções.</span><span class="sxs-lookup"><span data-stu-id="f6dc2-138">If you are interested in understanding the overall OData mapping process and purpose, read this article [Data Service OData Mapping](marketplace-publishing-data-service-creation-odata-mapping.md) to review definitions, structures, and instructions.</span></span>
* <span data-ttu-id="f6dc2-139">Se estiver interessado em aprender e em compreender os nós específicos e seus parâmetros, leia este artigo [Nós do mapeamento OData de Serviço de Dados](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) para obter definições, explicações, exemplos e contexto de casos de uso.</span><span class="sxs-lookup"><span data-stu-id="f6dc2-139">If you are interested in learning and understanding the specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="f6dc2-140">Para retornar ao caminho indicado para a publicação de um Serviço de Dados no Azure Marketplace, leia este artigo [Guia de publicação de Serviço de Dados](marketplace-publishing-data-service-creation.md).</span><span class="sxs-lookup"><span data-stu-id="f6dc2-140">To return to the prescribed path for publishing a Data Service to the Azure Marketplace, read this article [Data Service Publishing Guide](marketplace-publishing-data-service-creation.md).</span></span>

