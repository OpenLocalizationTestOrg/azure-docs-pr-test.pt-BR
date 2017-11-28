---
title: aaaSerialize dados no Hadoop - Microsoft Avro Library - Azure | Microsoft Docs
description: "Saiba como tooserialize e desserializar dados no Hadoop no HDInsight usando Olá Microsoft Avro Library toopersist toomemory, um banco de dados ou arquivo."
keywords: avro, hadoop avro
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: c78dc20d-5d8d-4366-94ac-abbe89aaac58
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: jgao
ms.custom: hdiseo17may2017
ms.openlocfilehash: f364f8e855a54c0fc160e9a106ec8d5b30c6db23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="serialize-data-in-hadoop-with-hello-microsoft-avro-library"></a><span data-ttu-id="04fdf-104">Serializar os dados no Hadoop com hello Microsoft Avro Library</span><span class="sxs-lookup"><span data-stu-id="04fdf-104">Serialize data in Hadoop with hello Microsoft Avro Library</span></span>

>[!NOTE]
><span data-ttu-id="04fdf-105">Olá Avro SDK não é suportado pela Microsoft.</span><span class="sxs-lookup"><span data-stu-id="04fdf-105">hello Avro SDK is no longer supported by Microsoft.</span></span> <span data-ttu-id="04fdf-106">biblioteca de saudação é suportado pela comunidade de código aberto.</span><span class="sxs-lookup"><span data-stu-id="04fdf-106">hello library is open source community supported.</span></span> <span data-ttu-id="04fdf-107">fontes de saudação para a biblioteca de saudação estão localizados em [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span><span class="sxs-lookup"><span data-stu-id="04fdf-107">hello sources for hello library are located in [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span></span>

<span data-ttu-id="04fdf-108">Este tópico mostra como Olá toouse [Microsoft Avro Library](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro) tooserialize objetos e outros dados estruturas em fluxos toopersist-los toomemory, um banco de dados ou um arquivo.</span><span class="sxs-lookup"><span data-stu-id="04fdf-108">This topic shows how toouse hello [Microsoft Avro Library](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro) tooserialize objects and other data structures into streams toopersist them toomemory, a database, or a file.</span></span> <span data-ttu-id="04fdf-109">Ele também mostra como toodeserialize-os objetos originais do toorecover hello.</span><span class="sxs-lookup"><span data-stu-id="04fdf-109">It also shows how toodeserialize them toorecover hello original objects.</span></span>

[!INCLUDE [windows-only](../../includes/hdinsight-windows-only.md)]

## <a name="apache-avro"></a><span data-ttu-id="04fdf-110">Apache Avro</span><span class="sxs-lookup"><span data-stu-id="04fdf-110">Apache Avro</span></span>
<span data-ttu-id="04fdf-111">Olá <a href="https://hadoopsdk.codeplex.com/wikipage?title=Avro%20Library" target="_blank">Microsoft Avro Library</a> implementa Olá Apache Avro sistema de serialização de dados para o ambiente do Microsoft.NET hello.</span><span class="sxs-lookup"><span data-stu-id="04fdf-111">hello <a href="https://hadoopsdk.codeplex.com/wikipage?title=Avro%20Library" target="_blank">Microsoft Avro Library</a> implements hello Apache Avro data serialization system for hello Microsoft.NET environment.</span></span> <span data-ttu-id="04fdf-112">O Apache Avro fornece um formato de intercâmbio de dados binários compactos para serialização.</span><span class="sxs-lookup"><span data-stu-id="04fdf-112">Apache Avro provides a compact binary data interchange format for serialization.</span></span> <span data-ttu-id="04fdf-113">Ele usa <a href="http://www.json.org" target="_blank">JSON</a> toodefine um esquema de linguagem independente que subscreve interoperabilidade de linguagem.</span><span class="sxs-lookup"><span data-stu-id="04fdf-113">It uses <a href="http://www.json.org" target="_blank">JSON</a> toodefine a language-agnostic schema that underwrites language interoperability.</span></span> <span data-ttu-id="04fdf-114">Os dados serializados em uma linguagem podem ser lidos em outra diferente.</span><span class="sxs-lookup"><span data-stu-id="04fdf-114">Data serialized in one language can be read in another.</span></span> <span data-ttu-id="04fdf-115">Atualmente, há suporte para C, C++, C#, Java, PHP, Python e Ruby.</span><span class="sxs-lookup"><span data-stu-id="04fdf-115">Currently C, C++, C#, Java, PHP, Python, and Ruby are supported.</span></span> <span data-ttu-id="04fdf-116">Informações detalhadas sobre o formato de saudação podem ser encontradas no hello <a href="http://avro.apache.org/docs/current/spec.html" target="_blank">especificação do Apache Avro</a>.</span><span class="sxs-lookup"><span data-stu-id="04fdf-116">Detailed information on hello format can be found in hello <a href="http://avro.apache.org/docs/current/spec.html" target="_blank">Apache Avro Specification</a>.</span></span> 

>[!NOTE]
><span data-ttu-id="04fdf-117">Olá Microsoft Avro Library não dá suporte a parte de RPCs (chamadas) de procedimento remoto Olá dessa especificação.</span><span class="sxs-lookup"><span data-stu-id="04fdf-117">hello Microsoft Avro Library does not support hello remote procedure calls (RPCs) part of this specification.</span></span>
>

<span data-ttu-id="04fdf-118">representação de saudação serializada de um objeto em Olá Avro sistema consiste em duas partes: esquema e o valor real.</span><span class="sxs-lookup"><span data-stu-id="04fdf-118">hello serialized representation of an object in hello Avro system consists of two parts: schema and actual value.</span></span> <span data-ttu-id="04fdf-119">esquema de Avro Olá descreve o modelo de dados de independente de linguagem de Olá dos dados Olá serializada com JSON.</span><span class="sxs-lookup"><span data-stu-id="04fdf-119">hello Avro schema describes hello language-independent data model of hello serialized data with JSON.</span></span> <span data-ttu-id="04fdf-120">Ela é apresentada lado a lado, com uma representação binária dos dados.</span><span class="sxs-lookup"><span data-stu-id="04fdf-120">It is presented side by side with a binary representation of data.</span></span> <span data-ttu-id="04fdf-121">Com o esquema de saudação separada da representação binária da saudação permite que cada toobe objeto escrito com nenhuma sobrecarga de por valor, fazer serialização rápida e hello representação pequeno.</span><span class="sxs-lookup"><span data-stu-id="04fdf-121">Having hello schema separate from hello binary representation permits each object toobe written with no per-value overheads, making serialization fast, and hello representation small.</span></span>

## <a name="hello-hadoop-scenario"></a><span data-ttu-id="04fdf-122">cenário de Hadoop Olá</span><span class="sxs-lookup"><span data-stu-id="04fdf-122">hello Hadoop scenario</span></span>
<span data-ttu-id="04fdf-123">formato de serialização do Apache Avro Olá é amplamente usado em outros ambientes de Apache Hadoop e HDInsight do Azure.</span><span class="sxs-lookup"><span data-stu-id="04fdf-123">hello Apache Avro serialization format is widely used in Azure HDInsight and other Apache Hadoop environments.</span></span> <span data-ttu-id="04fdf-124">Avro fornece uma maneira conveniente toorepresent estruturas de dados complexas dentro de um trabalho do Hadoop MapReduce.</span><span class="sxs-lookup"><span data-stu-id="04fdf-124">Avro provides a convenient way toorepresent complex data structures within a Hadoop MapReduce job.</span></span> <span data-ttu-id="04fdf-125">formato de saudação do Avro arquivos (arquivo de contêiner de objeto Avro) foi modelo de programação toosupport projetado Olá distribuída MapReduce.</span><span class="sxs-lookup"><span data-stu-id="04fdf-125">hello format of Avro files (Avro object container file) has been designed toosupport hello distributed MapReduce programming model.</span></span> <span data-ttu-id="04fdf-126">recurso de chave de saudação que permite a distribuição de saudação é que arquivos hello "divisíveis" no sentido de saudação que um pode atingir qualquer ponto em um arquivo e iniciar a leitura de um bloco específico.</span><span class="sxs-lookup"><span data-stu-id="04fdf-126">hello key feature that enables hello distribution is that hello files are “splittable” in hello sense that one can seek any point in a file and start reading from a particular block.</span></span>

## <a name="serialization-in-avro-library"></a><span data-ttu-id="04fdf-127">Serialização na biblioteca de Avro</span><span class="sxs-lookup"><span data-stu-id="04fdf-127">Serialization in Avro Library</span></span>
<span data-ttu-id="04fdf-128">Olá biblioteca .NET para Avro oferece suporte a duas maneiras de serializar objetos:</span><span class="sxs-lookup"><span data-stu-id="04fdf-128">hello .NET Library for Avro supports two ways of serializing objects:</span></span>

* <span data-ttu-id="04fdf-129">**reflexão** -esquema JSON de saudação para tipos de saudação é automaticamente criado a partir Olá dados atributos de contrato de toobe de tipos de .NET Olá serializado.</span><span class="sxs-lookup"><span data-stu-id="04fdf-129">**reflection** - hello JSON schema for hello types is automatically built from hello data contract attributes of hello .NET types toobe serialized.</span></span>
* <span data-ttu-id="04fdf-130">**Registro genérico** -esquema JSON de um for especificado explicitamente em um registro representado por Olá [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) classe quando nenhum tipo de .NET está presentes toodescribe Olá esquema Olá dados toobe serializado.</span><span class="sxs-lookup"><span data-stu-id="04fdf-130">**generic record** - A JSON schema is explicitly specified in a record represented by hello [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) class when no .NET types are present toodescribe hello schema for hello data toobe serialized.</span></span>

<span data-ttu-id="04fdf-131">Quando o esquema de dados Olá é conhecido gravador de saudação tooboth e um leitor de fluxo de saudação, dados saudação podem ser enviados sem seu esquema.</span><span class="sxs-lookup"><span data-stu-id="04fdf-131">When hello data schema is known tooboth hello writer and reader of hello stream, hello data can be sent without its schema.</span></span> <span data-ttu-id="04fdf-132">Em casos quando é usado um arquivo de contêiner de objetos do Avro, o esquema de saudação é armazenado no arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="04fdf-132">In cases when an Avro object container file is used, hello schema is stored within hello file.</span></span> <span data-ttu-id="04fdf-133">Outros parâmetros, como codec Olá usado para a compactação de dados, podem ser especificados.</span><span class="sxs-lookup"><span data-stu-id="04fdf-133">Other parameters, such as hello codec used for data compression, can be specified.</span></span> <span data-ttu-id="04fdf-134">Esses cenários são descritos mais detalhadamente e ilustrados na Olá exemplos de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="04fdf-134">These scenarios are outlined in more detail and illustrated in hello following code examples:</span></span>

## <a name="install-avro-library"></a><span data-ttu-id="04fdf-135">Instalar a Biblioteca do Avro</span><span class="sxs-lookup"><span data-stu-id="04fdf-135">Install Avro Library</span></span>
<span data-ttu-id="04fdf-136">a seguir Olá é necessária antes de instalar a biblioteca de saudação:</span><span class="sxs-lookup"><span data-stu-id="04fdf-136">hello following are required before you install hello library:</span></span>

* <span data-ttu-id="04fdf-137"><a href="http://www.microsoft.com/download/details.aspx?id=17851" target="_blank">Microsoft .NET Framework 4</a></span><span class="sxs-lookup"><span data-stu-id="04fdf-137"><a href="http://www.microsoft.com/download/details.aspx?id=17851" target="_blank">Microsoft .NET Framework 4</a></span></span>
* <span data-ttu-id="04fdf-138"><a href="http://james.newtonking.com/json" target="_blank">Newtonsoft Json.NET</a> (6.0.4 ou posterior)</span><span class="sxs-lookup"><span data-stu-id="04fdf-138"><a href="http://james.newtonking.com/json" target="_blank">Newtonsoft Json.NET</a> (6.0.4 or later)</span></span>

<span data-ttu-id="04fdf-139">Observe que Olá Newtonsoft.Json.dll dependência é baixada automaticamente com a instalação de saudação do hello Microsoft Avro Library.</span><span class="sxs-lookup"><span data-stu-id="04fdf-139">Note that hello Newtonsoft.Json.dll dependency is downloaded automatically with hello installation of hello Microsoft Avro Library.</span></span> <span data-ttu-id="04fdf-140">Olá procedimento é fornecido no hello seção a seguir:</span><span class="sxs-lookup"><span data-stu-id="04fdf-140">hello procedure is provided in hello following section:</span></span>

<span data-ttu-id="04fdf-141">Olá Microsoft Avro Library é distribuído como um pacote do NuGet que pode ser instalado do Visual Studio via Olá procedimento a seguir:</span><span class="sxs-lookup"><span data-stu-id="04fdf-141">hello Microsoft Avro Library is distributed as a NuGet package that can be installed from Visual Studio via hello following procedure:</span></span>

1. <span data-ttu-id="04fdf-142">Selecione Olá **projeto** -> guia **gerenciar pacotes NuGet...**</span><span class="sxs-lookup"><span data-stu-id="04fdf-142">Select hello **Project** tab -> **Manage NuGet Packages...**</span></span>
2. <span data-ttu-id="04fdf-143">Pesquise "Microsoft.Hadoop.Avro" no hello **Pesquisar Online** caixa.</span><span class="sxs-lookup"><span data-stu-id="04fdf-143">Search for "Microsoft.Hadoop.Avro" in hello **Search Online** box.</span></span>
3. <span data-ttu-id="04fdf-144">Clique em Olá **instalar** botão Avançar muito**biblioteca do Microsoft Azure HDInsight Avro**.</span><span class="sxs-lookup"><span data-stu-id="04fdf-144">Click hello **Install** button next too**Microsoft Azure HDInsight Avro Library**.</span></span>

<span data-ttu-id="04fdf-145">Observe que Olá Newtonsoft.Json.dll (> = 6.0.4) dependência também é baixada automaticamente com hello Microsoft Avro Library.</span><span class="sxs-lookup"><span data-stu-id="04fdf-145">Note that hello Newtonsoft.Json.dll (>=6.0.4) dependency is also downloaded automatically with hello Microsoft Avro Library.</span></span>

<span data-ttu-id="04fdf-146">Olá código-fonte Microsoft Avro Library está disponível em [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span><span class="sxs-lookup"><span data-stu-id="04fdf-146">hello Microsoft Avro Library source code is available at [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span></span>

## <a name="compile-schemas-using-avro-library"></a><span data-ttu-id="04fdf-147">Compilar esquemas usando a Biblioteca do Avro</span><span class="sxs-lookup"><span data-stu-id="04fdf-147">Compile schemas using Avro Library</span></span>
<span data-ttu-id="04fdf-148">Olá Microsoft Avro Library contém uma utilitário que permite a criação de tipos c# automaticamente com base em hello definido anteriormente esquema JSON a geração de código.</span><span class="sxs-lookup"><span data-stu-id="04fdf-148">hello Microsoft Avro Library contains a code generation utility that allows creating C# types automatically based on hello previously defined JSON schema.</span></span> <span data-ttu-id="04fdf-149">Utilitário de geração de código Olá não é distribuído como um binário executável, mas pode ser criado facilmente por meio de saudação procedimento a seguir:</span><span class="sxs-lookup"><span data-stu-id="04fdf-149">hello code generation utility is not distributed as a binary executable, but can be easily built via hello following procedure:</span></span>

1. <span data-ttu-id="04fdf-150">Baixar arquivo. zip de saudação com versão mais recente de saudação do código-fonte do SDK do HDInsight <a href="http://hadoopsdk.codeplex.com/SourceControl/latest#" target="_blank">Microsoft .NET SDK para Hadoop</a>.</span><span class="sxs-lookup"><span data-stu-id="04fdf-150">Download hello .zip file with hello latest version of HDInsight SDK source code from <a href="http://hadoopsdk.codeplex.com/SourceControl/latest#" target="_blank">Microsoft .NET SDK For Hadoop</a>.</span></span> <span data-ttu-id="04fdf-151">(Clique em Olá **baixar** ícone, Olá não **Downloads** guia.)</span><span class="sxs-lookup"><span data-stu-id="04fdf-151">(Click hello **Download** icon, not hello **Downloads** tab.)</span></span>
2. <span data-ttu-id="04fdf-152">Extrai Olá diretório do SDK do HDInsight tooa na máquina de saudação com o .NET Framework 4 instalado e conectado toohello Internet para baixar os pacotes do NuGet dependência necessária.</span><span class="sxs-lookup"><span data-stu-id="04fdf-152">Extract hello HDInsight SDK tooa directory on hello machine with .NET Framework 4 installed and connected toohello Internet for downloading necessary dependency NuGet packages.</span></span> <span data-ttu-id="04fdf-153">Abaixo, vamos supor que o código-fonte Olá é tooC:\SDK extraídos.</span><span class="sxs-lookup"><span data-stu-id="04fdf-153">Below, we assume that hello source code is extracted tooC:\SDK.</span></span>
3. <span data-ttu-id="04fdf-154">Pasta toohello C:\SDK\src\Microsoft.Hadoop.Avro.Tools e executar o build. bat.</span><span class="sxs-lookup"><span data-stu-id="04fdf-154">Go toohello folder C:\SDK\src\Microsoft.Hadoop.Avro.Tools and run build.bat.</span></span> <span data-ttu-id="04fdf-155">(Olá chamadas MSBuild do arquivo de distribuição de 32 bits de saudação de saudação do .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="04fdf-155">(hello file calls MSBuild from hello 32-bit distribution of hello .NET Framework.</span></span> <span data-ttu-id="04fdf-156">Se você deseja que a versão de 64 bits toouse hello, Build. bat editar, seguinte Olá comentários dentro do arquivo hello.) Certifique-se de que a compilação de saudação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="04fdf-156">If you would like toouse hello 64-bit version, edit build.bat, following hello comments inside hello file.) Ensure that hello build is successful.</span></span> <span data-ttu-id="04fdf-157">(Em alguns sistemas, o MSBuild pode gerar avisos.</span><span class="sxs-lookup"><span data-stu-id="04fdf-157">(On some systems, MSBuild may produce warnings.</span></span> <span data-ttu-id="04fdf-158">Esses avisos não afetam utilitário hello como não há nenhum erro de compilação.)</span><span class="sxs-lookup"><span data-stu-id="04fdf-158">These warnings do not affect hello utility as long as there are no build errors.)</span></span>
4. <span data-ttu-id="04fdf-159">Olá compilado utilitário está localizado em C:\SDK\Bin\Unsigned\Release\Microsoft.Hadoop.Avro.Tools.</span><span class="sxs-lookup"><span data-stu-id="04fdf-159">hello compiled utility is located in C:\SDK\Bin\Unsigned\Release\Microsoft.Hadoop.Avro.Tools.</span></span>

<span data-ttu-id="04fdf-160">tooget familiarizado com a sintaxe de linha de comando hello, execute Olá comando a seguir da pasta Olá onde o utilitário de geração de código hello está localizado:`Microsoft.Hadoop.Avro.Tools help /c:codegen`</span><span class="sxs-lookup"><span data-stu-id="04fdf-160">tooget familiar with hello command-line syntax, execute hello following command from hello folder where hello code generation utility is located: `Microsoft.Hadoop.Avro.Tools help /c:codegen`</span></span>

<span data-ttu-id="04fdf-161">Utilitário de saudação tootest, você pode gerar classes c# do arquivo de esquema Olá exemplo JSON fornecido com o código-fonte hello.</span><span class="sxs-lookup"><span data-stu-id="04fdf-161">tootest hello utility, you can generate C# classes from hello sample JSON schema file provided with hello source code.</span></span> <span data-ttu-id="04fdf-162">Execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="04fdf-162">Execute hello following command:</span></span>

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:

<span data-ttu-id="04fdf-163">Isso deve tooproduce c# dois arquivos no diretório atual Olá: SensorData.cs e Location.cs.</span><span class="sxs-lookup"><span data-stu-id="04fdf-163">This is supposed tooproduce two C# files in hello current directory: SensorData.cs and Location.cs.</span></span>

<span data-ttu-id="04fdf-164">lógica de saudação toounderstand que está usando o utilitário de geração de código Olá durante a conversão de tipos tooC # Olá JSON esquema, consulte o arquivo de saudação GenerationVerification.feature localizado em C:\SDK\src\Microsoft.Hadoop.Avro.Tools\Doc.</span><span class="sxs-lookup"><span data-stu-id="04fdf-164">toounderstand hello logic that hello code generation utility is using while converting hello JSON schema tooC# types, see hello file GenerationVerification.feature located in C:\SDK\src\Microsoft.Hadoop.Avro.Tools\Doc.</span></span>

<span data-ttu-id="04fdf-165">Namespaces são extraídas de esquema JSON hello, usando uma lógica Olá descrita no arquivo hello mencionado no parágrafo anterior hello.</span><span class="sxs-lookup"><span data-stu-id="04fdf-165">Namespaces are extracted from hello JSON schema, using hello logic described in hello file mentioned in hello previous paragraph.</span></span> <span data-ttu-id="04fdf-166">Namespaces extraídos do esquema Olá têm precedência sobre tudo o que é fornecido com o parâmetro de /n hello na linha de comando do utilitário hello.</span><span class="sxs-lookup"><span data-stu-id="04fdf-166">Namespaces extracted from hello schema take precedence over whatever is provided with hello /n parameter in hello utility command line.</span></span> <span data-ttu-id="04fdf-167">Se você quiser toooverride Olá namespaces contidos no esquema hello, use o parâmetro de /nf de saudação.</span><span class="sxs-lookup"><span data-stu-id="04fdf-167">If you want toooverride hello namespaces contained within hello schema, use hello /nf parameter.</span></span> <span data-ttu-id="04fdf-168">Por exemplo, toochange todos os namespaces de saudação SampleJSONSchema.avsc toomy.own.nspace, execute Olá seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="04fdf-168">For example, toochange all namespaces from hello SampleJSONSchema.avsc toomy.own.nspace, execute hello following command:</span></span>

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:. /nf:my.own.nspace

## <a name="about-hello-samples"></a><span data-ttu-id="04fdf-169">Sobre exemplos de saudação</span><span class="sxs-lookup"><span data-stu-id="04fdf-169">About hello samples</span></span>
<span data-ttu-id="04fdf-170">Seis exemplos fornecidos neste tópico ilustram diferentes cenários com suporte pelo Olá Microsoft Avro Library.</span><span class="sxs-lookup"><span data-stu-id="04fdf-170">Six examples provided in this topic illustrate different scenarios supported by hello Microsoft Avro Library.</span></span> <span data-ttu-id="04fdf-171">Olá Microsoft Avro Library é projetado toowork com qualquer fluxo.</span><span class="sxs-lookup"><span data-stu-id="04fdf-171">hello Microsoft Avro Library is designed toowork with any stream.</span></span> <span data-ttu-id="04fdf-172">Nestes exemplos, os dados são manipulados por fluxos de memória em vez de fluxos de arquivo ou bancos de dados, por questão de simplicidade e consistência.</span><span class="sxs-lookup"><span data-stu-id="04fdf-172">In these examples, data is manipulated via memory streams rather than file streams or databases for simplicity and consistency.</span></span> <span data-ttu-id="04fdf-173">abordagem de saudação usada em um ambiente de produção depende de requisitos de cenário exato hello, fonte de dados e volume, as restrições de desempenho e outros fatores.</span><span class="sxs-lookup"><span data-stu-id="04fdf-173">hello approach taken in a production environment depends on hello exact scenario requirements, data source and volume, performance constraints, and other factors.</span></span>

<span data-ttu-id="04fdf-174">Olá primeiro dois exemplos mostram como tooserialize e desserializar dados em buffers de fluxo de memória por meio de reflexão e registros genéricos.</span><span class="sxs-lookup"><span data-stu-id="04fdf-174">hello first two examples show how tooserialize and deserialize data into memory stream buffers by using reflection and generic records.</span></span> <span data-ttu-id="04fdf-175">Olá esquema nesses dois casos é considerada toobe compartilhado entre Olá leitores e gravadores fora de banda.</span><span class="sxs-lookup"><span data-stu-id="04fdf-175">hello schema in these two cases is assumed toobe shared between hello readers and writers out-of-band.</span></span>

<span data-ttu-id="04fdf-176">Olá terceiro e quarto exemplos mostram como tooserialize e desserializar dados usando arquivos de contêiner de objeto Olá Avro.</span><span class="sxs-lookup"><span data-stu-id="04fdf-176">hello third and fourth examples show how tooserialize and deserialize data by using hello Avro object container files.</span></span> <span data-ttu-id="04fdf-177">Quando dados são armazenados em um arquivo de contêiner Avro, seu esquema sempre é armazenado com ele porque o esquema de saudação deve ser compartilhada para desserialização.</span><span class="sxs-lookup"><span data-stu-id="04fdf-177">When data is stored in an Avro container file, its schema is always stored with it because hello schema must be shared for deserialization.</span></span>

<span data-ttu-id="04fdf-178">Olá contendo exemplo hello quatro primeiros exemplos podem ser baixados do hello <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-86055923" target="_blank">exemplos de código do Azure</a> site.</span><span class="sxs-lookup"><span data-stu-id="04fdf-178">hello sample containing hello first four examples can be downloaded from hello <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-86055923" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="04fdf-179">Olá quinto exemplo mostra como os arquivos de contêiner de objetos toouse um codec de compactação personalizada para Avro.</span><span class="sxs-lookup"><span data-stu-id="04fdf-179">hello fifth example shows how toouse a custom compression codec for Avro object container files.</span></span> <span data-ttu-id="04fdf-180">Um exemplo que contém o código de saudação para este exemplo pode ser baixado do hello <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-67159111" target="_blank">exemplos de código do Azure</a> site.</span><span class="sxs-lookup"><span data-stu-id="04fdf-180">A sample containing hello code for this example can be downloaded from hello <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-67159111" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="04fdf-181">exemplo de Hello sexto mostra como toouse Avro serialização tooupload dados tooAzure armazenamento de Blob e analisá-los usando o Hive com um cluster HDInsight (Hadoop).</span><span class="sxs-lookup"><span data-stu-id="04fdf-181">hello sixth sample shows how toouse Avro serialization tooupload data tooAzure Blob storage and then analyze it by using Hive with an HDInsight (Hadoop) cluster.</span></span> <span data-ttu-id="04fdf-182">Ele pode ser baixado da saudação <a href="https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3" target="_blank">exemplos de código do Azure</a> site.</span><span class="sxs-lookup"><span data-stu-id="04fdf-182">It can be downloaded from hello <a href="https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="04fdf-183">Estes são exemplos de seis toohello discutidos no tópico Olá links:</span><span class="sxs-lookup"><span data-stu-id="04fdf-183">Here are links toohello six samples discussed in hello topic:</span></span>

* <span data-ttu-id="04fdf-184"><a href="#Scenario1">**Serialização com reflexão** </a> -esquema JSON Olá toobe tipos serializado é automaticamente criado a partir Olá dados atributos de contrato.</span><span class="sxs-lookup"><span data-stu-id="04fdf-184"><a href="#Scenario1">**Serialization with reflection**</a> - hello JSON schema for types toobe serialized is automatically built from hello data contract attributes.</span></span>
* <span data-ttu-id="04fdf-185"><a href="#Scenario2">**Serialização com registro genérico** </a> -esquema JSON de saudação é especificado explicitamente em um registro quando nenhum tipo de .NET está disponível para reflexão.</span><span class="sxs-lookup"><span data-stu-id="04fdf-185"><a href="#Scenario2">**Serialization with generic record**</a> - hello JSON schema is explicitly specified in a record when no .NET type is available for reflection.</span></span>
* <span data-ttu-id="04fdf-186"><a href="#Scenario3">**Serialização usando arquivos de contêiner do objeto com reflexão** </a> -esquema JSON de saudação é automaticamente criado e compartilhado junto com dados Olá serializado por meio de um arquivo de contêiner do objeto Avro.</span><span class="sxs-lookup"><span data-stu-id="04fdf-186"><a href="#Scenario3">**Serialization using object container files with reflection**</a> - hello JSON schema is automatically built and shared together with hello serialized data via an Avro object container file.</span></span>
* <span data-ttu-id="04fdf-187"><a href="#Scenario4">**Serialização usando arquivos de contêiner do objeto com registro genérico** </a> -esquema JSON de saudação é explicitamente especificado antes de serialização hello e compartilhado junto com dados Olá por meio de um arquivo de contêiner do objeto Avro.</span><span class="sxs-lookup"><span data-stu-id="04fdf-187"><a href="#Scenario4">**Serialization using object container files with generic record**</a> - hello JSON schema is explicitly specified before hello serialization and shared together with hello data via an Avro object container file.</span></span>
* <span data-ttu-id="04fdf-188"><a href="#Scenario5">**Serialização usando arquivos de contêiner do objeto com um codec de compactação personalizada** </a> -exemplo hello mostra como o arquivo de contêiner com uma implementação personalizada de .NET de codec de compactação de dados Olá Deflate de objeto toocreate um Avro.</span><span class="sxs-lookup"><span data-stu-id="04fdf-188"><a href="#Scenario5">**Serialization using object container files with a custom compression codec**</a> - hello example shows how toocreate an Avro object container file with a customized .NET implementation of hello Deflate data compression codec.</span></span>
* <span data-ttu-id="04fdf-189"><a href="#Scenario6">**Usando dados de tooupload Avro para Olá serviço Microsoft Azure HDInsight** </a> -exemplo hello ilustra como a serialização de Avro interage com hello serviço HDInsight.</span><span class="sxs-lookup"><span data-stu-id="04fdf-189"><a href="#Scenario6">**Using Avro tooupload data for hello Microsoft Azure HDInsight service**</a> - hello example illustrates how Avro serialization interacts with hello HDInsight service.</span></span> <span data-ttu-id="04fdf-190">Um ativo do Azure assinatura e acesso tooan HDInsight do Azure são de cluster necessário toorun neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="04fdf-190">An active Azure subscription and access tooan Azure HDInsight cluster are required toorun this example.</span></span>

## <span data-ttu-id="04fdf-191"><a name="Scenario1"></a>Exemplo 1: Serialização com reflexão</span><span class="sxs-lookup"><span data-stu-id="04fdf-191"><a name="Scenario1"></a>Sample 1: Serialization with reflection</span></span>
<span data-ttu-id="04fdf-192">esquema JSON Olá para tipos de saudação pode ser automaticamente criada por Olá Microsoft Avro Library via reflexão de dados saudação atributos de contrato de saudação c# objetos toobe serializado.</span><span class="sxs-lookup"><span data-stu-id="04fdf-192">hello JSON schema for hello types can be automatically built by hello Microsoft Avro Library via reflection from hello data contract attributes of hello C# objects toobe serialized.</span></span> <span data-ttu-id="04fdf-193">Olá Microsoft Avro Library cria um [ **IAvroSeralizer<T>**  ](http://msdn.microsoft.com/library/dn627341.aspx) tooidentify Olá campos toobe serializado.</span><span class="sxs-lookup"><span data-stu-id="04fdf-193">hello Microsoft Avro Library creates an [**IAvroSeralizer<T>**](http://msdn.microsoft.com/library/dn627341.aspx) tooidentify hello fields toobe serialized.</span></span>

<span data-ttu-id="04fdf-194">Neste exemplo, objetos (um **SensorData** classe com um membro **local** struct) são serializados tooa fluxo de memória, e este fluxo por sua vez é desserializado.</span><span class="sxs-lookup"><span data-stu-id="04fdf-194">In this example, objects (a **SensorData** class with a member **Location** struct) are serialized tooa memory stream, and this stream is in turn deserialized.</span></span> <span data-ttu-id="04fdf-195">Olá resultado for comparado toohello inicial instância tooconfirm que Olá **SensorData** objeto recuperado é idêntico toohello original.</span><span class="sxs-lookup"><span data-stu-id="04fdf-195">hello result is then compared toohello initial instance tooconfirm that hello **SensorData** object recovered is identical toohello original.</span></span>

<span data-ttu-id="04fdf-196">esquema Olá neste exemplo é assumida toobe compartilhado entre Olá leitores e gravadores, formato de contêiner de objeto Olá Avro não é necessário.</span><span class="sxs-lookup"><span data-stu-id="04fdf-196">hello schema in this example is assumed toobe shared between hello readers and writers, so hello Avro object container format is not required.</span></span> <span data-ttu-id="04fdf-197">Para obter um exemplo de como tooserialize e desserializar dados em buffers de memória por meio de reflexão com formato de contêiner de objeto de saudação ao esquema Olá deve ser compartilhada com dados hello, consulte <a href="#Scenario3">serialização usando arquivos de contêiner do objeto com reflexão</a>.</span><span class="sxs-lookup"><span data-stu-id="04fdf-197">For an example of how tooserialize and deserialize data into memory buffers by using reflection with hello object container format when hello schema must be shared with hello data, see <a href="#Scenario3">Serialization using object container files with reflection</a>.</span></span>

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }

        //This class contains all methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serialize and deserialize sample data set represented as an object using reflection.
            //No explicit schema definition is required - schema of serialized objects is automatically built.
            public void SerializeDeserializeObjectUsingReflection()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION\n");
                Console.WriteLine("Serializing Sample Data Set...");

                //Create a new AvroSerializer instance and specify a custom serialization strategy AvroDataContractResolver
                //for serializing only properties attributed with DataContract/DateMember
                var avroSerializer = AvroSerializer.Create<SensorData>();

                //Create a memory stream buffer
                using (var buffer = new MemoryStream())
                {
                    //Create a data set by using sample class and struct
                    var expected = new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } };

                    //Serialize hello data toohello specified stream
                    avroSerializer.Serialize(buffer, expected);


                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Deserialize data from hello stream and cast it toohello same type used for serialization
                    var actual = avroSerializer.Deserialize(buffer);

                    Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                    //Finally, verify that deserialized data matches hello original one
                    bool isEqual = this.Equal(expected, actual);

                    Console.WriteLine("Result of Data Set Identity Comparison is {0}", isEqual);

                }
            }

            //
            //Helper methods
            //

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }



            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample Class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization toomemory using reflection
                Sample.SerializeDeserializeObjectUsingReflection();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION
    //
    // Serializing Sample Data Set...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // Result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-2-serialization-with-a-generic-record"></a><span data-ttu-id="04fdf-198">Exemplo 2: serialização com um registro genérico</span><span class="sxs-lookup"><span data-stu-id="04fdf-198">Sample 2: Serialization with a generic record</span></span>
