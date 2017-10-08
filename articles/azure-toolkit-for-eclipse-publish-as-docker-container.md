---
title: "Olá de aaaPublish um contêiner do Docker usando o Kit de ferramentas do Azure para Eclipse | Microsoft Docs"
description: "Saiba como toopublish uma tooMicrosoft de aplicativo web do Azure como um contêiner do Docker usando Olá Kit de ferramentas do Azure para Eclipse."
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
ms.openlocfilehash: 53ec3a7f7a171691024e03622fd48d6f1e257b50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a><span data-ttu-id="14d8b-103">Publicar um aplicativo web como um contêiner do Docker usando Olá Kit de ferramentas do Azure para Eclipse</span><span class="sxs-lookup"><span data-stu-id="14d8b-103">Publish a web app as a Docker container by using hello Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="14d8b-104">Contêineres do Docker são um método amplamente usado para implantar aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="14d8b-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="14d8b-105">Usando contêineres do Docker, os desenvolvedores podem consolidar todos os seus arquivos de projeto e dependências em um único pacote para o servidor de implantação tooa.</span><span class="sxs-lookup"><span data-stu-id="14d8b-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment tooa server.</span></span> <span data-ttu-id="14d8b-106">Olá Kit de ferramentas do Azure para Eclipse simplifica esse processo para desenvolvedores de Java adicionando *Publicar como contêiner Docker* recursos para tooMicrosoft de implantação do Azure.</span><span class="sxs-lookup"><span data-stu-id="14d8b-106">hello Azure Toolkit for Eclipse simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment tooMicrosoft Azure.</span></span> <span data-ttu-id="14d8b-107">Este artigo orienta Olá etapas necessárias toopublish tooAzure seus aplicativos como contêineres do Docker.</span><span class="sxs-lookup"><span data-stu-id="14d8b-107">This article walks you through hello steps required toopublish your applications tooAzure as Docker containers.</span></span>

