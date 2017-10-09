---
title: "aaaHow toouse hello Azure escravo de plug-in com a integração contínua Hudson | Microsoft Docs"
description: "Descreve como toouse hello Azure slave plug-in com a integração contínua Hudson."
services: virtual-machines-linux
documentationcenter: 
author: rmcmurray
manager: wpickett
editor: 
ms.assetid: b2083d1c-4de8-4a19-a615-ccc9d9b6e1d9
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: cd6e67ad71c208aa56746aa8b70ba507da20bee9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-slave-plug-in-with-hudson-continuous-integration"></a><span data-ttu-id="ea97f-103">Como toouse hello Azure slave plug-in com a integração contínua Hudson</span><span class="sxs-lookup"><span data-stu-id="ea97f-103">How toouse hello Azure slave plug-in with Hudson Continuous Integration</span></span>
<span data-ttu-id="ea97f-104">Hello Azure escravo de plug-in para Hudson permite que você tooprovision subordinado nós no Azure quando em execução distribuída cria.</span><span class="sxs-lookup"><span data-stu-id="ea97f-104">hello Azure slave plug-in for Hudson enables you tooprovision slave nodes on Azure when running distributed builds.</span></span>

## <a name="install-hello-azure-slave-plug-in"></a><span data-ttu-id="ea97f-105">Instalar hello Azure subordinado plug-in</span><span class="sxs-lookup"><span data-stu-id="ea97f-105">Install hello Azure Slave plug-in</span></span>
1. <span data-ttu-id="ea97f-106">No painel Hudson do hello, clique em **Hudson gerenciar**.</span><span class="sxs-lookup"><span data-stu-id="ea97f-106">In hello Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="ea97f-107">Em Olá **Hudson gerenciar** página, clique em **gerenciar plug-ins**.</span><span class="sxs-lookup"><span data-stu-id="ea97f-107">In hello **Manage Hudson** page, click on **Manage Plugins**.</span></span>
3. <span data-ttu-id="ea97f-108">Clique em Olá **disponível** guia.</span><span class="sxs-lookup"><span data-stu-id="ea97f-108">Click hello **Available** tab.</span></span>
4. <span data-ttu-id="ea97f-109">Clique em **pesquisa** e tipo **Azure** toolimit Olá lista toorelevant plug-ins.</span><span class="sxs-lookup"><span data-stu-id="ea97f-109">Click **Search** and type **Azure** toolimit hello list toorelevant plug-ins.</span></span>
   
    <span data-ttu-id="ea97f-110">Se você optar por tooscroll por meio da lista de saudação de plug-ins disponíveis, você encontrará hello Azure subordinado plug-in em Olá **distribuídas de compilação e de gerenciamento de Cluster** seção Olá **outros** guia.</span><span class="sxs-lookup"><span data-stu-id="ea97f-110">If you opt tooscroll through hello list of available plug-ins, you will find hello Azure slave plug-in under hello **Cluster Management and Distributed Build** section in hello **Others** tab.</span></span>
5. <span data-ttu-id="ea97f-111">Selecione caixa de seleção Olá para **plug-in do Azure subordinado**.</span><span class="sxs-lookup"><span data-stu-id="ea97f-111">Select hello checkbox for **Azure Slave Plugin**.</span></span>
6. <span data-ttu-id="ea97f-112">Clique em **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="ea97f-112">Click **Install**.</span></span>
7. <span data-ttu-id="ea97f-113">Reinicie o Hudson.</span><span class="sxs-lookup"><span data-stu-id="ea97f-113">Restart Hudson.</span></span>

<span data-ttu-id="ea97f-114">Agora que Olá plug-in estiver instalado, as próximas etapas Olá seria tooconfigure Olá plug-in com o perfil de assinatura do Azure e toocreate um modelo que será usado na criação de hello VM para o nó de escravo hello.</span><span class="sxs-lookup"><span data-stu-id="ea97f-114">Now that hello plug-in is installed, hello next steps would be tooconfigure hello plug-in with your Azure subscription profile and toocreate a template that will be used in creating hello VM for hello slave node.</span></span>