<span data-ttu-id="04fdf-199">Um esquema JSON pode ser especificado explicitamente em um registro genérico quando reflexão não pode ser usada porque dados saudação não podem ser representados por meio de classes .NET com um contrato de dados.</span><span class="sxs-lookup"><span data-stu-id="04fdf-199">A JSON schema can be explicitly specified in a generic record when reflection cannot be used because hello data cannot be represented via .NET classes with a data contract.</span></span> <span data-ttu-id="04fdf-200">Este método é mais lento do que usar reflexão.</span><span class="sxs-lookup"><span data-stu-id="04fdf-200">This method is slower than using reflection.</span></span> <span data-ttu-id="04fdf-201">Nesses casos, esquema de saudação para dados de saudação também pode ser dinâmica, ou seja, não é conhecido em tempo de compilação.</span><span class="sxs-lookup"><span data-stu-id="04fdf-201">In such cases, hello schema for hello data may also be dynamic, that is, not known at compile time.</span></span> <span data-ttu-id="04fdf-202">Dados representados como valores separados por vírgula (CSV) arquivos cujo esquema é desconhecida até que ele é transformado toohello Avro formato em tempo de execução é um exemplo desse tipo de cenário dinâmico.</span><span class="sxs-lookup"><span data-stu-id="04fdf-202">Data represented as comma-separated values (CSV) files whose schema is unknown until it is transformed toohello Avro format at run time is an example of this sort of dynamic scenario.</span></span>

