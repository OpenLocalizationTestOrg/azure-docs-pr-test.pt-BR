---
title: "aaaEnabling acesso remoto para implantações do Azure no Eclipse"
description: "Saiba como tooenable remoto acessa para implantações do Azure usando Olá Kit de ferramentas do Azure para Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: b6150006-9a7f-4d83-be18-d35ec780c7c5
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 00c2bf22c1f3ec792098f154f771c87506e87881
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-remote-access-for-azure-deployments-in-eclipse"></a><span data-ttu-id="eeaa7-103">Habilitando o Acesso Remoto para implantações do Azure no Eclipse</span><span class="sxs-lookup"><span data-stu-id="eeaa7-103">Enabling Remote Access for Azure Deployments in Eclipse</span></span>
<span data-ttu-id="eeaa7-104">toohelp solucionar problemas de suas implantações, você pode habilitar e usar o acesso remoto tooconnect toohello máquina virtual que hospeda sua implantação.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-104">toohelp troubleshoot your deployments, you may enable and use Remote Access tooconnect toohello virtual machine hosting your deployment.</span></span> <span data-ttu-id="eeaa7-105">Olá funcionalidade de acesso remoto depende Olá protocolo de área de trabalho remota (RDP).</span><span class="sxs-lookup"><span data-stu-id="eeaa7-105">hello Remote Access functionality relies on hello Remote Desktop Protocol (RDP).</span></span> <span data-ttu-id="eeaa7-106">Você pode configurar o acesso remoto para sua implantação depois que você tenha publicado tooAzure, ou se você estiver usando o Eclipse com um sistema operacional Windows, você pode configurar o acesso remoto antes de publicar tooAzure.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-106">You can configure Remote Access for your deployment after you have published it tooAzure, or if you are using Eclipse with a Windows operating system, you can configure Remote Access before you publish tooAzure.</span></span> <span data-ttu-id="eeaa7-107">Observe que você precisará de um cliente de desktop remoto é compatível com o sistema operacional na máquina de virtual da implantação do pedido tooconnect tooyour no Azure.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-107">Note that you will need a remote desktop client that is compatible with your operating system in order tooconnect tooyour deployment's virtual machine in Azure.</span></span>

## <a name="how-tooenable-remote-access-before-you-deploy-tooazure"></a><span data-ttu-id="eeaa7-108">Como tooenable acesso remoto antes de implantar tooAzure</span><span class="sxs-lookup"><span data-stu-id="eeaa7-108">How tooenable Remote Access before you deploy tooAzure</span></span>
> [!NOTE]
> <span data-ttu-id="eeaa7-109">tooenable acesso remoto antes de implantar seu aplicativo tooAzure, você precisa toobe executando o Eclipse no Windows.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-109">tooenable Remote Access before you deploy your application tooAzure, you need toobe running Eclipse on Windows.</span></span>
> 
> 

<span data-ttu-id="eeaa7-110">Olá, imagem a seguir mostra Olá **acesso remoto** caixa de diálogo de propriedades usada tooenable o acesso remoto.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-110">hello following image shows hello **Remote Access** properties dialog used tooenable remote access.</span></span>

![][ic719494]

<span data-ttu-id="eeaa7-111">Há dois Olá toodisplay de maneiras **acesso remoto** caixa de diálogo de propriedades:</span><span class="sxs-lookup"><span data-stu-id="eeaa7-111">There are two ways toodisplay hello **Remote Access** properties dialog:</span></span>

* <span data-ttu-id="eeaa7-112">Clique em Olá **avançado** link no hello **acesso remoto** seção Olá **publicar tooAzure** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-112">Click hello **Advanced** link in hello **Remote Access** section of hello **Publish tooAzure** dialog.</span></span>

* <span data-ttu-id="eeaa7-113">Olá abrir **propriedades** caixa de diálogo do projeto do Azure.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-113">Open hello **Properties** dialog of your Azure project.</span></span>

