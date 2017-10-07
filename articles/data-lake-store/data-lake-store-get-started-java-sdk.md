---
title: "aplicativos de toodevelop de Java SDK aaaUse Olá no repositório Azure Data Lake | Microsoft Docs"
description: "Use o SDK de Java do Azure Data Lake repositório toocreate uma conta do repositório Data Lake e executar operações básicas em Olá repositório Data Lake"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: d10e09db-5232-4e84-bb50-52efc2c21887
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/28/2017
ms.author: nitinme
ms.openlocfilehash: d3bcee449c2a2a4bd2f7b241af46ecc010b6b62e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-java"></a>Introdução ao Repositório Azure Data Lake usando o Java
> [!div class="op_single_selector"]
> * [Portal](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [SDK .NET](data-lake-store-get-started-net-sdk.md)
> * [Java SDK](data-lake-store-get-started-java-sdk.md)
> * [API REST](data-lake-store-get-started-rest-api.md)
> * [CLI 2.0 do Azure](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
> 

Saiba como operações básicas do tooperform toouse hello Azure Data Lake repositório Java SDK, como criam pastas, carregar e baixar arquivos de dados, etc. Para obter mais informações sobre o Data Lake, veja [Azure Data Lake Store](data-lake-store-overview.md).

Você pode acessar documentos de API do Java SDK Olá para repositório Azure Data Lake em [documentos de API de Java do Azure Data Lake repositório](https://azure.github.io/azure-data-lake-store-java/javadoc/).

## <a name="prerequisites"></a>Pré-requisitos
* Java Development Kit (JDK 7 ou superior, usando Java versão 1.7 ou superior)
* Conta do Azure Data Lake Store. Siga as instruções de saudação em [Introdução ao repositório Azure Data Lake usando hello Azure Portal](data-lake-store-get-started-portal.md).
* [Maven](https://maven.apache.org/install.html). Este tutorial usa o Maven para compilação e dependências de projeto. Embora seja possível toobuild sem usar um sistema de compilação como Maven ou Gradle, verifique esses sistemas é muito mais fácil dependências de toomanage.
* (Opcional) E IDE como [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) ou [Eclipse](https://www.eclipse.org/downloads/) ou semelhante.

## <a name="how-do-i-authenticate-using-azure-active-directory"></a>Como faço para me autenticar usando o Azure Active Directory?
Neste tutorial, usamos um tooretrieve segredo do AD do Azure aplicativo cliente um token do Active Directory do Azure (autenticação de serviços). Usamos este token toocreate um arquivo de operações do repositório Data Lake cliente objetos tooperform e operações de diretório. Para obter instruções sobre como tooauthenticate com o uso do repositório Azure Data Lake Olá segredo do cliente, executamos Olá seguindo as etapas de alto nível:

1. Criar um aplicativo Web do Azure AD
2. Recupere a ID de saudação do cliente, o segredo do cliente e o ponto de extremidade de token para Olá aplicativo de web do AD do Azure.
3. Configure o acesso para o aplicativo de web do AD do Azure Olá em Olá repositório Data Lake arquivo/pasta que você deseja tooaccess de saudação aplicativo Java que você está criando.

Para obter instruções sobre como tooperform essas etapas, consulte [criar um aplicativo do Active Directory](data-lake-store-authenticate-using-active-directory.md).

Active Directory do Azure fornece que outras opções também tooretrieve um token. Você pode escolher um número de toosuit de mecanismos de autenticação diferente do cenário, por exemplo, um aplicativo em execução em um navegador, um aplicativo distribuído como um aplicativo de área de trabalho ou um aplicativo de servidor em execução no local ou em um virtual do Azure máquina. Você também pode escolher diferentes tipos de credenciais, como senhas, certificados, autenticação de dois fatores etc. Além disso, o Active Directory do Azure permite toosynchronize os usuários do Active Directory local com a nuvem de saudação. Para obter detalhes, confira [Cenários de autenticação do Azure Active Directory](../active-directory/active-directory-authentication-scenarios.md). 

## <a name="create-a-java-application"></a>Criar um aplicativo Java
exemplo de código Olá disponível [no GitHub](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) orienta você pelo processo de saudação de criação de arquivos no repositório de saudação, concatenação de arquivos, download de um arquivo e excluir alguns arquivos no repositório de saudação. Esta seção do artigo Olá passo a passo de partes principais de saudação do código de saudação.

1. Crie um projeto Maven usando [mvn arquétipo](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) de Olá de linha de comando ou usando uma IDE. Para obter instruções sobre como toocreate um Java projeto usando IntelliJ, consulte [aqui](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html). Para obter instruções sobre como toocreate um projeto usando o Eclipse, consulte [aqui](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm). 
2. Adicionar Olá seguir dependências tooyour Maven **pom.xml** arquivo. Adicionar Olá seguindo o trecho de texto entre hello  **\</version >** marca e hello  **\</projeto >** marca:
   
        <dependencies>
          <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-data-lake-store-sdk</artifactId>
            <version>2.1.5</version>
          </dependency>
          <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-nop</artifactId>
            <version>1.7.21</version>
          </dependency>
        </dependencies>
   
    dependência primeiro Olá é toouse Olá SDK de repositório Data Lake (`azure-data-lake-store-sdk`) do repositório de maven hello. Olá dependência segundo (`slf4j-nop`) é toospecify quais toouse de estrutura de registro em log para este aplicativo. Olá SDK de repositório Data Lake usa [slf4j](http://www.slf4j.org/) fachada de registro em log, que permite a escolha de um número de estruturas de log populares, como log4j, Java logging, logback, etc., ou nenhum registro em log. Neste exemplo, vamos Desabilitar log, portanto, usamos Olá **slf4j nop** associação. toouse outras opções de log em seu aplicativo, consulte [aqui](http://www.slf4j.org/manual.html#projectDep).

### <a name="add-hello-application-code"></a>Adicione o código do aplicativo hello
Há três partes principais de código toohello.

1. Obter o token do Active Directory do Azure Olá
2. Use Olá token toocreate um cliente do repositório Data Lake.
3. Use Olá repositório Data Lake cliente tooperform operações.

#### <a name="step-1-obtain-an-azure-active-directory-token"></a>Etapa 1: obter um token do Azure Active Directory.
Olá Data Lake repositório SDK fornece a convenientes métodos que permitem que você gerencie os tokens de segurança Olá necessário tootalk toohello conta do repositório Data Lake. No entanto, a saudação SDK não obriga que somente esses métodos sejam usados. Você pode usar outros meios de obter token, assim como ao usar o hello [SDK do Azure Active Directory](https://github.com/AzureAD/azure-activedirectory-library-for-java), ou seu próprio código personalizado.

Olá toouse token do SDK de repositório Data Lake tooobtain para aplicativo do Active Directory na Web hello criado anteriormente, use uma das subclasses de saudação do `AccessTokenProvider` (exemplo hello abaixo usa `ClientCredsTokenProvider`). Olá provedor de token caches Olá credenciais usou o token de saudação do tooobtain na memória e renova automaticamente o token de saudação se trata-se de tooexpire. É possível toocreate suas próprias subclasses de `AccessTokenProvider` para tokens são obtidos pelo seu código de cliente, mas agora vamos apenas use Olá um fornecido na Olá SDK.

Substituir **preencher em aqui** com valores reais Olá Olá aplicativo Web do Azure Active Directory.

    private static String clientId = "FILL-IN-HERE";
    private static String authTokenEndpoint = "FILL-IN-HERE";
    private static String clientKey = "FILL-IN-HERE";

    AccessTokenProvider provider = new ClientCredsTokenProvider(authTokenEndpoint, clientId, clientKey);

#### <a name="step-2-create-an-azure-data-lake-store-client-adlstoreclient-object"></a>Etapa 2: criar um objeto de cliente (ADLStoreClient) do Azure Data Lake Store
Criando um [ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/) objeto requer toospecify Olá repositório Data Lake conta hello e nome de provedor de token gerados na última etapa do hello. Observe que Olá conta do repositório Data Lake nome precisa toobe um nome de domínio totalmente qualificado. Por exemplo, substitua **FILL-IN-HERE** por algo como **mydatalakestore.azuredatalakestore.net**.

    private static String accountFQDN = "FILL-IN-HERE";  // full account FQDN, not just hello account name
    ADLStoreClient client = ADLStoreClient.createClient(accountFQDN, provider);

### <a name="step-3-use-hello-adlstoreclient-tooperform-file-and-directory-operations"></a>Etapa 3: Usar operações de arquivo e diretório de tooperform de ADLStoreClient do hello
código de saudação abaixo contém os trechos de código de exemplo de algumas operações comuns. Você pode examinar Olá completo [documentos de API do SDK do Data Lake repositório Java](https://azure.github.io/azure-data-lake-store-java/javadoc/) de saudação **ADLStoreClient** objeto toosee outras operações.

Observe que os arquivos são lidos e gravados usando fluxos Java padrão. Isso significa que você pode definir qualquer um dos fluxos de Java Olá sobre Olá que toobenefit da funcionalidade de Java padrão (por exemplo, Print fluxos de saída formatada, ou qualquer um dos fluxos de compactação ou criptografia Olá para obter funcionalidade adicional em fluxos de repositório Data Lake principal, etc.).

     // create file and write some content
     String filename = "/a/b/c.txt";
     OutputStream stream = client.createFile(filename, IfExists.OVERWRITE  );
     PrintStream out = new PrintStream(stream);
     for (int i = 1; i <= 10; i++) {
         out.println("This is line #" + i);
         out.format("This is hello same line (%d), but using formatted output. %n", i);
     }
     out.close();
    
    // set file permission
    client.setPermission(filename, "744");

    // append toofile
    stream = client.getAppendStream(filename);
    stream.write(getSampleContent());
    stream.close();

    // Read File
    InputStream in = client.getReadStream(filename);
    byte[] b = new byte[64000];
    while (in.read(b) != -1) {
        System.out.write(b);
    }
    in.close();

    // concatenate hello two files into one
    List<String> fileList = Arrays.asList("/a/b/c.txt", "/a/b/d.txt");
    client.concatenateFiles("/a/b/f.txt", fileList);

    //rename hello file
    client.rename("/a/b/f.txt", "/a/b/g.txt");

    // list directory contents
    List<DirectoryEntry> list = client.enumerateDirectory("/a/b", 2000);
    System.out.println("Directory listing for directory /a/b:");
    for (DirectoryEntry entry : list) {
        printDirectoryInfo(entry);
    }

    // delete directory along with all hello subdirectories and files in it
    client.deleteRecursive("/a");

#### <a name="step-4-build-and-run-hello-application"></a>Etapa 4: Criar e executar o aplicativo hello
1. toorun de dentro de um IDE, localize e pressione Olá **executar** botão. toorun do Maven, use [exec: exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html).
2. tooproduce um jar autônomo que você pode executar de compilação de linha de comando Olá jar com todas as dependências incluídas, usando Olá [plug-in do Maven assembly](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html). Olá pom.xml em Olá [exemplo de código de origem no github](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml) tem um exemplo de como toodo isso.

## <a name="next-steps"></a>Próximas etapas
* [Explore JavaDoc para Olá SDK de Java](https://azure.github.io/azure-data-lake-store-java/javadoc/)
* [Proteger dados no Repositório Data Lake](data-lake-store-secure-data.md)
* [Usar a Análise Data Lake do Azure com o Repositório Data Lake](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Usar o Azure HDInsight com o Repositório Data Lake](data-lake-store-hdinsight-hadoop-use-portal.md)

