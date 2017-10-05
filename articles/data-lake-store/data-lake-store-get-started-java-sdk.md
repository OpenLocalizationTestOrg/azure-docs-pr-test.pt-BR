---
title: Use o SDK do Java para desenvolver aplicativos no Azure Data Lake Store | Microsoft Docs
description: "Use o SDK do Java do Azure Data Lake Store para criar uma conta do Data Lake Store e execute operações básicas no Data Lake Store"
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
ms.openlocfilehash: 91128b53a2f1cd3ddcbee5b07da0d67668944fb4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-java"></a><span data-ttu-id="86d31-103">Introdução ao Repositório Azure Data Lake usando o Java</span><span class="sxs-lookup"><span data-stu-id="86d31-103">Get started with Azure Data Lake Store using Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="86d31-104">Portal</span><span class="sxs-lookup"><span data-stu-id="86d31-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="86d31-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="86d31-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="86d31-106">SDK .NET</span><span class="sxs-lookup"><span data-stu-id="86d31-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="86d31-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="86d31-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="86d31-108">API REST</span><span class="sxs-lookup"><span data-stu-id="86d31-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="86d31-109">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="86d31-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="86d31-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="86d31-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="86d31-111">Python</span><span class="sxs-lookup"><span data-stu-id="86d31-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

