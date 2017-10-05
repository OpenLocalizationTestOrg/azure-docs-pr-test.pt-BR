---
title: "Serializar dados no Hadoop – Biblioteca do Microsoft Avro – Azure | Microsoft Docs"
description: "Saiba como serializar e desserializar dados no Hadoop no HDInsight usando a Biblioteca do Microsoft Avro para manter a memória, um banco de dados ou um arquivo."
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
ms.openlocfilehash: d06bf8ff4a21e4f4b29593bac32bfa2b32601fc4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="serialize-data-in-hadoop-with-the-microsoft-avro-library"></a><span data-ttu-id="c1b4d-104">Serializar dados no Hadoop com a Biblioteca do Microsoft Avro</span><span class="sxs-lookup"><span data-stu-id="c1b4d-104">Serialize data in Hadoop with the Microsoft Avro Library</span></span>

>[!NOTE]
><span data-ttu-id="c1b4d-105">A Microsoft não dá mais suporte ao SDK do Avro.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-105">The Avro SDK is no longer supported by Microsoft.</span></span> <span data-ttu-id="c1b4d-106">A biblioteca tem suporte pela comunidade de software livre.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-106">The library is open source community supported.</span></span> <span data-ttu-id="c1b4d-107">As fontes para a biblioteca estão localizadas no [GitHub](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span><span class="sxs-lookup"><span data-stu-id="c1b4d-107">The sources for the library are located in [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span></span>

<span data-ttu-id="c1b4d-108">Este tópico mostra como usar a [Biblioteca da Microsoft Avro](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro) para serializar objetos e outras estruturas de dados em fluxos para mantê-los na memória, em um banco de dados ou em um arquivo.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-108">This topic shows how to use the [Microsoft Avro Library](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro) to serialize objects and other data structures into streams to persist them to memory, a database, or a file.</span></span> <span data-ttu-id="c1b4d-109">Ele também mostra como desserializá-los para recuperar os objetos originais.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-109">It also shows how to deserialize them to recover the original objects.</span></span>

[!INCLUDE [windows-only](../../includes/hdinsight-windows-only.md)]

## <a name="apache-avro"></a><span data-ttu-id="c1b4d-110">Apache Avro</span><span class="sxs-lookup"><span data-stu-id="c1b4d-110">Apache Avro</span></span>
<span data-ttu-id="c1b4d-111">A <a href="https://hadoopsdk.codeplex.com/wikipage?title=Avro%20Library" target="_blank">Biblioteca do Microsoft Avro</a> implementa o sistema de serialização de dados Apache Avro para o ambiente Microsoft.NET.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-111">The <a href="https://hadoopsdk.codeplex.com/wikipage?title=Avro%20Library" target="_blank">Microsoft Avro Library</a> implements the Apache Avro data serialization system for the Microsoft.NET environment.</span></span> <span data-ttu-id="c1b4d-112">O Apache Avro fornece um formato de intercâmbio de dados binários compactos para serialização.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-112">Apache Avro provides a compact binary data interchange format for serialization.</span></span> <span data-ttu-id="c1b4d-113">Ele usa o <a href="http://www.json.org" target="_blank">JSON</a> para definir um esquema com neutralidade de linguagem que subscreve a interoperabilidade da linguagem.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-113">It uses <a href="http://www.json.org" target="_blank">JSON</a> to define a language-agnostic schema that underwrites language interoperability.</span></span> <span data-ttu-id="c1b4d-114">Os dados serializados em uma linguagem podem ser lidos em outra diferente.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-114">Data serialized in one language can be read in another.</span></span> <span data-ttu-id="c1b4d-115">Atualmente, há suporte para C, C++, C#, Java, PHP, Python e Ruby.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-115">Currently C, C++, C#, Java, PHP, Python, and Ruby are supported.</span></span> <span data-ttu-id="c1b4d-116">Você encontra informações detalhadas sobre o formato na <a href="http://avro.apache.org/docs/current/spec.html" target="_blank">Especificação do Apache Avro</a>.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-116">Detailed information on the format can be found in the <a href="http://avro.apache.org/docs/current/spec.html" target="_blank">Apache Avro Specification</a>.</span></span> 

>[!NOTE]
><span data-ttu-id="c1b4d-117">A Biblioteca do Microsoft Avro não dá suporte à parte sobre RPCs (chamadas de procedimento remoto) dessa especificação.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-117">The Microsoft Avro Library does not support the remote procedure calls (RPCs) part of this specification.</span></span>
>

<span data-ttu-id="c1b4d-118">A representação serializada de um objeto no sistema Avro tem duas partes: o esquema e o valor real.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-118">The serialized representation of an object in the Avro system consists of two parts: schema and actual value.</span></span> <span data-ttu-id="c1b4d-119">O esquema do Avro descreve o modelo de dados independente de linguagem dos dados serializados com JSON.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-119">The Avro schema describes the language-independent data model of the serialized data with JSON.</span></span> <span data-ttu-id="c1b4d-120">Ela é apresentada lado a lado, com uma representação binária dos dados.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-120">It is presented side by side with a binary representation of data.</span></span> <span data-ttu-id="c1b4d-121">Colocar o esquema separado da representação binária permite que cada objeto seja programado sem sobrecargas por valor, tornando a serialização rápida e a representação pequena.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-121">Having the schema separate from the binary representation permits each object to be written with no per-value overheads, making serialization fast, and the representation small.</span></span>

## <a name="the-hadoop-scenario"></a><span data-ttu-id="c1b4d-122">O cenário do Hadoop</span><span class="sxs-lookup"><span data-stu-id="c1b4d-122">The Hadoop scenario</span></span>
<span data-ttu-id="c1b4d-123">O formato de serialização do Apache Avro é amplamente utilizado no Azure HDInsight e em outros ambientes Apache Hadoop.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-123">The Apache Avro serialization format is widely used in Azure HDInsight and other Apache Hadoop environments.</span></span> <span data-ttu-id="c1b4d-124">O Avro fornece um meio conveniente de representar estruturas de dados complexas em um trabalho MapReduce do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-124">Avro provides a convenient way to represent complex data structures within a Hadoop MapReduce job.</span></span> <span data-ttu-id="c1b4d-125">O formato dos arquivos do Avro (arquivos contêiner de objetos do Avro) foi projetado para dar suporte ao modelo de programação distribuído do MapReduce.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-125">The format of Avro files (Avro object container file) has been designed to support the distributed MapReduce programming model.</span></span> <span data-ttu-id="c1b4d-126">O recurso principal que habilita a distribuição é o fato de os arquivos serem divisíveis, no sentido de que uma pessoa pode buscar qualquer ponto em um arquivo e iniciar a leitura por meio de um bloco em específico.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-126">The key feature that enables the distribution is that the files are “splittable” in the sense that one can seek any point in a file and start reading from a particular block.</span></span>

## <a name="serialization-in-avro-library"></a><span data-ttu-id="c1b4d-127">Serialização na biblioteca de Avro</span><span class="sxs-lookup"><span data-stu-id="c1b4d-127">Serialization in Avro Library</span></span>
<span data-ttu-id="c1b4d-128">A Biblioteca do Microsoft .NET para Avro suporta dois modos de serialização de objetos:</span><span class="sxs-lookup"><span data-stu-id="c1b4d-128">The .NET Library for Avro supports two ways of serializing objects:</span></span>

* <span data-ttu-id="c1b4d-129">**reflexão** : o esquema JSON dos tipos é criado automaticamente com base nos atributos do contrato de dados dos tipos .NET a serem serializados.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-129">**reflection** - The JSON schema for the types is automatically built from the data contract attributes of the .NET types to be serialized.</span></span>
* <span data-ttu-id="c1b4d-130">**registro genérico** - um esquema JSON é especificado explicitamente em um registro representado pela classe [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) quando nenhum tipo .NET está presente para descrever o esquema dos dados a serem serializados.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-130">**generic record** - A JSON schema is explicitly specified in a record represented by the [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) class when no .NET types are present to describe the schema for the data to be serialized.</span></span>

<span data-ttu-id="c1b4d-131">Quando o esquema de dados é conhecido tanto pelo gravador quanto pelo leitor do fluxo, os dados podem ser enviados sem o seu esquema.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-131">When the data schema is known to both the writer and reader of the stream, the data can be sent without its schema.</span></span> <span data-ttu-id="c1b4d-132">Caso um arquivo contêiner de objetos do Avro seja usado, o esquema será armazenado no arquivo.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-132">In cases when an Avro object container file is used, the schema is stored within the file.</span></span> <span data-ttu-id="c1b4d-133">Você pode especificar outros parâmetros, como o codec usado para a compactação dos dados.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-133">Other parameters, such as the codec used for data compression, can be specified.</span></span> <span data-ttu-id="c1b4d-134">Esses cenários são descritos com mais detalhes e ilustrados nos exemplos de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="c1b4d-134">These scenarios are outlined in more detail and illustrated in the following code examples:</span></span>

## <a name="install-avro-library"></a><span data-ttu-id="c1b4d-135">Instalar a Biblioteca do Avro</span><span class="sxs-lookup"><span data-stu-id="c1b4d-135">Install Avro Library</span></span>
<span data-ttu-id="c1b4d-136">Os itens a seguir são necessários antes de instalar a biblioteca:</span><span class="sxs-lookup"><span data-stu-id="c1b4d-136">The following are required before you install the library:</span></span>

* <span data-ttu-id="c1b4d-137"><a href="http://www.microsoft.com/download/details.aspx?id=17851" target="_blank">Microsoft .NET Framework 4</a></span><span class="sxs-lookup"><span data-stu-id="c1b4d-137"><a href="http://www.microsoft.com/download/details.aspx?id=17851" target="_blank">Microsoft .NET Framework 4</a></span></span>
* <span data-ttu-id="c1b4d-138"><a href="http://james.newtonking.com/json" target="_blank">Newtonsoft Json.NET</a> (6.0.4 ou posterior)</span><span class="sxs-lookup"><span data-stu-id="c1b4d-138"><a href="http://james.newtonking.com/json" target="_blank">Newtonsoft Json.NET</a> (6.0.4 or later)</span></span>

<span data-ttu-id="c1b4d-139">Observe que a dependência Newtonsoft.Json.dll também é baixada automaticamente com a instalação da Biblioteca do Microsoft Avro.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-139">Note that the Newtonsoft.Json.dll dependency is downloaded automatically with the installation of the Microsoft Avro Library.</span></span> <span data-ttu-id="c1b4d-140">O procedimento é fornecido na seção a seguir:</span><span class="sxs-lookup"><span data-stu-id="c1b4d-140">The procedure is provided in the following section:</span></span>

<span data-ttu-id="c1b4d-141">A Biblioteca do Microsoft Avro é distribuída como um pacote NuGet, que pode ser instalado pelo Visual Studio usando este procedimento:</span><span class="sxs-lookup"><span data-stu-id="c1b4d-141">The Microsoft Avro Library is distributed as a NuGet package that can be installed from Visual Studio via the following procedure:</span></span>

1. <span data-ttu-id="c1b4d-142">Selecione a guia **Projeto** -> **Gerenciar Pacotes NuGet...**</span><span class="sxs-lookup"><span data-stu-id="c1b4d-142">Select the **Project** tab -> **Manage NuGet Packages...**</span></span>
2. <span data-ttu-id="c1b4d-143">Pesquise "Microsoft.Hadoop.Avro" na caixa **Pesquisar Online** .</span><span class="sxs-lookup"><span data-stu-id="c1b4d-143">Search for "Microsoft.Hadoop.Avro" in the **Search Online** box.</span></span>
3. <span data-ttu-id="c1b4d-144">Clique no botão **Instalar** próximo à **Biblioteca Avro do Microsoft Azure HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-144">Click the **Install** button next to **Microsoft Azure HDInsight Avro Library**.</span></span>

<span data-ttu-id="c1b4d-145">Observe que a dependência Newtonsoft.Json.dll (>=6.0.4) também é baixada automaticamente com a Biblioteca do Microsoft Avro.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-145">Note that the Newtonsoft.Json.dll (>=6.0.4) dependency is also downloaded automatically with the Microsoft Avro Library.</span></span>

<span data-ttu-id="c1b4d-146">O código-fonte da Biblioteca do Microsoft Avro está disponível no [GitHub](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span><span class="sxs-lookup"><span data-stu-id="c1b4d-146">The Microsoft Avro Library source code is available at [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span></span>

## <a name="compile-schemas-using-avro-library"></a><span data-ttu-id="c1b4d-147">Compilar esquemas usando a Biblioteca do Avro</span><span class="sxs-lookup"><span data-stu-id="c1b4d-147">Compile schemas using Avro Library</span></span>
<span data-ttu-id="c1b4d-148">A Biblioteca do Microsoft Avro contém um utilitário de geração de código que permite criar tipos C# de maneira automática, com base no esquema JSON definido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-148">The Microsoft Avro Library contains a code generation utility that allows creating C# types automatically based on the previously defined JSON schema.</span></span> <span data-ttu-id="c1b4d-149">O utilitário de geração de código não é distribuído como um executável binário, mas pode ser facilmente compilado com este procedimento:</span><span class="sxs-lookup"><span data-stu-id="c1b4d-149">The code generation utility is not distributed as a binary executable, but can be easily built via the following procedure:</span></span>

1. <span data-ttu-id="c1b4d-150">Baixe o arquivo .zip com a versão mais recente do código-fonte do SDK do HDInsight em <a href="http://hadoopsdk.codeplex.com/SourceControl/latest#" target="_blank">SDK do Microsoft .NET para Hadoop</a>.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-150">Download the .zip file with the latest version of HDInsight SDK source code from <a href="http://hadoopsdk.codeplex.com/SourceControl/latest#" target="_blank">Microsoft .NET SDK For Hadoop</a>.</span></span> <span data-ttu-id="c1b4d-151">(Clique no ícone **Baixar**, não na guia **Downloads**.)</span><span class="sxs-lookup"><span data-stu-id="c1b4d-151">(Click the **Download** icon, not the **Downloads** tab.)</span></span>
2. <span data-ttu-id="c1b4d-152">Extraia o SDK do HDInsight para um diretório do computador com o .NET Framework 4 instalado e conectado à Internet para baixar os pacotes NuGet de dependência necessários.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-152">Extract the HDInsight SDK to a directory on the machine with .NET Framework 4 installed and connected to the Internet for downloading necessary dependency NuGet packages.</span></span> <span data-ttu-id="c1b4d-153">No exemplo a seguir, vamos supor que o código-fonte seja extraído para C:\SDK.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-153">Below, we assume that the source code is extracted to C:\SDK.</span></span>
3. <span data-ttu-id="c1b4d-154">Vá para a pasta C:\SDK\src\Microsoft.Hadoop.Avro.Tools e execute build.bat.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-154">Go to the folder C:\SDK\src\Microsoft.Hadoop.Avro.Tools and run build.bat.</span></span> <span data-ttu-id="c1b4d-155">(O arquivo chama o MSBuild da distribuição de 32 bits do .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-155">(The file calls MSBuild from the 32-bit distribution of the .NET Framework.</span></span> <span data-ttu-id="c1b4d-156">Se quiser usar a versão de 64 bits, edite o build.bat seguindo os comentários dentro do arquivo.) Confira se a compilação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-156">If you would like to use the 64-bit version, edit build.bat, following the comments inside the file.) Ensure that the build is successful.</span></span> <span data-ttu-id="c1b4d-157">(Em alguns sistemas, o MSBuild pode gerar avisos.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-157">(On some systems, MSBuild may produce warnings.</span></span> <span data-ttu-id="c1b4d-158">Esses avisos não afetam o utilitário, desde que não haja erros de compilação.)</span><span class="sxs-lookup"><span data-stu-id="c1b4d-158">These warnings do not affect the utility as long as there are no build errors.)</span></span>
4. <span data-ttu-id="c1b4d-159">O utilitário compilado está localizado em C:\SDK\Bin\Unsigned\Release\Microsoft.Hadoop.Avro.Tools.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-159">The compiled utility is located in C:\SDK\Bin\Unsigned\Release\Microsoft.Hadoop.Avro.Tools.</span></span>

<span data-ttu-id="c1b4d-160">Para se familiarizar com o a sintaxe de linha de comando, execute este comando na pasta em que se encontra o utilitário de geração de código:`Microsoft.Hadoop.Avro.Tools help /c:codegen`</span><span class="sxs-lookup"><span data-stu-id="c1b4d-160">To get familiar with the command-line syntax, execute the following command from the folder where the code generation utility is located: `Microsoft.Hadoop.Avro.Tools help /c:codegen`</span></span>

<span data-ttu-id="c1b4d-161">Para testar o utilitário, você pode gerar classes C# por meio do arquivo de esquema JSON de exemplo fornecido com o código-fonte.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-161">To test the utility, you can generate C# classes from the sample JSON schema file provided with the source code.</span></span> <span data-ttu-id="c1b4d-162">Execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="c1b4d-162">Execute the following command:</span></span>

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:

<span data-ttu-id="c1b4d-163">Isso deve produzir dois arquivos C# no diretório atual: SensorData.cs e Location.cs.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-163">This is supposed to produce two C# files in the current directory: SensorData.cs and Location.cs.</span></span>

<span data-ttu-id="c1b4d-164">Para entender a lógica usada pelo o utilitário de geração de código ao converter o esquema JSON em tipos C#, consulte o arquivo GenerationVerification.feature localizado em C:\SDK\src\Microsoft.Hadoop.Avro.Tools\Doc.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-164">To understand the logic that the code generation utility is using while converting the JSON schema to C# types, see the file GenerationVerification.feature located in C:\SDK\src\Microsoft.Hadoop.Avro.Tools\Doc.</span></span>

<span data-ttu-id="c1b4d-165">Os namespaces são extraídos do esquema JSON usando a lógica descrita no arquivo mencionado no parágrafo anterior.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-165">Namespaces are extracted from the JSON schema, using the logic described in the file mentioned in the previous paragraph.</span></span> <span data-ttu-id="c1b4d-166">Os namespaces extraídos do esquema têm prioridade sobre qualquer coisa fornecida com o parâmetro /n na linha de comando do utilitário.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-166">Namespaces extracted from the schema take precedence over whatever is provided with the /n parameter in the utility command line.</span></span> <span data-ttu-id="c1b4d-167">Se quiser substituir os namespaces que estão no esquema, use o parâmetro /nf.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-167">If you want to override the namespaces contained within the schema, use the /nf parameter.</span></span> <span data-ttu-id="c1b4d-168">Por exemplo, para alterar todos os namespaces de SampleJSONSchema.avsc para my.own.nspace, execute este comando:</span><span class="sxs-lookup"><span data-stu-id="c1b4d-168">For example, to change all namespaces from the SampleJSONSchema.avsc to my.own.nspace, execute the following command:</span></span>

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:. /nf:my.own.nspace

## <a name="about-the-samples"></a><span data-ttu-id="c1b4d-169">Sobre as amostras</span><span class="sxs-lookup"><span data-stu-id="c1b4d-169">About the samples</span></span>
<span data-ttu-id="c1b4d-170">Cada um dos seis exemplos fornecidos neste tópico ilustra um cenário diferente com suporte pela Biblioteca do Microsoft Avro.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-170">Six examples provided in this topic illustrate different scenarios supported by the Microsoft Avro Library.</span></span> <span data-ttu-id="c1b4d-171">A Biblioteca do Microsoft Avro foi projetada para funcionar com qualquer fluxo.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-171">The Microsoft Avro Library is designed to work with any stream.</span></span> <span data-ttu-id="c1b4d-172">Nestes exemplos, os dados são manipulados por fluxos de memória em vez de fluxos de arquivo ou bancos de dados, por questão de simplicidade e consistência.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-172">In these examples, data is manipulated via memory streams rather than file streams or databases for simplicity and consistency.</span></span> <span data-ttu-id="c1b4d-173">A abordagem usada em um ambiente de produção depende dos requisitos exatos do cenário, tais como fonte de dados e volume, restrições de desempenho e outros fatores.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-173">The approach taken in a production environment depends on the exact scenario requirements, data source and volume, performance constraints, and other factors.</span></span>

<span data-ttu-id="c1b4d-174">Os primeiros dois exemplos mostram como serializar e desserializar os dados nos buffers de fluxo de memória usando reflexão e registros genéricos.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-174">The first two examples show how to serialize and deserialize data into memory stream buffers by using reflection and generic records.</span></span> <span data-ttu-id="c1b4d-175">Presume-se que o esquema nesses dois casos é compartilhado entre os leitores e gravadores fora de banda.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-175">The schema in these two cases is assumed to be shared between the readers and writers out-of-band.</span></span>

<span data-ttu-id="c1b4d-176">O terceiro e quarto exemplos mostram como serializar e desserializar os dados usando os arquivos contêiner de objetos do Avro.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-176">The third and fourth examples show how to serialize and deserialize data by using the Avro object container files.</span></span> <span data-ttu-id="c1b4d-177">Quando os dados são armazenados em um arquivo contêiner do Avro, o esquema é sempre armazenado junto com o arquivo, uma vez que o esquema precisa ser compartilhado para a desserialização.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-177">When data is stored in an Avro container file, its schema is always stored with it because the schema must be shared for deserialization.</span></span>

<span data-ttu-id="c1b4d-178">O exemplo que contém os primeiros quatro exemplos pode ser baixado do site <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-86055923" target="_blank">Exemplos de código do Azure</a> .</span><span class="sxs-lookup"><span data-stu-id="c1b4d-178">The sample containing the first four examples can be downloaded from the <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-86055923" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="c1b4d-179">O quinto exemplo mostra como usar um codec de compactação personalizado para arquivos contêiner de objetos do Avro.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-179">The fifth example shows how to use a custom compression codec for Avro object container files.</span></span> <span data-ttu-id="c1b4d-180">Uma amostra contendo o código para esse exemplo pode ser baixada no site <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-67159111" target="_blank">Exemplos de código do Azure</a> .</span><span class="sxs-lookup"><span data-stu-id="c1b4d-180">A sample containing the code for this example can be downloaded from the <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-67159111" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="c1b4d-181">O sexto exemplo mostra como usar a serialização do Avro para carregar dados no armazenamento de Blob do Azure e analisá-los usando o Hive com um cluster HDInsight (Hadoop).</span><span class="sxs-lookup"><span data-stu-id="c1b4d-181">The sixth sample shows how to use Avro serialization to upload data to Azure Blob storage and then analyze it by using Hive with an HDInsight (Hadoop) cluster.</span></span> <span data-ttu-id="c1b4d-182">Ele pode ser baixado do site <a href="https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3" target="_blank">Exemplos de código do Azure</a> .</span><span class="sxs-lookup"><span data-stu-id="c1b4d-182">It can be downloaded from the <a href="https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="c1b4d-183">Aqui estão os links aos seis exemplos abordados neste tópico:</span><span class="sxs-lookup"><span data-stu-id="c1b4d-183">Here are links to the six samples discussed in the topic:</span></span>

* <span data-ttu-id="c1b4d-184"><a href="#Scenario1">**Serialização com reflexão**</a> - o esquema JSON dos tipos a serem serializados é criado automaticamente a partir dos atributos do contrato dos dados.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-184"><a href="#Scenario1">**Serialization with reflection**</a> - The JSON schema for types to be serialized is automatically built from the data contract attributes.</span></span>
* <span data-ttu-id="c1b4d-185"><a href="#Scenario2">**Serialização com registro genérico**</a> - o esquema JSON é especificado explicitamente em um registro quando nenhum tipo .NET está disponível para a reflexão.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-185"><a href="#Scenario2">**Serialization with generic record**</a> - The JSON schema is explicitly specified in a record when no .NET type is available for reflection.</span></span>
* <span data-ttu-id="c1b4d-186"><a href="#Scenario3">**Serialização usando arquivos do contêiner de objetos com reflexão**</a> - o esquema JSON é automaticamente criado e compartilhado junto com os dados serializados por meio de um arquivo do contêiner de objetos do Avro.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-186"><a href="#Scenario3">**Serialization using object container files with reflection**</a> - The JSON schema is automatically built and shared together with the serialized data via an Avro object container file.</span></span>
* <span data-ttu-id="c1b4d-187"><a href="#Scenario4">**Serialização usando arquivos do contêiner de objetos com registro genérico**</a> - o esquema JSON é explicitamente especificado antes da serialização e compartilhado junto com os dados por meio de um arquivo do contêiner de objetos do Avro.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-187"><a href="#Scenario4">**Serialization using object container files with generic record**</a> - The JSON schema is explicitly specified before the serialization and shared together with the data via an Avro object container file.</span></span>
* <span data-ttu-id="c1b4d-188"><a href="#Scenario5">**Serialização usando arquivos do contêiner de objetos com um codec de compactação personalizado**</a> - o exemplo mostra como criar um arquivo do contêiner de objetos do Avro com uma implementação .NET personalizada do codec de compactação de dados Deflate.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-188"><a href="#Scenario5">**Serialization using object container files with a custom compression codec**</a> - The example shows how to create an Avro object container file with a customized .NET implementation of the Deflate data compression codec.</span></span>
* <span data-ttu-id="c1b4d-189"><a href="#Scenario6">**Usando o Avro para carregar dados para o serviço Microsoft Azure HDInsight**</a> - o exemplo ilustra como a serialização do Avro interage com o serviço HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-189"><a href="#Scenario6">**Using Avro to upload data for the Microsoft Azure HDInsight service**</a> - The example illustrates how Avro serialization interacts with the HDInsight service.</span></span> <span data-ttu-id="c1b4d-190">Você precisa de uma assinatura ativa do Azure e acesso a um cluster Azure HDInsight para executar este exemplo.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-190">An active Azure subscription and access to an Azure HDInsight cluster are required to run this example.</span></span>

## <span data-ttu-id="c1b4d-191"><a name="Scenario1"></a>Exemplo 1: Serialização com reflexão</span><span class="sxs-lookup"><span data-stu-id="c1b4d-191"><a name="Scenario1"></a>Sample 1: Serialization with reflection</span></span>
<span data-ttu-id="c1b4d-192">O esquema JSON dos tipos pode ser compilado automaticamente pela Biblioteca do Microsoft Avro por reflexão, com base nos atributos do contrato de dados dos objetos C# a serem serializados.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-192">The JSON schema for the types can be automatically built by the Microsoft Avro Library via reflection from the data contract attributes of the C# objects to be serialized.</span></span> <span data-ttu-id="c1b4d-193">A Biblioteca do Microsoft Avro cria um [**IAvroSeralizer<T>**](http://msdn.microsoft.com/library/dn627341.aspx) para identificar os campos a serem serializados.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-193">The Microsoft Avro Library creates an [**IAvroSeralizer<T>**](http://msdn.microsoft.com/library/dn627341.aspx) to identify the fields to be serialized.</span></span>

<span data-ttu-id="c1b4d-194">Neste exemplo, os objetos (uma classe **SensorData** com um struct membro **Local**) são serializados para um fluxo de memória, que por sua vez é desserializado.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-194">In this example, objects (a **SensorData** class with a member **Location** struct) are serialized to a memory stream, and this stream is in turn deserialized.</span></span> <span data-ttu-id="c1b4d-195">O resultado é, então, comparado à instância inicial para confirmar que o objeto **SensorData** recuperado é idêntico ao original.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-195">The result is then compared to the initial instance to confirm that the **SensorData** object recovered is identical to the original.</span></span>

<span data-ttu-id="c1b4d-196">Presume-se que o esquema neste exemplo é compartilhado entre os leitores e gravadores, portanto, o formato do contêiner de objetos do Avro não é exigido.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-196">The schema in this example is assumed to be shared between the readers and writers, so the Avro object container format is not required.</span></span> <span data-ttu-id="c1b4d-197">Para ver um exemplo de como serializar e desserializar dados em buffers de memória usando reflexão com o formato de contêiner de objetos quando o esquema precisa ser serializado com os dados, consulte <a href="#Scenario3">Serialização usando arquivos contêiner de objetos com reflexão.</a></span><span class="sxs-lookup"><span data-stu-id="c1b4d-197">For an example of how to serialize and deserialize data into memory buffers by using reflection with the object container format when the schema must be shared with the data, see <a href="#Scenario3">Serialization using object container files with reflection</a>.</span></span>

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
        //the usage of Microsoft Avro Library
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

                    //Serialize the data to the specified stream
                    avroSerializer.Serialize(buffer, expected);


                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare the stream for deserializing the data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Deserialize data from the stream and cast it to the same type used for serialization
                    var actual = avroSerializer.Deserialize(buffer);

                    Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                    //Finally, verify that deserialized data matches the original one
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

                //Serialization to memory using reflection
                Sample.SerializeDeserializeObjectUsingReflection();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key to exit.");
                Console.Read();
            }
        }
    }
    // The example is expected to display the following output:
    // SERIALIZATION USING REFLECTION
    //
    // Serializing Sample Data Set...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // Result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key to exit.