<span data-ttu-id="eeaa7-114">Quando você cria um novo projeto de implantação do Azure, o projeto de saudação não terá acesso remoto habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-114">When you create a new Azure deployment project, hello project will not have Remote Access enabled by default.</span></span> <span data-ttu-id="eeaa7-115">No entanto, você pode facilmente habilitar acesso remoto especificando Olá nome de usuário e senha em Olá **publicar tooAzure** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-115">However, you can easily enable remote access by specifying hello user name and password in hello **Publish tooAzure** dialog.</span></span> <span data-ttu-id="eeaa7-116">senha de acesso remoto de saudação é criptografada usando certificados x. 509.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-116">hello Remote Access password is encrypted using X.509 certificates.</span></span> <span data-ttu-id="eeaa7-117">Se você não usar fornecer seu próprio certificado, Olá criptografia baseia-se em um certificado autoassinado fornecido com hello plug-in do Azure para Eclipse.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-117">If you do not use provide your own certificate, hello encryption relies on a self-signed certificate shipped with hello Azure Plugin for Eclipse.</span></span> <span data-ttu-id="eeaa7-118">Este certificado autoassinado está Olá **cert** pasta do seu projeto do Azure, armazenado como um arquivo de certificado público (SampleRemoteAccessPublic.cer) e como um Personal Information Exchange (PFX) (arquivo de certificado SampleRemoteAccessPrivate.pfx).</span><span class="sxs-lookup"><span data-stu-id="eeaa7-118">This self-signed certificate is in hello **cert** folder of your Azure project, stored both as a public certificate file (SampleRemoteAccessPublic.cer) and as a Personal Information Exchange (PFX) certificate file (SampleRemoteAccessPrivate.pfx).</span></span> <span data-ttu-id="eeaa7-119">Olá último contém a chave particular Olá certificado hello e tem uma senha padrão, **Password1**.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-119">hello latter contains hello private key for hello certificate, and it has a default password, **Password1**.</span></span> <span data-ttu-id="eeaa7-120">No entanto, desde que essa senha é de conhecimento público, certificado padrão de saudação deve ser usado apenas para fins de aprendizado, não para uma implantação de produção.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-120">However, since this password is public knowledge, hello default certificate should be used only for learning purposes, not for a production deployment.</span></span> <span data-ttu-id="eeaa7-121">Assim que para fins de aprendizado, quando você quiser tooenabled a sessões remotas para suas implantações, clique em Olá **avançado** link no hello **publicar tooAzure** toospecify da caixa de diálogo seu próprio certificado.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-121">So other than for learning purposes, when you want tooenabled remote sessions for your deployments, you should click hello **Advanced** link in hello **Publish tooAzure** dialog toospecify your own certificate.</span></span> <span data-ttu-id="eeaa7-122">Observe que você precisará tooupload Olá PFX versão Olá certificado tooyour hospedado do serviço de dentro Olá Portal de gerenciamento do Azure, para que o Azure possa descriptografar a senha do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-122">Note that you'll need tooupload hello PFX version of hello certificate tooyour hosted service within hello Azure Management Portal, so that Azure can decrypt hello user password.</span></span>

<span data-ttu-id="eeaa7-123">restante de saudação do tutorial Olá mostra como acessar o tooenable remoto para um projeto de implantação do Azure que foi inicialmente criado com o acesso remoto desativado.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-123">hello remainder of hello tutorial shows you how tooenable remote access for an Azure deployment project that was initially created with remote access disabled.</span></span> <span data-ttu-id="eeaa7-124">Para este tutorial, criaremos um novo certificado autoassinado e seu arquivo .pfx terá uma senha escolhida por você.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-124">For purposes of this tutorial, we'll create a new self-signed certificate, and its .pfx file will have a password of your choice.</span></span> <span data-ttu-id="eeaa7-125">Você também tem a opção de saudação do uso de um certificado emitido por uma autoridade de certificação.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-125">You also have hello option of using a certificate issued by a certificate authority.</span></span>

## <a name="how-tooenable-remote-access-after-you-have-deployed-tooazure"></a><span data-ttu-id="eeaa7-126">Como tooenable acesso remoto depois que você implantou tooAzure</span><span class="sxs-lookup"><span data-stu-id="eeaa7-126">How tooenable Remote Access after you have deployed tooAzure</span></span>
<span data-ttu-id="eeaa7-127">tooenable acesso remoto depois que você implantou tooAzure, Olá use as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="eeaa7-127">tooenable remote access after you have deployed tooAzure, use hello following steps:</span></span>

1. <span data-ttu-id="eeaa7-128">Faça logon no portal de gerenciamento do Azure hello usando sua conta do Azure</span><span class="sxs-lookup"><span data-stu-id="eeaa7-128">Log into hello Azure management portal using your Azure account</span></span>

2. <span data-ttu-id="eeaa7-129">Na lista de **Serviços de Nuvem**, escolha o serviço de nuvem implantado</span><span class="sxs-lookup"><span data-stu-id="eeaa7-129">In your list of **Cloud Services**, select your deployed cloud service</span></span>

