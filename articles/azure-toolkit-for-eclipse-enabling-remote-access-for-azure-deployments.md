---
title: "Habilitando o Acesso Remoto para implantações do Azure no Eclipse"
description: "Saiba como habilitar o acesso remoto para implantações do Azure usando o Kit de Ferramentas do Azure para Eclipse."
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
ms.openlocfilehash: 654d511bd5a62341f87569317e97360c94a6f26c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="enabling-remote-access-for-azure-deployments-in-eclipse"></a><span data-ttu-id="a9716-103">Habilitando o Acesso Remoto para implantações do Azure no Eclipse</span><span class="sxs-lookup"><span data-stu-id="a9716-103">Enabling Remote Access for Azure Deployments in Eclipse</span></span>
<span data-ttu-id="a9716-104">Para ajudar a solucionar problemas em suas implantações, você pode habilitar e usar o Acesso Remoto a fim de conectar-se à máquina virtual que hospeda sua implantação.</span><span class="sxs-lookup"><span data-stu-id="a9716-104">To help troubleshoot your deployments, you may enable and use Remote Access to connect to the virtual machine hosting your deployment.</span></span> <span data-ttu-id="a9716-105">A funcionalidade Acesso Remoto baseia-se no protocolo RDP (Remote Desktop Protocol).</span><span class="sxs-lookup"><span data-stu-id="a9716-105">The Remote Access functionality relies on the Remote Desktop Protocol (RDP).</span></span> <span data-ttu-id="a9716-106">Você pode configurar o Acesso Remoto para sua implantação após publicá-la no Azure ou, se você estiver usando o Eclipse com um sistema operacional Windows, poderá configurar o Acesso Remoto antes de publicar no Azure.</span><span class="sxs-lookup"><span data-stu-id="a9716-106">You can configure Remote Access for your deployment after you have published it to Azure, or if you are using Eclipse with a Windows operating system, you can configure Remote Access before you publish to Azure.</span></span> <span data-ttu-id="a9716-107">Saiba que você precisará de um cliente de área de trabalho remota compatível com seu sistema operacional a fim de conectar-se à máquina virtual da implantação no Azure.</span><span class="sxs-lookup"><span data-stu-id="a9716-107">Note that you will need a remote desktop client that is compatible with your operating system in order to connect to your deployment's virtual machine in Azure.</span></span>

## <a name="how-to-enable-remote-access-before-you-deploy-to-azure"></a><span data-ttu-id="a9716-108">Como habilitar o Acesso Remoto antes de implantar no Azure</span><span class="sxs-lookup"><span data-stu-id="a9716-108">How to enable Remote Access before you deploy to Azure</span></span>
> [!NOTE]
> <span data-ttu-id="a9716-109">Para habilitar o Acesso Remoto antes de implantar seu aplicativo no Azure, você precisará executar o Eclipse no Windows.</span><span class="sxs-lookup"><span data-stu-id="a9716-109">To enable Remote Access before you deploy your application to Azure, you need to be running Eclipse on Windows.</span></span>
> 
> 

<span data-ttu-id="a9716-110">A imagem a seguir mostra a caixa de diálogo de propriedades do **Acesso Remoto** usada para habilitar o acesso remoto.</span><span class="sxs-lookup"><span data-stu-id="a9716-110">The following image shows the **Remote Access** properties dialog used to enable remote access.</span></span>

![][ic719494]

<span data-ttu-id="a9716-111">Há duas maneiras de exibir a caixa de diálogo de propriedades do **Acesso Remoto** :</span><span class="sxs-lookup"><span data-stu-id="a9716-111">There are two ways to display the **Remote Access** properties dialog:</span></span>

* <span data-ttu-id="a9716-112">Clique no link **Avançado** na seção **Acesso Remoto** da caixa de diálogo **Publicar no Azure**.</span><span class="sxs-lookup"><span data-stu-id="a9716-112">Click the **Advanced** link in the **Remote Access** section of the **Publish to Azure** dialog.</span></span>