## <a name="sample-2-serialization-with-a-generic-record"></a><span data-ttu-id="c1b4d-198">Exemplo 2: serialização com um registro genérico</span><span class="sxs-lookup"><span data-stu-id="c1b4d-198">Sample 2: Serialization with a generic record</span></span>
<span data-ttu-id="c1b4d-199">Um esquema JSON pode ser especificado explicitamente em um registro genérico quando não é possível usar reflexão porque os dados não podem ser representados por classes .NET com um contrato de dados.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-199">A JSON schema can be explicitly specified in a generic record when reflection cannot be used because the data cannot be represented via .NET classes with a data contract.</span></span> <span data-ttu-id="c1b4d-200">Este método é mais lento do que usar reflexão.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-200">This method is slower than using reflection.</span></span> <span data-ttu-id="c1b4d-201">Nesses casos, o esquema dos dados também pode ser dinâmico, ou seja, pode não ser conhecido no tempo de compilação.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-201">In such cases, the schema for the data may also be dynamic, that is, not known at compile time.</span></span> <span data-ttu-id="c1b4d-202">Um exemplo desse tipo de cenário dinâmico são dados representados como arquivos CSV (valores separados por vírgulas) com esquema desconhecido até serem transformados no formato Avro em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-202">Data represented as comma-separated values (CSV) files whose schema is unknown until it is transformed to the Avro format at run time is an example of this sort of dynamic scenario.</span></span>

