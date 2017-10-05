---
title: "Configurar Apache Tomcat em uma máquina virtual Linux | Microsoft Docs"
description: "Saiba como configurar o Apache Tomcat7 usando Máquinas Virtuais do Azure que executam o Linux."
services: virtual-machines-linux
documentationcenter: 
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 45ecc89c-1cb0-4e80-8944-bd0d0bbedfdc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: ningk
ms.openlocfilehash: fa30c78a5a5d458ba8845c3c10b87538427786c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-tomcat7-on-a-linux-virtual-machine-with-azure"></a><span data-ttu-id="6e2d8-103">Configurar o Tomcat7 em uma máquina virtual Linux com o Azure</span><span class="sxs-lookup"><span data-stu-id="6e2d8-103">Set up Tomcat7 on a Linux virtual machine with Azure</span></span>
<span data-ttu-id="6e2d8-104">O Apache Tomcat (ou simplesmente Tomcat, também chamado anteriormente de Jacarta Tomcat) é um servidor Web de software livre e um contêiner de servlet desenvolvidos pela Apache Software Foundation (ASF).</span><span class="sxs-lookup"><span data-stu-id="6e2d8-104">Apache Tomcat (or simply Tomcat, also formerly called Jakarta Tomcat) is an open source web server and servlet container developed by the Apache Software Foundation (ASF).</span></span> <span data-ttu-id="6e2d8-105">O Tomcat implementa o Java Servlet e especificações de JSP (JavaServer Pages) da Sun Microsystems.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-105">Tomcat implements the Java Servlet and the JavaServer Pages (JSP) specifications from Sun Microsystems.</span></span> <span data-ttu-id="6e2d8-106">O Tomcat fornece um ambiente de servidor Web puramente Java HTTP no qual o código Java será executado.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-106">Tomcat provides a pure Java HTTP web server environment in which to run Java code.</span></span> <span data-ttu-id="6e2d8-107">Na configuração mais simples, o Tomcat é executado em um único processo do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-107">In the simplest configuration, Tomcat runs in a single operating system process.</span></span> <span data-ttu-id="6e2d8-108">Esse processo é executado em uma máquina virtual Java (JVM).</span><span class="sxs-lookup"><span data-stu-id="6e2d8-108">This process runs a Java virtual machine (JVM).</span></span> <span data-ttu-id="6e2d8-109">Todas as solicitações HTTP de um navegador para o Tomcat são processadas como um thread separado do processo do Tomcat.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-109">Every HTTP request from a browser to Tomcat is processed as a separate thread in the Tomcat process.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="6e2d8-110">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Azure Resource Manager e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="6e2d8-110">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="6e2d8-111">Este artigo aborda como usar o modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-111">This article covers how to use the classic deployment model.</span></span> <span data-ttu-id="6e2d8-112">Recomendamos que a maioria das novas implantações use o modelo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-112">We recommend that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="6e2d8-113">Para usar um modelo do Resource Manager para implantar uma VM Ubuntu com Open JDK e Tomcat, veja [este artigo](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/).</span><span class="sxs-lookup"><span data-stu-id="6e2d8-113">To use a Resource Manager template to deploy an Ubuntu VM with Open JDK and Tomcat, see [this article](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/).</span></span>

<span data-ttu-id="6e2d8-114">Neste artigo, você instalará o Tomcat7 em uma imagem do Linux e a implantará no Azure.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-114">In this article, you will install Tomcat7 on a Linux image and deploy it in Azure.</span></span>  

<span data-ttu-id="6e2d8-115">Você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="6e2d8-115">You will learn:</span></span>  

* <span data-ttu-id="6e2d8-116">Como criar uma máquina virtual no Azure.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-116">How to create a virtual machine in Azure.</span></span>
* <span data-ttu-id="6e2d8-117">Como preparar a máquina virtual para o Tomcat7.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-117">How to prepare the virtual machine for Tomcat7.</span></span>
* <span data-ttu-id="6e2d8-118">Como instalar o Tomcat7.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-118">How to install Tomcat7.</span></span>

<span data-ttu-id="6e2d8-119">Supomos que você já tem uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-119">It is assumed that you already have an Azure subscription.</span></span>  <span data-ttu-id="6e2d8-120">Se ainda não tiver uma, você poderá se inscrever para uma avaliação gratuita no [site do Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="6e2d8-120">If not, you can sign up for a free trial at [the Azure website](https://azure.microsoft.com/).</span></span> <span data-ttu-id="6e2d8-121">Se você tiver uma assinatura do MSDN, confira [Preço especial do Microsoft Azure: benefícios do MSDN, MPN e BizSpark](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39).</span><span class="sxs-lookup"><span data-stu-id="6e2d8-121">If you have an MSDN subscription, see [Microsoft Azure Special Pricing: MSDN, MPN, and BizSpark Benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39).</span></span> <span data-ttu-id="6e2d8-122">Para saber mais sobre o Azure, confira [o que é o Azure?](https://azure.microsoft.com/overview/what-is-azure/).</span><span class="sxs-lookup"><span data-stu-id="6e2d8-122">To learn more about Azure, see [What is Azure?](https://azure.microsoft.com/overview/what-is-azure/).</span></span>

<span data-ttu-id="6e2d8-123">Este artigo pressupõe que você tenha conhecimento prático básico do Tomcat e Linux.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-123">This article assumes that you have a basic working knowledge of Tomcat and Linux.</span></span>  

## <a name="phase-1-create-an-image"></a><span data-ttu-id="6e2d8-124">Fase 1: Criar uma imagem</span><span class="sxs-lookup"><span data-stu-id="6e2d8-124">Phase 1: Create an image</span></span>
<span data-ttu-id="6e2d8-125">Nesta fase, você criará uma máquina virtual usando uma imagem do Linux no Azure.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-125">In this phase, you will create a virtual machine by using a Linux image in Azure.</span></span>  

