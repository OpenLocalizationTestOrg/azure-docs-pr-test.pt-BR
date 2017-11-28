---
title: "aaaPublish um contêiner do Docker usando hello Kit de ferramentas do Azure para IntelliJ | Microsoft Docs"
description: "Saiba como toopublish uma tooMicrosoft de aplicativo web do Azure como um contêiner do Docker usando hello o Kit de ferramentas do Azure para IntelliJ."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: bee94cb269ea707ae7ad55232e23e915aec48c34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-intellij"></a><span data-ttu-id="4cb13-103">Publicar um aplicativo web como um contêiner do Docker usando Olá Kit de ferramentas do Azure para IntelliJ</span><span class="sxs-lookup"><span data-stu-id="4cb13-103">Publish a web app as a Docker container by using hello Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="4cb13-104">Contêineres do Docker são um método amplamente usado para implantar aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="4cb13-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="4cb13-105">Usando contêineres do Docker, os desenvolvedores podem consolidar todos os seus arquivos de projeto e dependências em um único pacote para o servidor de implantação tooa.</span><span class="sxs-lookup"><span data-stu-id="4cb13-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment tooa server.</span></span> <span data-ttu-id="4cb13-106">Olá Kit de ferramentas do Azure para IntelliJ simplifica esse processo para desenvolvedores de Java adicionando *Publicar como contêiner Docker* recursos para tooMicrosoft de implantação do Azure.</span><span class="sxs-lookup"><span data-stu-id="4cb13-106">hello Azure Toolkit for IntelliJ simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment tooMicrosoft Azure.</span></span> <span data-ttu-id="4cb13-107">Este artigo orienta Olá etapas necessárias toopublish tooAzure seus aplicativos como contêineres do Docker.</span><span class="sxs-lookup"><span data-stu-id="4cb13-107">This article walks you through hello steps required toopublish your applications tooAzure as Docker containers.</span></span>