## <a name="configure-hello-azure-slave-plug-in-with-your-subscription-profile"></a><span data-ttu-id="ea97f-115">Configurar hello Azure subordinado plug-in com o seu perfil de inscrição</span><span class="sxs-lookup"><span data-stu-id="ea97f-115">Configure hello Azure Slave plug-in with your subscription profile</span></span>
<span data-ttu-id="ea97f-116">Um perfil de assinatura, também chamado de tooas configurações de publicação, é um arquivo XML que contém credenciais seguras e informações adicionais, você precisará toowork com o Azure no seu ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="ea97f-116">A subscription profile, also referred tooas publish settings, is an XML file that contains secure credentials and some additional information you'll need toowork with Azure in your development environment.</span></span> <span data-ttu-id="ea97f-117">tooconfigure hello Azure escravo de plug-in, você precisa:</span><span class="sxs-lookup"><span data-stu-id="ea97f-117">tooconfigure hello Azure slave plug-in, you need:</span></span>

* <span data-ttu-id="ea97f-118">A ID de sua assinatura</span><span class="sxs-lookup"><span data-stu-id="ea97f-118">Your subscription id</span></span>
* <span data-ttu-id="ea97f-119">Um certificado de gerenciamento da sua assinatura</span><span class="sxs-lookup"><span data-stu-id="ea97f-119">A management certificate for your subscription</span></span>

<span data-ttu-id="ea97f-120">Eles podem ser encontrados em seu [perfil de assinatura].</span><span class="sxs-lookup"><span data-stu-id="ea97f-120">These can be found in your [subscription profile].</span></span> <span data-ttu-id="ea97f-121">Veja a seguir um exemplo de perfil de assinatura.</span><span class="sxs-lookup"><span data-stu-id="ea97f-121">Below is an example of a subscription profile.</span></span>

    <?xml version="1.0" encoding="utf-8"?>

        <PublishData>

          <PublishProfile SchemaVersion="2.0" PublishMethod="AzureServiceManagementAPI">

        <Subscription

              ServiceManagementUrl="https://management.core.windows.net"

              Id="<Subscription ID>"

              Name="Pay-As-You-Go"
            ManagementCertificate="<Management certificate value>" />

          </PublishProfile>

    </PublishData>

<span data-ttu-id="ea97f-122">Uma vez que o perfil de assinatura, siga essas tooconfigure de etapas hello Azure escravo de plug-in.</span><span class="sxs-lookup"><span data-stu-id="ea97f-122">Once you have your subscription profile, follow these steps tooconfigure hello Azure slave plug-in.</span></span>

1. <span data-ttu-id="ea97f-123">No painel Hudson do hello, clique em **Hudson gerenciar**.</span><span class="sxs-lookup"><span data-stu-id="ea97f-123">In hello Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="ea97f-124">Clique em **Configure System**.</span><span class="sxs-lookup"><span data-stu-id="ea97f-124">Click **Configure System**.</span></span>
3. <span data-ttu-id="ea97f-125">Role para baixo de saudação do hello página toofind **nuvem** seção.</span><span class="sxs-lookup"><span data-stu-id="ea97f-125">Scroll down hello page toofind hello **Cloud** section.</span></span>
4. <span data-ttu-id="ea97f-126">Clique em **Adicionar nova nuvem > Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="ea97f-126">Click **Add new cloud > Microsoft Azure**.</span></span>
   
    ![adicionar nova nuvem][add new cloud]
   
    <span data-ttu-id="ea97f-128">Isso mostrará campos Olá em que você precisa tooenter detalhes da sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="ea97f-128">This will show hello fields where you need tooenter your subscription details.</span></span>
   
    ![configurar perfil][configure profile]
5. <span data-ttu-id="ea97f-130">Copie o certificado de id e o gerenciamento de assinatura de saudação do seu perfil de inscrição e cole-os nos campos apropriados hello.</span><span class="sxs-lookup"><span data-stu-id="ea97f-130">Copy hello subscription id and management certificate from your subscription profile and paste them in hello appropriate fields.</span></span>
   
    <span data-ttu-id="ea97f-131">Ao copiar Olá assinatura id e o gerenciamento de certificado, **não** incluir aspas Olá colocar valores hello.</span><span class="sxs-lookup"><span data-stu-id="ea97f-131">When copying hello subscription id and management certificate, **do not** include hello quotes that enclose hello values.</span></span>
