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
# <a name="serialize-data-in-hadoop-with-hello-microsoft-avro-library"></a>Serializar os dados no Hadoop com hello Microsoft Avro Library

>[!NOTE]
>Olá Avro SDK não é suportado pela Microsoft. biblioteca de saudação é suportado pela comunidade de código aberto. fontes de saudação para a biblioteca de saudação estão localizados em [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).

Este tópico mostra como Olá toouse [Microsoft Avro Library](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro) tooserialize objetos e outros dados estruturas em fluxos toopersist-los toomemory, um banco de dados ou um arquivo. Ele também mostra como toodeserialize-os objetos originais do toorecover hello.

[!INCLUDE [windows-only](../../includes/hdinsight-windows-only.md)]

## <a name="apache-avro"></a>Apache Avro
Olá <a href="https://hadoopsdk.codeplex.com/wikipage?title=Avro%20Library" target="_blank">Microsoft Avro Library</a> implementa Olá Apache Avro sistema de serialização de dados para o ambiente do Microsoft.NET hello. O Apache Avro fornece um formato de intercâmbio de dados binários compactos para serialização. Ele usa <a href="http://www.json.org" target="_blank">JSON</a> toodefine um esquema de linguagem independente que subscreve interoperabilidade de linguagem. Os dados serializados em uma linguagem podem ser lidos em outra diferente. Atualmente, há suporte para C, C++, C#, Java, PHP, Python e Ruby. Informações detalhadas sobre o formato de saudação podem ser encontradas no hello <a href="http://avro.apache.org/docs/current/spec.html" target="_blank">especificação do Apache Avro</a>. 

>[!NOTE]
>Olá Microsoft Avro Library não dá suporte a parte de RPCs (chamadas) de procedimento remoto Olá dessa especificação.
>

representação de saudação serializada de um objeto em Olá Avro sistema consiste em duas partes: esquema e o valor real. esquema de Avro Olá descreve o modelo de dados de independente de linguagem de Olá dos dados Olá serializada com JSON. Ela é apresentada lado a lado, com uma representação binária dos dados. Com o esquema de saudação separada da representação binária da saudação permite que cada toobe objeto escrito com nenhuma sobrecarga de por valor, fazer serialização rápida e hello representação pequeno.

## <a name="hello-hadoop-scenario"></a>cenário de Hadoop Olá
formato de serialização do Apache Avro Olá é amplamente usado em outros ambientes de Apache Hadoop e HDInsight do Azure. Avro fornece uma maneira conveniente toorepresent estruturas de dados complexas dentro de um trabalho do Hadoop MapReduce. formato de saudação do Avro arquivos (arquivo de contêiner de objeto Avro) foi modelo de programação toosupport projetado Olá distribuída MapReduce. recurso de chave de saudação que permite a distribuição de saudação é que arquivos hello "divisíveis" no sentido de saudação que um pode atingir qualquer ponto em um arquivo e iniciar a leitura de um bloco específico.

## <a name="serialization-in-avro-library"></a>Serialização na biblioteca de Avro
Olá biblioteca .NET para Avro oferece suporte a duas maneiras de serializar objetos:

* **reflexão** -esquema JSON de saudação para tipos de saudação é automaticamente criado a partir Olá dados atributos de contrato de toobe de tipos de .NET Olá serializado.
* **Registro genérico** -esquema JSON de um for especificado explicitamente em um registro representado por Olá [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) classe quando nenhum tipo de .NET está presentes toodescribe Olá esquema Olá dados toobe serializado.

Quando o esquema de dados Olá é conhecido gravador de saudação tooboth e um leitor de fluxo de saudação, dados saudação podem ser enviados sem seu esquema. Em casos quando é usado um arquivo de contêiner de objetos do Avro, o esquema de saudação é armazenado no arquivo hello. Outros parâmetros, como codec Olá usado para a compactação de dados, podem ser especificados. Esses cenários são descritos mais detalhadamente e ilustrados na Olá exemplos de código a seguir:

## <a name="install-avro-library"></a>Instalar a Biblioteca do Avro
a seguir Olá é necessária antes de instalar a biblioteca de saudação:

* <a href="http://www.microsoft.com/download/details.aspx?id=17851" target="_blank">Microsoft .NET Framework 4</a>
* <a href="http://james.newtonking.com/json" target="_blank">Newtonsoft Json.NET</a> (6.0.4 ou posterior)