<span data-ttu-id="c1b4d-203">Este exemplo mostra como criar e usar um [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) para especificar explicitamente um esquema JSON e como preenchê-lo com dados para, depois, serializá-lo e desserializá-lo.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-203">This example shows how to create and use an [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) to explicitly specify a JSON schema, how to populate it with the data, and then how to serialize and deserialize it.</span></span> <span data-ttu-id="c1b4d-204">O resultado é, então, comparado à instância inicial para confirmar que o registro recuperado é idêntico ao original.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-204">The result is then compared to the initial instance to confirm that the record recovered is identical to the original.</span></span>

<span data-ttu-id="c1b4d-205">Presume-se que o esquema neste exemplo é compartilhado entre os leitores e gravadores, portanto, o formato do contêiner de objetos do Avro não é exigido.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-205">The schema in this example is assumed to be shared between the readers and writers, so the Avro object container format is not required.</span></span> <span data-ttu-id="c1b4d-206">Para ver um exemplo de como serializar e desserializar dados em buffers de memória usando um registro genérico com o formato de contêiner de objetos quando o esquema deve ser incluído com os dados serializados, consulte o exemplo <a href="#Scenario4">Serialização usando arquivos contêiner de objetos com registro genérico</a>.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-206">For an example of how to serialize and deserialize data into memory buffers by using a generic record with the object container format when the schema must be included with the serialized data, see the <a href="#Scenario4">Serialization using object container files with generic record</a> example.</span></span>

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
    //the usage of Microsoft Avro Library
    public class AvroSample
    {

        //Serialize and deserialize sample data set by using a generic record.
        //A generic record is a special class with the schema explicitly defined in JSON.
        //All serialized data should be mapped to the fields of the generic record,
        //which in turn is then serialized.
        public void SerializeDeserializeObjectUsingGenericRecords()
        {
            Console.WriteLine("SERIALIZATION USING GENERIC RECORD\n");
            Console.WriteLine("Defining the Schema and creating Sample Data Set...");

            //Define the schema in JSON
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

            //Create a generic serializer based on the schema
            var serializer = AvroSerializer.CreateGeneric(Schema);
            var rootSchema = serializer.WriterSchema as RecordSchema;

            //Create a memory stream buffer
            using (var stream = new MemoryStream())
            {
                //Create a generic record to represent the data
                dynamic location = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location.Floor = 1;
                location.Room = 243;

                dynamic expected = new AvroRecord(serializer.WriterSchema);
                expected.Location = location;
                expected.Value = new byte[] { 1, 2, 3, 4, 5 };

                Console.WriteLine("Serializing Sample Data Set...");

                //Serialize the data
                serializer.Serialize(stream, expected);

                stream.Seek(0, SeekOrigin.Begin);

                Console.WriteLine("Deserializing Sample Data Set...");

                //Deserialize the data into a generic record
                dynamic actual = serializer.Deserialize(stream);

                Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                //Finally, verify the results
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

            //Serialization to memory using generic record
            Sample.SerializeDeserializeObjectUsingGenericRecords();

            Console.WriteLine(sectionDivider);
            Console.WriteLine("Press any key to exit.");
            Console.Read();
        }
    }
    }
    // The example is expected to display the following output:
    // SERIALIZATION USING GENERIC RECORD
    //
    // Defining the Schema and creating Sample Data Set...
    // Serializing Sample Data Set...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // Result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key to exit.