6. <span data-ttu-id="ea97f-132">Clique em **Verify configuration**.</span><span class="sxs-lookup"><span data-stu-id="ea97f-132">Click on **Verify configuration**.</span></span>
7. <span data-ttu-id="ea97f-133">Quando a configuração de saudação é verificada com êxito, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="ea97f-133">When hello configuration is verified successfully, click **Save**.</span></span>

## <a name="set-up-a-virtual-machine-template-for-hello-azure-slave-plug-in"></a><span data-ttu-id="ea97f-134">Configurar um modelo de máquina virtual para hello Azure subordinado plug-in</span><span class="sxs-lookup"><span data-stu-id="ea97f-134">Set up a virtual machine template for hello Azure Slave plug-in</span></span>
<span data-ttu-id="ea97f-135">Um modelo de máquina virtual define parâmetros Olá Olá plug-in usará toocreate um nó subordinado no Azure.</span><span class="sxs-lookup"><span data-stu-id="ea97f-135">A virtual machine template defines hello parameters hello plug-in will use toocreate a slave node on Azure.</span></span> <span data-ttu-id="ea97f-136">Em Olá etapas a seguir é estará criando o modelo para uma VM Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="ea97f-136">In hello following steps we'll be creating template for an Ubuntu VM.</span></span>

1. <span data-ttu-id="ea97f-137">No painel Hudson do hello, clique em **Hudson gerenciar**.</span><span class="sxs-lookup"><span data-stu-id="ea97f-137">In hello Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="ea97f-138">Clique em **Configure System**.</span><span class="sxs-lookup"><span data-stu-id="ea97f-138">Click on **Configure System**.</span></span>
3. <span data-ttu-id="ea97f-139">Role para baixo de saudação do hello página toofind **nuvem** seção.</span><span class="sxs-lookup"><span data-stu-id="ea97f-139">Scroll down hello page toofind hello **Cloud** section.</span></span>
4. <span data-ttu-id="ea97f-140">Dentro de saudação **nuvem** seção, localize **Adicionar modelo de máquina Virtual do Azure** e clique em Olá **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="ea97f-140">Within hello **Cloud** section, find **Add Azure Virtual Machine Template** and click hello **Add** button.</span></span>
   
    ![adicionar modelo de vm][add vm template]