Observe que Olá Newtonsoft.Json.dll dependência é baixada automaticamente com a instalação de saudação do hello Microsoft Avro Library. Olá procedimento é fornecido no hello seção a seguir:

Olá Microsoft Avro Library é distribuído como um pacote do NuGet que pode ser instalado do Visual Studio via Olá procedimento a seguir:

1. Selecione Olá **projeto** -> guia **gerenciar pacotes NuGet...**
2. Pesquise "Microsoft.Hadoop.Avro" no hello **Pesquisar Online** caixa.
3. Clique em Olá **instalar** botão Avançar muito**biblioteca do Microsoft Azure HDInsight Avro**.

Observe que Olá Newtonsoft.Json.dll (> = 6.0.4) dependência também é baixada automaticamente com hello Microsoft Avro Library.

Olá código-fonte Microsoft Avro Library está disponível em [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).

## <a name="compile-schemas-using-avro-library"></a>Compilar esquemas usando a Biblioteca do Avro
Olá Microsoft Avro Library contém uma utilitário que permite a criação de tipos c# automaticamente com base em hello definido anteriormente esquema JSON a geração de código. Utilitário de geração de código Olá não é distribuído como um binário executável, mas pode ser criado facilmente por meio de saudação procedimento a seguir:

1. Baixar arquivo. zip de saudação com versão mais recente de saudação do código-fonte do SDK do HDInsight <a href="http://hadoopsdk.codeplex.com/SourceControl/latest#" target="_blank">Microsoft .NET SDK para Hadoop</a>. (Clique em Olá **baixar** ícone, Olá não **Downloads** guia.)
2. Extrai Olá diretório do SDK do HDInsight tooa na máquina de saudação com o .NET Framework 4 instalado e conectado toohello Internet para baixar os pacotes do NuGet dependência necessária. Abaixo, vamos supor que o código-fonte Olá é tooC:\SDK extraídos.
3. Pasta toohello C:\SDK\src\Microsoft.Hadoop.Avro.Tools e executar o build. bat. (Olá chamadas MSBuild do arquivo de distribuição de 32 bits de saudação de saudação do .NET Framework. Se você deseja que a versão de 64 bits toouse hello, Build. bat editar, seguinte Olá comentários dentro do arquivo hello.) Certifique-se de que a compilação de saudação foi bem-sucedida. (Em alguns sistemas, o MSBuild pode gerar avisos. Esses avisos não afetam utilitário hello como não há nenhum erro de compilação.)
4. Olá compilado utilitário está localizado em C:\SDK\Bin\Unsigned\Release\Microsoft.Hadoop.Avro.Tools.

tooget familiarizado com a sintaxe de linha de comando hello, execute Olá comando a seguir da pasta Olá onde o utilitário de geração de código hello está localizado:`Microsoft.Hadoop.Avro.Tools help /c:codegen`

Utilitário de saudação tootest, você pode gerar classes c# do arquivo de esquema Olá exemplo JSON fornecido com o código-fonte hello. Execute Olá comando a seguir:

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:

Isso deve tooproduce c# dois arquivos no diretório atual Olá: SensorData.cs e Location.cs.

lógica de saudação toounderstand que está usando o utilitário de geração de código Olá durante a conversão de tipos tooC # Olá JSON esquema, consulte o arquivo de saudação GenerationVerification.feature localizado em C:\SDK\src\Microsoft.Hadoop.Avro.Tools\Doc.

Namespaces são extraídas de esquema JSON hello, usando uma lógica Olá descrita no arquivo hello mencionado no parágrafo anterior hello. Namespaces extraídos do esquema Olá têm precedência sobre tudo o que é fornecido com o parâmetro de /n hello na linha de comando do utilitário hello. Se você quiser toooverride Olá namespaces contidos no esquema hello, use o parâmetro de /nf de saudação. Por exemplo, toochange todos os namespaces de saudação SampleJSONSchema.avsc toomy.own.nspace, execute Olá seguinte comando:

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:. /nf:my.own.nspace