* <span data-ttu-id="a9716-113">Abra a caixa de diálogo **Propriedades** de seu projeto do Azure.</span><span class="sxs-lookup"><span data-stu-id="a9716-113">Open the **Properties** dialog of your Azure project.</span></span>

<span data-ttu-id="a9716-114">Ao criar um novo projeto de implantação do Azure, o acesso remoto não estará habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="a9716-114">When you create a new Azure deployment project, the project will not have Remote Access enabled by default.</span></span> <span data-ttu-id="a9716-115">No entanto, você pode habilitá-lo com facilidade especificando o nome de usuário e a senha na caixa de diálogo **Publicar no Azure** .</span><span class="sxs-lookup"><span data-stu-id="a9716-115">However, you can easily enable remote access by specifying the user name and password in the **Publish to Azure** dialog.</span></span> <span data-ttu-id="a9716-116">A senha do Acesso Remoto é criptografada usando certificados X.509.</span><span class="sxs-lookup"><span data-stu-id="a9716-116">The Remote Access password is encrypted using X.509 certificates.</span></span> <span data-ttu-id="a9716-117">Se você não usar seu próprio certificado, a criptografia dependerá de um certificado autoassinado fornecido com o plug-in do Azure para Eclipse.</span><span class="sxs-lookup"><span data-stu-id="a9716-117">If you do not use provide your own certificate, the encryption relies on a self-signed certificate shipped with the Azure Plugin for Eclipse.</span></span> <span data-ttu-id="a9716-118">Esse certificado autoassinado está na pasta **cert** de seu projeto do Azure, armazenado como um arquivo de certificado público (SampleRemoteAccessPublic.cer) e um arquivo de certificado PFX (Troca de Informações Pessoais) (SampleRemoteAccessPrivate.pfx).</span><span class="sxs-lookup"><span data-stu-id="a9716-118">This self-signed certificate is in the **cert** folder of your Azure project, stored both as a public certificate file (SampleRemoteAccessPublic.cer) and as a Personal Information Exchange (PFX) certificate file (SampleRemoteAccessPrivate.pfx).</span></span> <span data-ttu-id="a9716-119">O segundo contém a chave privada do certificado e uma senha padrão, **Password1**.</span><span class="sxs-lookup"><span data-stu-id="a9716-119">The latter contains the private key for the certificate, and it has a default password, **Password1**.</span></span> <span data-ttu-id="a9716-120">No entanto, como essa senha é de conhecimento público, o certificado padrão deve ser usado apenas para fins de aprendizado e não para uma implantação de produção.</span><span class="sxs-lookup"><span data-stu-id="a9716-120">However, since this password is public knowledge, the default certificate should be used only for learning purposes, not for a production deployment.</span></span> <span data-ttu-id="a9716-121">Assim, exceto para fins de aprendizado, quando você quiser habilitar as sessões remotas para suas implantações, deverá clicar no link **Avançado** na caixa de diálogo **Publicar no Azure** para especificar seu próprio certificado.</span><span class="sxs-lookup"><span data-stu-id="a9716-121">So other than for learning purposes, when you want to enabled remote sessions for your deployments, you should click the **Advanced** link in the **Publish to Azure** dialog to specify your own certificate.</span></span> <span data-ttu-id="a9716-122">Observe que você precisará carregar a versão PFX do certificado no serviço hospedado no Portal de Gerenciamento do Azure, para que o Azure possa descriptografar a senha do usuário.</span><span class="sxs-lookup"><span data-stu-id="a9716-122">Note that you'll need to upload the PFX version of the certificate to your hosted service within the Azure Management Portal, so that Azure can decrypt the user password.</span></span>