<span data-ttu-id="04fdf-203">Este exemplo mostra como toocreate e usar um [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) tooexplicitly especificar um esquema JSON, como toopopulate-lo com dados saudação e, em seguida, como tooserialize e desserializá-la.</span><span class="sxs-lookup"><span data-stu-id="04fdf-203">This example shows how toocreate and use an [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) tooexplicitly specify a JSON schema, how toopopulate it with hello data, and then how tooserialize and deserialize it.</span></span> <span data-ttu-id="04fdf-204">Olá resultado é comparado toohello inicial de instâncias tooconfirm que Olá recuperado do registro é idêntico toohello original.</span><span class="sxs-lookup"><span data-stu-id="04fdf-204">hello result is then compared toohello initial instance tooconfirm that hello record recovered is identical toohello original.</span></span>

<span data-ttu-id="04fdf-205">esquema Olá neste exemplo é assumida toobe compartilhado entre Olá leitores e gravadores, formato de contêiner de objeto Olá Avro não é necessário.</span><span class="sxs-lookup"><span data-stu-id="04fdf-205">hello schema in this example is assumed toobe shared between hello readers and writers, so hello Avro object container format is not required.</span></span> <span data-ttu-id="04fdf-206">Para obter um exemplo de como tooserialize e desserializar dados em buffers de memória usando um registro genérico com formato de contêiner de objeto hello, quando o esquema de saudação deve ser incluída com dados serializado de saudação, consulte Olá <a href="#Scenario4">usando o contêiner do objeto de serialização arquivos com registro genérico</a> exemplo.</span><span class="sxs-lookup"><span data-stu-id="04fdf-206">For an example of how tooserialize and deserialize data into memory buffers by using a generic record with hello object container format when hello schema must be included with hello serialized data, see hello <a href="#Scenario4">Serialization using object container files with generic record</a> example.</span></span>

    namespace Microsoft.Hadoop.Avro.Sample
    {
    using System;
    using System.Collections.Generic;
    using System.IO;
    using System.Linq;
    using System.Runtime.Serialization;
    using Microsoft.Hadoop.Avro.Container;
    using Microsoft.Hadoop.Avro.Schema;
    using Microsoft.Hadoop.Avro;

    //This class contains all methods demonstrating
    //hello usage of Microsoft Avro Library
    public class AvroSample
    {

        //Serialize and deserialize sample data set by using a generic record.
        //A generic record is a special class with hello schema explicitly defined in JSON.
        //All serialized data should be mapped toohello fields of hello generic record,
        //which in turn is then serialized.
        public void SerializeDeserializeObjectUsingGenericRecords()
        {
            Console.WriteLine("SERIALIZATION USING GENERIC RECORD\n");
            Console.WriteLine("Defining hello Schema and creating Sample Data Set...");

            //Define hello schema in JSON
            const string Schema = @"{
                                ""type"":""record"",
                                ""name"":""Microsoft.Hadoop.Avro.Specifications.SensorData"",
                                ""fields"":
                                    [
                                        {
                                            ""name"":""Location"",
                                            ""type"":
                                                {
                                                    ""type"":""record"",
                                                    ""name"":""Microsoft.Hadoop.Avro.Specifications.Location"",
                                                    ""fields"":
                                                        [
                                                            { ""name"":""Floor"", ""type"":""int"" },
                                                            { ""name"":""Room"", ""type"":""int"" }
                                                        ]
                                                }
                                        },
                                        { ""name"":""Value"", ""type"":""bytes"" }
                                    ]
                            }";

            //Create a generic serializer based on hello schema
            var serializer = AvroSerializer.CreateGeneric(Schema);
            var rootSchema = serializer.WriterSchema as RecordSchema;

            //Create a memory stream buffer
            using (var stream = new MemoryStream())
            {
                //Create a generic record toorepresent hello data
                dynamic location = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location.Floor = 1;
                location.Room = 243;

                dynamic expected = new AvroRecord(serializer.WriterSchema);
                expected.Location = location;
                expected.Value = new byte[] { 1, 2, 3, 4, 5 };

                Console.WriteLine("Serializing Sample Data Set...");

                //Serialize hello data
                serializer.Serialize(stream, expected);

                stream.Seek(0, SeekOrigin.Begin);

                Console.WriteLine("Deserializing Sample Data Set...");

                //Deserialize hello data into a generic record
                dynamic actual = serializer.Deserialize(stream);

                Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                //Finally, verify hello results
                bool isEqual = expected.Location.Floor.Equals(actual.Location.Floor);
                isEqual = isEqual && expected.Location.Room.Equals(actual.Location.Room);
                isEqual = isEqual && ((byte[])expected.Value).SequenceEqual((byte[])actual.Value);
                Console.WriteLine("Result of Data Set Identity Comparison is {0}", isEqual);
            }
        }

        static void Main()
        {

            string sectionDivider = "---------------------------------------- ";

            //Create an instance of AvroSample class and invoke methods
            //illustrating different serializing approaches
            AvroSample Sample = new AvroSample();

            //Serialization toomemory using generic record
            Sample.SerializeDeserializeObjectUsingGenericRecords();

            Console.WriteLine(sectionDivider);
            Console.WriteLine("Press any key tooexit.");
            Console.Read();
        }
    }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING GENERIC RECORD
    //
    // Defining hello Schema and creating Sample Data Set...
    // Serializing Sample Data Set...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // Result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-3-serialization-using-object-container-files-and-serialization-with-reflection"></a><span data-ttu-id="04fdf-207">Exemplo 3: serialização usando arquivos do contêiner de objetos e serialização com reflexão</span><span class="sxs-lookup"><span data-stu-id="04fdf-207">Sample 3: Serialization using object container files and serialization with reflection</span></span>