<span data-ttu-id="86d31-112">Saiba como usar o SDK Java para o Azure Data Lake Store a fim de executar operações básicas, como criar pastas, carregar e baixar arquivos de dados etc. Para obter mais informações sobre o Data Lake, veja [Azure Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="86d31-112">Learn how to use the Azure Data Lake Store Java SDK to perform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

<span data-ttu-id="86d31-113">Você pode acessar os documentos de API do Java SDK do Azure Data Lake Store em [Documentos de API Java do Azure Data Lake Store](https://azure.github.io/azure-data-lake-store-java/javadoc/).</span><span class="sxs-lookup"><span data-stu-id="86d31-113">You can access the Java SDK API docs for Azure Data Lake Store at [Azure Data Lake Store Java API docs](https://azure.github.io/azure-data-lake-store-java/javadoc/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86d31-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="86d31-114">Prerequisites</span></span>
* <span data-ttu-id="86d31-115">Java Development Kit (JDK 7 ou superior, usando Java versão 1.7 ou superior)</span><span class="sxs-lookup"><span data-stu-id="86d31-115">Java Development Kit (JDK 7 or higher, using Java version 1.7 or higher)</span></span>
* <span data-ttu-id="86d31-116">Conta do Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="86d31-116">Azure Data Lake Store account.</span></span> <span data-ttu-id="86d31-117">Siga as instruções em [Introdução ao Repositório Azure Data Lake usando o Portal do Azure](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="86d31-117">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](data-lake-store-get-started-portal.md).</span></span>
* <span data-ttu-id="86d31-118">[Maven](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="86d31-118">[Maven](https://maven.apache.org/install.html).</span></span> <span data-ttu-id="86d31-119">Este tutorial usa o Maven para compilação e dependências de projeto.</span><span class="sxs-lookup"><span data-stu-id="86d31-119">This tutorial uses Maven for build and project dependencies.</span></span> <span data-ttu-id="86d31-120">Embora seja possível compilar sem usar um sistema de compilação como Maven ou Gradle, com esses sistemas é muito mais fácil gerenciar dependências.</span><span class="sxs-lookup"><span data-stu-id="86d31-120">Although it is possible to build without using a build system like Maven or Gradle, these systems make is much easier to manage dependencies.</span></span>
* <span data-ttu-id="86d31-121">(Opcional) E IDE como [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) ou [Eclipse](https://www.eclipse.org/downloads/) ou semelhante.</span><span class="sxs-lookup"><span data-stu-id="86d31-121">(Optional) And IDE like [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) or [Eclipse](https://www.eclipse.org/downloads/) or similar.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="86d31-122">Como faço para me autenticar usando o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="86d31-122">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="86d31-123">Neste tutorial, usamos um segredo do cliente de aplicativo do Azure AD para recuperar um token do Azure Active Directory (autenticação de serviço a serviço).</span><span class="sxs-lookup"><span data-stu-id="86d31-123">In this tutorial we use a Azure AD application client secret to retrieve an Azure Active Directory token (service-to-service authentication).</span></span> <span data-ttu-id="86d31-124">Podemos usar esse token para criar um objeto de cliente do Data Lake Store para executar operações de arquivo e operações de diretório.</span><span class="sxs-lookup"><span data-stu-id="86d31-124">We use this token to create an Data Lake Store client object to perform operations file and directory operations.</span></span> <span data-ttu-id="86d31-125">Para obter instruções sobre como autenticar com o Azure Data Lake Store usando o segredo do cliente, podemos executar as seguintes etapas de alto nível:</span><span class="sxs-lookup"><span data-stu-id="86d31-125">For instructions on how to authenticate with Azure Data Lake Store using the client secret, we perform the following high-level steps:</span></span>

1. <span data-ttu-id="86d31-126">Criar um aplicativo Web do Azure AD</span><span class="sxs-lookup"><span data-stu-id="86d31-126">Create an Azure AD web application</span></span>
2. <span data-ttu-id="86d31-127">Recupere a ID do cliente, o segredo do cliente e o ponto de extremidade de token para o aplicativo Web do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="86d31-127">Retrieve the client ID, client secret, and token endpoint for the Azure AD web application.</span></span>
3. <span data-ttu-id="86d31-128">Configure o acesso ao aplicativo Web do Azure AD no arquivo/pasta do Data Lake Store que você deseja acessar por meio do aplicativo Java que está criando.</span><span class="sxs-lookup"><span data-stu-id="86d31-128">Configure access for the Azure AD web application on the Data Lake Store file/folder that you want to access from the Java application you are creating.</span></span>

<span data-ttu-id="86d31-129">Para obter instruções sobre como executar essas etapas, confira [Criar um aplicativo do Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="86d31-129">For instructions on how to perform these steps, see [Create an Active Directory application](data-lake-store-authenticate-using-active-directory.md).</span></span>

<span data-ttu-id="86d31-130">O Azure Active Directory fornece outras opções, bem como a recuperação de um token.</span><span class="sxs-lookup"><span data-stu-id="86d31-130">Azure Active Directory provides other options as well to retrieve a token.</span></span> <span data-ttu-id="86d31-131">Você pode escolher vários mecanismos de autenticação diferentes de acordo com seu cenário; por exemplo, um aplicativo em execução em um navegador, um aplicativo distribuído como um aplicativo da área de trabalho ou um aplicativo de servidor em execução no local ou em uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="86d31-131">You can pick from a number of different authentication mechanisms to suit your scenario, for example, an application running in a browser, an application distributed as a desktop application, or a server application running on-premises or in an Azure virtual machine.</span></span> <span data-ttu-id="86d31-132">Você também pode escolher diferentes tipos de credenciais, como senhas, certificados, autenticação de dois fatores etc. Além disso, o Azure Active Directory permite sincronizar os usuários do Active Directory locais com a nuvem.</span><span class="sxs-lookup"><span data-stu-id="86d31-132">You can also pick from different types of credentials like passwords, certificates, 2-factor authentication, etc. In addition, Azure Active Directory allows you to synchronize your on-premises Active Directory users with the cloud.</span></span> <span data-ttu-id="86d31-133">Para obter detalhes, confira [Cenários de autenticação do Azure Active Directory](../active-directory/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="86d31-133">For details, see [Authentication Scenarios for Azure Active Directory](../active-directory/active-directory-authentication-scenarios.md).</span></span> 

## <a name="create-a-java-application"></a><span data-ttu-id="86d31-134">Criar um aplicativo Java</span><span class="sxs-lookup"><span data-stu-id="86d31-134">Create a Java application</span></span>
<span data-ttu-id="86d31-135">O exemplo de código disponível [no GitHub](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) explica o processo de criação de arquivos no armazenamento, concatenação de arquivos, download de um arquivo e exclusão de alguns arquivos no armazenamento.</span><span class="sxs-lookup"><span data-stu-id="86d31-135">The code sample available [on GitHub](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) walks you through the process of creating files in the store, concatenating files, downloading a file, and deleting some files in the store.</span></span> <span data-ttu-id="86d31-136">Esta seção do artigo explica as principais partes do código.</span><span class="sxs-lookup"><span data-stu-id="86d31-136">This section of the article walk you through the main parts of the code.</span></span>

1. <span data-ttu-id="86d31-137">Crie um projeto do Maven usando [mvn archetype](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) na linha de comando ou usando um IDE.</span><span class="sxs-lookup"><span data-stu-id="86d31-137">Create a Maven project using [mvn archetype](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) from the command-line or using an IDE.</span></span> <span data-ttu-id="86d31-138">Para obter instruções sobre como criar um projeto Java usando IntelliJ, veja [aqui](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html).</span><span class="sxs-lookup"><span data-stu-id="86d31-138">For instructions on how to create a Java project using IntelliJ, see [here](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html).</span></span> <span data-ttu-id="86d31-139">Para obter instruções sobre como criar um projeto usando o Eclipse, veja [aqui](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm).</span><span class="sxs-lookup"><span data-stu-id="86d31-139">For instructions on how to create a project using Eclipse, see [here](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm).</span></span> 
2. <span data-ttu-id="86d31-140">Adicione as dependências a seguir para o arquivo **pom.xml** do Maven.</span><span class="sxs-lookup"><span data-stu-id="86d31-140">Add the following dependencies to your Maven **pom.xml** file.</span></span> <span data-ttu-id="86d31-141">Adicione o seguinte trecho de texto entre a marca **\</version>** e a marca **\</project>**:</span><span class="sxs-lookup"><span data-stu-id="86d31-141">Add the following snippet of text between the **\</version>** tag and the **\</project>** tag:</span></span>
   
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
   
    <span data-ttu-id="86d31-142">A primeira dependência é usar o SDK do Data Lake Store (`azure-data-lake-store-sdk`) do repositório do maven.</span><span class="sxs-lookup"><span data-stu-id="86d31-142">The first dependency is to use the Data Lake Store SDK (`azure-data-lake-store-sdk`) from the maven repository.</span></span> <span data-ttu-id="86d31-143">A segunda dependência (`slf4j-nop`) é especificar qual estrutura de registros a ser usada para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="86d31-143">The second dependency (`slf4j-nop`) is to specify which logging framework to use for this application.</span></span> <span data-ttu-id="86d31-144">O SDK do Data Lake Store usa a fachada de registro em log [slf4j](http://www.slf4j.org/), que permite que você escolha entre uma série de estruturas de log populares, como log4j, registro em log Java, logback etc. ou nenhum log.</span><span class="sxs-lookup"><span data-stu-id="86d31-144">The Data Lake Store SDK uses [slf4j](http://www.slf4j.org/) logging façade, which lets you choose from a number of popular logging frameworks, like log4j, Java logging, logback, etc., or no logging.</span></span> <span data-ttu-id="86d31-145">Para este exemplo, desabilitaremos o registro em log, por isso, usaremos a associação **slf4j nop**.</span><span class="sxs-lookup"><span data-stu-id="86d31-145">For this example, we will disable logging, hence we use the **slf4j-nop** binding.</span></span> <span data-ttu-id="86d31-146">Para usar outras opções de log em seu aplicativo, veja [aqui](http://www.slf4j.org/manual.html#projectDep).</span><span class="sxs-lookup"><span data-stu-id="86d31-146">To use other logging options in your app, see [here](http://www.slf4j.org/manual.html#projectDep).</span></span>

### <a name="add-the-application-code"></a><span data-ttu-id="86d31-147">Adicionar o código do aplicativo</span><span class="sxs-lookup"><span data-stu-id="86d31-147">Add the application code</span></span>
<span data-ttu-id="86d31-148">Há três partes principais para o código.</span><span class="sxs-lookup"><span data-stu-id="86d31-148">There are three main parts to the code.</span></span>

1. <span data-ttu-id="86d31-149">Obter o token do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="86d31-149">Obtain the Azure Active Directory token</span></span>
2. <span data-ttu-id="86d31-150">Use o token para criar um cliente do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="86d31-150">Use the token to create a Data Lake Store client.</span></span>
3. <span data-ttu-id="86d31-151">Use o cliente do Data Lake Store para executar operações.</span><span class="sxs-lookup"><span data-stu-id="86d31-151">Use the Data Lake Store client to perform operations.</span></span>

#### <a name="step-1-obtain-an-azure-active-directory-token"></a><span data-ttu-id="86d31-152">Etapa 1: obter um token do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="86d31-152">Step 1: Obtain an Azure Active Directory token.</span></span>
<span data-ttu-id="86d31-153">O SDK do Data Lake Store fornece métodos convenientes que permitem gerenciar os tokens de segurança necessários para se comunicar com a conta do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="86d31-153">The Data Lake Store SDK provides convenient methods that let you manage the security tokens needed to talk to the Data Lake Store account.</span></span> <span data-ttu-id="86d31-154">No entanto, o SDK não exige que apenas esses métodos sejam usados.</span><span class="sxs-lookup"><span data-stu-id="86d31-154">However, the SDK does not mandate that only these methods be used.</span></span> <span data-ttu-id="86d31-155">Você pode usar qualquer outro meio de obter o token, como usar o [SDK do Azure Active Directory](https://github.com/AzureAD/azure-activedirectory-library-for-java) ou seu próprio código personalizado.</span><span class="sxs-lookup"><span data-stu-id="86d31-155">You can use any other means of obtaining token as well, like using the [Azure Active Directory SDK](https://github.com/AzureAD/azure-activedirectory-library-for-java), or your own custom code.</span></span>

<span data-ttu-id="86d31-156">Para usar o SDK do Data Lake Store para obter o token para o aplicativo Web do Active Directory que você criou anteriormente, use uma das subclasses de `AccessTokenProvider` (o exemplo abaixo usa `ClientCredsTokenProvider`).</span><span class="sxs-lookup"><span data-stu-id="86d31-156">To use the Data Lake Store SDK to obtain token for the Active Directory Web application you created earlier, use one of the subclasses of `AccessTokenProvider` (the example below uses `ClientCredsTokenProvider`).</span></span> <span data-ttu-id="86d31-157">O provedor de token armazena em cache as credenciais usadas para obter o token na memória e renova automaticamente o token se ele está prestes a expirar.</span><span class="sxs-lookup"><span data-stu-id="86d31-157">The token provider caches the creds used to obtain the token in memory, and automatically renews the token if it is about to expire.</span></span> <span data-ttu-id="86d31-158">É possível criar suas próprias subclasses de `AccessTokenProvider`. Assim, os tokens são obtidos por seu código de cliente, mas agora vamos simplesmente usar aquele fornecido no SDK.</span><span class="sxs-lookup"><span data-stu-id="86d31-158">It is possible to create your own subclasses of `AccessTokenProvider` so tokens are obtained by your customer code, but for now let's just use the one provided in the SDK.</span></span>

<span data-ttu-id="86d31-159">Substitua **FILL-IN-HERE** pelos valores reais para o aplicativo Web do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="86d31-159">Replace **FILL-IN-HERE** with the actual values for the Azure Active Directory Web application.</span></span>

    private static String clientId = "FILL-IN-HERE";
    private static String authTokenEndpoint = "FILL-IN-HERE";
    private static String clientKey = "FILL-IN-HERE";

    AccessTokenProvider provider = new ClientCredsTokenProvider(authTokenEndpoint, clientId, clientKey);

#### <a name="step-2-create-an-azure-data-lake-store-client-adlstoreclient-object"></a><span data-ttu-id="86d31-160">Etapa 2: criar um objeto de cliente (ADLStoreClient) do Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="86d31-160">Step 2: Create an Azure Data Lake Store client (ADLStoreClient) object</span></span>
<span data-ttu-id="86d31-161">Criar um objeto [ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/) requer que você especifique o nome da conta do Data Lake Store e o provedor de token gerado na última etapa.</span><span class="sxs-lookup"><span data-stu-id="86d31-161">Creating an [ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/) object requires you to specify the Data Lake Store account name and the token provider you generated in the last step.</span></span> <span data-ttu-id="86d31-162">Observe que o nome da conta do Data Lake Store deve ser um nome de domínio totalmente qualificado.</span><span class="sxs-lookup"><span data-stu-id="86d31-162">Note that the Data Lake Store account name needs to be a fully qualified domain name.</span></span> <span data-ttu-id="86d31-163">Por exemplo, substitua **FILL-IN-HERE** por algo como **mydatalakestore.azuredatalakestore.net**.</span><span class="sxs-lookup"><span data-stu-id="86d31-163">For example, replace **FILL-IN-HERE** with something like **mydatalakestore.azuredatalakestore.net**.</span></span>

    private static String accountFQDN = "FILL-IN-HERE";  // full account FQDN, not just the account name
    ADLStoreClient client = ADLStoreClient.createClient(accountFQDN, provider);

### <a name="step-3-use-the-adlstoreclient-to-perform-file-and-directory-operations"></a><span data-ttu-id="86d31-164">Etapa 3: usar o ADLStoreClient para executar operações de arquivo e diretório</span><span class="sxs-lookup"><span data-stu-id="86d31-164">Step 3: Use the ADLStoreClient to perform file and directory operations</span></span>
<span data-ttu-id="86d31-165">O código a seguir contém trechos de código de exemplo de algumas operações comuns.</span><span class="sxs-lookup"><span data-stu-id="86d31-165">The code below contains example snippets of some common operations.</span></span> <span data-ttu-id="86d31-166">Você pode examinar os [documentos de API do SDK Javado Data Lake Store](https://azure.github.io/azure-data-lake-store-java/javadoc/) completos do objeto **ADLStoreClient** para ver outras operações.</span><span class="sxs-lookup"><span data-stu-id="86d31-166">You can look at the full [Data Lake Store Java SDK API docs](https://azure.github.io/azure-data-lake-store-java/javadoc/) of the **ADLStoreClient** object to see other operations.</span></span>

<span data-ttu-id="86d31-167">Observe que os arquivos são lidos e gravados usando fluxos Java padrão.</span><span class="sxs-lookup"><span data-stu-id="86d31-167">Note that files are read from and written into using standard Java streams.</span></span> <span data-ttu-id="86d31-168">Isso significa que você pode definir qualquer um dos fluxos Java sobre os fluxos do Data Lake Store para tirar proveito da funcionalidade padrão do Java (por exemplo, impressão de fluxos de saída formatada ou qualquer um dos fluxos de compactação ou criptografia para funcionalidade adicional etc.).</span><span class="sxs-lookup"><span data-stu-id="86d31-168">This means that you can layer any of the Java streams on top of the Data Lake Store streams to benefit from standard Java functionality (e.g., Print streams for formatted output, or any of the compression or encryption streams for additional functionality on top, etc.).</span></span>

     // create file and write some content
     String filename = "/a/b/c.txt";
     OutputStream stream = client.createFile(filename, IfExists.OVERWRITE  );
     PrintStream out = new PrintStream(stream);
     for (int i = 1; i <= 10; i++) {
         out.println("This is line #" + i);
         out.format("This is the same line (%d), but using formatted output. %n", i);
     }
     out.close();
    
    // set file permission
    client.setPermission(filename, "744");

    // append to file
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

    // concatenate the two files into one
    List<String> fileList = Arrays.asList("/a/b/c.txt", "/a/b/d.txt");
    client.concatenateFiles("/a/b/f.txt", fileList);

    //rename the file
    client.rename("/a/b/f.txt", "/a/b/g.txt");

    // list directory contents
    List<DirectoryEntry> list = client.enumerateDirectory("/a/b", 2000);
    System.out.println("Directory listing for directory /a/b:");
    for (DirectoryEntry entry : list) {
        printDirectoryInfo(entry);
    }

    // delete directory along with all the subdirectories and files in it
    client.deleteRecursive("/a");

#### <a name="step-4-build-and-run-the-application"></a><span data-ttu-id="86d31-169">Etapa 4: compile e execute o aplicativo</span><span class="sxs-lookup"><span data-stu-id="86d31-169">Step 4: Build and run the application</span></span>
1. <span data-ttu-id="86d31-170">Para executar por meio de um IDE, localize e pressione o botão **Executar**.</span><span class="sxs-lookup"><span data-stu-id="86d31-170">To run from within an IDE, locate and press the **Run** button.</span></span> <span data-ttu-id="86d31-171">Para executar por meio do Maven, use [exec:exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html).</span><span class="sxs-lookup"><span data-stu-id="86d31-171">To run from Maven, use [exec:exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html).</span></span>
2. <span data-ttu-id="86d31-172">Para produzir um jar autônomo que você pode executar na linha de comando, compile o jar com todas as dependências incluídas, usando o [plug-in de assembly do Maven](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html).</span><span class="sxs-lookup"><span data-stu-id="86d31-172">To produce a standalone jar that you can run from command-line build the jar with all dependencies included, using the [Maven assembly plugin](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html).</span></span> <span data-ttu-id="86d31-173">O pom.xml no [código de exemplo no github](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml) tem um exemplo de como fazer isso.</span><span class="sxs-lookup"><span data-stu-id="86d31-173">The pom.xml in the [example source code on github](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml) has an example of how to do this.</span></span>

## <a name="next-steps"></a><span data-ttu-id="86d31-174">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="86d31-174">Next steps</span></span>
* [<span data-ttu-id="86d31-175">Explorar o JavaDoc para o Java SDK</span><span class="sxs-lookup"><span data-stu-id="86d31-175">Explore JavaDoc for the Java SDK</span></span>](https://azure.github.io/azure-data-lake-store-java/javadoc/)
* [<span data-ttu-id="86d31-176">Proteger dados no Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="86d31-176">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="86d31-177">Usar a Análise Data Lake do Azure com o Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="86d31-177">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="86d31-178">Usar o Azure HDInsight com o Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="86d31-178">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

