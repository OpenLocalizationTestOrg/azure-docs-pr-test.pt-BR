---
title: "Implantar um serviço de divisão e mesclagem | Microsoft Docs"
description: "Divisão e mesclagem com ferramenta de banco de dados elástico"
services: sql-database
documentationcenter: 
author: ddove
manager: jhubbard
editor: 
ms.assetid: 9a993c0f-7052-46cd-aa59-073bea8d535a
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 6e2fea882c248fa095a9d450ed54a7b4e64b45e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-split-merge-service"></a><span data-ttu-id="7229e-103">Implantar um serviço de divisão e mesclagem</span><span class="sxs-lookup"><span data-stu-id="7229e-103">Deploy a split-merge service</span></span>
<span data-ttu-id="7229e-104">A ferramenta de divisão e mesclagem permite mover dados entre bancos de dados fragmentados.</span><span class="sxs-lookup"><span data-stu-id="7229e-104">The split-merge tool lets you move data between sharded databases.</span></span> <span data-ttu-id="7229e-105">Veja [Mover dados entre bancos de dados na nuvem escalados horizontalmente](sql-database-elastic-scale-overview-split-and-merge.md)</span><span class="sxs-lookup"><span data-stu-id="7229e-105">See [Moving data between scaled-out cloud databases](sql-database-elastic-scale-overview-split-and-merge.md)</span></span>

## <a name="download-the-split-merge-packages"></a><span data-ttu-id="7229e-106">Baixe os pacotes de Divisão-Mesclagem</span><span class="sxs-lookup"><span data-stu-id="7229e-106">Download the Split-Merge packages</span></span>
1. <span data-ttu-id="7229e-107">Baixe a versão mais recente do NuGet de [NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).</span><span class="sxs-lookup"><span data-stu-id="7229e-107">Download the latest NuGet version from [NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).</span></span>
2. <span data-ttu-id="7229e-108">Abra um prompt de comando e navegue até o diretório onde baixou o nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="7229e-108">Open a command prompt and navigate to the directory where you downloaded nuget.exe.</span></span> <span data-ttu-id="7229e-109">O download inclui comandos do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7229e-109">The download includes PowerShell commmands.</span></span>
3. <span data-ttu-id="7229e-110">Baixe o pacote de mesclagem divisão mais recente no diretório atual com o comando abaixo:</span><span class="sxs-lookup"><span data-stu-id="7229e-110">Download the latest Split-Merge package into the current directory with the below command:</span></span>
   ```
   nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge
   ```  

