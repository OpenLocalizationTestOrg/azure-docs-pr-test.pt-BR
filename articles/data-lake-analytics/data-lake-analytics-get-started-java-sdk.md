---
title: "aplicativos de toodevelop do SDK de Java em análise Data Lake aaaUse | Microsoft Docs"
description: "Usar aplicativos do Azure Data Lake análise Java SDK toodevelop"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 07830b36-2fe3-4809-a846-129cf67b6a9e
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 0d975812fe659ed34ee9befd37ee7c0bf50d3414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-java-sdk"></a><span data-ttu-id="2fd84-103">Introdução ao Azure Data Lake Analytics usando o SDK do Java</span><span class="sxs-lookup"><span data-stu-id="2fd84-103">Get started with Azure Data Lake Analytics using Java SDK</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="2fd84-104">Saiba como toouse hello Azure Data Lake análise Java SDK toocreate uma conta do Azure Data Lake e executar operações básicas, como criar pastas, carregar e baixar arquivos de dados, excluir sua conta e trabalhar com trabalhos.</span><span class="sxs-lookup"><span data-stu-id="2fd84-104">Learn how toouse hello Azure Data Lake Analytics Java SDK toocreate an Azure Data Lake account and perform basic operations such as create folders, upload and download data files, delete your account, and work with jobs.</span></span> <span data-ttu-id="2fd84-105">Para saber mais sobre o Data Lake, confira [Análise Azure Data Lake](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2fd84-105">For more information about Data Lake, see [Azure Data Lake Analytics](data-lake-analytics-overview.md).</span></span>

