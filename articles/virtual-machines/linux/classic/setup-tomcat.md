---
title: "aaaSet o Apache Tomcat em uma máquina virtual Linux | Microsoft Docs"
description: "Saiba como tooset o Apache Tomcat7 usando máquinas virtuais do Azure executando o Linux."
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
ms.openlocfilehash: b837a73e91fcb25d5459d993a0e93ceef1a1fc8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-tomcat7-on-a-linux-virtual-machine-with-azure"></a><span data-ttu-id="a9572-103">Configurar o Tomcat7 em uma máquina virtual Linux com o Azure</span><span class="sxs-lookup"><span data-stu-id="a9572-103">Set up Tomcat7 on a Linux virtual machine with Azure</span></span>
<span data-ttu-id="a9572-104">Apache Tomcat (ou simplesmente Tomcat, também anteriormente denominado Tomcat Jacarta) é um servidor web de código-fonte aberto e o contêiner de servlet desenvolvido pela Olá Apache Software Foundation (ASF).</span><span class="sxs-lookup"><span data-stu-id="a9572-104">Apache Tomcat (or simply Tomcat, also formerly called Jakarta Tomcat) is an open source web server and servlet container developed by hello Apache Software Foundation (ASF).</span></span> <span data-ttu-id="a9572-105">Tomcat implementa hello Servlet Java e especificações de JavaServer Pages (JSP) Olá da Sun Microsystems.</span><span class="sxs-lookup"><span data-stu-id="a9572-105">Tomcat implements hello Java Servlet and hello JavaServer Pages (JSP) specifications from Sun Microsystems.</span></span> <span data-ttu-id="a9572-106">Tomcat fornece um ambiente de servidor de web HTTP de Java puro no qual toorun código Java.</span><span class="sxs-lookup"><span data-stu-id="a9572-106">Tomcat provides a pure Java HTTP web server environment in which toorun Java code.</span></span> <span data-ttu-id="a9572-107">Configuração mais simples de hello, Tomcat é executado em um processo do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="a9572-107">In hello simplest configuration, Tomcat runs in a single operating system process.</span></span> <span data-ttu-id="a9572-108">Esse processo é executado em uma máquina virtual Java (JVM).</span><span class="sxs-lookup"><span data-stu-id="a9572-108">This process runs a Java virtual machine (JVM).</span></span> <span data-ttu-id="a9572-109">Todas as solicitações HTTP de um navegador tooTomcat é processada como um thread separado no processo de saudação do Tomcat.</span><span class="sxs-lookup"><span data-stu-id="a9572-109">Every HTTP request from a browser tooTomcat is processed as a separate thread in hello Tomcat process.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="a9572-110">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Azure Resource Manager e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a9572-110">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="a9572-111">Este artigo aborda como toouse Olá modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="a9572-111">This article covers how toouse hello classic deployment model.</span></span> <span data-ttu-id="a9572-112">É recomendável que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="a9572-112">We recommend that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="a9572-113">toouse um modelo de Gerenciador de recursos toodeploy uma VM Ubuntu com Open JDK e o Tomcat, consulte [neste artigo](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/).</span><span class="sxs-lookup"><span data-stu-id="a9572-113">toouse a Resource Manager template toodeploy an Ubuntu VM with Open JDK and Tomcat, see [this article](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/).</span></span>

<span data-ttu-id="a9572-114">Neste artigo, você instalará o Tomcat7 em uma imagem do Linux e a implantará no Azure.</span><span class="sxs-lookup"><span data-stu-id="a9572-114">In this article, you will install Tomcat7 on a Linux image and deploy it in Azure.</span></span>  

<span data-ttu-id="a9572-115">Você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="a9572-115">You will learn:</span></span>  

* <span data-ttu-id="a9572-116">Como toocreate uma máquina virtual no Azure.</span><span class="sxs-lookup"><span data-stu-id="a9572-116">How toocreate a virtual machine in Azure.</span></span>
* <span data-ttu-id="a9572-117">Como tooprepare hello máquina virtual para Tomcat7.</span><span class="sxs-lookup"><span data-stu-id="a9572-117">How tooprepare hello virtual machine for Tomcat7.</span></span>
* <span data-ttu-id="a9572-118">Como tooinstall Tomcat7.</span><span class="sxs-lookup"><span data-stu-id="a9572-118">How tooinstall Tomcat7.</span></span>