> [!NOTE]
> <span data-ttu-id="14d8b-108">Para obter mais informações sobre o Docker estão disponíveis no hello [site Docker].</span><span class="sxs-lookup"><span data-stu-id="14d8b-108">More information about Docker is available on hello [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="14d8b-109">Publicar seu tooAzure de aplicativo web usando um contêiner do Docker</span><span class="sxs-lookup"><span data-stu-id="14d8b-109">Publish your web app tooAzure by using a Docker container</span></span>

1. <span data-ttu-id="14d8b-110">Abra seu projeto de aplicativo Web no Eclipse.</span><span class="sxs-lookup"><span data-stu-id="14d8b-110">Open your web app project in Eclipse.</span></span>

2. <span data-ttu-id="14d8b-111">Olá toostart **Publicar como contêiner Docker** assistente, faça o seguinte de saudação:</span><span class="sxs-lookup"><span data-stu-id="14d8b-111">toostart hello **Publish as Docker Container** wizard, do either of hello following:</span></span>

   * <span data-ttu-id="14d8b-112">Em Olá **navegador** exibir, clique com o botão direito, clique em **Azure**e, em seguida, clique em **Publicar como contêiner Docker**.</span><span class="sxs-lookup"><span data-stu-id="14d8b-112">In hello **Navigator** view, right-click your project, click **Azure**, and then click **Publish as Docker Container**.</span></span>

      ![Comando Publicar como Contêiner do Docker da exibição Navegador][PUB01]

   * <span data-ttu-id="14d8b-114">Na barra de ferramentas do Eclipse hello, clique em Olá **publicar** botão e, em seguida, clique em **Publicar como contêiner Docker**.</span><span class="sxs-lookup"><span data-stu-id="14d8b-114">On hello Eclipse toolbar, click hello **Publish** button, and then click **Publish as Docker Container**.</span></span>

      ![Comando Publicar como Contêiner do Docker da barra de ferramentas do Eclipse][PUB02]
      
    <span data-ttu-id="14d8b-116">Olá **implantar o contêiner do Docker no Azure** assistente é aberto.</span><span class="sxs-lookup"><span data-stu-id="14d8b-116">hello **Deploy Docker Container on Azure** wizard opens.</span></span>

    ![Olá implantar o contêiner do Docker no Assistente do Azure][PUB03]

3. <span data-ttu-id="14d8b-118">Em Olá **digite um nome de imagem, selecione o caminho do artefato hello e verificar um toobe de host do Docker usado** janela, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="14d8b-118">In hello **Type an image name, select hello artifact's path and check a Docker host toobe used** window, do hello following:</span></span>

    <span data-ttu-id="14d8b-119">a.</span><span class="sxs-lookup"><span data-stu-id="14d8b-119">a.</span></span> <span data-ttu-id="14d8b-120">Em Olá **nome de imagem do Docker** , digite um nome exclusivo para o host do Docker.</span><span class="sxs-lookup"><span data-stu-id="14d8b-120">In hello **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="14d8b-121">(Olá criará automaticamente um nome, mas você pode modificá-la.)</span><span class="sxs-lookup"><span data-stu-id="14d8b-121">(hello wizard automatically creates a name, but you can modify it.)</span></span>

    <span data-ttu-id="14d8b-122">b.</span><span class="sxs-lookup"><span data-stu-id="14d8b-122">b.</span></span> <span data-ttu-id="14d8b-123">Olá **Hosts** área exibe os hosts de Docker que você criou.</span><span class="sxs-lookup"><span data-stu-id="14d8b-123">hello **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="14d8b-124">Siga um destes procedimentos hello:</span><span class="sxs-lookup"><span data-stu-id="14d8b-124">Do either of hello following:</span></span>

    * <span data-ttu-id="14d8b-125">Se você tiver um host Docker existente, você pode implantar seu tooit de aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="14d8b-125">If you have an existing Docker host, you can deploy your web app tooit.</span></span>
    * <span data-ttu-id="14d8b-126">Clique em toocreate um novo host do Docker, **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="14d8b-126">toocreate a new Docker host, click **Add**.</span></span>  
      
    <span data-ttu-id="14d8b-127">Olá **criar Host do Docker** caixa de diálogo é aberta.</span><span class="sxs-lookup"><span data-stu-id="14d8b-127">hello **Create Docker Host** dialog box opens.</span></span>

    ![Assistente para Implantar o Contêiner do Docker no Azure][PUB04a]

4. <span data-ttu-id="14d8b-129">Em Olá **configurar nova máquina de virtual Olá** janela, especificar Olá para o host do Docker as opções a seguir.</span><span class="sxs-lookup"><span data-stu-id="14d8b-129">In hello **Configure hello new virtual machine** window, specify hello following options for your Docker host.</span></span> <span data-ttu-id="14d8b-130">(Assistente de saudação gera automaticamente a maioria das opções de saudação para você, mas você pode modificar qualquer um deles.)</span><span class="sxs-lookup"><span data-stu-id="14d8b-130">(hello wizard automatically generates most of hello options for you, but you can modify any of them.)</span></span>

   <span data-ttu-id="14d8b-131">a.</span><span class="sxs-lookup"><span data-stu-id="14d8b-131">a.</span></span> <span data-ttu-id="14d8b-132">**Nome**: insira um nome exclusivo para o host do Docker hello.</span><span class="sxs-lookup"><span data-stu-id="14d8b-132">**Name**: Enter a unique name for hello Docker host.</span></span> <span data-ttu-id="14d8b-133">(É não Olá mesmo Olá nome de imagem do Docker que você especificou anteriormente.)</span><span class="sxs-lookup"><span data-stu-id="14d8b-133">(It is not hello same as hello Docker image name that you specified earlier.)</span></span>

   <span data-ttu-id="14d8b-134">b.</span><span class="sxs-lookup"><span data-stu-id="14d8b-134">b.</span></span> <span data-ttu-id="14d8b-135">**Assinatura**: insira Olá assinatura do Azure que você usa para o host.</span><span class="sxs-lookup"><span data-stu-id="14d8b-135">**Subscription**: Enter hello Azure subscription that you use for your host.</span></span>

   <span data-ttu-id="14d8b-136">c.</span><span class="sxs-lookup"><span data-stu-id="14d8b-136">c.</span></span> <span data-ttu-id="14d8b-137">**Região**: Inserir Olá região geográfica em que o host está localizado.</span><span class="sxs-lookup"><span data-stu-id="14d8b-137">**Region**: Enter hello geographical region where your host is located.</span></span>

   <span data-ttu-id="14d8b-138">d.</span><span class="sxs-lookup"><span data-stu-id="14d8b-138">d.</span></span> <span data-ttu-id="14d8b-139">Em Olá **sistema operacional do Host e o tamanho** guia:</span><span class="sxs-lookup"><span data-stu-id="14d8b-139">On hello **Host OS and Size** tab:</span></span>
     * <span data-ttu-id="14d8b-140">**Sistema operacional do host**: insira o sistema operacional de saudação para a máquina virtual Olá que contém seu host.</span><span class="sxs-lookup"><span data-stu-id="14d8b-140">**Host OS**: Enter hello operating system for hello virtual machine that contains your host.</span></span>
     * <span data-ttu-id="14d8b-141">**Tamanho**: insira o tamanho da máquina virtual Olá para o host.</span><span class="sxs-lookup"><span data-stu-id="14d8b-141">**Size**: Enter hello virtual-machine size for your host.</span></span>

   <span data-ttu-id="14d8b-142">e.</span><span class="sxs-lookup"><span data-stu-id="14d8b-142">e.</span></span> <span data-ttu-id="14d8b-143">Em Olá **grupo de recursos** guia:</span><span class="sxs-lookup"><span data-stu-id="14d8b-143">On hello **Resource Group** tab:</span></span>
     * <span data-ttu-id="14d8b-144">**Novo grupo de recursos**: crie um novo grupo de recursos para o host.</span><span class="sxs-lookup"><span data-stu-id="14d8b-144">**New resource group**: Create a new resource group for your host.</span></span>
     * <span data-ttu-id="14d8b-145">**Grupo de recursos existente**: insira um grupo de recursos existente de sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="14d8b-145">**Existing resource group**: Enter an existing resource group from your Azure account.</span></span>

   <span data-ttu-id="14d8b-146">f.</span><span class="sxs-lookup"><span data-stu-id="14d8b-146">f.</span></span> <span data-ttu-id="14d8b-147">Em Olá **rede** guia:</span><span class="sxs-lookup"><span data-stu-id="14d8b-147">On hello **Network** tab:</span></span>
     * <span data-ttu-id="14d8b-148">**Nova rede virtual**: crie uma nova rede virtual para o host.</span><span class="sxs-lookup"><span data-stu-id="14d8b-148">**New virtual network**: Create a new virtual network for your host.</span></span>
     * <span data-ttu-id="14d8b-149">**Rede virtual existente**: insira uma rede virtual existente de sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="14d8b-149">**Existing virtual network**: Enter an existing virtual network from your Azure account.</span></span>

   <span data-ttu-id="14d8b-150">g.</span><span class="sxs-lookup"><span data-stu-id="14d8b-150">g.</span></span> <span data-ttu-id="14d8b-151">Em Olá **armazenamento** guia:</span><span class="sxs-lookup"><span data-stu-id="14d8b-151">On hello **Storage** tab:</span></span>
     * <span data-ttu-id="14d8b-152">**Nova conta de armazenamento**: crie uma nova conta de armazenamento para o host.</span><span class="sxs-lookup"><span data-stu-id="14d8b-152">**New storage account**: Create a new storage account for your host.</span></span>
     * <span data-ttu-id="14d8b-153">**Conta de armazenamento existente**: insira uma conta de armazenamento existente da sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="14d8b-153">**Existing storage account**: Enter an existing storage account from your Azure account.</span></span>

5. <span data-ttu-id="14d8b-154">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="14d8b-154">Click **Next**.</span></span>

6. <span data-ttu-id="14d8b-155">Em Olá **configurar log de credenciais e configurações de porta** janela, selecione uma das Olá as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="14d8b-155">In hello **Configure log in credentials and port settings** window, select one of hello following options:</span></span>

    * <span data-ttu-id="14d8b-156">**Importar credenciais do Azure Key Vault**: especifica um conjunto de credenciais salvas anteriormente que são armazenadas em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="14d8b-156">**Import credentials from Azure Key Vault**: Specifies a previously saved set of credentials that are stored in your Azure subscription.</span></span>

      >[!NOTE]
      ><span data-ttu-id="14d8b-157">Um cofre de chaves do Azure que é criada com uma conta específica ou entidade de serviço não é automaticamente acessível por outra conta ou entidade de serviço que compartilha assinatura hello.</span><span class="sxs-lookup"><span data-stu-id="14d8b-157">An Azure Key Vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares hello subscription.</span></span> <span data-ttu-id="14d8b-158">tooallow outra conta ou serviço toouse principal Olá Cofre de chaves, você deve usar o hello conta de saudação tooadd portal do Azure ou entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="14d8b-158">tooallow another account or service principal toouse hello Key Vault, you must use hello Azure portal tooadd hello account or service principal.</span></span>

    * <span data-ttu-id="14d8b-159">**Novas credenciais de logon**: cria um novo conjunto de credenciais de logon.</span><span class="sxs-lookup"><span data-stu-id="14d8b-159">**New log in credentials**: Creates a new set of login credentials.</span></span> <span data-ttu-id="14d8b-160">Se você selecionar essa opção, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="14d8b-160">If you select this option, do hello following:</span></span>
    
      * <span data-ttu-id="14d8b-161">Em Olá **VM credenciais** guia, escolha uma das seguintes Olá opções para credenciais de logon de máquina virtual de saudação do seu host do Docker:</span><span class="sxs-lookup"><span data-stu-id="14d8b-161">On hello **VM Credentials** tab, choose one of hello following options for hello virtual-machine login credentials of your Docker host:</span></span>

          * <span data-ttu-id="14d8b-162">**Nome de usuário**: insira o nome de usuário de saudação suas credenciais de logon de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="14d8b-162">**Username**: Enter hello username for your virtual machine login credentials.</span></span>
          * <span data-ttu-id="14d8b-163">**Senha** e **confirmar**: insira a senha de saudação suas credenciais de logon de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="14d8b-163">**Password** and **Confirm**: Enter hello password for your virtual machine login credentials.</span></span>
          * <span data-ttu-id="14d8b-164">**SSH**: insira as configurações do hello Secure Shell (SSH) para o host do Docker.</span><span class="sxs-lookup"><span data-stu-id="14d8b-164">**SSH**: Enter hello Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="14d8b-165">Você pode escolher Olá as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="14d8b-165">You can choose from hello following options:</span></span>
            * <span data-ttu-id="14d8b-166">**Nenhum**: especifica que a sua máquina virtual não permitirá conexões SSH.</span><span class="sxs-lookup"><span data-stu-id="14d8b-166">**None**: Specifies that your virtual machine will not allow SSH connections.</span></span>
            * <span data-ttu-id="14d8b-167">**Gerar automaticamente**: cria automaticamente Olá configurações necessárias para conectar-se via SSH.</span><span class="sxs-lookup"><span data-stu-id="14d8b-167">**Auto-generate**: Automatically creates hello requisite settings for connecting via SSH.</span></span>
            * <span data-ttu-id="14d8b-168">**Importar do diretório**: especifica um diretório que contém um conjunto de configurações de SSH salvas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="14d8b-168">**Import from directory**: Specifies a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="14d8b-169">diretório de saudação deve conter Olá dois arquivos a seguir:</span><span class="sxs-lookup"><span data-stu-id="14d8b-169">hello directory must contain hello following two files:</span></span>
                * <span data-ttu-id="14d8b-170">*id_rsa*: contém a identificação de RSA Olá para um usuário.</span><span class="sxs-lookup"><span data-stu-id="14d8b-170">*id_rsa*: Contains hello RSA identification for a user.</span></span>
                * <span data-ttu-id="14d8b-171">*id_rsa.pub*: contém Olá chave pública RSA que é usado para autenticação.</span><span class="sxs-lookup"><span data-stu-id="14d8b-171">*id_rsa.pub*: Contains hello RSA public key that is used for authentication.</span></span>
        
        ![Criar host do Docker][PUB05]

      * <span data-ttu-id="14d8b-173">Em Olá **Docker Daemon credenciais** especifique Olá as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="14d8b-173">On hello **Docker Daemon Credentials** tab, specify hello following options:</span></span>

          * <span data-ttu-id="14d8b-174">**Porta de Daemon do docker**: insira a porta TCP exclusiva Olá para o host do Docker.</span><span class="sxs-lookup"><span data-stu-id="14d8b-174">**Docker Daemon port**: Enter hello unique TCP port for your Docker host.</span></span>
          * <span data-ttu-id="14d8b-175">**Segurança de TLS**: insira Olá Transport Layer Security configurações para o host do Docker.</span><span class="sxs-lookup"><span data-stu-id="14d8b-175">**TLS Security**: Enter hello Transport Layer Security settings for your Docker host.</span></span> <span data-ttu-id="14d8b-176">Você pode escolher Olá as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="14d8b-176">You can choose from hello following options:</span></span>
            * <span data-ttu-id="14d8b-177">**Nenhum**: especifica que a sua máquina virtual não permitirá conexões TLS.</span><span class="sxs-lookup"><span data-stu-id="14d8b-177">**None**: Specifies that your virtual machine will not allow TLS connections.</span></span>
            * <span data-ttu-id="14d8b-178">**Gerar automaticamente**: cria automaticamente Olá configurações necessárias para se conectar por meio de TLS.</span><span class="sxs-lookup"><span data-stu-id="14d8b-178">**Auto-generate**: Automatically creates hello requisite settings for connecting via TLS.</span></span>
            * <span data-ttu-id="14d8b-179">**Importar do diretório**: especifica um diretório que contém um conjunto de configurações de TLS salvas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="14d8b-179">**Import from directory**: Specifies a directory that contains a set of previously saved TLS settings.</span></span> <span data-ttu-id="14d8b-180">Mais especificamente, o diretório de saudação deve conter Olá seis arquivos a seguir:</span><span class="sxs-lookup"><span data-stu-id="14d8b-180">More specifically, hello directory must contain hello following six files:</span></span>
                * <span data-ttu-id="14d8b-181">*CA. PEM* e *key.pem ca*: contêm o certificado hello e uma chave pública para Olá autoridade de certificação de TLS.</span><span class="sxs-lookup"><span data-stu-id="14d8b-181">*ca.pem* and *ca-key.pem*: Contain hello certificate and public key for hello TLS Certificate Authority.</span></span>
                * <span data-ttu-id="14d8b-182">*cert.PEM* e *key.pem*: contêm o certificado do cliente hello e uma chave pública que é usado para autenticação de TLS.</span><span class="sxs-lookup"><span data-stu-id="14d8b-182">*cert.pem* and *key.pem*: Contain hello client certificate and public key that is used for TLS authentication.</span></span>
                * <span data-ttu-id="14d8b-183">*Server.PEM* e *key.pem server*: contêm o certificado do servidor de saudação e a chave pública para o host de saudação.</span><span class="sxs-lookup"><span data-stu-id="14d8b-183">*server.pem* and *server-key.pem*: Contain hello server certificate and public key for hello host.</span></span>

        ![Criar host do Docker][PUB06]

7. <span data-ttu-id="14d8b-185">Depois que você inseriu todos Olá informações anteriores, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="14d8b-185">After you have entered all of hello preceding information, click **Finish**.</span></span>

8. <span data-ttu-id="14d8b-186">Em Olá **implantar o contêiner do Docker no Azure** assistente, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="14d8b-186">In hello **Deploy Docker Container on Azure** wizard, click **Next**.</span></span>

   ![Olá implantar o contêiner do Docker no Assistente do Azure][PUB07]

9. <span data-ttu-id="14d8b-188">Em Olá **configurar Olá Docker contêiner toobe criado** janela, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="14d8b-188">In hello **Configure hello Docker container toobe created** window, do hello following:</span></span>

   <span data-ttu-id="14d8b-189">a.</span><span class="sxs-lookup"><span data-stu-id="14d8b-189">a.</span></span> <span data-ttu-id="14d8b-190">Em Olá **nome do contêiner Docker** , digite um nome exclusivo para o contêiner do Docker.</span><span class="sxs-lookup"><span data-stu-id="14d8b-190">In hello **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="14d8b-191">b.</span><span class="sxs-lookup"><span data-stu-id="14d8b-191">b.</span></span> <span data-ttu-id="14d8b-192">Escolha uma saudação imagens do Docker a seguir:</span><span class="sxs-lookup"><span data-stu-id="14d8b-192">Choose one of hello following Docker images:</span></span>
     * <span data-ttu-id="14d8b-193">**Imagem do Docker predefinida**: especifica uma imagem já existente do Docker do Azure.</span><span class="sxs-lookup"><span data-stu-id="14d8b-193">**Predefined Docker image**: Specifies a pre-existing Docker image from Azure.</span></span>

       >[!NOTE]
       ><span data-ttu-id="14d8b-194">Olá lista de imagens do Docker nesta caixa consiste em várias imagens que Olá Kit de ferramentas do Azure foi configurado toopatch de forma que o artefato é implantado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="14d8b-194">hello list of Docker images in this box consists of several images that hello Azure Toolkit has been configured toopatch so that your artifact is deployed automatically.</span></span>

     * <span data-ttu-id="14d8b-195">**Dockerfile personalizado**: especifica um Dockerfile salvo anteriormente do computador local.</span><span class="sxs-lookup"><span data-stu-id="14d8b-195">**Custom Dockerfile**: Specifies a previously saved Dockerfile from your local computer.</span></span>

       >[!NOTE]
       ><span data-ttu-id="14d8b-196">Esse é um recurso mais avançado para desenvolvedores que querem toodeploy seu próprios Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="14d8b-196">This is a more advanced feature for developers who want toodeploy their own Dockerfile.</span></span> <span data-ttu-id="14d8b-197">No entanto, ele é toodevelopers que usam essa tooensure de opção seu Dockerfile é criado corretamente.</span><span class="sxs-lookup"><span data-stu-id="14d8b-197">However, it is up toodevelopers who use this option tooensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="14d8b-198">Olá Kit de ferramentas do Azure não validar o conteúdo de saudação em um Dockerfile personalizado, para que implantação Olá poderá falhar se Olá Dockerfile tem problemas.</span><span class="sxs-lookup"><span data-stu-id="14d8b-198">hello Azure Toolkit does not validate hello content in a custom Dockerfile, so hello deployment might fail if hello Dockerfile has issues.</span></span> <span data-ttu-id="14d8b-199">Além disso, Olá Kit de ferramentas do Azure espera Olá personalizado toocontain de Dockerfile um artefato de aplicativo web, e ele tentará tooopen uma conexão HTTP.</span><span class="sxs-lookup"><span data-stu-id="14d8b-199">In addition, hello Azure Toolkit expects hello custom Dockerfile toocontain a web app artifact, and it will attempt tooopen an HTTP connection.</span></span> <span data-ttu-id="14d8b-200">Se os desenvolvedores publicarem um tipo diferente de artefato, eles poderão receber erros inócuos após a implantação.</span><span class="sxs-lookup"><span data-stu-id="14d8b-200">If developers publish a different type of artifact, they may receive innocuous errors after deployment.</span></span>

   <span data-ttu-id="14d8b-201">c.</span><span class="sxs-lookup"><span data-stu-id="14d8b-201">c.</span></span> <span data-ttu-id="14d8b-202">**Configurações de porta**: insira associação porta TCP de saudação exclusiva para o contêiner do Docker.</span><span class="sxs-lookup"><span data-stu-id="14d8b-202">**Port settings**: Enter hello unique TCP port binding for your Docker container.</span></span>

     ![janela de toobe criado Olá configurar Olá Docker contêiner][PUB08]

10. <span data-ttu-id="14d8b-204">Depois de concluir todas Olá etapas anteriores, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="14d8b-204">After you have completed all of hello preceding steps, click **Finish**.</span></span>

<span data-ttu-id="14d8b-205">Olá Kit de ferramentas do Azure começa a implantar seu tooAzure de aplicativo web em um contêiner do Docker.</span><span class="sxs-lookup"><span data-stu-id="14d8b-205">hello Azure Toolkit begins deploying your web app tooAzure in a Docker container.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="14d8b-206">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="14d8b-206">Next steps</span></span>
<span data-ttu-id="14d8b-207">Para obter mais informações sobre Olá kits de ferramentas do Azure para Java IDEs, consulte Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="14d8b-207">For more information about hello Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="14d8b-208">[Kit de ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="14d8b-208">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="14d8b-209">[O que há de novo no hello Kit de ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="14d8b-209">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="14d8b-210">[Saudação de instalar o Kit de ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="14d8b-210">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="14d8b-211">[Instruções de entrada para Olá Kit de ferramentas do Azure para Eclipse]</span><span class="sxs-lookup"><span data-stu-id="14d8b-211">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="14d8b-212">[Criar um aplicativo Web Olá, Mundo para o Azure no Eclipse]</span><span class="sxs-lookup"><span data-stu-id="14d8b-212">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="14d8b-213">[Kit de Ferramentas do Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="14d8b-213">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="14d8b-214">[O que há de novo no hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="14d8b-214">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="14d8b-215">[Saudação de instalar o Kit de ferramentas do Azure para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="14d8b-215">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="14d8b-216">[Instruções entrar para hello Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="14d8b-216">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="14d8b-217">[Criar um aplicativo Web Olá, Mundo para o Azure no IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="14d8b-217">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="14d8b-218">Para saber mais sobre como usar o Azure com Java, confira o [Centro de Desenvolvedores Java do Azure] e as [Ferramentas Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="14d8b-218">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="14d8b-219">Para obter recursos adicionais do Docker, consulte oficial Olá [site Docker].</span><span class="sxs-lookup"><span data-stu-id="14d8b-219">For additional resources for Docker, see hello official [Docker website].</span></span>

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

[Centro de Desenvolvedores Java do Azure]: https://azure.microsoft.com/develop/java/
[Ferramentas Java para Visual Studio Team Services]: https://java.visualstudio.com/

[site Docker]: https://www.docker.com/

<!-- IMG List -->

[PUB01]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB01.png
[PUB02]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB02.png
[PUB03]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB03.png
[PUB04a]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04a.png
[PUB04b]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04b.png
[PUB04c]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04c.png
[PUB04d]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04d.png
[PUB05]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB05.png
[PUB06]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB06.png
[PUB07]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB07.png
[PUB08]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB08.png