## <a name="sample-3-serialization-using-object-container-files-and-serialization-with-reflection"></a><span data-ttu-id="c1b4d-207">Exemplo 3: serialização usando arquivos do contêiner de objetos e serialização com reflexão</span><span class="sxs-lookup"><span data-stu-id="c1b4d-207">Sample 3: Serialization using object container files and serialization with reflection</span></span>
<span data-ttu-id="c1b4d-208">Este exemplo é semelhante ao cenário do <a href="#Scenario1"> primeiro exemplo</a>, cujo esquema é especificado implicitamente com reflexão.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-208">This example is similar to the scenario in the <a href="#Scenario1"> first example</a>, where the schema is implicitly specified with reflection.</span></span> <span data-ttu-id="c1b4d-209">A diferença é que, aqui, não presumimos que o esquema seja conhecido do leitor que o desserializa.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-209">The difference is that here, the schema is not assumed to be known to the reader that deserializes it.</span></span> <span data-ttu-id="c1b4d-210">Os objetos **SensorData** a serem serializados e seu esquema especificado implicitamente são armazenados em um arquivo do contêiner de objetos Avro representado pela classe [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx).</span><span class="sxs-lookup"><span data-stu-id="c1b4d-210">The **SensorData** objects to be serialized and their implicitly specified schema are stored in an Avro object container file represented by the [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) class.</span></span>

