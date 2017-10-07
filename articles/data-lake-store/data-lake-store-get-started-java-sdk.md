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
# <a name="get-started-with-azure-data-lake-store-using-java"></a><span data-ttu-id="d8e77-103">Introdução ao Repositório Azure Data Lake usando o Java</span><span class="sxs-lookup"><span data-stu-id="d8e77-103">Get started with Azure Data Lake Store using Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d8e77-104">Portal</span><span class="sxs-lookup"><span data-stu-id="d8e77-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="d8e77-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d8e77-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="d8e77-106">SDK .NET</span><span class="sxs-lookup"><span data-stu-id="d8e77-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="d8e77-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="d8e77-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="d8e77-108">API REST</span><span class="sxs-lookup"><span data-stu-id="d8e77-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="d8e77-109">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="d8e77-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="d8e77-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="d8e77-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="d8e77-111">Python</span><span class="sxs-lookup"><span data-stu-id="d8e77-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

<span data-ttu-id="d8e77-112">Saiba como operações básicas do tooperform toouse hello Azure Data Lake repositório Java SDK, como criam pastas, carregar e baixar arquivos de dados, etc. Para obter mais informações sobre o Data Lake, veja [Azure Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d8e77-112">Learn how toouse hello Azure Data Lake Store Java SDK tooperform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

<span data-ttu-id="d8e77-113">Você pode acessar documentos de API do Java SDK Olá para repositório Azure Data Lake em [documentos de API de Java do Azure Data Lake repositório](https://azure.github.io/azure-data-lake-store-java/javadoc/).</span><span class="sxs-lookup"><span data-stu-id="d8e77-113">You can access hello Java SDK API docs for Azure Data Lake Store at [Azure Data Lake Store Java API docs](https://azure.github.io/azure-data-lake-store-java/javadoc/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d8e77-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d8e77-114">Prerequisites</span></span>
* <span data-ttu-id="d8e77-115">Java Development Kit (JDK 7 ou superior, usando Java versão 1.7 ou superior)</span><span class="sxs-lookup"><span data-stu-id="d8e77-115">Java Development Kit (JDK 7 or higher, using Java version 1.7 or higher)</span></span>
* <span data-ttu-id="d8e77-116">Conta do Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d8e77-116">Azure Data Lake Store account.</span></span> <span data-ttu-id="d8e77-117">Siga as instruções de saudação em [Introdução ao repositório Azure Data Lake usando hello Azure Portal](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d8e77-117">Follow hello instructions at [Get started with Azure Data Lake Store using hello Azure Portal](data-lake-store-get-started-portal.md).</span></span>
* <span data-ttu-id="d8e77-118">[Maven](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="d8e77-118">[Maven](https://maven.apache.org/install.html).</span></span> <span data-ttu-id="d8e77-119">Este tutorial usa o Maven para compilação e dependências de projeto.</span><span class="sxs-lookup"><span data-stu-id="d8e77-119">This tutorial uses Maven for build and project dependencies.</span></span> <span data-ttu-id="d8e77-120">Embora seja possível toobuild sem usar um sistema de compilação como Maven ou Gradle, verifique esses sistemas é muito mais fácil dependências de toomanage.</span><span class="sxs-lookup"><span data-stu-id="d8e77-120">Although it is possible toobuild without using a build system like Maven or Gradle, these systems make is much easier toomanage dependencies.</span></span>
* <span data-ttu-id="d8e77-121">(Opcional) E IDE como [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) ou [Eclipse](https://www.eclipse.org/downloads/) ou semelhante.</span><span class="sxs-lookup"><span data-stu-id="d8e77-121">(Optional) And IDE like [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) or [Eclipse](https://www.eclipse.org/downloads/) or similar.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="d8e77-122">Como faço para me autenticar usando o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d8e77-122">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="d8e77-123">Neste tutorial, usamos um tooretrieve segredo do AD do Azure aplicativo cliente um token do Active Directory do Azure (autenticação de serviços).</span><span class="sxs-lookup"><span data-stu-id="d8e77-123">In this tutorial we use a Azure AD application client secret tooretrieve an Azure Active Directory token (service-to-service authentication).</span></span> <span data-ttu-id="d8e77-124">Usamos este token toocreate um arquivo de operações do repositório Data Lake cliente objetos tooperform e operações de diretório.</span><span class="sxs-lookup"><span data-stu-id="d8e77-124">We use this token toocreate an Data Lake Store client object tooperform operations file and directory operations.</span></span> <span data-ttu-id="d8e77-125">Para obter instruções sobre como tooauthenticate com o uso do repositório Azure Data Lake Olá segredo do cliente, executamos Olá seguindo as etapas de alto nível:</span><span class="sxs-lookup"><span data-stu-id="d8e77-125">For instructions on how tooauthenticate with Azure Data Lake Store using hello client secret, we perform hello following high-level steps:</span></span>

1. <span data-ttu-id="d8e77-126">Criar um aplicativo Web do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8e77-126">Create an Azure AD web application</span></span>
2. <span data-ttu-id="d8e77-127">Recupere a ID de saudação do cliente, o segredo do cliente e o ponto de extremidade de token para Olá aplicativo de web do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="d8e77-127">Retrieve hello client ID, client secret, and token endpoint for hello Azure AD web application.</span></span>
3. <span data-ttu-id="d8e77-128">Configure o acesso para o aplicativo de web do AD do Azure Olá em Olá repositório Data Lake arquivo/pasta que você deseja tooaccess de saudação aplicativo Java que você está criando.</span><span class="sxs-lookup"><span data-stu-id="d8e77-128">Configure access for hello Azure AD web application on hello Data Lake Store file/folder that you want tooaccess from hello Java application you are creating.</span></span>

<span data-ttu-id="d8e77-129">Para obter instruções sobre como tooperform essas etapas, consulte [criar um aplicativo do Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="d8e77-129">For instructions on how tooperform these steps, see [Create an Active Directory application](data-lake-store-authenticate-using-active-directory.md).</span></span>

<span data-ttu-id="d8e77-130">Active Directory do Azure fornece que outras opções também tooretrieve um token.</span><span class="sxs-lookup"><span data-stu-id="d8e77-130">Azure Active Directory provides other options as well tooretrieve a token.</span></span> <span data-ttu-id="d8e77-131">Você pode escolher um número de toosuit de mecanismos de autenticação diferente do cenário, por exemplo, um aplicativo em execução em um navegador, um aplicativo distribuído como um aplicativo de área de trabalho ou um aplicativo de servidor em execução no local ou em um virtual do Azure máquina.</span><span class="sxs-lookup"><span data-stu-id="d8e77-131">You can pick from a number of different authentication mechanisms toosuit your scenario, for example, an application running in a browser, an application distributed as a desktop application, or a server application running on-premises or in an Azure virtual machine.</span></span> <span data-ttu-id="d8e77-132">Você também pode escolher diferentes tipos de credenciais, como senhas, certificados, autenticação de dois fatores etc. Além disso, o Active Directory do Azure permite toosynchronize os usuários do Active Directory local com a nuvem de saudação.</span><span class="sxs-lookup"><span data-stu-id="d8e77-132">You can also pick from different types of credentials like passwords, certificates, 2-factor authentication, etc. In addition, Azure Active Directory allows you toosynchronize your on-premises Active Directory users with hello cloud.</span></span> <span data-ttu-id="d8e77-133">Para obter detalhes, confira [Cenários de autenticação do Azure Active Directory](../active-directory/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="d8e77-133">For details, see [Authentication Scenarios for Azure Active Directory](../active-directory/active-directory-authentication-scenarios.md).</span></span> 

## <a name="create-a-java-application"></a><span data-ttu-id="d8e77-134">Criar um aplicativo Java</span><span class="sxs-lookup"><span data-stu-id="d8e77-134">Create a Java application</span></span>
<span data-ttu-id="d8e77-135">exemplo de código Olá disponível [no GitHub](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) orienta você pelo processo de saudação de criação de arquivos no repositório de saudação, concatenação de arquivos, download de um arquivo e excluir alguns arquivos no repositório de saudação.</span><span class="sxs-lookup"><span data-stu-id="d8e77-135">hello code sample available [on GitHub](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) walks you through hello process of creating files in hello store, concatenating files, downloading a file, and deleting some files in hello store.</span></span> <span data-ttu-id="d8e77-136">Esta seção do artigo Olá passo a passo de partes principais de saudação do código de saudação.</span><span class="sxs-lookup"><span data-stu-id="d8e77-136">This section of hello article walk you through hello main parts of hello code.</span></span>

1. <span data-ttu-id="d8e77-137">Crie um projeto Maven usando [mvn arquétipo](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) de Olá de linha de comando ou usando uma IDE.</span><span class="sxs-lookup"><span data-stu-id="d8e77-137">Create a Maven project using [mvn archetype](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) from hello command-line or using an IDE.</span></span> <span data-ttu-id="d8e77-138">Para obter instruções sobre como toocreate um Java projeto usando IntelliJ, consulte [aqui](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html).</span><span class="sxs-lookup"><span data-stu-id="d8e77-138">For instructions on how toocreate a Java project using IntelliJ, see [here](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html).</span></span> <span data-ttu-id="d8e77-139">Para obter instruções sobre como toocreate um projeto usando o Eclipse, consulte [aqui](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm).</span><span class="sxs-lookup"><span data-stu-id="d8e77-139">For instructions on how toocreate a project using Eclipse, see [here](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm).</span></span> 
2. <span data-ttu-id="d8e77-140">Adicionar Olá seguir dependências tooyour Maven **pom.xml** arquivo.</span><span class="sxs-lookup"><span data-stu-id="d8e77-140">Add hello following dependencies tooyour Maven **pom.xml** file.</span></span> <span data-ttu-id="d8e77-141">Adicionar Olá seguindo o trecho de texto entre hello  **\</version >** marca e hello  **\</projeto >** marca:</span><span class="sxs-lookup"><span data-stu-id="d8e77-141">Add hello following snippet of text between hello **\</version>** tag and hello **\</project>** tag:</span></span>
   
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
   
    <span data-ttu-id="d8e77-142">dependência primeiro Olá é toouse Olá SDK de repositório Data Lake (`azure-data-lake-store-sdk`) do repositório de maven hello.</span><span class="sxs-lookup"><span data-stu-id="d8e77-142">hello first dependency is toouse hello Data Lake Store SDK (`azure-data-lake-store-sdk`) from hello maven repository.</span></span> <span data-ttu-id="d8e77-143">Olá dependência segundo (`slf4j-nop`) é toospecify quais toouse de estrutura de registro em log para este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d8e77-143">hello second dependency (`slf4j-nop`) is toospecify which logging framework toouse for this application.</span></span> <span data-ttu-id="d8e77-144">Olá SDK de repositório Data Lake usa [slf4j](http://www.slf4j.org/) fachada de registro em log, que permite a escolha de um número de estruturas de log populares, como log4j, Java logging, logback, etc., ou nenhum registro em log.</span><span class="sxs-lookup"><span data-stu-id="d8e77-144">hello Data Lake Store SDK uses [slf4j](http://www.slf4j.org/) logging façade, which lets you choose from a number of popular logging frameworks, like log4j, Java logging, logback, etc., or no logging.</span></span> <span data-ttu-id="d8e77-145">Neste exemplo, vamos Desabilitar log, portanto, usamos Olá **slf4j nop** associação.</span><span class="sxs-lookup"><span data-stu-id="d8e77-145">For this example, we will disable logging, hence we use hello **slf4j-nop** binding.</span></span> <span data-ttu-id="d8e77-146">toouse outras opções de log em seu aplicativo, consulte [aqui](http://www.slf4j.org/manual.html#projectDep).</span><span class="sxs-lookup"><span data-stu-id="d8e77-146">toouse other logging options in your app, see [here](http://www.slf4j.org/manual.html#projectDep).</span></span>

### <a name="add-hello-application-code"></a><span data-ttu-id="d8e77-147">Adicione o código do aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="d8e77-147">Add hello application code</span></span>
<span data-ttu-id="d8e77-148">Há três partes principais de código toohello.</span><span class="sxs-lookup"><span data-stu-id="d8e77-148">There are three main parts toohello code.</span></span>

1. <span data-ttu-id="d8e77-149">Obter o token do Active Directory do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="d8e77-149">Obtain hello Azure Active Directory token</span></span>
2. <span data-ttu-id="d8e77-150">Use Olá token toocreate um cliente do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="d8e77-150">Use hello token toocreate a Data Lake Store client.</span></span>
3. <span data-ttu-id="d8e77-151">Use Olá repositório Data Lake cliente tooperform operações.</span><span class="sxs-lookup"><span data-stu-id="d8e77-151">Use hello Data Lake Store client tooperform operations.</span></span>

#### <a name="step-1-obtain-an-azure-active-directory-token"></a><span data-ttu-id="d8e77-152">Etapa 1: obter um token do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d8e77-152">Step 1: Obtain an Azure Active Directory token.</span></span>
<span data-ttu-id="d8e77-153">Olá Data Lake repositório SDK fornece a convenientes métodos que permitem que você gerencie os tokens de segurança Olá necessário tootalk toohello conta do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="d8e77-153">hello Data Lake Store SDK provides convenient methods that let you manage hello security tokens needed tootalk toohello Data Lake Store account.</span></span> <span data-ttu-id="d8e77-154">No entanto, a saudação SDK não obriga que somente esses métodos sejam usados.</span><span class="sxs-lookup"><span data-stu-id="d8e77-154">However, hello SDK does not mandate that only these methods be used.</span></span> <span data-ttu-id="d8e77-155">Você pode usar outros meios de obter token, assim como ao usar o hello [SDK do Azure Active Directory](https://github.com/AzureAD/azure-activedirectory-library-for-java), ou seu próprio código personalizado.</span><span class="sxs-lookup"><span data-stu-id="d8e77-155">You can use any other means of obtaining token as well, like using hello [Azure Active Directory SDK](https://github.com/AzureAD/azure-activedirectory-library-for-java), or your own custom code.</span></span>

<span data-ttu-id="d8e77-156">Olá toouse token do SDK de repositório Data Lake tooobtain para aplicativo do Active Directory na Web hello criado anteriormente, use uma das subclasses de saudação do `AccessTokenProvider` (exemplo hello abaixo usa `ClientCredsTokenProvider`).</span><span class="sxs-lookup"><span data-stu-id="d8e77-156">toouse hello Data Lake Store SDK tooobtain token for hello Active Directory Web application you created earlier, use one of hello subclasses of `AccessTokenProvider` (hello example below uses `ClientCredsTokenProvider`).</span></span> <span data-ttu-id="d8e77-157">Olá provedor de token caches Olá credenciais usou o token de saudação do tooobtain na memória e renova automaticamente o token de saudação se trata-se de tooexpire.</span><span class="sxs-lookup"><span data-stu-id="d8e77-157">hello token provider caches hello creds used tooobtain hello token in memory, and automatically renews hello token if it is about tooexpire.</span></span> <span data-ttu-id="d8e77-158">É possível toocreate suas próprias subclasses de `AccessTokenProvider` para tokens são obtidos pelo seu código de cliente, mas agora vamos apenas use Olá um fornecido na Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="d8e77-158">It is possible toocreate your own subclasses of `AccessTokenProvider` so tokens are obtained by your customer code, but for now let's just use hello one provided in hello SDK.</span></span>

<span data-ttu-id="d8e77-159">Substituir **preencher em aqui** com valores reais Olá Olá aplicativo Web do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d8e77-159">Replace **FILL-IN-HERE** with hello actual values for hello Azure Active Directory Web application.</span></span>

    private static String clientId = "FILL-IN-HERE";
    private static String authTokenEndpoint = "FILL-IN-HERE";
    private static String clientKey = "FILL-IN-HERE";

    AccessTokenProvider provider = new ClientCredsTokenProvider(authTokenEndpoint, clientId, clientKey);

#### <a name="step-2-create-an-azure-data-lake-store-client-adlstoreclient-object"></a><span data-ttu-id="d8e77-160">Etapa 2: criar um objeto de cliente (ADLStoreClient) do Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d8e77-160">Step 2: Create an Azure Data Lake Store client (ADLStoreClient) object</span></span>
<span data-ttu-id="d8e77-161">Criando um [ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/) objeto requer toospecify Olá repositório Data Lake conta hello e nome de provedor de token gerados na última etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="d8e77-161">Creating an [ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/) object requires you toospecify hello Data Lake Store account name and hello token provider you generated in hello last step.</span></span> <span data-ttu-id="d8e77-162">Observe que Olá conta do repositório Data Lake nome precisa toobe um nome de domínio totalmente qualificado.</span><span class="sxs-lookup"><span data-stu-id="d8e77-162">Note that hello Data Lake Store account name needs toobe a fully qualified domain name.</span></span> <span data-ttu-id="d8e77-163">Por exemplo, substitua **FILL-IN-HERE** por algo como **mydatalakestore.azuredatalakestore.net**.</span><span class="sxs-lookup"><span data-stu-id="d8e77-163">For example, replace **FILL-IN-HERE** with something like **mydatalakestore.azuredatalakestore.net**.</span></span>

    private static String accountFQDN = "FILL-IN-HERE";  // full account FQDN, not just hello account name
    ADLStoreClient client = ADLStoreClient.createClient(accountFQDN, provider);

### <a name="step-3-use-hello-adlstoreclient-tooperform-file-and-directory-operations"></a><span data-ttu-id="d8e77-164">Etapa 3: Usar operações de arquivo e diretório de tooperform de ADLStoreClient do hello</span><span class="sxs-lookup"><span data-stu-id="d8e77-164">Step 3: Use hello ADLStoreClient tooperform file and directory operations</span></span>
<span data-ttu-id="d8e77-165">código de saudação abaixo contém os trechos de código de exemplo de algumas operações comuns.</span><span class="sxs-lookup"><span data-stu-id="d8e77-165">hello code below contains example snippets of some common operations.</span></span> <span data-ttu-id="d8e77-166">Você pode examinar Olá completo [documentos de API do SDK do Data Lake repositório Java](https://azure.github.io/azure-data-lake-store-java/javadoc/) de saudação **ADLStoreClient** objeto toosee outras operações.</span><span class="sxs-lookup"><span data-stu-id="d8e77-166">You can look at hello full [Data Lake Store Java SDK API docs](https://azure.github.io/azure-data-lake-store-java/javadoc/) of hello **ADLStoreClient** object toosee other operations.</span></span>

<span data-ttu-id="d8e77-167">Observe que os arquivos são lidos e gravados usando fluxos Java padrão.</span><span class="sxs-lookup"><span data-stu-id="d8e77-167">Note that files are read from and written into using standard Java streams.</span></span> <span data-ttu-id="d8e77-168">Isso significa que você pode definir qualquer um dos fluxos de Java Olá sobre Olá que toobenefit da funcionalidade de Java padrão (por exemplo, Print fluxos de saída formatada, ou qualquer um dos fluxos de compactação ou criptografia Olá para obter funcionalidade adicional em fluxos de repositório Data Lake principal, etc.).</span><span class="sxs-lookup"><span data-stu-id="d8e77-168">This means that you can layer any of hello Java streams on top of hello Data Lake Store streams toobenefit from standard Java functionality (e.g., Print streams for formatted output, or any of hello compression or encryption streams for additional functionality on top, etc.).</span></span>

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

#### <a name="step-4-build-and-run-hello-application"></a><span data-ttu-id="d8e77-169">Etapa 4: Criar e executar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="d8e77-169">Step 4: Build and run hello application</span></span>
1. <span data-ttu-id="d8e77-170">toorun de dentro de um IDE, localize e pressione Olá **executar** botão.</span><span class="sxs-lookup"><span data-stu-id="d8e77-170">toorun from within an IDE, locate and press hello **Run** button.</span></span> <span data-ttu-id="d8e77-171">toorun do Maven, use [exec: exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html).</span><span class="sxs-lookup"><span data-stu-id="d8e77-171">toorun from Maven, use [exec:exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html).</span></span>
2. <span data-ttu-id="d8e77-172">tooproduce um jar autônomo que você pode executar de compilação de linha de comando Olá jar com todas as dependências incluídas, usando Olá [plug-in do Maven assembly](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html).</span><span class="sxs-lookup"><span data-stu-id="d8e77-172">tooproduce a standalone jar that you can run from command-line build hello jar with all dependencies included, using hello [Maven assembly plugin](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html).</span></span> <span data-ttu-id="d8e77-173">Olá pom.xml em Olá [exemplo de código de origem no github](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml) tem um exemplo de como toodo isso.</span><span class="sxs-lookup"><span data-stu-id="d8e77-173">hello pom.xml in hello [example source code on github](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml) has an example of how toodo this.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8e77-174">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d8e77-174">Next steps</span></span>
* [<span data-ttu-id="d8e77-175">Explore JavaDoc para Olá SDK de Java</span><span class="sxs-lookup"><span data-stu-id="d8e77-175">Explore JavaDoc for hello Java SDK</span></span>](https://azure.github.io/azure-data-lake-store-java/javadoc/)
* [<span data-ttu-id="d8e77-176">Proteger dados no Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="d8e77-176">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="d8e77-177">Usar a Análise Data Lake do Azure com o Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="d8e77-177">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="d8e77-178">Usar o Azure HDInsight com o Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="d8e77-178">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