3. <span data-ttu-id="eeaa7-130">Na página de web de serviço de nuvem hello, clique em Olá **configurar** link</span><span class="sxs-lookup"><span data-stu-id="eeaa7-130">In hello cloud service web page, click hello **Configure** link</span></span>

4. <span data-ttu-id="eeaa7-131">Na parte inferior de saudação da página de configuração hello, clique em Olá **remoto** link</span><span class="sxs-lookup"><span data-stu-id="eeaa7-131">On hello bottom of hello configuration page, click hello **Remote** link</span></span>

5. <span data-ttu-id="eeaa7-132">Quando for exibida a caixa de diálogo pop-up de saudação:</span><span class="sxs-lookup"><span data-stu-id="eeaa7-132">When hello pop-up dialog box appears:</span></span>
   
   * <span data-ttu-id="eeaa7-133">Especificar Olá função você para o qual você deseja acesso remoto tooenable</span><span class="sxs-lookup"><span data-stu-id="eeaa7-133">Specify hello Role you for which you want tooenable remote access</span></span>

   * <span data-ttu-id="eeaa7-134">Clique em Olá tooselect **habilitar área de trabalho remota** caixa de seleção</span><span class="sxs-lookup"><span data-stu-id="eeaa7-134">Click tooselect hello **Enable Remote Desktop** checkbox</span></span>
   
   * <span data-ttu-id="eeaa7-135">Especifique um nome de usuário e senha que você deseja toouse para acesso remoto</span><span class="sxs-lookup"><span data-stu-id="eeaa7-135">Specify a user name and password you want toouse for remote access</span></span>
   
   * <span data-ttu-id="eeaa7-136">Selecione Olá certificado toouse</span><span class="sxs-lookup"><span data-stu-id="eeaa7-136">Select hello certificate toouse</span></span>

6. <span data-ttu-id="eeaa7-137">Clique em **OK**</span><span class="sxs-lookup"><span data-stu-id="eeaa7-137">Click **OK**</span></span> 

<span data-ttu-id="eeaa7-138">Você verá uma mensagem informando que a alteração da configuração está em andamento, o que pode levar alguns toocomplete de minutos.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-138">You will see a message stating that your configuration change is in progress, which may take a few minutes toocomplete.</span></span> <span data-ttu-id="eeaa7-139">Após a alteração de configuração hello, siga as etapas de Olá Olá **toolog em remotamente** seção mais adiante neste artigo.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-139">After hello configuration change has completed, follow hello steps in hello **toolog in remotely** section later in this article.</span></span>

## <a name="how-tooenable-remote-access-in-your-package"></a><span data-ttu-id="eeaa7-140">Como tooenable de acesso remoto no pacote</span><span class="sxs-lookup"><span data-stu-id="eeaa7-140">How tooenable Remote Access in your package</span></span>
1. <span data-ttu-id="eeaa7-141">No painel Gerenciador de Projetos do Eclipse, clique com o botão direito no projeto do Azure e clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-141">Within Eclipse's Project Explorer pane, right-click your Azure project and click **Properties**.</span></span>

2. <span data-ttu-id="eeaa7-142">Em Olá **propriedades** caixa de diálogo, expanda **Azure** no painel esquerdo do hello e clique em **acesso remoto**.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-142">In hello **Properties** dialog, expand **Azure** in hello left-hand pane and click **Remote Access**.</span></span>

3. <span data-ttu-id="eeaa7-143">Em Olá **acesso remoto** caixa de diálogo, certifique-se de **habilitar todas as funções tooaccept conexões de área de trabalho remota com essas credenciais de logon** é verificada.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-143">In hello **Remote Access** dialog, ensure **Enable all roles tooaccept Remote Desktop Connections with these login credentials** is checked.</span></span>

4. <span data-ttu-id="eeaa7-144">Especifique um nome de usuário para Olá conexão de área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-144">Specify a user name for hello Remote Desktop connection.</span></span>

5. <span data-ttu-id="eeaa7-145">Especifique e confirme a senha de saudação do usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-145">Specify and confirm hello password for hello user.</span></span> <span data-ttu-id="eeaa7-146">produtos de valores de nome e a senha de usuário Olá definidos nesta caixa de diálogo serão usados quando você faz uma conexão de área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-146">hello user name and password values set in this dialog will be used when you make a Remote Desktop connection.</span></span> <span data-ttu-id="eeaa7-147">(Observe que essa é uma senha separada da sua senha PFX).</span><span class="sxs-lookup"><span data-stu-id="eeaa7-147">(Note that this is a separate password from your PFX password.)</span></span>

6. <span data-ttu-id="eeaa7-148">Especifique a data de validade de Olá Olá conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-148">Specify hello expiration date for hello user account.</span></span>