<span data-ttu-id="c1b4d-211">Os dados são serializados neste exemplo com [**SequentialWriter<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx) e desserializados com [**SequentialReader<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx).</span><span class="sxs-lookup"><span data-stu-id="c1b4d-211">The data is serialized in this example with [**SequentialWriter<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx) and deserialized with [**SequentialReader<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx).</span></span> <span data-ttu-id="c1b4d-212">O resultado é, então, comparado com as instâncias iniciais para garantir a identidade.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-212">The result then is compared to the initial instances to ensure identity.</span></span>

<span data-ttu-id="c1b4d-213">Os dados no arquivo contêiner de objetos são compactados pelo codec de compactação padrão [**Deflate**][deflate-100] do .NET Framework 4.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-213">The data in the object container file is compressed via the default [**Deflate**][deflate-100] compression codec from .NET Framework 4.</span></span> <span data-ttu-id="c1b4d-214">Consulte o <a href="#Scenario5"> quinto exemplo</a> neste tópico para aprender a usar uma versão mais recente e superior do codec de compactação [**Deflate**][deflate-110], disponível no .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-214">See the <a href="#Scenario5"> fifth example</a> in this topic to learn how to use a more recent and superior version of the [**Deflate**][deflate-110] compression codec available in .NET Framework 4.5.</span></span>

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
        //the usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes the sample data set by using reflection and Avro object container files.
            //Serialized data is compressed with the Deflate codec.
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

                //Serializing and saving data to file.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects to stream.
                    //Data is compressed using the Deflate codec.
                    using (var w = AvroContainer.CreateWriter<SensorData>(buffer, Codec.Deflate))
                    {
                        using (var writer = new SequentialWriter<SensorData>(w, 24))
                        {
                            // Serialize the data to stream by using the sequential writer
                            testData.ForEach(writer.Write);
                        }
                    }

                    //Save stream to file
                    Console.WriteLine("Saving serialized data to file...");
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

                    //Prepare the stream for deserializing the data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from the given stream.
                    //It allows iterating over the deserialized objects because it implements the IEnumerable<T> interface.
                    using (var reader = new SequentialReader<SensorData>(
                        AvroContainer.CreateReader<SensorData>(buffer, true)))
                    {
                        var results = reader.Objects;

                        //Finally, verify that deserialized data matches the original one
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

                //Delete the file
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

            //Saving memory stream to a new file with the given path
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
                        Console.WriteLine("The following exception was thrown during creation and writing to the file \"{0}\"", path);
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

            //Reading a file content by using the given path to a memory stream
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
                    Console.WriteLine("The following exception was thrown during reading from the file \"{0}\"", path);
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
                        Console.WriteLine("The following exception was thrown during deleting the file \"{0}\"", path);
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

                //Serialization using reflection to Avro object container file
                Sample.SerializeDeserializeUsingObjectContainersReflection();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key to exit.");
                Console.Read();
            }
        }
    }
    // The example is expected to display the following output:
    // SERIALIZATION USING REFLECTION AND AVRO OBJECT CONTAINER FILES
    //
    // Serializing Sample Data Set...
    // Saving serialized data to file...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    // For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key to exit.