<span data-ttu-id="2fd84-106">Neste tutorial, você desenvolverá um aplicativo de console Java que contém exemplos de tarefas administrativas comuns, além de criar dados de teste e enviar um trabalho.</span><span class="sxs-lookup"><span data-stu-id="2fd84-106">In this tutorial, you will develop a Java console application which contains samples of common administrative tasks as well as creating test data and submitting a job.</span></span>  <span data-ttu-id="2fd84-107">toogo por meio de Olá mesmo tutorial usando outros suporte para ferramentas, clique nas guias de saudação na parte superior da saudação desta seção.</span><span class="sxs-lookup"><span data-stu-id="2fd84-107">toogo through hello same tutorial using other supported tools, click hello tabs on hello top of this section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2fd84-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2fd84-108">Prerequisites</span></span>
* <span data-ttu-id="2fd84-109">Java Development Kit (JDK) 8 (usando o Java versão 1.8).</span><span class="sxs-lookup"><span data-stu-id="2fd84-109">Java Development Kit (JDK) 8 (using Java version 1.8).</span></span>
* <span data-ttu-id="2fd84-110">IntelliJ ou outro ambiente de desenvolvimento Java adequado.</span><span class="sxs-lookup"><span data-stu-id="2fd84-110">IntelliJ or another suitable Java development environment.</span></span> <span data-ttu-id="2fd84-111">Isto é opcional, mas recomendado.</span><span class="sxs-lookup"><span data-stu-id="2fd84-111">This is optional but recommended.</span></span> <span data-ttu-id="2fd84-112">instruções de saudação abaixo usam IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="2fd84-112">hello instructions below use IntelliJ.</span></span>
* <span data-ttu-id="2fd84-113">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="2fd84-113">**An Azure subscription**.</span></span> <span data-ttu-id="2fd84-114">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2fd84-114">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="2fd84-115">Crie um aplicativo do AAD (Azure Active Directory) e recupere a **ID do Cliente**, a **ID de Locatário** e a **Chave**.</span><span class="sxs-lookup"><span data-stu-id="2fd84-115">Create an Azure Active Directory (AAD) application and retrieve its **Client ID**, **Tenant ID**, and **Key**.</span></span> <span data-ttu-id="2fd84-116">Para obter mais informações sobre aplicativos AAD e instruções sobre como tooget uma ID de cliente, consulte [entidade de serviço usando o portal e de aplicativo do Active Directory criar](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2fd84-116">For more information about AAD applications and instructions on how tooget a client ID, see [Create Active Directory application and service principal using portal](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="2fd84-117">Olá URI de resposta e a chave também está disponível no portal de saudação de uma vez que o aplicativo hello criado e a chave gerada.</span><span class="sxs-lookup"><span data-stu-id="2fd84-117">hello Reply URI and Key will also be available from hello portal once you have hello application created and key generated.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="2fd84-118">Como faço para me autenticar usando o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2fd84-118">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="2fd84-119">trecho de código Olá abaixo fornece código para **não interativo** autenticação, onde o aplicativo hello fornece suas próprias credenciais.</span><span class="sxs-lookup"><span data-stu-id="2fd84-119">hello code snippet below provides code for **non-interactive** authentication, where hello application provides its own credentials.</span></span>

<span data-ttu-id="2fd84-120">Você precisará toogive os recursos de toocreate de permissão do aplicativo no Azure para este tutorial toowork.</span><span class="sxs-lookup"><span data-stu-id="2fd84-120">You will need toogive your application permission toocreate resources in Azure for this tutorial toowork.</span></span> <span data-ttu-id="2fd84-121">É **altamente recomendável** conceda somente esse grupo de recursos novos, não utilizados e vazio do aplicativo Colaborador permissões tooa na sua assinatura do Azure para fins de saudação deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="2fd84-121">It is **highly recommended** that you only give this application Contributor permissions tooa new, unused, and empty resource group in your Azure subscription for hello purposes of this tutorial.</span></span>

## <a name="create-a-java-application"></a><span data-ttu-id="2fd84-122">Criar um aplicativo Java</span><span class="sxs-lookup"><span data-stu-id="2fd84-122">Create a Java application</span></span>
1. <span data-ttu-id="2fd84-123">Abra IntelliJ e crie um novo projeto de Java usando Olá **aplicativo de linha de comando** modelo.</span><span class="sxs-lookup"><span data-stu-id="2fd84-123">Open IntelliJ and create a new Java project using hello **Command Line App** template.</span></span>
2. <span data-ttu-id="2fd84-124">Clique com botão direito no projeto Olá no lado esquerdo de saudação da tela e clique em **adicionar suporte de Framework**.</span><span class="sxs-lookup"><span data-stu-id="2fd84-124">Right-click on hello project on hello left-hand side of your screen and click **Add Framework Support**.</span></span> <span data-ttu-id="2fd84-125">Escolha **Maven** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="2fd84-125">Choose **Maven** and click **OK**.</span></span>
3. <span data-ttu-id="2fd84-126">Abra Olá recém-criado **"pom.xml"** de arquivos e adicionar Olá seguindo o trecho de texto entre hello  **\</version >** marca e hello  **\< /projeto >** marca:</span><span class="sxs-lookup"><span data-stu-id="2fd84-126">Open hello newly created **"pom.xml"** file and add hello following snippet of text between hello **\</version>** tag and hello **\</project>** tag:</span></span>

    >[!NOTE]
    ><span data-ttu-id="2fd84-127">Esta etapa é temporária até hello Azure Data Lake análise SDK está disponível no Maven.</span><span class="sxs-lookup"><span data-stu-id="2fd84-127">This step is temporary until hello Azure Data Lake Analytics SDK is available in Maven.</span></span> <span data-ttu-id="2fd84-128">Este artigo será atualizado após Olá SDK está disponível no Maven.</span><span class="sxs-lookup"><span data-stu-id="2fd84-128">This article will be updated once hello SDK is available in Maven.</span></span> <span data-ttu-id="2fd84-129">Todas as atualizações futuras toothis SDK estará disponível por meio de Maven.</span><span class="sxs-lookup"><span data-stu-id="2fd84-129">All future updates toothis SDK will be availble through Maven.</span></span>
    >

        <repositories>
            <repository>
                <id>adx-snapshots</id>
                <name>Azure ADX Snapshots</name>
                <url>http://adxsnapshots.azurewebsites.net/</url>
                <layout>default</layout>
                <snapshots>
                    <enabled>true</enabled>
                </snapshots>
            </repository>
            <repository>
                <id>oss-snapshots</id>
                <name>Open Source Snapshots</name>
                <url>https://oss.sonatype.org/content/repositories/snapshots/</url>
                <layout>default</layout>
                <snapshots>
                    <enabled>true</enabled>
                    <updatePolicy>always</updatePolicy>
                </snapshots>
            </repository>
        </repositories>
        <dependencies>
            <dependency>
                <groupId>com.microsoft.azure</groupId>
                <artifactId>azure-client-authentication</artifactId>
                <version>1.0.0-20160513.000802-24</version>
            </dependency>
            <dependency>
                <groupId>com.microsoft.azure</groupId>
                <artifactId>azure-client-runtime</artifactId>
                <version>1.0.0-20160513.000812-28</version>
            </dependency>
            <dependency>
                <groupId>com.microsoft.rest</groupId>
                <artifactId>client-runtime</artifactId>
                <version>1.0.0-20160513.000825-29</version>
            </dependency>
            <dependency>
                <groupId>com.microsoft.azure</groupId>
                <artifactId>azure-mgmt-datalake-store</artifactId>
                <version>1.0.0-SNAPSHOT</version>
            </dependency>
            <dependency>
                <groupId>com.microsoft.azure</groupId>
                <artifactId>azure-mgmt-datalake-analytics</artifactId>
                <version>1.0.0-SNAPSHOT</version>
            </dependency>
        </dependencies>
4. <span data-ttu-id="2fd84-130">Vá muito**arquivo**, em seguida, **configurações**, em seguida, **criar**, **execução**, **implantação**.</span><span class="sxs-lookup"><span data-stu-id="2fd84-130">Go too**File**, then **Settings**, then **Build**, **Execution**, **Deployment**.</span></span> <span data-ttu-id="2fd84-131">Selecione **Ferramentas de Compilação**, **Maven**, **Importando**.</span><span class="sxs-lookup"><span data-stu-id="2fd84-131">Select **Build Tools**, **Maven**, **Importing**.</span></span> <span data-ttu-id="2fd84-132">Depois, marque **Importar projetos Maven automaticamente**.</span><span class="sxs-lookup"><span data-stu-id="2fd84-132">Then check **Import Maven projects automatically**.</span></span>
5. <span data-ttu-id="2fd84-133">Abra **Main.java** e substituir Olá bloco de código existente com hello código a seguir.</span><span class="sxs-lookup"><span data-stu-id="2fd84-133">Open **Main.java** and replace hello existing code block with hello following code.</span></span> <span data-ttu-id="2fd84-134">Além disso, forneça valores de saudação para parâmetros chamados no trecho de código hello, tais como **localFolderPath**, **_adlaAccountName**, **_adlsAccountName**, **_ resourceGroupName** e substitua os espaços reservados para **ID do cliente**, **segredo do cliente**, **ID de LOCATÁRIO**, e  **ID da assinatura**.</span><span class="sxs-lookup"><span data-stu-id="2fd84-134">Also, provide hello values for parameters called out in hello code snippet, such as **localFolderPath**, **_adlaAccountName**, **_adlsAccountName**, **_resourceGroupName** and replace placeholders for **CLIENT-ID**, **CLIENT-SECRET**, **TENANT-ID**, and **SUBSCRIPTION-ID**.</span></span>

    <span data-ttu-id="2fd84-135">Esse código vai pelo processo de saudação de criação de contas do repositório Data Lake e análise Data Lake, criação de arquivos no repositório de hello, executando um trabalho, obtendo o status do trabalho, baixando a saída de trabalho e finalmente excluindo conta hello.</span><span class="sxs-lookup"><span data-stu-id="2fd84-135">This code goes through hello process of creating Data Lake Store and Data Lake Analytics accounts, creating files in hello store, running a job, getting job status, downloading job output, and finally deleting hello account.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2fd84-136">Atualmente, há um problema conhecido com hello serviço do Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="2fd84-136">There is currently a known issue with hello Azure Data Lake Service.</span></span>  <span data-ttu-id="2fd84-137">Se o aplicativo de exemplo hello for interrompido ou encontra um erro, talvez seja necessário toomanually delete Olá repositório Data Lake & análise Data Lake contas que o script hello cria.</span><span class="sxs-lookup"><span data-stu-id="2fd84-137">If hello sample app is interrupted or encounters an error, you may need toomanually delete hello Data Lake Store & Data Lake Analytics accounts that hello script creates.</span></span>  <span data-ttu-id="2fd84-138">Se você não estiver familiarizado com hello Portal, Olá [Gerenciar análise Azure Data Lake usando o Portal do Azure](data-lake-analytics-manage-use-portal.md) guia obterá começar.</span><span class="sxs-lookup"><span data-stu-id="2fd84-138">If you're not familiar with hello Portal, hello [Manage Azure Data Lake Analytics using Azure Portal](data-lake-analytics-manage-use-portal.md) guide will get you started.</span></span>
   >
   >

        package com.company;

        import com.microsoft.azure.CloudException;
        import com.microsoft.azure.credentials.ApplicationTokenCredentials;
        import com.microsoft.azure.management.datalake.store.*;
        import com.microsoft.azure.management.datalake.store.models.*;
        import com.microsoft.azure.management.datalake.analytics.*;
        import com.microsoft.azure.management.datalake.analytics.models.*;
        import com.microsoft.rest.credentials.ServiceClientCredentials;
        import java.io.*;
        import java.nio.charset.Charset;
        import java.nio.file.Files;
        import java.nio.file.Paths;
        import java.util.ArrayList;
        import java.util.UUID;
        import java.util.List;

        public class Main {
            private static String _adlsAccountName;
            private static String _adlaAccountName;
            private static String _resourceGroupName;
            private static String _location;

            private static String _tenantId;
            private static String _subId;
            private static String _clientId;
            private static String _clientSecret;

            private static DataLakeStoreAccountManagementClient _adlsClient;
            private static DataLakeStoreFileSystemManagementClient _adlsFileSystemClient;
            private static DataLakeAnalyticsAccountManagementClient _adlaClient;
            private static DataLakeAnalyticsJobManagementClient _adlaJobClient;
            private static DataLakeAnalyticsCatalogManagementClient _adlaCatalogClient;

            public static void main(String[] args) throws Exception {
                _adlsAccountName = "<DATA-LAKE-STORE-NAME>";
                _adlaAccountName = "<DATA-LAKE-ANALYTICS-NAME>";
                _resourceGroupName = "<RESOURCE-GROUP-NAME>";
                _location = "East US 2";

                _tenantId = "<TENANT-ID>";
                _subId =  "<SUBSCRIPTION-ID>";
                _clientId = "<CLIENT-ID>";

                _clientSecret = "<CLIENT-SECRET>"; // TODO: For production scenarios, we recommend that you replace this line with a more secure way of acquiring hello application client secret, rather than hard-coding it in hello source code.

                String localFolderPath = "C:\\local_path\\"; // TODO: Change this tooany unused, new, empty folder on your local machine.

                // Authenticate
                ApplicationTokenCredentials creds = new ApplicationTokenCredentials(_clientId, _tenantId, _clientSecret, null);
                SetupClients(creds);

                // Create Data Lake Store and Analytics accounts
                WaitForNewline("Authenticated.", "Creating NEW accounts.");
                CreateAccounts();
                WaitForNewline("Accounts created.", "Displaying accounts.");

                // List Data Lake Store and Analytics accounts that this app can access
                System.out.println(String.format("All ADL Store accounts that this app can access in subscription %s:", _subId));
                List<DataLakeStoreAccount> adlsListResult = _adlsClient.getAccountOperations().list().getBody();
                for (DataLakeStoreAccount acct : adlsListResult) {
                    System.out.println(acct.getName());
                }
                System.out.println(String.format("All ADL Analytics accounts that this app can access in subscription %s:", _subId));
                List<DataLakeAnalyticsAccount> adlaListResult = _adlaClient.getAccountOperations().list().getBody();
                for (DataLakeAnalyticsAccount acct : adlaListResult) {
                    System.out.println(acct.getName());
                }
                WaitForNewline("Accounts displayed.", "Creating files.");

                // Create a file in Data Lake Store: input1.csv
                // TODO: these change order in hello next patch
                byte[] bytesContents = "123,abc".getBytes();
                _adlsFileSystemClient.getFileSystemOperations().create(_adlsAccountName, "/input1.csv", bytesContents, true);

                WaitForNewline("File created.", "Submitting a job.");

                // Submit a job tooData Lake Analytics
                UUID jobId = SubmitJobByScript("@input =  EXTRACT Data string FROM \"/input1.csv\" USING Extractors.Csv(); OUTPUT @input too@\"/output1.csv\" USING Outputters.Csv();", "testJob");
                WaitForNewline("Job submitted.", "Getting job status.");

                // Wait for job completion and output job status
                System.out.println(String.format("Job status: %s", GetJobStatus(jobId)));
                System.out.println("Waiting for job completion.");
                WaitForJob(jobId);
                System.out.println(String.format("Job status: %s", GetJobStatus(jobId)));
                WaitForNewline("Job completed.", "Downloading job output.");

                // Download job output from Data Lake Store
                DownloadFile("/output1.csv", localFolderPath + "output1.csv");
                WaitForNewline("Job output downloaded.", "Deleting file.");

                // Delete file from Data Lake Store
                DeleteFile("/output1.csv");
                WaitForNewline("File deleted.", "Deleting account.");

                // Delete account
                _adlsClient.getAccountOperations().delete(_resourceGroupName, _adlsAccountName);
                _adlaClient.getAccountOperations().delete(_resourceGroupName, _adlaAccountName);
                WaitForNewline("Account deleted.", "DONE.");
            }

            //Set up clients
            public static void SetupClients(ServiceClientCredentials creds)
            {
                _adlsClient = new DataLakeStoreAccountManagementClientImpl(creds);
                _adlsFileSystemClient = new DataLakeStoreFileSystemManagementClientImpl(creds);
                _adlaClient = new DataLakeAnalyticsAccountManagementClientImpl(creds);
                _adlaJobClient = new DataLakeAnalyticsJobManagementClientImpl(creds);
                _adlaCatalogClient = new DataLakeAnalyticsCatalogManagementClientImpl(creds);
                _adlsClient.setSubscriptionId(_subId);
                _adlaClient.setSubscriptionId(_subId);
            }

            // Helper function tooshow status and wait for user input
            public static void WaitForNewline(String reason, String nextAction)
            {
                if (nextAction == null)
                    nextAction = "";

                System.out.println(reason + "\r\nPress ENTER toocontinue...");
                try{System.in.read();}
                catch(Exception e){}

                if (!nextAction.isEmpty())
                {
                    System.out.println(nextAction);
                }
            }

            // Create Data Lake Store and Analytics accounts
            public static void CreateAccounts() throws InterruptedException, CloudException, IOException {
                // Create ADLS account
                DataLakeStoreAccount adlsParameters = new DataLakeStoreAccount();
                adlsParameters.setLocation(_location);

                _adlsClient.getAccountOperations().create(_resourceGroupName, _adlsAccountName, adlsParameters);

                // Create ADLA account
                DataLakeStoreAccountInfo adlsInfo = new DataLakeStoreAccountInfo();
                adlsInfo.setName(_adlsAccountName);

                DataLakeStoreAccountInfoProperties adlsInfoProperties = new DataLakeStoreAccountInfoProperties();
                adlsInfo.setProperties(adlsInfoProperties);

                List<DataLakeStoreAccountInfo> adlsInfoList = new ArrayList<DataLakeStoreAccountInfo>();
                adlsInfoList.add(adlsInfo);

                DataLakeAnalyticsAccountProperties adlaProperties = new DataLakeAnalyticsAccountProperties();
                adlaProperties.setDataLakeStoreAccounts(adlsInfoList);
                adlaProperties.setDefaultDataLakeStoreAccount(_adlsAccountName);

                DataLakeAnalyticsAccount adlaParameters = new DataLakeAnalyticsAccount();
                adlaParameters.setLocation(_location);
                adlaParameters.setName(_adlaAccountName);
                adlaParameters.setProperties(adlaProperties);

                    /* If this line generates an error message like "hello deep update for property 'DataLakeStoreAccounts' is not supported", please delete hello ADLS and ADLA accounts via hello portal and re-run your script. */

                _adlaClient.getAccountOperations().create(_resourceGroupName, _adlaAccountName, adlaParameters);
            }

            //todo: this changes in hello next version of hello API
            public static void CreateFile(String path, String contents, boolean force) throws IOException, CloudException {
                byte[] bytesContents = contents.getBytes();

                _adlsFileSystemClient.getFileSystemOperations().create(_adlsAccountName, path, bytesContents, force);
            }

            public static void DeleteFile(String filePath) throws IOException, CloudException {
                _adlsFileSystemClient.getFileSystemOperations().delete(filePath, _adlsAccountName);
            }

            // Download file
            public static void DownloadFile(String srcPath, String destPath) throws IOException, CloudException {
                InputStream stream = _adlsFileSystemClient.getFileSystemOperations().open(srcPath, _adlsAccountName).getBody();

                PrintWriter pWriter = new PrintWriter(destPath, Charset.defaultCharset().name());

                String fileContents = "";
                if (stream != null) {
                    Writer writer = new StringWriter();

                    char[] buffer = new char[1024];
                    try {
                        Reader reader = new BufferedReader(
                                new InputStreamReader(stream, "UTF-8"));
                        int n;
                        while ((n = reader.read(buffer)) != -1) {
                            writer.write(buffer, 0, n);
                        }
                    } finally {
                        stream.close();
                    }
                    fileContents =  writer.toString();
                }

                pWriter.println(fileContents);
                pWriter.close();
            }

            // Submit a U-SQL job by providing script contents.
            // Returns hello job ID
            public static UUID SubmitJobByScript(String script, String jobName) throws IOException, CloudException {
                UUID jobId = java.util.UUID.randomUUID();
                USqlJobProperties properties = new USqlJobProperties();
                properties.setScript(script);
                JobInformation parameters = new JobInformation();
                parameters.setName(jobName);
                parameters.setJobId(jobId);
                parameters.setType(JobType.USQL);
                parameters.setProperties(properties);

                JobInformation jobInfo = _adlaJobClient.getJobOperations().create(_adlaAccountName, jobId, parameters).getBody();

                return jobId;
            }

            // Wait for job completion
            public static JobResult WaitForJob(UUID jobId) throws IOException, CloudException {
                JobInformation jobInfo = _adlaJobClient.getJobOperations().get(_adlaAccountName, jobId).getBody();
                while (jobInfo.getState() != JobState.ENDED)
                {
                    jobInfo = _adlaJobClient.getJobOperations().get(_adlaAccountName,jobId).getBody();
                }
                return jobInfo.getResult();
            }

            // Get job status
            public static String GetJobStatus(UUID jobId) throws IOException, CloudException {
                JobInformation jobInfo = _adlaJobClient.getJobOperations().get(_adlaAccountName, jobId).getBody();
                return jobInfo.getState().toValue();
            }
        }

1. <span data-ttu-id="2fd84-139">Siga Olá prompts toorun e aplicativo hello concluída.</span><span class="sxs-lookup"><span data-stu-id="2fd84-139">Follow hello prompts toorun and complete hello application.</span></span>

## <a name="see-also"></a><span data-ttu-id="2fd84-140">Consulte também</span><span class="sxs-lookup"><span data-stu-id="2fd84-140">See also</span></span>
* <span data-ttu-id="2fd84-141">toosee Olá mesmo tutorial usando outras ferramentas, clique em seletores de guia Olá na parte superior de saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="2fd84-141">toosee hello same tutorial using other tools, click hello tab selectors on hello top of hello page.</span></span>
* <span data-ttu-id="2fd84-142">toosee uma consulta mais complexa, consulte [site analisar logs usando a análise do Azure Data Lake](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="2fd84-142">toosee a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="2fd84-143">tooget iniciar o desenvolvimento de aplicativos de U-SQL, consulte [scripts de desenvolver U-SQL usando o Data Lake Tools para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2fd84-143">tooget started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="2fd84-144">toolearn U-SQL, consulte [começar com a linguagem da análise Azure Data Lake U-SQL](data-lake-analytics-u-sql-get-started.md), e [referência de linguagem SQL U](http://go.microsoft.com/fwlink/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="2fd84-144">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md), and [U-SQL language reference](http://go.microsoft.com/fwlink/?LinkId=691348).</span></span>
* <span data-ttu-id="2fd84-145">Para obter as tarefas de gerenciamento, veja [Gerenciar a Análise do Azure Data Lake usando o Portal do Azure](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2fd84-145">For management tasks, see [Manage Azure Data Lake Analytics using Azure Portal](data-lake-analytics-manage-use-portal.md).</span></span>
* <span data-ttu-id="2fd84-146">tooget uma visão geral da análise Data Lake, consulte [visão geral da análise Azure Data Lake](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2fd84-146">tooget an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>