7. <span data-ttu-id="eeaa7-149">Clique em **novo** toocreate um novo certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-149">Click **New** toocreate a new self-signed certificate.</span></span> <span data-ttu-id="eeaa7-150">(Como alternativa, você pode selecionar um certificado de seu espaço de trabalho ou sistema de arquivos por meio de saudação **espaço de trabalho** ou **FileSystem** botões, respectivamente, mas para fins deste tutorial, criaremos um novo certificado).</span><span class="sxs-lookup"><span data-stu-id="eeaa7-150">(Alternatively, you could select a certificate from your workspace or file system through hello **Workspace** or **FileSystem** buttons, respectively, but for purposes of this tutorial we'll create a new certificate.)</span></span>

   * <span data-ttu-id="eeaa7-151">Em Olá **novo certificado** caixa de diálogo, especifique e confirme a senha de saudação que será usada para o arquivo PFX.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-151">In hello **New Certificate** dialog, specify and confirm hello password you'll use for your PFX file.</span></span>

   * <span data-ttu-id="eeaa7-152">Aceite Olá valor fornecido para **nome (CN)**, ou use um nome personalizado.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-152">Accept hello value provided for **Name (CN)**, or use a custom name.</span></span>

   * <span data-ttu-id="eeaa7-153">Especifique Olá caminho e nome de arquivo onde Olá novo certificado, no formato. cer, será salvo.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-153">Specify hello path and file name where hello new certificate, in .cer form, will be saved.</span></span> <span data-ttu-id="eeaa7-154">Para esta etapa e Olá próxima, você poderá usar Olá **cert** pasta do seu projeto do Azure, mas estiver livre toochoose outro local.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-154">For this step and hello next step, you could use hello **cert** folder of your Azure project, but you're free toochoose another location.</span></span> <span data-ttu-id="eeaa7-155">Para este tutorial, usaremos **c:\mycert\mycert.cer**.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-155">For purposes of this tutorial, we'll use **c:\mycert\mycert.cer**.</span></span> <span data-ttu-id="eeaa7-156">(Criar hello **c:\mycert** tooproceeding anterior da pasta ou usar uma pasta existente, se desejado.)</span><span class="sxs-lookup"><span data-stu-id="eeaa7-156">(Create hello **c:\mycert** folder prior tooproceeding, or use an existing folder if desired.)</span></span>

   * <span data-ttu-id="eeaa7-157">Especifique Olá caminho e nome de arquivo onde Olá novo certificado e sua chave privada, no formato. pfx, serão salvos.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-157">Specify hello path and file name where hello new certificate and its private key, in .pfx form, will be saved.</span></span> <span data-ttu-id="eeaa7-158">Para este tutorial, usaremos **c:\mycert\mycert.pfx**.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-158">For purposes of this tutorial, we'll use **c:\mycert\mycert.pfx**.</span></span> <span data-ttu-id="eeaa7-159">O **novo certificado** caixa de diálogo deve parecer semelhante seguinte de toohello (atualizar os caminhos de pasta Olá se você não usou **c:\mycert**):</span><span class="sxs-lookup"><span data-stu-id="eeaa7-159">Your **New Certificate** dialog should look similar toohello following (update hello folder paths if you did not use **c:\mycert**):</span></span>
     
      ![][ic712275]

   * <span data-ttu-id="eeaa7-160">Clique em **Okey** tooclose Olá **novo certificado** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-160">Click **OK** tooclose hello **New Certificate** dialog.</span></span>

8. <span data-ttu-id="eeaa7-161">O **acesso remoto** caixa de diálogo deve ser a seguir toohello semelhante:</span><span class="sxs-lookup"><span data-stu-id="eeaa7-161">Your **Remote Access** dialog should look similar toohello following:</span></span></p>
   
   ![][ic719495]

9. <span data-ttu-id="eeaa7-162">Clique em **Okey** tooclose Olá **acesso remoto** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-162">Click **OK** tooclose hello **Remote Access** dialog.</span></span>

<span data-ttu-id="eeaa7-163">Recrie seu aplicativo, com hello criar conjunto de toocloud de implantação.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-163">Rebuild your application, with hello build set for deployment toocloud.</span></span>

## <a name="toolog-in-remotely"></a><span data-ttu-id="eeaa7-164">toolog em remotamente</span><span class="sxs-lookup"><span data-stu-id="eeaa7-164">toolog in remotely</span></span>
<span data-ttu-id="eeaa7-165">Quando sua instância de função estiver pronta, você poderá fazer logon remotamente na máquina virtual toohello que está hospedando o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-165">Once your role instance is ready, you can remotely log in toohello virtual machine that is hosting your application.</span></span>