## <a name="about-hello-samples"></a>Sobre exemplos de saudação
Seis exemplos fornecidos neste tópico ilustram diferentes cenários com suporte pelo Olá Microsoft Avro Library. Olá Microsoft Avro Library é projetado toowork com qualquer fluxo. Nestes exemplos, os dados são manipulados por fluxos de memória em vez de fluxos de arquivo ou bancos de dados, por questão de simplicidade e consistência. abordagem de saudação usada em um ambiente de produção depende de requisitos de cenário exato hello, fonte de dados e volume, as restrições de desempenho e outros fatores.

Olá primeiro dois exemplos mostram como tooserialize e desserializar dados em buffers de fluxo de memória por meio de reflexão e registros genéricos. Olá esquema nesses dois casos é considerada toobe compartilhado entre Olá leitores e gravadores fora de banda.

Olá terceiro e quarto exemplos mostram como tooserialize e desserializar dados usando arquivos de contêiner de objeto Olá Avro. Quando dados são armazenados em um arquivo de contêiner Avro, seu esquema sempre é armazenado com ele porque o esquema de saudação deve ser compartilhada para desserialização.

Olá contendo exemplo hello quatro primeiros exemplos podem ser baixados do hello <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-86055923" target="_blank">exemplos de código do Azure</a> site.

Olá quinto exemplo mostra como os arquivos de contêiner de objetos toouse um codec de compactação personalizada para Avro. Um exemplo que contém o código de saudação para este exemplo pode ser baixado do hello <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-67159111" target="_blank">exemplos de código do Azure</a> site.

exemplo de Hello sexto mostra como toouse Avro serialização tooupload dados tooAzure armazenamento de Blob e analisá-los usando o Hive com um cluster HDInsight (Hadoop). Ele pode ser baixado da saudação <a href="https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3" target="_blank">exemplos de código do Azure</a> site.

Estes são exemplos de seis toohello discutidos no tópico Olá links:

* <a href="#Scenario1">**Serialização com reflexão** </a> -esquema JSON Olá toobe tipos serializado é automaticamente criado a partir Olá dados atributos de contrato.
* <a href="#Scenario2">**Serialização com registro genérico** </a> -esquema JSON de saudação é especificado explicitamente em um registro quando nenhum tipo de .NET está disponível para reflexão.
* <a href="#Scenario3">**Serialização usando arquivos de contêiner do objeto com reflexão** </a> -esquema JSON de saudação é automaticamente criado e compartilhado junto com dados Olá serializado por meio de um arquivo de contêiner do objeto Avro.
* <a href="#Scenario4">**Serialização usando arquivos de contêiner do objeto com registro genérico** </a> -esquema JSON de saudação é explicitamente especificado antes de serialização hello e compartilhado junto com dados Olá por meio de um arquivo de contêiner do objeto Avro.
* <a href="#Scenario5">**Serialização usando arquivos de contêiner do objeto com um codec de compactação personalizada** </a> -exemplo hello mostra como o arquivo de contêiner com uma implementação personalizada de .NET de codec de compactação de dados Olá Deflate de objeto toocreate um Avro.
* <a href="#Scenario6">**Usando dados de tooupload Avro para Olá serviço Microsoft Azure HDInsight** </a> -exemplo hello ilustra como a serialização de Avro interage com hello serviço HDInsight. Um ativo do Azure assinatura e acesso tooan HDInsight do Azure são de cluster necessário toorun neste exemplo.

## <a name="Scenario1"></a>Exemplo 1: Serialização com reflexão
esquema JSON Olá para tipos de saudação pode ser automaticamente criada por Olá Microsoft Avro Library via reflexão de dados saudação atributos de contrato de saudação c# objetos toobe serializado. Olá Microsoft Avro Library cria um [ **IAvroSeralizer<T>**  ](http://msdn.microsoft.com/library/dn627341.aspx) tooidentify Olá campos toobe serializado.

Neste exemplo, objetos (um **SensorData** classe com um membro **local** struct) são serializados tooa fluxo de memória, e este fluxo por sua vez é desserializado. Olá resultado for comparado toohello inicial instância tooconfirm que Olá **SensorData** objeto recuperado é idêntico toohello original.

esquema Olá neste exemplo é assumida toobe compartilhado entre Olá leitores e gravadores, formato de contêiner de objeto Olá Avro não é necessário. Para obter um exemplo de como tooserialize e desserializar dados em buffers de memória por meio de reflexão com formato de contêiner de objeto de saudação ao esquema Olá deve ser compartilhada com dados hello, consulte <a href="#Scenario3">serialização usando arquivos de contêiner do objeto com reflexão</a>.

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