<span data-ttu-id="7229e-111">Os arquivos são colocados em um diretório chamado **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x** onde *x.x.xxx.x* reflete o número de versão.</span><span class="sxs-lookup"><span data-stu-id="7229e-111">The files are placed in a directory named **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x** where *x.x.xxx.x* reflects the version number.</span></span> <span data-ttu-id="7229e-112">Localize os arquivos do Serviço de divisão e mesclagem no subdiretório **content\splitmerge\service** e os scripts de divisão e mesclagem do PowerShell (e as .dlls do cliente necessárias) no subdiretório **content\splitmerge\powershell**.</span><span class="sxs-lookup"><span data-stu-id="7229e-112">Find the split-merge Service files in the **content\splitmerge\service** sub-directory, and the Split-Merge PowerShell scripts (and required client .dlls) in the **content\splitmerge\powershell** sub-directory.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7229e-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7229e-113">Prerequisites</span></span>
1. <span data-ttu-id="7229e-114">Crie um banco de dados do Banco de Dados SQL do Azure que será usado como o banco de dados de status de divisão e mesclagem.</span><span class="sxs-lookup"><span data-stu-id="7229e-114">Create an Azure SQL DB database that will be used as the split-merge status database.</span></span> <span data-ttu-id="7229e-115">Vá para o [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7229e-115">Go to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="7229e-116">Crie um novo **banco de dados SQL**.</span><span class="sxs-lookup"><span data-stu-id="7229e-116">Create a new **SQL Database**.</span></span> <span data-ttu-id="7229e-117">Nomeie o banco de dados e crie um novo administrador e uma senha.</span><span class="sxs-lookup"><span data-stu-id="7229e-117">Give the database a name and create a new administrator and password.</span></span> <span data-ttu-id="7229e-118">Certifique-se de registrar o nome e a senha para uso posterior.</span><span class="sxs-lookup"><span data-stu-id="7229e-118">Be sure to record the name and password for later use.</span></span>
2. <span data-ttu-id="7229e-119">Certifique-se de que o servidor de Banco de Dados SQL do Azure permite que os Serviços do Azure se conectem a ele.</span><span class="sxs-lookup"><span data-stu-id="7229e-119">Ensure that your Azure SQL DB server allows Azure Services to connect to it.</span></span> <span data-ttu-id="7229e-120">No portal, em **Configurações de firewall**, verifique se a configuração **Permitir acesso aos serviços do Azure** foi definida como **Ativada**.</span><span class="sxs-lookup"><span data-stu-id="7229e-120">In the portal, in the **Firewall Settings**, ensure that the **Allow access to Azure Services** setting is set to **On**.</span></span> <span data-ttu-id="7229e-121">Clique no botão “Salvar”.</span><span class="sxs-lookup"><span data-stu-id="7229e-121">Click the "save" icon.</span></span>
   
   ![Serviços permitidos][1]
3. <span data-ttu-id="7229e-123">Crie uma conta de Armazenamento do Azure que será usada para a saída de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="7229e-123">Create an Azure Storage account that will be used for diagnostics output.</span></span> <span data-ttu-id="7229e-124">Vá para o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7229e-124">Go to the Azure Portal.</span></span> <span data-ttu-id="7229e-125">Na barra de ferramentas à esquerda, clique em **Novo**, **Dados + armazenamento** e em **Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="7229e-125">In the left bar, click **New**, click **Data + Storage**, then **Storage**.</span></span>
4. <span data-ttu-id="7229e-126">Crie um Serviço de nuvem do Azure que conterá o seu serviço de Divisão-Mesclagem.</span><span class="sxs-lookup"><span data-stu-id="7229e-126">Create an Azure Cloud Service that will contain your Split-Merge service.</span></span>  <span data-ttu-id="7229e-127">Vá para o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7229e-127">Go to the Azure Portal.</span></span> <span data-ttu-id="7229e-128">Na barra de ferramentas à esquerda, clique em **Novo**, **Calcular**, **Serviço de Nuvem** e **Criar**.</span><span class="sxs-lookup"><span data-stu-id="7229e-128">In the left bar, click **New**, then **Compute**, **Cloud Service**, and **Create**.</span></span> 

## <a name="configure-your-split-merge-service"></a><span data-ttu-id="7229e-129">Configurar o serviço de divisão e mesclagem</span><span class="sxs-lookup"><span data-stu-id="7229e-129">Configure your Split-Merge service</span></span>
### <a name="split-merge-service-configuration"></a><span data-ttu-id="7229e-130">Configuração do serviço de Divisão-Mesclagem</span><span class="sxs-lookup"><span data-stu-id="7229e-130">Split-Merge service configuration</span></span>
1. <span data-ttu-id="7229e-131">Na pasta em que você baixou os assemblies de Divisão e Mesclagem, crie uma cópia do arquivo **ServiceConfiguration.Template.cscfg** fornecido junto com **SplitMergeService.cspkg** e renomeie para **ServiceConfiguration.cscfg**.</span><span class="sxs-lookup"><span data-stu-id="7229e-131">In the folder where you downloaded the Split-Merge assemblies, create a copy of the **ServiceConfiguration.Template.cscfg** file that shipped alongside **SplitMergeService.cspkg** and rename it **ServiceConfiguration.cscfg**.</span></span>
2. <span data-ttu-id="7229e-132">Abra **ServiceConfiguration.cscfg** em um editor de texto como o Visual Studio que valide as entradas como o formato de impressões digitais de certificado.</span><span class="sxs-lookup"><span data-stu-id="7229e-132">Open **ServiceConfiguration.cscfg** in a text editor such as Visual Studio that validates inputs such as the format of certificate thumbprints.</span></span>
3. <span data-ttu-id="7229e-133">Crie um novo banco de dados ou escolha um já existente para servir como o banco de dados de status para as operações de Divisão/Mesclagem e recupere a cadeia de conexão do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="7229e-133">Create a new database or choose an existing database to serve as the status database for Split-Merge operations and retrieve the connection string of that database.</span></span> 
   
   > [!IMPORTANT]
   > <span data-ttu-id="7229e-134">Neste momento, o banco de dados de status deve usar o agrupamento latino (SQL\_Latin1\_General\_CP1\_CI\_AS).</span><span class="sxs-lookup"><span data-stu-id="7229e-134">At this time, the status database must use the Latin  collation (SQL\_Latin1\_General\_CP1\_CI\_AS).</span></span> <span data-ttu-id="7229e-135">Para obter mais informações, consulte [Nome do agrupamento do Windows (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).</span><span class="sxs-lookup"><span data-stu-id="7229e-135">For more information, see [Windows Collation Name (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).</span></span>
   >

   <span data-ttu-id="7229e-136">Com o Banco de Dados SQL do Azure, a cadeia de caracteres de conexão normalmente tem o seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="7229e-136">With Azure SQL DB, the connection string typically is of the form:</span></span>
      ```
      Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
      ```

4. <span data-ttu-id="7229e-137">Insira essa cadeia de conexão no arquivo cscfg nas seções de função **SplitMergeWeb** e **SplitMergeWorker** na configuração de ElasticScaleMetadata.</span><span class="sxs-lookup"><span data-stu-id="7229e-137">Enter this connection string in the cscfg file in both the **SplitMergeWeb** and **SplitMergeWorker** role sections in the ElasticScaleMetadata setting.</span></span>
5. <span data-ttu-id="7229e-138">Para a função **SplitMergeWorker**, digite uma cadeia de caracteres de conexão válida para o armazenamento do Azure para a configuração **WorkerRoleSynchronizationStorageAccountConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="7229e-138">For the **SplitMergeWorker** role, enter a valid connection string to Azure storage for the **WorkerRoleSynchronizationStorageAccountConnectionString** setting.</span></span>

### <a name="configure-security"></a><span data-ttu-id="7229e-139">Configurar a segurança</span><span class="sxs-lookup"><span data-stu-id="7229e-139">Configure security</span></span>
<span data-ttu-id="7229e-140">Para obter instruções detalhadas configurar a segurança do serviço, consulte as [Configuração de segurança da divisão e mesclagem](sql-database-elastic-scale-split-merge-security-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="7229e-140">For detailed instructions to configure the security of the service, refer to the [Split-Merge security configuration](sql-database-elastic-scale-split-merge-security-configuration.md).</span></span>

<span data-ttu-id="7229e-141">Para fins de implantação de teste simples para este tutorial, um conjunto mínimo de etapas de configuração será executado para colocar o serviço em operação.</span><span class="sxs-lookup"><span data-stu-id="7229e-141">For the purposes of a simple test deployment for this tutorial, a minimal set of configuration steps will be performed to get the service up and running.</span></span> <span data-ttu-id="7229e-142">Essas etapas permite que somente o computador/conta que as executa se comunique com o serviço.</span><span class="sxs-lookup"><span data-stu-id="7229e-142">These steps enable only the one machine/account executing them to communicate with the service.</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="7229e-143">Crie um certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="7229e-143">Create a self-signed certificate</span></span>
<span data-ttu-id="7229e-144">Crie um novo diretório e, nesse diretório, execute o seguinte comando usando uma janela de [Prompt de comando do desenvolvedor para o Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) :</span><span class="sxs-lookup"><span data-stu-id="7229e-144">Create a new directory and from this directory execute the following command using a [Developer Command Prompt for Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) window:</span></span>

   ```
    makecert ^
    -n "CN=*.cloudapp.net" ^
    -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2" ^
    -a sha1 -len 2048 ^
    -sr currentuser -ss root ^
    -sv MyCert.pvk MyCert.cer
   ```

<span data-ttu-id="7229e-145">Você precisará fornecer uma senha para proteger a chave privada.</span><span class="sxs-lookup"><span data-stu-id="7229e-145">You are asked for a password to protect the private key.</span></span> <span data-ttu-id="7229e-146">Digite uma senha forte e confirme-a.</span><span class="sxs-lookup"><span data-stu-id="7229e-146">Enter a strong password and confirm it.</span></span> <span data-ttu-id="7229e-147">Em seguida, será solicitado que você digite a senha mais uma vez.</span><span class="sxs-lookup"><span data-stu-id="7229e-147">You are then prompted for the password to be used once more after that.</span></span> <span data-ttu-id="7229e-148">Clique em **Sim** no final para importá-la no armazenamento Raiz de autoridades de certificação confiável.</span><span class="sxs-lookup"><span data-stu-id="7229e-148">Click **Yes** at the end to import it to the Trusted Certification Authorities Root store.</span></span>

### <a name="create-a-pfx-file"></a><span data-ttu-id="7229e-149">Criar um arquivo PFX</span><span class="sxs-lookup"><span data-stu-id="7229e-149">Create a PFX file</span></span>
<span data-ttu-id="7229e-150">Execute o seguinte comando na mesma janela onde o makecert foi executado; use a mesma senha que você usou para criar o certificado:</span><span class="sxs-lookup"><span data-stu-id="7229e-150">Execute the following command from the same window where makecert was executed; use the same password that you used to create the certificate:</span></span>

    pvk2pfx -pvk MyCert.pvk -spc MyCert.cer -pfx MyCert.pfx -pi <password>

### <a name="import-the-client-certificate-into-the-personal-store"></a><span data-ttu-id="7229e-151">Importe o certificado do cliente no repositório pessoal</span><span class="sxs-lookup"><span data-stu-id="7229e-151">Import the client certificate into the personal store</span></span>
1. <span data-ttu-id="7229e-152">No Windows Explorer, clique duas vezes em **Mycert.pfx**.</span><span class="sxs-lookup"><span data-stu-id="7229e-152">In Windows Explorer, double-click **MyCert.pfx**.</span></span>
2. <span data-ttu-id="7229e-153">No **Assistente de importação de certificado**, selecione o **Usuário Atual** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="7229e-153">In the **Certificate Import Wizard** select **Current User** and click **Next**.</span></span>
3. <span data-ttu-id="7229e-154">Confirme o caminho do arquivo e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="7229e-154">Confirm the file path and click **Next**.</span></span>
4. <span data-ttu-id="7229e-155">Digite a senha, deixe **Incluir todas as propriedades estendidas** marcado e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="7229e-155">Type the password, leave **Include all extended properties** checked and click **Next**.</span></span>
5. <span data-ttu-id="7229e-156">Deixe **Selecionar automaticamente o repositório de certificados[...]** marcado e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="7229e-156">Leave **Automatically select the certificate store[…]** checked and click **Next**.</span></span>
6. <span data-ttu-id="7229e-157">Clique em **Concluir** e em **OK**.</span><span class="sxs-lookup"><span data-stu-id="7229e-157">Click **Finish** and **OK**.</span></span>

### <a name="upload-the-pfx-file-to-the-cloud-service"></a><span data-ttu-id="7229e-158">Carregue o arquivo PFX para o serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="7229e-158">Upload the PFX file to the cloud service</span></span>
1. <span data-ttu-id="7229e-159">Vá para o [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7229e-159">Go to the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7229e-160">Selecione os **Serviços de nuvem**.</span><span class="sxs-lookup"><span data-stu-id="7229e-160">Select **Cloud Services**.</span></span>
3. <span data-ttu-id="7229e-161">Selecione o serviço de nuvem criado anteriormente para o serviço de Divisão/Mesclagem.</span><span class="sxs-lookup"><span data-stu-id="7229e-161">Select the cloud service you created above for the Split/Merge service.</span></span>
4. <span data-ttu-id="7229e-162">Clique em **Certificados** no menu superior.</span><span class="sxs-lookup"><span data-stu-id="7229e-162">Click **Certificates** on the top menu.</span></span>
5. <span data-ttu-id="7229e-163">Clique em **Carregar** na barra de ferramentas inferior.</span><span class="sxs-lookup"><span data-stu-id="7229e-163">Click **Upload** in the bottom bar.</span></span>
6. <span data-ttu-id="7229e-164">Selecione o arquivo PFX e digite a mesma senha como acima.</span><span class="sxs-lookup"><span data-stu-id="7229e-164">Select the PFX file and enter the same password as above.</span></span>
7. <span data-ttu-id="7229e-165">Depois de concluído, copie a impressão digital do certificado da nova entrada na lista.</span><span class="sxs-lookup"><span data-stu-id="7229e-165">Once completed, copy the certificate thumbprint from the new entry in the list.</span></span>

### <a name="update-the-service-configuration-file"></a><span data-ttu-id="7229e-166">Atualize o arquivo de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="7229e-166">Update the service configuration file</span></span>
<span data-ttu-id="7229e-167">Cole a impressão digital do certificado copiado acima no atributo de impressão digital/valor dessas configurações.</span><span class="sxs-lookup"><span data-stu-id="7229e-167">Paste the certificate thumbprint copied above into the thumbprint/value attribute of these settings.</span></span>
<span data-ttu-id="7229e-168">Para a função de trabalho:</span><span class="sxs-lookup"><span data-stu-id="7229e-168">For the worker role:</span></span>
   ```
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

<span data-ttu-id="7229e-169">Para a função da web:</span><span class="sxs-lookup"><span data-stu-id="7229e-169">For the web role:</span></span>

   ```
    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />
    <Setting name="AllowedClientCertificateThumbprints" value="" />
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

<span data-ttu-id="7229e-170">Observe que para implantações de produção devem ser usados certificados separados para a autoridade de certificação, para criptografia, o certificado do servidor e os certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="7229e-170">Please note that for production deployments separate certificates should be used for the CA, for encryption, the Server certificate and client certificates.</span></span> <span data-ttu-id="7229e-171">Para obter instruções detalhadas sobre isso, consulte a [Configuração de segurança](sql-database-elastic-scale-split-merge-security-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="7229e-171">For detailed instructions on this, see [Security Configuration](sql-database-elastic-scale-split-merge-security-configuration.md).</span></span>

## <a name="deploy-your-service"></a><span data-ttu-id="7229e-172">Implantar o serviço</span><span class="sxs-lookup"><span data-stu-id="7229e-172">Deploy your service</span></span>
1. <span data-ttu-id="7229e-173">Vá para o [Portal do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="7229e-173">Go to the [Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="7229e-174">Clique na guia **Serviços de nuvem** à esquerda e selecione o serviço de nuvem que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="7229e-174">Click the **Cloud Services** tab on the left, and select the cloud service that you created earlier.</span></span>
3. <span data-ttu-id="7229e-175">Clique em **Painel**.</span><span class="sxs-lookup"><span data-stu-id="7229e-175">Click **Dashboard**.</span></span>
4. <span data-ttu-id="7229e-176">Escolha o ambiente de preparo e clique em **Carregar uma nova implantação de preparo**.</span><span class="sxs-lookup"><span data-stu-id="7229e-176">Choose the staging environment, then click **Upload a new staging deployment**.</span></span>
   
   ![Staging][3]
5. <span data-ttu-id="7229e-178">Na caixa de diálogo, digite um rótulo de implantação.</span><span class="sxs-lookup"><span data-stu-id="7229e-178">In the dialog box, enter a deployment label.</span></span> <span data-ttu-id="7229e-179">Para 'Pacote' e 'Configuração', clique em 'Do local' e escolha o arquivo **SplitMergeService.cspkg** e seu arquivo .cscfg que você configurou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="7229e-179">For both 'Package' and 'Configuration', click 'From Local' and choose the **SplitMergeService.cspkg** file and your .cscfg file that you configured earlier.</span></span>
6. <span data-ttu-id="7229e-180">Certifique-se de que a caixa de seleção rotulada **Implantar mesmo se uma ou mais funções contiverem uma única instância** esteja marcada.</span><span class="sxs-lookup"><span data-stu-id="7229e-180">Ensure that the checkbox labeled **Deploy even if one or more roles contain a single instance** is checked.</span></span>
7. <span data-ttu-id="7229e-181">Clique no botão de escala no canto inferior direito para iniciar a implantação.</span><span class="sxs-lookup"><span data-stu-id="7229e-181">Hit the tick button in the bottom right to begin the deployment.</span></span> <span data-ttu-id="7229e-182">Isso poderá levar alguns minutos para ser concluído.</span><span class="sxs-lookup"><span data-stu-id="7229e-182">Expect it to take a few minutes to complete.</span></span>

   ![Carregar][4]

## <a name="troubleshoot-the-deployment"></a><span data-ttu-id="7229e-184">Solucionar problemas de implantação</span><span class="sxs-lookup"><span data-stu-id="7229e-184">Troubleshoot the deployment</span></span>
<span data-ttu-id="7229e-185">Se sua função web não ficar online, provavelmente é um problema com a configuração de segurança.</span><span class="sxs-lookup"><span data-stu-id="7229e-185">If your web role fails to come online, it is likely a problem with the security configuration.</span></span> <span data-ttu-id="7229e-186">Verifique se o SSL está configurado como descrito acima.</span><span class="sxs-lookup"><span data-stu-id="7229e-186">Check that the SSL is configured as described above.</span></span>

<span data-ttu-id="7229e-187">Se sua função de trabalho não fica online, mas sua função web tiver êxito, provavelmente é um problema na conexão com o banco de dados de status que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="7229e-187">If your worker role fails to come online, but your web role succeeds, it is most likely a problem connecting to the status database that you created earlier.</span></span>

* <span data-ttu-id="7229e-188">Certifique-se de que a cadeia de caracteres de conexão no seu .cscfg seja precisa.</span><span class="sxs-lookup"><span data-stu-id="7229e-188">Make sure that the connection string in your .cscfg is accurate.</span></span>
* <span data-ttu-id="7229e-189">Verifique se o servidor e o banco de dados existem e se a ID de usuário e a senha estão corretas.</span><span class="sxs-lookup"><span data-stu-id="7229e-189">Check that the server and database exist, and that the user id and password are correct.</span></span>
* <span data-ttu-id="7229e-190">Para o Banco de Dados SQL do Azure, a cadeia de conexão deve estar no formato:</span><span class="sxs-lookup"><span data-stu-id="7229e-190">For Azure SQL DB, the connection string should be of the form:</span></span>

   ```  
   Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
   ```

* <span data-ttu-id="7229e-191">Verifique se o nome do servidor não começa com **https://**.</span><span class="sxs-lookup"><span data-stu-id="7229e-191">Ensure that the server name does not begin with **https://**.</span></span>
* <span data-ttu-id="7229e-192">Certifique-se de que o servidor de Banco de Dados SQL do Azure permite que os Serviços do Azure se conectem a ele.</span><span class="sxs-lookup"><span data-stu-id="7229e-192">Ensure that your Azure SQL DB server allows Azure Services to connect to it.</span></span> <span data-ttu-id="7229e-193">Para fazer isso, abra https://manage.windowsazure.com, clique em "Bancos de dados SQL" à esquerda, clique em "Servidores" na parte superior e selecione seu servidor.</span><span class="sxs-lookup"><span data-stu-id="7229e-193">To do this, open https://manage.windowsazure.com, click “SQL Databases” on the left, click “Servers” at the top, and select your server.</span></span> <span data-ttu-id="7229e-194">Clique em **Configurar** na parte superior e verifique se a configuração dos **Serviços do Azure** estão definidas como “Sim”.</span><span class="sxs-lookup"><span data-stu-id="7229e-194">Click **Configure** at the top and ensure that the **Azure Services** setting is set to “Yes”.</span></span> <span data-ttu-id="7229e-195">(Consulte a seção Pré-requisitos na parte superior deste artigo).</span><span class="sxs-lookup"><span data-stu-id="7229e-195">(See the Prerequisites section at the top of this article).</span></span>

## <a name="test-the-service-deployment"></a><span data-ttu-id="7229e-196">Testar a implantação do serviço</span><span class="sxs-lookup"><span data-stu-id="7229e-196">Test the service deployment</span></span>
### <a name="connect-with-a-web-browser"></a><span data-ttu-id="7229e-197">Conectar-se com um navegador da Web</span><span class="sxs-lookup"><span data-stu-id="7229e-197">Connect with a web browser</span></span>
<span data-ttu-id="7229e-198">Determine o ponto de extremidade da web do serviço de Divisão-Mesclagem.</span><span class="sxs-lookup"><span data-stu-id="7229e-198">Determine the web endpoint of your Split-Merge service.</span></span> <span data-ttu-id="7229e-199">Você pode descobrir isso no Portal Clássico do Azure indo para o **Painel** do seu serviço de nuvem e procurando na **URL do Site**, no lado direito.</span><span class="sxs-lookup"><span data-stu-id="7229e-199">You can find this in the Azure Classic Portal by going to the **Dashboard** of your cloud service and looking under **Site URL** on the right side.</span></span> <span data-ttu-id="7229e-200">Substitua **http://** por **https://**, uma vez que as configurações de segurança padrão desabilitam o ponto de extremidade HTTP.</span><span class="sxs-lookup"><span data-stu-id="7229e-200">Replace **http://** with **https://** since the default security settings disable the HTTP endpoint.</span></span> <span data-ttu-id="7229e-201">Carregue a página para este URL no seu navegador.</span><span class="sxs-lookup"><span data-stu-id="7229e-201">Load the page for this URL into your browser.</span></span>

### <a name="test-with-powershell-scripts"></a><span data-ttu-id="7229e-202">Testes com scripts do PowerShell</span><span class="sxs-lookup"><span data-stu-id="7229e-202">Test with PowerShell scripts</span></span>
<span data-ttu-id="7229e-203">A implantação e sue ambiente podem ser testados, executando os scripts de exemplo do PowerShell incluídos.</span><span class="sxs-lookup"><span data-stu-id="7229e-203">The deployment and your environment can be tested by running the included sample PowerShell scripts.</span></span>

<span data-ttu-id="7229e-204">Os arquivos de script incluídos são:</span><span class="sxs-lookup"><span data-stu-id="7229e-204">The script files included are:</span></span>

1. <span data-ttu-id="7229e-205">**SetupSampleSplitMergeEnvironment.ps1** - configura uma camada de dados de teste para Divisão/Mesclagem (consulte a tabela abaixo para uma descrição detalhada)</span><span class="sxs-lookup"><span data-stu-id="7229e-205">**SetupSampleSplitMergeEnvironment.ps1** - sets up a test data tier for Split/Merge (see table below for detailed description)</span></span>
2. <span data-ttu-id="7229e-206">**ExecuteSampleSplitMerge.ps1** - executa operações de teste no teste de camada de dados (consulte a tabela abaixo para uma descrição detalhada)</span><span class="sxs-lookup"><span data-stu-id="7229e-206">**ExecuteSampleSplitMerge.ps1** - executes test operations on the test data tier (see table below for detailed description)</span></span>
3. <span data-ttu-id="7229e-207">**GetMappings.ps1** — o script de exemplo de nível superior que imprime o estado atual dos mapeamentos de fragmento.</span><span class="sxs-lookup"><span data-stu-id="7229e-207">**GetMappings.ps1** - top-level sample script that prints out the current state of the shard mappings.</span></span>
4. <span data-ttu-id="7229e-208">**ShardManagement.psm1** – o script auxiliar que encapsula a API ShardManagement</span><span class="sxs-lookup"><span data-stu-id="7229e-208">**ShardManagement.psm1**  - helper script that wraps the ShardManagement API</span></span>
5. <span data-ttu-id="7229e-209">**SqlDatabaseHelpers.psm1** – o script auxiliar para criar e gerenciar bancos de dados SQL</span><span class="sxs-lookup"><span data-stu-id="7229e-209">**SqlDatabaseHelpers.psm1** - helper script for creating and managing SQL databases</span></span>
   
   <table style="width:100%">
     <tr>
       <th><span data-ttu-id="7229e-210">Arquivo do PowerShell</span><span class="sxs-lookup"><span data-stu-id="7229e-210">PowerShell file</span></span></th>
       <th><span data-ttu-id="7229e-211">Etapas</span><span class="sxs-lookup"><span data-stu-id="7229e-211">Steps</span></span></th>
     </tr>
     <tr>
       <th rowspan="5"><span data-ttu-id="7229e-212">SetupSampleSplitMergeEnvironment.ps1</span><span class="sxs-lookup"><span data-stu-id="7229e-212">SetupSampleSplitMergeEnvironment.ps1</span></span></th>
       <td>1.    <span data-ttu-id="7229e-213">Cria um banco de dados do gerenciador de mapa do fragmento</span><span class="sxs-lookup"><span data-stu-id="7229e-213">Creates a shard map manager database</span></span></td>
     </tr>
     <tr>
       <td>2.    <span data-ttu-id="7229e-214">Cria 2 bancos de dados do fragmento.</span><span class="sxs-lookup"><span data-stu-id="7229e-214">Creates 2 shard databases.</span></span>
     </tr>
     <tr>
       <td>3.    <span data-ttu-id="7229e-215">Cria um mapa do fragmento para esses bancos de dados (exclui quaisquer mapas do fragmento existentes nesses bancos de dados).</span><span class="sxs-lookup"><span data-stu-id="7229e-215">Creates a shard map for those database (deletes any existing shard maps on those databases).</span></span> </td>
     </tr>
     <tr>
       <td>4.    <span data-ttu-id="7229e-216">Cria uma pequena tabela de exemplo em ambos os fragmentos e preenche a tabela em um dos fragmentos.</span><span class="sxs-lookup"><span data-stu-id="7229e-216">Creates a small sample table in both the shards, and populates the table in one of the shards.</span></span></td>
     </tr>
     <tr>
       <td>5.    <span data-ttu-id="7229e-217">Declara o SchemaInfo para a tabela fragmentada.</span><span class="sxs-lookup"><span data-stu-id="7229e-217">Declares the SchemaInfo for the sharded table.</span></span></td>
     </tr>
   </table>
   <table style="width:100%">
     <tr>
       <th><span data-ttu-id="7229e-218">Arquivo do PowerShell</span><span class="sxs-lookup"><span data-stu-id="7229e-218">PowerShell file</span></span></th>
       <th><span data-ttu-id="7229e-219">Etapas</span><span class="sxs-lookup"><span data-stu-id="7229e-219">Steps</span></span></th>
     </tr>
   <tr>
       <th rowspan="4"><span data-ttu-id="7229e-220">ExecuteSampleSplitMerge.ps1</span><span class="sxs-lookup"><span data-stu-id="7229e-220">ExecuteSampleSplitMerge.ps1</span></span> </th>
       <td>1.    <span data-ttu-id="7229e-221">Envia uma solicitação divisão para o front-end da Web do Serviço de Divisão-Mesclagem, que divide metade dos dados do primeiro fragmento para o segundo.</span><span class="sxs-lookup"><span data-stu-id="7229e-221">Sends a split request to the Split-Merge Service web frontend, which splits half the data from the first shard to the second shard.</span></span></td>
     </tr>
     <tr>
       <td>2.    <span data-ttu-id="7229e-222">Elege o front-end da web para o status da solicitação de divisão e aguarda até que a solicitação seja concluída.</span><span class="sxs-lookup"><span data-stu-id="7229e-222">Polls the web frontend for the split request status and waits until the request completes.</span></span></td>
     </tr>
     <tr>
       <td>3.    <span data-ttu-id="7229e-223">Envia uma solicitação de mesclagem ao front-end da Web do Serviço de Divisão-Mesclagem, que move os dados do segundo fragmento para o primeiro.</span><span class="sxs-lookup"><span data-stu-id="7229e-223">Sends a merge request to the Split-Merge Service web frontend, which moves the data from the second shard back to the first shard.</span></span></td>
     </tr>
     <tr>
       <td>4.    <span data-ttu-id="7229e-224">Elege o front-end da web para o status da solicitação de mesclagem e aguarda até que a solicitação seja concluída.</span><span class="sxs-lookup"><span data-stu-id="7229e-224">Polls the web frontend for the merge request status and waits until the request completes.</span></span></td>
     </tr>
   </table>
   
## <a name="use-powershell-to-verify-your-deployment"></a><span data-ttu-id="7229e-225">Usar o PowerShell para verificar sua implantação</span><span class="sxs-lookup"><span data-stu-id="7229e-225">Use PowerShell to verify your deployment</span></span>
1. <span data-ttu-id="7229e-226">Abra uma nova janela do PowerShell, navegue até o diretório onde baixou o pacote de Divisão-Mesclagem e, em seguida, navegue para o diretório do “powershell”.</span><span class="sxs-lookup"><span data-stu-id="7229e-226">Open a new PowerShell window and navigate to the directory where you downloaded the Split-Merge package, and then navigate into the “powershell” directory.</span></span>
2. <span data-ttu-id="7229e-227">Crie um servidor de banco de dados SQL do Azure (ou escolha um servidor existente) onde o gerenciador do mapa do fragmento e os fragmentos serão criados.</span><span class="sxs-lookup"><span data-stu-id="7229e-227">Create an Azure SQL database server (or choose an existing server) where the shard map manager and shards will be created.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7229e-228">O script SetupSampleSplitMergeEnvironment.ps1 cria todos esses bancos de dados no mesmo servidor por padrão para manter o script simples.</span><span class="sxs-lookup"><span data-stu-id="7229e-228">The SetupSampleSplitMergeEnvironment.ps1 script creates all these databases on the same server by default to keep the script simple.</span></span> <span data-ttu-id="7229e-229">Isso não é uma restrição do Serviço de Divisão-Mesclagem em si.</span><span class="sxs-lookup"><span data-stu-id="7229e-229">This is not a restriction of the Split-Merge Service itself.</span></span>
   >
   
   <span data-ttu-id="7229e-230">Um logon de autenticação do SQL com acesso de leitura/gravação para os bancos de dados será necessário para que o serviço de Divisão-Mesclagem mova os dados e atualize o mapa do fragmento.</span><span class="sxs-lookup"><span data-stu-id="7229e-230">A SQL authentication login with read/write access to the DBs will be needed for the Split-Merge service to move data and update the shard map.</span></span> <span data-ttu-id="7229e-231">Desde que o Serviço de Divisão-Mesclagem seja executado na nuvem, ele atualmente não dá suporte à Autenticação integrada.</span><span class="sxs-lookup"><span data-stu-id="7229e-231">Since the Split-Merge Service runs in the cloud, it does not currently support Integrated Authentication.</span></span>
   
   <span data-ttu-id="7229e-232">Verifique se o SQL Server do Azure está configurado para permitir acesso do endereço IP do computador que executa esses scripts.</span><span class="sxs-lookup"><span data-stu-id="7229e-232">Make sure the Azure SQL server is configured to allow access from the IP address of the machine running these scripts.</span></span> <span data-ttu-id="7229e-233">Você pode encontrar essa configuração em SQL Server do Azure / configuração / endereços de IP permitidos.</span><span class="sxs-lookup"><span data-stu-id="7229e-233">You can find this setting under the Azure SQL server / configuration / allowed IP addresses.</span></span>
3. <span data-ttu-id="7229e-234">Execute o script SetupSampleSplitMergeEnvironment.ps1 para criar o ambiente de exemplo.</span><span class="sxs-lookup"><span data-stu-id="7229e-234">Execute the SetupSampleSplitMergeEnvironment.ps1 script to create the sample environment.</span></span>
   
   <span data-ttu-id="7229e-235">A execução desse script apagará quaisquer estruturas de dados de gerenciamento de mapa do fragmento existentes no banco de dados do gerenciador do mapa do fragmento e nos fragmentos.</span><span class="sxs-lookup"><span data-stu-id="7229e-235">Running this script will wipe out any existing shard map management data structures on the shard map manager database and the shards.</span></span> <span data-ttu-id="7229e-236">Ele pode ser útil para executar novamente o script, se desejar reinicializar o mapa do fragmento ou os fragmentos.</span><span class="sxs-lookup"><span data-stu-id="7229e-236">It may be useful to rerun the script if you wish to re-initialize the shard map or shards.</span></span>
   
   <span data-ttu-id="7229e-237">Linha de comando de exemplo:</span><span class="sxs-lookup"><span data-stu-id="7229e-237">Sample command line:</span></span>

   ```   
     .\SetupSampleSplitMergeEnvironment.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'
   ```      
4. <span data-ttu-id="7229e-238">Execute o script Getmappings.ps1 para exibir os mapeamentos que existem atualmente no ambiente de exemplo.</span><span class="sxs-lookup"><span data-stu-id="7229e-238">Execute the Getmappings.ps1 script to view the mappings that currently exist in the sample environment.</span></span>
   
   ```
     .\GetMappings.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'

   ```         
5. <span data-ttu-id="7229e-239">Execute o script ExecuteSampleSplitMerge.ps1 para executar uma operação de divisão (mover metade dos dados no primeiro fragmento para o segundo) e, em seguida, uma operação de mesclagem (mover os dados de volta para o primeiro fragmento).</span><span class="sxs-lookup"><span data-stu-id="7229e-239">Execute the ExecuteSampleSplitMerge.ps1 script to execute a split operation (moving half the data on the first shard to the second shard) and then a merge operation (moving the data back onto the first shard).</span></span> <span data-ttu-id="7229e-240">Se você configurou o SSL e deixou o ponto de extremidade http desabilitado, verifique se, ao invés disso, usou o ponto de extremidade https://.</span><span class="sxs-lookup"><span data-stu-id="7229e-240">If you configured SSL and left the http endpoint disabled, ensure that you use the https:// endpoint instead.</span></span>
   
   <span data-ttu-id="7229e-241">Linha de comando de exemplo:</span><span class="sxs-lookup"><span data-stu-id="7229e-241">Sample command line:</span></span>

   ```   
     .\ExecuteSampleSplitMerge.ps1
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net' 
         -SplitMergeServiceEndpoint 'https://mysplitmergeservice.cloudapp.net' 
         -CertificateThumbprint '0123456789abcdef0123456789abcdef01234567'
   ```      
   
   <span data-ttu-id="7229e-242">Se você receber o erro abaixo, provavelmente é um problema com o certificado do ponto de extremidade da Web.</span><span class="sxs-lookup"><span data-stu-id="7229e-242">If you receive the below error, it is most likely a problem with your Web endpoint’s certificate.</span></span> <span data-ttu-id="7229e-243">Tente se conectar ao ponto de extremidade da Web com seu navegador da Web favorito e verifique se há um erro de certificado.</span><span class="sxs-lookup"><span data-stu-id="7229e-243">Try connecting to the Web endpoint with your favorite Web browser and check if there is a certificate error.</span></span>
   
     ```
     Invoke-WebRequest : The underlying connection was closed: Could not establish trust relationship for the SSL/TLSsecure channel.
     ```
   
   <span data-ttu-id="7229e-244">Se for bem-sucedido, a saída deve se parecer com isso:</span><span class="sxs-lookup"><span data-stu-id="7229e-244">If it succeeded, the output should look like the below:</span></span>
   
   ```
   > .\ExecuteSampleSplitMerge.ps1 -UserName 'mysqluser' -Password 'MySqlPassw0rd' -ShardMapManagerServerName 'abcdefghij.database.windows.net' -SplitMergeServiceEndpoint 'http://mysplitmergeservice.cloudapp.net' -CertificateThumbprint 0123456789abcdef0123456789abcdef01234567
   > Sending split request
   > Began split operation with id dc68dfa0-e22b-4823-886a-9bdc903c80f3
   > Polling split-merge request status. Press Ctrl-C to end
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source to target shard.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Waiting for reference tables copy     completion.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source to target shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing the request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > Sending merge request
   > Began merge operation with id 6ffc308f-d006-466b-b24e-857242ec5f66
   > Polling request status. Press Ctrl-C to end
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source to target shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing the request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > 
   ```
6. <span data-ttu-id="7229e-245">Experimente outros tipos de dados!</span><span class="sxs-lookup"><span data-stu-id="7229e-245">Experiment with other data types!</span></span> <span data-ttu-id="7229e-246">Todos esses scripts usam um parâmetro de - ShardKeyType opcional que permite que você especifique o tipo de chave.</span><span class="sxs-lookup"><span data-stu-id="7229e-246">All of these scripts take an optional -ShardKeyType parameter that allows you to specify the key type.</span></span> <span data-ttu-id="7229e-247">O padrão é Int32, mas você também pode especificar Int64, Guid ou binário.</span><span class="sxs-lookup"><span data-stu-id="7229e-247">The default is Int32, but you can also specify Int64, Guid, or Binary.</span></span>

## <a name="create-requests"></a><span data-ttu-id="7229e-248">Criar solicitações</span><span class="sxs-lookup"><span data-stu-id="7229e-248">Create requests</span></span>
<span data-ttu-id="7229e-249">O serviço pode ser usado por meio da IU da web ou importando e usando o módulo SplitMerge.psm1 do PowerShell que irá enviar suas solicitações por meio da função web.</span><span class="sxs-lookup"><span data-stu-id="7229e-249">The service can be used either by using the web UI or by importing and using the SplitMerge.psm1 PowerShell module which will submit your requests through the web role.</span></span>

<span data-ttu-id="7229e-250">O serviço pode mover dados em tabelas fragmentadas e tabelas de referência.</span><span class="sxs-lookup"><span data-stu-id="7229e-250">The service can move data in both sharded tables and reference tables.</span></span> <span data-ttu-id="7229e-251">Uma tabela fragmentada possui uma coluna de chave de fragmentação e tem diferentes dados de linha em cada fragmento.</span><span class="sxs-lookup"><span data-stu-id="7229e-251">A sharded table has a sharding key column and has different row data on each shard.</span></span> <span data-ttu-id="7229e-252">Uma tabela de referência não é fragmentada para que ele contenha os mesmos dados de linha em cada fragmento.</span><span class="sxs-lookup"><span data-stu-id="7229e-252">A reference table is not sharded so it contains the same row data on every shard.</span></span> <span data-ttu-id="7229e-253">As tabelas de referência são úteis para dados que não mudam com frequência e são usadas para associação com tabelas fragmentadas em consultas.</span><span class="sxs-lookup"><span data-stu-id="7229e-253">Reference tables are useful for data that does not change often and is used to JOIN with sharded tables in queries.</span></span>

<span data-ttu-id="7229e-254">Para executar uma operação de Divisão-Mesclagem, você deve declarar as tabelas fragmentadas e as tabelas de referência que deseja mover.</span><span class="sxs-lookup"><span data-stu-id="7229e-254">In order to perform a split-merge operation, you must declare the sharded tables and reference tables that you want to have moved.</span></span> <span data-ttu-id="7229e-255">Isso é feito com a API **SchemaInfo** .</span><span class="sxs-lookup"><span data-stu-id="7229e-255">This is accomplished with the **SchemaInfo** API.</span></span> <span data-ttu-id="7229e-256">Esta API está no namespace **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** .</span><span class="sxs-lookup"><span data-stu-id="7229e-256">This API is in the **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** namespace.</span></span>

1. <span data-ttu-id="7229e-257">Para cada tabela fragmentada, crie um objeto **ShardedTableInfo** que descreve o nome do esquema da tabela pai (opcional, o padrão é “dbo”), o nome da tabela e o nome da coluna na tabela que contém a chave de fragmentação.</span><span class="sxs-lookup"><span data-stu-id="7229e-257">For each sharded table, create a **ShardedTableInfo** object describing the table’s parent schema name (optional, defaults to “dbo”), the table name, and the column name in that table that contains the sharding key.</span></span>
2. <span data-ttu-id="7229e-258">Para cada tabela de referência, crie um objeto de **ReferenceTableInfo** que descreve o nome do esquema da tabela pai (opcional, o padrão é “dbo”) e o nome da tabela.</span><span class="sxs-lookup"><span data-stu-id="7229e-258">For each reference table, create a **ReferenceTableInfo** object describing the table’s parent schema name (optional, defaults to “dbo”) and the table name.</span></span>
3. <span data-ttu-id="7229e-259">Adicione os objetos TableInfo acima para um novo objeto **SchemaInfo** .</span><span class="sxs-lookup"><span data-stu-id="7229e-259">Add the above TableInfo objects to a new **SchemaInfo** object.</span></span>
4. <span data-ttu-id="7229e-260">Obtenha uma referência para um objeto **ShardMapManager** e chame **GetSchemaInfoCollection**.</span><span class="sxs-lookup"><span data-stu-id="7229e-260">Get a reference to a **ShardMapManager** object, and call **GetSchemaInfoCollection**.</span></span>
5. <span data-ttu-id="7229e-261">Adicione o **SchemaInfo** ao **SchemaInfoCollection**, fornecendo o nome do mapa de fragmento.</span><span class="sxs-lookup"><span data-stu-id="7229e-261">Add the **SchemaInfo** to the **SchemaInfoCollection**, providing the shard map name.</span></span>

<span data-ttu-id="7229e-262">Um exemplo disso pode ser visto no script SetupSampleSplitMergeEnvironment.ps1.</span><span class="sxs-lookup"><span data-stu-id="7229e-262">An example of this can be seen in the SetupSampleSplitMergeEnvironment.ps1 script.</span></span>

<span data-ttu-id="7229e-263">O serviço de Divisão-Mesclagem não cria para você o banco de dados de destino (ou o esquema para todas as tabelas no banco de dados).</span><span class="sxs-lookup"><span data-stu-id="7229e-263">The Split-Merge service does not create the target database (or schema for any tables in the database) for you.</span></span> <span data-ttu-id="7229e-264">Eles devem ser criados previamente antes de enviar uma solicitação ao serviço.</span><span class="sxs-lookup"><span data-stu-id="7229e-264">They must be pre-created before sending a request to the service.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="7229e-265">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="7229e-265">Troubleshooting</span></span>
<span data-ttu-id="7229e-266">Você pode ver a mensagem abaixo ao executar os scripts do powershell de exemplo:</span><span class="sxs-lookup"><span data-stu-id="7229e-266">You may see the below message when running the sample powershell scripts:</span></span>

   ```
   Invoke-WebRequest : The underlying connection was closed: Could not establish trust relationship for the SSL/TLS secure channel.
   ```

<span data-ttu-id="7229e-267">Esse erro significa que o certificado SSL não está corretamente configurado.</span><span class="sxs-lookup"><span data-stu-id="7229e-267">This error means that your SSL certificate is not configured correctly.</span></span> <span data-ttu-id="7229e-268">Siga as instruções na seção 'Conectando-se com um navegador da Web'.</span><span class="sxs-lookup"><span data-stu-id="7229e-268">Please follow the instructions in section 'Connecting with a web browser'.</span></span>

<span data-ttu-id="7229e-269">Se não for possível enviar solicitações, você verá isso:</span><span class="sxs-lookup"><span data-stu-id="7229e-269">If you cannot submit requests you may see this:</span></span>

```
[Exception] System.Data.SqlClient.SqlException (0x80131904): Could not find stored procedure 'dbo.InsertRequest'. 
```

<span data-ttu-id="7229e-270">Nesse caso, verifique seu arquivo de configuração, em particular a configuração para **WorkerRoleSynchronizationStorageAccountConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="7229e-270">In this case, check your configuration file, in particular the setting for **WorkerRoleSynchronizationStorageAccountConnectionString**.</span></span> <span data-ttu-id="7229e-271">Esse erro normalmente indica que a função de trabalho não pôde inicializar com êxito o banco de dados de metadados no primeiro uso.</span><span class="sxs-lookup"><span data-stu-id="7229e-271">This error typically indicates that the worker role could not successfully initialize the metadata database on first use.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/allowed-services.png
[2]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/manage.png
[3]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/staging.png
[4]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/upload.png
[5]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/storage.png