## <a name="sample-4-serialization-using-object-container-files-and-serialization-with-generic-record"></a><span data-ttu-id="c1b4d-215">Exemplo 4: serialização usando arquivos do contêiner de objetos e serialização com registro genérico</span><span class="sxs-lookup"><span data-stu-id="c1b4d-215">Sample 4: Serialization using object container files and serialization with generic record</span></span>
<span data-ttu-id="c1b4d-216">Este exemplo é semelhante ao cenário do <a href="#Scenario2"> segundo exemplo</a>, cujo esquema é especificado explicitamente com JSON.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-216">This example is similar to the scenario in the <a href="#Scenario2"> second example</a>, where the schema is explicitly specified with JSON.</span></span> <span data-ttu-id="c1b4d-217">A diferença é que, aqui, não presumimos que o esquema seja conhecido do leitor que o desserializa.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-217">The difference is that here, the schema is not assumed to be known to the reader that deserializes it.</span></span>

<span data-ttu-id="c1b4d-218">O conjunto de dados de teste é coletado em uma lista de objetos [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) por meio de um esquema JSON definido explicitamente e armazenado em um arquivo do contêiner de objetos representado pela classe [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx).</span><span class="sxs-lookup"><span data-stu-id="c1b4d-218">The test data set is collected into a list of [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) objects via an explicitly defined JSON schema and then stored in an object container file represented by the [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) class.</span></span> <span data-ttu-id="c1b4d-219">Esse arquivo contêiner cria um gravador usado para serializar os dados descompactados em um fluxo de memória que é salvo em um arquivo.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-219">This container file creates a writer that is used to serialize the data, uncompressed, to a memory stream that is then saved to a file.</span></span> <span data-ttu-id="c1b4d-220">O parâmetro [**Codec.Null**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.codec.null.aspx) usado para criar o leitor especifica que esses dados não são compactados.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-220">The [**Codec.Null**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.codec.null.aspx) parameter used for creating the reader specifies that this data is not compressed.</span></span>

<span data-ttu-id="c1b4d-221">Em seguida, os dados são lidos a partir do arquivo e desserializados em uma coleção de objetos.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-221">The data is then read from the file and deserialized into a collection of objects.</span></span> <span data-ttu-id="c1b4d-222">Essa coleção é comparada à lista inicial de registros do Avro para confirmar que são idênticos.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-222">This collection is compared to the initial list of Avro records to confirm that they are identical.</span></span>

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
        //the usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes a sample data set by using a generic record and Avro object container files.
            //Serialized data is not compressed.
            public void SerializeDeserializeUsingObjectContainersGenericRecord()
            {
                Console.WriteLine("SERIALIZATION USING GENERIC RECORD AND AVRO OBJECT CONTAINER FILES\n");

                //Path for Avro object container file
                string path = "AvroSampleGenericRecordNullCodec.avro";

                Console.WriteLine("Defining the Schema and creating Sample Data Set...");

                //Define the schema in JSON
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

                //Create a generic serializer based on the schema
                var serializer = AvroSerializer.CreateGeneric(Schema);
                var rootSchema = serializer.WriterSchema as RecordSchema;

                //Create a generic record to represent the data
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

                //Serializing and saving data to file.
                //Create a MemoryStream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects to stream.
                    //Data is not compressed (Null compression codec).
                    using (var writer = AvroContainer.CreateGenericWriter(Schema, buffer, Codec.Null))
                    {
                        using (var streamWriter = new SequentialWriter<object>(writer, 24))
                        {
                            // Serialize the data to stream by using the sequential writer
                            testData.ForEach(streamWriter.Write);
                        }
                    }

                    Console.WriteLine("Saving serialized data to file...");

                    //Save stream to file
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing the data.
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

                    //Prepare the stream for deserializing the data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from the given stream.
                    //It allows iterating over the deserialized objects because it implements the IEnumerable<T> interface.
                    using (var reader = AvroContainer.CreateGenericReader(buffer))
                    {
                        using (var streamReader = new SequentialReader<object>(reader))
                        {
                            var results = streamReader.Objects;

                            Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                            //Finally, verify the results
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

                //Delete the file
                RemoveFile(path);
            }

            //
            //Helper methods
            //

            //Saving memory stream to a new file with the given path
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
                        Console.WriteLine("The following exception was thrown during creation and writing to the file \"{0}\"", path);
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

            //Reading a file content by using the given path to a memory stream
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
                    Console.WriteLine("The following exception was thrown during reading from the file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using the given path
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
                        Console.WriteLine("The following exception was thrown during deleting the file \"{0}\"", path);
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

                //Create an instance of the AvroSample class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using generic record to Avro object container file
                Sample.SerializeDeserializeUsingObjectContainersGenericRecord();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key to exit.");
                Console.Read();
            }
        }
    }
    // The example is expected to display the following output:
    // SERIALIZATION USING GENERIC RECORD AND AVRO OBJECT CONTAINER FILES
    //
    // Defining the Schema and creating Sample Data Set...
    // Serializing Sample Data Set...
    // Saving serialized data to file...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    // For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key to exit.