## <a name="sample-2-serialization-with-a-generic-record"></a>Exemplo 2: serialização com um registro genérico
Um esquema JSON pode ser especificado explicitamente em um registro genérico quando reflexão não pode ser usada porque dados saudação não podem ser representados por meio de classes .NET com um contrato de dados. Este método é mais lento do que usar reflexão. Nesses casos, esquema de saudação para dados de saudação também pode ser dinâmica, ou seja, não é conhecido em tempo de compilação. Dados representados como valores separados por vírgula (CSV) arquivos cujo esquema é desconhecida até que ele é transformado toohello Avro formato em tempo de execução é um exemplo desse tipo de cenário dinâmico.

Este exemplo mostra como toocreate e usar um [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) tooexplicitly especificar um esquema JSON, como toopopulate-lo com dados saudação e, em seguida, como tooserialize e desserializá-la. Olá resultado é comparado toohello inicial de instâncias tooconfirm que Olá recuperado do registro é idêntico toohello original.

esquema Olá neste exemplo é assumida toobe compartilhado entre Olá leitores e gravadores, formato de contêiner de objeto Olá Avro não é necessário. Para obter um exemplo de como tooserialize e desserializar dados em buffers de memória usando um registro genérico com formato de contêiner de objeto hello, quando o esquema de saudação deve ser incluída com dados serializado de saudação, consulte Olá <a href="#Scenario4">usando o contêiner do objeto de serialização arquivos com registro genérico</a> exemplo.

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


## <a name="sample-3-serialization-using-object-container-files-and-serialization-with-reflection"></a>Exemplo 3: serialização usando arquivos do contêiner de objetos e serialização com reflexão
Este exemplo é o cenário toohello semelhante em Olá <a href="#Scenario1"> primeiro exemplo</a>, onde o esquema de saudação implicitamente é especificada com reflexão. Olá diferença é que aqui, esquema de saudação não presume toobe conhecido leitor toohello desserializa a ele. Olá **SensorData** toobe objetos serializados e seu esquema implicitamente especificada são armazenados em um arquivo de contêiner de objeto Avro representado por Olá [ **AvroContainer** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) classe.