<span data-ttu-id="04fdf-208">Este exemplo é o cenário toohello semelhante em Olá <a href="#Scenario1"> primeiro exemplo</a>, onde o esquema de saudação implicitamente é especificada com reflexão.</span><span class="sxs-lookup"><span data-stu-id="04fdf-208">This example is similar toohello scenario in hello <a href="#Scenario1"> first example</a>, where hello schema is implicitly specified with reflection.</span></span> <span data-ttu-id="04fdf-209">Olá diferença é que aqui, esquema de saudação não presume toobe conhecido leitor toohello desserializa a ele.</span><span class="sxs-lookup"><span data-stu-id="04fdf-209">hello difference is that here, hello schema is not assumed toobe known toohello reader that deserializes it.</span></span> <span data-ttu-id="04fdf-210">Olá **SensorData** toobe objetos serializados e seu esquema implicitamente especificada são armazenados em um arquivo de contêiner de objeto Avro representado por Olá [ **AvroContainer** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) classe.</span><span class="sxs-lookup"><span data-stu-id="04fdf-210">hello **SensorData** objects toobe serialized and their implicitly specified schema are stored in an Avro object container file represented by hello [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) class.</span></span>

<span data-ttu-id="04fdf-211">Neste exemplo com os dados de saudação são serializados [ **SequentialWriter<SensorData>**  ](http://msdn.microsoft.com/library/dn627340.aspx) e desserializado com [ **SequentialReader<SensorData>** ](http://msdn.microsoft.com/library/dn627340.aspx).</span><span class="sxs-lookup"><span data-stu-id="04fdf-211">hello data is serialized in this example with [**SequentialWriter<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx) and deserialized with [**SequentialReader<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx).</span></span> <span data-ttu-id="04fdf-212">resultado de Hello, em seguida, é comparado toohello instâncias iniciais tooensure identidade.</span><span class="sxs-lookup"><span data-stu-id="04fdf-212">hello result then is compared toohello initial instances tooensure identity.</span></span>

<span data-ttu-id="04fdf-213">Olá dados saudação do objeto contêiner é compactado por meio de padrão de saudação [ **Deflate** ] [ deflate-100] codec de compactação do .NET Framework 4.</span><span class="sxs-lookup"><span data-stu-id="04fdf-213">hello data in hello object container file is compressed via hello default [**Deflate**][deflate-100] compression codec from .NET Framework 4.</span></span> <span data-ttu-id="04fdf-214">Consulte Olá <a href="#Scenario5"> quinto exemplo</a> na toolearn neste tópico como toouse uma versão mais recente e superior do hello [ **Deflate** ] [ deflate-110] compactação codec disponível no .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="04fdf-214">See hello <a href="#Scenario5"> fifth example</a> in this topic toolearn how toouse a more recent and superior version of hello [**Deflate**][deflate-110] compression codec available in .NET Framework 4.5.</span></span>

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }

        //This class contains all methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes hello sample data set by using reflection and Avro object container files.
            //Serialized data is compressed with hello Deflate codec.
            public void SerializeDeserializeUsingObjectContainersReflection()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION AND AVRO OBJECT CONTAINER FILES\n");

                //Path for Avro object container file
                string path = "AvroSampleReflectionDeflate.avro";

                //Create a data set by using sample class and struct
                var testData = new List<SensorData>
                        {
                            new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } },
                            new SensorData { Value = new byte[] { 6, 7, 8, 9 }, Position = new Location { Room = 244, Floor = 1 } }
                        };

                //Serializing and saving data toofile.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Data is compressed using hello Deflate codec.
                    using (var w = AvroContainer.CreateWriter<SensorData>(buffer, Codec.Deflate))
                    {
                        using (var writer = new SequentialWriter<SensorData>(w, 24))
                        {
                            // Serialize hello data toostream by using hello sequential writer
                            testData.ForEach(writer.Write);
                        }
                    }

                    //Save stream toofile
                    Console.WriteLine("Saving serialized data toofile...");
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing data.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    using (var reader = new SequentialReader<SensorData>(
                        AvroContainer.CreateReader<SensorData>(buffer, true)))
                    {
                        var results = reader.Objects;

                        //Finally, verify that deserialized data matches hello original one
                        Console.WriteLine("Comparing Initial and Deserialized Data Sets...");
                        int count = 1;
                        var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = serialized, actual = deserialized });
                        foreach (var pair in pairs)
                        {
                            bool isEqual = this.Equal(pair.expected, pair.actual);
                            Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual);
                            count++;
                        }
                    }
                }

                //Delete hello file
                RemoveFile(path);
            }

            //
            //Helper methods
            //

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }

            //Saving memory stream tooa new file with hello given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading a file content by using hello given path tooa memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using reflection tooAvro object container file
                Sample.SerializeDeserializeUsingObjectContainersReflection();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION AND AVRO OBJECT CONTAINER FILES
    //
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    // For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-4-serialization-using-object-container-files-and-serialization-with-generic-record"></a><span data-ttu-id="04fdf-215">Exemplo 4: serialização usando arquivos do contêiner de objetos e serialização com registro genérico</span><span class="sxs-lookup"><span data-stu-id="04fdf-215">Sample 4: Serialization using object container files and serialization with generic record</span></span>
<span data-ttu-id="04fdf-216">Este exemplo é o cenário toohello semelhante em Olá <a href="#Scenario2"> segundo exemplo</a>, onde o esquema de saudação é especificada explicitamente com JSON.</span><span class="sxs-lookup"><span data-stu-id="04fdf-216">This example is similar toohello scenario in hello <a href="#Scenario2"> second example</a>, where hello schema is explicitly specified with JSON.</span></span> <span data-ttu-id="04fdf-217">Olá diferença é que aqui, esquema de saudação não presume toobe conhecido leitor toohello desserializa a ele.</span><span class="sxs-lookup"><span data-stu-id="04fdf-217">hello difference is that here, hello schema is not assumed toobe known toohello reader that deserializes it.</span></span>

