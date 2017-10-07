---
title: "servidor de aplicativos Java aaaRun em uma VM clássico do Azure | Microsoft Docs"
description: "Este tutorial usa recursos criados com o modelo de implantação clássico hello e mostra como toocreate um Virtual do Windows do computador e configure-o servidor de aplicativos do Apache Tomcat toorun."
services: virtual-machines-windows
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: d627aa09-f7d6-4239-8110-f8fc5111b939
ms.service: virtual-machines-windows
ms.workload: web
ms.tgt_pltfrm: vm-windows
ms.devlang: Java
ms.topic: article
ms.date: 03/16/2017
ms.author: robmcm
ms.openlocfilehash: 2d9f586c9f628d3738522b320996b95b078d7454
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-java-application-server-on-a-virtual-machine-created-with-hello-classic-deployment-model"></a><span data-ttu-id="3f328-103">Como toorun um servidor de aplicativos Java em uma máquina virtual criada com o modelo de implantação clássico Olá</span><span class="sxs-lookup"><span data-stu-id="3f328-103">How toorun a Java application server on a virtual machine created with hello classic deployment model</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3f328-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="3f328-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="3f328-105">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="3f328-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="3f328-106">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="3f328-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="3f328-107">Para um modelo de Gerenciador de recursos toodeploy um aplicativo Web com o Java 8 e do Tomcat, consulte [aqui](https://azure.microsoft.com/documentation/templates/201-web-app-java-tomcat/).</span><span class="sxs-lookup"><span data-stu-id="3f328-107">For a Resource Manager template toodeploy a webapp with Java 8 and Tomcat, see [here](https://azure.microsoft.com/documentation/templates/201-web-app-java-tomcat/).</span></span>

<span data-ttu-id="3f328-108">Com o Azure, você pode usar os recursos de servidor de tooprovide uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3f328-108">With Azure, you can use a virtual machine tooprovide server capabilities.</span></span> <span data-ttu-id="3f328-109">Por exemplo, uma máquina virtual em execução no Azure pode ser configurado toohost um servidor de aplicativos Java, como o Apache Tomcat.</span><span class="sxs-lookup"><span data-stu-id="3f328-109">As an example, a virtual machine running on Azure can be configured toohost a Java application server, such as Apache Tomcat.</span></span>

<span data-ttu-id="3f328-110">Depois de concluir este guia, você terá uma compreensão de como toocreate uma máquina virtual em execução no Azure e configurá-lo toorun um servidor de aplicativos Java.</span><span class="sxs-lookup"><span data-stu-id="3f328-110">After completing this guide, you will have an understanding of how toocreate a virtual machine running on Azure and configure it toorun a Java application server.</span></span> <span data-ttu-id="3f328-111">Você saiba e executar Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="3f328-111">You will learn and perform hello following tasks:</span></span>

* <span data-ttu-id="3f328-112">Como toocreate uma máquina virtual do computador que tem um Java Development Kit (JDK) já está instalado.</span><span class="sxs-lookup"><span data-stu-id="3f328-112">How toocreate a virtual machine that has a Java Development Kit (JDK) already installed.</span></span>
* <span data-ttu-id="3f328-113">Como tooremotely entrar na máquina virtual de tooyour.</span><span class="sxs-lookup"><span data-stu-id="3f328-113">How tooremotely sign in tooyour virtual machine.</span></span>
* <span data-ttu-id="3f328-114">Como tooinstall um servidor de aplicativos Java – Apache Tomcat - em sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3f328-114">How tooinstall a Java application server--Apache Tomcat--on your virtual machine.</span></span>
* <span data-ttu-id="3f328-115">Como toocreate um ponto de extremidade para sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3f328-115">How toocreate an endpoint for your virtual machine.</span></span>
* <span data-ttu-id="3f328-116">Como tooopen uma porta no hello de firewall para o servidor de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="3f328-116">How tooopen a port in hello firewall for your application server.</span></span>

<span data-ttu-id="3f328-117">Olá concluída resultados da instalação no Tomcat em execução em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3f328-117">hello completed installation results in Tomcat running on a virtual machine.</span></span>

![Máquina virtual executando o Apache Tomcat][virtual_machine_tomcat]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="toocreate-a-virtual-machine"></a><span data-ttu-id="3f328-119">toocreate uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="3f328-119">toocreate a virtual machine</span></span>
1. <span data-ttu-id="3f328-120">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3f328-120">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="3f328-121">Clique em **novo**, clique em **de computação**, em seguida, clique em **ver todos os** em Olá **aplicativos em destaque**.</span><span class="sxs-lookup"><span data-stu-id="3f328-121">Click **New**, click **Compute**, then click **See all** in hello **Featured apps**.</span></span>
3. <span data-ttu-id="3f328-122">Clique em **JDK**, clique em **JDK 8** em Olá **JDK** painel.</span><span class="sxs-lookup"><span data-stu-id="3f328-122">Click **JDK**, click **JDK 8** in hello **JDK** pane.</span></span>  
   <span data-ttu-id="3f328-123">Imagens de máquina virtual que dão suporte a **JDK 6** e **JDK 7** estão disponíveis se você tiver aplicativos herdados que não estão pronto toorun JDK 8.</span><span class="sxs-lookup"><span data-stu-id="3f328-123">Virtual machine images that support **JDK 6** and **JDK 7** are available if you have legacy applications that are not ready toorun in JDK 8.</span></span>
4. <span data-ttu-id="3f328-124">No painel de saudação JDK 8 Selecione **clássico**, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="3f328-124">In hello JDK 8 pane, select **Classic**, then click **Create**.</span></span>
5. <span data-ttu-id="3f328-125">Em Olá **Noções básicas sobre** folha:</span><span class="sxs-lookup"><span data-stu-id="3f328-125">In hello **Basics** blade:</span></span>
   1. <span data-ttu-id="3f328-126">Especifique um nome para a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="3f328-126">Specify a name for hello virtual machine.</span></span>
   2. <span data-ttu-id="3f328-127">Insira um nome para o administrador de saudação em Olá **nome de usuário** campo.</span><span class="sxs-lookup"><span data-stu-id="3f328-127">Enter a name for hello administrator in hello **User Name** field.</span></span> <span data-ttu-id="3f328-128">Lembre-se esse nome e Olá senha associada que segue no campo próximo hello.</span><span class="sxs-lookup"><span data-stu-id="3f328-128">Remember this name and hello associated password that follows in hello next field.</span></span> <span data-ttu-id="3f328-129">Você precisa-os quando entram remotamente na máquina virtual de toohello.</span><span class="sxs-lookup"><span data-stu-id="3f328-129">You need them when you remotely sign in toohello virtual machine.</span></span>
   3. <span data-ttu-id="3f328-130">Digite uma senha na Olá **nova senha** campo e digite-a novamente no hello **Confirmar senha** campo.</span><span class="sxs-lookup"><span data-stu-id="3f328-130">Enter a password in hello **New password** field, and reenter it in hello **Confirm password** field.</span></span> <span data-ttu-id="3f328-131">Essa senha é para Olá conta de administrador.</span><span class="sxs-lookup"><span data-stu-id="3f328-131">This password is for hello Administrator account.</span></span>
   4. <span data-ttu-id="3f328-132">Selecione Olá apropriado **assinatura**.</span><span class="sxs-lookup"><span data-stu-id="3f328-132">Select hello appropriate **Subscription**.</span></span>
   5. <span data-ttu-id="3f328-133">Para Olá **grupo de recursos**, clique em **criar novo** e insira o nome de saudação do novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3f328-133">For hello **Resource group**, click **Create new** and enter hello name of a new resource group.</span></span> <span data-ttu-id="3f328-134">Ou, clique em **usar existente** e selecione um dos grupos de recursos disponíveis de saudação.</span><span class="sxs-lookup"><span data-stu-id="3f328-134">Or, click **Use existing** and select one of hello available resource groups.</span></span>
   6. <span data-ttu-id="3f328-135">Selecione um local onde Olá máquina de virtual reside, como **Centro Sul dos EUA**.</span><span class="sxs-lookup"><span data-stu-id="3f328-135">Select a location where hello virtual machine resides, such as **South Central US**.</span></span>
6. <span data-ttu-id="3f328-136">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="3f328-136">Click **Next**.</span></span>
7. <span data-ttu-id="3f328-137">Em Olá **tamanho da imagem de máquina Virtual** folha, selecione **A1 padrão** ou outra imagem apropriada.</span><span class="sxs-lookup"><span data-stu-id="3f328-137">In hello **Virtual machine image size** blade, select **A1 Standard** or another appropriate image.</span></span>
8. <span data-ttu-id="3f328-138">Clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="3f328-138">Click **Select**.</span></span>

9. <span data-ttu-id="3f328-139">Em Olá **configurações** folha, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="3f328-139">In hello **Settings** blade, click **OK**.</span></span> <span data-ttu-id="3f328-140">Você pode usar valores padrão de saudação fornecidos pelo Azure.</span><span class="sxs-lookup"><span data-stu-id="3f328-140">You can use hello default values provided by Azure.</span></span>  
10. <span data-ttu-id="3f328-141">Em Olá **resumo** folha, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="3f328-141">In hello **Summary** blade, click **OK**.</span></span>

## <a name="tooremotely-sign-in-tooyour-virtual-machine"></a><span data-ttu-id="3f328-142">tooremotely logon na máquina virtual de tooyour</span><span class="sxs-lookup"><span data-stu-id="3f328-142">tooremotely sign in tooyour virtual machine</span></span>
1. <span data-ttu-id="3f328-143">Faça logon no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3f328-143">Log on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3f328-144">Clique em **Máquinas virtuais (clássicas)**.</span><span class="sxs-lookup"><span data-stu-id="3f328-144">Click **Virtual machines (classic)**.</span></span> <span data-ttu-id="3f328-145">Se necessário, clique em **mais serviços** em Olá inferior esquerda em categorias de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="3f328-145">If needed, click **More services** at hello bottom left corner under hello service categories.</span></span> <span data-ttu-id="3f328-146">Olá **máquinas virtuais (clássicas)** entrada será listada em Olá **de computação** grupo.</span><span class="sxs-lookup"><span data-stu-id="3f328-146">hello **Virtual machines (classic)** entry is listed in hello **Compute** group.</span></span>
3. <span data-ttu-id="3f328-147">Clique Olá nome da máquina virtual Olá que você deseja toosign no.</span><span class="sxs-lookup"><span data-stu-id="3f328-147">Click hello name of hello virtual machine that you want toosign in to.</span></span>
4. <span data-ttu-id="3f328-148">Após a inicialização da máquina virtual hello, um menu na parte superior de saudação do painel Olá permite conexões.</span><span class="sxs-lookup"><span data-stu-id="3f328-148">After hello virtual machine has started, a menu at hello top of hello pane allows connections.</span></span>
5. <span data-ttu-id="3f328-149">Clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="3f328-149">Click **Connect**.</span></span>
6. <span data-ttu-id="3f328-150">Responda toohello prompts como máquina de virtual toohello tooconnect necessários.</span><span class="sxs-lookup"><span data-stu-id="3f328-150">Respond toohello prompts as needed tooconnect toohello virtual machine.</span></span> <span data-ttu-id="3f328-151">Normalmente, você salva ou abre arquivo. rdp Olá que contém os detalhes de conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="3f328-151">Typically, you save or open hello .rdp file that contains hello connection details.</span></span> <span data-ttu-id="3f328-152">Você pode ter toocopy Olá url: porta como a última parte Olá da primeira linha de saudação do arquivo. rdp de saudação e cole-o em um aplicativo de logon remoto.</span><span class="sxs-lookup"><span data-stu-id="3f328-152">You might have toocopy hello url:port as hello last part of hello first line of hello .rdp file and paste it in a remote sign-in application.</span></span>

## <a name="tooinstall-a-java-application-server-on-your-virtual-machine"></a><span data-ttu-id="3f328-153">tooinstall um servidor de aplicativos Java em sua máquina virtual</span><span class="sxs-lookup"><span data-stu-id="3f328-153">tooinstall a Java application server on your virtual machine</span></span>
<span data-ttu-id="3f328-154">Você pode copiar uma máquina virtual do Java application server tooyour, ou você pode instalar um servidor de aplicativos Java por meio de um instalador.</span><span class="sxs-lookup"><span data-stu-id="3f328-154">You can copy a Java application server tooyour virtual machine, or you can install a Java application server through an installer.</span></span>

<span data-ttu-id="3f328-155">Este tutorial usa Tomcat como Olá Java application server tooinstall.</span><span class="sxs-lookup"><span data-stu-id="3f328-155">This tutorial uses Tomcat as hello Java application server tooinstall.</span></span>

1. <span data-ttu-id="3f328-156">Quando você está conectado na máquina virtual de tooyour, abra uma sessão do navegador muito[Apache Tomcat](http://tomcat.apache.org/download-80.cgi).</span><span class="sxs-lookup"><span data-stu-id="3f328-156">When you are signed in tooyour virtual machine, open a browser session too[Apache Tomcat](http://tomcat.apache.org/download-80.cgi).</span></span>
2. <span data-ttu-id="3f328-157">Clique duas vezes no link Olá para **instalador de serviço do Windows de 32 bits/64 bits**.</span><span class="sxs-lookup"><span data-stu-id="3f328-157">Double-click hello link for **32-bit/64-bit Windows Service Installer**.</span></span> <span data-ttu-id="3f328-158">Ao usar essa técnica, o Tomcat é instalado como um serviço Windows.</span><span class="sxs-lookup"><span data-stu-id="3f328-158">By using this technique, Tomcat installs as a Windows service.</span></span>
3. <span data-ttu-id="3f328-159">Quando solicitado, escolha o instalador de saudação toorun.</span><span class="sxs-lookup"><span data-stu-id="3f328-159">When prompted, choose toorun hello installer.</span></span>
4. <span data-ttu-id="3f328-160">Dentro de saudação **Apache Tomcat instalação** assistente, siga Olá solicita tooinstall Tomcat.</span><span class="sxs-lookup"><span data-stu-id="3f328-160">Within hello **Apache Tomcat Setup** wizard, follow hello prompts tooinstall Tomcat.</span></span> <span data-ttu-id="3f328-161">Para fins de saudação deste tutorial, aceitando os padrões de saudação é bom.</span><span class="sxs-lookup"><span data-stu-id="3f328-161">For hello purposes of this tutorial, accepting hello defaults is fine.</span></span> <span data-ttu-id="3f328-162">Quando você chegar Olá **Olá Concluindo o Assistente de instalação do Apache Tomcat** caixa de diálogo, você pode verificar opcionalmente **executar Apache Tomcat** toohave início do Tomcat agora.</span><span class="sxs-lookup"><span data-stu-id="3f328-162">When you reach hello **Completing hello Apache Tomcat Setup Wizard** dialog box, you can optionally check **Run Apache Tomcat** toohave Tomcat start now.</span></span> <span data-ttu-id="3f328-163">Clique em **concluir** toocomplete Olá o processo de instalação do Tomcat.</span><span class="sxs-lookup"><span data-stu-id="3f328-163">Click **Finish** toocomplete hello Tomcat setup process.</span></span>

## <a name="toostart-tomcat"></a><span data-ttu-id="3f328-164">toostart Tomcat</span><span class="sxs-lookup"><span data-stu-id="3f328-164">toostart Tomcat</span></span>

<span data-ttu-id="3f328-165">Você pode iniciar manualmente Tomcat abrindo um prompt de comando em sua máquina virtual e executando o comando Olá **net&nbsp;iniciar&nbsp;Tomcat8**.</span><span class="sxs-lookup"><span data-stu-id="3f328-165">You can manually start Tomcat by opening a command prompt on your virtual machine and running hello command **net&nbsp;start&nbsp;Tomcat8**.</span></span>

<span data-ttu-id="3f328-166">Quando Tomcat estiver em execução, você pode acessar o Tomcat digitando a URL de saudação <http://localhost:8080> no navegador Olá máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3f328-166">Once Tomcat is running, you can access Tomcat by entering hello URL <http://localhost:8080> in hello virtual machine's browser.</span></span>

<span data-ttu-id="3f328-167">toosee Tomcat em execução de computadores externos, você precisa toocreate um ponto de extremidade e abre uma porta.</span><span class="sxs-lookup"><span data-stu-id="3f328-167">toosee Tomcat running from external machines, you need toocreate an endpoint and open a port.</span></span>

## <a name="toocreate-an-endpoint-for-your-virtual-machine"></a><span data-ttu-id="3f328-168">toocreate um ponto de extremidade para sua máquina virtual</span><span class="sxs-lookup"><span data-stu-id="3f328-168">toocreate an endpoint for your virtual machine</span></span>
1. <span data-ttu-id="3f328-169">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3f328-169">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3f328-170">Clique em **Máquinas virtuais (clássicas)**.</span><span class="sxs-lookup"><span data-stu-id="3f328-170">Click **Virtual machines (classic)**.</span></span>
3. <span data-ttu-id="3f328-171">Clique em nome de saudação da máquina virtual Olá que está executando o servidor de aplicativos Java.</span><span class="sxs-lookup"><span data-stu-id="3f328-171">Click hello name of hello virtual machine that is running your Java application server.</span></span>
4. <span data-ttu-id="3f328-172">Clique em **Pontos de Extremidade**.</span><span class="sxs-lookup"><span data-stu-id="3f328-172">Click **Endpoints**.</span></span>
5. <span data-ttu-id="3f328-173">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="3f328-173">Click **Add**.</span></span>
6. <span data-ttu-id="3f328-174">Em Olá **Adicionar ponto de extremidade** caixa de diálogo:</span><span class="sxs-lookup"><span data-stu-id="3f328-174">In hello **Add endpoint** dialog box:</span></span>
   1. <span data-ttu-id="3f328-175">Especifique um nome para o ponto de extremidade Olá; Por exemplo, **HttpIn**.</span><span class="sxs-lookup"><span data-stu-id="3f328-175">Specify a name for hello endpoint; for example, **HttpIn**.</span></span>
   2. <span data-ttu-id="3f328-176">Selecione **TCP** para o protocolo de saudação.</span><span class="sxs-lookup"><span data-stu-id="3f328-176">Select **TCP** for hello protocol.</span></span>
   3. <span data-ttu-id="3f328-177">Especifique **80** para a porta pública hello.</span><span class="sxs-lookup"><span data-stu-id="3f328-177">Specify **80** for hello public port.</span></span>
   4. <span data-ttu-id="3f328-178">Especifique **8080** para a porta privada hello.</span><span class="sxs-lookup"><span data-stu-id="3f328-178">Specify **8080** for hello private port.</span></span>
   5. <span data-ttu-id="3f328-179">Selecione **desabilitado** para Olá flutuante endereço IP.</span><span class="sxs-lookup"><span data-stu-id="3f328-179">Select **Disabled** for hello floating IP address.</span></span>
   6. <span data-ttu-id="3f328-180">Deixe a lista de controle de acesso hello como está.</span><span class="sxs-lookup"><span data-stu-id="3f328-180">Leave hello access control list as is.</span></span>
   7. <span data-ttu-id="3f328-181">Clique em Olá **Okey** botão caixa de diálogo tooclose hello e criar o ponto de extremidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="3f328-181">Click hello **OK** button tooclose hello dialog box and create hello endpoint.</span></span>

## <a name="tooopen-a-port-in-hello-firewall-for-your-virtual-machine"></a><span data-ttu-id="3f328-182">tooopen uma porta no firewall Olá para sua máquina virtual</span><span class="sxs-lookup"><span data-stu-id="3f328-182">tooopen a port in hello firewall for your virtual machine</span></span>
1. <span data-ttu-id="3f328-183">Entrar na máquina virtual de tooyour.</span><span class="sxs-lookup"><span data-stu-id="3f328-183">Sign in tooyour virtual machine.</span></span>
2. <span data-ttu-id="3f328-184">Clique em **Iniciar do Windows**.</span><span class="sxs-lookup"><span data-stu-id="3f328-184">Click **Windows Start**.</span></span>
3. <span data-ttu-id="3f328-185">Clique em **Painel de Controle**.</span><span class="sxs-lookup"><span data-stu-id="3f328-185">Click **Control Panel**.</span></span>
4. <span data-ttu-id="3f328-186">Clique em **Sistema e Segurança**, clique em **Firewall do Windows** e, em seguida, clique em **Configurações Avançadas**.</span><span class="sxs-lookup"><span data-stu-id="3f328-186">Click **System and Security**, click **Windows Firewall**, and then click **Advanced Settings**.</span></span>
5. <span data-ttu-id="3f328-187">Clique em **Regras de Entrada** e, em seguida, clique em **Nova Regra**.</span><span class="sxs-lookup"><span data-stu-id="3f328-187">Click **Inbound Rules**, and then click **New Rule**.</span></span>  
   <span data-ttu-id="3f328-188">![Nova regra de entrada][NewIBRule]</span><span class="sxs-lookup"><span data-stu-id="3f328-188">![New inbound rule][NewIBRule]</span></span>
6. <span data-ttu-id="3f328-189">Para Olá **tipo de regra**, selecione **porta**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="3f328-189">For hello **Rule Type**, select **Port**, and then click **Next**.</span></span>  
   <span data-ttu-id="3f328-190">![Nova porta de regra de entrada][NewRulePort]</span><span class="sxs-lookup"><span data-stu-id="3f328-190">![New inbound rule port][NewRulePort]</span></span>
7. <span data-ttu-id="3f328-191">Em Olá **protocolo e portas** tela, selecione **TCP**, especifique **8080** como Olá **porta local específica**e, em seguida, clique em **Próxima**.</span><span class="sxs-lookup"><span data-stu-id="3f328-191">On hello **Protocol and Ports** screen, select **TCP**, specify **8080** as hello **Specific local port**, and then click **Next**.</span></span>  
  <span data-ttu-id="3f328-192">![Nova regra de entrada][NewRuleProtocol]</span><span class="sxs-lookup"><span data-stu-id="3f328-192">![New inbound rule ][NewRuleProtocol]</span></span>
8. <span data-ttu-id="3f328-193">Em Olá **ação** tela, selecione **Permitir conexão Olá**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="3f328-193">On hello **Action** screen, select **Allow hello connection**, and then click **Next**.</span></span>
   <span data-ttu-id="3f328-194">![Nova ação de regra de entrada][NewRuleAction]</span><span class="sxs-lookup"><span data-stu-id="3f328-194">![New inbound rule action][NewRuleAction]</span></span>
9. <span data-ttu-id="3f328-195">Em Olá **perfil** tela, verifique se **domínio**, **privada**, e **pública** estão selecionados e, em seguida, clique em **Avançar** .</span><span class="sxs-lookup"><span data-stu-id="3f328-195">On hello **Profile** screen, ensure that **Domain**, **Private**, and **Public** are selected, and then click **Next**.</span></span>
   <span data-ttu-id="3f328-196">![Novo perfil de regra de entrada][NewRuleProfile]</span><span class="sxs-lookup"><span data-stu-id="3f328-196">![New inbound rule profile][NewRuleProfile]</span></span>
10. <span data-ttu-id="3f328-197">Em Olá **nome** tela, especifique um nome para a regra de saudação, como **HttpIn** (nome da regra de saudação não é necessário toomatch Olá ponto de extremidade nome, no entanto) e, em seguida, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="3f328-197">On hello **Name** screen, specify a name for hello rule, such as **HttpIn** (hello rule name is not required toomatch hello endpoint name, however), and then click **Finish**.</span></span>  
    <span data-ttu-id="3f328-198">![Nome da nova regra de entrada][NewRuleName]</span><span class="sxs-lookup"><span data-stu-id="3f328-198">![New inbound rule name][NewRuleName]</span></span>

<span data-ttu-id="3f328-199">Neste ponto, o site do Tomcat deverá estar visível em um navegador externo.</span><span class="sxs-lookup"><span data-stu-id="3f328-199">At this point, your Tomcat website should be viewable from an external browser.</span></span> <span data-ttu-id="3f328-200">Na janela de endereço do navegador hello, digite uma URL do formulário de saudação  **http://*sua\_DNS\_nome*. cloudapp.net**, onde ***sua\_DNS\_nome*** é nome DNS de saudação você especificou quando criou a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="3f328-200">In hello browser's address window, type a URL of hello form **http://*your\_DNS\_name*.cloudapp.net**, where ***your\_DNS\_name*** is hello DNS name you specified when you created hello virtual machine.</span></span>

## <a name="application-lifecycle-considerations"></a><span data-ttu-id="3f328-201">Considerações sobre o ciclo de vida do aplicativo</span><span class="sxs-lookup"><span data-stu-id="3f328-201">Application lifecycle considerations</span></span>
* <span data-ttu-id="3f328-202">Você pode criar seu próprio arquivo de aplicativo da web (WAR) e adicioná-lo toohello **webapps** pasta.</span><span class="sxs-lookup"><span data-stu-id="3f328-202">You could create your own web application archive (WAR) and add it toohello **webapps** folder.</span></span> <span data-ttu-id="3f328-203">Por exemplo, crie um projeto Web dinâmico JSP (Página de Serviço Java) básico e exporte-o como um arquivo WAR.</span><span class="sxs-lookup"><span data-stu-id="3f328-203">For example, create a basic Java Service Page (JSP) dynamic web project and export it as a WAR file.</span></span> <span data-ttu-id="3f328-204">Em seguida, copie Olá WAR toohello Apache Tomcat **webapps** pasta na máquina virtual de hello, em seguida, executá-lo em um navegador.</span><span class="sxs-lookup"><span data-stu-id="3f328-204">Next, copy hello WAR toohello Apache Tomcat **webapps** folder on hello virtual machine, then run it in a browser.</span></span>
* <span data-ttu-id="3f328-205">Por padrão quando Olá serviço Tomcat é instalado, ele é definido toostart manualmente.</span><span class="sxs-lookup"><span data-stu-id="3f328-205">By default when hello Tomcat service is installed, it is set toostart manually.</span></span> <span data-ttu-id="3f328-206">Você pode desativá-toostart automaticamente usando o snap-in de serviços de saudação.</span><span class="sxs-lookup"><span data-stu-id="3f328-206">You can switch it toostart automatically by using hello Services snap-in.</span></span> <span data-ttu-id="3f328-207">Inicie o snap-in de serviços de saudação clicando **inicial do Windows**, **ferramentas administrativas**e, em seguida, **serviços**.</span><span class="sxs-lookup"><span data-stu-id="3f328-207">Start hello Services snap-in by clicking **Windows Start**, **Administrative Tools**, and then **Services**.</span></span> <span data-ttu-id="3f328-208">Clique duas vezes em Olá **Apache Tomcat** de serviço e defina **o tipo de inicialização** muito**automática**.</span><span class="sxs-lookup"><span data-stu-id="3f328-208">Double-click hello **Apache Tomcat** service and set **Startup type** too**Automatic**.</span></span>

    ![Configuração de um serviço toostart automaticamente][service_automatic_startup]

    <span data-ttu-id="3f328-210">Olá benefício de ter Tomcat iniciar automaticamente é que ela começa em execução quando a máquina virtual de saudação é reinicializada (por exemplo, após a instalação atualizações de software que exigem uma reinicialização).</span><span class="sxs-lookup"><span data-stu-id="3f328-210">hello benefit of having Tomcat start automatically is that it starts running when hello virtual machine is rebooted (for example, after software updates that require a reboot are installed).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f328-211">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3f328-211">Next steps</span></span>
<span data-ttu-id="3f328-212">Você pode aprender sobre outros serviços (como o armazenamento do Azure, barramento de serviço e banco de dados SQL) que podem ser tooinclude com seus aplicativos Java.</span><span class="sxs-lookup"><span data-stu-id="3f328-212">You can learn about other services (such as Azure Storage, service bus, and SQL Database) that you may want tooinclude with your Java applications.</span></span> <span data-ttu-id="3f328-213">Exibir informações de saudação disponíveis a saudação [Central de desenvolvedores de Java](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="3f328-213">View hello information available at hello [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

[virtual_machine_tomcat]:media/java-run-tomcat-app-server/WA_VirtualMachineRunningApacheTomcat.png

[service_automatic_startup]:media/java-run-tomcat-app-server/WA_TomcatServiceAutomaticStart.png









[NewIBRule]:media/java-run-tomcat-app-server/NewInboundRule.png
[NewRulePort]:media/java-run-tomcat-app-server/NewRulePort.png
[NewRuleProtocol]:media/java-run-tomcat-app-server/NewRuleProtocol.png
[NewRuleAction]:media/java-run-tomcat-app-server/NewRuleAction.png
[NewRuleName]:media/java-run-tomcat-app-server/NewRuleName.png
[NewRuleProfile]:media/java-run-tomcat-app-server/NewRuleProfile.png


<!-- Deleted from hello "toocreate an ednpoint for your virtual mache" 3/17/2017,
     toouse hello new portal.
6. In hello **Add endpoint** dialog box, ensure **Add standalone endpoint** is selected, and then click **Next**.
7. In hello **New endpoint details** dialog box:
-->
