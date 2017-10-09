---
title: "aaaDeploy um serviço de divisão mesclagem | Microsoft Docs"
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
ms.openlocfilehash: 6fef641cbc1e73ce34a851c53298a072dade8f9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-split-merge-service"></a><span data-ttu-id="43954-103">Implantar um serviço de divisão e mesclagem</span><span class="sxs-lookup"><span data-stu-id="43954-103">Deploy a split-merge service</span></span>
<span data-ttu-id="43954-104">ferramenta de mesclagem de divisão de saudação permite mover dados entre bancos de dados fragmentados.</span><span class="sxs-lookup"><span data-stu-id="43954-104">hello split-merge tool lets you move data between sharded databases.</span></span> <span data-ttu-id="43954-105">Veja [Mover dados entre bancos de dados na nuvem escalados horizontalmente](sql-database-elastic-scale-overview-split-and-merge.md)</span><span class="sxs-lookup"><span data-stu-id="43954-105">See [Moving data between scaled-out cloud databases](sql-database-elastic-scale-overview-split-and-merge.md)</span></span>

## <a name="download-hello-split-merge-packages"></a><span data-ttu-id="43954-106">Baixe os pacotes de divisão mesclagem Olá</span><span class="sxs-lookup"><span data-stu-id="43954-106">Download hello Split-Merge packages</span></span>
1. <span data-ttu-id="43954-107">Baixar a versão mais recente de NuGet saudação do [NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).</span><span class="sxs-lookup"><span data-stu-id="43954-107">Download hello latest NuGet version from [NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).</span></span>
2. <span data-ttu-id="43954-108">Abra um prompt de comando e navegue toohello diretório onde você baixou o nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="43954-108">Open a command prompt and navigate toohello directory where you downloaded nuget.exe.</span></span> <span data-ttu-id="43954-109">download de saudação inclui commmands do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="43954-109">hello download includes PowerShell commmands.</span></span>
3. <span data-ttu-id="43954-110">Baixe o pacote de mesclagem a divisão mais recente do hello no diretório atual de saudação com hello comando abaixo:</span><span class="sxs-lookup"><span data-stu-id="43954-110">Download hello latest Split-Merge package into hello current directory with hello below command:</span></span>
   ```
   nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge
   ```  

<span data-ttu-id="43954-111">Olá arquivos são colocados em um diretório chamado **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x** onde *x.x.xxx.x* reflete o número de versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="43954-111">hello files are placed in a directory named **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x** where *x.x.xxx.x* reflects hello version number.</span></span> <span data-ttu-id="43954-112">Localizar arquivos de serviço de divisão de mesclagem de Olá no hello **content\splitmerge\service** subdiretório e Olá scripts do PowerShell de divisão de mesclagem (e DLLs de cliente necessárias) em Olá **content\splitmerge\powershell** subdiretório.</span><span class="sxs-lookup"><span data-stu-id="43954-112">Find hello split-merge Service files in hello **content\splitmerge\service** sub-directory, and hello Split-Merge PowerShell scripts (and required client .dlls) in hello **content\splitmerge\powershell** sub-directory.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="43954-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="43954-113">Prerequisites</span></span>
1. <span data-ttu-id="43954-114">Crie um banco de dados do banco de dados de SQL do Azure que será usado como banco de dados de status de divisão mesclagem Olá.</span><span class="sxs-lookup"><span data-stu-id="43954-114">Create an Azure SQL DB database that will be used as hello split-merge status database.</span></span> <span data-ttu-id="43954-115">Vá toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="43954-115">Go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="43954-116">Crie um novo **banco de dados SQL**.</span><span class="sxs-lookup"><span data-stu-id="43954-116">Create a new **SQL Database**.</span></span> <span data-ttu-id="43954-117">Dê um nome de banco de dados de saudação e criar um novo administrador e uma senha.</span><span class="sxs-lookup"><span data-stu-id="43954-117">Give hello database a name and create a new administrator and password.</span></span> <span data-ttu-id="43954-118">Ser-se de nome de saudação do toorecord e a senha para uso posterior.</span><span class="sxs-lookup"><span data-stu-id="43954-118">Be sure toorecord hello name and password for later use.</span></span>
2. <span data-ttu-id="43954-119">Certifique-se de que o servidor de banco de dados de SQL do Azure permite que serviços do Azure tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="43954-119">Ensure that your Azure SQL DB server allows Azure Services tooconnect tooit.</span></span> <span data-ttu-id="43954-120">No portal de saudação em hello **as configurações do Firewall**, certifique-se de que Olá **permitir acesso a serviços tooAzure** configuração está definida muito**em**.</span><span class="sxs-lookup"><span data-stu-id="43954-120">In hello portal, in hello **Firewall Settings**, ensure that hello **Allow access tooAzure Services** setting is set too**On**.</span></span> <span data-ttu-id="43954-121">Clique em hello "Salvar" ícone.</span><span class="sxs-lookup"><span data-stu-id="43954-121">Click hello "save" icon.</span></span>
   
   ![Serviços permitidos][1]
3. <span data-ttu-id="43954-123">Crie uma conta de Armazenamento do Azure que será usada para a saída de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="43954-123">Create an Azure Storage account that will be used for diagnostics output.</span></span> <span data-ttu-id="43954-124">Vá toohello Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="43954-124">Go toohello Azure Portal.</span></span> <span data-ttu-id="43954-125">Na barra de saudação à esquerda, clique em **novo**, clique em **dados + armazenamento**, em seguida, **armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="43954-125">In hello left bar, click **New**, click **Data + Storage**, then **Storage**.</span></span>
4. <span data-ttu-id="43954-126">Crie um Serviço de nuvem do Azure que conterá o seu serviço de Divisão-Mesclagem.</span><span class="sxs-lookup"><span data-stu-id="43954-126">Create an Azure Cloud Service that will contain your Split-Merge service.</span></span>  <span data-ttu-id="43954-127">Vá toohello Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="43954-127">Go toohello Azure Portal.</span></span> <span data-ttu-id="43954-128">Na barra de saudação à esquerda, clique em **novo**, em seguida, **de computação**, **serviço de nuvem**, e **criar**.</span><span class="sxs-lookup"><span data-stu-id="43954-128">In hello left bar, click **New**, then **Compute**, **Cloud Service**, and **Create**.</span></span> 