<span data-ttu-id="04fdf-218">Olá conjunto de dados de teste é coletado em uma lista de [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) objetos por meio de um esquema definido explicitamente de JSON e armazenados em um arquivo de contêiner do objeto representado por Olá [ **AvroContainer** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) classe.</span><span class="sxs-lookup"><span data-stu-id="04fdf-218">hello test data set is collected into a list of [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) objects via an explicitly defined JSON schema and then stored in an object container file represented by hello [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) class.</span></span> <span data-ttu-id="04fdf-219">Esse arquivo de contêiner cria um gravador tooserialize usado Olá dados, descompactados, tooa fluxo de memória que é salvo, em seguida, o arquivo tooa.</span><span class="sxs-lookup"><span data-stu-id="04fdf-219">This container file creates a writer that is used tooserialize hello data, uncompressed, tooa memory stream that is then saved tooa file.</span></span> <span data-ttu-id="04fdf-220">Olá [ **Codec.Null** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.codec.null.aspx) parâmetro usado para criar o leitor de saudação especifica que os dados não são compactados.</span><span class="sxs-lookup"><span data-stu-id="04fdf-220">hello [**Codec.Null**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.codec.null.aspx) parameter used for creating hello reader specifies that this data is not compressed.</span></span>

<span data-ttu-id="04fdf-221">Olá dados, em seguida, ler do arquivo hello e desserializados em uma coleção de objetos.</span><span class="sxs-lookup"><span data-stu-id="04fdf-221">hello data is then read from hello file and deserialized into a collection of objects.</span></span> <span data-ttu-id="04fdf-222">Essa coleção está toohello em comparação com a lista inicial de Avro registros tooconfirm se eles são idênticos.</span><span class="sxs-lookup"><span data-stu-id="04fdf-222">This collection is compared toohello initial list of Avro records tooconfirm that they are identical.</span></span>

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro.Schema;
        using Microsoft.Hadoop.Avro;

        //This class contains all methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes a sample data set by using a generic record and Avro object container files.
            //Serialized data is not compressed.
            public void SerializeDeserializeUsingObjectContainersGenericRecord()
            {
                Console.WriteLine("SERIALIZATION USING GENERIC RECORD AND AVRO OBJECT CONTAINER FILES\n");

                //Path for Avro object container file
                string path = "AvroSampleGenericRecordNullCodec.avro";

                Console.WriteLine("Defining hello Schema and creating Sample Data Set...");

                //Define hello schema in JSON
                const string Schema = @"{
                                ""type"":""record"",
                                ""name"":""Microsoft.Hadoop.Avro.Specifications.SensorData"",
                                ""fields"":
                                    [
                                        {
                                            ""name"":""Location"",
                                            ""type"":
                                                {
                                                    ""type"":""record"",
                                                    ""name"":""Microsoft.Hadoop.Avro.Specifications.Location"",
                                                    ""fields"":
                                                        [
                                                            { ""name"":""Floor"", ""type"":""int"" },
                                                            { ""name"":""Room"", ""type"":""int"" }
                                                        ]
                                                }
                                        },
                                        { ""name"":""Value"", ""type"":""bytes"" }
                                    ]
                            }";

                //Create a generic serializer based on hello schema
                var serializer = AvroSerializer.CreateGeneric(Schema);
                var rootSchema = serializer.WriterSchema as RecordSchema;

                //Create a generic record toorepresent hello data
                var testData = new List<AvroRecord>();

                dynamic expected1 = new AvroRecord(rootSchema);
                dynamic location1 = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location1.Floor = 1;
                location1.Room = 243;
                expected1.Location = location1;
                expected1.Value = new byte[] { 1, 2, 3, 4, 5 };
                testData.Add(expected1);

                dynamic expected2 = new AvroRecord(rootSchema);
                dynamic location2 = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location2.Floor = 1;
                location2.Room = 244;
                expected2.Location = location2;
                expected2.Value = new byte[] { 6, 7, 8, 9 };
                testData.Add(expected2);

                //Serializing and saving data toofile.
                //Create a MemoryStream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Data is not compressed (Null compression codec).
                    using (var writer = AvroContainer.CreateGenericWriter(Schema, buffer, Codec.Null))
                    {
                        using (var streamWriter = new SequentialWriter<object>(writer, 24))
                        {
                            // Serialize hello data toostream by using hello sequential writer
                            testData.ForEach(streamWriter.Write);
                        }
                    }

                    Console.WriteLine("Saving serialized data toofile...");

                    //Save stream toofile
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing hello data.
                //Create a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    using (var reader = AvroContainer.CreateGenericReader(buffer))
                    {
                        using (var streamReader = new SequentialReader<object>(reader))
                        {
                            var results = streamReader.Objects;

                            Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                            //Finally, verify hello results
                            var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = (dynamic)serialized, actual = (dynamic)deserialized });
                            int count = 1;
                            foreach (var pair in pairs)
                            {
                                bool isEqual = pair.expected.Location.Floor.Equals(pair.actual.Location.Floor);
                                isEqual = isEqual && pair.expected.Location.Room.Equals(pair.actual.Location.Room);
                                isEqual = isEqual && ((byte[])pair.expected.Value).SequenceEqual((byte[])pair.actual.Value);
                                Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual.ToString());
                                count++;
                            }
                        }
                    }
                }

                //Delete hello file
                RemoveFile(path);
            }

            //
            //Helper methods
            //

            //Saving memory stream tooa new file with hello given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading a file content by using hello given path tooa memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using hello given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of hello AvroSample class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using generic record tooAvro object container file
                Sample.SerializeDeserializeUsingObjectContainersGenericRecord();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING GENERIC RECORD AND AVRO OBJECT CONTAINER FILES
    //
    // Defining hello Schema and creating Sample Data Set...
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    // For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.




