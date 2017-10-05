---
title: Aplicativo Java que requer muitos recursos computacionais em uma VM | Microsoft Docs
description: "Saiba como criar uma máquina virtual do Azure que execute aplicativos Java que requerem muitos recursos computacionais e podem ser monitorados por outro aplicativo Java."
services: virtual-machines-windows
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: ae6f2737-94c7-4569-9913-d871450c2827
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 8c51c0bb37e25ad61fe58a85dd641dabe0a1958c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-run-a-compute-intensive-task-in-java-on-a-virtual-machine"></a><span data-ttu-id="47d9e-103">Como executar uma tarefa com uso intenso de computação no Java em uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="47d9e-103">How to run a compute-intensive task in Java on a virtual machine</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="47d9e-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="47d9e-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="47d9e-105">Este artigo aborda o uso do modelo de implantação Clássica.</span><span class="sxs-lookup"><span data-stu-id="47d9e-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="47d9e-106">A Microsoft recomenda que a maioria das implantações novas use o modelo do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="47d9e-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="47d9e-107">Com o Azure, você pode usar uma máquina virtual para lidar com tarefas de computação intensiva.</span><span class="sxs-lookup"><span data-stu-id="47d9e-107">With Azure, you can use a virtual machine to handle compute-intensive tasks.</span></span> <span data-ttu-id="47d9e-108">Por exemplo, uma máquina virtual pode lidar com tarefas e fornecer resultados às máquinas dos clientes ou aos aplicativos móveis.</span><span class="sxs-lookup"><span data-stu-id="47d9e-108">For example, a virtual machine can handle tasks and deliver results to client machines or mobile applications.</span></span> <span data-ttu-id="47d9e-109">Depois de ler este artigo, você terá um entendimento de como criar uma máquina virtual que executa um aplicativo Java de computação intensiva que pode ser monitorado por outro aplicativo Java.</span><span class="sxs-lookup"><span data-stu-id="47d9e-109">After reading this article, you will have an understanding of how to create a virtual machine that runs a compute-intensive Java application that can be monitored by another Java application.</span></span>

<span data-ttu-id="47d9e-110">Este tutorial supõe que você sabe como criar aplicativos de console Java, pode importar bibliotecas para o seu aplicativo Java e pode gerar um arquivo Java (JAR).</span><span class="sxs-lookup"><span data-stu-id="47d9e-110">This tutorial assumes you know how to create Java console applications, can import libraries to your Java application, and can generate a Java archive (JAR).</span></span> <span data-ttu-id="47d9e-111">Nenhum conhecimento do Microsoft Azure é assumido.</span><span class="sxs-lookup"><span data-stu-id="47d9e-111">No knowledge of Microsoft Azure is assumed.</span></span>

<span data-ttu-id="47d9e-112">Você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="47d9e-112">You will learn:</span></span>

* <span data-ttu-id="47d9e-113">Como criar uma máquina virtual que já tenha um JDK (Java Development Kit) instalado.</span><span class="sxs-lookup"><span data-stu-id="47d9e-113">How to create a virtual machine with a Java Development Kit (JDK) already installed.</span></span>
* <span data-ttu-id="47d9e-114">Fazer logon remotamente na máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="47d9e-114">How to remotely log in to your virtual machine.</span></span>
* <span data-ttu-id="47d9e-115">Como criar um espaço de nomes de barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="47d9e-115">How to create a service bus namespace.</span></span>
* <span data-ttu-id="47d9e-116">Como criar um aplicativo Java que executa uma tarefa de computação intensiva.</span><span class="sxs-lookup"><span data-stu-id="47d9e-116">How to create a Java application that performs a compute-intensive task.</span></span>
* <span data-ttu-id="47d9e-117">Como criar um aplicativo Java que monitora o andamento da tarefa de computação intensiva.</span><span class="sxs-lookup"><span data-stu-id="47d9e-117">How to create a Java application that monitors the progress of the compute-intensive task.</span></span>
* <span data-ttu-id="47d9e-118">Como executar os aplicativos Java.</span><span class="sxs-lookup"><span data-stu-id="47d9e-118">How to run the Java applications.</span></span>
* <span data-ttu-id="47d9e-119">Como parar os aplicativos Java.</span><span class="sxs-lookup"><span data-stu-id="47d9e-119">How to stop the Java applications.</span></span>

<span data-ttu-id="47d9e-120">Este tutorial usará o problema do Caixeiro Viajante para a tarefa de computação intensiva.</span><span class="sxs-lookup"><span data-stu-id="47d9e-120">This tutorial will use the Traveling Salesman Problem for the compute-intensive task.</span></span> <span data-ttu-id="47d9e-121">Este é um exemplo do aplicativo Java que executa a tarefa de computação intensiva.</span><span class="sxs-lookup"><span data-stu-id="47d9e-121">The following is an example of the Java application running the compute-intensive task.</span></span>

![Solucionador de problemas do Caixeiro Viajante][solver_output]

<span data-ttu-id="47d9e-123">Este é um exemplo do aplicativo Java que monitora a tarefa de computação intensiva.</span><span class="sxs-lookup"><span data-stu-id="47d9e-123">The following is an example of the Java application monitoring the compute-intensive task.</span></span>