<span data-ttu-id="a9572-119">Supomos que você já tem uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="a9572-119">It is assumed that you already have an Azure subscription.</span></span>  <span data-ttu-id="a9572-120">Se não, você pode se inscrever para uma avaliação gratuita em [Olá site do Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="a9572-120">If not, you can sign up for a free trial at [hello Azure website](https://azure.microsoft.com/).</span></span> <span data-ttu-id="a9572-121">Se você tiver uma assinatura do MSDN, confira [Preço especial do Microsoft Azure: benefícios do MSDN, MPN e BizSpark](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39).</span><span class="sxs-lookup"><span data-stu-id="a9572-121">If you have an MSDN subscription, see [Microsoft Azure Special Pricing: MSDN, MPN, and BizSpark Benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39).</span></span> <span data-ttu-id="a9572-122">toolearn mais sobre o Azure, consulte [o que é o Azure?](https://azure.microsoft.com/overview/what-is-azure/).</span><span class="sxs-lookup"><span data-stu-id="a9572-122">toolearn more about Azure, see [What is Azure?](https://azure.microsoft.com/overview/what-is-azure/).</span></span>

<span data-ttu-id="a9572-123">Este artigo pressupõe que você tenha conhecimento prático básico do Tomcat e Linux.</span><span class="sxs-lookup"><span data-stu-id="a9572-123">This article assumes that you have a basic working knowledge of Tomcat and Linux.</span></span>  

## <a name="phase-1-create-an-image"></a><span data-ttu-id="a9572-124">Fase 1: Criar uma imagem</span><span class="sxs-lookup"><span data-stu-id="a9572-124">Phase 1: Create an image</span></span>
<span data-ttu-id="a9572-125">Nesta fase, você criará uma máquina virtual usando uma imagem do Linux no Azure.</span><span class="sxs-lookup"><span data-stu-id="a9572-125">In this phase, you will create a virtual machine by using a Linux image in Azure.</span></span>  

### <a name="step-1-generate-an-ssh-authentication-key"></a><span data-ttu-id="a9572-126">Etapa 1: Gerar uma chave de autenticação SSH</span><span class="sxs-lookup"><span data-stu-id="a9572-126">Step 1: Generate an SSH authentication key</span></span>
<span data-ttu-id="a9572-127">O SSH é uma ferramenta importante para os administradores do sistema.</span><span class="sxs-lookup"><span data-stu-id="a9572-127">SSH is an important tool for system administrators.</span></span> <span data-ttu-id="a9572-128">No entanto, não é recomendado configurar a segurança de acesso com base em uma senha determinada por humanos.</span><span class="sxs-lookup"><span data-stu-id="a9572-128">However, configuring access security based on a human-determined password is not recommended.</span></span> <span data-ttu-id="a9572-129">Usuários mal-intencionados podem entrar em seu sistema usando um nome de usuário e uma senha fraca.</span><span class="sxs-lookup"><span data-stu-id="a9572-129">Malicious users can break into your system based on a username and a weak password.</span></span>

<span data-ttu-id="a9572-130">Olá boa notícia é que há uma maneira de acesso remoto tooleave abrir e não se preocupar com senhas.</span><span class="sxs-lookup"><span data-stu-id="a9572-130">hello good news is that there is a way tooleave remote access open and not worry about passwords.</span></span> <span data-ttu-id="a9572-131">O método consiste na autenticação com criptografia assimétrica.</span><span class="sxs-lookup"><span data-stu-id="a9572-131">This method consists of authentication with asymmetric cryptography.</span></span> <span data-ttu-id="a9572-132">Olá, chave privada do usuário é hello que concede a autenticação de saudação.</span><span class="sxs-lookup"><span data-stu-id="a9572-132">hello user’s private key is hello one that grants hello authentication.</span></span> <span data-ttu-id="a9572-133">Você pode até mesmo bloquear Olá conta de usuário toonot permitir a autenticação de senha.</span><span class="sxs-lookup"><span data-stu-id="a9572-133">You can even lock hello user’s account toonot allow password authentication.</span></span>

<span data-ttu-id="a9572-134">Outra vantagem desse método é que você não precisa toosign senhas diferentes em servidores toodifferent.</span><span class="sxs-lookup"><span data-stu-id="a9572-134">Another advantage of this method is that you do not need different passwords toosign in toodifferent servers.</span></span> <span data-ttu-id="a9572-135">Você pode autenticar usando Olá pessoal chave privada em todos os servidores, que impede que você tenha tooremember várias senhas.</span><span class="sxs-lookup"><span data-stu-id="a9572-135">You can authenticate by using hello personal private key on all servers, which prevents you from having tooremember several passwords.</span></span>



<span data-ttu-id="a9572-136">Siga estas etapas toogenerate Olá SSH da chave de autenticação.</span><span class="sxs-lookup"><span data-stu-id="a9572-136">Follow these steps toogenerate hello SSH authentication key.</span></span>

1. <span data-ttu-id="a9572-137">Baixe e instale o PuTTYgen da saudação local a seguir: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span><span class="sxs-lookup"><span data-stu-id="a9572-137">Download and install PuTTYgen from hello following location: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span></span>
2. <span data-ttu-id="a9572-138">Execute o Puttygen.exe.</span><span class="sxs-lookup"><span data-stu-id="a9572-138">Run Puttygen.exe.</span></span>
3. <span data-ttu-id="a9572-139">Clique em **gerar** toogenerate chaves de saudação.</span><span class="sxs-lookup"><span data-stu-id="a9572-139">Click **Generate** toogenerate hello keys.</span></span> <span data-ttu-id="a9572-140">No processo de saudação, você pode aumentar aleatoriedade pela movimentação do mouse Olá sobre a área em branco Olá na janela de saudação.</span><span class="sxs-lookup"><span data-stu-id="a9572-140">In hello process, you can increase randomness by moving hello mouse over hello blank area in hello window.</span></span>  
   <span data-ttu-id="a9572-141">![Captura de tela de gerador de chave puTTY que mostra Olá gerar novo botão de chave][1]</span><span class="sxs-lookup"><span data-stu-id="a9572-141">![PuTTY Key Generator screenshot that shows hello generate new key button][1]</span></span>
4. <span data-ttu-id="a9572-142">Depois de saudação Gerar processo, Puttygen.exe mostrará sua nova chave pública.</span><span class="sxs-lookup"><span data-stu-id="a9572-142">After hello generate process, Puttygen.exe will show your new public key.</span></span>  
   ![Captura de tela de gerador de chave puTTY que mostra a nova chave pública de saudação e hello Salvar botão da chave privada][2]
5. <span data-ttu-id="a9572-144">Selecione e copie a chave pública hello e salvá-lo em um arquivo chamado publicKey.pem.</span><span class="sxs-lookup"><span data-stu-id="a9572-144">Select and copy hello public key, and save it in a file named publicKey.pem.</span></span> <span data-ttu-id="a9572-145">Não clique **salva a chave pública**, pois Olá salvo o formato de arquivo da chave pública é diferente da chave pública de saudação que desejamos.</span><span class="sxs-lookup"><span data-stu-id="a9572-145">Don’t click **Save public key**, because hello saved public key’s file format is different from hello public key we want.</span></span>
6. <span data-ttu-id="a9572-146">Clique em **Salvar chave privada** e salve-a em um arquivo chamado privateKey.ppk.</span><span class="sxs-lookup"><span data-stu-id="a9572-146">Click **Save private key**, and save it in a file named privateKey.ppk.</span></span>

### <a name="step-2-create-hello-image-in-hello-azure-portal"></a><span data-ttu-id="a9572-147">Etapa 2: Criar a imagem de saudação em Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a9572-147">Step 2: Create hello image in hello Azure portal</span></span>
1. <span data-ttu-id="a9572-148">Em Olá [portal](https://portal.azure.com/), clique em **novo** em Olá barra de tarefas toocreate uma imagem.</span><span class="sxs-lookup"><span data-stu-id="a9572-148">In hello [portal](https://portal.azure.com/), click **New** in hello task bar toocreate an image.</span></span> <span data-ttu-id="a9572-149">Escolha Olá Linux imagem com base em suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="a9572-149">Then choose hello Linux image that is based on your needs.</span></span> <span data-ttu-id="a9572-150">Olá, exemplo a seguir usa Olá Ubuntu 14.04 imagem.</span><span class="sxs-lookup"><span data-stu-id="a9572-150">hello following example uses hello Ubuntu 14.04 image.</span></span>
<span data-ttu-id="a9572-151">![Captura de tela de portal Olá que mostra o botão novo Olá][3]</span><span class="sxs-lookup"><span data-stu-id="a9572-151">![Screenshot of hello portal that shows hello New button][3]</span></span>

2. <span data-ttu-id="a9572-152">Para **nome de Host**, especifique nome Olá Olá URL que você e os clientes da Internet usará tooaccess esta máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a9572-152">For **Host Name**, specify hello name for hello URL that you and Internet clients will use tooaccess this virtual machine.</span></span> <span data-ttu-id="a9572-153">Defina a última parte Olá de nome DNS hello, por exemplo, tomcatdemo.</span><span class="sxs-lookup"><span data-stu-id="a9572-153">Define hello last part of hello DNS name, for example, tomcatdemo.</span></span> <span data-ttu-id="a9572-154">Azure gera Olá URL como tomcatdemo.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="a9572-154">Azure will then generate hello URL as tomcatdemo.cloudapp.net.</span></span>  

3. <span data-ttu-id="a9572-155">Para **chave de autenticação SSH**, copie o valor de chave de saudação do arquivo de publicKey.pem hello, que contém chave pública de saudação gerado pelo PuTTYgen.</span><span class="sxs-lookup"><span data-stu-id="a9572-155">For **SSH Authentication Key**, copy hello key value from hello publicKey.pem file, which contains hello public key generated by PuTTYgen.</span></span>  
<span data-ttu-id="a9572-156">![Caixa de chave de autenticação SSH no portal de saudação][4]</span><span class="sxs-lookup"><span data-stu-id="a9572-156">![SSH Authentication Key box in hello portal][4]</span></span>

4. <span data-ttu-id="a9572-157">Defina as outras configurações conforme necessário e, em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a9572-157">Configure other settings as needed, and then click **Create**.</span></span>  

## <a name="phase-2-prepare-your-virtual-machine-for-tomcat7"></a><span data-ttu-id="a9572-158">Fase 2: Preparar sua máquina virtual para o Tomcat7</span><span class="sxs-lookup"><span data-stu-id="a9572-158">Phase 2: Prepare your virtual machine for Tomcat7</span></span>
<span data-ttu-id="a9572-159">Nesta fase, você configurar um ponto de extremidade para o tráfego do Tomcat e, em seguida, conecte-se tooyour nova máquina de virtual.</span><span class="sxs-lookup"><span data-stu-id="a9572-159">In this phase, you will configure an endpoint for Tomcat traffic, and then connect tooyour new virtual machine.</span></span>

### <a name="step-1-open-hello-http-port-tooallow-web-access"></a><span data-ttu-id="a9572-160">Etapa 1: Abrir o acesso via web do hello HTTP porta tooallow</span><span class="sxs-lookup"><span data-stu-id="a9572-160">Step 1: Open hello HTTP port tooallow web access</span></span>
<span data-ttu-id="a9572-161">Os pontos de extremidade no Azure são compostos por um protocolo TCP ou UDP juntamente com uma porta pública e privada.</span><span class="sxs-lookup"><span data-stu-id="a9572-161">Endpoints in Azure consist of a TCP or UDP protocol, along with a public and private port.</span></span> <span data-ttu-id="a9572-162">Olá privada porta é Olá que serviço Olá escutando tooon Olá VM.</span><span class="sxs-lookup"><span data-stu-id="a9572-162">hello private port is hello port that hello service is listening tooon hello virtual machine.</span></span> <span data-ttu-id="a9572-163">porta pública Olá é a porta Olá Olá serviço de nuvem do Azure escuta tooexternally para o tráfego de entrada, baseado na Internet.</span><span class="sxs-lookup"><span data-stu-id="a9572-163">hello public port is hello port that hello Azure cloud service listens tooexternally for incoming, Internet-based traffic.</span></span>  

<span data-ttu-id="a9572-164">A porta TCP 8080 é o número da porta padrão Olá Tomcat usa toolisten.</span><span class="sxs-lookup"><span data-stu-id="a9572-164">TCP port 8080 is hello default port number that Tomcat uses toolisten.</span></span> <span data-ttu-id="a9572-165">Se esta porta for aberta com um Ponto de Extremidade do Azure, você e outros clientes da Internet poderão acessar páginas do Tomcat.</span><span class="sxs-lookup"><span data-stu-id="a9572-165">If this port is opened with an Azure endpoint, you and other Internet clients can access Tomcat pages.</span></span>  

1. <span data-ttu-id="a9572-166">No portal de saudação, clique em **procurar** > **máquinas virtuais**e, em seguida, clique em máquina virtual Olá que você criou.</span><span class="sxs-lookup"><span data-stu-id="a9572-166">In hello portal, click **Browse** > **Virtual machines**, and then click hello virtual machine that you created.</span></span>  
   <span data-ttu-id="a9572-167">![Captura de tela de diretório do hello máquinas virtuais][5]</span><span class="sxs-lookup"><span data-stu-id="a9572-167">![Screenshot of hello Virtual machines directory][5]</span></span>
2. <span data-ttu-id="a9572-168">tooadd uma máquina virtual de tooyour de ponto de extremidade, clique em Olá **pontos de extremidade** caixa.</span><span class="sxs-lookup"><span data-stu-id="a9572-168">tooadd an endpoint tooyour virtual machine, click hello **Endpoints** box.</span></span>
   <span data-ttu-id="a9572-169">![Captura de tela que mostra a caixa de pontos de extremidade Olá][6]</span><span class="sxs-lookup"><span data-stu-id="a9572-169">![Screenshot that shows hello Endpoints box][6]</span></span>
3. <span data-ttu-id="a9572-170">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a9572-170">Click **Add**.</span></span>  

   1. <span data-ttu-id="a9572-171">Ponto de extremidade hello, insira um nome para o ponto de extremidade de saudação em **ponto de extremidade**e, em seguida, digite 80 na **porta pública**.</span><span class="sxs-lookup"><span data-stu-id="a9572-171">For hello endpoint, enter a name for hello endpoint in **Endpoint**, and then enter 80 in **Public Port**.</span></span>  

      <span data-ttu-id="a9572-172">Se você definir too80, número da porta tooinclude Olá Olá URL que é usado tooaccess Tomcat não é necessário.</span><span class="sxs-lookup"><span data-stu-id="a9572-172">If you set it too80, you don’t need tooinclude hello port number in hello URL that is used tooaccess Tomcat.</span></span> <span data-ttu-id="a9572-173">Por exemplo, http://tomcatdemo.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="a9572-173">For example, http://tomcatdemo.cloudapp.net.</span></span>    

      <span data-ttu-id="a9572-174">Se você definir o valor de tooanother, como 81, será necessário tooadd Olá porta número toohello URL tooaccess Tomcat.</span><span class="sxs-lookup"><span data-stu-id="a9572-174">If you set it tooanother value, such as 81, you need tooadd hello port number toohello URL tooaccess Tomcat.</span></span> <span data-ttu-id="a9572-175">Por exemplo, http://tomcatdemo.cloudapp.net:81/.</span><span class="sxs-lookup"><span data-stu-id="a9572-175">For example,  http://tomcatdemo.cloudapp.net:81/.</span></span>
   2. <span data-ttu-id="a9572-176">Digite 8080 em **Porta Privada**.</span><span class="sxs-lookup"><span data-stu-id="a9572-176">Enter 8080 in **Private Port**.</span></span> <span data-ttu-id="a9572-177">Por padrão, o Tomcat escuta a porta 8080 TCP.</span><span class="sxs-lookup"><span data-stu-id="a9572-177">By default, Tomcat listens on TCP port 8080.</span></span> <span data-ttu-id="a9572-178">Se você alterou a porta de escuta de padrão saudação do Tomcat, você deve atualizar **porta privada** toobe Olá mesmo Olá porta de escuta do Tomcat.</span><span class="sxs-lookup"><span data-stu-id="a9572-178">If you changed hello default listen port of Tomcat, you should update **Private Port** toobe hello same as hello Tomcat listen port.</span></span>  
      <span data-ttu-id="a9572-179">![Captura de tela da interface do usuário que mostra o comando Adicionar, a Porta Pública e a Porta Privada][7]</span><span class="sxs-lookup"><span data-stu-id="a9572-179">![Screenshot of UI that shows Add command, Public Port, and Private Port][7]</span></span>
4. <span data-ttu-id="a9572-180">Clique em **Okey** tooadd Olá ponto de extremidade tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="a9572-180">Click **OK** tooadd hello endpoint tooyour virtual machine.</span></span>

### <a name="step-2-connect-toohello-image-you-created"></a><span data-ttu-id="a9572-181">Etapa 2: Conectar-se a imagem toohello criada</span><span class="sxs-lookup"><span data-stu-id="a9572-181">Step 2: Connect toohello image you created</span></span>
<span data-ttu-id="a9572-182">Você pode escolher qualquer máquina virtual do SSH ferramenta tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="a9572-182">You can choose any SSH tool tooconnect tooyour virtual machine.</span></span> <span data-ttu-id="a9572-183">Neste exemplo, usamos PuTTY.</span><span class="sxs-lookup"><span data-stu-id="a9572-183">In this example, we use PuTTY.</span></span>  

1. <span data-ttu-id="a9572-184">Obter nome DNS de saudação de sua máquina virtual no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="a9572-184">Get hello DNS name of your virtual machine from hello portal.</span></span>
    1. <span data-ttu-id="a9572-185">Clique em **Procurar** > **Máquinas Virtuais**.</span><span class="sxs-lookup"><span data-stu-id="a9572-185">Click **Browse** > **Virtual machines**.</span></span>
    2. <span data-ttu-id="a9572-186">Selecione Olá nome da máquina virtual e, em seguida, clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="a9572-186">Select hello name of your virtual machine, and then click **Properties**.</span></span>
    3. <span data-ttu-id="a9572-187">Em Olá **propriedades** lado a lado, procure em Olá **nome de domínio** nome DNS do caixa tooget hello.</span><span class="sxs-lookup"><span data-stu-id="a9572-187">In hello **Properties** tile, look in hello **Domain Name** box tooget hello DNS name.</span></span>  

2. <span data-ttu-id="a9572-188">Obter o número da porta Olá para conexões SSH de saudação **SSH** caixa.</span><span class="sxs-lookup"><span data-stu-id="a9572-188">Get hello port number for SSH connections from hello **SSH** box.</span></span>  
<span data-ttu-id="a9572-189">![Captura de tela que mostra o número da porta de conexão do hello SSH][8]</span><span class="sxs-lookup"><span data-stu-id="a9572-189">![Screenshot that shows hello SSH connection port number][8]</span></span>

3. <span data-ttu-id="a9572-190">Baixe [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="a9572-190">Download [PuTTY](http://www.putty.org/).</span></span>  

4. <span data-ttu-id="a9572-191">Após o download, clique em arquivo executável do hello Putty.exe.</span><span class="sxs-lookup"><span data-stu-id="a9572-191">After downloading, click hello executable file Putty.exe.</span></span> <span data-ttu-id="a9572-192">Configuração PuTTY, configurar opções básicas de saudação com o nome de host de saudação e porta número que é obtido das propriedades de saudação de sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a9572-192">In PuTTY configuration, configure hello basic options with hello host name and port number that is obtained from hello properties of your virtual machine.</span></span>   
![Captura de tela que mostra as opções de nome e a porta de host de configuração PuTTY Olá][9]

5. <span data-ttu-id="a9572-194">No painel esquerdo do hello, clique em **Conexão** > **SSH** > **Auth**e, em seguida, clique em **procurar** toospecify local de saudação do arquivo de privateKey.ppk de saudação.</span><span class="sxs-lookup"><span data-stu-id="a9572-194">In hello left pane, click **Connection** > **SSH** > **Auth**, and then click **Browse** toospecify hello location of hello privateKey.ppk file.</span></span> <span data-ttu-id="a9572-195">arquivo de privateKey.ppk de Olá contém a chave privada de saudação que é gerado pelo PuTTYgen anteriormente hello "Fase 1: criar uma imagem" deste artigo.</span><span class="sxs-lookup"><span data-stu-id="a9572-195">hello privateKey.ppk file contains hello private key that is generated by PuTTYgen earlier in hello "Phase 1: Create an image" section of this article.</span></span>  
<span data-ttu-id="a9572-196">![Captura de tela que mostra a hierarquia de diretórios de Conexão hello e o botão Procurar][10]</span><span class="sxs-lookup"><span data-stu-id="a9572-196">![Screenshot that shows hello Connection directory hierarchy and Browse button][10]</span></span>

6. <span data-ttu-id="a9572-197">Clique em **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="a9572-197">Click **Open**.</span></span> <span data-ttu-id="a9572-198">Você pode ser alertado por uma caixa de mensagem.</span><span class="sxs-lookup"><span data-stu-id="a9572-198">You might be alerted by a message box.</span></span> <span data-ttu-id="a9572-199">Se você tiver configurado o nome DNS hello e número da porta corretamente, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="a9572-199">If you have configured hello DNS name and port number correctly, click **Yes**.</span></span>
<span data-ttu-id="a9572-200">![Captura de tela que mostra a notificação de saudação][11]</span><span class="sxs-lookup"><span data-stu-id="a9572-200">![Screenshot that shows hello notification][11]</span></span>

7. <span data-ttu-id="a9572-201">Você está tooenter solicitado seu nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="a9572-201">You are prompted tooenter your username.</span></span>  
![Captura de tela que mostra onde username tooenter][12]

8. <span data-ttu-id="a9572-203">Insira nome de usuário de saudação que você usou toocreate Olá VM em hello "Fase 1: criar uma imagem" seção neste artigo.</span><span class="sxs-lookup"><span data-stu-id="a9572-203">Enter hello username that you used toocreate hello virtual machine in hello "Phase 1: Create an image" section earlier in this article.</span></span> <span data-ttu-id="a9572-204">Você verá algo parecido com hello seguinte:</span><span class="sxs-lookup"><span data-stu-id="a9572-204">You will see something like hello following:</span></span>  
![Captura de tela que mostra a confirmação de autenticação Olá][13]

## <a name="phase-3-install-software"></a><span data-ttu-id="a9572-206">Fase 3: Instalar o software</span><span class="sxs-lookup"><span data-stu-id="a9572-206">Phase 3: Install software</span></span>
<span data-ttu-id="a9572-207">Nesta fase, você pode instalar o Java runtime environment hello, Tomcat7 e outros componentes de Tomcat7.</span><span class="sxs-lookup"><span data-stu-id="a9572-207">In this phase, you install hello Java runtime environment, Tomcat7, and other Tomcat7 components.</span></span>  

### <a name="java-runtime-environment"></a><span data-ttu-id="a9572-208">Java runtime environment</span><span class="sxs-lookup"><span data-stu-id="a9572-208">Java runtime environment</span></span>
<span data-ttu-id="a9572-209">O tomcat é escrito em Java.</span><span class="sxs-lookup"><span data-stu-id="a9572-209">Tomcat is written in Java.</span></span> <span data-ttu-id="a9572-210">Há dois tipos de JDKs (Kits de desenvolvimento Java), OpenJDK e Oracle JDK.</span><span class="sxs-lookup"><span data-stu-id="a9572-210">There are two kinds of Java Development Kits (JDKs), OpenJDK and Oracle JDK.</span></span> <span data-ttu-id="a9572-211">Você pode escolher Olá aquele que você deseja.</span><span class="sxs-lookup"><span data-stu-id="a9572-211">You can choose hello one you want.</span></span>  

> [!NOTE]
> <span data-ttu-id="a9572-212">Tanto JDKs tem quase Olá mesmo código para classes Olá Olá API Java, mas Olá código para a máquina virtual de saudação é diferente.</span><span class="sxs-lookup"><span data-stu-id="a9572-212">Both JDKs have almost hello same code for hello classes in hello Java API, but hello code for hello virtual machine is different.</span></span> <span data-ttu-id="a9572-213">OpenJDK tende a bibliotecas abertas toouse, enquanto tende a Oracle JDK toouse fechado aqueles.</span><span class="sxs-lookup"><span data-stu-id="a9572-213">OpenJDK tends toouse open libraries, while Oracle JDK tends toouse closed ones.</span></span> <span data-ttu-id="a9572-214">O Oracle JDK tem mais classes e alguns bugs corrigidos, sendo também mais estável que o OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="a9572-214">Oracle JDK has more classes and some fixed bugs, and Oracle JDK is more stable than OpenJDK.</span></span>

#### <a name="install-openjdk"></a><span data-ttu-id="a9572-215">Instalar o OpenJDK</span><span class="sxs-lookup"><span data-stu-id="a9572-215">Install OpenJDK</span></span>  

<span data-ttu-id="a9572-216">Use Olá toodownload comando OpenJDK a seguir.</span><span class="sxs-lookup"><span data-stu-id="a9572-216">Use hello following command toodownload OpenJDK.</span></span>   

    sudo apt-get update  
    sudo apt-get install openjdk-7-jre  


* <span data-ttu-id="a9572-217">toocreate toocontain um diretório Olá arquivos JDK:</span><span class="sxs-lookup"><span data-stu-id="a9572-217">toocreate a directory toocontain hello JDK files:</span></span>  

        sudo mkdir /usr/lib/jvm  
* <span data-ttu-id="a9572-218">arquivos JDK tooextract Olá no diretório usr/lib/jvm/hello:</span><span class="sxs-lookup"><span data-stu-id="a9572-218">tooextract hello JDK files into hello /usr/lib/jvm/ directory:</span></span>  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/

#### <a name="install-oracle-jdk"></a><span data-ttu-id="a9572-219">Instalar o Oracle JDK</span><span class="sxs-lookup"><span data-stu-id="a9572-219">Install Oracle JDK</span></span>


<span data-ttu-id="a9572-220">Use Olá toodownload comando Oracle JDK a seguir no site da Oracle de saudação.</span><span class="sxs-lookup"><span data-stu-id="a9572-220">Use hello following command toodownload Oracle JDK from hello Oracle website.</span></span>  

     wget --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u5-b13/jdk-8u5-linux-x64.tar.gz  
* <span data-ttu-id="a9572-221">toocreate toocontain um diretório Olá arquivos JDK:</span><span class="sxs-lookup"><span data-stu-id="a9572-221">toocreate a directory toocontain hello JDK files:</span></span>  

        sudo mkdir /usr/lib/jvm  
* <span data-ttu-id="a9572-222">arquivos JDK tooextract Olá no diretório usr/lib/jvm/hello:</span><span class="sxs-lookup"><span data-stu-id="a9572-222">tooextract hello JDK files into hello /usr/lib/jvm/ directory:</span></span>  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/  
* <span data-ttu-id="a9572-223">tooset Oracle JDK como Olá a máquina virtual Java com padrão:</span><span class="sxs-lookup"><span data-stu-id="a9572-223">tooset Oracle JDK as hello default Java virtual machine:</span></span>  

        sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk1.8.0_05/bin/java 100  

        sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk1.8.0_05/bin/javac 100  

#### <a name="confirm-that-java-installation-is-successful"></a><span data-ttu-id="a9572-224">Confirme se a instalação do Java foi bem-sucedida</span><span class="sxs-lookup"><span data-stu-id="a9572-224">Confirm that Java installation is successful</span></span>
<span data-ttu-id="a9572-225">Você pode usar um comando como Olá tootest a seguir se Olá Java runtime environment está instalado corretamente:</span><span class="sxs-lookup"><span data-stu-id="a9572-225">You can use a command like hello following tootest if hello Java runtime environment is installed correctly:</span></span>  

    java -version  

<span data-ttu-id="a9572-226">Se você instalou OpenJDK, você verá uma mensagem semelhante seguinte Olá: ![mensagem de instalação OpenJDK bem-sucedida][14]</span><span class="sxs-lookup"><span data-stu-id="a9572-226">If you installed OpenJDK, you should see a message like hello following: ![Successful OpenJDK installation message][14]</span></span>

<span data-ttu-id="a9572-227">Se você instalou o JDK da Oracle, você verá uma mensagem semelhante seguinte Olá: ![mensagem de instalação do JDK bem-sucedida do Oracle][15]</span><span class="sxs-lookup"><span data-stu-id="a9572-227">If you installed Oracle JDK, you should see a message like hello following: ![Successful Oracle JDK installation message][15]</span></span>

### <a name="install-tomcat7"></a><span data-ttu-id="a9572-228">Instalar o Tomcat7</span><span class="sxs-lookup"><span data-stu-id="a9572-228">Install Tomcat7</span></span>
<span data-ttu-id="a9572-229">Use Olá comando tooinstall Tomcat7 a seguir.</span><span class="sxs-lookup"><span data-stu-id="a9572-229">Use hello following command tooinstall Tomcat7.</span></span>  

    sudo apt-get install tomcat7  

<span data-ttu-id="a9572-230">Se você não estiver usando Tomcat7, use a variação apropriada Olá desse comando.</span><span class="sxs-lookup"><span data-stu-id="a9572-230">If you are not using Tomcat7, use hello appropriate variation of this command.</span></span>  

#### <a name="confirm-that-tomcat7-installation-is-successful"></a><span data-ttu-id="a9572-231">Confirme se a instalação do Tomcat7 foi bem-sucedida</span><span class="sxs-lookup"><span data-stu-id="a9572-231">Confirm that Tomcat7 installation is successful</span></span>
<span data-ttu-id="a9572-232">toocheck se Tomcat7 for instalado com êxito, procure o nome DNS do servidor do tooyour Tomcat.</span><span class="sxs-lookup"><span data-stu-id="a9572-232">toocheck if Tomcat7 is successfully installed, browse tooyour Tomcat server’s DNS name.</span></span> <span data-ttu-id="a9572-233">Neste artigo, URL de exemplo hello é http://tomcatexample.cloudapp.net/.</span><span class="sxs-lookup"><span data-stu-id="a9572-233">In this article, hello example URL is http://tomcatexample.cloudapp.net/.</span></span> <span data-ttu-id="a9572-234">Se você vir uma mensagem semelhante Olá seguinte, Tomcat7 está instalado corretamente.</span><span class="sxs-lookup"><span data-stu-id="a9572-234">If you see a message like hello following, Tomcat7 is installed correctly.</span></span>
<span data-ttu-id="a9572-235">![Mensagem de instalação bem-sucedida do Tomcat7][16]</span><span class="sxs-lookup"><span data-stu-id="a9572-235">![Successful Tomcat7 installation message][16]</span></span>

### <a name="install-other-tomcat7-components"></a><span data-ttu-id="a9572-236">Instalar outros componentes do Tomcat7</span><span class="sxs-lookup"><span data-stu-id="a9572-236">Install other Tomcat7 components</span></span>
<span data-ttu-id="a9572-237">Há outros componentes opcionais do Tomcat que você pode instalar.</span><span class="sxs-lookup"><span data-stu-id="a9572-237">There are other optional Tomcat components that you can install.</span></span>  

<span data-ttu-id="a9572-238">Saudação de uso **tomcat7 de pesquisa de cache apt sudo** toosee comando todos os componentes disponíveis hello.</span><span class="sxs-lookup"><span data-stu-id="a9572-238">Use hello **sudo apt-cache search tomcat7** command toosee all of hello available components.</span></span> <span data-ttu-id="a9572-239">Use Olá tooinstall comandos a seguir alguns componentes úteis.</span><span class="sxs-lookup"><span data-stu-id="a9572-239">Use hello following commands tooinstall some useful components.</span></span>  

    sudo apt-get install tomcat7-admin      #admin web applications

    sudo apt-get install tomcat7-user         #tools toocreate user instances  

## <a name="phase-4-configure-tomcat7"></a><span data-ttu-id="a9572-240">Fase 4: Configurar o Tomcat7</span><span class="sxs-lookup"><span data-stu-id="a9572-240">Phase 4: Configure Tomcat7</span></span>
<span data-ttu-id="a9572-241">Nesta fase, você administrará o Tomcat.</span><span class="sxs-lookup"><span data-stu-id="a9572-241">In this phase, you administer Tomcat.</span></span>

### <a name="start-and-stop-tomcat7"></a><span data-ttu-id="a9572-242">Iniciar e parar o Tomcat7</span><span class="sxs-lookup"><span data-stu-id="a9572-242">Start and stop Tomcat7</span></span>
<span data-ttu-id="a9572-243">servidor de Tomcat7 Olá é iniciado automaticamente quando você instalá-lo.</span><span class="sxs-lookup"><span data-stu-id="a9572-243">hello Tomcat7 server automatically starts when you install it.</span></span> <span data-ttu-id="a9572-244">Você também poderá iniciá-lo com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="a9572-244">You can also start it with hello following command:</span></span>   

    sudo /etc/init.d/tomcat7 start

<span data-ttu-id="a9572-245">toostop Tomcat7:</span><span class="sxs-lookup"><span data-stu-id="a9572-245">toostop Tomcat7:</span></span>

    sudo /etc/init.d/tomcat7 stop

<span data-ttu-id="a9572-246">status de saudação do tooview do Tomcat7:</span><span class="sxs-lookup"><span data-stu-id="a9572-246">tooview hello status of Tomcat7:</span></span>

    sudo /etc/init.d/tomcat7 status

<span data-ttu-id="a9572-247">serviços do Tomcat toorestart:</span><span class="sxs-lookup"><span data-stu-id="a9572-247">toorestart Tomcat services:</span></span> 

    sudo /etc/init.d/tomcat7 restart

### <a name="tomcat7-administration"></a><span data-ttu-id="a9572-248">Administração do Tomcat7</span><span class="sxs-lookup"><span data-stu-id="a9572-248">Tomcat7 administration</span></span>
<span data-ttu-id="a9572-249">Você pode editar tooset de arquivo de configuração do hello Tomcat usuário se suas credenciais de administrador.</span><span class="sxs-lookup"><span data-stu-id="a9572-249">You can edit hello Tomcat user configuration file tooset up your admin credentials.</span></span> <span data-ttu-id="a9572-250">Use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="a9572-250">Use hello following command:</span></span>  

    sudo vi  /etc/tomcat7/tomcat-users.xml   

<span data-ttu-id="a9572-251">Aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="a9572-251">Here is an example:</span></span>  
![Captura de tela que mostra a saída do comando Olá sudo vi][17]  

> [!NOTE]
> <span data-ttu-id="a9572-253">Crie uma senha forte para o nome de usuário de administrador hello.</span><span class="sxs-lookup"><span data-stu-id="a9572-253">Create a strong password for hello admin username.</span></span>  

<span data-ttu-id="a9572-254">Depois de editar esse arquivo, é necessário reiniciar os serviços de Tomcat7 com hello tooensure de comando que Olá alterações entrem em vigor a seguir:</span><span class="sxs-lookup"><span data-stu-id="a9572-254">After editing this file, you should restart Tomcat7 services with hello following command tooensure that hello changes take effect:</span></span>  

    sudo /etc/init.d/tomcat7 restart  

<span data-ttu-id="a9572-255">Abra seu navegador e digite **http://<your tomcat server DNS name>manager/html** como Olá URL.</span><span class="sxs-lookup"><span data-stu-id="a9572-255">Open your browser, and enter **http://<your tomcat server DNS name>/manager/html** as hello URL.</span></span> <span data-ttu-id="a9572-256">Por exemplo hello neste artigo, URL Olá é http://tomcatexample.cloudapp.net/manager/html.</span><span class="sxs-lookup"><span data-stu-id="a9572-256">For hello example in this article, hello URL is http://tomcatexample.cloudapp.net/manager/html.</span></span>  

<span data-ttu-id="a9572-257">Depois de se conectar, você verá algo semelhante seguinte de toohello:</span><span class="sxs-lookup"><span data-stu-id="a9572-257">After connecting, you should see something similar toohello following:</span></span>  
![Captura de tela da saudação Gerenciador de aplicativos da Web Tomcat][18]

## <a name="common-issues"></a><span data-ttu-id="a9572-259">Problemas comuns</span><span class="sxs-lookup"><span data-stu-id="a9572-259">Common issues</span></span>
### <a name="cant-access-hello-virtual-machine-with-tomcat-and-moodle-from-hello-internet"></a><span data-ttu-id="a9572-260">Não é possível acessar a máquina virtual Olá Tomcat e o Moodle de saudação da Internet</span><span class="sxs-lookup"><span data-stu-id="a9572-260">Can't access hello virtual machine with Tomcat and Moodle from hello Internet</span></span>
#### <a name="symptom"></a><span data-ttu-id="a9572-261">Sintoma</span><span class="sxs-lookup"><span data-stu-id="a9572-261">Symptom</span></span>  
  <span data-ttu-id="a9572-262">Tomcat está sendo executado, mas você não conseguir ver a página de padrão do Tomcat Olá com seu navegador.</span><span class="sxs-lookup"><span data-stu-id="a9572-262">Tomcat is running but you can’t see hello Tomcat default page with your browser.</span></span>
#### <a name="possible-root-cause"></a><span data-ttu-id="a9572-263">Possível causa raiz</span><span class="sxs-lookup"><span data-stu-id="a9572-263">Possible root cause</span></span>   

  * <span data-ttu-id="a9572-264">porta de escuta do Tomcat Olá não é Olá mesmo que a porta privada saudação do ponto de extremidade da sua máquina virtual para o tráfego do Tomcat.</span><span class="sxs-lookup"><span data-stu-id="a9572-264">hello Tomcat listen port is not hello same as hello private port of your virtual machine's endpoint for Tomcat traffic.</span></span>  

     <span data-ttu-id="a9572-265">Verifique a porta pública e privada configurações de ponto de extremidade de porta e verifique se a porta privada Olá é Olá mesmo Olá Tomcat a porta de escuta.</span><span class="sxs-lookup"><span data-stu-id="a9572-265">Check your public port and private port endpoint settings and make sure hello private port is hello same as hello Tomcat listen port.</span></span> <span data-ttu-id="a9572-266">Consulte a seção “Fase 1: Criar uma imagem” deste artigo para obter instruções sobre como configurar os pontos de extremidade para sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a9572-266">See "Phase 1: Create an image" section of this article for instructions on configuring endpoints for your virtual machine.</span></span>  

     <span data-ttu-id="a9572-267">Olá toodetermine Tomcat porta de escuta, abra /etc/httpd/conf/httpd.conf (versão do Red Hat) ou /etc/tomcat7/server.xml (versão Debian).</span><span class="sxs-lookup"><span data-stu-id="a9572-267">toodetermine hello Tomcat listen port, open /etc/httpd/conf/httpd.conf (Red Hat release), or /etc/tomcat7/server.xml (Debian release).</span></span> <span data-ttu-id="a9572-268">Por padrão, a saudação porta de escuta do Tomcat é 8080.</span><span class="sxs-lookup"><span data-stu-id="a9572-268">By default, hello Tomcat listen port is 8080.</span></span> <span data-ttu-id="a9572-269">Aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="a9572-269">Here is an example:</span></span>  

        <Connector port="8080" protocol="HTTP/1.1"  connectionTimeout="20000"   URIEncoding="UTF-8"            redirectPort="8443" />  

     <span data-ttu-id="a9572-270">Se você estiver usando uma máquina virtual que Debian ou Ubuntu e você deseja toochange saudação padrão porta do Tomcat escutar (por exemplo, 8081), você também deve abrir a porta Olá para o sistema operacional de saudação.</span><span class="sxs-lookup"><span data-stu-id="a9572-270">If you are using a virtual machine like Debian or Ubuntu and you want toochange hello default port of Tomcat Listen (for example 8081), you should also open hello port for hello operating system.</span></span> <span data-ttu-id="a9572-271">Primeiro, abra o perfil de saudação:</span><span class="sxs-lookup"><span data-stu-id="a9572-271">First, open hello profile:</span></span>  

        sudo vi /etc/default/tomcat7  

     <span data-ttu-id="a9572-272">Em seguida, remova a última linha de saudação e altere "não" muito "Sim".</span><span class="sxs-lookup"><span data-stu-id="a9572-272">Then uncomment hello last line and change “no” too“yes”.</span></span>  

        AUTHBIND=yes
  2. <span data-ttu-id="a9572-273">firewall Olá desabilitou Olá porta de escuta do Tomcat.</span><span class="sxs-lookup"><span data-stu-id="a9572-273">hello firewall has disabled hello listen port of Tomcat.</span></span>

     <span data-ttu-id="a9572-274">Você só pode ver a página do hello Tomcat padrão do host local hello.</span><span class="sxs-lookup"><span data-stu-id="a9572-274">You can only see hello Tomcat default page from hello local host.</span></span> <span data-ttu-id="a9572-275">problema de saudação é mais provável que porta hello, que é atendida tooby Tomcat, seja bloqueada pelo firewall hello.</span><span class="sxs-lookup"><span data-stu-id="a9572-275">hello problem is most likely that hello port, which is listened tooby Tomcat, is blocked by hello firewall.</span></span> <span data-ttu-id="a9572-276">Você pode usar a página da Web do hello w3m ferramenta toobrowse hello.</span><span class="sxs-lookup"><span data-stu-id="a9572-276">You can use hello w3m tool toobrowse hello webpage.</span></span> <span data-ttu-id="a9572-277">Olá comandos a seguir instalar w3m e procurar toohello Tomcat padrão página:</span><span class="sxs-lookup"><span data-stu-id="a9572-277">hello following commands install w3m and browse toohello Tomcat default page:</span></span>  


        <span data-ttu-id="a9572-278">sudo yum  install w3m w3m-img</span><span class="sxs-lookup"><span data-stu-id="a9572-278">sudo yum  install w3m w3m-img</span></span>


        <span data-ttu-id="a9572-279">w3m http://localhost:8080</span><span class="sxs-lookup"><span data-stu-id="a9572-279">w3m http://localhost:8080</span></span>  
#### <a name="solution"></a><span data-ttu-id="a9572-280">Solução</span><span class="sxs-lookup"><span data-stu-id="a9572-280">Solution</span></span>

  * <span data-ttu-id="a9572-281">Se Olá porta de escuta do Tomcat não está hello mesmo como a porta privada saudação do ponto de extremidade de saudação da máquina de virtual toohello tráfego, você precisará alterá porta privada Olá toobe Olá mesmo Olá porta de escuta do Tomcat.</span><span class="sxs-lookup"><span data-stu-id="a9572-281">If hello Tomcat listen port is not hello same as hello private port of hello endpoint for traffic toohello virtual machine, you need change hello private port toobe hello same as hello Tomcat listen port.</span></span>   
  2. <span data-ttu-id="a9572-282">Se Olá problema é causado por um firewall/iptables, adicione Olá linhas muito/etc/sysconfig/iptables a seguir.</span><span class="sxs-lookup"><span data-stu-id="a9572-282">If hello issue is caused by firewall/iptables, add hello following lines too/etc/sysconfig/iptables.</span></span> <span data-ttu-id="a9572-283">segunda linha de saudação é necessário apenas para tráfego https:</span><span class="sxs-lookup"><span data-stu-id="a9572-283">hello second line is only needed for https traffic:</span></span>  

      <span data-ttu-id="a9572-284">-A INPUT -p tcp -m tcp --dport 80 -j ACCEPT</span><span class="sxs-lookup"><span data-stu-id="a9572-284">-A INPUT -p tcp -m tcp --dport 80 -j ACCEPT</span></span>

      <span data-ttu-id="a9572-285">-A INPUT -p tcp -m tcp --dport 443 -j ACCEPT</span><span class="sxs-lookup"><span data-stu-id="a9572-285">-A INPUT -p tcp -m tcp --dport 443 -j ACCEPT</span></span>  

     > [!IMPORTANT]
     > <span data-ttu-id="a9572-286">Certifique-se de linhas anteriores Olá são posicionadas acima todas as linhas que globalmente seriam restringir o acesso, como a seguir Olá: - A -j rejeitar – rejeitar com proibido de host de icmp de entrada</span><span class="sxs-lookup"><span data-stu-id="a9572-286">Make sure hello previous lines are positioned above any lines that would globally restrict access, such as hello following: -A INPUT -j REJECT --reject-with icmp-host-prohibited</span></span>



<span data-ttu-id="a9572-287">iptables tooreload hello, executar Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="a9572-287">tooreload hello iptables, run hello following command:</span></span>

    service iptables restart

<span data-ttu-id="a9572-288">Isso foi testado no CentOS 6.3.</span><span class="sxs-lookup"><span data-stu-id="a9572-288">This has been tested on CentOS 6.3.</span></span>

### <a name="permission-denied-when-you-upload-project-files-toovarlibtomcat7webapps"></a><span data-ttu-id="a9572-289">Permissão negada ao carregar projeto arquivos muito/var/lib/tomcat7/webapps /</span><span class="sxs-lookup"><span data-stu-id="a9572-289">Permission denied when you upload project files too/var/lib/tomcat7/webapps/</span></span>
#### <a name="symptom"></a><span data-ttu-id="a9572-290">Sintoma</span><span class="sxs-lookup"><span data-stu-id="a9572-290">Symptom</span></span>
  <span data-ttu-id="a9572-291">Quando você usar uma máquina virtual do SFTP cliente (como FileZilla) tooconnect tooyour e navegue muito/var/lib/tomcat7/webapps/toopublish seu site, você obtém uma erro mensagem semelhante toohello a seguir:</span><span class="sxs-lookup"><span data-stu-id="a9572-291">When you use an SFTP client (such as FileZilla) tooconnect tooyour virtual machine and navigate too/var/lib/tomcat7/webapps/ toopublish your site, you get an error message similar toohello following:</span></span>  

     status:    Listing directory /var/lib/tomcat7/webapps
     Command:    put "C:\Users\liang\Desktop\info.jsp" "info.jsp"
     Error:    /var/lib/tomcat7/webapps/info.jsp: open for write: permission denied
     Error:    File transfer failed
#### <a name="possible-root-cause"></a><span data-ttu-id="a9572-292">Possível causa raiz</span><span class="sxs-lookup"><span data-stu-id="a9572-292">Possible root cause</span></span>
  <span data-ttu-id="a9572-293">Você não tem nenhuma pasta de /var/lib/tomcat7/webapps permissões tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="a9572-293">You have no permissions tooaccess hello /var/lib/tomcat7/webapps folder.</span></span>  
#### <a name="solution"></a><span data-ttu-id="a9572-294">Solução</span><span class="sxs-lookup"><span data-stu-id="a9572-294">Solution</span></span>  
  <span data-ttu-id="a9572-295">Você precisa de permissão de tooget da conta raiz de saudação.</span><span class="sxs-lookup"><span data-stu-id="a9572-295">You need tooget permission from hello root account.</span></span> <span data-ttu-id="a9572-296">Você pode alterar a propriedade Olá dessa pasta de raiz toohello nome de usuário usado ao provisionar a máquina de saudação.</span><span class="sxs-lookup"><span data-stu-id="a9572-296">You can change hello ownership of that folder from root toohello username you used when you provisioned hello machine.</span></span> <span data-ttu-id="a9572-297">Aqui está um exemplo com o nome da conta azureuser hello:</span><span class="sxs-lookup"><span data-stu-id="a9572-297">Here is an example with hello azureuser account name:</span></span>  

     sudo chown azureuser -R /var/lib/tomcat7/webapps

  <span data-ttu-id="a9572-298">Use permissões de Olá Olá -R opção tooapply para todos os arquivos dentro de um diretório também.</span><span class="sxs-lookup"><span data-stu-id="a9572-298">Use hello -R option tooapply hello permissions for all files inside of a directory too.</span></span>  

  <span data-ttu-id="a9572-299">Este comando também funciona para diretórios.</span><span class="sxs-lookup"><span data-stu-id="a9572-299">This command also works for directories.</span></span> <span data-ttu-id="a9572-300">as alterações da opção -R Olá Olá permissões para todos os arquivos e diretórios dentro do diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="a9572-300">hello -R option changes hello permissions for all files and directories inside hello directory.</span></span> <span data-ttu-id="a9572-301">Aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="a9572-301">Here is an example:</span></span>  

     sudo chown -R username:group directory  

  <span data-ttu-id="a9572-302">Esse comando altera a propriedade (usuário e grupo) para todos os arquivos e pastas que estão dentro do diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="a9572-302">This command changes ownership (both user and group) for all files and directories that are inside hello directory.</span></span>  

  <span data-ttu-id="a9572-303">Olá comando a seguir altera somente permissão de saudação do diretório da pasta hello.</span><span class="sxs-lookup"><span data-stu-id="a9572-303">hello following command only changes hello permission of hello folder directory.</span></span> <span data-ttu-id="a9572-304">arquivos de saudação e pastas dentro do diretório de saudação não são alteradas.</span><span class="sxs-lookup"><span data-stu-id="a9572-304">hello files and folders inside hello directory are not changed.</span></span>  

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