<span data-ttu-id="a9716-123">O restante do tutorial mostra como habilitar o acesso remoto para um projeto de implantação do Azure criado inicialmente com o acesso remoto desabilitado.</span><span class="sxs-lookup"><span data-stu-id="a9716-123">The remainder of the tutorial shows you how to enable remote access for an Azure deployment project that was initially created with remote access disabled.</span></span> <span data-ttu-id="a9716-124">Para este tutorial, criaremos um novo certificado autoassinado e seu arquivo .pfx terá uma senha escolhida por você.</span><span class="sxs-lookup"><span data-stu-id="a9716-124">For purposes of this tutorial, we'll create a new self-signed certificate, and its .pfx file will have a password of your choice.</span></span> <span data-ttu-id="a9716-125">Você também tem a opção de usar um certificado emitido por uma autoridade de certificação.</span><span class="sxs-lookup"><span data-stu-id="a9716-125">You also have the option of using a certificate issued by a certificate authority.</span></span>

## <a name="how-to-enable-remote-access-after-you-have-deployed-to-azure"></a><span data-ttu-id="a9716-126">Como habilitar o Acesso Remoto após a implantação no Azure</span><span class="sxs-lookup"><span data-stu-id="a9716-126">How to enable Remote Access after you have deployed to Azure</span></span>
<span data-ttu-id="a9716-127">Para habilitar o acesso remoto após a implantação no Azure, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="a9716-127">To enable remote access after you have deployed to Azure, use the following steps:</span></span>

1. <span data-ttu-id="a9716-128">Fazer logon no portal de gerenciamento do Azure usando sua conta do Azure</span><span class="sxs-lookup"><span data-stu-id="a9716-128">Log into the Azure management portal using your Azure account</span></span>

2. <span data-ttu-id="a9716-129">Na lista de **Serviços de Nuvem**, escolha o serviço de nuvem implantado</span><span class="sxs-lookup"><span data-stu-id="a9716-129">In your list of **Cloud Services**, select your deployed cloud service</span></span>

3. <span data-ttu-id="a9716-130">Na página da Web do serviço de nuvem, clique no link **Configurar**</span><span class="sxs-lookup"><span data-stu-id="a9716-130">In the cloud service web page, click the **Configure** link</span></span>

4. <span data-ttu-id="a9716-131">Na parte inferior da página de configuração, clique no link **Remoto**</span><span class="sxs-lookup"><span data-stu-id="a9716-131">On the bottom of the configuration page, click the **Remote** link</span></span>

5. <span data-ttu-id="a9716-132">Quando a caixa de diálogo pop-up aparecer:</span><span class="sxs-lookup"><span data-stu-id="a9716-132">When the pop-up dialog box appears:</span></span>
   
   * <span data-ttu-id="a9716-133">Especifique a Função para a qual você deseja habilitar o acesso remoto</span><span class="sxs-lookup"><span data-stu-id="a9716-133">Specify the Role you for which you want to enable remote access</span></span>

   * <span data-ttu-id="a9716-134">Clique para marcar a caixa de seleção **Habilitar Área de Trabalho Remota**</span><span class="sxs-lookup"><span data-stu-id="a9716-134">Click to select the **Enable Remote Desktop** checkbox</span></span>
   
   * <span data-ttu-id="a9716-135">Especifique um nome de usuário e senha que você deseja usar para o acesso remoto</span><span class="sxs-lookup"><span data-stu-id="a9716-135">Specify a user name and password you want to use for remote access</span></span>
   
   * <span data-ttu-id="a9716-136">Escolher o certificado a ser usado</span><span class="sxs-lookup"><span data-stu-id="a9716-136">Select the certificate to use</span></span>

6. <span data-ttu-id="a9716-137">Clique em **OK**</span><span class="sxs-lookup"><span data-stu-id="a9716-137">Click **OK**</span></span> 

<span data-ttu-id="a9716-138">Você verá uma mensagem informando que a alteração da configuração está em andamento, o que pode levar alguns minutos para ser concluído.</span><span class="sxs-lookup"><span data-stu-id="a9716-138">You will see a message stating that your configuration change is in progress, which may take a few minutes to complete.</span></span> <span data-ttu-id="a9716-139">Após a conclusão da alteração de configuração, execute as etapas na seção **Para fazer logon remotamente** posteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="a9716-139">After the configuration change has completed, follow the steps in the **To log in remotely** section later in this article.</span></span>