Neste exemplo com os dados de saudação são serializados [ **SequentialWriter<SensorData>**  ](http://msdn.microsoft.com/library/dn627340.aspx) e desserializado com [ **SequentialReader<SensorData>** ](http://msdn.microsoft.com/library/dn627340.aspx). resultado de Hello, em seguida, é comparado toohello instâncias iniciais tooensure identidade.

Olá dados saudação do objeto contêiner é compactado por meio de padrão de saudação [ **Deflate** ] [ deflate-100] codec de compactação do .NET Framework 4. Consulte Olá <a href="#Scenario5"> quinto exemplo</a> na toolearn neste tópico como toouse uma versão mais recente e superior do hello [ **Deflate** ] [ deflate-110] compactação codec disponível no .NET Framework 4.5.

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


## <a name="sample-4-serialization-using-object-container-files-and-serialization-with-generic-record"></a>Exemplo 4: serialização usando arquivos do contêiner de objetos e serialização com registro genérico
Este exemplo é o cenário toohello semelhante em Olá <a href="#Scenario2"> segundo exemplo</a>, onde o esquema de saudação é especificada explicitamente com JSON. Olá diferença é que aqui, esquema de saudação não presume toobe conhecido leitor toohello desserializa a ele.

Olá conjunto de dados de teste é coletado em uma lista de [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) objetos por meio de um esquema definido explicitamente de JSON e armazenados em um arquivo de contêiner do objeto representado por Olá [ **AvroContainer** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) classe. Esse arquivo de contêiner cria um gravador tooserialize usado Olá dados, descompactados, tooa fluxo de memória que é salvo, em seguida, o arquivo tooa. Olá [ **Codec.Null** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.codec.null.aspx) parâmetro usado para criar o leitor de saudação especifica que os dados não são compactados.

Olá dados, em seguida, ler do arquivo hello e desserializados em uma coleção de objetos. Essa coleção está toohello em comparação com a lista inicial de Avro registros tooconfirm se eles são idênticos.

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




## <a name="sample-5-serialization-using-object-container-files-with-a-custom-compression-codec"></a>Exemplo 5: serialização usando arquivos do contêiner de objetos com um codec de compactação personalizado
Olá quinto exemplo mostra como os arquivos de contêiner de objetos toouse um codec de compactação personalizada para Avro. Um exemplo que contém o código de saudação para este exemplo pode ser baixado do hello [exemplos de código do Azure](http://code.msdn.microsoft.com/Serialize-data-with-the-67159111) site.

Olá [Avro especificação](http://avro.apache.org/docs/current/spec.html#Required+Codecs) permite a utilização de um codec de compactação opcional (além de muito**nulo** e **Deflate** padrões). Este exemplo não está implementando um novo codec como Snappy (mencionados como um codec opcional com suporte no hello [Avro especificação](http://avro.apache.org/docs/current/spec.html#snappy)). Ele mostra como toouse Olá implementação do .NET Framework 4.5 do hello [ **Deflate** ] [ deflate-110] codec, que fornece um melhor algoritmo de compactação com base em Olá [zlib](http://zlib.net/) biblioteca de compactação que a versão do saudação padrão do .NET Framework 4.

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

## <a name="sample-6-using-avro-tooupload-data-for-hello-microsoft-azure-hdinsight-service"></a>Exemplo 6: Usando dados de tooupload Avro para Olá serviço Microsoft Azure HDInsight
exemplo sexto Hello ilustra alguns toointeracting relacionados de técnicas programação com o serviço do Azure HDInsight hello. Um exemplo que contém o código de saudação para este exemplo pode ser baixado do hello [exemplos de código do Azure](https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3) site.

exemplo Hello Olá seguintes tarefas:

* Conecta-se tooan cluster de serviço HDInsight existente.
* Serializa vários arquivos CSV e carrega o armazenamento de Blob Olá resultado tooAzure. (os arquivos CSV Olá são distribuídos junto com o exemplo hello e representam uma extração dos dados históricos de estoque AMEX distribuídas por [Infochimps](http://www.infochimps.com/) por período de saudação 1970-2010. exemplo Hello lê dados de arquivos CSV, converte Olá tooinstances registros de saudação **estoque** classe e, em seguida, serializa-a por meio de reflexão. Definição de tipo de estoque é criada de um esquema JSON por meio de saudação utilitário de geração de código Microsoft Avro Library.
* Cria uma nova tabela externa chamada **ações** no Hive e o vincula toohello dados carregados na etapa anterior hello.
* Executa uma consulta por meio do Hive em Olá **ações** tabela.

Além disso, o exemplo hello executa um procedimento de limpeza antes e depois de executar operações principais. Durante a saudação limpeza, todos Olá relacionados pastas e dados de Blob do Azure são removidas e tabela de Hive Olá é descartada. Você também pode chamar o procedimento de limpeza de saudação da linha de comando do exemplo hello.

exemplo Hello tem Olá pré-requisitos a seguir:

* Uma assinatura do Microsoft Azure ativa e a ID de assinatura correspondente.
* Um certificado de gerenciamento para a assinatura de saudação com chave privada correspondente do hello. certificado de saudação deve ser instalado em Olá atual usuário armazenamento privado em Olá máquina usada toorun Olá amostra.
* Um cluster HDInsight ativo.
* Uma conta de armazenamento do Azure vinculada cluster do HDInsight toohello de pré-requisito anterior hello, junto com a correspondente chave de acesso primária ou secundária hello.

Todas as informações de saudação de pré-requisitos de saudação devem ser inserido toohello arquivo de configuração de exemplo antes de exemplo hello é executado. Há dois toodo de maneiras possíveis-lo:

* Editar o arquivo App. config de saudação no diretório de raiz do exemplo hello e, em seguida, compilar o exemplo hello
* Primeiro compilar o exemplo hello e edite AvroHDISample.exe.config no diretório de compilação Olá

Em ambos os casos, todas as edições devem ser feitas no hello  **<appSettings>**  seção de configurações. Siga os comentários de saudação no arquivo hello.
Olá exemplo é executado na linha de comando hello, Olá comando a seguir (onde hello arquivo. zip com o exemplo hello foi considerado tooC:\AvroHDISample toobe extraído; se caso contrário, use Olá relevantes caminho do arquivo):

    AvroHDISample run C:\AvroHDISample\Data

tooclean cluster hello, executar Olá comando a seguir:

    AvroHDISample clean

[deflate-100]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.100).aspx
[deflate-110]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.110).aspx