5. <span data-ttu-id="ea97f-142">Especifique um nome de serviço de nuvem no hello **nome** campo.</span><span class="sxs-lookup"><span data-stu-id="ea97f-142">Specify a cloud service name in hello **Name** field.</span></span> <span data-ttu-id="ea97f-143">Se o nome hello especificado refere-se tooan existente de serviço de nuvem, Olá VM será provisionado no serviço.</span><span class="sxs-lookup"><span data-stu-id="ea97f-143">If hello name you specify refers tooan existing cloud service, hello VM will be provisioned in that service.</span></span> <span data-ttu-id="ea97f-144">Caso contrário, o Azure criará um novo.</span><span class="sxs-lookup"><span data-stu-id="ea97f-144">Otherwise, Azure will create a new one.</span></span>
6. <span data-ttu-id="ea97f-145">Em Olá **descrição** , digite o texto que descreve o modelo de saudação você está criando.</span><span class="sxs-lookup"><span data-stu-id="ea97f-145">In hello **Description** field, enter text that describes hello template you are creating.</span></span> <span data-ttu-id="ea97f-146">Essas informações são apenas para fins de documentação e não são usadas no provisionamento de uma VM.</span><span class="sxs-lookup"><span data-stu-id="ea97f-146">This information is only for documentary purposes and is not used in provisioning a VM.</span></span>
7. <span data-ttu-id="ea97f-147">Em Olá **rótulos** , digite **linux**.</span><span class="sxs-lookup"><span data-stu-id="ea97f-147">In hello **Labels** field, enter **linux**.</span></span> <span data-ttu-id="ea97f-148">Este rótulo é usado tooidentify Olá modelo que você está criando e é o modelo de saudação de tooreference subsequentemente usada ao criar um trabalho de Hudson.</span><span class="sxs-lookup"><span data-stu-id="ea97f-148">This label is used tooidentify hello template you are creating and is subsequently used tooreference hello template when creating a Hudson job.</span></span>
8. <span data-ttu-id="ea97f-149">Selecione uma região onde Olá VM será criado.</span><span class="sxs-lookup"><span data-stu-id="ea97f-149">Select a region where hello VM will be created.</span></span>
9. <span data-ttu-id="ea97f-150">Selecione o tamanho da VM Olá apropriado.</span><span class="sxs-lookup"><span data-stu-id="ea97f-150">Select hello appropriate VM size.</span></span>
10. <span data-ttu-id="ea97f-151">Especifique uma conta de armazenamento onde Olá VM será criado.</span><span class="sxs-lookup"><span data-stu-id="ea97f-151">Specify a storage account where hello VM will be created.</span></span> <span data-ttu-id="ea97f-152">Certifique-se de que ela está em Olá mesma região que o serviço de nuvem Olá você está usando.</span><span class="sxs-lookup"><span data-stu-id="ea97f-152">Make sure that it is in hello same region as hello cloud service you'll be using.</span></span> <span data-ttu-id="ea97f-153">Se desejar que o novo toobe de armazenamento criada, você pode deixar esse campo em branco.</span><span class="sxs-lookup"><span data-stu-id="ea97f-153">If you want new storage toobe created, you can leave this field blank.</span></span>
11. <span data-ttu-id="ea97f-154">Tempo de retenção Especifica o número de saudação de minutos antes de Hudson exclui um subordinado ocioso.</span><span class="sxs-lookup"><span data-stu-id="ea97f-154">Retention time specifies hello number of minutes before Hudson deletes an idle slave.</span></span> <span data-ttu-id="ea97f-155">Deixe este valor saudação padrão é 60.</span><span class="sxs-lookup"><span data-stu-id="ea97f-155">Leave this at hello default value of 60.</span></span>
12. <span data-ttu-id="ea97f-156">Em **uso**, selecione Olá condição adequada quando esse nó subordinado será usado.</span><span class="sxs-lookup"><span data-stu-id="ea97f-156">In **Usage**, select hello appropriate condition when this slave node will be used.</span></span> <span data-ttu-id="ea97f-157">Por enquanto, selecione **Utilize this node as much as possible**.</span><span class="sxs-lookup"><span data-stu-id="ea97f-157">For now, select **Utilize this node as much as possible**.</span></span>
    
     <span data-ttu-id="ea97f-158">Neste ponto, seu formulário seria toothis um pouco semelhante:</span><span class="sxs-lookup"><span data-stu-id="ea97f-158">At this point, your form would look somewhat similar toothis:</span></span>
    
     ![configuração de modelo][template config]
13. <span data-ttu-id="ea97f-160">Em **família de imagem ou Id** ter toospecify qual imagem do sistema será instalada na sua VM.</span><span class="sxs-lookup"><span data-stu-id="ea97f-160">In **Image Family or Id** you have toospecify what system image will be installed on your VM.</span></span> <span data-ttu-id="ea97f-161">Você pode selecionar em uma lista de famílias de imagens ou especificar uma imagem personalizada.</span><span class="sxs-lookup"><span data-stu-id="ea97f-161">You can either select from a list of image families or specify a custom image.</span></span>
    
     <span data-ttu-id="ea97f-162">Se você quiser tooselect em uma lista de famílias de imagem, digite Olá primeiro caractere (diferencia maiusculas de minúsculas) de nome de família de imagem hello.</span><span class="sxs-lookup"><span data-stu-id="ea97f-162">If you want tooselect from a list of image families, enter hello first character (case-sensitive) of hello image family name.</span></span> <span data-ttu-id="ea97f-163">Por exemplo, se você digitar **U** , será exibida uma lista das famílias de servidores do Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="ea97f-163">For instance, typing **U** will bring up a list of Ubuntu Server families.</span></span> <span data-ttu-id="ea97f-164">Depois que você seleciona na lista de hello, Jenkins usará a versão mais recente de saudação dessa imagem do sistema de família ao provisionar a VM.</span><span class="sxs-lookup"><span data-stu-id="ea97f-164">Once you select from hello list, Jenkins will use hello latest version of that system image from that family when provisioning your VM.</span></span>
    
     ![lista de famílias de SO][OS family list]
    
     <span data-ttu-id="ea97f-166">Se você tiver uma imagem personalizada que você deseja toouse, digite o nome de saudação da imagem personalizada.</span><span class="sxs-lookup"><span data-stu-id="ea97f-166">If you have a custom image that you want toouse instead, enter hello name of that custom image.</span></span> <span data-ttu-id="ea97f-167">Nomes de imagens personalizadas não são mostrados em uma lista para que você tenha tooensure que Olá nome foi digitado corretamente.</span><span class="sxs-lookup"><span data-stu-id="ea97f-167">Custom image names are not shown in a list so you have tooensure that hello name is entered correctly.</span></span>    
    
     <span data-ttu-id="ea97f-168">Para este tutorial, digite **U** toobring uma lista de imagens Ubuntu e selecione **Ubuntu Server 14.04 LTS**.</span><span class="sxs-lookup"><span data-stu-id="ea97f-168">For this tutorial, type **U** toobring up a list of Ubuntu images and select **Ubuntu Server 14.04 LTS**.</span></span>