## <a name="how-to-enable-remote-access-in-your-package"></a><span data-ttu-id="a9716-140">Como habilitar o Acesso Remoto em seu pacote</span><span class="sxs-lookup"><span data-stu-id="a9716-140">How to enable Remote Access in your package</span></span>
1. <span data-ttu-id="a9716-141">No painel Gerenciador de Projetos do Eclipse, clique com o botão direito no projeto do Azure e clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="a9716-141">Within Eclipse's Project Explorer pane, right-click your Azure project and click **Properties**.</span></span>

2. <span data-ttu-id="a9716-142">Na caixa de diálogo **Propriedades**, expanda **Azure** no painel esquerdo e clique em **Acesso Remoto**.</span><span class="sxs-lookup"><span data-stu-id="a9716-142">In the **Properties** dialog, expand **Azure** in the left-hand pane and click **Remote Access**.</span></span>

3. <span data-ttu-id="a9716-143">Na caixa de diálogo **Acesso Remoto**, verifique se **Habilitar todas as funções para aceitar as Conexões da Área de Trabalho Remota com essas credenciais de logon** está marcada.</span><span class="sxs-lookup"><span data-stu-id="a9716-143">In the **Remote Access** dialog, ensure **Enable all roles to accept Remote Desktop Connections with these login credentials** is checked.</span></span>

4. <span data-ttu-id="a9716-144">Especifique um nome de usuário para a conexão de Área de Trabalho Remota.</span><span class="sxs-lookup"><span data-stu-id="a9716-144">Specify a user name for the Remote Desktop connection.</span></span>

5. <span data-ttu-id="a9716-145">Especifique e confirme a senha para o usuário.</span><span class="sxs-lookup"><span data-stu-id="a9716-145">Specify and confirm the password for the user.</span></span> <span data-ttu-id="a9716-146">Os valores de nome de usuário e senha definidos nesta caixa de diálogo serão usados quando você fizer uma conexão de Área de Trabalho Remota.</span><span class="sxs-lookup"><span data-stu-id="a9716-146">The user name and password values set in this dialog will be used when you make a Remote Desktop connection.</span></span> <span data-ttu-id="a9716-147">(Observe que essa é uma senha separada da sua senha PFX).</span><span class="sxs-lookup"><span data-stu-id="a9716-147">(Note that this is a separate password from your PFX password.)</span></span>

6. <span data-ttu-id="a9716-148">Especifique a data de expiração da conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="a9716-148">Specify the expiration date for the user account.</span></span>