### <a name="step-1-generate-an-ssh-authentication-key"></a><span data-ttu-id="6e2d8-126">Etapa 1: Gerar uma chave de autenticação SSH</span><span class="sxs-lookup"><span data-stu-id="6e2d8-126">Step 1: Generate an SSH authentication key</span></span>
<span data-ttu-id="6e2d8-127">O SSH é uma ferramenta importante para os administradores do sistema.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-127">SSH is an important tool for system administrators.</span></span> <span data-ttu-id="6e2d8-128">No entanto, não é recomendado configurar a segurança de acesso com base em uma senha determinada por humanos.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-128">However, configuring access security based on a human-determined password is not recommended.</span></span> <span data-ttu-id="6e2d8-129">Usuários mal-intencionados podem entrar em seu sistema usando um nome de usuário e uma senha fraca.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-129">Malicious users can break into your system based on a username and a weak password.</span></span>

<span data-ttu-id="6e2d8-130">A boa notícia é que há uma maneira de deixar o acesso remoto aberto e não precisar se preocupar com as senhas.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-130">The good news is that there is a way to leave remote access open and not worry about passwords.</span></span> <span data-ttu-id="6e2d8-131">O método consiste na autenticação com criptografia assimétrica.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-131">This method consists of authentication with asymmetric cryptography.</span></span> <span data-ttu-id="6e2d8-132">A chave privada do usuário é a que concede a autenticação.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-132">The user’s private key is the one that grants the authentication.</span></span> <span data-ttu-id="6e2d8-133">Você ainda pode bloquear a conta do usuário para não permitir a autenticação de senha.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-133">You can even lock the user’s account to not allow password authentication.</span></span>

<span data-ttu-id="6e2d8-134">Outra vantagem desse método é que você não precisa de senhas diferentes para entrar em servidores diferentes.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-134">Another advantage of this method is that you do not need different passwords to sign in to different servers.</span></span> <span data-ttu-id="6e2d8-135">Você pode autenticar usando a chave privada pessoal em todos os servidores, fazendo com que você não precise se lembrar de várias senhas.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-135">You can authenticate by using the personal private key on all servers, which prevents you from having to remember several passwords.</span></span>



<span data-ttu-id="6e2d8-136">Siga estas etapas para gerar a chave de autenticação SSH.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-136">Follow these steps to generate the SSH authentication key.</span></span>

