---
title: "Executar o servidor de aplicativos Java em uma VM clássica do Azure | Microsoft Docs"
description: "Este tutorial usa os recursos criados com o modelo de implantação clássico e mostra como criar uma Máquina virtual do Windows e configurá-la para executar o servidor de aplicativos do Apache Tomcat."
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
ms.openlocfilehash: 6e02f42613808bcb13c0057e9f8fcc1c02273e77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-run-a-java-application-server-on-a-virtual-machine-created-with-the-classic-deployment-model"></a><span data-ttu-id="27851-103">Como executar um servidor de aplicativos do Java em uma máquina virtual criada com o modelo de implantação clássico</span><span class="sxs-lookup"><span data-stu-id="27851-103">How to run a Java application server on a virtual machine created with the classic deployment model</span></span>
> [!IMPORTANT]
> <span data-ttu-id="27851-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="27851-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="27851-105">Este artigo aborda o uso do modelo de implantação Clássica.</span><span class="sxs-lookup"><span data-stu-id="27851-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="27851-106">A Microsoft recomenda que a maioria das implantações novas use o modelo do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="27851-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="27851-107">Para um modelo do Resource Manager para implantar um aplicativo Web com o Java 8 e o Tomcat, veja [aqui](https://azure.microsoft.com/documentation/templates/201-web-app-java-tomcat/).</span><span class="sxs-lookup"><span data-stu-id="27851-107">For a Resource Manager template to deploy a webapp with Java 8 and Tomcat, see [here](https://azure.microsoft.com/documentation/templates/201-web-app-java-tomcat/).</span></span>

<span data-ttu-id="27851-108">Com o Azure, você pode usar uma máquina virtual para fornecer recursos de servidor.</span><span class="sxs-lookup"><span data-stu-id="27851-108">With Azure, you can use a virtual machine to provide server capabilities.</span></span> <span data-ttu-id="27851-109">Como um exemplo, uma máquina virtual em execução no Azure pode ser configurada para hospedar um servidor de aplicativos Java, como o Apache Tomcat.</span><span class="sxs-lookup"><span data-stu-id="27851-109">As an example, a virtual machine running on Azure can be configured to host a Java application server, such as Apache Tomcat.</span></span>

<span data-ttu-id="27851-110">Depois de concluir este guia, você entenderá como criar uma máquina virtual em execução no Azure e configurá-la para executar um servidor de aplicativos Java.</span><span class="sxs-lookup"><span data-stu-id="27851-110">After completing this guide, you will have an understanding of how to create a virtual machine running on Azure and configure it to run a Java application server.</span></span> <span data-ttu-id="27851-111">Você aprenderá e executará as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="27851-111">You will learn and perform the following tasks:</span></span>

* <span data-ttu-id="27851-112">Como criar uma máquina virtual que já tenha um JDK (Java Development Kit) instalado.</span><span class="sxs-lookup"><span data-stu-id="27851-112">How to create a virtual machine that has a Java Development Kit (JDK) already installed.</span></span>
* <span data-ttu-id="27851-113">Entre remotamente na máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="27851-113">How to remotely sign in to your virtual machine.</span></span>
* <span data-ttu-id="27851-114">Como instalar um servidor de aplicativos Java – Apache Tomcat – na máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="27851-114">How to install a Java application server--Apache Tomcat--on your virtual machine.</span></span>
* <span data-ttu-id="27851-115">Criar um ponto de extremidade para a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="27851-115">How to create an endpoint for your virtual machine.</span></span>
* <span data-ttu-id="27851-116">Abrir uma porta no firewall para o servidor de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="27851-116">How to open a port in the firewall for your application server.</span></span>

<span data-ttu-id="27851-117">A instalação completa resulta na execução do Tomcat em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="27851-117">The completed installation results in Tomcat running on a virtual machine.</span></span>

![Máquina virtual executando o Apache Tomcat][virtual_machine_tomcat]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="to-create-a-virtual-machine"></a><span data-ttu-id="27851-119">Para criar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="27851-119">To create a virtual machine</span></span>
1. <span data-ttu-id="27851-120">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="27851-120">Sign in to the [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="27851-121">Clique em **Novo**, em **Computação** e, em seguida, em **Ver todos** nos **Aplicativos em destaque**.</span><span class="sxs-lookup"><span data-stu-id="27851-121">Click **New**, click **Compute**, then click **See all** in the **Featured apps**.</span></span>
3. <span data-ttu-id="27851-122">Clique em **JDK** e em **JDK 8** no painel **JDK**.</span><span class="sxs-lookup"><span data-stu-id="27851-122">Click **JDK**, click **JDK 8** in the **JDK** pane.</span></span>  
   <span data-ttu-id="27851-123">Imagens de máquina virtual que dão suporte ao **JDK 6** e ao **JDK 7** estão disponíveis se você tem aplicativos herdados que não estão prontos para serem executados no JDK 8.</span><span class="sxs-lookup"><span data-stu-id="27851-123">Virtual machine images that support **JDK 6** and **JDK 7** are available if you have legacy applications that are not ready to run in JDK 8.</span></span>
4. <span data-ttu-id="27851-124">No painel do JDK 8, selecione **Clássico** e, em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="27851-124">In the JDK 8 pane, select **Classic**, then click **Create**.</span></span>
5. <span data-ttu-id="27851-125">Na folha **Básico**:</span><span class="sxs-lookup"><span data-stu-id="27851-125">In the **Basics** blade:</span></span>
   1. <span data-ttu-id="27851-126">Especifique um nome para a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="27851-126">Specify a name for the virtual machine.</span></span>
   2. <span data-ttu-id="27851-127">Digite um nome para o administrador no campo **Nome do Usuário** .</span><span class="sxs-lookup"><span data-stu-id="27851-127">Enter a name for the administrator in the **User Name** field.</span></span> <span data-ttu-id="27851-128">Memorize esse nome e a senha associada mostrada no próximo campo.</span><span class="sxs-lookup"><span data-stu-id="27851-128">Remember this name and the associated password that follows in the next field.</span></span> <span data-ttu-id="27851-129">Você precisará deles quando entrar remotamente na máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="27851-129">You need them when you remotely sign in to the virtual machine.</span></span>
   3. <span data-ttu-id="27851-130">Insira uma senha no campo **Nova senha** e insira-a novamente no campo **Confirmar senha**.</span><span class="sxs-lookup"><span data-stu-id="27851-130">Enter a password in the **New password** field, and reenter it in the **Confirm password** field.</span></span> <span data-ttu-id="27851-131">Essa senha refere-se à conta de Administrador.</span><span class="sxs-lookup"><span data-stu-id="27851-131">This password is for the Administrator account.</span></span>
   4. <span data-ttu-id="27851-132">Selecione a **Assinatura** apropriada.</span><span class="sxs-lookup"><span data-stu-id="27851-132">Select the appropriate **Subscription**.</span></span>
   5. <span data-ttu-id="27851-133">Para o **Grupo de recursos**, clique em **Criar novo** e insira o nome de um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="27851-133">For the **Resource group**, click **Create new** and enter the name of a new resource group.</span></span> <span data-ttu-id="27851-134">Se preferir, clique em **Usar existente** e selecione um dos grupos de recursos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="27851-134">Or, click **Use existing** and select one of the available resource groups.</span></span>
   6. <span data-ttu-id="27851-135">Selecione uma localização em que a máquina virtual reside, como **Centro-Sul dos EUA**.</span><span class="sxs-lookup"><span data-stu-id="27851-135">Select a location where the virtual machine resides, such as **South Central US**.</span></span>
6. <span data-ttu-id="27851-136">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="27851-136">Click **Next**.</span></span>
7. <span data-ttu-id="27851-137">Na folha **Tamanho da imagem de máquina virtual**, selecione **A1 Padrão** ou outra imagem apropriada.</span><span class="sxs-lookup"><span data-stu-id="27851-137">In the **Virtual machine image size** blade, select **A1 Standard** or another appropriate image.</span></span>
8. <span data-ttu-id="27851-138">Clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="27851-138">Click **Select**.</span></span>

9. <span data-ttu-id="27851-139">Na folha **Configurações**, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="27851-139">In the **Settings** blade, click **OK**.</span></span> <span data-ttu-id="27851-140">É possível usar os valores padrão fornecidos pelo Azure.</span><span class="sxs-lookup"><span data-stu-id="27851-140">You can use the default values provided by Azure.</span></span>  
10. <span data-ttu-id="27851-141">Na folha **Resumo**, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="27851-141">In the **Summary** blade, click **OK**.</span></span>

## <a name="to-remotely-sign-in-to-your-virtual-machine"></a><span data-ttu-id="27851-142">Para entrar remotamente na máquina virtual</span><span class="sxs-lookup"><span data-stu-id="27851-142">To remotely sign in to your virtual machine</span></span>
1. <span data-ttu-id="27851-143">Faça logon no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="27851-143">Log on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="27851-144">Clique em **Máquinas virtuais (clássicas)**.</span><span class="sxs-lookup"><span data-stu-id="27851-144">Click **Virtual machines (classic)**.</span></span> <span data-ttu-id="27851-145">Se necessário, clique em **Mais serviços** no canto inferior esquerdo nas categorias de serviços.</span><span class="sxs-lookup"><span data-stu-id="27851-145">If needed, click **More services** at the bottom left corner under the service categories.</span></span> <span data-ttu-id="27851-146">A entrada **Máquinas virtuais (clássicas)** é listada no grupo **Computação**.</span><span class="sxs-lookup"><span data-stu-id="27851-146">The **Virtual machines (classic)** entry is listed in the **Compute** group.</span></span>
3. <span data-ttu-id="27851-147">Clique no nome da Máquina Virtual na qual você deseja entrar.</span><span class="sxs-lookup"><span data-stu-id="27851-147">Click the name of the virtual machine that you want to sign in to.</span></span>
4. <span data-ttu-id="27851-148">Depois que a máquina virtual for iniciada, um menu na parte superior do painel permitirá conexões.</span><span class="sxs-lookup"><span data-stu-id="27851-148">After the virtual machine has started, a menu at the top of the pane allows connections.</span></span>
5. <span data-ttu-id="27851-149">Clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="27851-149">Click **Connect**.</span></span>
6. <span data-ttu-id="27851-150">Responda às solicitações conforme necessário para se conectar à máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="27851-150">Respond to the prompts as needed to connect to the virtual machine.</span></span> <span data-ttu-id="27851-151">Normalmente, você salva ou abre o arquivo .rdp que contém os detalhes de conexão.</span><span class="sxs-lookup"><span data-stu-id="27851-151">Typically, you save or open the .rdp file that contains the connection details.</span></span> <span data-ttu-id="27851-152">Pode ser necessário copiar url:port como último parte da primeira linha do arquivo .rdp e colar essa informações em um aplicativo de entrada remoto.</span><span class="sxs-lookup"><span data-stu-id="27851-152">You might have to copy the url:port as the last part of the first line of the .rdp file and paste it in a remote sign-in application.</span></span>

## <a name="to-install-a-java-application-server-on-your-virtual-machine"></a><span data-ttu-id="27851-153">Para instalar um servidor de aplicativos Java em sua máquina virtual</span><span class="sxs-lookup"><span data-stu-id="27851-153">To install a Java application server on your virtual machine</span></span>
<span data-ttu-id="27851-154">Você pode copiar um servidor de aplicativos Java em sua máquina virtual ou instalar um servidor de aplicativos Java por meio de um instalador.</span><span class="sxs-lookup"><span data-stu-id="27851-154">You can copy a Java application server to your virtual machine, or you can install a Java application server through an installer.</span></span>

<span data-ttu-id="27851-155">Este tutorial usa o Tomcat como o servidor de aplicativos Java a ser instalado.</span><span class="sxs-lookup"><span data-stu-id="27851-155">This tutorial uses Tomcat as the Java application server to install.</span></span>

1. <span data-ttu-id="27851-156">Depois de se conectar à máquina virtual, abra uma sessão do navegador para [Apache Tomcat](http://tomcat.apache.org/download-80.cgi).</span><span class="sxs-lookup"><span data-stu-id="27851-156">When you are signed in to your virtual machine, open a browser session to [Apache Tomcat](http://tomcat.apache.org/download-80.cgi).</span></span>
2. <span data-ttu-id="27851-157">Clique duas vezes no link **Instalador de serviço do Windows de 32 bits/64 bits**.</span><span class="sxs-lookup"><span data-stu-id="27851-157">Double-click the link for **32-bit/64-bit Windows Service Installer**.</span></span> <span data-ttu-id="27851-158">Ao usar essa técnica, o Tomcat é instalado como um serviço Windows.</span><span class="sxs-lookup"><span data-stu-id="27851-158">By using this technique, Tomcat installs as a Windows service.</span></span>
3. <span data-ttu-id="27851-159">Quando solicitado, opte por executar o instalador.</span><span class="sxs-lookup"><span data-stu-id="27851-159">When prompted, choose to run the installer.</span></span>
4. <span data-ttu-id="27851-160">No assistente de **Configuração do Apache Tomcat** , siga os prompts para instalar o Tomcat.</span><span class="sxs-lookup"><span data-stu-id="27851-160">Within the **Apache Tomcat Setup** wizard, follow the prompts to install Tomcat.</span></span> <span data-ttu-id="27851-161">Para o objetivo deste tutorial, aceitar os padrões será o suficiente.</span><span class="sxs-lookup"><span data-stu-id="27851-161">For the purposes of this tutorial, accepting the defaults is fine.</span></span> <span data-ttu-id="27851-162">Quando você chegar à caixa de diálogo **Concluindo o Assistente de Instalação do Apache Tomcat**, poderá marcar opcionalmente **Executar o Apache Tomcat** para que o Tomcat inicie agora.</span><span class="sxs-lookup"><span data-stu-id="27851-162">When you reach the **Completing the Apache Tomcat Setup Wizard** dialog box, you can optionally check **Run Apache Tomcat** to have Tomcat start now.</span></span> <span data-ttu-id="27851-163">Clique em **Concluir** para concluir o processo de configuração do Tomcat.</span><span class="sxs-lookup"><span data-stu-id="27851-163">Click **Finish** to complete the Tomcat setup process.</span></span>

## <a name="to-start-tomcat"></a><span data-ttu-id="27851-164">Para iniciar o Tomcat</span><span class="sxs-lookup"><span data-stu-id="27851-164">To start Tomcat</span></span>

<span data-ttu-id="27851-165">É possível iniciar o Tomcat manualmente abrindo um prompt de comando na máquina virtual e executando o comando **net&nbsp;start&nbsp;Tomcat8**.</span><span class="sxs-lookup"><span data-stu-id="27851-165">You can manually start Tomcat by opening a command prompt on your virtual machine and running the command **net&nbsp;start&nbsp;Tomcat8**.</span></span>

<span data-ttu-id="27851-166">Quando o Tomcat estiver em execução, você poderá acessá-lo inserindo a URL <http://localhost:8080> no navegador da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="27851-166">Once Tomcat is running, you can access Tomcat by entering the URL <http://localhost:8080> in the virtual machine's browser.</span></span>

<span data-ttu-id="27851-167">Para ver o Tomcat em execução em máquinas externas, você precisará criar um ponto de extremidade e abrir uma porta.</span><span class="sxs-lookup"><span data-stu-id="27851-167">To see Tomcat running from external machines, you need to create an endpoint and open a port.</span></span>

## <a name="to-create-an-endpoint-for-your-virtual-machine"></a><span data-ttu-id="27851-168">Para criar um ponto de extremidade para sua máquina virtual</span><span class="sxs-lookup"><span data-stu-id="27851-168">To create an endpoint for your virtual machine</span></span>
1. <span data-ttu-id="27851-169">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="27851-169">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="27851-170">Clique em **Máquinas virtuais (clássicas)**.</span><span class="sxs-lookup"><span data-stu-id="27851-170">Click **Virtual machines (classic)**.</span></span>
3. <span data-ttu-id="27851-171">Clique no nome da máquina virtual que está executando o servidor de aplicativos Java.</span><span class="sxs-lookup"><span data-stu-id="27851-171">Click the name of the virtual machine that is running your Java application server.</span></span>
4. <span data-ttu-id="27851-172">Clique em **Pontos de Extremidade**.</span><span class="sxs-lookup"><span data-stu-id="27851-172">Click **Endpoints**.</span></span>
5. <span data-ttu-id="27851-173">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="27851-173">Click **Add**.</span></span>
6. <span data-ttu-id="27851-174">Na caixa de diálogo **Adicionar ponto de extremidade**:</span><span class="sxs-lookup"><span data-stu-id="27851-174">In the **Add endpoint** dialog box:</span></span>
   1. <span data-ttu-id="27851-175">Especifique um nome para o ponto de extremidade. Por exemplo, **HttpIn**.</span><span class="sxs-lookup"><span data-stu-id="27851-175">Specify a name for the endpoint; for example, **HttpIn**.</span></span>
   2. <span data-ttu-id="27851-176">Selecione **TCP** como o protocolo.</span><span class="sxs-lookup"><span data-stu-id="27851-176">Select **TCP** for the protocol.</span></span>
   3. <span data-ttu-id="27851-177">Especifique **80** para a porta pública.</span><span class="sxs-lookup"><span data-stu-id="27851-177">Specify **80** for the public port.</span></span>
   4. <span data-ttu-id="27851-178">Especifique **8080** para a porta privada.</span><span class="sxs-lookup"><span data-stu-id="27851-178">Specify **8080** for the private port.</span></span>
   5. <span data-ttu-id="27851-179">Selecione **Desabilitado** para o endereço IP flutuante.</span><span class="sxs-lookup"><span data-stu-id="27851-179">Select **Disabled** for the floating IP address.</span></span>
   6. <span data-ttu-id="27851-180">Deixe a lista de controle de acesso como está.</span><span class="sxs-lookup"><span data-stu-id="27851-180">Leave the access control list as is.</span></span>
   7. <span data-ttu-id="27851-181">Clique no botão **OK** para fechar a caixa de diálogo e criar o ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="27851-181">Click the **OK** button to close the dialog box and create the endpoint.</span></span>

## <a name="to-open-a-port-in-the-firewall-for-your-virtual-machine"></a><span data-ttu-id="27851-182">Para abrir uma porta no firewall para sua máquina virtual</span><span class="sxs-lookup"><span data-stu-id="27851-182">To open a port in the firewall for your virtual machine</span></span>
1. <span data-ttu-id="27851-183">Entre na máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="27851-183">Sign in to your virtual machine.</span></span>
2. <span data-ttu-id="27851-184">Clique em **Iniciar do Windows**.</span><span class="sxs-lookup"><span data-stu-id="27851-184">Click **Windows Start**.</span></span>
3. <span data-ttu-id="27851-185">Clique em **Painel de Controle**.</span><span class="sxs-lookup"><span data-stu-id="27851-185">Click **Control Panel**.</span></span>
4. <span data-ttu-id="27851-186">Clique em **Sistema e Segurança**, clique em **Firewall do Windows** e, em seguida, clique em **Configurações Avançadas**.</span><span class="sxs-lookup"><span data-stu-id="27851-186">Click **System and Security**, click **Windows Firewall**, and then click **Advanced Settings**.</span></span>
5. <span data-ttu-id="27851-187">Clique em **Regras de Entrada** e, em seguida, clique em **Nova Regra**.</span><span class="sxs-lookup"><span data-stu-id="27851-187">Click **Inbound Rules**, and then click **New Rule**.</span></span>  
   <span data-ttu-id="27851-188">![Nova regra de entrada][NewIBRule]</span><span class="sxs-lookup"><span data-stu-id="27851-188">![New inbound rule][NewIBRule]</span></span>
6. <span data-ttu-id="27851-189">Para o **Tipo de Regra**, selecione **Porta** e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="27851-189">For the **Rule Type**, select **Port**, and then click **Next**.</span></span>  
   <span data-ttu-id="27851-190">![Nova porta de regra de entrada][NewRulePort]</span><span class="sxs-lookup"><span data-stu-id="27851-190">![New inbound rule port][NewRulePort]</span></span>
7. <span data-ttu-id="27851-191">Na tela **Protocolo e Portas**, selecione **TCP**, especifique **8080** como a **Porta local específica** e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="27851-191">On the **Protocol and Ports** screen, select **TCP**, specify **8080** as the **Specific local port**, and then click **Next**.</span></span>  
  <span data-ttu-id="27851-192">![Nova regra de entrada][NewRuleProtocol]</span><span class="sxs-lookup"><span data-stu-id="27851-192">![New inbound rule ][NewRuleProtocol]</span></span>
8. <span data-ttu-id="27851-193">Na tela **Ação**, selecione **Permitir a conexão** e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="27851-193">On the **Action** screen, select **Allow the connection**, and then click **Next**.</span></span>
   <span data-ttu-id="27851-194">![Nova ação de regra de entrada][NewRuleAction]</span><span class="sxs-lookup"><span data-stu-id="27851-194">![New inbound rule action][NewRuleAction]</span></span>
9. <span data-ttu-id="27851-195">Na tela **Perfil**, verifique se **Domínio**, **Privado** e **Público** estão marcados e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="27851-195">On the **Profile** screen, ensure that **Domain**, **Private**, and **Public** are selected, and then click **Next**.</span></span>
   <span data-ttu-id="27851-196">![Novo perfil de regra de entrada][NewRuleProfile]</span><span class="sxs-lookup"><span data-stu-id="27851-196">![New inbound rule profile][NewRuleProfile]</span></span>
10. <span data-ttu-id="27851-197">Na tela **Nome**, especifique um nome para a regra, como **HttpIn** (no entanto, o nome da regra não precisa corresponder ao nome do ponto de extremidade) e clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="27851-197">On the **Name** screen, specify a name for the rule, such as **HttpIn** (the rule name is not required to match the endpoint name, however), and then click **Finish**.</span></span>  
    <span data-ttu-id="27851-198">![Nome da nova regra de entrada][NewRuleName]</span><span class="sxs-lookup"><span data-stu-id="27851-198">![New inbound rule name][NewRuleName]</span></span>

<span data-ttu-id="27851-199">Neste ponto, o site do Tomcat deverá estar visível em um navegador externo.</span><span class="sxs-lookup"><span data-stu-id="27851-199">At this point, your Tomcat website should be viewable from an external browser.</span></span> <span data-ttu-id="27851-200">Na janela de endereço do navegador, digite uma URL do formulário  **http://*sua\_DNS\_nome*. cloudapp.net**, onde ***sua\_DNS\_nome*** é o nome DNS que você especificou quando criou a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="27851-200">In the browser's address window, type a URL of the form **http://*your\_DNS\_name*.cloudapp.net**, where ***your\_DNS\_name*** is the DNS name you specified when you created the virtual machine.</span></span>

## <a name="application-lifecycle-considerations"></a><span data-ttu-id="27851-201">Considerações sobre o ciclo de vida do aplicativo</span><span class="sxs-lookup"><span data-stu-id="27851-201">Application lifecycle considerations</span></span>
* <span data-ttu-id="27851-202">Você pode criar o próprio arquivo web do aplicativo (WAR) e adicioná-lo à pasta **webapps** .</span><span class="sxs-lookup"><span data-stu-id="27851-202">You could create your own web application archive (WAR) and add it to the **webapps** folder.</span></span> <span data-ttu-id="27851-203">Por exemplo, crie um projeto Web dinâmico JSP (Página de Serviço Java) básico e exporte-o como um arquivo WAR.</span><span class="sxs-lookup"><span data-stu-id="27851-203">For example, create a basic Java Service Page (JSP) dynamic web project and export it as a WAR file.</span></span> <span data-ttu-id="27851-204">Em seguida, copie o WAR para a pasta **webapps** do Apache Tomcat na máquina virtual e, em seguida, execute-o em um navegador.</span><span class="sxs-lookup"><span data-stu-id="27851-204">Next, copy the WAR to the Apache Tomcat **webapps** folder on the virtual machine, then run it in a browser.</span></span>
* <span data-ttu-id="27851-205">Por padrão, quando o serviço Tomcat for instalado, ele será definido para iniciar manualmente.</span><span class="sxs-lookup"><span data-stu-id="27851-205">By default when the Tomcat service is installed, it is set to start manually.</span></span> <span data-ttu-id="27851-206">Você pode mudá-lo para iniciar automaticamente, usando o snap-in Serviços.</span><span class="sxs-lookup"><span data-stu-id="27851-206">You can switch it to start automatically by using the Services snap-in.</span></span> <span data-ttu-id="27851-207">Inicie o snap-in Serviços clicando em **Iniciar do Windows**, **Ferramentas Administrativas** e em **Serviços**.</span><span class="sxs-lookup"><span data-stu-id="27851-207">Start the Services snap-in by clicking **Windows Start**, **Administrative Tools**, and then **Services**.</span></span> <span data-ttu-id="27851-208">Clique duas vezes no serviço **Apache Tomcat** e defina **Tipo de inicialização** como **Automático**.</span><span class="sxs-lookup"><span data-stu-id="27851-208">Double-click the **Apache Tomcat** service and set **Startup type** to **Automatic**.</span></span>

    ![Configurando um serviço para iniciar automaticamente][service_automatic_startup]

    <span data-ttu-id="27851-210">A vantagem de fazer com que o Tomcat seja iniciado automaticamente é que ele começa a ser executado quando a máquina virtual é reinicializada (por exemplo, após a instalação das atualizações de software que exigem uma reinicialização).</span><span class="sxs-lookup"><span data-stu-id="27851-210">The benefit of having Tomcat start automatically is that it starts running when the virtual machine is rebooted (for example, after software updates that require a reboot are installed).</span></span>

## <a name="next-steps"></a><span data-ttu-id="27851-211">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="27851-211">Next steps</span></span>
<span data-ttu-id="27851-212">É possível saber mais sobre outros serviços (como o Armazenamento do Azure, barramento de serviço e Banco de Dados SQL) que talvez você deseje incluir nos aplicativos Java.</span><span class="sxs-lookup"><span data-stu-id="27851-212">You can learn about other services (such as Azure Storage, service bus, and SQL Database) that you may want to include with your Java applications.</span></span> <span data-ttu-id="27851-213">Exibir as informações disponíveis no [Central de desenvolvedores do Java](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="27851-213">View the information available at the [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

[virtual_machine_tomcat]:media/java-run-tomcat-app-server/WA_VirtualMachineRunningApacheTomcat.png

[service_automatic_startup]:media/java-run-tomcat-app-server/WA_TomcatServiceAutomaticStart.png









[NewIBRule]:media/java-run-tomcat-app-server/NewInboundRule.png
[NewRulePort]:media/java-run-tomcat-app-server/NewRulePort.png
[NewRuleProtocol]:media/java-run-tomcat-app-server/NewRuleProtocol.png
[NewRuleAction]:media/java-run-tomcat-app-server/NewRuleAction.png
[NewRuleName]:media/java-run-tomcat-app-server/NewRuleName.png
[NewRuleProfile]:media/java-run-tomcat-app-server/NewRuleProfile.png


<!-- Deleted from the "To create an ednpoint for your virtual mache" 3/17/2017,
     to use the new portal.
6. In the **Add endpoint** dialog box, ensure **Add standalone endpoint** is selected, and then click **Next**.
7. In the **New endpoint details** dialog box:
-->