7. <span data-ttu-id="a9716-149">Clique em **Novo** para criar um novo certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="a9716-149">Click **New** to create a new self-signed certificate.</span></span> <span data-ttu-id="a9716-150">(Como alternativa, você pode selecionar um certificado de seu espaço de trabalho ou sistema de arquivos por meio dos botões **Espaço de Trabalho** ou **Sistema de Arquivos**, respectivamente, mas este tutorial, criaremos um novo certificado.)</span><span class="sxs-lookup"><span data-stu-id="a9716-150">(Alternatively, you could select a certificate from your workspace or file system through the **Workspace** or **FileSystem** buttons, respectively, but for purposes of this tutorial we'll create a new certificate.)</span></span>

   * <span data-ttu-id="a9716-151">Na caixa de diálogo **Novo Certificado** , especifique e confirme a senha que você usará para o arquivo PFX.</span><span class="sxs-lookup"><span data-stu-id="a9716-151">In the **New Certificate** dialog, specify and confirm the password you'll use for your PFX file.</span></span>

   * <span data-ttu-id="a9716-152">Aceite o valor fornecido para **Nome (CN)**ou use um nome personalizado.</span><span class="sxs-lookup"><span data-stu-id="a9716-152">Accept the value provided for **Name (CN)**, or use a custom name.</span></span>

   * <span data-ttu-id="a9716-153">Especifique o caminho e o nome de arquivo no qual o novo certificado, no formato .cer, será salvo.</span><span class="sxs-lookup"><span data-stu-id="a9716-153">Specify the path and file name where the new certificate, in .cer form, will be saved.</span></span> <span data-ttu-id="a9716-154">Para essa etapa e a próxima, você poderá usar a pasta **cert** de seu projeto do Azure, mas sinta-se à vontade para escolher outro local.</span><span class="sxs-lookup"><span data-stu-id="a9716-154">For this step and the next step, you could use the **cert** folder of your Azure project, but you're free to choose another location.</span></span> <span data-ttu-id="a9716-155">Para este tutorial, usaremos **c:\mycert\mycert.cer**.</span><span class="sxs-lookup"><span data-stu-id="a9716-155">For purposes of this tutorial, we'll use **c:\mycert\mycert.cer**.</span></span> <span data-ttu-id="a9716-156">(Crie a pasta **c:\mycert** antes de prosseguir ou use uma pasta existente, se desejado.)</span><span class="sxs-lookup"><span data-stu-id="a9716-156">(Create the **c:\mycert** folder prior to proceeding, or use an existing folder if desired.)</span></span>

   * <span data-ttu-id="a9716-157">Especifique o caminho e o nome de arquivo no qual o novo certificado e sua chave privada, no formato .pfx, serão salvos.</span><span class="sxs-lookup"><span data-stu-id="a9716-157">Specify the path and file name where the new certificate and its private key, in .pfx form, will be saved.</span></span> <span data-ttu-id="a9716-158">Para este tutorial, usaremos **c:\mycert\mycert.pfx**.</span><span class="sxs-lookup"><span data-stu-id="a9716-158">For purposes of this tutorial, we'll use **c:\mycert\mycert.pfx**.</span></span> <span data-ttu-id="a9716-159">Sua caixa de diálogo **Novo Certificado** deve ser parecida com a seguinte (atualize os caminhos da pasta se você não usou **c:\mycert**):</span><span class="sxs-lookup"><span data-stu-id="a9716-159">Your **New Certificate** dialog should look similar to the following (update the folder paths if you did not use **c:\mycert**):</span></span>
     
      ![][ic712275]

   * <span data-ttu-id="a9716-160">Clique em **OK** para fechar a caixa de diálogo **Novo Certificado**.</span><span class="sxs-lookup"><span data-stu-id="a9716-160">Click **OK** to close the **New Certificate** dialog.</span></span>

8. <span data-ttu-id="a9716-161">A caixa de diálogo **Acesso Remoto** deve ser semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="a9716-161">Your **Remote Access** dialog should look similar to the following:</span></span></p>
   
   ![][ic719495]

9. <span data-ttu-id="a9716-162">Clique em **OK** para fechar a caixa de diálogo **cesso Remoto**.</span><span class="sxs-lookup"><span data-stu-id="a9716-162">Click **OK** to close the **Remote Access** dialog.</span></span>

<span data-ttu-id="a9716-163">Recrie seu aplicativo, com a compilação definida para implantação em nuvem.</span><span class="sxs-lookup"><span data-stu-id="a9716-163">Rebuild your application, with the build set for deployment to cloud.</span></span>

## <a name="to-log-in-remotely"></a><span data-ttu-id="a9716-164">Para fazer logon remotamente</span><span class="sxs-lookup"><span data-stu-id="a9716-164">To log in remotely</span></span>
<span data-ttu-id="a9716-165">Quando a sua instância de função estiver pronta, você poderá fazer logon remotamente na máquina virtual que está hospedando o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a9716-165">Once your role instance is ready, you can remotely log in to the virtual machine that is hosting your application.</span></span>

* <span data-ttu-id="a9716-166">Se você estiver usando o Eclipse no Windows e selecionou a opção **Iniciar área de trabalho remota na implantação** durante a implantação do Azure, receberá uma tela de logon para a Conexão de Área de Trabalho Remota quando a implantação for iniciada.</span><span class="sxs-lookup"><span data-stu-id="a9716-166">If are using Eclipse on Windows and you selected the **Start remote desktop on deploy** option during your deployment to Azure, you will be presented with a Remote Desktop Connection logon screen when your deployment starts.</span></span> <span data-ttu-id="a9716-167">Quando receber a solicitação de nome de usuário e senha, insira os valores que você especificou para o usuário remoto e assim conseguirá fazer logon.</span><span class="sxs-lookup"><span data-stu-id="a9716-167">When you are prompted for the user name and password, enter the values that you specified for the remote user and will be able to log in.</span></span>

* <span data-ttu-id="a9716-168">Outra maneira de fazer logon remotamente é por meio do <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Portal de Gerenciamento do Azure</a>:</span><span class="sxs-lookup"><span data-stu-id="a9716-168">Another way to log in remotely is through the <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Azure Management Portal</a>:</span></span>
  
  * <span data-ttu-id="a9716-169">Na exibição **Serviços de Nuvem** do portal de Gerenciamento do Azure, clique em seu serviço de nuvem, clique em **Instâncias**, em uma instância específica, em seguida, clique no botão **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="a9716-169">Within the **Cloud Services** view of the Azure Management portal, click your cloud service, click **Instances**, click a specific instance, and then click the **Connect** button.</span></span> <span data-ttu-id="a9716-170">O botão **Conectar** aparece da seguinte forma na barra de comandos:</span><span class="sxs-lookup"><span data-stu-id="a9716-170">The **Connect** button appears as the following in the command bar:</span></span>
    
      ![][ic659273]

  * <span data-ttu-id="a9716-171">Depois de clicar no botão **Conectar** , você receberá uma solicitação para abrir um arquivo RDP.</span><span class="sxs-lookup"><span data-stu-id="a9716-171">After clicking the **Connect** button, you will be prompted to open an RDP file.</span></span> <span data-ttu-id="a9716-172">Abra o arquivo e siga os prompts.</span><span class="sxs-lookup"><span data-stu-id="a9716-172">Open the file and follow the prompts.</span></span> <span data-ttu-id="a9716-173">(Você pode também salvar esse arquivo em seu computador local e depois executar o arquivo clicando duas vezes nele para fazer logon remoto em sua máquina virtual sem a necessidade de acessar primeiro o portal de gerenciamento).</span><span class="sxs-lookup"><span data-stu-id="a9716-173">(You could also save this file to your local computer, and then run the file by double-clicking it to remote log in to your virtual machine without needing to first go the management portal.)</span></span>

  * <span data-ttu-id="a9716-174">Quando receber a solicitação de nome de usuário e senha, insira os valores que você especificou para o usuário remoto e assim conseguirá fazer logon.</span><span class="sxs-lookup"><span data-stu-id="a9716-174">When you are prompted for the user name and password, enter the values that you specified for the remote user and will be able to log in.</span></span>

> [!NOTE]
> <span data-ttu-id="a9716-175">Se você estiver em um sistema operacional que não seja o Windows, será necessário usar um cliente de Área de Trabalho Remota compatível com o sistema operacional e executar as etapas para definir esse cliente com as configurações no arquivo RDP baixado.</span><span class="sxs-lookup"><span data-stu-id="a9716-175">If you are on a non-Windows operating system, you need to use a Remote Desktop client that is compatible with your operating system and follow the steps to configure that client with the settings in the RDP file that you downloaded.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="a9716-176">Consulte também</span><span class="sxs-lookup"><span data-stu-id="a9716-176">See Also</span></span>
<span data-ttu-id="a9716-177">[Kit de Ferramentas do Azure para Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="a9716-177">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="a9716-178">[Criar um aplicativo Hello World para Azure no Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="a9716-178">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="a9716-179">[Instalar o Kit de Ferramentas do Azure para Eclipse][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="a9716-179">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="a9716-180">Para saber mais sobre como usar o Azure com o Java, confira o [Centro de Desenvolvedores Java do Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="a9716-180">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic712275]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic712275.png
[ic719495]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719495.png
[ic719494]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719494.png
[ic659273]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic659273.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690951.aspx -->