* <span data-ttu-id="eeaa7-166">Se estiver usando o Eclipse no Windows e selecionado Olá **implantação de área de trabalho remota no início** opção durante tooAzure sua implantação, você verá uma tela de logon da Conexão de área de trabalho remota quando sua implantação for iniciada.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-166">If are using Eclipse on Windows and you selected hello **Start remote desktop on deploy** option during your deployment tooAzure, you will be presented with a Remote Desktop Connection logon screen when your deployment starts.</span></span> <span data-ttu-id="eeaa7-167">Quando você for solicitado Olá nome de usuário e senha, insira valores hello que você especificou para o usuário remoto hello e será capaz de toolog no.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-167">When you are prompted for hello user name and password, enter hello values that you specified for hello remote user and will be able toolog in.</span></span>

* <span data-ttu-id="eeaa7-168">Toolog de outra forma no remotamente é por meio de saudação <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Portal de gerenciamento</a>:</span><span class="sxs-lookup"><span data-stu-id="eeaa7-168">Another way toolog in remotely is through hello <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Azure Management Portal</a>:</span></span>
  
  * <span data-ttu-id="eeaa7-169">Dentro de saudação **serviços de nuvem** exibição de saudação portal de gerenciamento do Azure, clique em seu serviço de nuvem, **instâncias**, clique em uma instância específica e, em seguida, clique em Olá **conectar**botão.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-169">Within hello **Cloud Services** view of hello Azure Management portal, click your cloud service, click **Instances**, click a specific instance, and then click hello **Connect** button.</span></span> <span data-ttu-id="eeaa7-170">Olá **conectar** botão aparece como a seguir na barra de comandos Olá Olá:</span><span class="sxs-lookup"><span data-stu-id="eeaa7-170">hello **Connect** button appears as hello following in hello command bar:</span></span>
    
      ![][ic659273]

  * <span data-ttu-id="eeaa7-171">Depois de clicar em Olá **conectar** botão, você será solicitado tooopen um arquivo RDP.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-171">After clicking hello **Connect** button, you will be prompted tooopen an RDP file.</span></span> <span data-ttu-id="eeaa7-172">Abra o arquivo hello e siga os prompts de saudação.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-172">Open hello file and follow hello prompts.</span></span> <span data-ttu-id="eeaa7-173">(Você pode também salvar este computador local do arquivo tooyour e executar arquivo hello clicando duas vezes nele log tooremote no tooyour máquina virtual sem a necessidade de toofirst acesse o portal de gerenciamento hello.)</span><span class="sxs-lookup"><span data-stu-id="eeaa7-173">(You could also save this file tooyour local computer, and then run hello file by double-clicking it tooremote log in tooyour virtual machine without needing toofirst go hello management portal.)</span></span>

  * <span data-ttu-id="eeaa7-174">Quando você for solicitado Olá nome de usuário e senha, insira valores hello que você especificou para o usuário remoto hello e será capaz de toolog no.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-174">When you are prompted for hello user name and password, enter hello values that you specified for hello remote user and will be able toolog in.</span></span>

> [!NOTE]
> <span data-ttu-id="eeaa7-175">Se você estiver usando um sistema operacional Windows não, você precisa toouse um cliente de área de trabalho remota que é compatível com o sistema operacional e siga Olá etapas tooconfigure que o cliente com as configurações de saudação no arquivo RDP Olá que você baixou.</span><span class="sxs-lookup"><span data-stu-id="eeaa7-175">If you are on a non-Windows operating system, you need toouse a Remote Desktop client that is compatible with your operating system and follow hello steps tooconfigure that client with hello settings in hello RDP file that you downloaded.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="eeaa7-176">Consulte também</span><span class="sxs-lookup"><span data-stu-id="eeaa7-176">See Also</span></span>
<span data-ttu-id="eeaa7-177">[Kit de Ferramentas do Azure para Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="eeaa7-177">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="eeaa7-178">[Criar um aplicativo Hello World para Azure no Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="eeaa7-178">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="eeaa7-179">[Saudação de instalar o Kit de ferramentas do Azure para Eclipse][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="eeaa7-179">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="eeaa7-180">Para obter mais informações sobre como usar o Azure com Java, consulte Olá [Centro de desenvolvedores de Java do Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="eeaa7-180">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic712275]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic712275.png
[ic719495]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719495.png
[ic719494]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719494.png
[ic659273]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic659273.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690951.aspx -->