## <a name="sample-5-serialization-using-object-container-files-with-a-custom-compression-codec"></a><span data-ttu-id="04fdf-223">Exemplo 5: serialização usando arquivos do contêiner de objetos com um codec de compactação personalizado</span><span class="sxs-lookup"><span data-stu-id="04fdf-223">Sample 5: Serialization using object container files with a custom compression codec</span></span>
<span data-ttu-id="04fdf-224">Olá quinto exemplo mostra como os arquivos de contêiner de objetos toouse um codec de compactação personalizada para Avro.</span><span class="sxs-lookup"><span data-stu-id="04fdf-224">hello fifth example shows how toouse a custom compression codec for Avro object container files.</span></span> <span data-ttu-id="04fdf-225">Um exemplo que contém o código de saudação para este exemplo pode ser baixado do hello [exemplos de código do Azure](http://code.msdn.microsoft.com/Serialize-data-with-the-67159111) site.</span><span class="sxs-lookup"><span data-stu-id="04fdf-225">A sample containing hello code for this example can be downloaded from hello [Azure code samples](http://code.msdn.microsoft.com/Serialize-data-with-the-67159111) site.</span></span>

<span data-ttu-id="04fdf-226">Olá [Avro especificação](http://avro.apache.org/docs/current/spec.html#Required+Codecs) permite a utilização de um codec de compactação opcional (além de muito**nulo** e **Deflate** padrões).</span><span class="sxs-lookup"><span data-stu-id="04fdf-226">hello [Avro Specification](http://avro.apache.org/docs/current/spec.html#Required+Codecs) allows usage of an optional compression codec (in addition too**Null** and **Deflate** defaults).</span></span> <span data-ttu-id="04fdf-227">Este exemplo não está implementando um novo codec como Snappy (mencionados como um codec opcional com suporte no hello [Avro especificação](http://avro.apache.org/docs/current/spec.html#snappy)).</span><span class="sxs-lookup"><span data-stu-id="04fdf-227">This example is not implementing a new codec such as Snappy (mentioned as a supported optional codec in hello [Avro Specification](http://avro.apache.org/docs/current/spec.html#snappy)).</span></span> <span data-ttu-id="04fdf-228">Ele mostra como toouse Olá implementação do .NET Framework 4.5 do hello [ **Deflate** ] [ deflate-110] codec, que fornece um melhor algoritmo de compactação com base em Olá [zlib](http://zlib.net/) biblioteca de compactação que a versão do saudação padrão do .NET Framework 4.</span><span class="sxs-lookup"><span data-stu-id="04fdf-228">It shows how toouse hello .NET Framework 4.5 implementation of hello [**Deflate**][deflate-110] codec, which provides a better compression algorithm based on hello [zlib](http://zlib.net/) compression library than hello default .NET Framework 4 version.</span></span>

    //
    // This code needs toobe compiled with hello parameter Target Framework set as ".NET Framework 4.5"
    // tooensure hello desired implementation of hello Deflate compression algorithm is used.
    // Ensure your C# project is set up accordingly.
    //

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.IO;
        using System.IO.Compression;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        #region Defining objects for serialization
        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }
        #endregion

        #region Defining custom codec based on .NET Framework V.4.5 Deflate
        //Avro.NET codec class contains two methods,
        //GetCompressedStreamOver(Stream uncompressed) and GetDecompressedStreamOver(Stream compressed),
        //which are hello key ones for data compression.
        //tooenable a custom codec, one needs tooimplement these methods for hello required codec.

        #region Defining Compression and Decompression Streams
        //DeflateStream (class from System.IO.Compression namespace that implements Deflate algorithm)
        //cannot be directly used for Avro because it does not support vital operations like Seek.
        //Thus one needs tooimplement two classes inherited from stream
        //(one for compressed and one for decompressed stream)
        //that use Deflate compression and implement all required features.
        internal sealed class CompressionStreamDeflate45 : Stream
        {
            private readonly Stream buffer;
            private DeflateStream compressionStream;

            public CompressionStreamDeflate45(Stream buffer)
            {
                Debug.Assert(buffer != null, "Buffer is not allowed toobe null.");

                this.compressionStream = new DeflateStream(buffer, CompressionLevel.Fastest, true);
                this.buffer = buffer;
            }

            public override bool CanRead
            {
                get { return this.buffer.CanRead; }
            }

            public override bool CanSeek
            {
                get { return true; }
            }

            public override bool CanWrite
            {
                get { return this.buffer.CanWrite; }
            }

            public override void Flush()
            {
                this.compressionStream.Close();
            }

            public override long Length
            {
                get { return this.buffer.Length; }
            }

            public override long Position
            {
                get
                {
                    return this.buffer.Position;
                }

                set
                {
                    this.buffer.Position = value;
                }
            }

            public override int Read(byte[] buffer, int offset, int count)
            {
                return this.buffer.Read(buffer, offset, count);
            }

            public override long Seek(long offset, SeekOrigin origin)
            {
                return this.buffer.Seek(offset, origin);
            }

            public override void SetLength(long value)
            {
                throw new NotSupportedException();
            }

            public override void Write(byte[] buffer, int offset, int count)
            {
                this.compressionStream.Write(buffer, offset, count);
            }

            protected override void Dispose(bool disposed)
            {
                base.Dispose(disposed);

                if (disposed)
                {
                    this.compressionStream.Dispose();
                    this.compressionStream = null;
                }
            }
        }

        internal sealed class DecompressionStreamDeflate45 : Stream
        {
            private readonly DeflateStream decompressed;

            public DecompressionStreamDeflate45(Stream compressed)
            {
                this.decompressed = new DeflateStream(compressed, CompressionMode.Decompress, true);
            }

            public override bool CanRead
            {
                get { return true; }
            }

            public override bool CanSeek
            {
                get { return true; }
            }

            public override bool CanWrite
            {
                get { return false; }
            }

            public override void Flush()
            {
                this.decompressed.Close();
            }

            public override long Length
            {
                get { return this.decompressed.Length; }
            }

            public override long Position
            {
                get
                {
                    return this.decompressed.Position;
                }

                set
                {
                    throw new NotSupportedException();
                }
            }

            public override int Read(byte[] buffer, int offset, int count)
            {
                return this.decompressed.Read(buffer, offset, count);
            }

            public override long Seek(long offset, SeekOrigin origin)
            {
                throw new NotSupportedException();
            }

            public override void SetLength(long value)
            {
                throw new NotSupportedException();
            }

            public override void Write(byte[] buffer, int offset, int count)
            {
                throw new NotSupportedException();
            }

            protected override void Dispose(bool disposing)
            {
                base.Dispose(disposing);

                if (disposing)
                {
                    this.decompressed.Dispose();
                }
            }
        }
        #endregion

        #region Define Codec
        //Define hello actual codec class containing hello required methods for manipulating streams:
        //GetCompressedStreamOver(Stream uncompressed) and GetDecompressedStreamOver(Stream compressed).
        //Codec class uses classes for compressed and decompressed streams defined above.
        internal sealed class DeflateCodec45 : Codec
        {

            //We merely use different IMPLEMENTATIONS of Deflate, so CodecName remains "deflate"
            public static readonly string CodecName = "deflate";

            public DeflateCodec45()
                : base(CodecName)
            {
            }

            public override Stream GetCompressedStreamOver(Stream decompressed)
            {
                if (decompressed == null)
                {
                    throw new ArgumentNullException("decompressed");
                }

                return new CompressionStreamDeflate45(decompressed);
            }

            public override Stream GetDecompressedStreamOver(Stream compressed)
            {
                if (compressed == null)
                {
                    throw new ArgumentNullException("compressed");
                }

                return new DecompressionStreamDeflate45(compressed);
            }
        }
        #endregion

        #region Define modified Codec Factory
        //Define modified codec factory toobe used in hello reader.
        //It catches hello attempt toouse "Deflate" and provide  a custom codec.
        //For all other cases, it relies on hello base class (CodecFactory).
        internal sealed class CodecFactoryDeflate45 : CodecFactory
        {

            public override Codec Create(string codecName)
            {
                if (codecName == DeflateCodec45.CodecName)
                    return new DeflateCodec45();
                else
                    return base.Create(codecName);
            }
        }
        #endregion

        #endregion

        #region Sample Class with demonstration methods
        //This class contains methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes sample data set by using reflection and Avro object container files.
            //Serialized data is compressed with hello custom compression codec (Deflate of .NET Framework 4.5).
            //
            //This sample uses memory stream for all operations related tooserialization, deserialization and
            //object container manipulation, though file stream could be easily used.
            public void SerializeDeserializeUsingObjectContainersReflectionCustomCodec()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION, AVRO OBJECT CONTAINER FILES AND CUSTOM CODEC\n");

                //Path for Avro object container file
                string path = "AvroSampleReflectionDeflate45.avro";

                //Create a data set by using sample class and struct
                var testData = new List<SensorData>
                        {
                            new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } },
                            new SensorData { Value = new byte[] { 6, 7, 8, 9 }, Position = new Location { Room = 244, Floor = 1 } }
                        };

                //Serializing and saving data toofile.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Here hello custom codec is introduced. For convenience, hello next commented code line shows how toouse built-in Deflate.
                    //Note that because hello sample deals with different IMPLEMENTATIONS of Deflate, built-in and custom codecs are interchangeable
                    //in read-write operations.
                    //using (var w = AvroContainer.CreateWriter<SensorData>(buffer, Codec.Deflate))
                    using (var w = AvroContainer.CreateWriter<SensorData>(buffer, new DeflateCodec45()))
                    {
                        using (var writer = new SequentialWriter<SensorData>(w, 24))
                        {
                            // Serialize hello data toostream using hello sequential writer
                            testData.ForEach(writer.Write);
                        }
                    }

                    //Save stream toofile
                    Console.WriteLine("Saving serialized data toofile...");
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing data.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Because of SequentialReader<T> constructor signature, an AvroSerializerSettings instance is required
                    //when codec factory is explicitly specified.
                    //You may comment hello line below if you want toouse built-in Deflate (see next comment).
                    AvroSerializerSettings settings = new AvroSerializerSettings();

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    //Here hello custom codec factory is introduced.
                    //For convenience, hello next commented code line shows how toouse built-in Deflate
                    //(no explicit Codec Factory parameter is required in this case).
                    //Note that because hello sample deals with different IMPLEMENTATIONS of Deflate, built-in and custom codecs are interchangeable
                    //in read-write operations.
                    //using (var reader = new SequentialReader<SensorData>(AvroContainer.CreateReader<SensorData>(buffer, true)))
                    using (var reader = new SequentialReader<SensorData>(
                        AvroContainer.CreateReader<SensorData>(buffer, true, settings, new CodecFactoryDeflate45())))
                    {
                        var results = reader.Objects;

                        //Finally, verify that deserialized data matches hello original one
                        Console.WriteLine("Comparing Initial and Deserialized Data Sets...");
                        bool isEqual;
                        int count = 1;
                        var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = serialized, actual = deserialized });
                        foreach (var pair in pairs)
                        {
                            isEqual = this.Equal(pair.expected, pair.actual);
                            Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual.ToString());
                            count++;
                        }
                    }
                }

                //Delete hello file
                RemoveFile(path);
            }
        #endregion

            #region Helper Methods

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }

            //Saving memory stream tooa new file with hello given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading file content by using hello given path tooa memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }
            #endregion

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample Class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using reflection tooAvro object container file using custom codec
                Sample.SerializeDeserializeUsingObjectContainersReflectionCustomCodec();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION, AVRO OBJECT CONTAINER FILES AND CUSTOM CODEC
    //
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    //For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.