## <a name="sample-5-serialization-using-object-container-files-with-a-custom-compression-codec"></a><span data-ttu-id="c1b4d-223">Exemplo 5: serialização usando arquivos do contêiner de objetos com um codec de compactação personalizado</span><span class="sxs-lookup"><span data-stu-id="c1b4d-223">Sample 5: Serialization using object container files with a custom compression codec</span></span>
<span data-ttu-id="c1b4d-224">O quinto exemplo mostra como usar um codec de compactação personalizado para arquivos contêiner de objetos do Avro.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-224">The fifth example shows how to use a custom compression codec for Avro object container files.</span></span> <span data-ttu-id="c1b4d-225">Uma amostra contendo o código para esse exemplo pode ser baixada no site [Exemplos de código do Azure](http://code.msdn.microsoft.com/Serialize-data-with-the-67159111) .</span><span class="sxs-lookup"><span data-stu-id="c1b4d-225">A sample containing the code for this example can be downloaded from the [Azure code samples](http://code.msdn.microsoft.com/Serialize-data-with-the-67159111) site.</span></span>

<span data-ttu-id="c1b4d-226">A [Especificação Avro](http://avro.apache.org/docs/current/spec.html#Required+Codecs) permite o uso de um codec de compactação opcional (além dos padrões **Null** e **Deflate**).</span><span class="sxs-lookup"><span data-stu-id="c1b4d-226">The [Avro Specification](http://avro.apache.org/docs/current/spec.html#Required+Codecs) allows usage of an optional compression codec (in addition to **Null** and **Deflate** defaults).</span></span> <span data-ttu-id="c1b4d-227">Este exemplo não implementa um codec novo como o Snappy (mencionado como codec opcional compatível na [Especificação do Avro](http://avro.apache.org/docs/current/spec.html#snappy)).</span><span class="sxs-lookup"><span data-stu-id="c1b4d-227">This example is not implementing a new codec such as Snappy (mentioned as a supported optional codec in the [Avro Specification](http://avro.apache.org/docs/current/spec.html#snappy)).</span></span> <span data-ttu-id="c1b4d-228">Ele mostra como usar a implementação do .NET Framework 4.5 do codec [**Deflate**][deflate-110], que oferece um algoritmo de compactação baseado na biblioteca de compactação [zlib](http://zlib.net/) melhor do que a versão padrão do .NET Framework 4.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-228">It shows how to use the .NET Framework 4.5 implementation of the [**Deflate**][deflate-110] codec, which provides a better compression algorithm based on the [zlib](http://zlib.net/) compression library than the default .NET Framework 4 version.</span></span>

    //
    // This code needs to be compiled with the parameter Target Framework set as ".NET Framework 4.5"
    // to ensure the desired implementation of the Deflate compression algorithm is used.
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
        //which are the key ones for data compression.
        //To enable a custom codec, one needs to implement these methods for the required codec.

        #region Defining Compression and Decompression Streams
        //DeflateStream (class from System.IO.Compression namespace that implements Deflate algorithm)
        //cannot be directly used for Avro because it does not support vital operations like Seek.
        //Thus one needs to implement two classes inherited from stream
        //(one for compressed and one for decompressed stream)
        //that use Deflate compression and implement all required features.
        internal sealed class CompressionStreamDeflate45 : Stream
        {
            private readonly Stream buffer;
            private DeflateStream compressionStream;

            public CompressionStreamDeflate45(Stream buffer)
            {
                Debug.Assert(buffer != null, "Buffer is not allowed to be null.");

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
        //Define the actual codec class containing the required methods for manipulating streams:
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
        //Define modified codec factory to be used in the reader.
        //It catches the attempt to use "Deflate" and provide  a custom codec.
        //For all other cases, it relies on the base class (CodecFactory).
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
        //the usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes sample data set by using reflection and Avro object container files.
            //Serialized data is compressed with the custom compression codec (Deflate of .NET Framework 4.5).
            //
            //This sample uses memory stream for all operations related to serialization, deserialization and
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

                //Serializing and saving data to file.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects to stream.
                    //Here the custom codec is introduced. For convenience, the next commented code line shows how to use built-in Deflate.
                    //Note that because the sample deals with different IMPLEMENTATIONS of Deflate, built-in and custom codecs are interchangeable
                    //in read-write operations.
                    //using (var w = AvroContainer.CreateWriter<SensorData>(buffer, Codec.Deflate))
                    using (var w = AvroContainer.CreateWriter<SensorData>(buffer, new DeflateCodec45()))
                    {
                        using (var writer = new SequentialWriter<SensorData>(w, 24))
                        {
                            // Serialize the data to stream using the sequential writer
                            testData.ForEach(writer.Write);
                        }
                    }

                    //Save stream to file
                    Console.WriteLine("Saving serialized data to file...");
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

                    //Prepare the stream for deserializing the data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Because of SequentialReader<T> constructor signature, an AvroSerializerSettings instance is required
                    //when codec factory is explicitly specified.
                    //You may comment the line below if you want to use built-in Deflate (see next comment).
                    AvroSerializerSettings settings = new AvroSerializerSettings();

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from the given stream.
                    //It allows iterating over the deserialized objects because it implements the IEnumerable<T> interface.
                    //Here the custom codec factory is introduced.
                    //For convenience, the next commented code line shows how to use built-in Deflate
                    //(no explicit Codec Factory parameter is required in this case).
                    //Note that because the sample deals with different IMPLEMENTATIONS of Deflate, built-in and custom codecs are interchangeable
                    //in read-write operations.
                    //using (var reader = new SequentialReader<SensorData>(AvroContainer.CreateReader<SensorData>(buffer, true)))
                    using (var reader = new SequentialReader<SensorData>(
                        AvroContainer.CreateReader<SensorData>(buffer, true, settings, new CodecFactoryDeflate45())))
                    {
                        var results = reader.Objects;

                        //Finally, verify that deserialized data matches the original one
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

                //Delete the file
                RemoveFile(path);
            }
        #endregion

            #region Helper Methods

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }

            //Saving memory stream to a new file with the given path
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
                        Console.WriteLine("The following exception was thrown during creation and writing to the file \"{0}\"", path);
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

            //Reading file content by using the given path to a memory stream
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
                    Console.WriteLine("The following exception was thrown during reading from the file \"{0}\"", path);
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
                        Console.WriteLine("The following exception was thrown during deleting the file \"{0}\"", path);
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

                //Serialization using reflection to Avro object container file using custom codec
                Sample.SerializeDeserializeUsingObjectContainersReflectionCustomCodec();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key to exit.");
                Console.Read();
            }
        }
    }
    // The example is expected to display the following output:
    // SERIALIZATION USING REFLECTION, AVRO OBJECT CONTAINER FILES AND CUSTOM CODEC
    //
    // Serializing Sample Data Set...
    // Saving serialized data to file...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    //For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key to exit.