14. <span data-ttu-id="ea97f-169">Em **Método de Inicialização**, selecione **SSH**.</span><span class="sxs-lookup"><span data-stu-id="ea97f-169">For **Launch method**, select **SSH**.</span></span>
15. <span data-ttu-id="ea97f-170">Script de saudação abaixo de copiar e colar no hello **script Init** campo.</span><span class="sxs-lookup"><span data-stu-id="ea97f-170">Copy hello script below and paste in hello **Init script** field.</span></span>
    
         # Install Java
    
         sudo apt-get -y update
    
         sudo apt-get install -y openjdk-7-jdk
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y openjdk-7-jdk
    
         # Install git
    
         sudo apt-get install -y git
    
         #Install ant
    
         sudo apt-get install -y ant
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y ant
    
     <span data-ttu-id="ea97f-171">Olá **script Init** será executado depois de saudação VM é criada.</span><span class="sxs-lookup"><span data-stu-id="ea97f-171">hello **Init script** will be executed after hello VM is created.</span></span> <span data-ttu-id="ea97f-172">Neste exemplo, o script hello instala ant, Java e git.</span><span class="sxs-lookup"><span data-stu-id="ea97f-172">In this example, hello script installs Java, git, and ant.</span></span>
16. <span data-ttu-id="ea97f-173">Em Olá **Username** e **senha** campos, insira valores de sua preferência para a conta de administrador hello será criada na sua VM.</span><span class="sxs-lookup"><span data-stu-id="ea97f-173">In hello **Username** and **Password** fields, enter your preferred values for hello administrator account that will be created on your VM.</span></span>
17. <span data-ttu-id="ea97f-174">Clique em **Verificar modelo** toocheck se Olá parâmetros especificados são válidos.</span><span class="sxs-lookup"><span data-stu-id="ea97f-174">Click on **Verify Template** toocheck if hello parameters you specified are valid.</span></span>
18. <span data-ttu-id="ea97f-175">Clique em **Save**.</span><span class="sxs-lookup"><span data-stu-id="ea97f-175">Click on **Save**.</span></span>

## <a name="create-a-hudson-job-that-runs-on-a-slave-node-on-azure"></a><span data-ttu-id="ea97f-176">Criar um trabalho do Hudson executado em um nó subordinado no Azure</span><span class="sxs-lookup"><span data-stu-id="ea97f-176">Create a Hudson job that runs on a slave node on Azure</span></span>
<span data-ttu-id="ea97f-177">Nesta seção, você criará uma tarefa do Hudson que será executada em um nó subordinado no Azure.</span><span class="sxs-lookup"><span data-stu-id="ea97f-177">In this section, you'll be creating a Hudson task that will run on a slave node on Azure.</span></span>