## <a name="sample-6-using-avro-tooupload-data-for-hello-microsoft-azure-hdinsight-service"></a><span data-ttu-id="04fdf-229">Exemplo 6: Usando dados de tooupload Avro para Olá serviço Microsoft Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="04fdf-229">Sample 6: Using Avro tooupload data for hello Microsoft Azure HDInsight service</span></span>
<span data-ttu-id="04fdf-230">exemplo sexto Hello ilustra alguns toointeracting relacionados de técnicas programação com o serviço do Azure HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="04fdf-230">hello sixth example illustrates some programming techniques related toointeracting with hello Azure HDInsight service.</span></span> <span data-ttu-id="04fdf-231">Um exemplo que contém o código de saudação para este exemplo pode ser baixado do hello [exemplos de código do Azure](https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3) site.</span><span class="sxs-lookup"><span data-stu-id="04fdf-231">A sample containing hello code for this example can be downloaded from hello [Azure code samples](https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3) site.</span></span>

<span data-ttu-id="04fdf-232">exemplo Hello Olá seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="04fdf-232">hello sample does hello following tasks:</span></span>

* <span data-ttu-id="04fdf-233">Conecta-se tooan cluster de serviço HDInsight existente.</span><span class="sxs-lookup"><span data-stu-id="04fdf-233">Connects tooan existing HDInsight service cluster.</span></span>
* <span data-ttu-id="04fdf-234">Serializa vários arquivos CSV e carrega o armazenamento de Blob Olá resultado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="04fdf-234">Serializes several CSV files and uploads hello result tooAzure Blob storage.</span></span> <span data-ttu-id="04fdf-235">(os arquivos CSV Olá são distribuídos junto com o exemplo hello e representam uma extração dos dados históricos de estoque AMEX distribuídas por [Infochimps](http://www.infochimps.com/) por período de saudação 1970-2010.</span><span class="sxs-lookup"><span data-stu-id="04fdf-235">(hello CSV files are distributed together with hello sample and represent an extract from AMEX Stock historical data distributed by [Infochimps](http://www.infochimps.com/) for hello period 1970-2010.</span></span> <span data-ttu-id="04fdf-236">exemplo Hello lê dados de arquivos CSV, converte Olá tooinstances registros de saudação **estoque** classe e, em seguida, serializa-a por meio de reflexão.</span><span class="sxs-lookup"><span data-stu-id="04fdf-236">hello sample reads CSV file data, converts hello records tooinstances of hello **Stock** class, and then serializes them by using reflection.</span></span> <span data-ttu-id="04fdf-237">Definição de tipo de estoque é criada de um esquema JSON por meio de saudação utilitário de geração de código Microsoft Avro Library.</span><span class="sxs-lookup"><span data-stu-id="04fdf-237">Stock type definition is created from a JSON schema via hello Microsoft Avro Library code generation utility.</span></span>
* <span data-ttu-id="04fdf-238">Cria uma nova tabela externa chamada **ações** no Hive e o vincula toohello dados carregados na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="04fdf-238">Creates a new external table called **Stocks** in Hive, and links it toohello data uploaded in hello previous step.</span></span>
* <span data-ttu-id="04fdf-239">Executa uma consulta por meio do Hive em Olá **ações** tabela.</span><span class="sxs-lookup"><span data-stu-id="04fdf-239">Executes a query by using Hive over hello **Stocks** table.</span></span>

<span data-ttu-id="04fdf-240">Além disso, o exemplo hello executa um procedimento de limpeza antes e depois de executar operações principais.</span><span class="sxs-lookup"><span data-stu-id="04fdf-240">In addition, hello sample performs a clean-up procedure before and after performing major operations.</span></span> <span data-ttu-id="04fdf-241">Durante a saudação limpeza, todos Olá relacionados pastas e dados de Blob do Azure são removidas e tabela de Hive Olá é descartada.</span><span class="sxs-lookup"><span data-stu-id="04fdf-241">During hello clean-up, all of hello related Azure Blob data and folders are removed, and hello Hive table is dropped.</span></span> <span data-ttu-id="04fdf-242">Você também pode chamar o procedimento de limpeza de saudação da linha de comando do exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="04fdf-242">You can also invoke hello clean-up procedure from hello sample command line.</span></span>

<span data-ttu-id="04fdf-243">exemplo Hello tem Olá pré-requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="04fdf-243">hello sample has hello following prerequisites:</span></span>

* <span data-ttu-id="04fdf-244">Uma assinatura do Microsoft Azure ativa e a ID de assinatura correspondente.</span><span class="sxs-lookup"><span data-stu-id="04fdf-244">An active Microsoft Azure subscription and its subscription ID.</span></span>
* <span data-ttu-id="04fdf-245">Um certificado de gerenciamento para a assinatura de saudação com chave privada correspondente do hello.</span><span class="sxs-lookup"><span data-stu-id="04fdf-245">A management certificate for hello subscription with hello corresponding private key.</span></span> <span data-ttu-id="04fdf-246">certificado de saudação deve ser instalado em Olá atual usuário armazenamento privado em Olá máquina usada toorun Olá amostra.</span><span class="sxs-lookup"><span data-stu-id="04fdf-246">hello certificate should be installed in hello current user private storage on hello machine used toorun hello sample.</span></span>
* <span data-ttu-id="04fdf-247">Um cluster HDInsight ativo.</span><span class="sxs-lookup"><span data-stu-id="04fdf-247">An active HDInsight cluster.</span></span>
* <span data-ttu-id="04fdf-248">Uma conta de armazenamento do Azure vinculada cluster do HDInsight toohello de pré-requisito anterior hello, junto com a correspondente chave de acesso primária ou secundária hello.</span><span class="sxs-lookup"><span data-stu-id="04fdf-248">An Azure Storage account linked toohello HDInsight cluster from hello previous prerequisite, together with hello corresponding primary, or secondary access key.</span></span>

<span data-ttu-id="04fdf-249">Todas as informações de saudação de pré-requisitos de saudação devem ser inserido toohello arquivo de configuração de exemplo antes de exemplo hello é executado.</span><span class="sxs-lookup"><span data-stu-id="04fdf-249">All of hello information from hello prerequisites should be entered toohello sample configuration file before hello sample is run.</span></span> <span data-ttu-id="04fdf-250">Há dois toodo de maneiras possíveis-lo:</span><span class="sxs-lookup"><span data-stu-id="04fdf-250">There are two possible ways toodo it:</span></span>

* <span data-ttu-id="04fdf-251">Editar o arquivo App. config de saudação no diretório de raiz do exemplo hello e, em seguida, compilar o exemplo hello</span><span class="sxs-lookup"><span data-stu-id="04fdf-251">Edit hello app.config file in hello sample root directory and then build hello sample</span></span>
* <span data-ttu-id="04fdf-252">Primeiro compilar o exemplo hello e edite AvroHDISample.exe.config no diretório de compilação Olá</span><span class="sxs-lookup"><span data-stu-id="04fdf-252">First build hello sample, and then edit AvroHDISample.exe.config in hello build directory</span></span>

<span data-ttu-id="04fdf-253">Em ambos os casos, todas as edições devem ser feitas no hello  **<appSettings>**  seção de configurações.</span><span class="sxs-lookup"><span data-stu-id="04fdf-253">In both cases, all edits should be done in hello **<appSettings>** settings section.</span></span> <span data-ttu-id="04fdf-254">Siga os comentários de saudação no arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="04fdf-254">Follow hello comments in hello file.</span></span>
<span data-ttu-id="04fdf-255">Olá exemplo é executado na linha de comando hello, Olá comando a seguir (onde hello arquivo. zip com o exemplo hello foi considerado tooC:\AvroHDISample toobe extraído; se caso contrário, use Olá relevantes caminho do arquivo):</span><span class="sxs-lookup"><span data-stu-id="04fdf-255">hello sample is run from hello command line by executing hello following command (where hello .zip file with hello sample was assumed toobe extracted tooC:\AvroHDISample; if otherwise, use hello relevant file path):</span></span>

    AvroHDISample run C:\AvroHDISample\Data

<span data-ttu-id="04fdf-256">tooclean cluster hello, executar Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="04fdf-256">tooclean up hello cluster, run hello following command:</span></span>

    AvroHDISample clean

[deflate-100]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.100).aspx
[deflate-110]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.110).aspx