## <a name="configure-your-split-merge-service"></a><span data-ttu-id="43954-129">Configurar o serviço de divisão e mesclagem</span><span class="sxs-lookup"><span data-stu-id="43954-129">Configure your Split-Merge service</span></span>
### <a name="split-merge-service-configuration"></a><span data-ttu-id="43954-130">Configuração do serviço de Divisão-Mesclagem</span><span class="sxs-lookup"><span data-stu-id="43954-130">Split-Merge service configuration</span></span>
1. <span data-ttu-id="43954-131">Na pasta de saudação onde você baixou assemblies Olá direta de divisão, crie uma cópia da saudação **ServiceConfiguration.Template.cscfg** arquivo enviado junto com o **SplitMergeService.cspkg** e renomeá-lo **ServiceConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="43954-131">In hello folder where you downloaded hello Split-Merge assemblies, create a copy of hello **ServiceConfiguration.Template.cscfg** file that shipped alongside **SplitMergeService.cspkg** and rename it **ServiceConfiguration.cscfg**.</span></span>
2. <span data-ttu-id="43954-132">Abra **ServiceConfiguration** em um editor de texto como o Visual Studio valida entradas, como o formato de saudação de impressões digitais de certificado.</span><span class="sxs-lookup"><span data-stu-id="43954-132">Open **ServiceConfiguration.cscfg** in a text editor such as Visual Studio that validates inputs such as hello format of certificate thumbprints.</span></span>
3. <span data-ttu-id="43954-133">Criar um novo banco de dados ou escolha um tooserve existentes do banco de dados como banco de dados de status de saudação para operações de divisão de mesclagem e recuperar Olá cadeia de caracteres de conexão do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="43954-133">Create a new database or choose an existing database tooserve as hello status database for Split-Merge operations and retrieve hello connection string of that database.</span></span> 
   
   > [!IMPORTANT]
   > <span data-ttu-id="43954-134">Neste momento, o banco de dados de status de saudação deve usar agrupamento latino hello (SQL\_latino1\_geral\_CP1\_CI\_AS).</span><span class="sxs-lookup"><span data-stu-id="43954-134">At this time, hello status database must use hello Latin  collation (SQL\_Latin1\_General\_CP1\_CI\_AS).</span></span> <span data-ttu-id="43954-135">Para obter mais informações, consulte [Nome do agrupamento do Windows (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).</span><span class="sxs-lookup"><span data-stu-id="43954-135">For more information, see [Windows Collation Name (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).</span></span>
   >

   <span data-ttu-id="43954-136">Com o banco de dados de SQL do Azure, cadeia de caracteres de conexão Olá normalmente é de formulário de saudação:</span><span class="sxs-lookup"><span data-stu-id="43954-136">With Azure SQL DB, hello connection string typically is of hello form:</span></span>
      ```
      Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
      ```

4. <span data-ttu-id="43954-137">Insira essa cadeia de caracteres de conexão no arquivo de cscfg Olá em ambos os Olá **SplitMergeWeb** e **SplitMergeWorker** seções de função na configuração de ElasticScaleMetadata hello.</span><span class="sxs-lookup"><span data-stu-id="43954-137">Enter this connection string in hello cscfg file in both hello **SplitMergeWeb** and **SplitMergeWorker** role sections in hello ElasticScaleMetadata setting.</span></span>
5. <span data-ttu-id="43954-138">Para Olá **SplitMergeWorker** função, digite um armazenamento de tooAzure de cadeia de caracteres de conexão válida para Olá **WorkerRoleSynchronizationStorageAccountConnectionString** configuração.</span><span class="sxs-lookup"><span data-stu-id="43954-138">For hello **SplitMergeWorker** role, enter a valid connection string tooAzure storage for hello **WorkerRoleSynchronizationStorageAccountConnectionString** setting.</span></span>

### <a name="configure-security"></a><span data-ttu-id="43954-139">Configurar a segurança</span><span class="sxs-lookup"><span data-stu-id="43954-139">Configure security</span></span>
<span data-ttu-id="43954-140">Para instruções detalhadas tooconfigure Olá a segurança do serviço de hello, consulte toohello [configuração de segurança de divisão mesclagem](sql-database-elastic-scale-split-merge-security-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="43954-140">For detailed instructions tooconfigure hello security of hello service, refer toohello [Split-Merge security configuration](sql-database-elastic-scale-split-merge-security-configuration.md).</span></span>

<span data-ttu-id="43954-141">Para fins de saudação de uma implantação de teste simples para este tutorial, um conjunto mínimo de configuração etapas serão executadas tooget serviço de saudação em funcionamento.</span><span class="sxs-lookup"><span data-stu-id="43954-141">For hello purposes of a simple test deployment for this tutorial, a minimal set of configuration steps will be performed tooget hello service up and running.</span></span> <span data-ttu-id="43954-142">Essas etapas habilitam apenas Olá uma máquina/conta executá-los toocommunicate com o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="43954-142">These steps enable only hello one machine/account executing them toocommunicate with hello service.</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="43954-143">Crie um certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="43954-143">Create a self-signed certificate</span></span>
<span data-ttu-id="43954-144">Criar um novo diretório e de saudação de executar esse diretório usando o comando a seguir um [Prompt de comando do desenvolvedor para o Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) janela:</span><span class="sxs-lookup"><span data-stu-id="43954-144">Create a new directory and from this directory execute hello following command using a [Developer Command Prompt for Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) window:</span></span>

   ```
    makecert ^
    -n "CN=*.cloudapp.net" ^
    -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2" ^
    -a sha1 -len 2048 ^
    -sr currentuser -ss root ^
    -sv MyCert.pvk MyCert.cer
   ```

<span data-ttu-id="43954-145">Você será solicitado para uma chave privada do tooprotect Olá de senha.</span><span class="sxs-lookup"><span data-stu-id="43954-145">You are asked for a password tooprotect hello private key.</span></span> <span data-ttu-id="43954-146">Digite uma senha forte e confirme-a.</span><span class="sxs-lookup"><span data-stu-id="43954-146">Enter a strong password and confirm it.</span></span> <span data-ttu-id="43954-147">Você será solicitado para Olá senha toobe usado mais uma vez depois disso.</span><span class="sxs-lookup"><span data-stu-id="43954-147">You are then prompted for hello password toobe used once more after that.</span></span> <span data-ttu-id="43954-148">Clique em **Sim** em Olá final tooimport-toohello repositório de raiz de autoridades de certificação confiável.</span><span class="sxs-lookup"><span data-stu-id="43954-148">Click **Yes** at hello end tooimport it toohello Trusted Certification Authorities Root store.</span></span>

### <a name="create-a-pfx-file"></a><span data-ttu-id="43954-149">Criar um arquivo PFX</span><span class="sxs-lookup"><span data-stu-id="43954-149">Create a PFX file</span></span>
<span data-ttu-id="43954-150">Executar Olá após o comando Olá mesma janela onde makecert foi executado; Use Olá mesma senha que você toocreate usado Olá certificado:</span><span class="sxs-lookup"><span data-stu-id="43954-150">Execute hello following command from hello same window where makecert was executed; use hello same password that you used toocreate hello certificate:</span></span>

    pvk2pfx -pvk MyCert.pvk -spc MyCert.cer -pfx MyCert.pfx -pi <password>

### <a name="import-hello-client-certificate-into-hello-personal-store"></a><span data-ttu-id="43954-151">Importe o certificado de cliente de saudação no repositório pessoal Olá</span><span class="sxs-lookup"><span data-stu-id="43954-151">Import hello client certificate into hello personal store</span></span>
1. <span data-ttu-id="43954-152">No Windows Explorer, clique duas vezes em **Mycert.pfx**.</span><span class="sxs-lookup"><span data-stu-id="43954-152">In Windows Explorer, double-click **MyCert.pfx**.</span></span>
2. <span data-ttu-id="43954-153">Em Olá **Assistente de importação de certificado** selecione **usuário atual** e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="43954-153">In hello **Certificate Import Wizard** select **Current User** and click **Next**.</span></span>
3. <span data-ttu-id="43954-154">Verifique o caminho do arquivo hello e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="43954-154">Confirm hello file path and click **Next**.</span></span>
4. <span data-ttu-id="43954-155">Senha do tipo hello, deixe **incluem todas as propriedades estendidas** marcada e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="43954-155">Type hello password, leave **Include all extended properties** checked and click **Next**.</span></span>
5. <span data-ttu-id="43954-156">Deixe **repositório de certificados automaticamente Olá [...]**  marcada e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="43954-156">Leave **Automatically select hello certificate store[…]** checked and click **Next**.</span></span>
6. <span data-ttu-id="43954-157">Clique em **Concluir** e em **OK**.</span><span class="sxs-lookup"><span data-stu-id="43954-157">Click **Finish** and **OK**.</span></span>

### <a name="upload-hello-pfx-file-toohello-cloud-service"></a><span data-ttu-id="43954-158">Carregar o serviço de nuvem do hello PFX arquivo toohello</span><span class="sxs-lookup"><span data-stu-id="43954-158">Upload hello PFX file toohello cloud service</span></span>
1. <span data-ttu-id="43954-159">Vá toohello [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="43954-159">Go toohello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="43954-160">Selecione os **Serviços de nuvem**.</span><span class="sxs-lookup"><span data-stu-id="43954-160">Select **Cloud Services**.</span></span>
3. <span data-ttu-id="43954-161">Selecione o serviço de nuvem de saudação criado anteriormente para o serviço de divisão/mesclagem hello.</span><span class="sxs-lookup"><span data-stu-id="43954-161">Select hello cloud service you created above for hello Split/Merge service.</span></span>
4. <span data-ttu-id="43954-162">Clique em **certificados** no menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="43954-162">Click **Certificates** on hello top menu.</span></span>
5. <span data-ttu-id="43954-163">Clique em **carregar** na barra inferior de saudação.</span><span class="sxs-lookup"><span data-stu-id="43954-163">Click **Upload** in hello bottom bar.</span></span>
6. <span data-ttu-id="43954-164">Selecione o arquivo PFX de saudação e digite Olá senha acima.</span><span class="sxs-lookup"><span data-stu-id="43954-164">Select hello PFX file and enter hello same password as above.</span></span>
7. <span data-ttu-id="43954-165">Depois de concluído, copie impressão digital do certificado Olá da nova entrada na lista de saudação de hello.</span><span class="sxs-lookup"><span data-stu-id="43954-165">Once completed, copy hello certificate thumbprint from hello new entry in hello list.</span></span>

### <a name="update-hello-service-configuration-file"></a><span data-ttu-id="43954-166">Atualizar o arquivo de configuração de serviço Olá</span><span class="sxs-lookup"><span data-stu-id="43954-166">Update hello service configuration file</span></span>
<span data-ttu-id="43954-167">Cole a impressão digital do certificado Olá copiado acima em seu atributo/valor de impressão digital Olá dessas configurações.</span><span class="sxs-lookup"><span data-stu-id="43954-167">Paste hello certificate thumbprint copied above into hello thumbprint/value attribute of these settings.</span></span>
<span data-ttu-id="43954-168">Olá função de trabalho:</span><span class="sxs-lookup"><span data-stu-id="43954-168">For hello worker role:</span></span>
   ```
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

<span data-ttu-id="43954-169">Para função de web hello:</span><span class="sxs-lookup"><span data-stu-id="43954-169">For hello web role:</span></span>

   ```
    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />
    <Setting name="AllowedClientCertificateThumbprints" value="" />
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

<span data-ttu-id="43954-170">Observe que, para implantações de produção certificados separados devem ser usados para Olá autoridade de certificação para criptografia, Olá certificado de servidor e certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="43954-170">Please note that for production deployments separate certificates should be used for hello CA, for encryption, hello Server certificate and client certificates.</span></span> <span data-ttu-id="43954-171">Para obter instruções detalhadas sobre isso, consulte a [Configuração de segurança](sql-database-elastic-scale-split-merge-security-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="43954-171">For detailed instructions on this, see [Security Configuration](sql-database-elastic-scale-split-merge-security-configuration.md).</span></span>

## <a name="deploy-your-service"></a><span data-ttu-id="43954-172">Implantar o serviço</span><span class="sxs-lookup"><span data-stu-id="43954-172">Deploy your service</span></span>
1. <span data-ttu-id="43954-173">Vá toohello [portal do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="43954-173">Go toohello [Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="43954-174">Clique em Olá **serviços de nuvem** Olá esquerda e selecione o serviço de nuvem Olá que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="43954-174">Click hello **Cloud Services** tab on hello left, and select hello cloud service that you created earlier.</span></span>
3. <span data-ttu-id="43954-175">Clique em **Painel**.</span><span class="sxs-lookup"><span data-stu-id="43954-175">Click **Dashboard**.</span></span>
4. <span data-ttu-id="43954-176">Escolha Olá ambiente de preparo, e clique em **carregar uma nova implantação de preparo**.</span><span class="sxs-lookup"><span data-stu-id="43954-176">Choose hello staging environment, then click **Upload a new staging deployment**.</span></span>
   
   ![Staging][3]
5. <span data-ttu-id="43954-178">Na caixa de diálogo hello, digite um rótulo de implantação.</span><span class="sxs-lookup"><span data-stu-id="43954-178">In hello dialog box, enter a deployment label.</span></span> <span data-ttu-id="43954-179">Para 'Pacote' e 'Configuration', clique em 'Do Local' e escolha Olá **SplitMergeService.cspkg** de arquivo e o arquivo. cscfg configurados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="43954-179">For both 'Package' and 'Configuration', click 'From Local' and choose hello **SplitMergeService.cspkg** file and your .cscfg file that you configured earlier.</span></span>
6. <span data-ttu-id="43954-180">Verifique se essa caixa de seleção Olá **implantar mesmo se uma ou mais funções contiverem uma única instância** é verificada.</span><span class="sxs-lookup"><span data-stu-id="43954-180">Ensure that hello checkbox labeled **Deploy even if one or more roles contain a single instance** is checked.</span></span>
7. <span data-ttu-id="43954-181">Pressione o botão de escala de saudação na implantação de Olá Olá inferior direita toobegin.</span><span class="sxs-lookup"><span data-stu-id="43954-181">Hit hello tick button in hello bottom right toobegin hello deployment.</span></span> <span data-ttu-id="43954-182">Espera que ele tootake toocomplete de alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="43954-182">Expect it tootake a few minutes toocomplete.</span></span>

   ![Carregar][4]

## <a name="troubleshoot-hello-deployment"></a><span data-ttu-id="43954-184">Solucionar problemas de implantação de saudação</span><span class="sxs-lookup"><span data-stu-id="43954-184">Troubleshoot hello deployment</span></span>
<span data-ttu-id="43954-185">Se sua função web falhar toocome on-line, provavelmente é um problema com a configuração de segurança hello.</span><span class="sxs-lookup"><span data-stu-id="43954-185">If your web role fails toocome online, it is likely a problem with hello security configuration.</span></span> <span data-ttu-id="43954-186">Verifique que Olá que SSL configurado conforme descrito acima.</span><span class="sxs-lookup"><span data-stu-id="43954-186">Check that hello SSL is configured as described above.</span></span>

<span data-ttu-id="43954-187">Se sua função de trabalho falha toocome online, mas sua função web for bem-sucedida, provavelmente é um problema de conexão de banco de dados de status de toohello que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="43954-187">If your worker role fails toocome online, but your web role succeeds, it is most likely a problem connecting toohello status database that you created earlier.</span></span>

* <span data-ttu-id="43954-188">Certifique-se de que a cadeia de caracteres de conexão de saudação em seu. cscfg é precisa.</span><span class="sxs-lookup"><span data-stu-id="43954-188">Make sure that hello connection string in your .cscfg is accurate.</span></span>
* <span data-ttu-id="43954-189">Verificação de banco de dados e servidor de saudação existem e Olá identificação de usuário e senha estão corretos.</span><span class="sxs-lookup"><span data-stu-id="43954-189">Check that hello server and database exist, and that hello user id and password are correct.</span></span>
* <span data-ttu-id="43954-190">Para o banco de dados de SQL do Azure, cadeia de caracteres de conexão Olá deve estar Olá formato:</span><span class="sxs-lookup"><span data-stu-id="43954-190">For Azure SQL DB, hello connection string should be of hello form:</span></span>

   ```  
   Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
   ```

* <span data-ttu-id="43954-191">Certifique-se de que esse nome de servidor de saudação não começa com **https://**.</span><span class="sxs-lookup"><span data-stu-id="43954-191">Ensure that hello server name does not begin with **https://**.</span></span>
* <span data-ttu-id="43954-192">Certifique-se de que o servidor de banco de dados de SQL do Azure permite que serviços do Azure tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="43954-192">Ensure that your Azure SQL DB server allows Azure Services tooconnect tooit.</span></span> <span data-ttu-id="43954-193">toodo isso, abra https://manage.windowsazure.com, clique "Bancos de dados SQL" em saudação à esquerda, clique em "Servidores" na parte superior do hello e selecione o servidor.</span><span class="sxs-lookup"><span data-stu-id="43954-193">toodo this, open https://manage.windowsazure.com, click “SQL Databases” on hello left, click “Servers” at hello top, and select your server.</span></span> <span data-ttu-id="43954-194">Clique em **configurar** em Olá principais e certifique-se de que Olá **serviços do Azure** configuração é definida muito "Sim".</span><span class="sxs-lookup"><span data-stu-id="43954-194">Click **Configure** at hello top and ensure that hello **Azure Services** setting is set too“Yes”.</span></span> <span data-ttu-id="43954-195">(Consulte os pré-requisitos de saudação seção na parte superior da saudação deste artigo).</span><span class="sxs-lookup"><span data-stu-id="43954-195">(See hello Prerequisites section at hello top of this article).</span></span>

## <a name="test-hello-service-deployment"></a><span data-ttu-id="43954-196">Testar a implantação do serviço Olá</span><span class="sxs-lookup"><span data-stu-id="43954-196">Test hello service deployment</span></span>
### <a name="connect-with-a-web-browser"></a><span data-ttu-id="43954-197">Conectar-se com um navegador da Web</span><span class="sxs-lookup"><span data-stu-id="43954-197">Connect with a web browser</span></span>
<span data-ttu-id="43954-198">Determine o ponto de extremidade de web de saudação do seu serviço de divisão de mesclagem.</span><span class="sxs-lookup"><span data-stu-id="43954-198">Determine hello web endpoint of your Split-Merge service.</span></span> <span data-ttu-id="43954-199">Você pode encontrá-lo em Olá Portal clássico do Azure por vai toohello **painel** de seu serviço de nuvem e olhando na **URL do Site** Olá direita.</span><span class="sxs-lookup"><span data-stu-id="43954-199">You can find this in hello Azure Classic Portal by going toohello **Dashboard** of your cloud service and looking under **Site URL** on hello right side.</span></span> <span data-ttu-id="43954-200">Substituir **http://** com **https://** desde que as configurações de segurança de saudação desabilitar ponto de extremidade de saudação HTTP.</span><span class="sxs-lookup"><span data-stu-id="43954-200">Replace **http://** with **https://** since hello default security settings disable hello HTTP endpoint.</span></span> <span data-ttu-id="43954-201">Página de saudação de carga para esta URL no seu navegador.</span><span class="sxs-lookup"><span data-stu-id="43954-201">Load hello page for this URL into your browser.</span></span>

### <a name="test-with-powershell-scripts"></a><span data-ttu-id="43954-202">Testes com scripts do PowerShell</span><span class="sxs-lookup"><span data-stu-id="43954-202">Test with PowerShell scripts</span></span>
<span data-ttu-id="43954-203">implantação de saudação e seu ambiente podem ser testados executando scripts do PowerShell de exemplo hello incluído.</span><span class="sxs-lookup"><span data-stu-id="43954-203">hello deployment and your environment can be tested by running hello included sample PowerShell scripts.</span></span>

<span data-ttu-id="43954-204">arquivos de script Hello incluídos são:</span><span class="sxs-lookup"><span data-stu-id="43954-204">hello script files included are:</span></span>

1. <span data-ttu-id="43954-205">**SetupSampleSplitMergeEnvironment.ps1** - configura uma camada de dados de teste para Divisão/Mesclagem (consulte a tabela abaixo para uma descrição detalhada)</span><span class="sxs-lookup"><span data-stu-id="43954-205">**SetupSampleSplitMergeEnvironment.ps1** - sets up a test data tier for Split/Merge (see table below for detailed description)</span></span>
2. <span data-ttu-id="43954-206">**ExecuteSampleSplitMerge.ps1** -executa operações de teste no teste de saudação da camada de dados (consulte a tabela abaixo para obter a descrição detalhada)</span><span class="sxs-lookup"><span data-stu-id="43954-206">**ExecuteSampleSplitMerge.ps1** - executes test operations on hello test data tier (see table below for detailed description)</span></span>
3. <span data-ttu-id="43954-207">**GetMappings.ps1** - nível superior que imprime o estado atual de saudação do mapeamentos de fragmento Olá script de exemplo.</span><span class="sxs-lookup"><span data-stu-id="43954-207">**GetMappings.ps1** - top-level sample script that prints out hello current state of hello shard mappings.</span></span>
4. <span data-ttu-id="43954-208">**ShardManagement.psm1** -script auxiliar que encapsula Olá ShardManagement API</span><span class="sxs-lookup"><span data-stu-id="43954-208">**ShardManagement.psm1**  - helper script that wraps hello ShardManagement API</span></span>
5. <span data-ttu-id="43954-209">**SqlDatabaseHelpers.psm1** – o script auxiliar para criar e gerenciar bancos de dados SQL</span><span class="sxs-lookup"><span data-stu-id="43954-209">**SqlDatabaseHelpers.psm1** - helper script for creating and managing SQL databases</span></span>
   
   <table style="width:100%">
     <tr>
       <th><span data-ttu-id="43954-210">Arquivo do PowerShell</span><span class="sxs-lookup"><span data-stu-id="43954-210">PowerShell file</span></span></th>
       <th><span data-ttu-id="43954-211">Etapas</span><span class="sxs-lookup"><span data-stu-id="43954-211">Steps</span></span></th>
     </tr>
     <tr>
       <th rowspan="5"><span data-ttu-id="43954-212">SetupSampleSplitMergeEnvironment.ps1</span><span class="sxs-lookup"><span data-stu-id="43954-212">SetupSampleSplitMergeEnvironment.ps1</span></span></th>
       <td>1.    <span data-ttu-id="43954-213">Cria um banco de dados do gerenciador de mapa do fragmento</span><span class="sxs-lookup"><span data-stu-id="43954-213">Creates a shard map manager database</span></span></td>
     </tr>
     <tr>
       <td>2.    <span data-ttu-id="43954-214">Cria 2 bancos de dados do fragmento.</span><span class="sxs-lookup"><span data-stu-id="43954-214">Creates 2 shard databases.</span></span>
     </tr>
     <tr>
       <td>3.    <span data-ttu-id="43954-215">Cria um mapa do fragmento para esses bancos de dados (exclui quaisquer mapas do fragmento existentes nesses bancos de dados).</span><span class="sxs-lookup"><span data-stu-id="43954-215">Creates a shard map for those database (deletes any existing shard maps on those databases).</span></span> </td>
     </tr>
     <tr>
       <td>4.    <span data-ttu-id="43954-216">Cria uma tabela de exemplo pequeno em ambos os fragmentos hello e preenche a tabela Olá em um dos fragmentos de saudação.</span><span class="sxs-lookup"><span data-stu-id="43954-216">Creates a small sample table in both hello shards, and populates hello table in one of hello shards.</span></span></td>
     </tr>
     <tr>
       <td>5.    <span data-ttu-id="43954-217">Declara hello SchemaInfo para a tabela fragmentada hello.</span><span class="sxs-lookup"><span data-stu-id="43954-217">Declares hello SchemaInfo for hello sharded table.</span></span></td>
     </tr>
   </table>
   <table style="width:100%">
     <tr>
       <th><span data-ttu-id="43954-218">Arquivo do PowerShell</span><span class="sxs-lookup"><span data-stu-id="43954-218">PowerShell file</span></span></th>
       <th><span data-ttu-id="43954-219">Etapas</span><span class="sxs-lookup"><span data-stu-id="43954-219">Steps</span></span></th>
     </tr>
   <tr>
       <th rowspan="4"><span data-ttu-id="43954-220">ExecuteSampleSplitMerge.ps1</span><span class="sxs-lookup"><span data-stu-id="43954-220">ExecuteSampleSplitMerge.ps1</span></span> </th>
       <td>1.    <span data-ttu-id="43954-221">Envia um divisão solicitação toohello divisão mesclagem serviço web front-end, que divide os dados de saudação metade do segundo-fragmento primeiro toohello de fragmento hello.</span><span class="sxs-lookup"><span data-stu-id="43954-221">Sends a split request toohello Split-Merge Service web frontend, which splits half hello data from hello first shard toohello second shard.</span></span></td>
     </tr>
     <tr>
       <td>2.    <span data-ttu-id="43954-222">Pesquisas Olá web front-end para Olá dividir o status da solicitação e aguarda até que a solicitação de saudação é concluída.</span><span class="sxs-lookup"><span data-stu-id="43954-222">Polls hello web frontend for hello split request status and waits until hello request completes.</span></span></td>
     </tr>
     <tr>
       <td>3.    <span data-ttu-id="43954-223">Envia um mesclagem solicitação toohello divisão mesclagem serviço web front-end, que move dados de saudação do primeiro-fragmento segundo toohello voltar de fragmento hello.</span><span class="sxs-lookup"><span data-stu-id="43954-223">Sends a merge request toohello Split-Merge Service web frontend, which moves hello data from hello second shard back toohello first shard.</span></span></td>
     </tr>
     <tr>
       <td>4.    <span data-ttu-id="43954-224">Olá sondagens web front-end para o status da solicitação de mesclagem hello e aguarda até que a solicitação de saudação é concluída.</span><span class="sxs-lookup"><span data-stu-id="43954-224">Polls hello web frontend for hello merge request status and waits until hello request completes.</span></span></td>
     </tr>
   </table>
   
## <a name="use-powershell-tooverify-your-deployment"></a><span data-ttu-id="43954-225">Use o PowerShell tooverify sua implantação</span><span class="sxs-lookup"><span data-stu-id="43954-225">Use PowerShell tooverify your deployment</span></span>
1. <span data-ttu-id="43954-226">Abra uma nova janela do PowerShell e navegue toohello diretório onde você baixou o pacote de divisão mesclagem hello e, em seguida, navegue até o diretório de "powershell" hello.</span><span class="sxs-lookup"><span data-stu-id="43954-226">Open a new PowerShell window and navigate toohello directory where you downloaded hello Split-Merge package, and then navigate into hello “powershell” directory.</span></span>
2. <span data-ttu-id="43954-227">Criar um servidor de banco de dados do SQL Azure (ou escolha um servidor existente) onde Gerenciador do mapa de fragmentos hello e fragmentos serão criados.</span><span class="sxs-lookup"><span data-stu-id="43954-227">Create an Azure SQL database server (or choose an existing server) where hello shard map manager and shards will be created.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="43954-228">Olá SetupSampleSplitMergeEnvironment.ps1 script cria esses bancos de dados em Olá mesmo servidor pelo script do hello tookeep padrão simple.</span><span class="sxs-lookup"><span data-stu-id="43954-228">hello SetupSampleSplitMergeEnvironment.ps1 script creates all these databases on hello same server by default tookeep hello script simple.</span></span> <span data-ttu-id="43954-229">Isso não é uma restrição de saudação serviço de divisão de mesclagem em si.</span><span class="sxs-lookup"><span data-stu-id="43954-229">This is not a restriction of hello Split-Merge Service itself.</span></span>
   >
   
   <span data-ttu-id="43954-230">Um logon de autenticação do SQL com toohello de acesso de leitura/gravação, que bancos de dados serão necessários para hello toomove dados do serviço de divisão de mesclagem e o mapa de fragmento de saudação de atualização.</span><span class="sxs-lookup"><span data-stu-id="43954-230">A SQL authentication login with read/write access toohello DBs will be needed for hello Split-Merge service toomove data and update hello shard map.</span></span> <span data-ttu-id="43954-231">Como Olá serviço de divisão de mesclagem é executado na nuvem Olá, ele não atualmente suporta autenticação integrada.</span><span class="sxs-lookup"><span data-stu-id="43954-231">Since hello Split-Merge Service runs in hello cloud, it does not currently support Integrated Authentication.</span></span>
   
   <span data-ttu-id="43954-232">Certifique-se de saudação do Azure SQL server está configurada tooallow acesso do endereço IP de saudação da máquina Olá execução desses scripts.</span><span class="sxs-lookup"><span data-stu-id="43954-232">Make sure hello Azure SQL server is configured tooallow access from hello IP address of hello machine running these scripts.</span></span> <span data-ttu-id="43954-233">Você pode encontrar essa configuração em um servidor do SQL Azure Olá / configuração / endereços IP permitidos.</span><span class="sxs-lookup"><span data-stu-id="43954-233">You can find this setting under hello Azure SQL server / configuration / allowed IP addresses.</span></span>
3. <span data-ttu-id="43954-234">Execute o ambiente de exemplo hello SetupSampleSplitMergeEnvironment.ps1 script toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="43954-234">Execute hello SetupSampleSplitMergeEnvironment.ps1 script toocreate hello sample environment.</span></span>
   
   <span data-ttu-id="43954-235">Executar esse script irá apagar os dados de gerenciamento de mapa de fragmento existentes estruturas no banco de dados do fragmento mapa manager hello e fragmentos de saudação.</span><span class="sxs-lookup"><span data-stu-id="43954-235">Running this script will wipe out any existing shard map management data structures on hello shard map manager database and hello shards.</span></span> <span data-ttu-id="43954-236">Talvez seja útil toorerun script de saudação se desejar que o mapa do fragmento Olá toore inicializar ou fragmentos.</span><span class="sxs-lookup"><span data-stu-id="43954-236">It may be useful toorerun hello script if you wish toore-initialize hello shard map or shards.</span></span>
   
   <span data-ttu-id="43954-237">Linha de comando de exemplo:</span><span class="sxs-lookup"><span data-stu-id="43954-237">Sample command line:</span></span>

   ```   
     .\SetupSampleSplitMergeEnvironment.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'
   ```      
4. <span data-ttu-id="43954-238">Execute Olá Getmappings.ps1 tooview Olá mapeamentos de script que existem atualmente no ambiente de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="43954-238">Execute hello Getmappings.ps1 script tooview hello mappings that currently exist in hello sample environment.</span></span>
   
   ```
     .\GetMappings.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'

   ```         
5. <span data-ttu-id="43954-239">Execute Olá ExecuteSampleSplitMerge.ps1 script tooexecute uma operação de divisão (mover dados de saudação metade no segundo-fragmento primeiro toohello de fragmento Olá) e, em seguida, uma operação de mesclagem (movimentação de dados Olá novamente no fragmento primeiro Olá).</span><span class="sxs-lookup"><span data-stu-id="43954-239">Execute hello ExecuteSampleSplitMerge.ps1 script tooexecute a split operation (moving half hello data on hello first shard toohello second shard) and then a merge operation (moving hello data back onto hello first shard).</span></span> <span data-ttu-id="43954-240">Se você configurou o SSL e o ponto de extremidade http Olá esquerdo desabilitado, certifique-se de que você use o ponto de extremidade do hello https://.</span><span class="sxs-lookup"><span data-stu-id="43954-240">If you configured SSL and left hello http endpoint disabled, ensure that you use hello https:// endpoint instead.</span></span>
   
   <span data-ttu-id="43954-241">Linha de comando de exemplo:</span><span class="sxs-lookup"><span data-stu-id="43954-241">Sample command line:</span></span>

   ```   
     .\ExecuteSampleSplitMerge.ps1
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net' 
         -SplitMergeServiceEndpoint 'https://mysplitmergeservice.cloudapp.net' 
         -CertificateThumbprint '0123456789abcdef0123456789abcdef01234567'
   ```      
   
   <span data-ttu-id="43954-242">Se você receber Olá erro abaixo, provavelmente é um problema com o certificado do ponto de extremidade seu Web.</span><span class="sxs-lookup"><span data-stu-id="43954-242">If you receive hello below error, it is most likely a problem with your Web endpoint’s certificate.</span></span> <span data-ttu-id="43954-243">Tente conectar-se o ponto de extremidade de Web toohello com seu navegador favorito e verifique se há um erro de certificado.</span><span class="sxs-lookup"><span data-stu-id="43954-243">Try connecting toohello Web endpoint with your favorite Web browser and check if there is a certificate error.</span></span>
   
     ```
     Invoke-WebRequest : hello underlying connection was closed: Could not establish trust relationship for hello SSL/TLSsecure channel.
     ```
   
   <span data-ttu-id="43954-244">Se tiver êxito, saída de hello deve ter a aparência Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="43954-244">If it succeeded, hello output should look like hello below:</span></span>
   
   ```
   > .\ExecuteSampleSplitMerge.ps1 -UserName 'mysqluser' -Password 'MySqlPassw0rd' -ShardMapManagerServerName 'abcdefghij.database.windows.net' -SplitMergeServiceEndpoint 'http://mysplitmergeservice.cloudapp.net' -CertificateThumbprint 0123456789abcdef0123456789abcdef01234567
   > Sending split request
   > Began split operation with id dc68dfa0-e22b-4823-886a-9bdc903c80f3
   > Polling split-merge request status. Press Ctrl-C tooend
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Waiting for reference tables copy     completion.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing hello request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > Sending merge request
   > Began merge operation with id 6ffc308f-d006-466b-b24e-857242ec5f66
   > Polling request status. Press Ctrl-C tooend
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing hello request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > 
   ```
6. <span data-ttu-id="43954-245">Experimente outros tipos de dados!</span><span class="sxs-lookup"><span data-stu-id="43954-245">Experiment with other data types!</span></span> <span data-ttu-id="43954-246">Todos esses scripts levar um parâmetro - ShardKeyType opcional que permite que o tipo de chave de saudação do toospecify.</span><span class="sxs-lookup"><span data-stu-id="43954-246">All of these scripts take an optional -ShardKeyType parameter that allows you toospecify hello key type.</span></span> <span data-ttu-id="43954-247">padrão de saudação é Int32, mas você também pode especificar Int64, Guid ou Binary.</span><span class="sxs-lookup"><span data-stu-id="43954-247">hello default is Int32, but you can also specify Int64, Guid, or Binary.</span></span>

## <a name="create-requests"></a><span data-ttu-id="43954-248">Criar solicitações</span><span class="sxs-lookup"><span data-stu-id="43954-248">Create requests</span></span>
<span data-ttu-id="43954-249">serviço de saudação pode ser usado por meio da interface da web hello ou importando e usando o módulo de PowerShell SplitMerge.psm1 Olá que enviará solicitações por meio da função de web hello.</span><span class="sxs-lookup"><span data-stu-id="43954-249">hello service can be used either by using hello web UI or by importing and using hello SplitMerge.psm1 PowerShell module which will submit your requests through hello web role.</span></span>

<span data-ttu-id="43954-250">serviço de saudação pode mover dados em tabelas fragmentadas e tabelas de referência.</span><span class="sxs-lookup"><span data-stu-id="43954-250">hello service can move data in both sharded tables and reference tables.</span></span> <span data-ttu-id="43954-251">Uma tabela fragmentada possui uma coluna de chave de fragmentação e tem diferentes dados de linha em cada fragmento.</span><span class="sxs-lookup"><span data-stu-id="43954-251">A sharded table has a sharding key column and has different row data on each shard.</span></span> <span data-ttu-id="43954-252">Uma tabela de referência não é fragmentada para que ele contém Olá mesmo linhas de dados em cada fragmento.</span><span class="sxs-lookup"><span data-stu-id="43954-252">A reference table is not sharded so it contains hello same row data on every shard.</span></span> <span data-ttu-id="43954-253">Tabelas de referência são úteis para dados que não são alterados com frequência e tooJOIN usado com tabelas fragmentadas em consultas.</span><span class="sxs-lookup"><span data-stu-id="43954-253">Reference tables are useful for data that does not change often and is used tooJOIN with sharded tables in queries.</span></span>

<span data-ttu-id="43954-254">Em ordem tooperform uma operação de mesclagem de divisão, você deve declarar tabelas fragmentadas hello e tabelas de referência que você deseja toohave movido.</span><span class="sxs-lookup"><span data-stu-id="43954-254">In order tooperform a split-merge operation, you must declare hello sharded tables and reference tables that you want toohave moved.</span></span> <span data-ttu-id="43954-255">Isso é feito com hello **SchemaInfo** API.</span><span class="sxs-lookup"><span data-stu-id="43954-255">This is accomplished with hello **SchemaInfo** API.</span></span> <span data-ttu-id="43954-256">Esta API está em Olá **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** namespace.</span><span class="sxs-lookup"><span data-stu-id="43954-256">This API is in hello **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** namespace.</span></span>

1. <span data-ttu-id="43954-257">Para cada tabela fragmentada, crie um **ShardedTableInfo** que descreve o nome do esquema da tabela de saudação do pai do objeto (opcional, padrão é muito "dbo"), Olá nome da tabela e Olá nome da coluna na tabela que contém a chave de fragmentação hello.</span><span class="sxs-lookup"><span data-stu-id="43954-257">For each sharded table, create a **ShardedTableInfo** object describing hello table’s parent schema name (optional, defaults too“dbo”), hello table name, and hello column name in that table that contains hello sharding key.</span></span>
2. <span data-ttu-id="43954-258">Para cada tabela de referência, crie uma **ReferenceTableInfo** que descreve o nome do esquema da tabela de saudação do pai do objeto (opcional, padrão é muito "dbo") e o nome da tabela hello.</span><span class="sxs-lookup"><span data-stu-id="43954-258">For each reference table, create a **ReferenceTableInfo** object describing hello table’s parent schema name (optional, defaults too“dbo”) and hello table name.</span></span>
3. <span data-ttu-id="43954-259">Adicionar Olá acima TableInfo objetos tooa novo **SchemaInfo** objeto.</span><span class="sxs-lookup"><span data-stu-id="43954-259">Add hello above TableInfo objects tooa new **SchemaInfo** object.</span></span>
4. <span data-ttu-id="43954-260">Obter uma referência tooa **ShardMapManager** objeto e chame **GetSchemaInfoCollection**.</span><span class="sxs-lookup"><span data-stu-id="43954-260">Get a reference tooa **ShardMapManager** object, and call **GetSchemaInfoCollection**.</span></span>
5. <span data-ttu-id="43954-261">Adicionar Olá **SchemaInfo** toohello **SchemaInfoCollection**, fornecendo o nome do mapa de fragmentos hello.</span><span class="sxs-lookup"><span data-stu-id="43954-261">Add hello **SchemaInfo** toohello **SchemaInfoCollection**, providing hello shard map name.</span></span>

<span data-ttu-id="43954-262">Um exemplo disso pode ser visto no hello SetupSampleSplitMergeEnvironment.ps1 script.</span><span class="sxs-lookup"><span data-stu-id="43954-262">An example of this can be seen in hello SetupSampleSplitMergeEnvironment.ps1 script.</span></span>

<span data-ttu-id="43954-263">Olá serviço de divisão de mesclagem não criar o banco de dados de destino hello (ou o esquema para todas as tabelas no banco de dados de saudação) para você.</span><span class="sxs-lookup"><span data-stu-id="43954-263">hello Split-Merge service does not create hello target database (or schema for any tables in hello database) for you.</span></span> <span data-ttu-id="43954-264">Eles devem ser pré-criados antes de enviar uma solicitação de serviço toohello.</span><span class="sxs-lookup"><span data-stu-id="43954-264">They must be pre-created before sending a request toohello service.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="43954-265">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="43954-265">Troubleshooting</span></span>
<span data-ttu-id="43954-266">Você pode ver Olá abaixo mensagem ao executar scripts do powershell de exemplo hello:</span><span class="sxs-lookup"><span data-stu-id="43954-266">You may see hello below message when running hello sample powershell scripts:</span></span>

   ```
   Invoke-WebRequest : hello underlying connection was closed: Could not establish trust relationship for hello SSL/TLS secure channel.
   ```

<span data-ttu-id="43954-267">Esse erro significa que o certificado SSL não está corretamente configurado.</span><span class="sxs-lookup"><span data-stu-id="43954-267">This error means that your SSL certificate is not configured correctly.</span></span> <span data-ttu-id="43954-268">Siga as instruções de saudação na seção 'Conectar-se com um navegador da web'.</span><span class="sxs-lookup"><span data-stu-id="43954-268">Please follow hello instructions in section 'Connecting with a web browser'.</span></span>

<span data-ttu-id="43954-269">Se não for possível enviar solicitações, você verá isso:</span><span class="sxs-lookup"><span data-stu-id="43954-269">If you cannot submit requests you may see this:</span></span>

```
[Exception] System.Data.SqlClient.SqlException (0x80131904): Could not find stored procedure 'dbo.InsertRequest'. 
```

<span data-ttu-id="43954-270">Nesse caso, verifique o arquivo de configuração, na configuração de saudação específico para **WorkerRoleSynchronizationStorageAccountConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="43954-270">In this case, check your configuration file, in particular hello setting for **WorkerRoleSynchronizationStorageAccountConnectionString**.</span></span> <span data-ttu-id="43954-271">Esse erro normalmente indica que essa função de trabalho Olá com êxito não foi possível inicializar banco de dados de metadados de saudação no primeiro uso.</span><span class="sxs-lookup"><span data-stu-id="43954-271">This error typically indicates that hello worker role could not successfully initialize hello metadata database on first use.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/allowed-services.png
[2]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/manage.png
[3]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/staging.png
[4]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/upload.png
[5]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/storage.png