1. <span data-ttu-id="ea97f-178">No painel Hudson do hello, clique em **novo trabalho**.</span><span class="sxs-lookup"><span data-stu-id="ea97f-178">In hello Hudson dashboard, click **New Job**.</span></span>
2. <span data-ttu-id="ea97f-179">Insira um nome para o trabalho de saudação que você está criando.</span><span class="sxs-lookup"><span data-stu-id="ea97f-179">Enter a name for hello job you are creating.</span></span>
3. <span data-ttu-id="ea97f-180">Para o tipo de trabalho hello, selecione **criar um trabalho de software livre de estilo**.</span><span class="sxs-lookup"><span data-stu-id="ea97f-180">For hello job type, select **Build a free-style software job**.</span></span>
4. <span data-ttu-id="ea97f-181">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="ea97f-181">Click **OK**.</span></span>
5. <span data-ttu-id="ea97f-182">Na página de configuração de trabalho hello, selecione **restringir onde este projeto pode ser executado**.</span><span class="sxs-lookup"><span data-stu-id="ea97f-182">In hello job configuration page, select **Restrict where this project can be run**.</span></span>
6. <span data-ttu-id="ea97f-183">Selecione **nó e o rótulo do menu** e selecione **linux** (especificamos a este rótulo ao criar o modelo de máquina virtual de saudação na seção anterior Olá).</span><span class="sxs-lookup"><span data-stu-id="ea97f-183">Select **Node and label menu** and select **linux** (we specified this label when creating hello virtual machine template in hello previous section).</span></span>
7. <span data-ttu-id="ea97f-184">Em Olá **criar** seção, clique em **adicionar a etapa de compilação** e selecione **executar shell**.</span><span class="sxs-lookup"><span data-stu-id="ea97f-184">In hello **Build** section, click **Add build step** and select **Execute shell**.</span></span>
8. <span data-ttu-id="ea97f-185">Editar saudação script a seguir, substituindo **{seu nome de conta do github}**, **{o nome do projeto}**, e **{diretório do projeto}** com valores adequados e cole Olá Editar script na área de texto de saudação que aparece.</span><span class="sxs-lookup"><span data-stu-id="ea97f-185">Edit hello following script, replacing **{your github account name}**, **{your project name}**, and **{your project directory}** with appropriate values, and paste hello edited script in hello text area that appears.</span></span>
   
        # Clone from git repo
   
        currentDir="$PWD"
   
        if [ -e {your project directory} ]; then
   
              cd {your project directory}
   
              git pull origin master
   
        else
   
              git clone https://github.com/{your github account name}/{your project name}.git
   
        fi
   
        # change directory tooproject
   
        cd $currentDir/{your project directory}
   
        #Execute build task
   
        ant
9. <span data-ttu-id="ea97f-186">Clique em **Save**.</span><span class="sxs-lookup"><span data-stu-id="ea97f-186">Click on **Save**.</span></span>
10. <span data-ttu-id="ea97f-187">Olá painel Hudson em, encontre o trabalho de saudação que você acabou de criar e clique em Olá **agendar uma compilação** ícone.</span><span class="sxs-lookup"><span data-stu-id="ea97f-187">In hello Hudson dashboard, find hello job you just created and click on hello **Schedule a build** icon.</span></span>

<span data-ttu-id="ea97f-188">Hudson será, em seguida, criar um nó subordinado usando Olá modelo criado na seção anterior hello e executar script hello especificado na etapa de compilação Olá para esta tarefa.</span><span class="sxs-lookup"><span data-stu-id="ea97f-188">Hudson will then create a slave node using hello template created in hello previous section and execute hello script you specified in hello build step for this task.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea97f-189">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ea97f-189">Next Steps</span></span>
<span data-ttu-id="ea97f-190">Para obter mais informações sobre como usar o Azure com Java, consulte Olá [Centro de desenvolvedores de Java do Azure].</span><span class="sxs-lookup"><span data-stu-id="ea97f-190">For more information about using Azure with Java, see hello [Azure Java Developer Center].</span></span>

<!-- URL List -->

[Centro de desenvolvedores de Java do Azure]: https://azure.microsoft.com/develop/java/
[perfil de assinatura]: http://go.microsoft.com/fwlink/?LinkID=396395

<!-- IMG List -->

[add new cloud]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addcloud.png
[configure profile]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-configureprofile.png
[add vm template]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addnewvmtemplate.png
[template config]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-templateconfig1-withdata.png
[OS family list]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-oslist.png

