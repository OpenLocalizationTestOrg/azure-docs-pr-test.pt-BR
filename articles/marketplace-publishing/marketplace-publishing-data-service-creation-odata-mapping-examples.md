---
title: "aaaGuide toocreating um serviço de dados para Olá Marketplace | Microsoft Docs"
description: "Instruções detalhadas de como toocreate, certificar e implantar um serviço de dados para compra em hello Azure Marketplace."
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
ms.openlocfilehash: 8917a43959834d15f70866297f98d24bb83e217f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="examples-of-mapping-an-existing-web-service-tooodata-through-csdls"></a><span data-ttu-id="19bab-103">Exemplos de mapeamento existente web tooOData de serviço por meio de CSDLs</span><span class="sxs-lookup"><span data-stu-id="19bab-103">Examples of mapping an existing web service tooOData through CSDLs</span></span>
> [!IMPORTANT]
> <span data-ttu-id="19bab-104">**Neste momento, não estamos mais realizando a integração de novos editores de Serviço de Dados. Novos serviços de dados não serão ser aprovados para listagem.**</span><span class="sxs-lookup"><span data-stu-id="19bab-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="19bab-105">Se você tiver um aplicativo de negócios SaaS você gostaria que toopublish em AppSource, você pode encontrar mais informações [aqui](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="19bab-105">If you have a SaaS business application you would like toopublish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="19bab-106">Se você tiver aplicativos de IaaS ou desenvolvedor de serviço seria como toopublish no Azure Marketplace, você pode encontrar mais informações [aqui](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="19bab-106">If you have an IaaS applications or developer service you would like toopublish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

## <a name="example-functionimport-for-raw-data-returned-using-post"></a><span data-ttu-id="19bab-107">Exemplo: FunctionImport para dados “Brutos” retornados usando "POST"</span><span class="sxs-lookup"><span data-stu-id="19bab-107">Example: FunctionImport for "Raw" data returned using "POST"</span></span>
<span data-ttu-id="19bab-108">Use toocreate POST bruto de dados subordinado novo e seu servidor URL(location) tooupdate parte Olá subordinado no servidor de saudação definido ou URL de retorno.</span><span class="sxs-lookup"><span data-stu-id="19bab-108">Use POST Raw data toocreate a new subordinate and return its server defined URL(location) or tooupdate part of hello subordinate at hello server defined URL.</span></span>  <span data-ttu-id="19bab-109">Onde Olá subordinado é um fluxo, ou seja, não estruturado, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="19bab-109">Where hello subordinate is a stream, i.e. unstructured, ex.</span></span> <span data-ttu-id="19bab-110">um arquivo de texto.</span><span class="sxs-lookup"><span data-stu-id="19bab-110">a text file.</span></span>  <span data-ttu-id="19bab-111">Esteja ciente de que POST não é idempotente sem um local.</span><span class="sxs-lookup"><span data-stu-id="19bab-111">Beware POST in not idempotent without a location.</span></span>

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

## <a name="example-functionimport-using-delete"></a><span data-ttu-id="19bab-112">Exemplo: FunctionImport usando "EXCLUIR"</span><span class="sxs-lookup"><span data-stu-id="19bab-112">Example: FunctionImport using "DELETE"</span></span>
<span data-ttu-id="19bab-113">Use tooremove excluir um URI especificado.</span><span class="sxs-lookup"><span data-stu-id="19bab-113">Use DELETE tooremove a specified URI.</span></span>

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

## <a name="example-functionimport-using-post"></a><span data-ttu-id="19bab-114">Exemplo: FunctionImport usando "POST"</span><span class="sxs-lookup"><span data-stu-id="19bab-114">Example: FunctionImport using "POST"</span></span>
<span data-ttu-id="19bab-115">Use toocreate POST bruto de dados subordinado novo e seu servidor URL(location) tooupdate parte Olá subordinado no servidor de saudação definido ou URL de retorno.</span><span class="sxs-lookup"><span data-stu-id="19bab-115">Use POST Raw data toocreate a new subordinate and return its server defined URL(location) or tooupdate part of hello subordinate at hello server defined URL.</span></span>  <span data-ttu-id="19bab-116">Onde Olá subordinado é uma estrutura.</span><span class="sxs-lookup"><span data-stu-id="19bab-116">Where hello subordinate is a structure.</span></span> <span data-ttu-id="19bab-117">Esteja ciente de que POST não é idempotente sem um local.</span><span class="sxs-lookup"><span data-stu-id="19bab-117">Beware POST is not idempotent without a location.</span></span>

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