![Cliente de problemas do Caixeiro Viajante][client_output]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="to-create-a-virtual-machine"></a><span data-ttu-id="47d9e-125">Para criar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="47d9e-125">To create a virtual machine</span></span>
1. <span data-ttu-id="47d9e-126">Faça logon no [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="47d9e-126">Log in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="47d9e-127">Clique em **Nova**, clique em **Computação**, clique em **Máquina virtual** e, em seguida, clique em **Da Galeria**.</span><span class="sxs-lookup"><span data-stu-id="47d9e-127">Click **New**, click **Compute**, click **Virtual machine**, and then click **From Gallery**.</span></span>
3. <span data-ttu-id="47d9e-128">Na caixa de diálogo **Seleção de imagem da máquina virtual**, selecione **JDK 7 Windows Server 2012**.</span><span class="sxs-lookup"><span data-stu-id="47d9e-128">In the **Virtual machine image select** dialog box, select **JDK 7 Windows Server 2012**.</span></span>
   <span data-ttu-id="47d9e-129">Observe que o **JDK 6 Windows Server 2012** está disponível caso você tenha aplicativos legados que ainda não estejam prontos para serem executados no JDK 7.</span><span class="sxs-lookup"><span data-stu-id="47d9e-129">Note that **JDK 6 Windows Server 2012** is available in case you have legacy applications that are not yet ready to run in JDK 7.</span></span>
4. <span data-ttu-id="47d9e-130">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="47d9e-130">Click **Next**.</span></span>
5. <span data-ttu-id="47d9e-131">Na caixa de diálogo **Configuração da máquina virtual** :</span><span class="sxs-lookup"><span data-stu-id="47d9e-131">In the **Virtual machine configuration** dialog box:</span></span>
   1. <span data-ttu-id="47d9e-132">Especifique um nome para a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="47d9e-132">Specify a name for the virtual machine.</span></span>
   2. <span data-ttu-id="47d9e-133">Especifique o tamanho a ser usado para a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="47d9e-133">Specify the size to use for the virtual machine.</span></span>
   3. <span data-ttu-id="47d9e-134">Digite um nome para o administrador no campo **Nome do Usuário** .</span><span class="sxs-lookup"><span data-stu-id="47d9e-134">Enter a name for the administrator in the **User Name** field.</span></span> <span data-ttu-id="47d9e-135">Lembre-se do nome e da senha que você digitará a seguir, você irá usá-los ao fazer logon remotamente na máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="47d9e-135">Remember this name and the password you will enter next, you will use them when you remotely log in to the virtual machine.</span></span>
   4. <span data-ttu-id="47d9e-136">Digite uma senha no campo **Nova senha** e insira-a novamente no campo **Confirmar**.</span><span class="sxs-lookup"><span data-stu-id="47d9e-136">Enter a password in the **New password** field, and re-enter it in the **Confirm** field.</span></span> <span data-ttu-id="47d9e-137">Esta é a senha da conta do Administrador.</span><span class="sxs-lookup"><span data-stu-id="47d9e-137">This is the Administrator account password.</span></span>
   5. <span data-ttu-id="47d9e-138">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="47d9e-138">Click **Next**.</span></span>
6. <span data-ttu-id="47d9e-139">Na próxima caixa de diálogo **Configuração da máquina virtual** :</span><span class="sxs-lookup"><span data-stu-id="47d9e-139">In the next **Virtual machine configuration** dialog box:</span></span>
   1. <span data-ttu-id="47d9e-140">Para **Serviço de Nuvem**, use o padrão **Criar um novo serviço de nuvem**.</span><span class="sxs-lookup"><span data-stu-id="47d9e-140">For **Cloud service**, use the default **Create a new cloud service**.</span></span>
   2. <span data-ttu-id="47d9e-141">O valor de **Nome DNS do Serviço de Nuvem** deve ser exclusivo no cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="47d9e-141">The value for **Cloud service DNS name** must be unique across cloudapp.net.</span></span> <span data-ttu-id="47d9e-142">Se necessário, modifique esse valor para que o Azure indique que ele é exclusivo.</span><span class="sxs-lookup"><span data-stu-id="47d9e-142">If needed, modify this value so that Azure indicates it is unique.</span></span>
   3. <span data-ttu-id="47d9e-143">Especifique uma região, um grupo de afinidade ou uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="47d9e-143">Specify a region, affinity group, or virtual network.</span></span> <span data-ttu-id="47d9e-144">Para o objetivo deste tutorial, especifique uma região, como **Oeste dos Estados Unidos**.</span><span class="sxs-lookup"><span data-stu-id="47d9e-144">For purposes of this tutorial, specify a region such as **West US**.</span></span>
   4. <span data-ttu-id="47d9e-145">Para **Conta de Armazenamento**, selecione **Usar uma conta de armazenamento gerada automaticamente**.</span><span class="sxs-lookup"><span data-stu-id="47d9e-145">For **Storage Account**, select **Use an automatically generated storage account**.</span></span>
   5. <span data-ttu-id="47d9e-146">Para **Conjunto de Disponibilidade**, selecione **(Nenhum)**.</span><span class="sxs-lookup"><span data-stu-id="47d9e-146">For **Availability Set**, select **(None)**.</span></span>
   6. <span data-ttu-id="47d9e-147">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="47d9e-147">Click **Next**.</span></span>
7. <span data-ttu-id="47d9e-148">Na caixa de diálogo **Configuração da máquina virtual** final:</span><span class="sxs-lookup"><span data-stu-id="47d9e-148">In the final **Virtual machine configuration** dialog box:</span></span>
   1. <span data-ttu-id="47d9e-149">Aceite as entradas de ponto de extremidade padrão.</span><span class="sxs-lookup"><span data-stu-id="47d9e-149">Accept the default endpoint entries.</span></span>
   2. <span data-ttu-id="47d9e-150">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="47d9e-150">Click **Complete**.</span></span>

## <a name="to-remotely-log-in-to-your-virtual-machine"></a><span data-ttu-id="47d9e-151">Para fazer logon remotamente na máquina virtual</span><span class="sxs-lookup"><span data-stu-id="47d9e-151">To remotely log in to your virtual machine</span></span>
1. <span data-ttu-id="47d9e-152">Faça logon no [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="47d9e-152">Log on to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="47d9e-153">Clique em **Máquinas Virtuais**.</span><span class="sxs-lookup"><span data-stu-id="47d9e-153">Click **Virtual machines**.</span></span>
3. <span data-ttu-id="47d9e-154">Clique no nome da máquina virtual na qual você deseja fazer logon.</span><span class="sxs-lookup"><span data-stu-id="47d9e-154">Click the name of the virtual machine that you want to log in to.</span></span>
4. <span data-ttu-id="47d9e-155">Clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="47d9e-155">Click **Connect**.</span></span>
5. <span data-ttu-id="47d9e-156">Responda às solicitações conforme necessário para se conectar à máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="47d9e-156">Respond to the prompts as needed to connect to the virtual machine.</span></span> <span data-ttu-id="47d9e-157">Quando for solicitado o nome do administrador e a senha, use os valores que você forneceu quando criou a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="47d9e-157">When prompted for the administrator name and password, use the values that you provided when you created the virtual machine.</span></span>

<span data-ttu-id="47d9e-158">Observe que a funcionalidade do Service Bus do Azure requer que o certificado de Baltimore CyberTrust Root seja instalado como parte do armazenamento **cacerts** do JRE.</span><span class="sxs-lookup"><span data-stu-id="47d9e-158">Note that the Azure Service Bus functionality requires the Baltimore CyberTrust Root certificate to be installed as part of your JRE's **cacerts** store.</span></span> <span data-ttu-id="47d9e-159">Este certificado é automaticamente incluído no Java Runtime Environment (JRE) usado por este tutorial.</span><span class="sxs-lookup"><span data-stu-id="47d9e-159">This certificate is automatically included in the Java Runtime Environment (JRE) used by this tutorial.</span></span> <span data-ttu-id="47d9e-160">Se você não tem este certificado no armazenamento **cacerts** do JRE, consulte [Adicionar um certificado no repositório de certificados de autoridade de certificação Java][add_ca_cert] para obter informações sobre como adicioná-lo (bem como informações sobre como exibir os certificados no seu armazenamento cacerts).</span><span class="sxs-lookup"><span data-stu-id="47d9e-160">If you do not have this certificate in your JRE **cacerts** store, see [Adding a Certificate to the Java CA Certificate Store][add_ca_cert] for information on adding it (as well as information on viewing the certificates in your cacerts store).</span></span>

## <a name="how-to-create-a-service-bus-namespace"></a><span data-ttu-id="47d9e-161">Como criar um namespace do barramento de serviço</span><span class="sxs-lookup"><span data-stu-id="47d9e-161">How to create a service bus namespace</span></span>
<span data-ttu-id="47d9e-162">Para começar a usar filas do Barramento de Serviço no Azure, primeiro crie um namespace de serviço.</span><span class="sxs-lookup"><span data-stu-id="47d9e-162">To begin using Service Bus queues in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="47d9e-163">Um namespace de serviço fornece um contêiner de controle para endereçamento dos recursos do Barramento de Serviço em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="47d9e-163">A service namespace provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="47d9e-164">Para criar um namespace de serviço:</span><span class="sxs-lookup"><span data-stu-id="47d9e-164">To create a service namespace:</span></span>

1. <span data-ttu-id="47d9e-165">Faça logon no [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="47d9e-165">Log on to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="47d9e-166">No painel de navegação esquerdo inferior do portal clássico do Azure, clique em **Barramento de Serviço, Controle de Acesso e Caching**.</span><span class="sxs-lookup"><span data-stu-id="47d9e-166">In the lower-left navigation pane of the Azure classic portal, click **Service Bus, Access Control & Caching**.</span></span>
3. <span data-ttu-id="47d9e-167">No painel superior esquerdo do portal clássico do Azure, clique no nó de **Barramento de Serviço** e, em seguida, clique no botão **Novo**.</span><span class="sxs-lookup"><span data-stu-id="47d9e-167">In the upper-left pane of the Azure classic portal, click the **Service Bus** node, and then click the **New** button.</span></span>  
   <span data-ttu-id="47d9e-168">![Captura de tela do nó do Service Bus][svc_bus_node]</span><span class="sxs-lookup"><span data-stu-id="47d9e-168">![Service Bus Node screenshot][svc_bus_node]</span></span>
4. <span data-ttu-id="47d9e-169">Na caixa de diálogo **Criar um novo namespace de serviço**, digite um **Namespace** e, em seguida, para verificar se ele é exclusivo, clique no botão **Verificar Disponibilidade**.</span><span class="sxs-lookup"><span data-stu-id="47d9e-169">In the **Create a new Service Namespace** dialog box, enter a **Namespace**, and then to make sure that it is unique, click the **Check Availability** button.</span></span>  
   <span data-ttu-id="47d9e-170">![Criar uma captura de tela do novo Namespace][create_namespace]</span><span class="sxs-lookup"><span data-stu-id="47d9e-170">![Create a New Namespace screenshot][create_namespace]</span></span>
5. <span data-ttu-id="47d9e-171">Depois de verificar se o nome do namespace está disponível, escolha o país ou a região na qual o namespace deve estar hospedado e, em seguida, clique no botão **Criar Namespace** .</span><span class="sxs-lookup"><span data-stu-id="47d9e-171">After making sure the namespace name is available, choose the country or region in which your namespace should be hosted, and then click the **Create Namespace** button.</span></span>  
   
   <span data-ttu-id="47d9e-172">O namespace que você criou aparecerá no portal clássico do Azure e demorará algum tempo para ser ativado.</span><span class="sxs-lookup"><span data-stu-id="47d9e-172">The namespace you created will then appear in the Azure classic portal and takes a moment to activate.</span></span> <span data-ttu-id="47d9e-173">Aguarde até que o status esteja **Ativo** para passar à próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="47d9e-173">Wait until the status is **Active** before continuing with the next step.</span></span>

## <a name="obtain-the-default-management-credentials-for-the-namespace"></a><span data-ttu-id="47d9e-174">Obter as Credenciais de gerenciamento padrão do namespace</span><span class="sxs-lookup"><span data-stu-id="47d9e-174">Obtain the Default Management Credentials for the namespace</span></span>
<span data-ttu-id="47d9e-175">A fim de executar operações de gerenciamento, como criar uma fila no novo namespace, você precisar obter as credenciais de gerenciamento para o namespace.</span><span class="sxs-lookup"><span data-stu-id="47d9e-175">In order to perform management operations, such as creating a queue, on the new namespace, you need to obtain the management credentials for the namespace.</span></span>

1. <span data-ttu-id="47d9e-176">No painel de navegação esquerdo, clique no nó **Barramento de Serviço** para exibir a lista de namespaces disponíveis.</span><span class="sxs-lookup"><span data-stu-id="47d9e-176">In the left navigation pane, click the **Service Bus** node to display the list of available namespaces.</span></span>
   <span data-ttu-id="47d9e-177">![Captura de tela de namespaces disponíveis][avail_namespaces]</span><span class="sxs-lookup"><span data-stu-id="47d9e-177">![Available Namespaces screenshot][avail_namespaces]</span></span>
2. <span data-ttu-id="47d9e-178">Selecione o namespace que você acabou de criar na lista exibida.</span><span class="sxs-lookup"><span data-stu-id="47d9e-178">Select the namespace you just created from the list shown.</span></span>
   <span data-ttu-id="47d9e-179">![Captura de tela da lista de namespaces][namespace_list]</span><span class="sxs-lookup"><span data-stu-id="47d9e-179">![Namespace List screenshot][namespace_list]</span></span>
3. <span data-ttu-id="47d9e-180">O painel direito **Propriedades** listará as propriedades do novo namespace.</span><span class="sxs-lookup"><span data-stu-id="47d9e-180">The right-hand **Properties** pane lists the properties for the new namespace.</span></span>
   <span data-ttu-id="47d9e-181">![Captura de tela do painel Propriedades][properties_pane]</span><span class="sxs-lookup"><span data-stu-id="47d9e-181">![Properties Pane screenshot][properties_pane]</span></span>
4. <span data-ttu-id="47d9e-182">A **Chave padrão** está oculta.</span><span class="sxs-lookup"><span data-stu-id="47d9e-182">The **Default Key** is hidden.</span></span> <span data-ttu-id="47d9e-183">Clique no botão **Exibir** para exibir as credenciais de segurança.</span><span class="sxs-lookup"><span data-stu-id="47d9e-183">Click the **View** button to display the security credentials.</span></span>
   <span data-ttu-id="47d9e-184">![Captura de tela da chave padrão][default_key]</span><span class="sxs-lookup"><span data-stu-id="47d9e-184">![Default Key screenshot][default_key]</span></span>
5. <span data-ttu-id="47d9e-185">Anote o **Emissor Padrão** e a **Chave Padrão**, pois você usará essas informações abaixo para executar operações com o namespace.</span><span class="sxs-lookup"><span data-stu-id="47d9e-185">Make a note of the **Default Issuer** and the **Default Key** as you will use this information below to perform operations with the namespace.</span></span>

## <a name="how-to-create-a-java-application-that-performs-a-compute-intensive-task"></a><span data-ttu-id="47d9e-186">Como criar um aplicativo Java que executa uma tarefa de computação intensiva</span><span class="sxs-lookup"><span data-stu-id="47d9e-186">How to create a Java application that performs a compute-intensive task</span></span>
1. <span data-ttu-id="47d9e-187">Na sua máquina de desenvolvimento (que não tem de ser a máquina virtual que você criou), faça o download do [Azure SDK para Java](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="47d9e-187">On your development machine (which does not have to be the virtual machine that you created), download the [Azure SDK for Java](https://azure.microsoft.com/develop/java/).</span></span>
2. <span data-ttu-id="47d9e-188">Crie um aplicativo de console Java usando o código de exemplo no final desta seção.</span><span class="sxs-lookup"><span data-stu-id="47d9e-188">Create a Java console application using the example code at the end of this section.</span></span> <span data-ttu-id="47d9e-189">Neste tutorial, usaremos **TSPSolver.java** como o nome do arquivo Java.</span><span class="sxs-lookup"><span data-stu-id="47d9e-189">In this tutorial, we'll use **TSPSolver.java** as the Java file name.</span></span> <span data-ttu-id="47d9e-190">Modifique os espaços reservados **your\_service\_bus\_namespace**, **your\_service\_bus\_owner** e **your\_service\_bus\_key** para usar o **namespace** do barramento de serviço e os valores **Emissor Padrão** e **Chave Padrão**, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="47d9e-190">Modify the **your\_service\_bus\_namespace**, **your\_service\_bus\_owner**, and **your\_service\_bus\_key** placeholders to use your service bus **namespace**, **Default Issuer** and **Default Key** values, respectively.</span></span>
3. <span data-ttu-id="47d9e-191">Depois de codificar, exporte o aplicativo para um arquivo executável Java (JAR) e empacote as bibliotecas necessárias para o JAR gerado.</span><span class="sxs-lookup"><span data-stu-id="47d9e-191">After coding, export the application to a runnable Java archive (JAR), and package the required libraries into the generated JAR.</span></span> <span data-ttu-id="47d9e-192">Neste tutorial, usaremos **TSPSolver.jar** como o nome do arquivo JAR gerado.</span><span class="sxs-lookup"><span data-stu-id="47d9e-192">In this tutorial, we'll use **TSPSolver.jar** as the generated JAR name.</span></span>

<p/>

    // TSPSolver.java

    import com.microsoft.windowsazure.services.core.Configuration;
    import com.microsoft.windowsazure.services.core.ServiceException;
    import com.microsoft.windowsazure.services.serviceBus.*;
    import com.microsoft.windowsazure.services.serviceBus.models.*;
    import java.io.*;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import java.util.ArrayList;
    import java.util.Date;
    import java.util.List;

    public class TSPSolver {

        //  Value specifying how often to provide an update to the console.
        private static long loopCheck = 100000000;  

        private static long nTimes = 0, nLoops=0;

        private static double[][] distances;
        private static String[] cityNames;
        private static int[] bestOrder;
        private static double minDistance;
        private static ServiceBusContract service;

        private static void buildDistances(String fileLocation, int numCities) throws Exception{
            try{
                BufferedReader file = new BufferedReader(new InputStreamReader(new DataInputStream(new FileInputStream(new File(fileLocation)))));
                double[][] cityLocs = new double[numCities][2];
                for (int i = 0; i<numCities; i++){
                    String[] line = file.readLine().split(", ");
                    cityNames[i] = line[0];
                    cityLocs[i][0] = Double.parseDouble(line[1]);
                    cityLocs[i][1] = Double.parseDouble(line[2]);
                }
                for (int i = 0; i<numCities; i++){
                    for (int j = i; j<numCities; j++){
                        distances[i][j] = Math.hypot(Math.abs(cityLocs[i][0] - cityLocs[j][0]), Math.abs(cityLocs[i][1] - cityLocs[j][1]));
                        distances[j][i] = distances[i][j];
                    }
                }
            } catch (Exception e){
                throw e;
            }
        }

        private static void permutation(List<Integer> startCities, double distSoFar, List<Integer> restCities) throws Exception {

            try
            {
                nTimes++;
                if (nTimes == loopCheck)
                {
                    nLoops++;
                    nTimes = 0;
                    DateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");
                    Date date = new Date();
                    System.out.print("Current time is " + dateFormat.format(date) + ". ");
                    System.out.println(  "Completed " + nLoops + " iterations of size of " + loopCheck + ".");
                }

                if ((restCities.size() == 1) && ((minDistance == -1) || (distSoFar + distances[restCities.get(0)][startCities.get(0)] + distances[restCities.get(0)][startCities.get(startCities.size()-1)] < minDistance))){
                    startCities.add(restCities.get(0));
                    newBestDistance(startCities, distSoFar + distances[restCities.get(0)][startCities.get(0)] + distances[restCities.get(0)][startCities.get(startCities.size()-2)]);
                    startCities.remove(startCities.size()-1);
                }
                else{
                    for (int i=0; i<restCities.size(); i++){
                        startCities.add(restCities.get(0));
                        restCities.remove(0);
                        permutation(startCities, distSoFar + distances[startCities.get(startCities.size()-1)][startCities.get(startCities.size()-2)],restCities);
                        restCities.add(startCities.get(startCities.size()-1));
                        startCities.remove(startCities.size()-1);
                    }
                }
            }
            catch (Exception e)
            {
                throw e;
            }
        }

        private static void newBestDistance(List<Integer> cities, double distance) throws ServiceException, Exception {
            try
            {
                minDistance = distance;
                String cityList = "Shortest distance is "+minDistance+", with route: ";
                for (int i = 0; i<bestOrder.length; i++){
                    bestOrder[i] = cities.get(i);
                    cityList += cityNames[bestOrder[i]];
                    if (i != bestOrder.length -1)
                        cityList += ", ";
                }
                System.out.println(cityList);
                service.sendQueueMessage("TSPQueue", new BrokeredMessage(cityList));
            }
            catch (ServiceException se)
            {
                throw se;
            }
            catch (Exception e)
            {
                throw e;
            }
        }

        public static void main(String args[]){

            try {

                Configuration config = ServiceBusConfiguration.configureWithWrapAuthentication(
                        "your_service_bus_namespace", "your_service_bus_owner",
                        "your_service_bus_key",
                        ".servicebus.windows.net",
                        "-sb.accesscontrol.windows.net/WRAPv0.9");

                service = ServiceBusService.create(config);

                int numCities = 10;  // Use as the default, if no value is specified at command line.
                if (args.length != 0)
                {
                    if (args[0].toLowerCase().compareTo("createqueue")==0)
                    {
                        // No processing to occur other than creating the queue.
                        QueueInfo queueInfo = new QueueInfo("TSPQueue");

                        service.createQueue(queueInfo);

                        System.out.println("Queue named TSPQueue was created.");

                        System.exit(0);
                    }

                    if (args[0].toLowerCase().compareTo("deletequeue")==0)
                    {
                        // No processing to occur other than deleting the queue.
                        service.deleteQueue("TSPQueue");

                        System.out.println("Queue named TSPQueue was deleted.");

                        System.exit(0);
                    }

                    // Neither creating or deleting a queue.
                    // Assume the value passed in is the number of cities to solve.
                    numCities = Integer.valueOf(args[0]);  
                }

                System.out.println("Running for " + numCities + " cities.");

                List<Integer> startCities = new ArrayList<Integer>();
                List<Integer> restCities = new ArrayList<Integer>();
                startCities.add(0);
                for(int i = 1; i<numCities; i++)
                    restCities.add(i);
                distances = new double[numCities][numCities];
                cityNames = new String[numCities];
                buildDistances("c:\\TSP\\cities.txt", numCities);
                minDistance = -1;
                bestOrder = new int[numCities];
                permutation(startCities, 0, restCities);
                System.out.println("Final solution found!");
                service.sendQueueMessage("TSPQueue", new BrokeredMessage("Complete"));
            }
            catch (ServiceException se)
            {
                System.out.println(se.getMessage());
                se.printStackTrace();
                System.exit(-1);
            }
            catch (Exception e)
            {
                System.out.println(e.getMessage());
                e.printStackTrace();
                System.exit(-1);
            }
        }

    }



## <a name="how-to-create-a-java-application-that-monitors-the-progress-of-the-compute-intensive-task"></a><span data-ttu-id="47d9e-193">Como criar um aplicativo Java que monitora o andamento da tarefa de computação intensiva</span><span class="sxs-lookup"><span data-stu-id="47d9e-193">How to create a Java application that monitors the progress of the compute-intensive task</span></span>
1. <span data-ttu-id="47d9e-194">Na sua máquina de desenvolvimento, crie um aplicativo de console Java usando o código de exemplo no final desta seção.</span><span class="sxs-lookup"><span data-stu-id="47d9e-194">On your development machine, create a Java console application using the example code at the end of this section.</span></span> <span data-ttu-id="47d9e-195">Neste tutorial, usaremos **TSPClient.java** como o nome do arquivo Java.</span><span class="sxs-lookup"><span data-stu-id="47d9e-195">In this tutorial, we'll use **TSPClient.java** as the Java file name.</span></span> <span data-ttu-id="47d9e-196">Conforme mostrado anteriormente, modifique os espaços reservados **your\_service\_bus\_namespace**, **your\_service\_bus\_owner** e **your\_service\_bus\_key** para usar o **namespace** do barramento de serviço e os valores **Emissor Padrão** e **Chave Padrão**, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="47d9e-196">As shown earlier, modify the **your\_service\_bus\_namespace**, **your\_service\_bus\_owner**, and **your\_service\_bus\_key** placeholders to use your service bus **namespace**, **Default Issuer** and **Default Key** values, respectively.</span></span>
2. <span data-ttu-id="47d9e-197">Exporte o aplicativo para um JAR executável e empacote as bibliotecas necessárias para o JAR gerado.</span><span class="sxs-lookup"><span data-stu-id="47d9e-197">Export the application to a runnable JAR, and package the required libraries into the generated JAR.</span></span> <span data-ttu-id="47d9e-198">Neste tutorial, usaremos **TSPClient.jar** como o nome do arquivo JAR gerado.</span><span class="sxs-lookup"><span data-stu-id="47d9e-198">In this tutorial, we'll use **TSPClient.jar** as the generated JAR name.</span></span>

<p/>

    // TSPClient.java

    import java.util.Date;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import com.microsoft.windowsazure.services.serviceBus.*;
    import com.microsoft.windowsazure.services.serviceBus.models.*;
    import com.microsoft.windowsazure.services.core.*;

    public class TSPClient
    {

        public static void main(String[] args)
        {
                try
                {

                    DateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");
                    Date date = new Date();
                    System.out.println("Starting at " + dateFormat.format(date) + ".");

                    String namespace = "your_service_bus_namespace";
                    String issuer = "your_service_bus_owner";
                    String key = "your_service_bus_key";

                    Configuration config;
                    config = ServiceBusConfiguration.configureWithWrapAuthentication(
                            namespace, issuer, key,
                            ".servicebus.windows.net",
                            "-sb.accesscontrol.windows.net/WRAPv0.9");

                    ServiceBusContract service = ServiceBusService.create(config);

                    BrokeredMessage message;

                    int waitMinutes = 3;  // Use as the default, if no value is specified at command line.
                    if (args.length != 0)
                    {
                        waitMinutes = Integer.valueOf(args[0]);  
                    }

                    String waitString;

                    waitString = (waitMinutes == 1) ? "minute." : waitMinutes + " minutes.";

                    // This queue must have previously been created.
                    service.getQueue("TSPQueue");

                    int numRead;

                    String s = null;

                    while (true)
                    {

                        ReceiveQueueMessageResult resultQM = service.receiveQueueMessage("TSPQueue");
                        message = resultQM.getValue();

                        if (null != message && null != message.getMessageId())
                        {

                            // Display the queue message.
                            byte[] b = new byte[200];

                            System.out.print("From queue: ");

                            s = null;
                            numRead = message.getBody().read(b);
                            while (-1 != numRead)
                            {
                                s = new String(b);
                                s = s.trim();
                                System.out.print(s);
                                numRead = message.getBody().read(b);
                            }
                            System.out.println();
                            if (s.compareTo("Complete") == 0)
                            {
                                // No more processing to occur.
                                date = new Date();
                                System.out.println("Finished at " + dateFormat.format(date) + ".");
                                break;
                            }
                        }
                        else
                        {
                            // The queue is empty.
                            System.out.println("Queue is empty. Sleeping for another " + waitString);
                            Thread.sleep(60000 * waitMinutes);
                        }
                    }

            }
            catch (ServiceException se)
            {
                System.out.println(se.getMessage());
                se.printStackTrace();
                System.exit(-1);
            }
            catch (Exception e)
            {
                System.out.println(e.getMessage());
                e.printStackTrace();
                System.exit(-1);
            }

        }

    }

## <a name="how-to-run-the-java-applications"></a><span data-ttu-id="47d9e-199">Como executar os aplicativos Java.</span><span class="sxs-lookup"><span data-stu-id="47d9e-199">How to run the Java applications</span></span>
<span data-ttu-id="47d9e-200">Execute o aplicativo que exija muita computação, primeiro para criar a fila, depois para solucionar o Problema do Caixeiro Viajante, que adicionará a melhor rota atual para a fila do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="47d9e-200">Run the compute-intensive application, first to create the queue, then to solve the Traveling Saleseman Problem, which will add the current best route to the service bus queue.</span></span> <span data-ttu-id="47d9e-201">Enquanto o aplicativo que exige muita computação está em execução (ou depois), execute o cliente para exibir os resultados da fila do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="47d9e-201">While the compute-intensive application is running (or afterwards), run the client to display results from the service bus queue.</span></span>

### <a name="to-run-the-compute-intensive-application"></a><span data-ttu-id="47d9e-202">Executar o aplicativo exige computação intensiva</span><span class="sxs-lookup"><span data-stu-id="47d9e-202">To run the compute-intensive application</span></span>
1. <span data-ttu-id="47d9e-203">Faça logon na máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="47d9e-203">Log on to your virtual machine.</span></span>
2. <span data-ttu-id="47d9e-204">Crie uma pasta onde você executará seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="47d9e-204">Create a folder where you will run your application.</span></span> <span data-ttu-id="47d9e-205">Por exemplo, **c:\TSP**.</span><span class="sxs-lookup"><span data-stu-id="47d9e-205">For example, **c:\TSP**.</span></span>
3. <span data-ttu-id="47d9e-206">Copie **TSPSolver.jar** para **c:\TSP**,</span><span class="sxs-lookup"><span data-stu-id="47d9e-206">Copy **TSPSolver.jar** to **c:\TSP**,</span></span>
4. <span data-ttu-id="47d9e-207">Crie um arquivo chamado **c:\TSP\cities.txt** com o conteúdo abaixo.</span><span class="sxs-lookup"><span data-stu-id="47d9e-207">Create a file named **c:\TSP\cities.txt** with the following contents.</span></span>
   
        City_1, 1002.81, -1841.35
        City_2, -953.55, -229.6
        City_3, -1363.11, -1027.72
        City_4, -1884.47, -1616.16
        City_5, 1603.08, -1030.03
        City_6, -1555.58, 218.58
        City_7, 578.8, -12.87
        City_8, 1350.76, 77.79
        City_9, 293.36, -1820.01
        City_10, 1883.14, 1637.28
        City_11, -1271.41, -1670.5
        City_12, 1475.99, 225.35
        City_13, 1250.78, 379.98
        City_14, 1305.77, 569.75
        City_15, 230.77, 231.58
        City_16, -822.63, -544.68
        City_17, -817.54, -81.92
        City_18, 303.99, -1823.43
        City_19, 239.95, 1007.91
        City_20, -1302.92, 150.39
        City_21, -116.11, 1933.01
        City_22, 382.64, 835.09
        City_23, -580.28, 1040.04
        City_24, 205.55, -264.23
        City_25, -238.81, -576.48
        City_26, -1722.9, -909.65
        City_27, 445.22, 1427.28
        City_28, 513.17, 1828.72
        City_29, 1750.68, -1668.1
        City_30, 1705.09, -309.35
        City_31, -167.34, 1003.76
        City_32, -1162.85, -1674.33
        City_33, 1490.32, 821.04
        City_34, 1208.32, 1523.3
        City_35, 18.04, 1857.11
        City_36, 1852.46, 1647.75
        City_37, -167.44, -336.39
        City_38, 115.4, 0.2
        City_39, -66.96, 917.73
        City_40, 915.96, 474.1
        City_41, 140.03, 725.22
        City_42, -1582.68, 1608.88
        City_43, -567.51, 1253.83
        City_44, 1956.36, 830.92
        City_45, -233.38, 909.93
        City_46, -1750.45, 1940.76
        City_47, 405.81, 421.84
        City_48, 363.68, 768.21
        City_49, -120.3, -463.13
        City_50, 588.51, 679.33
5. <span data-ttu-id="47d9e-208">Em um prompt de comando, altere os diretórios para c:\TSP.</span><span class="sxs-lookup"><span data-stu-id="47d9e-208">At a command prompt, change directories to c:\TSP.</span></span>
6. <span data-ttu-id="47d9e-209">Certifique-se de que a pasta da lixeira do JRE está na variável de ambiente PATH.</span><span class="sxs-lookup"><span data-stu-id="47d9e-209">Ensure the JRE's bin folder is in the PATH environment variable.</span></span>
7. <span data-ttu-id="47d9e-210">Você precisará criar a fila do barramento de serviço antes de executar as permutas de solver TSP.</span><span class="sxs-lookup"><span data-stu-id="47d9e-210">You'll need to create the service bus queue before you run the TSP solver permutations.</span></span> <span data-ttu-id="47d9e-211">Execute o seguinte comando para criar a fila do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="47d9e-211">Run the following command to create the service bus queue.</span></span>
   
        java -jar TSPSolver.jar createqueue
8. <span data-ttu-id="47d9e-212">Agora que a fila está criada, você pode executar as permutas de solver TSP.</span><span class="sxs-lookup"><span data-stu-id="47d9e-212">Now that the queue is created, you can run the TSP solver permutations.</span></span> <span data-ttu-id="47d9e-213">Por exemplo, execute o seguinte comando para executar o solver para 8 cidades.</span><span class="sxs-lookup"><span data-stu-id="47d9e-213">For example, run the following command to run the solver for 8 cities.</span></span>
   
        java -jar TSPSolver.jar 8
   
   <span data-ttu-id="47d9e-214">Se você não especificar um número, ele será executado para 10 cidades.</span><span class="sxs-lookup"><span data-stu-id="47d9e-214">If you don't specify a number, it will run for 10 cities.</span></span> <span data-ttu-id="47d9e-215">Como localiza rotas atuais mais curtas, o solver as adicionará à fila.</span><span class="sxs-lookup"><span data-stu-id="47d9e-215">As the solver finds current shortest routes, it will add them to the queue.</span></span>

> [!NOTE]
> <span data-ttu-id="47d9e-216">Quanto maior o número que você especificar, por mais tempo o solver será executado.</span><span class="sxs-lookup"><span data-stu-id="47d9e-216">The larger the number that you specify, the longer the solver will run.</span></span> <span data-ttu-id="47d9e-217">Por exemplo, a execução de 14 cidades pode levar vários minutos, e a execução de 15 cidades pode levar várias horas.</span><span class="sxs-lookup"><span data-stu-id="47d9e-217">For example, running for 14 cities could take several minutes, and running for 15 cities could take several hours.</span></span> <span data-ttu-id="47d9e-218">Aumentar para 16 ou mais cidades pode resultar em dias de tempo de execução (acabando em semanas, meses e anos).</span><span class="sxs-lookup"><span data-stu-id="47d9e-218">Increasing to 16 or more cities could result in days of runtime (eventually weeks, months, and years).</span></span> <span data-ttu-id="47d9e-219">Isso ocorre porque o rápido aumento do número de permutas avaliadas pelo solver, como o número de cidades, aumenta.</span><span class="sxs-lookup"><span data-stu-id="47d9e-219">This is due to the rapid increase in the number of permutations evaluated by the solver as the number of cities increases.</span></span>
> 
> 

### <a name="how-to-run-the-monitoring-client-application"></a><span data-ttu-id="47d9e-220">Como executar o aplicativo cliente de monitoramento</span><span class="sxs-lookup"><span data-stu-id="47d9e-220">How to run the monitoring client application</span></span>
1. <span data-ttu-id="47d9e-221">Faça logon no computador onde você executará o aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="47d9e-221">Log on to your machine where you will run the client application.</span></span> <span data-ttu-id="47d9e-222">Ele não precisa estar na mesma máquina executando o aplicativo **TSPSolver** , embora possa ser.</span><span class="sxs-lookup"><span data-stu-id="47d9e-222">This does not need to be the same machine running the **TSPSolver** application, although it can be.</span></span>
2. <span data-ttu-id="47d9e-223">Crie uma pasta onde você executará seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="47d9e-223">Create a folder where you will run your application.</span></span> <span data-ttu-id="47d9e-224">Por exemplo, **c:\TSP**.</span><span class="sxs-lookup"><span data-stu-id="47d9e-224">For example, **c:\TSP**.</span></span>
3. <span data-ttu-id="47d9e-225">Copie **TSPClient.jar** para **c:\TSP**,</span><span class="sxs-lookup"><span data-stu-id="47d9e-225">Copy **TSPClient.jar** to **c:\TSP**,</span></span>
4. <span data-ttu-id="47d9e-226">Certifique-se de que a pasta da lixeira do JRE está na variável de ambiente PATH.</span><span class="sxs-lookup"><span data-stu-id="47d9e-226">Ensure the JRE's bin folder is in the PATH environment variable.</span></span>
5. <span data-ttu-id="47d9e-227">Em um prompt de comando, altere os diretórios para c:\TSP.</span><span class="sxs-lookup"><span data-stu-id="47d9e-227">At a command prompt, change directories to c:\TSP.</span></span>
6. <span data-ttu-id="47d9e-228">Execute o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="47d9e-228">Run the following command.</span></span>
   
        java -jar TSPClient.jar
   
    <span data-ttu-id="47d9e-229">Como opção, especifique o número de minutos de suspensão entre a verificação da fila passando um argumento de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="47d9e-229">Optionally, specify the number of minutes to sleep in between checking the queue, by passing in a command-line argument.</span></span> <span data-ttu-id="47d9e-230">O período de suspensão padrão para a verificação da fila é de 3 minutos, que será usado se nenhum argumento de linha de comando for transmitido para **TSPClient**.</span><span class="sxs-lookup"><span data-stu-id="47d9e-230">The default sleep period for checking the queue is 3 minutes, which is used if no command-line argument is passed to **TSPClient**.</span></span> <span data-ttu-id="47d9e-231">Se você quiser usar um valor diferente para o intervalo de suspensão, como um minuto, por exemplo, execute o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="47d9e-231">If you want to use a different value for the sleep interval, for example, one minute, run the following command.</span></span>
   
        java -jar TSPClient.jar 1
   
    <span data-ttu-id="47d9e-232">O cliente será executado até ver a mensagem de uma fila "Concluído".</span><span class="sxs-lookup"><span data-stu-id="47d9e-232">The client will run until it sees a queue message of "Complete".</span></span> <span data-ttu-id="47d9e-233">Observe que, se executar várias ocorrências do solver sem executar o cliente, você precisará executar o cliente várias vezes para esvaziar completamente a fila.</span><span class="sxs-lookup"><span data-stu-id="47d9e-233">Note that if you run multiple occurrences of the solver without running the client, you may need to run the client multiple times to completely empty the queue.</span></span> <span data-ttu-id="47d9e-234">Também é possível excluir a fila e depois criá-la novamente.</span><span class="sxs-lookup"><span data-stu-id="47d9e-234">Alternatively, you can delete the queue and then create it again.</span></span> <span data-ttu-id="47d9e-235">Para excluir a fila, execute o comando do **TSPSolver** (não **TSPClient**) a seguir.</span><span class="sxs-lookup"><span data-stu-id="47d9e-235">To delete the queue, run the following **TSPSolver** (not **TSPClient**)  command.</span></span>
   
        java -jar TSPSolver.jar deletequeue
   
    <span data-ttu-id="47d9e-236">O solver será executado até terminar de examinar todas as rotas.</span><span class="sxs-lookup"><span data-stu-id="47d9e-236">The solver will run until it finishes examining all routes.</span></span>

## <a name="how-to-stop-the-java-applications"></a><span data-ttu-id="47d9e-237">Como parar os aplicativos Java.</span><span class="sxs-lookup"><span data-stu-id="47d9e-237">How to stop the Java applications</span></span>
<span data-ttu-id="47d9e-238">Para os aplicativos solver e de cliente, é possível pressionar **Ctrl+C** para sair se você quiser encerrar antes da conclusão normal.</span><span class="sxs-lookup"><span data-stu-id="47d9e-238">For both the solver and client applications, you can press **Ctrl+C** to exit if you want to end prior to normal completion.</span></span>

[solver_output]:media/java-run-compute-intensive-task/WA_JavaTSPSolver.png
[client_output]:media/java-run-compute-intensive-task/WA_JavaTSPClient.png
[svc_bus_node]:media/java-run-compute-intensive-task/SvcBusQueues_02_SvcBusNode.jpg
[create_namespace]:media/java-run-compute-intensive-task/SvcBusQueues_03_CreateNewSvcNamespace.jpg
[avail_namespaces]:media/java-run-compute-intensive-task/SvcBusQueues_04_SvcBusNode_AvailNamespaces.jpg
[namespace_list]:media/java-run-compute-intensive-task/SvcBusQueues_05_NamespaceList.jpg
[properties_pane]:media/java-run-compute-intensive-task/SvcBusQueues_06_PropertiesPane.jpg
[default_key]:media/java-run-compute-intensive-task/SvcBusQueues_07_DefaultKey.jpg
[add_ca_cert]: ../../../java-add-certificate-ca-store.md