1. <span data-ttu-id="6e2d8-137">Baixe e instale o PuTTYgen do seguinte local: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.htm](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span><span class="sxs-lookup"><span data-stu-id="6e2d8-137">Download and install PuTTYgen from the following location: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span></span>
2. <span data-ttu-id="6e2d8-138">Execute o Puttygen.exe.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-138">Run Puttygen.exe.</span></span>
3. <span data-ttu-id="6e2d8-139">Clique em **Gerar** para gerar as chaves.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-139">Click **Generate** to generate the keys.</span></span> <span data-ttu-id="6e2d8-140">No processo, você pode aumentar a aleatoriedade movendo o mouse sobre a área em branco na janela.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-140">In the process, you can increase randomness by moving the mouse over the blank area in the window.</span></span>  
   <span data-ttu-id="6e2d8-141">![Captura de tela do PuTTY Key Generator que mostra o novo botão para gerar chave][1]</span><span class="sxs-lookup"><span data-stu-id="6e2d8-141">![PuTTY Key Generator screenshot that shows the generate new key button][1]</span></span>
4. <span data-ttu-id="6e2d8-142">Após o processo de geração, Puttygen.exe mostrará sua nova chave pública.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-142">After the generate process, Puttygen.exe will show your new public key.</span></span>  
   ![Captura de tela do PuTTY Key Generator que mostra a nova chave pública e o botão para salvar chave privada][2]
5. <span data-ttu-id="6e2d8-144">Selecione e copie a chave pública e salve-a em um arquivo chamado publicKey.pem.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-144">Select and copy the public key, and save it in a file named publicKey.pem.</span></span> <span data-ttu-id="6e2d8-145">Não clique em **Salvar chave pública**, porque o formato de arquivo da chave pública salva é diferente da chave pública que queremos.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-145">Don’t click **Save public key**, because the saved public key’s file format is different from the public key we want.</span></span>
6. <span data-ttu-id="6e2d8-146">Clique em **Salvar chave privada** e salve-a em um arquivo chamado privateKey.ppk.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-146">Click **Save private key**, and save it in a file named privateKey.ppk.</span></span>

### <a name="step-2-create-the-image-in-the-azure-portal"></a><span data-ttu-id="6e2d8-147">Etapa 2: Criar a imagem no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6e2d8-147">Step 2: Create the image in the Azure portal</span></span>
1. <span data-ttu-id="6e2d8-148">No [Portal](https://portal.azure.com/), clique em **Novo** na barra de tarefas para criar uma imagem.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-148">In the [portal](https://portal.azure.com/), click **New** in the task bar to create an image.</span></span> <span data-ttu-id="6e2d8-149">Em seguida, escolha a imagem do Linux conforme suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-149">Then choose the Linux image that is based on your needs.</span></span> <span data-ttu-id="6e2d8-150">O exemplo a seguir usa a imagem do Ubuntu 14.04.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-150">The following example uses the Ubuntu 14.04 image.</span></span>
<span data-ttu-id="6e2d8-151">![Captura de tela do portal que mostra o botão Novo][3]</span><span class="sxs-lookup"><span data-stu-id="6e2d8-151">![Screenshot of the portal that shows the New button][3]</span></span>

2. <span data-ttu-id="6e2d8-152">Para o **Nome do Host**, especifique o nome para a URL que você e os clientes da Internet usarão para acessar esta máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-152">For **Host Name**, specify the name for the URL that you and Internet clients will use to access this virtual machine.</span></span> <span data-ttu-id="6e2d8-153">Defina a última parte do nome DNS, por exemplo, tomcatdemo.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-153">Define the last part of the DNS name, for example, tomcatdemo.</span></span> <span data-ttu-id="6e2d8-154">O Azure gerará a URL como tomcatdemo.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-154">Azure will then generate the URL as tomcatdemo.cloudapp.net.</span></span>  

3. <span data-ttu-id="6e2d8-155">Para a **Chave de Autenticação SSH**, copie o valor da chave do arquivo publicKey.pem, que contém a chave pública gerada pelo PuTTYgen.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-155">For **SSH Authentication Key**, copy the key value from the publicKey.pem file, which contains the public key generated by PuTTYgen.</span></span>  
<span data-ttu-id="6e2d8-156">![Caixa da Chave de Autenticação SSH no portal][4]</span><span class="sxs-lookup"><span data-stu-id="6e2d8-156">![SSH Authentication Key box in the portal][4]</span></span>

4. <span data-ttu-id="6e2d8-157">Defina as outras configurações conforme necessário e, em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-157">Configure other settings as needed, and then click **Create**.</span></span>  

## <a name="phase-2-prepare-your-virtual-machine-for-tomcat7"></a><span data-ttu-id="6e2d8-158">Fase 2: Preparar sua máquina virtual para o Tomcat7</span><span class="sxs-lookup"><span data-stu-id="6e2d8-158">Phase 2: Prepare your virtual machine for Tomcat7</span></span>
<span data-ttu-id="6e2d8-159">Nesta fase, você configurará um ponto de extremidade para o tráfego do Tomcat e, em seguida, se conectará à nova máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-159">In this phase, you will configure an endpoint for Tomcat traffic, and then connect to your new virtual machine.</span></span>

### <a name="step-1-open-the-http-port-to-allow-web-access"></a><span data-ttu-id="6e2d8-160">Etapa 1: Abrir a porta HTTP para permitir o acesso via Web</span><span class="sxs-lookup"><span data-stu-id="6e2d8-160">Step 1: Open the HTTP port to allow web access</span></span>
<span data-ttu-id="6e2d8-161">Os pontos de extremidade no Azure são compostos por um protocolo TCP ou UDP juntamente com uma porta pública e privada.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-161">Endpoints in Azure consist of a TCP or UDP protocol, along with a public and private port.</span></span> <span data-ttu-id="6e2d8-162">A porta privada é aquela que o serviço está escutando na máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-162">The private port is the port that the service is listening to on the virtual machine.</span></span> <span data-ttu-id="6e2d8-163">A porta pública é aquela em que o serviço de nuvem do Azure escuta tráfego de entrada baseado na Internet.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-163">The public port is the port that the Azure cloud service listens to externally for incoming, Internet-based traffic.</span></span>  

<span data-ttu-id="6e2d8-164">A porta 8080 TCP é o número da porta padrão que o Tomcat escuta.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-164">TCP port 8080 is the default port number that Tomcat uses to listen.</span></span> <span data-ttu-id="6e2d8-165">Se esta porta for aberta com um Ponto de Extremidade do Azure, você e outros clientes da Internet poderão acessar páginas do Tomcat.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-165">If this port is opened with an Azure endpoint, you and other Internet clients can access Tomcat pages.</span></span>  

1. <span data-ttu-id="6e2d8-166">No portal, clique em **Procurar** > **Máquinas Virtuais** e clique na máquina virtual que você criou.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-166">In the portal, click **Browse** > **Virtual machines**, and then click the virtual machine that you created.</span></span>  
   <span data-ttu-id="6e2d8-167">![Captura de tela do diretório de máquinas virtuais][5]</span><span class="sxs-lookup"><span data-stu-id="6e2d8-167">![Screenshot of the Virtual machines directory][5]</span></span>
2. <span data-ttu-id="6e2d8-168">Para adicionar um ponto de extremidade à máquina virtual, clique na caixa **Pontos de extremidade** .</span><span class="sxs-lookup"><span data-stu-id="6e2d8-168">To add an endpoint to your virtual machine, click the **Endpoints** box.</span></span>
   <span data-ttu-id="6e2d8-169">![Captura de tela que mostra a caixa de Pontos de Extremidade][6]</span><span class="sxs-lookup"><span data-stu-id="6e2d8-169">![Screenshot that shows the Endpoints box][6]</span></span>
3. <span data-ttu-id="6e2d8-170">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-170">Click **Add**.</span></span>  

   1. <span data-ttu-id="6e2d8-171">Digite um nome para o ponto de extremidade em **Ponto de Extremidade** e digite 80 em **Porta Pública**.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-171">For the endpoint, enter a name for the endpoint in **Endpoint**, and then enter 80 in **Public Port**.</span></span>  

      <span data-ttu-id="6e2d8-172">Se você defini-la para 80, não será necessário incluir o número da porta na URL usada para acessar o Tomcat.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-172">If you set it to 80, you don’t need to include the port number in the URL that is used to access Tomcat.</span></span> <span data-ttu-id="6e2d8-173">Por exemplo, http://tomcatdemo.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-173">For example, http://tomcatdemo.cloudapp.net.</span></span>    

      <span data-ttu-id="6e2d8-174">Se você defini-la para outro valor, tal como 81, será necessário adicionar o número da porta à URL para acessar o Tomcat.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-174">If you set it to another value, such as 81, you need to add the port number to the URL to access Tomcat.</span></span> <span data-ttu-id="6e2d8-175">Por exemplo, http://tomcatdemo.cloudapp.net:81/.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-175">For example,  http://tomcatdemo.cloudapp.net:81/.</span></span>
   2. <span data-ttu-id="6e2d8-176">Digite 8080 em **Porta Privada**.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-176">Enter 8080 in **Private Port**.</span></span> <span data-ttu-id="6e2d8-177">Por padrão, o Tomcat escuta a porta 8080 TCP.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-177">By default, Tomcat listens on TCP port 8080.</span></span> <span data-ttu-id="6e2d8-178">Se você alterou a porta de escuta padrão do Tomcat, deverá atualizar a **Porta Privada** para a mesma que a porta de escuta do Tomcat.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-178">If you changed the default listen port of Tomcat, you should update **Private Port** to be the same as the Tomcat listen port.</span></span>  
      <span data-ttu-id="6e2d8-179">![Captura de tela da interface do usuário que mostra o comando Adicionar, a Porta Pública e a Porta Privada][7]</span><span class="sxs-lookup"><span data-stu-id="6e2d8-179">![Screenshot of UI that shows Add command, Public Port, and Private Port][7]</span></span>
4. <span data-ttu-id="6e2d8-180">Clique em **OK** para adicionar o ponto de extremidade à máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-180">Click **OK** to add the endpoint to your virtual machine.</span></span>

### <a name="step-2-connect-to-the-image-you-created"></a><span data-ttu-id="6e2d8-181">Etapa 2: Conectar-se à imagem criada</span><span class="sxs-lookup"><span data-stu-id="6e2d8-181">Step 2: Connect to the image you created</span></span>
<span data-ttu-id="6e2d8-182">Você pode escolher qualquer ferramenta SSH para se conectar à sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-182">You can choose any SSH tool to connect to your virtual machine.</span></span> <span data-ttu-id="6e2d8-183">Neste exemplo, usamos PuTTY.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-183">In this example, we use PuTTY.</span></span>  

1. <span data-ttu-id="6e2d8-184">Obtenha o nome DNS da máquina virtual no portal.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-184">Get the DNS name of your virtual machine from the portal.</span></span>
    1. <span data-ttu-id="6e2d8-185">Clique em **Procurar** > **Máquinas Virtuais**.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-185">Click **Browse** > **Virtual machines**.</span></span>
    2. <span data-ttu-id="6e2d8-186">Selecione o nome da máquina virtual e clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-186">Select the name of your virtual machine, and then click **Properties**.</span></span>
    3. <span data-ttu-id="6e2d8-187">No bloco **Propriedades**, examine a caixa **Nome de Domínio** para obter o nome DNS.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-187">In the **Properties** tile, look in the **Domain Name** box to get the DNS name.</span></span>  

2. <span data-ttu-id="6e2d8-188">Obtenha o número da porta para conexões SSH na caixa **SSH**.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-188">Get the port number for SSH connections from the **SSH** box.</span></span>  
<span data-ttu-id="6e2d8-189">![Captura de tela que mostra o número da porta da conexão SSH][8]</span><span class="sxs-lookup"><span data-stu-id="6e2d8-189">![Screenshot that shows the SSH connection port number][8]</span></span>

3. <span data-ttu-id="6e2d8-190">Baixe [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="6e2d8-190">Download [PuTTY](http://www.putty.org/).</span></span>  

4. <span data-ttu-id="6e2d8-191">Depois de baixar, clique no arquivo executável Putty.exe.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-191">After downloading, click the executable file Putty.exe.</span></span> <span data-ttu-id="6e2d8-192">Na configuração PuTTY, configure s opções básicas com o nome do host e o número da porta obtido nas propriedades da sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-192">In PuTTY configuration, configure the basic options with the host name and port number that is obtained from the properties of your virtual machine.</span></span>   
![Captura de tela que mostra as opções de nome e porta do host de configuração PuTTY][9]

5. <span data-ttu-id="6e2d8-194">No painel esquerdo, clique em **Conexão** > **SSH** > **Autenticar**e, em seguida, clique em **Procurar** para especificar o local do arquivo privateKey.ppk.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-194">In the left pane, click **Connection** > **SSH** > **Auth**, and then click **Browse** to specify the location of the privateKey.ppk file.</span></span> <span data-ttu-id="6e2d8-195">O arquivo privateKey.ppk contém a chave privada que foi gerada pelo PuTTYgen anteriormente na seção “Fase 1: Criar uma imagem” deste artigo.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-195">The privateKey.ppk file contains the private key that is generated by PuTTYgen earlier in the "Phase 1: Create an image" section of this article.</span></span>  
<span data-ttu-id="6e2d8-196">![Captura de tela que mostra a hierarquia do Diretório de conexão e o botão Procurar][10]</span><span class="sxs-lookup"><span data-stu-id="6e2d8-196">![Screenshot that shows the Connection directory hierarchy and Browse button][10]</span></span>

6. <span data-ttu-id="6e2d8-197">Clique em **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-197">Click **Open**.</span></span> <span data-ttu-id="6e2d8-198">Você pode ser alertado por uma caixa de mensagem.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-198">You might be alerted by a message box.</span></span> <span data-ttu-id="6e2d8-199">Se você tiver configurado o nome DNS e o número da porta corretamente, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-199">If you have configured the DNS name and port number correctly, click **Yes**.</span></span>
<span data-ttu-id="6e2d8-200">![Captura de tela que mostra a notificação][11]</span><span class="sxs-lookup"><span data-stu-id="6e2d8-200">![Screenshot that shows the notification][11]</span></span>

7. <span data-ttu-id="6e2d8-201">Será solicitado que você insira inserir seu nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-201">You are prompted to enter your username.</span></span>  
![Captura de tela que mostra onde inserir o nome de usuário][12]

8. <span data-ttu-id="6e2d8-203">Insira o nome de usuário que você usou para criar a máquina virtual na seção “Fase 1: Criar uma imagem” neste artigo.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-203">Enter the username that you used to create the virtual machine in the "Phase 1: Create an image" section earlier in this article.</span></span> <span data-ttu-id="6e2d8-204">Você verá algo semelhante ao que se segue:</span><span class="sxs-lookup"><span data-stu-id="6e2d8-204">You will see something like the following:</span></span>  
![Captura de tela que mostra a confirmação de autenticação][13]

## <a name="phase-3-install-software"></a><span data-ttu-id="6e2d8-206">Fase 3: Instalar o software</span><span class="sxs-lookup"><span data-stu-id="6e2d8-206">Phase 3: Install software</span></span>
<span data-ttu-id="6e2d8-207">Nesta fase, você pode instalar o Java Runtime Environment, Tomcat7 e demais componentes do Tomcat7.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-207">In this phase, you install the Java runtime environment, Tomcat7, and other Tomcat7 components.</span></span>  

### <a name="java-runtime-environment"></a><span data-ttu-id="6e2d8-208">Java runtime environment</span><span class="sxs-lookup"><span data-stu-id="6e2d8-208">Java runtime environment</span></span>
<span data-ttu-id="6e2d8-209">O tomcat é escrito em Java.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-209">Tomcat is written in Java.</span></span> <span data-ttu-id="6e2d8-210">Há dois tipos de JDKs (Kits de desenvolvimento Java), OpenJDK e Oracle JDK.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-210">There are two kinds of Java Development Kits (JDKs), OpenJDK and Oracle JDK.</span></span> <span data-ttu-id="6e2d8-211">Você pode escolher aquele que preferir.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-211">You can choose the one you want.</span></span>  

> [!NOTE]
> <span data-ttu-id="6e2d8-212">Ambos os JDKs têm código quase idêntico para as classes na API do Java, porém o código para a máquina virtual é diferente.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-212">Both JDKs have almost the same code for the classes in the Java API, but the code for the virtual machine is different.</span></span> <span data-ttu-id="6e2d8-213">O OpenJDK tende a usar bibliotecas abertas, enquanto o Oracle JDK tende a usar bibliotecas fechadas.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-213">OpenJDK tends to use open libraries, while Oracle JDK tends to use closed ones.</span></span> <span data-ttu-id="6e2d8-214">O Oracle JDK tem mais classes e alguns bugs corrigidos, sendo também mais estável que o OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-214">Oracle JDK has more classes and some fixed bugs, and Oracle JDK is more stable than OpenJDK.</span></span>

#### <a name="install-openjdk"></a><span data-ttu-id="6e2d8-215">Instalar o OpenJDK</span><span class="sxs-lookup"><span data-stu-id="6e2d8-215">Install OpenJDK</span></span>  

<span data-ttu-id="6e2d8-216">Use o seguinte comando para baixar o OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-216">Use the following command to download OpenJDK.</span></span>   

    sudo apt-get update  
    sudo apt-get install openjdk-7-jre  


* <span data-ttu-id="6e2d8-217">Para criar um diretório para conter os arquivos JDK:</span><span class="sxs-lookup"><span data-stu-id="6e2d8-217">To create a directory to contain the JDK files:</span></span>  

        sudo mkdir /usr/lib/jvm  
* <span data-ttu-id="6e2d8-218">Para extrair os arquivos JDK para diretório /usr/lib/jvm/:</span><span class="sxs-lookup"><span data-stu-id="6e2d8-218">To extract the JDK files into the /usr/lib/jvm/ directory:</span></span>  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/

#### <a name="install-oracle-jdk"></a><span data-ttu-id="6e2d8-219">Instalar o Oracle JDK</span><span class="sxs-lookup"><span data-stu-id="6e2d8-219">Install Oracle JDK</span></span>


<span data-ttu-id="6e2d8-220">Use o seguinte comando para baixar o Oracle JDK do site do Oracle.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-220">Use the following command to download Oracle JDK from the Oracle website.</span></span>  

     wget --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u5-b13/jdk-8u5-linux-x64.tar.gz  
* <span data-ttu-id="6e2d8-221">Para criar um diretório para conter os arquivos JDK:</span><span class="sxs-lookup"><span data-stu-id="6e2d8-221">To create a directory to contain the JDK files:</span></span>  

        sudo mkdir /usr/lib/jvm  
* <span data-ttu-id="6e2d8-222">Para extrair os arquivos JDK para diretório /usr/lib/jvm/:</span><span class="sxs-lookup"><span data-stu-id="6e2d8-222">To extract the JDK files into the /usr/lib/jvm/ directory:</span></span>  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/  
* <span data-ttu-id="6e2d8-223">Para definir o Oracle JDK como a máquina virtual Java padrão:</span><span class="sxs-lookup"><span data-stu-id="6e2d8-223">To set Oracle JDK as the default Java virtual machine:</span></span>  

        sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk1.8.0_05/bin/java 100  

        sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk1.8.0_05/bin/javac 100  

#### <a name="confirm-that-java-installation-is-successful"></a><span data-ttu-id="6e2d8-224">Confirme se a instalação do Java foi bem-sucedida</span><span class="sxs-lookup"><span data-stu-id="6e2d8-224">Confirm that Java installation is successful</span></span>
<span data-ttu-id="6e2d8-225">Você pode usar um comando semelhante ao seguinte para testar se o Java runtime environment está instalado corretamente:</span><span class="sxs-lookup"><span data-stu-id="6e2d8-225">You can use a command like the following to test if the Java runtime environment is installed correctly:</span></span>  

    java -version  

<span data-ttu-id="6e2d8-226">Se você instalou o OpenJDK, verá uma mensagem semelhante à seguinte: ![Mensagem de instalação bem-sucedida do OpenJDK][14]</span><span class="sxs-lookup"><span data-stu-id="6e2d8-226">If you installed OpenJDK, you should see a message like the following: ![Successful OpenJDK installation message][14]</span></span>

<span data-ttu-id="6e2d8-227">Se você instalou o Oracle JDK, verá uma mensagem semelhante à seguinte: ![Mensagem de instalação bem-sucedida do Oracle JDK][15]</span><span class="sxs-lookup"><span data-stu-id="6e2d8-227">If you installed Oracle JDK, you should see a message like the following: ![Successful Oracle JDK installation message][15]</span></span>

### <a name="install-tomcat7"></a><span data-ttu-id="6e2d8-228">Instalar o Tomcat7</span><span class="sxs-lookup"><span data-stu-id="6e2d8-228">Install Tomcat7</span></span>
<span data-ttu-id="6e2d8-229">Use o seguinte comando para instalar o Tomcat7.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-229">Use the following command to install Tomcat7.</span></span>  

    sudo apt-get install tomcat7  

<span data-ttu-id="6e2d8-230">Se você não estiver usando o Tomcat7, use a variação apropriada desse comando.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-230">If you are not using Tomcat7, use the appropriate variation of this command.</span></span>  

#### <a name="confirm-that-tomcat7-installation-is-successful"></a><span data-ttu-id="6e2d8-231">Confirme se a instalação do Tomcat7 foi bem-sucedida</span><span class="sxs-lookup"><span data-stu-id="6e2d8-231">Confirm that Tomcat7 installation is successful</span></span>
<span data-ttu-id="6e2d8-232">Para verificar se o Tomcat7 foi instalado com êxito, navegue para o nome DNS do seu servidor do Tomcat.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-232">To check if Tomcat7 is successfully installed, browse to your Tomcat server’s DNS name.</span></span> <span data-ttu-id="6e2d8-233">Neste artigo, a URL de exemplo é http://tomcatexample.cloudapp.net/.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-233">In this article, the example URL is http://tomcatexample.cloudapp.net/.</span></span> <span data-ttu-id="6e2d8-234">Se você encontrar uma mensagem semelhante à seguinte, o Tomcat7 estará instalado corretamente.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-234">If you see a message like the following, Tomcat7 is installed correctly.</span></span>
<span data-ttu-id="6e2d8-235">![Mensagem de instalação bem-sucedida do Tomcat7][16]</span><span class="sxs-lookup"><span data-stu-id="6e2d8-235">![Successful Tomcat7 installation message][16]</span></span>

### <a name="install-other-tomcat7-components"></a><span data-ttu-id="6e2d8-236">Instalar outros componentes do Tomcat7</span><span class="sxs-lookup"><span data-stu-id="6e2d8-236">Install other Tomcat7 components</span></span>
<span data-ttu-id="6e2d8-237">Há outros componentes opcionais do Tomcat que você pode instalar.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-237">There are other optional Tomcat components that you can install.</span></span>  

<span data-ttu-id="6e2d8-238">Use o comando **sudo apt-cache search tomcat7** para ver todos os componentes disponíveis.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-238">Use the **sudo apt-cache search tomcat7** command to see all of the available components.</span></span> <span data-ttu-id="6e2d8-239">Use os comandos a seguir para instalar alguns componentes úteis.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-239">Use the following commands to install some useful components.</span></span>  

    sudo apt-get install tomcat7-admin      #admin web applications

    sudo apt-get install tomcat7-user         #tools to create user instances  

## <a name="phase-4-configure-tomcat7"></a><span data-ttu-id="6e2d8-240">Fase 4: Configurar o Tomcat7</span><span class="sxs-lookup"><span data-stu-id="6e2d8-240">Phase 4: Configure Tomcat7</span></span>
<span data-ttu-id="6e2d8-241">Nesta fase, você administrará o Tomcat.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-241">In this phase, you administer Tomcat.</span></span>

### <a name="start-and-stop-tomcat7"></a><span data-ttu-id="6e2d8-242">Iniciar e parar o Tomcat7</span><span class="sxs-lookup"><span data-stu-id="6e2d8-242">Start and stop Tomcat7</span></span>
<span data-ttu-id="6e2d8-243">O servidor do Tomcat7 será iniciado automaticamente quando você o instala.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-243">The Tomcat7 server automatically starts when you install it.</span></span> <span data-ttu-id="6e2d8-244">Você também pode iniciá-lo com o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="6e2d8-244">You can also start it with the following command:</span></span>   

    sudo /etc/init.d/tomcat7 start

<span data-ttu-id="6e2d8-245">Para interromper o Tomcat7:</span><span class="sxs-lookup"><span data-stu-id="6e2d8-245">To stop Tomcat7:</span></span>

    sudo /etc/init.d/tomcat7 stop

<span data-ttu-id="6e2d8-246">Para exibir o status do Tomcat7:</span><span class="sxs-lookup"><span data-stu-id="6e2d8-246">To view the status of Tomcat7:</span></span>

    sudo /etc/init.d/tomcat7 status

<span data-ttu-id="6e2d8-247">Para reiniciar os serviços do Tomcat:</span><span class="sxs-lookup"><span data-stu-id="6e2d8-247">To restart Tomcat services:</span></span> 

    sudo /etc/init.d/tomcat7 restart

### <a name="tomcat7-administration"></a><span data-ttu-id="6e2d8-248">Administração do Tomcat7</span><span class="sxs-lookup"><span data-stu-id="6e2d8-248">Tomcat7 administration</span></span>
<span data-ttu-id="6e2d8-249">Você pode editar o arquivo de configuração de usuário do Tomcat para configurar as credenciais de administrador.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-249">You can edit the Tomcat user configuration file to set up your admin credentials.</span></span> <span data-ttu-id="6e2d8-250">Use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="6e2d8-250">Use the following command:</span></span>  

    sudo vi  /etc/tomcat7/tomcat-users.xml   

<span data-ttu-id="6e2d8-251">Aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="6e2d8-251">Here is an example:</span></span>  
![Captura de tela que mostra a saída do comando sudo vi][17]  

> [!NOTE]
> <span data-ttu-id="6e2d8-253">Crie uma senha forte para o nome de usuário do administrador.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-253">Create a strong password for the admin username.</span></span>  

<span data-ttu-id="6e2d8-254">Depois de editar esse arquivo, você deverá reiniciar os serviços do Tomcat7 com o comando a seguir para garantir que as alterações entrem em vigor:</span><span class="sxs-lookup"><span data-stu-id="6e2d8-254">After editing this file, you should restart Tomcat7 services with the following command to ensure that the changes take effect:</span></span>  

    sudo /etc/init.d/tomcat7 restart  

<span data-ttu-id="6e2d8-255">Abra o navegador e digite **http://<your tomcat server DNS name>/manager/html** como a URL.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-255">Open your browser, and enter **http://<your tomcat server DNS name>/manager/html** as the URL.</span></span> <span data-ttu-id="6e2d8-256">Para o exemplo neste artigo, a URL é http://tomcatexample.cloudapp.net/manager/html.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-256">For the example in this article, the URL is http://tomcatexample.cloudapp.net/manager/html.</span></span>  

<span data-ttu-id="6e2d8-257">Após conectar, você deverá ver algo semelhante ao seguinte: </span><span class="sxs-lookup"><span data-stu-id="6e2d8-257">After connecting, you should see something similar to the following:</span></span>  
![Captura de tela do Tomcat Web Application Manager][18]

## <a name="common-issues"></a><span data-ttu-id="6e2d8-259">Problemas comuns</span><span class="sxs-lookup"><span data-stu-id="6e2d8-259">Common issues</span></span>
### <a name="cant-access-the-virtual-machine-with-tomcat-and-moodle-from-the-internet"></a><span data-ttu-id="6e2d8-260">Não é possível acessar a máquina virtual com o Tomcat e o Moodle por meio da Internet</span><span class="sxs-lookup"><span data-stu-id="6e2d8-260">Can't access the virtual machine with Tomcat and Moodle from the Internet</span></span>
#### <a name="symptom"></a><span data-ttu-id="6e2d8-261">Sintoma</span><span class="sxs-lookup"><span data-stu-id="6e2d8-261">Symptom</span></span>  
  <span data-ttu-id="6e2d8-262">O Tomcat está sendo executado, mas você não consegue ver a página padrão do Tomcat com seu navegador.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-262">Tomcat is running but you can’t see the Tomcat default page with your browser.</span></span>
#### <a name="possible-root-cause"></a><span data-ttu-id="6e2d8-263">Possível causa raiz</span><span class="sxs-lookup"><span data-stu-id="6e2d8-263">Possible root cause</span></span>   

  * <span data-ttu-id="6e2d8-264">A porta de escuta do Tomcat não é a mesma que a porta privada do ponto de extremidade da máquina virtual para o tráfego do Tomcat.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-264">The Tomcat listen port is not the same as the private port of your virtual machine's endpoint for Tomcat traffic.</span></span>  

     <span data-ttu-id="6e2d8-265">Verifique as configurações de ponto de extremidade da porta pública e da porta privada e certifique-se de que a porta privada seja a mesma que a porta de escuta do Tomcat.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-265">Check your public port and private port endpoint settings and make sure the private port is the same as the Tomcat listen port.</span></span> <span data-ttu-id="6e2d8-266">Consulte a seção “Fase 1: Criar uma imagem” deste artigo para obter instruções sobre como configurar os pontos de extremidade para sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-266">See "Phase 1: Create an image" section of this article for instructions on configuring endpoints for your virtual machine.</span></span>  

     <span data-ttu-id="6e2d8-267">Para determinar a porta de escuta do Tomcat, abra /etc/httpd/conf/httpd.conf (versão Red Hat) ou /etc/tomcat7/server.xml (versão Debian).</span><span class="sxs-lookup"><span data-stu-id="6e2d8-267">To determine the Tomcat listen port, open /etc/httpd/conf/httpd.conf (Red Hat release), or /etc/tomcat7/server.xml (Debian release).</span></span> <span data-ttu-id="6e2d8-268">Por padrão, a porta de escuta do Tomcat é 8080.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-268">By default, the Tomcat listen port is 8080.</span></span> <span data-ttu-id="6e2d8-269">Aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="6e2d8-269">Here is an example:</span></span>  

        <Connector port="8080" protocol="HTTP/1.1"  connectionTimeout="20000"   URIEncoding="UTF-8"            redirectPort="8443" />  

     <span data-ttu-id="6e2d8-270">Se você estiver usando uma máquina virtual como Debian ou Ubuntu e desejar alterar a porta padrão do Tomcat Listen (por exemplo, 8081), você também deverá abrir a porta para o sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-270">If you are using a virtual machine like Debian or Ubuntu and you want to change the default port of Tomcat Listen (for example 8081), you should also open the port for the operating system.</span></span> <span data-ttu-id="6e2d8-271">Primeiro, abra o perfil:</span><span class="sxs-lookup"><span data-stu-id="6e2d8-271">First, open the profile:</span></span>  

        sudo vi /etc/default/tomcat7  

     <span data-ttu-id="6e2d8-272">Remova a marca de comentário da última linha e altere “não” para “sim”.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-272">Then uncomment the last line and change “no” to “yes”.</span></span>  

        AUTHBIND=yes
  2. <span data-ttu-id="6e2d8-273">O firewall desabilitou a porta de escuta do tomcat.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-273">The firewall has disabled the listen port of Tomcat.</span></span>

     <span data-ttu-id="6e2d8-274">Você só pode ver a página padrão do Tomcat do host local.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-274">You can only see the Tomcat default page from the local host.</span></span> <span data-ttu-id="6e2d8-275">O problema é provavelmente se deve à porta, que o Tomcat escuta, estar bloqueada pelo firewall.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-275">The problem is most likely that the port, which is listened to by Tomcat, is blocked by the firewall.</span></span> <span data-ttu-id="6e2d8-276">Você pode usar a ferramenta w3m para procurar a página da Web.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-276">You can use the w3m tool to browse the webpage.</span></span> <span data-ttu-id="6e2d8-277">Os seguintes comandos instalar w3m e navegue até a página padrão do Tomcat:</span><span class="sxs-lookup"><span data-stu-id="6e2d8-277">The following commands install w3m and browse to the Tomcat default page:</span></span>  


        <span data-ttu-id="6e2d8-278">sudo yum  install w3m w3m-img</span><span class="sxs-lookup"><span data-stu-id="6e2d8-278">sudo yum  install w3m w3m-img</span></span>


        <span data-ttu-id="6e2d8-279">w3m http://localhost:8080</span><span class="sxs-lookup"><span data-stu-id="6e2d8-279">w3m http://localhost:8080</span></span>  
#### <a name="solution"></a><span data-ttu-id="6e2d8-280">Solução</span><span class="sxs-lookup"><span data-stu-id="6e2d8-280">Solution</span></span>

  * <span data-ttu-id="6e2d8-281">Se a porta de escuta do Tomcat não for a mesma que a porta provada do ponto de extremidade para tráfego para a máquina virtual, você precisará alterar a porta privada para a mesma porta de escuta do Tomcat.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-281">If the Tomcat listen port is not the same as the private port of the endpoint for traffic to the virtual machine, you need change the private port to be the same as the Tomcat listen port.</span></span>   
  2. <span data-ttu-id="6e2d8-282">Se o problema for causado pelo firewall/iptables, adicione as seguintes linhas a /etc/sysconfig/iptables.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-282">If the issue is caused by firewall/iptables, add the following lines to /etc/sysconfig/iptables.</span></span> <span data-ttu-id="6e2d8-283">A segunda linha é necessária apenas para tráfego https:</span><span class="sxs-lookup"><span data-stu-id="6e2d8-283">The second line is only needed for https traffic:</span></span>  

      <span data-ttu-id="6e2d8-284">-A INPUT -p tcp -m tcp --dport 80 -j ACCEPT</span><span class="sxs-lookup"><span data-stu-id="6e2d8-284">-A INPUT -p tcp -m tcp --dport 80 -j ACCEPT</span></span>

      <span data-ttu-id="6e2d8-285">-A INPUT -p tcp -m tcp --dport 443 -j ACCEPT</span><span class="sxs-lookup"><span data-stu-id="6e2d8-285">-A INPUT -p tcp -m tcp --dport 443 -j ACCEPT</span></span>  

     > [!IMPORTANT]
     > <span data-ttu-id="6e2d8-286">Verifique se as linhas anteriores estão posicionadas acima de todas as linhas restringiriam o acesso globalmente, tal como a seguinte: -A INPUT -j REJECT --reject-with icmp-host-prohibited</span><span class="sxs-lookup"><span data-stu-id="6e2d8-286">Make sure the previous lines are positioned above any lines that would globally restrict access, such as the following: -A INPUT -j REJECT --reject-with icmp-host-prohibited</span></span>



<span data-ttu-id="6e2d8-287">Para recarregar o iptables, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="6e2d8-287">To reload the iptables, run the following command:</span></span>

    service iptables restart

<span data-ttu-id="6e2d8-288">Isso foi testado no CentOS 6.3.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-288">This has been tested on CentOS 6.3.</span></span>

### <a name="permission-denied-when-you-upload-project-files-to-varlibtomcat7webapps"></a><span data-ttu-id="6e2d8-289">Permissão negada ao carregar os arquivos do projeto para /var/lib/tomcat7/webapps/</span><span class="sxs-lookup"><span data-stu-id="6e2d8-289">Permission denied when you upload project files to /var/lib/tomcat7/webapps/</span></span>
#### <a name="symptom"></a><span data-ttu-id="6e2d8-290">Sintoma</span><span class="sxs-lookup"><span data-stu-id="6e2d8-290">Symptom</span></span>
  <span data-ttu-id="6e2d8-291">Ao usar um cliente SFTP (por exemplo, o FileZilla) para se conectar à máquina virtual e navegar para /var/lib/tomcat7/webapps/ para publicar seu site, você receberá uma mensagem de erro semelhante à seguinte:</span><span class="sxs-lookup"><span data-stu-id="6e2d8-291">When you use an SFTP client (such as FileZilla) to connect to your virtual machine and navigate to /var/lib/tomcat7/webapps/ to publish your site, you get an error message similar to the following:</span></span>  

     status:    Listing directory /var/lib/tomcat7/webapps
     Command:    put "C:\Users\liang\Desktop\info.jsp" "info.jsp"
     Error:    /var/lib/tomcat7/webapps/info.jsp: open for write: permission denied
     Error:    File transfer failed
#### <a name="possible-root-cause"></a><span data-ttu-id="6e2d8-292">Possível causa raiz</span><span class="sxs-lookup"><span data-stu-id="6e2d8-292">Possible root cause</span></span>
  <span data-ttu-id="6e2d8-293">Você não tem permissões para acessar a pasta /var/lib/tomcat7/webapps.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-293">You have no permissions to access the /var/lib/tomcat7/webapps folder.</span></span>  
#### <a name="solution"></a><span data-ttu-id="6e2d8-294">Solução</span><span class="sxs-lookup"><span data-stu-id="6e2d8-294">Solution</span></span>  
  <span data-ttu-id="6e2d8-295">É necessário obter permissão da conta raiz.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-295">You need to get permission from the root account.</span></span> <span data-ttu-id="6e2d8-296">Você pode alterar a propriedade da pasta raiz para o nome de usuário usado ao provisionar o computador.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-296">You can change the ownership of that folder from root to the username you used when you provisioned the machine.</span></span> <span data-ttu-id="6e2d8-297">Aqui está um exemplo com o nome de conta azureuser:</span><span class="sxs-lookup"><span data-stu-id="6e2d8-297">Here is an example with the azureuser account name:</span></span>  

     sudo chown azureuser -R /var/lib/tomcat7/webapps

  <span data-ttu-id="6e2d8-298">Use a opção -R para aplicar as permissões para todos os arquivos dentro de um diretório também.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-298">Use the -R option to apply the permissions for all files inside of a directory too.</span></span>  

  <span data-ttu-id="6e2d8-299">Este comando também funciona para diretórios.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-299">This command also works for directories.</span></span> <span data-ttu-id="6e2d8-300">A opção -R altera as permissões para todos os arquivos e diretórios dentro do diretório.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-300">The -R option changes the permissions for all files and directories inside the directory.</span></span> <span data-ttu-id="6e2d8-301">Aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="6e2d8-301">Here is an example:</span></span>  

     sudo chown -R username:group directory  

  <span data-ttu-id="6e2d8-302">Este comando altera a propriedade (tanto de usuário como de grupo) para todos os arquivos e diretórios dentro do diretório.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-302">This command changes ownership (both user and group) for all files and directories that are inside the directory.</span></span>  

  <span data-ttu-id="6e2d8-303">O comando a seguir altera apenas a permissão do diretório da pasta.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-303">The following command only changes the permission of the folder directory.</span></span> <span data-ttu-id="6e2d8-304">Os arquivos e pastas dentro do diretório não são alterados.</span><span class="sxs-lookup"><span data-stu-id="6e2d8-304">The files and folders inside the directory are not changed.</span></span>  

     sudo chown username:group directory

[1]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-01.png
[2]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-02.png
[3]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-03.png
[4]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-04.png
[5]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-05.png
[6]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-06.png
[7]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-07.png
[8]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-08.png
[9]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-09.png
[10]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-10.png
[11]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-11.png
[12]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-12.png
[13]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-13.png
[14]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-14.png
[15]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-15.png
[16]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-16.png
[17]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-17.png
[18]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-18.png