> [!NOTE]
>
> <span data-ttu-id="4cb13-108">Para obter mais informações sobre o Docker estão disponíveis no hello [site Docker].</span><span class="sxs-lookup"><span data-stu-id="4cb13-108">More information about Docker is available on hello [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="4cb13-109">Publicar seu tooAzure de aplicativo web usando um contêiner do Docker</span><span class="sxs-lookup"><span data-stu-id="4cb13-109">Publish your web app tooAzure by using a Docker container</span></span>

> [!NOTE]
> * <span data-ttu-id="4cb13-110">toopublish seu aplicativo web, você deve criar um artefato pronto para implantação.</span><span class="sxs-lookup"><span data-stu-id="4cb13-110">toopublish your web app, you must create a deployment-ready artifact.</span></span> <span data-ttu-id="4cb13-111">toolearn mais, consulte Olá [informações adicionais sobre como criar artefatos](#artifacts) seção.</span><span class="sxs-lookup"><span data-stu-id="4cb13-111">toolearn more, see hello [Additional information about creating artifacts](#artifacts) section.</span></span>
>
> * <span data-ttu-id="4cb13-112">Depois de concluir o Assistente de implantação Olá pelo menos uma vez, a maioria de suas configurações é usada como padrões quando você executar novamente o Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="4cb13-112">After you have completed hello deployment wizard at least once, most of your settings are used as defaults when you run hello wizard again.</span></span>
>

1. <span data-ttu-id="4cb13-113">Abra seu projeto de aplicativo Web no IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="4cb13-113">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="4cb13-114">Olá toostart **Publicar como contêiner Docker** assistente, faça o seguinte de saudação:</span><span class="sxs-lookup"><span data-stu-id="4cb13-114">toostart hello **Publish as Docker Container** wizard, do either of hello following:</span></span>

   * <span data-ttu-id="4cb13-115">Em Olá **projeto** janela de ferramenta, clique com o botão direito, clique em **Azure**e, em seguida, clique em **Publicar como contêiner Docker**:</span><span class="sxs-lookup"><span data-stu-id="4cb13-115">In hello **Project** tool window, right-click your project, click **Azure**, and then click **Publish as Docker Container**:</span></span>

      ![Olá Publicar como comando contêiner Docker][PUB01]

   * <span data-ttu-id="4cb13-117">Na barra de ferramentas de IntelliJ Olá, clique em Olá **grupo publicar** botão e, em seguida, clique em **Publicar como contêiner Docker**:</span><span class="sxs-lookup"><span data-stu-id="4cb13-117">On hello IntelliJ toolbar, click hello **Publish Group** button, and then click **Publish as Docker Container**:</span></span>

      <span data-ttu-id="4cb13-118">![Olá Publicar como comando contêiner Docker][PUB02]</span><span class="sxs-lookup"><span data-stu-id="4cb13-118">![hello Publish as Docker Container command][PUB02]</span></span>  
    <span data-ttu-id="4cb13-119">Olá **implantar o contêiner do Docker no Azure** assistente é aberto.</span><span class="sxs-lookup"><span data-stu-id="4cb13-119">hello **Deploy Docker Container on Azure** wizard opens.</span></span>

   ![Olá implantar o contêiner do Docker no Assistente do Azure][PUB03]

3. <span data-ttu-id="4cb13-121">Em Olá **digite um nome de imagem, selecione o caminho do artefato hello e verificar um toobe de host do Docker usado** janela, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="4cb13-121">In hello **Type an image name, select hello artifact's path and check a Docker host toobe used** window, do hello following:</span></span> 

   <span data-ttu-id="4cb13-122">a.</span><span class="sxs-lookup"><span data-stu-id="4cb13-122">a.</span></span> <span data-ttu-id="4cb13-123">Em Olá **nome de imagem do Docker** , digite um nome exclusivo para o host do Docker.</span><span class="sxs-lookup"><span data-stu-id="4cb13-123">In hello **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="4cb13-124">(Olá criará automaticamente um nome, mas você pode modificá-la.)</span><span class="sxs-lookup"><span data-stu-id="4cb13-124">(hello wizard automatically creates a name, but you can modify it.)</span></span> 

   <span data-ttu-id="4cb13-125">b.</span><span class="sxs-lookup"><span data-stu-id="4cb13-125">b.</span></span> <span data-ttu-id="4cb13-126">Olá **Hosts** área exibe os hosts de Docker que você criou.</span><span class="sxs-lookup"><span data-stu-id="4cb13-126">hello **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="4cb13-127">Siga um destes procedimentos hello:</span><span class="sxs-lookup"><span data-stu-id="4cb13-127">Do either of hello following:</span></span> 
      * <span data-ttu-id="4cb13-128">Se você tiver um host Docker existente, você pode implantar seu tooit de aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="4cb13-128">If you have an existing Docker host, you can deploy your web app tooit.</span></span>
      * <span data-ttu-id="4cb13-129">Clique em toocreate um host Docker, sinal de adição verde hello (**+**).</span><span class="sxs-lookup"><span data-stu-id="4cb13-129">toocreate a Docker host, click hello green plus sign (**+**).</span></span>  
       <span data-ttu-id="4cb13-130">Olá **criar Host do Docker** caixa de diálogo é aberta.</span><span class="sxs-lookup"><span data-stu-id="4cb13-130">hello **Create Docker Host** dialog box opens.</span></span> 

      ![Assistente para Implantar o Contêiner do Docker no Azure][PUB04a]

4. <span data-ttu-id="4cb13-132">Em Olá **configurar nova máquina de virtual Olá** janela, forneça Olá seguintes informações sobre o host do Docker.</span><span class="sxs-lookup"><span data-stu-id="4cb13-132">In hello **Configure hello new virtual machine** window, provide hello following information about your Docker host.</span></span> <span data-ttu-id="4cb13-133">(Assistente de saudação gera automaticamente a maioria das informações de saudação para você, mas você pode modificar qualquer um deles.)</span><span class="sxs-lookup"><span data-stu-id="4cb13-133">(hello wizard automatically generates most of hello information for you, but you can modify any of them.)</span></span> 

   <span data-ttu-id="4cb13-134">a.</span><span class="sxs-lookup"><span data-stu-id="4cb13-134">a.</span></span> <span data-ttu-id="4cb13-135">Em Olá **nome** , digite um nome exclusivo para o host do Docker hello.</span><span class="sxs-lookup"><span data-stu-id="4cb13-135">In hello **Name** box, enter a unique name for hello Docker host.</span></span> <span data-ttu-id="4cb13-136">(É não Olá mesmo Olá nome de imagem do Docker que você especificou anteriormente.)</span><span class="sxs-lookup"><span data-stu-id="4cb13-136">(It is not hello same as hello Docker image name that you specified earlier.)</span></span> 
    
   <span data-ttu-id="4cb13-137">b.</span><span class="sxs-lookup"><span data-stu-id="4cb13-137">b.</span></span> <span data-ttu-id="4cb13-138">Em Olá **assinatura** , digite Olá assinatura do Azure que você usa para o host.</span><span class="sxs-lookup"><span data-stu-id="4cb13-138">In hello **Subscription** box, enter hello Azure subscription that you use for your host.</span></span> 
      
   <span data-ttu-id="4cb13-139">c.</span><span class="sxs-lookup"><span data-stu-id="4cb13-139">c.</span></span> <span data-ttu-id="4cb13-140">Em Olá **região** , digite região geográfica hello, onde o host está localizado.</span><span class="sxs-lookup"><span data-stu-id="4cb13-140">In hello **Region** box, enter hello geographical region where your host is located.</span></span>
      
   <span data-ttu-id="4cb13-141">d.</span><span class="sxs-lookup"><span data-stu-id="4cb13-141">d.</span></span> <span data-ttu-id="4cb13-142">Em Olá **sistema operacional e o tamanho** guia, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="4cb13-142">On hello **OS and Size** tab, do hello following:</span></span>      
      * <span data-ttu-id="4cb13-143">**Sistema operacional do host**: insira o sistema operacional de saudação para a máquina virtual Olá que contém seu host.</span><span class="sxs-lookup"><span data-stu-id="4cb13-143">**Host OS**: Enter hello operating system for hello virtual machine that contains your host.</span></span> 
      * <span data-ttu-id="4cb13-144">**Tamanho**: insira o tamanho da máquina virtual Olá para o host.</span><span class="sxs-lookup"><span data-stu-id="4cb13-144">**Size**: Enter hello virtual-machine size for your host.</span></span>   
       
   <span data-ttu-id="4cb13-145">e.</span><span class="sxs-lookup"><span data-stu-id="4cb13-145">e.</span></span> <span data-ttu-id="4cb13-146">Em Olá **grupo de recursos** , selecione qualquer um dos seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="4cb13-146">On hello **Resource Group** tab, select either of hello following:</span></span>      
      * <span data-ttu-id="4cb13-147">**Novo grupo de recursos**: crie um grupo de recursos para o host.</span><span class="sxs-lookup"><span data-stu-id="4cb13-147">**New resource group**: Create a resource group for your host.</span></span>
      * <span data-ttu-id="4cb13-148">**Grupo de recursos existente**: especifique um grupo de recursos existente de sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="4cb13-148">**Existing resource group**: Specify an existing resource group from your Azure account.</span></span> 
       
   <span data-ttu-id="4cb13-149">f.</span><span class="sxs-lookup"><span data-stu-id="4cb13-149">f.</span></span> <span data-ttu-id="4cb13-150">Em Olá **rede** , selecione qualquer um dos seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="4cb13-150">On hello **Network** tab, select either of hello following:</span></span>      
      * <span data-ttu-id="4cb13-151">**Nova rede virtual**: crie uma rede virtual para o host.</span><span class="sxs-lookup"><span data-stu-id="4cb13-151">**New virtual network**: Create a virtual network for your host.</span></span>
      * <span data-ttu-id="4cb13-152">**Rede virtual existente**: especifique uma rede virtual existente de sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="4cb13-152">**Existing virtual network**: Specify an existing virtual network from your Azure account.</span></span> 
       
   <span data-ttu-id="4cb13-153">g.</span><span class="sxs-lookup"><span data-stu-id="4cb13-153">g.</span></span> <span data-ttu-id="4cb13-154">Em Olá **armazenamento** , selecione qualquer um dos seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="4cb13-154">On hello **Storage** tab, select either of hello following:</span></span>      
      * <span data-ttu-id="4cb13-155">**Nova conta de armazenamento**: crie uma conta de armazenamento para o host.</span><span class="sxs-lookup"><span data-stu-id="4cb13-155">**New storage account**: Create a storage account for your host.</span></span>
      * <span data-ttu-id="4cb13-156">**Conta de armazenamento existente**: especifique uma conta de armazenamento existente da sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="4cb13-156">**Existing storage account**: Specify an existing storage account from your Azure account.</span></span>
       
5. <span data-ttu-id="4cb13-157">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="4cb13-157">Click **Next**.</span></span>  
     <span data-ttu-id="4cb13-158">Olá **configurar log de credenciais e configurações de porta** janela será aberta.</span><span class="sxs-lookup"><span data-stu-id="4cb13-158">hello **Configure log in credentials and port settings** window opens.</span></span>

      ![log de configurar Olá na janela de configurações de porta e credenciais][PUB05]

6. <span data-ttu-id="4cb13-160">Selecione uma saudação as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="4cb13-160">Select one of hello following options:</span></span>

      * <span data-ttu-id="4cb13-161">**Importar credenciais do Azure Key Vault**: especifique um conjunto de credenciais que são armazenadas em sua assinatura do Azure salva anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4cb13-161">**Import credentials from Azure Key Vault**: Specify a previously saved set of credentials that are stored in your Azure subscription.</span></span>

          > [!NOTE]
          > <span data-ttu-id="4cb13-162">Um cofre de chaves do Azure que é criado com uma conta específica ou entidade de serviço não é automaticamente acessível por outra conta ou entidade de serviço que compartilha assinatura hello.</span><span class="sxs-lookup"><span data-stu-id="4cb13-162">An Azure key vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares hello subscription.</span></span> <span data-ttu-id="4cb13-163">tooallow outra chave de conta ou serviço de toouse principal Olá cofre, você deve usar o hello conta de saudação tooadd portal do Azure ou entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="4cb13-163">tooallow another account or service principal toouse hello key vault, you must use hello Azure portal tooadd hello account or service principal.</span></span>

      * <span data-ttu-id="4cb13-164">**Novas credenciais de logon**: crie um novo conjunto de credenciais de logon.</span><span class="sxs-lookup"><span data-stu-id="4cb13-164">**New log in credentials**: Create a new set of login credentials.</span></span> <span data-ttu-id="4cb13-165">Se você selecionar essa opção, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="4cb13-165">If you select this option, do hello following:</span></span>

        <span data-ttu-id="4cb13-166">a.</span><span class="sxs-lookup"><span data-stu-id="4cb13-166">a.</span></span> <span data-ttu-id="4cb13-167">Em Olá **VM credenciais** guia, forneça Olá seguintes informações para as credenciais de logon de máquina virtual de saudação do seu host do Docker: * **Username**: insira o nome de usuário de saudação para seu logon de máquina virtual credenciais.</span><span class="sxs-lookup"><span data-stu-id="4cb13-167">On hello **VM Credentials** tab, provide hello following information for hello virtual-machine login credentials of your Docker host: * **Username**: Enter hello username for your virtual-machine login credentials.</span></span>
             <span data-ttu-id="4cb13-168">* **Senha** e **confirmar**: insira a senha de saudação para suas credenciais de logon de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4cb13-168">* **Password** and **Confirm**: Enter hello password for your virtual-machine login credentials.</span></span>
             <span data-ttu-id="4cb13-169">* **SSH**: insira as configurações do hello Secure Shell (SSH) para o host do Docker.</span><span class="sxs-lookup"><span data-stu-id="4cb13-169">* **SSH**: Enter hello Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="4cb13-170">Você pode selecionar uma saudação as opções a seguir: * **nenhum**: Especifica que a sua máquina virtual não permite conexões SSH.</span><span class="sxs-lookup"><span data-stu-id="4cb13-170">You can select one of hello following options: * **None**: Specifies that your virtual machine does not allow SSH connections.</span></span>
                <span data-ttu-id="4cb13-171">* **Gerar automaticamente**: cria automaticamente Olá configurações necessárias para conectar-se via SSH.</span><span class="sxs-lookup"><span data-stu-id="4cb13-171">* **Auto-generate**: Automatically creates hello requisite settings for connecting via SSH.</span></span>
                <span data-ttu-id="4cb13-172">* **Importar do diretório**: permite que você toospecify um diretório que contém um conjunto de configurações de SSH salvos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4cb13-172">* **Import from directory**: Allows you toospecify a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="4cb13-173">diretório de saudação deve conter Olá dois arquivos a seguir:</span><span class="sxs-lookup"><span data-stu-id="4cb13-173">hello directory must contain hello following two files:</span></span>
                
                  * *id_rsa*: Contains hello RSA identification for a user.
                  * *id_rsa.pub*: Contains hello RSA public key that is used for authentication.
            
        <span data-ttu-id="4cb13-174">b.</span><span class="sxs-lookup"><span data-stu-id="4cb13-174">b.</span></span> <span data-ttu-id="4cb13-175">Em Olá **Docker Daemon acesso** guia, forneça Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="4cb13-175">On hello **Docker Daemon Access** tab, provide hello following information:</span></span>

          ![Criar host do Docker][PUB06]
    
             * **Docker Daemon port**: Enter hello unique TCP port for your Docker host.
             * **TLS Security**: Enter hello Transport Layer Security settings for your Docker host. You can choose from hello following options:
                * **None**: Specifies that your virtual machine does not allow TLS connections.
                * **Auto-generate**: Automatically creates hello requisite settings for connecting via TLS.
                * **Import from directory**: Specifies a directory that contains a set of previously saved TLS settings. hello directory must contain hello following six files: 
                   * *ca.pem* and *ca-key.pem*: Contain hello certificate and public key for hello TLS Certificate Authority.
                   * *cert.pem* and *key.pem*: Contain client certificate and public key which will be used for TLS authentication.
                   * *server.pem* and *server-key.pem*: Contain hello client certificate and public key that is used for TLS authentication.

7. <span data-ttu-id="4cb13-177">Depois que você inseriu as informações de saudação necessárias, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="4cb13-177">After you have entered hello required information, click **Finish**.</span></span>  
    <span data-ttu-id="4cb13-178">Olá **implantar o contêiner do Docker no Azure** assistente será exibida novamente.</span><span class="sxs-lookup"><span data-stu-id="4cb13-178">hello **Deploy Docker Container on Azure** wizard reappears.</span></span>

   ![Assistente para Implantar o Contêiner do Docker no Azure][PUB07]

8. <span data-ttu-id="4cb13-180">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="4cb13-180">Click **Next**.</span></span>  
    <span data-ttu-id="4cb13-181">Olá **configurar Olá Docker contêiner toobe criado** janela será aberta.</span><span class="sxs-lookup"><span data-stu-id="4cb13-181">hello **Configure hello Docker container toobe created** window opens.</span></span>

   ![janela de toobe criado Olá configurar Olá Docker contêiner][PUB08]

9. <span data-ttu-id="4cb13-183">Em Olá **configurar Olá Docker contêiner toobe criado** janela, forneça Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="4cb13-183">In hello **Configure hello Docker container toobe created** window, provide hello following information:</span></span> 

   <span data-ttu-id="4cb13-184">a.</span><span class="sxs-lookup"><span data-stu-id="4cb13-184">a.</span></span> <span data-ttu-id="4cb13-185">Em Olá **nome do contêiner Docker** , digite um nome exclusivo para o contêiner do Docker.</span><span class="sxs-lookup"><span data-stu-id="4cb13-185">In hello **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="4cb13-186">b.</span><span class="sxs-lookup"><span data-stu-id="4cb13-186">b.</span></span> <span data-ttu-id="4cb13-187">Escolha uma saudação imagens do Docker a seguir:</span><span class="sxs-lookup"><span data-stu-id="4cb13-187">Choose one of hello following Docker images:</span></span> 

      * <span data-ttu-id="4cb13-188">**Imagem do Docker predefinida**: especifique uma imagem já existente do Docker do Azure.</span><span class="sxs-lookup"><span data-stu-id="4cb13-188">**Predefined Docker image**: Specify a pre-existing Docker image from Azure.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="4cb13-189">Olá lista de imagens do Docker nesta caixa consiste em várias imagens que Olá Kit de ferramentas do Azure foi configurado toopatch de forma que o artefato é implantado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="4cb13-189">hello list of Docker images in this box consists of several images that hello Azure Toolkit has been configured toopatch so that your artifact is deployed automatically.</span></span> 

      * <span data-ttu-id="4cb13-190">**Dockerfile personalizado**: especifique um Dockerfile salvo anteriormente do computador local.</span><span class="sxs-lookup"><span data-stu-id="4cb13-190">**Custom Dockerfile**: Specify a previously saved Dockerfile from your local computer.</span></span>

        > [!NOTE]
        > <span data-ttu-id="4cb13-191">Esse é um recurso mais avançado para desenvolvedores que querem toodeploy seu próprios Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="4cb13-191">This is a more advanced feature for developers who want toodeploy their own Dockerfile.</span></span> <span data-ttu-id="4cb13-192">No entanto, ele é toodevelopers que usam essa tooensure de opção seu Dockerfile é criado corretamente.</span><span class="sxs-lookup"><span data-stu-id="4cb13-192">However, it is up toodevelopers who use this option tooensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="4cb13-193">Porque Olá Kit de ferramentas do Azure não validam o conteúdo de saudação em um Dockerfile personalizado, implantação de saudação poderá falhar se Olá Dockerfile tem problemas.</span><span class="sxs-lookup"><span data-stu-id="4cb13-193">Because hello Azure Toolkit does not validate hello content in a custom Dockerfile, hello deployment might fail if hello Dockerfile has issues.</span></span> <span data-ttu-id="4cb13-194">Além disso, porque Olá Kit de ferramentas do Azure espera Olá personalizado toocontain de Dockerfile um artefato de aplicativo web, ele tenta tooopen uma conexão HTTP.</span><span class="sxs-lookup"><span data-stu-id="4cb13-194">In addition, because hello Azure Toolkit expects hello custom Dockerfile toocontain a web app artifact, it attempts tooopen an HTTP connection.</span></span> <span data-ttu-id="4cb13-195">Se os desenvolvedores publicarem um tipo diferente de artefato, eles poderão receber erros inócuos após a implantação.</span><span class="sxs-lookup"><span data-stu-id="4cb13-195">If developers publish a different type of artifact, they might receive innocuous errors after deployment.</span></span>

   <span data-ttu-id="4cb13-196">c.</span><span class="sxs-lookup"><span data-stu-id="4cb13-196">c.</span></span> <span data-ttu-id="4cb13-197">Em Olá **as configurações de porta** , digite associação porta TCP de saudação exclusiva para o contêiner do Docker.</span><span class="sxs-lookup"><span data-stu-id="4cb13-197">In hello **Port settings** box, enter hello unique TCP port binding for your Docker container.</span></span> 

10. <span data-ttu-id="4cb13-198">Depois de concluir Olá etapas anteriores, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="4cb13-198">After you have completed hello preceding steps, click **Finish**.</span></span> 

<span data-ttu-id="4cb13-199">Olá Kit de ferramentas do Azure começa a implantar seu tooAzure de aplicativo web em um contêiner do Docker.</span><span class="sxs-lookup"><span data-stu-id="4cb13-199">hello Azure Toolkit begins deploying your web app tooAzure in a Docker container.</span></span> <span data-ttu-id="4cb13-200">A menos que você configurou toobe IntelliJ implantado no plano de fundo hello, um **Implantando tooAzure** barra de progresso é exibida.</span><span class="sxs-lookup"><span data-stu-id="4cb13-200">Unless you have configured IntelliJ toobe deployed in hello background, a **Deploying tooAzure** progress bar appears.</span></span> 

![barra de progresso de implantação Olá][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a><span data-ttu-id="4cb13-202">Informações adicionais sobre a criação de artefatos</span><span class="sxs-lookup"><span data-stu-id="4cb13-202">Additional information about creating artifacts</span></span>

<span data-ttu-id="4cb13-203">toocreate artefato um pronto para implantação, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="4cb13-203">toocreate a deployment-ready artifact, do hello following:</span></span>

1. <span data-ttu-id="4cb13-204">Abra seu projeto de aplicativo Web no IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="4cb13-204">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="4cb13-205">Clique em **Arquivo** e depois em **Estrutura do Projeto**.</span><span class="sxs-lookup"><span data-stu-id="4cb13-205">Click **File**, and then click **Project Structure**.</span></span>

   ![Olá comando estrutura do projeto][ART01]

3. <span data-ttu-id="4cb13-207">tooadd um artefato, clique em sinal de adição verde hello (**+**) e, em seguida, clique em **aplicativo Web: arquivo**.</span><span class="sxs-lookup"><span data-stu-id="4cb13-207">tooadd an artifact, click hello green plus sign (**+**), and then click **Web Application: Archive**.</span></span>

   ![Olá comando ": arquivo do aplicativo Web"][ART02]

4. <span data-ttu-id="4cb13-209">Em Olá **nome** , digite um nome para o artefato (não inclua Olá *. war* extensão) e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="4cb13-209">In hello **Name** box, enter a name for your artifact (do not include hello *.war* extension), and then click **OK**.</span></span>

   ![caixa de nome de artefato Olá][ART03]

<span data-ttu-id="4cb13-211">Para obter mais informações sobre como criar artefatos no IntelliJ, consulte [Configurando artefatos] no site de JetBrains hello.</span><span class="sxs-lookup"><span data-stu-id="4cb13-211">For more information about creating artifacts in IntelliJ, see [Configuring artifacts] on hello JetBrains website.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4cb13-212">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4cb13-212">Next steps</span></span>
<span data-ttu-id="4cb13-213">Para obter mais informações sobre Olá kits de ferramentas do Azure para Java IDEs, consulte Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="4cb13-213">For more information about hello Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="4cb13-214">[Kit de ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="4cb13-214">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="4cb13-215">[O que há de novo no hello Kit de ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="4cb13-215">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="4cb13-216">[Saudação de instalar o Kit de ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="4cb13-216">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="4cb13-217">[Instruções de entrada para Olá Kit de ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="4cb13-217">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="4cb13-218">[Criar um aplicativo Web Olá, Mundo para o Azure no Eclipse]</span><span class="sxs-lookup"><span data-stu-id="4cb13-218">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="4cb13-219">[Kit de Ferramentas do Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="4cb13-219">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="4cb13-220">[O que há de novo no hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="4cb13-220">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="4cb13-221">[Saudação de instalar o Kit de ferramentas do Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="4cb13-221">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="4cb13-222">[Instruções entrar para hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="4cb13-222">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="4cb13-223">[Criar um aplicativo Web Olá, Mundo para o Azure no IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="4cb13-223">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="4cb13-224">Para obter mais informações sobre como usar o Azure com Java, consulte Olá [Centro de desenvolvedores de Java do Azure] e hello [ferramentas Java para o Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="4cb13-224">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="4cb13-225">Para obter recursos adicionais do Docker, consulte oficial Olá [site Docker].</span><span class="sxs-lookup"><span data-stu-id="4cb13-225">For additional resources for Docker, see hello official [Docker website].</span></span>

<!-- URL List -->

[Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse.md
[Kit de Ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij.md
[Criar um aplicativo Web Olá, Mundo para o Azure no Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Criar um aplicativo Web Olá, Mundo para o Azure no IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Saudação de instalar o Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Saudação de instalar o Kit de ferramentas do Azure para IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Instruções de entrada para Olá Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Instruções entrar para hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[O que há de novo no hello Kit de ferramentas do Azure para Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[O que há de novo no hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Centro de desenvolvedores de Java do Azure]: https://azure.microsoft.com/develop/java/
[ferramentas Java para o Visual Studio Team Services]: https://java.visualstudio.com/

[site Docker]: https://www.docker.com/
[Configurando artefatos]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html

<!-- IMG List -->

[PUB01]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB01.png
[PUB02]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB02.png
[PUB03]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB03.png
[PUB04a]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04a.png
[PUB04b]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04b.png
[PUB04c]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04c.png
[PUB04d]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04d.png
[PUB05]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB05.png
[PUB06]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB06.png
[PUB07]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB07.png
[PUB08]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB08.png
[PUB09]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB09.png

[ART01]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART01.png
[ART02]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART02.png
[ART03]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART03.png