## <a name="sample-6-using-avro-to-upload-data-for-the-microsoft-azure-hdinsight-service"></a><span data-ttu-id="c1b4d-229">Exemplo 6: usando o Avro para carregar dados para o serviço do Microsoft Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="c1b4d-229">Sample 6: Using Avro to upload data for the Microsoft Azure HDInsight service</span></span>
<span data-ttu-id="c1b4d-230">O sexto exemplo ilustra algumas técnicas de programação relacionadas à interação com o serviço do Microsoft Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-230">The sixth example illustrates some programming techniques related to interacting with the Azure HDInsight service.</span></span> <span data-ttu-id="c1b4d-231">Uma amostra contendo o código para esse exemplo pode ser baixada no site [Exemplos de código do Azure](https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3) .</span><span class="sxs-lookup"><span data-stu-id="c1b4d-231">A sample containing the code for this example can be downloaded from the [Azure code samples](https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3) site.</span></span>

<span data-ttu-id="c1b4d-232">O exemplo a seguir realiza as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="c1b4d-232">The sample does the following tasks:</span></span>

* <span data-ttu-id="c1b4d-233">Conecta-se a um cluster de serviço do HDInsight existente.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-233">Connects to an existing HDInsight service cluster.</span></span>
* <span data-ttu-id="c1b4d-234">Serializa diversos arquivos CSV e carrega o resultado na Armazenamento de Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-234">Serializes several CSV files and uploads the result to Azure Blob storage.</span></span> <span data-ttu-id="c1b4d-235">(Os arquivos CSV são distribuídos junto com o exemplo e representam amostras de dados históricos da Bolsa de Valores AMEX distribuídos pela [Infochimps](http://www.infochimps.com/) para o período de 1970-2010.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-235">(The CSV files are distributed together with the sample and represent an extract from AMEX Stock historical data distributed by [Infochimps](http://www.infochimps.com/) for the period 1970-2010.</span></span> <span data-ttu-id="c1b4d-236">O exemplo lê os dados dos arquivos CSV, converte os registros em instâncias da classe **Stock** (Ações) e os serializa usando reflexão.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-236">The sample reads CSV file data, converts the records to instances of the **Stock** class, and then serializes them by using reflection.</span></span> <span data-ttu-id="c1b4d-237">A definição do tipo de ação é criada com base no esquema JSON pelo utilitário de geração de código da Biblioteca do Microsoft Avro.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-237">Stock type definition is created from a JSON schema via the Microsoft Avro Library code generation utility.</span></span>
* <span data-ttu-id="c1b4d-238">Cria uma nova tabela externa chamada **Stocks** (Ações) no Hive e a vincula aos dados carregados na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-238">Creates a new external table called **Stocks** in Hive, and links it to the data uploaded in the previous step.</span></span>
* <span data-ttu-id="c1b4d-239">Executa uma consulta usando o Hive na tabela **Stocks** .</span><span class="sxs-lookup"><span data-stu-id="c1b4d-239">Executes a query by using Hive over the **Stocks** table.</span></span>

<span data-ttu-id="c1b4d-240">Além disso, o exemplo realiza um procedimento de limpeza antes e depois da realização de operações mais importantes.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-240">In addition, the sample performs a clean-up procedure before and after performing major operations.</span></span> <span data-ttu-id="c1b4d-241">Durante a limpeza, todos os dados e pastas de Blob do Azure relacionados são removidos e a tabela do Hive é removida.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-241">During the clean-up, all of the related Azure Blob data and folders are removed, and the Hive table is dropped.</span></span> <span data-ttu-id="c1b4d-242">Você também pode invocar um procedimento de limpeza na linha de comando do exemplo.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-242">You can also invoke the clean-up procedure from the sample command line.</span></span>

<span data-ttu-id="c1b4d-243">O exemplo tem os seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="c1b4d-243">The sample has the following prerequisites:</span></span>

* <span data-ttu-id="c1b4d-244">Uma assinatura do Microsoft Azure ativa e a ID de assinatura correspondente.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-244">An active Microsoft Azure subscription and its subscription ID.</span></span>
* <span data-ttu-id="c1b4d-245">Um certificado de gerenciamento da assinatura com a chave privada correspondente.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-245">A management certificate for the subscription with the corresponding private key.</span></span> <span data-ttu-id="c1b4d-246">O Certificado deve ser instalado no armazenamento privado do usuário atual no computador usado para executar o exemplo.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-246">The certificate should be installed in the current user private storage on the machine used to run the sample.</span></span>
* <span data-ttu-id="c1b4d-247">Um cluster HDInsight ativo.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-247">An active HDInsight cluster.</span></span>
* <span data-ttu-id="c1b4d-248">Uma conta de Armazenamento do Azure vinculada ao cluster HDInsight do pré-requisito anterior, juntamente com a chave de acesso primária ou secundária correspondente.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-248">An Azure Storage account linked to the HDInsight cluster from the previous prerequisite, together with the corresponding primary, or secondary access key.</span></span>

<span data-ttu-id="c1b4d-249">Todas as informações dos pré-requisitos devem ser inseridas no arquivo de configuração do exemplo antes deste ser executado.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-249">All of the information from the prerequisites should be entered to the sample configuration file before the sample is run.</span></span> <span data-ttu-id="c1b4d-250">Há duas maneiras possíveis de fazer isso:</span><span class="sxs-lookup"><span data-stu-id="c1b4d-250">There are two possible ways to do it:</span></span>

* <span data-ttu-id="c1b4d-251">Editar o arquivo app.config no diretório raiz do exemplo e compilar o exemplo</span><span class="sxs-lookup"><span data-stu-id="c1b4d-251">Edit the app.config file in the sample root directory and then build the sample</span></span>
* <span data-ttu-id="c1b4d-252">Primeiro compilar o exemplo e, depois, editar o AvroHDISample.exe.config no diretório de compilação</span><span class="sxs-lookup"><span data-stu-id="c1b4d-252">First build the sample, and then edit AvroHDISample.exe.config in the build directory</span></span>

<span data-ttu-id="c1b4d-253">Em ambos os casos, todas as edições devem ser feitas na seção de configurações **<appSettings>**.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-253">In both cases, all edits should be done in the **<appSettings>** settings section.</span></span> <span data-ttu-id="c1b4d-254">Siga os comentários no arquivo.</span><span class="sxs-lookup"><span data-stu-id="c1b4d-254">Follow the comments in the file.</span></span>
<span data-ttu-id="c1b4d-255">O exemplo é executado na linha de comando pela execução do seguinte comando (presume-se que o arquivo .zip com o exemplo tenha sido extraído para C:\AvroHDISample; caso contrário, use o caminho de arquivo relevante):</span><span class="sxs-lookup"><span data-stu-id="c1b4d-255">The sample is run from the command line by executing the following command (where the .zip file with the sample was assumed to be extracted to C:\AvroHDISample; if otherwise, use the relevant file path):</span></span>

    AvroHDISample run C:\AvroHDISample\Data

<span data-ttu-id="c1b4d-256">Para limpar o cluster, execute este comando:</span><span class="sxs-lookup"><span data-stu-id="c1b4d-256">To clean up the cluster, run the following command:</span></span>

    AvroHDISample clean

[deflate-100]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.100).aspx
[deflate-110]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.110).aspx