## <a name="example-functionimport-using-put"></a><span data-ttu-id="19bab-118">Exemplo: FunctionImport usando "PUT"</span><span class="sxs-lookup"><span data-stu-id="19bab-118">Example: FunctionImport using "PUT"</span></span>
<span data-ttu-id="19bab-119">Usar PUT toocreate subordinado novo ou subordinado inteira do hello tooupdate em um servidor definido URL.</span><span class="sxs-lookup"><span data-stu-id="19bab-119">Use PUT toocreate a new subordinate or tooupdate hello entire subordinate at a server defined URL.</span></span>  <span data-ttu-id="19bab-120">Onde Olá subordinado é uma estrutura, PUT é idempotente para várias ocorrências resultará em Olá mesmo estado, ou seja</span><span class="sxs-lookup"><span data-stu-id="19bab-120">Where hello subordinate is a structure, PUT is idempotent so multiple occurrences will result in hello same state, i.e</span></span> <span data-ttu-id="19bab-121">x = 5.</span><span class="sxs-lookup"><span data-stu-id="19bab-121">x=5.</span></span>  <span data-ttu-id="19bab-122">PUT deve ser usada com hello conteúdo completo de saudação especificada recursos.</span><span class="sxs-lookup"><span data-stu-id="19bab-122">Put should be used with hello full content of hello specified resource.</span></span>

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


## <a name="example-functionimport-for-raw-data-returned-using-put"></a><span data-ttu-id="19bab-123">Exemplo: FunctionImport para dados “Brutos” retornados usando "PUT"</span><span class="sxs-lookup"><span data-stu-id="19bab-123">Example: FunctionImport for "Raw" data returned using "PUT"</span></span>
<span data-ttu-id="19bab-124">Use toocreate colocar bruto de dados subordinado novo ou subordinado inteira de saudação tooupdate em uma URL de servidor definido.</span><span class="sxs-lookup"><span data-stu-id="19bab-124">Use PUT Raw data toocreate a new subordinate or tooupdate hello entire subordinate at a server defined URL.</span></span>  <span data-ttu-id="19bab-125">Onde Olá subordinado é um fluxo, ou seja, não estruturado, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="19bab-125">Where hello subordinate is a stream, i.e. unstructured, ex.</span></span> <span data-ttu-id="19bab-126">um arquivo de texto.</span><span class="sxs-lookup"><span data-stu-id="19bab-126">a text file.</span></span>  <span data-ttu-id="19bab-127">PUT é idempotente para várias ocorrências resultará em Olá mesmo estado, ou seja</span><span class="sxs-lookup"><span data-stu-id="19bab-127">PUT is idempotent so multiple occurrences will result in hello same state, i.e</span></span> <span data-ttu-id="19bab-128">x = 5.</span><span class="sxs-lookup"><span data-stu-id="19bab-128">x=5.</span></span>  <span data-ttu-id="19bab-129">PUT deve ser usada com hello conteúdo completo de saudação especificada recursos.</span><span class="sxs-lookup"><span data-stu-id="19bab-129">Put should be used with hello full content of hello specified resource.</span></span>

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


## <a name="example-functionimport-for-raw-data-returned-using-get"></a><span data-ttu-id="19bab-130">Exemplo: FunctionImport para dados “Brutos” retornados usando "GET"</span><span class="sxs-lookup"><span data-stu-id="19bab-130">Example: FunctionImport for "Raw" data returned using "GET"</span></span>
<span data-ttu-id="19bab-131">Use obter bruto dados tooreturn subordinado que é não estruturado, ou seja, o texto.</span><span class="sxs-lookup"><span data-stu-id="19bab-131">Use GET Raw data tooreturn a subordinate that is unstructured, i.e. text.</span></span>

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

## <a name="example-functionimport-for-paging-through-returned-data"></a><span data-ttu-id="19bab-132">Exemplo: FunctionImport para "Paginação" através de dados retornados</span><span class="sxs-lookup"><span data-stu-id="19bab-132">Example: FunctionImport for "Paging" through returned data</span></span>
<span data-ttu-id="19bab-133">Use implementar paginação RESTful atraves de seus dados com GET.</span><span class="sxs-lookup"><span data-stu-id="19bab-133">Use implement RESTful paging through your data with GET.</span></span>  <span data-ttu-id="19bab-134">Paginação padrão é definida too100 de linhas por página de dados.</span><span class="sxs-lookup"><span data-stu-id="19bab-134">Default paging is set too100 row per page of data.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="19bab-135">Consulte também</span><span class="sxs-lookup"><span data-stu-id="19bab-135">See Also</span></span>
* <span data-ttu-id="19bab-136">Se você estiver interessado em entender Olá processo geral de mapeamento de OData e a finalidade, leia este artigo [dados serviço OData mapeamento](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview definições, estruturas e instruções.</span><span class="sxs-lookup"><span data-stu-id="19bab-136">If you are interested in understanding hello overall OData mapping process and purpose, read this article [Data Service OData Mapping](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview definitions, structures, and instructions.</span></span>
* <span data-ttu-id="19bab-137">Se você estiver interessado em aprendizado e nós específicos de saudação de compreensão e seus parâmetros, leia este artigo [dados serviço OData mapeamento nós](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) para definições e explicações, exemplos e contexto de casos de uso.</span><span class="sxs-lookup"><span data-stu-id="19bab-137">If you are interested in learning and understanding hello specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="19bab-138">toohello tooreturn prescrita caminho para publicar um serviço de dados de toohello Azure Marketplace, leia este artigo [guia de publicação de serviço de dados](marketplace-publishing-data-service-creation.md).</span><span class="sxs-lookup"><span data-stu-id="19bab-138">tooreturn toohello prescribed path for publishing a Data Service toohello Azure Marketplace, read this article [Data Service Publishing Guide](marketplace-publishing-data-service-creation.md).</span></span>

