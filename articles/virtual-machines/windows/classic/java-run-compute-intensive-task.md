---
title: "aplicativo em uma máquina virtual Java que utiliza a aaaCompute | Microsoft Docs"
description: "Saiba como toocreate uma máquina virtual do Azure que executa um aplicativo de Java com computação intensiva que pode ser monitorado por outro aplicativo de Java."
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
ms.openlocfilehash: 02a198802a8d78bd444cd5a9197a78cb94f48e3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-compute-intensive-task-in-java-on-a-virtual-machine"></a><span data-ttu-id="c337e-103">Como toorun uma computação intensa de tarefas em Java em uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="c337e-103">How toorun a compute-intensive task in Java on a virtual machine</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="c337e-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c337e-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="c337e-105">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="c337e-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="c337e-106">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="c337e-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="c337e-107">Com o Azure, você pode usar tarefas de computação intensa de toohandle uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c337e-107">With Azure, you can use a virtual machine toohandle compute-intensive tasks.</span></span> <span data-ttu-id="c337e-108">Por exemplo, uma máquina virtual pode lidar com tarefas e fornecer máquinas de tooclient resultados ou aplicativos móveis.</span><span class="sxs-lookup"><span data-stu-id="c337e-108">For example, a virtual machine can handle tasks and deliver results tooclient machines or mobile applications.</span></span> <span data-ttu-id="c337e-109">Depois de ler este artigo, você terá uma compreensão de como toocreate uma máquina virtual que executa um aplicativo de Java com computação intensiva que pode ser monitorado por outro aplicativo de Java.</span><span class="sxs-lookup"><span data-stu-id="c337e-109">After reading this article, you will have an understanding of how toocreate a virtual machine that runs a compute-intensive Java application that can be monitored by another Java application.</span></span>

<span data-ttu-id="c337e-110">Este tutorial presume que você sabe como aplicativos de console de Java toocreate, pode importar um aplicativo de Java tooyour bibliotecas e pode gerar um JAR (Java archive).</span><span class="sxs-lookup"><span data-stu-id="c337e-110">This tutorial assumes you know how toocreate Java console applications, can import libraries tooyour Java application, and can generate a Java archive (JAR).</span></span> <span data-ttu-id="c337e-111">Nenhum conhecimento do Microsoft Azure é assumido.</span><span class="sxs-lookup"><span data-stu-id="c337e-111">No knowledge of Microsoft Azure is assumed.</span></span>

<span data-ttu-id="c337e-112">Você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="c337e-112">You will learn:</span></span>

* <span data-ttu-id="c337e-113">Como toocreate uma máquina virtual com um Java Development Kit (JDK) já instalado.</span><span class="sxs-lookup"><span data-stu-id="c337e-113">How toocreate a virtual machine with a Java Development Kit (JDK) already installed.</span></span>
* <span data-ttu-id="c337e-114">Como tooremotely fazem logon na máquina virtual de tooyour.</span><span class="sxs-lookup"><span data-stu-id="c337e-114">How tooremotely log in tooyour virtual machine.</span></span>
* <span data-ttu-id="c337e-115">Como toocreate um serviço de barramento de namespace.</span><span class="sxs-lookup"><span data-stu-id="c337e-115">How toocreate a service bus namespace.</span></span>
* <span data-ttu-id="c337e-116">Como toocreate um aplicativo Java que executa uma tarefa de computação intensa.</span><span class="sxs-lookup"><span data-stu-id="c337e-116">How toocreate a Java application that performs a compute-intensive task.</span></span>
* <span data-ttu-id="c337e-117">Como toocreate um aplicativo Java que monitora Olá progresso da tarefa de computação intensiva hello.</span><span class="sxs-lookup"><span data-stu-id="c337e-117">How toocreate a Java application that monitors hello progress of hello compute-intensive task.</span></span>
* <span data-ttu-id="c337e-118">Como toorun Olá aplicativos Java.</span><span class="sxs-lookup"><span data-stu-id="c337e-118">How toorun hello Java applications.</span></span>
* <span data-ttu-id="c337e-119">Como toostop Olá aplicativos Java.</span><span class="sxs-lookup"><span data-stu-id="c337e-119">How toostop hello Java applications.</span></span>

<span data-ttu-id="c337e-120">Este tutorial usará Olá problema do Caixeiro Viajante para tarefas de computação intensa hello.</span><span class="sxs-lookup"><span data-stu-id="c337e-120">This tutorial will use hello Traveling Salesman Problem for hello compute-intensive task.</span></span> <span data-ttu-id="c337e-121">a seguir Olá é um exemplo de tarefa de computação intensa do hello Java aplicativo em execução hello.</span><span class="sxs-lookup"><span data-stu-id="c337e-121">hello following is an example of hello Java application running hello compute-intensive task.</span></span>

![Solucionador de problemas do Caixeiro Viajante][solver_output]

<span data-ttu-id="c337e-123">a seguir Olá é um exemplo de hello Java aplicativo hello com computação intensiva a tarefa de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="c337e-123">hello following is an example of hello Java application monitoring hello compute-intensive task.</span></span>

![Cliente de problemas do Caixeiro Viajante][client_output]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="toocreate-a-virtual-machine"></a><span data-ttu-id="c337e-125">toocreate uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="c337e-125">toocreate a virtual machine</span></span>
1. <span data-ttu-id="c337e-126">Faça logon no toohello [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="c337e-126">Log in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="c337e-127">Clique em **Nova**, clique em **Computação**, clique em **Máquina virtual** e, em seguida, clique em **Da Galeria**.</span><span class="sxs-lookup"><span data-stu-id="c337e-127">Click **New**, click **Compute**, click **Virtual machine**, and then click **From Gallery**.</span></span>
3. <span data-ttu-id="c337e-128">Em Olá **select de imagem de máquina Virtual** caixa de diálogo, selecione **JDK 7 Windows Server 2012**.</span><span class="sxs-lookup"><span data-stu-id="c337e-128">In hello **Virtual machine image select** dialog box, select **JDK 7 Windows Server 2012**.</span></span>
   <span data-ttu-id="c337e-129">Observe que **JDK 6 Windows Server 2012** está disponível caso você tenha aplicativos herdados que ainda não estão pronto toorun JDK 7.</span><span class="sxs-lookup"><span data-stu-id="c337e-129">Note that **JDK 6 Windows Server 2012** is available in case you have legacy applications that are not yet ready toorun in JDK 7.</span></span>
4. <span data-ttu-id="c337e-130">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="c337e-130">Click **Next**.</span></span>
5. <span data-ttu-id="c337e-131">Em Olá **configuração de máquina Virtual** caixa de diálogo:</span><span class="sxs-lookup"><span data-stu-id="c337e-131">In hello **Virtual machine configuration** dialog box:</span></span>
   1. <span data-ttu-id="c337e-132">Especifique um nome para a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="c337e-132">Specify a name for hello virtual machine.</span></span>
   2. <span data-ttu-id="c337e-133">Especifique Olá toouse de tamanho da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="c337e-133">Specify hello size toouse for hello virtual machine.</span></span>
   3. <span data-ttu-id="c337e-134">Insira um nome para o administrador de saudação em Olá **nome de usuário** campo.</span><span class="sxs-lookup"><span data-stu-id="c337e-134">Enter a name for hello administrator in hello **User Name** field.</span></span> <span data-ttu-id="c337e-135">Guarde essa senha de nome e hello que entrará em seguida, você usará-los quando você fazer logon remotamente na máquina virtual de toohello.</span><span class="sxs-lookup"><span data-stu-id="c337e-135">Remember this name and hello password you will enter next, you will use them when you remotely log in toohello virtual machine.</span></span>
   4. <span data-ttu-id="c337e-136">Digite uma senha na Olá **nova senha** campo e insira-a novamente no hello **confirmar** campo.</span><span class="sxs-lookup"><span data-stu-id="c337e-136">Enter a password in hello **New password** field, and re-enter it in hello **Confirm** field.</span></span> <span data-ttu-id="c337e-137">Isso é a senha da conta de administrador hello.</span><span class="sxs-lookup"><span data-stu-id="c337e-137">This is hello Administrator account password.</span></span>
   5. <span data-ttu-id="c337e-138">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="c337e-138">Click **Next**.</span></span>
6. <span data-ttu-id="c337e-139">Em Olá próximo **configuração de máquina Virtual** caixa de diálogo:</span><span class="sxs-lookup"><span data-stu-id="c337e-139">In hello next **Virtual machine configuration** dialog box:</span></span>
   1. <span data-ttu-id="c337e-140">Para **serviço de nuvem**, use o padrão de saudação **criar um novo serviço de nuvem**.</span><span class="sxs-lookup"><span data-stu-id="c337e-140">For **Cloud service**, use hello default **Create a new cloud service**.</span></span>
   2. <span data-ttu-id="c337e-141">Olá valor **nome DNS do serviço de nuvem** devem ser exclusivas em c.</span><span class="sxs-lookup"><span data-stu-id="c337e-141">hello value for **Cloud service DNS name** must be unique across cloudapp.net.</span></span> <span data-ttu-id="c337e-142">Se necessário, modifique esse valor para que o Azure indique que ele é exclusivo.</span><span class="sxs-lookup"><span data-stu-id="c337e-142">If needed, modify this value so that Azure indicates it is unique.</span></span>
   3. <span data-ttu-id="c337e-143">Especifique uma região, um grupo de afinidade ou uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="c337e-143">Specify a region, affinity group, or virtual network.</span></span> <span data-ttu-id="c337e-144">Para o objetivo deste tutorial, especifique uma região, como **Oeste dos Estados Unidos**.</span><span class="sxs-lookup"><span data-stu-id="c337e-144">For purposes of this tutorial, specify a region such as **West US**.</span></span>
   4. <span data-ttu-id="c337e-145">Para **Conta de Armazenamento**, selecione **Usar uma conta de armazenamento gerada automaticamente**.</span><span class="sxs-lookup"><span data-stu-id="c337e-145">For **Storage Account**, select **Use an automatically generated storage account**.</span></span>
   5. <span data-ttu-id="c337e-146">Para **Conjunto de Disponibilidade**, selecione **(Nenhum)**.</span><span class="sxs-lookup"><span data-stu-id="c337e-146">For **Availability Set**, select **(None)**.</span></span>
   6. <span data-ttu-id="c337e-147">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="c337e-147">Click **Next**.</span></span>
7. <span data-ttu-id="c337e-148">No final da saudação **configuração de máquina Virtual** caixa de diálogo:</span><span class="sxs-lookup"><span data-stu-id="c337e-148">In hello final **Virtual machine configuration** dialog box:</span></span>
   1. <span data-ttu-id="c337e-149">Aceite entradas de ponto de extremidade padrão hello.</span><span class="sxs-lookup"><span data-stu-id="c337e-149">Accept hello default endpoint entries.</span></span>
   2. <span data-ttu-id="c337e-150">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="c337e-150">Click **Complete**.</span></span>

## <a name="tooremotely-log-in-tooyour-virtual-machine"></a><span data-ttu-id="c337e-151">log tooremotely na máquina virtual de tooyour</span><span class="sxs-lookup"><span data-stu-id="c337e-151">tooremotely log in tooyour virtual machine</span></span>
1. <span data-ttu-id="c337e-152">Faça logon no toohello [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="c337e-152">Log on toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="c337e-153">Clique em **Máquinas Virtuais**.</span><span class="sxs-lookup"><span data-stu-id="c337e-153">Click **Virtual machines**.</span></span>
3. <span data-ttu-id="c337e-154">Clique Olá nome da máquina virtual Olá que você deseja toolog no.</span><span class="sxs-lookup"><span data-stu-id="c337e-154">Click hello name of hello virtual machine that you want toolog in to.</span></span>
4. <span data-ttu-id="c337e-155">Clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="c337e-155">Click **Connect**.</span></span>
5. <span data-ttu-id="c337e-156">Responda toohello prompts como máquina de virtual toohello tooconnect necessários.</span><span class="sxs-lookup"><span data-stu-id="c337e-156">Respond toohello prompts as needed tooconnect toohello virtual machine.</span></span> <span data-ttu-id="c337e-157">Quando solicitado para Olá administrador nome e senha, use valores hello fornecida quando você criou a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="c337e-157">When prompted for hello administrator name and password, use hello values that you provided when you created hello virtual machine.</span></span>

<span data-ttu-id="c337e-158">Observe que Olá funcionalidade do barramento de serviço do Azure requer Olá Baltimore CyberTrust Root certificado toobe instalado como parte do seu JRE **cacerts** armazenar.</span><span class="sxs-lookup"><span data-stu-id="c337e-158">Note that hello Azure Service Bus functionality requires hello Baltimore CyberTrust Root certificate toobe installed as part of your JRE's **cacerts** store.</span></span> <span data-ttu-id="c337e-159">Esse certificado é incluído automaticamente em Olá Java Runtime Environment (JRE) usado por este tutorial.</span><span class="sxs-lookup"><span data-stu-id="c337e-159">This certificate is automatically included in hello Java Runtime Environment (JRE) used by this tutorial.</span></span> <span data-ttu-id="c337e-160">Se você não tem esse certificado em seu JRE **cacerts** de armazenamento, consulte [adicionando um toohello certificado repositório de certificados de autoridade de certificação de Java] [ add_ca_cert] para obter informações sobre como adicioná-lo (bem como informações sobre como visualizar certificados Olá em seu repositório cacerts).</span><span class="sxs-lookup"><span data-stu-id="c337e-160">If you do not have this certificate in your JRE **cacerts** store, see [Adding a Certificate toohello Java CA Certificate Store][add_ca_cert] for information on adding it (as well as information on viewing hello certificates in your cacerts store).</span></span>

## <a name="how-toocreate-a-service-bus-namespace"></a><span data-ttu-id="c337e-161">Como o namespace de barramento toocreate um serviço</span><span class="sxs-lookup"><span data-stu-id="c337e-161">How toocreate a service bus namespace</span></span>
<span data-ttu-id="c337e-162">filas de toobegin usando o barramento de serviço no Azure, você deve primeiro criar um namespace de serviço.</span><span class="sxs-lookup"><span data-stu-id="c337e-162">toobegin using Service Bus queues in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="c337e-163">Um namespace de serviço fornece um contêiner de controle para endereçamento dos recursos do Barramento de Serviço em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c337e-163">A service namespace provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="c337e-164">toocreate um namespace de serviço:</span><span class="sxs-lookup"><span data-stu-id="c337e-164">toocreate a service namespace:</span></span>

1. <span data-ttu-id="c337e-165">Faça logon no toohello [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="c337e-165">Log on toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="c337e-166">No painel de navegação inferior esquerda Olá de saudação portal clássico do Azure, clique **barramento de serviço, controle de acesso e cache**.</span><span class="sxs-lookup"><span data-stu-id="c337e-166">In hello lower-left navigation pane of hello Azure classic portal, click **Service Bus, Access Control & Caching**.</span></span>
3. <span data-ttu-id="c337e-167">No painel superior esquerdo de saudação do hello portal clássico do Azure, clique em Olá **Service Bus** nó e, em seguida, clique em Olá **novo** botão.</span><span class="sxs-lookup"><span data-stu-id="c337e-167">In hello upper-left pane of hello Azure classic portal, click hello **Service Bus** node, and then click hello **New** button.</span></span>  
   <span data-ttu-id="c337e-168">![Captura de tela do nó do Service Bus][svc_bus_node]</span><span class="sxs-lookup"><span data-stu-id="c337e-168">![Service Bus Node screenshot][svc_bus_node]</span></span>
4. <span data-ttu-id="c337e-169">Em Olá **criar um novo Namespace de serviço** caixa de diálogo, digite um **Namespace**, e, em seguida, clique em toomake-se de que ele seja exclusivo, o **Verificar disponibilidade** botão.</span><span class="sxs-lookup"><span data-stu-id="c337e-169">In hello **Create a new Service Namespace** dialog box, enter a **Namespace**, and then toomake sure that it is unique, click the **Check Availability** button.</span></span>  
   <span data-ttu-id="c337e-170">![Criar uma captura de tela do novo Namespace][create_namespace]</span><span class="sxs-lookup"><span data-stu-id="c337e-170">![Create a New Namespace screenshot][create_namespace]</span></span>
5. <span data-ttu-id="c337e-171">Depois de verificar se o nome do namespace hello está disponível, escolha o país ou região em que o namespace deve ser hospedado e, em seguida, clique em Olá **criar Namespace** botão.</span><span class="sxs-lookup"><span data-stu-id="c337e-171">After making sure hello namespace name is available, choose the country or region in which your namespace should be hosted, and then click hello **Create Namespace** button.</span></span>  
   
   <span data-ttu-id="c337e-172">Olá namespace criado será exibida no portal clássico do Azure de saudação e entra em um momento tooactivate.</span><span class="sxs-lookup"><span data-stu-id="c337e-172">hello namespace you created will then appear in hello Azure classic portal and takes a moment tooactivate.</span></span> <span data-ttu-id="c337e-173">Aguarde até que o status de saudação **Active** antes de continuar com a próxima etapa de saudação.</span><span class="sxs-lookup"><span data-stu-id="c337e-173">Wait until hello status is **Active** before continuing with hello next step.</span></span>

## <a name="obtain-hello-default-management-credentials-for-hello-namespace"></a><span data-ttu-id="c337e-174">Obter Olá gerenciamento de credenciais padrão para o namespace de saudação</span><span class="sxs-lookup"><span data-stu-id="c337e-174">Obtain hello Default Management Credentials for hello namespace</span></span>
<span data-ttu-id="c337e-175">Em operações de gerenciamento de tooperform ordem, como a criação de uma fila, no novo namespace de hello, você precisa ter credenciais de gerenciamento de saudação do tooobtain para o namespace.</span><span class="sxs-lookup"><span data-stu-id="c337e-175">In order tooperform management operations, such as creating a queue, on hello new namespace, you need tooobtain hello management credentials for the namespace.</span></span>

1. <span data-ttu-id="c337e-176">No painel de navegação esquerdo hello, clique em Olá **Service Bus** nó para exibir a lista de saudação de namespaces disponíveis.</span><span class="sxs-lookup"><span data-stu-id="c337e-176">In hello left navigation pane, click hello **Service Bus** node to display hello list of available namespaces.</span></span>
   <span data-ttu-id="c337e-177">![Captura de tela de namespaces disponíveis][avail_namespaces]</span><span class="sxs-lookup"><span data-stu-id="c337e-177">![Available Namespaces screenshot][avail_namespaces]</span></span>
2. <span data-ttu-id="c337e-178">Selecione o namespace de saudação que você acabou de criar na lista Olá mostrada.</span><span class="sxs-lookup"><span data-stu-id="c337e-178">Select hello namespace you just created from hello list shown.</span></span>
   <span data-ttu-id="c337e-179">![Captura de tela da lista de namespaces][namespace_list]</span><span class="sxs-lookup"><span data-stu-id="c337e-179">![Namespace List screenshot][namespace_list]</span></span>
3. <span data-ttu-id="c337e-180">Olá direito **propriedades** painel lista as propriedades de saudação para o novo namespace.</span><span class="sxs-lookup"><span data-stu-id="c337e-180">hello right-hand **Properties** pane lists hello properties for the new namespace.</span></span>
   <span data-ttu-id="c337e-181">![Captura de tela do painel Propriedades][properties_pane]</span><span class="sxs-lookup"><span data-stu-id="c337e-181">![Properties Pane screenshot][properties_pane]</span></span>
4. <span data-ttu-id="c337e-182">Olá **chave padrão** está oculto.</span><span class="sxs-lookup"><span data-stu-id="c337e-182">hello **Default Key** is hidden.</span></span> <span data-ttu-id="c337e-183">Clique em Olá **exibição** botão credenciais de segurança toodisplay hello.</span><span class="sxs-lookup"><span data-stu-id="c337e-183">Click hello **View** button toodisplay hello security credentials.</span></span>
   <span data-ttu-id="c337e-184">![Captura de tela da chave padrão][default_key]</span><span class="sxs-lookup"><span data-stu-id="c337e-184">![Default Key screenshot][default_key]</span></span>
5. <span data-ttu-id="c337e-185">Anote Olá **emissor padrão** e hello **chave padrão** como você usará essas informações abaixo tooperform operações com o namespace.</span><span class="sxs-lookup"><span data-stu-id="c337e-185">Make a note of hello **Default Issuer** and hello **Default Key** as you will use this information below tooperform operations with the namespace.</span></span>

## <a name="how-toocreate-a-java-application-that-performs-a-compute-intensive-task"></a><span data-ttu-id="c337e-186">Como toocreate um aplicativo Java que executa uma tarefa de computação intensa</span><span class="sxs-lookup"><span data-stu-id="c337e-186">How toocreate a Java application that performs a compute-intensive task</span></span>
1. <span data-ttu-id="c337e-187">No computador de desenvolvimento (que não tem a máquina virtual do toobe Olá que você criou), download Olá [SDK do Azure para Java](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="c337e-187">On your development machine (which does not have toobe hello virtual machine that you created), download hello [Azure SDK for Java](https://azure.microsoft.com/develop/java/).</span></span>
2. <span data-ttu-id="c337e-188">Crie um aplicativo de console de Java usando o código de exemplo hello final Olá desta seção.</span><span class="sxs-lookup"><span data-stu-id="c337e-188">Create a Java console application using hello example code at hello end of this section.</span></span> <span data-ttu-id="c337e-189">Neste tutorial, vamos usar **TSPSolver.java** como nome de arquivo hello Java.</span><span class="sxs-lookup"><span data-stu-id="c337e-189">In this tutorial, we'll use **TSPSolver.java** as hello Java file name.</span></span> <span data-ttu-id="c337e-190">Modificar Olá **sua\_service\_barramento\_namespace**, **sua\_service\_barramento\_proprietário**e **seu\_service\_barramento\_chave** toouse de espaços reservados para o barramento de serviço **namespace**, **emissor padrão** e  **Chave padrão** valores, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="c337e-190">Modify hello **your\_service\_bus\_namespace**, **your\_service\_bus\_owner**, and **your\_service\_bus\_key** placeholders toouse your service bus **namespace**, **Default Issuer** and **Default Key** values, respectively.</span></span>
3. <span data-ttu-id="c337e-191">Depois de codificar, exportação Olá aplicativo tooa executável JAR (Java archive) e saudação de pacote necessários bibliotecas em Olá gerado JAR.</span><span class="sxs-lookup"><span data-stu-id="c337e-191">After coding, export hello application tooa runnable Java archive (JAR), and package hello required libraries into hello generated JAR.</span></span> <span data-ttu-id="c337e-192">Neste tutorial, vamos usar **TSPSolver.jar** como nome do JAR Olá gerado.</span><span class="sxs-lookup"><span data-stu-id="c337e-192">In this tutorial, we'll use **TSPSolver.jar** as hello generated JAR name.</span></span>

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

        //  Value specifying how often tooprovide an update toohello console.
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

                int numCities = 10;  // Use as hello default, if no value is specified at command line.
                if (args.length != 0)
                {
                    if (args[0].toLowerCase().compareTo("createqueue")==0)
                    {
                        // No processing toooccur other than creating hello queue.
                        QueueInfo queueInfo = new QueueInfo("TSPQueue");

                        service.createQueue(queueInfo);

                        System.out.println("Queue named TSPQueue was created.");

                        System.exit(0);
                    }

                    if (args[0].toLowerCase().compareTo("deletequeue")==0)
                    {
                        // No processing toooccur other than deleting hello queue.
                        service.deleteQueue("TSPQueue");

                        System.out.println("Queue named TSPQueue was deleted.");

                        System.exit(0);
                    }

                    // Neither creating or deleting a queue.
                    // Assume hello value passed in is hello number of cities toosolve.
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



## <a name="how-toocreate-a-java-application-that-monitors-hello-progress-of-hello-compute-intensive-task"></a><span data-ttu-id="c337e-193">Como toocreate um aplicativo Java que monitora Olá progresso da tarefa de computação intensiva Olá</span><span class="sxs-lookup"><span data-stu-id="c337e-193">How toocreate a Java application that monitors hello progress of hello compute-intensive task</span></span>
1. <span data-ttu-id="c337e-194">No computador de desenvolvimento, crie um aplicativo de console Java usando o código de exemplo hello final Olá desta seção.</span><span class="sxs-lookup"><span data-stu-id="c337e-194">On your development machine, create a Java console application using hello example code at hello end of this section.</span></span> <span data-ttu-id="c337e-195">Neste tutorial, vamos usar **TSPClient.java** como nome de arquivo hello Java.</span><span class="sxs-lookup"><span data-stu-id="c337e-195">In this tutorial, we'll use **TSPClient.java** as hello Java file name.</span></span> <span data-ttu-id="c337e-196">Como mostrado anteriormente, modificar Olá **sua\_serviço\_barramento\_namespace**, **sua\_service\_barramento\_proprietário**, e **seu\_service\_barramento\_chave** toouse de espaços reservados para o barramento de serviço **namespace**, **emissor padrão**e **chave padrão** valores, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="c337e-196">As shown earlier, modify hello **your\_service\_bus\_namespace**, **your\_service\_bus\_owner**, and **your\_service\_bus\_key** placeholders toouse your service bus **namespace**, **Default Issuer** and **Default Key** values, respectively.</span></span>
2. <span data-ttu-id="c337e-197">Exportar Olá aplicativo tooa executável JAR e saudação de pacote necessários bibliotecas em Olá gerado JAR.</span><span class="sxs-lookup"><span data-stu-id="c337e-197">Export hello application tooa runnable JAR, and package hello required libraries into hello generated JAR.</span></span> <span data-ttu-id="c337e-198">Neste tutorial, vamos usar **TSPClient.jar** como nome do JAR Olá gerado.</span><span class="sxs-lookup"><span data-stu-id="c337e-198">In this tutorial, we'll use **TSPClient.jar** as hello generated JAR name.</span></span>

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

                    int waitMinutes = 3;  // Use as hello default, if no value is specified at command line.
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

                            // Display hello queue message.
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
                                // No more processing toooccur.
                                date = new Date();
                                System.out.println("Finished at " + dateFormat.format(date) + ".");
                                break;
                            }
                        }
                        else
                        {
                            // hello queue is empty.
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

## <a name="how-toorun-hello-java-applications"></a><span data-ttu-id="c337e-199">Como toorun Olá aplicativos Java</span><span class="sxs-lookup"><span data-stu-id="c337e-199">How toorun hello Java applications</span></span>
<span data-ttu-id="c337e-200">Executar aplicativos de computação intensiva hello, primeira fila de saudação toocreate, em seguida, toosolve Olá problema Saleseman viajando, que adicionará Olá atual melhor rota toohello fila do service bus.</span><span class="sxs-lookup"><span data-stu-id="c337e-200">Run hello compute-intensive application, first toocreate hello queue, then toosolve hello Traveling Saleseman Problem, which will add hello current best route toohello service bus queue.</span></span> <span data-ttu-id="c337e-201">Durante a saudação aplicativos de computação intensiva está em execução (ou posteriormente), execução Olá cliente toodisplay resulta da fila do barramento de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="c337e-201">While hello compute-intensive application is running (or afterwards), run hello client toodisplay results from hello service bus queue.</span></span>

### <a name="toorun-hello-compute-intensive-application"></a><span data-ttu-id="c337e-202">aplicativos de computação intensiva Olá toorun</span><span class="sxs-lookup"><span data-stu-id="c337e-202">toorun hello compute-intensive application</span></span>
1. <span data-ttu-id="c337e-203">Faça logon na máquina virtual de tooyour.</span><span class="sxs-lookup"><span data-stu-id="c337e-203">Log on tooyour virtual machine.</span></span>
2. <span data-ttu-id="c337e-204">Crie uma pasta onde você executará seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c337e-204">Create a folder where you will run your application.</span></span> <span data-ttu-id="c337e-205">Por exemplo, **c:\TSP**.</span><span class="sxs-lookup"><span data-stu-id="c337e-205">For example, **c:\TSP**.</span></span>
3. <span data-ttu-id="c337e-206">Cópia **TSPSolver.jar** muito**c:\TSP**,</span><span class="sxs-lookup"><span data-stu-id="c337e-206">Copy **TSPSolver.jar** too**c:\TSP**,</span></span>
4. <span data-ttu-id="c337e-207">Crie um arquivo chamado **c:\TSP\cities.txt** com hello conteúdo a seguir.</span><span class="sxs-lookup"><span data-stu-id="c337e-207">Create a file named **c:\TSP\cities.txt** with hello following contents.</span></span>
   
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
5. <span data-ttu-id="c337e-208">Em um prompt de comando, altere os diretórios tooc:\TSP.</span><span class="sxs-lookup"><span data-stu-id="c337e-208">At a command prompt, change directories tooc:\TSP.</span></span>
6. <span data-ttu-id="c337e-209">Verifique a pasta bin de saudação do JRE é na variável de ambiente PATH hello.</span><span class="sxs-lookup"><span data-stu-id="c337e-209">Ensure hello JRE's bin folder is in hello PATH environment variable.</span></span>
7. <span data-ttu-id="c337e-210">Você precisará fila do barramento de serviço toocreate Olá antes de executar permutações de solver TSP hello.</span><span class="sxs-lookup"><span data-stu-id="c337e-210">You'll need toocreate hello service bus queue before you run hello TSP solver permutations.</span></span> <span data-ttu-id="c337e-211">Execute Olá fila do barramento de serviço do comando toocreate Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="c337e-211">Run hello following command toocreate hello service bus queue.</span></span>
   
        java -jar TSPSolver.jar createqueue
8. <span data-ttu-id="c337e-212">Agora que hello fila é criada, você pode executar permutações de solver TSP hello.</span><span class="sxs-lookup"><span data-stu-id="c337e-212">Now that hello queue is created, you can run hello TSP solver permutations.</span></span> <span data-ttu-id="c337e-213">Por exemplo, execute Olá solver de saudação do comando toorun para cidades de 8 a seguir.</span><span class="sxs-lookup"><span data-stu-id="c337e-213">For example, run hello following command toorun hello solver for 8 cities.</span></span>
   
        java -jar TSPSolver.jar 8
   
   <span data-ttu-id="c337e-214">Se você não especificar um número, ele será executado para 10 cidades.</span><span class="sxs-lookup"><span data-stu-id="c337e-214">If you don't specify a number, it will run for 10 cities.</span></span> <span data-ttu-id="c337e-215">Como solver Olá localiza rotas menores atuais, ele adicionará toohello fila.</span><span class="sxs-lookup"><span data-stu-id="c337e-215">As hello solver finds current shortest routes, it will add them toohello queue.</span></span>

> [!NOTE]
> <span data-ttu-id="c337e-216">Olá maior Olá número que você especificar, mais solver de Olá Olá será executado.</span><span class="sxs-lookup"><span data-stu-id="c337e-216">hello larger hello number that you specify, hello longer hello solver will run.</span></span> <span data-ttu-id="c337e-217">Por exemplo, a execução de 14 cidades pode levar vários minutos, e a execução de 15 cidades pode levar várias horas.</span><span class="sxs-lookup"><span data-stu-id="c337e-217">For example, running for 14 cities could take several minutes, and running for 15 cities could take several hours.</span></span> <span data-ttu-id="c337e-218">Aumentando too16 ou cidades mais pode resultar em dias de tempo de execução (eventualmente semanas, meses e anos).</span><span class="sxs-lookup"><span data-stu-id="c337e-218">Increasing too16 or more cities could result in days of runtime (eventually weeks, months, and years).</span></span> <span data-ttu-id="c337e-219">Isso é devido toohello rápido aumento no número de saudação de permutações avaliada pelo solver hello como Olá aumento do número de cidades.</span><span class="sxs-lookup"><span data-stu-id="c337e-219">This is due toohello rapid increase in hello number of permutations evaluated by hello solver as hello number of cities increases.</span></span>
> 
> 

### <a name="how-toorun-hello-monitoring-client-application"></a><span data-ttu-id="c337e-220">Como toorun Olá monitoramento do aplicativo cliente</span><span class="sxs-lookup"><span data-stu-id="c337e-220">How toorun hello monitoring client application</span></span>
1. <span data-ttu-id="c337e-221">Faça logon na máquina tooyour onde você executa o aplicativo de cliente hello.</span><span class="sxs-lookup"><span data-stu-id="c337e-221">Log on tooyour machine where you will run hello client application.</span></span> <span data-ttu-id="c337e-222">Não é necessário toobe Olá mesma máquina executando Olá **TSPSolver** aplicativo, embora ele possa ser.</span><span class="sxs-lookup"><span data-stu-id="c337e-222">This does not need toobe hello same machine running hello **TSPSolver** application, although it can be.</span></span>
2. <span data-ttu-id="c337e-223">Crie uma pasta onde você executará seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c337e-223">Create a folder where you will run your application.</span></span> <span data-ttu-id="c337e-224">Por exemplo, **c:\TSP**.</span><span class="sxs-lookup"><span data-stu-id="c337e-224">For example, **c:\TSP**.</span></span>
3. <span data-ttu-id="c337e-225">Cópia **TSPClient.jar** muito**c:\TSP**,</span><span class="sxs-lookup"><span data-stu-id="c337e-225">Copy **TSPClient.jar** too**c:\TSP**,</span></span>
4. <span data-ttu-id="c337e-226">Verifique a pasta bin de saudação do JRE é na variável de ambiente PATH hello.</span><span class="sxs-lookup"><span data-stu-id="c337e-226">Ensure hello JRE's bin folder is in hello PATH environment variable.</span></span>
5. <span data-ttu-id="c337e-227">Em um prompt de comando, altere os diretórios tooc:\TSP.</span><span class="sxs-lookup"><span data-stu-id="c337e-227">At a command prompt, change directories tooc:\TSP.</span></span>
6. <span data-ttu-id="c337e-228">Execute Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="c337e-228">Run hello following command.</span></span>
   
        java -jar TSPClient.jar
   
    <span data-ttu-id="c337e-229">Opcionalmente, especifique o número de saudação de toosleep minutos entre a verificação de fila hello, passando um argumento de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="c337e-229">Optionally, specify hello number of minutes toosleep in between checking hello queue, by passing in a command-line argument.</span></span> <span data-ttu-id="c337e-230">Olá período de espera padrão para a verificação de fila de saudação é 3 minutos, que é usado se nenhum argumento de linha de comando é passado muito**TSPClient**.</span><span class="sxs-lookup"><span data-stu-id="c337e-230">hello default sleep period for checking hello queue is 3 minutes, which is used if no command-line argument is passed too**TSPClient**.</span></span> <span data-ttu-id="c337e-231">Se você quiser toouse um valor diferente para o intervalo de suspensão de saudação, por exemplo, um minuto, execute Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="c337e-231">If you want toouse a different value for hello sleep interval, for example, one minute, run hello following command.</span></span>
   
        java -jar TSPClient.jar 1
   
    <span data-ttu-id="c337e-232">cliente Olá será executado até que ele vê uma mensagem da fila de "Completo".</span><span class="sxs-lookup"><span data-stu-id="c337e-232">hello client will run until it sees a queue message of "Complete".</span></span> <span data-ttu-id="c337e-233">Observe que, se você executar várias ocorrências do solver Olá sem executar o cliente hello, talvez seja necessário cliente de saudação toorun fila de saudação vazio toocompletely várias vezes.</span><span class="sxs-lookup"><span data-stu-id="c337e-233">Note that if you run multiple occurrences of hello solver without running hello client, you may need toorun hello client multiple times toocompletely empty hello queue.</span></span> <span data-ttu-id="c337e-234">Como alternativa, você pode excluir fila hello e, em seguida, crie-o novamente.</span><span class="sxs-lookup"><span data-stu-id="c337e-234">Alternatively, you can delete hello queue and then create it again.</span></span> <span data-ttu-id="c337e-235">fila de Olá toodelete, execute o seguinte de saudação **TSPSolver** (não **TSPClient**) comando.</span><span class="sxs-lookup"><span data-stu-id="c337e-235">toodelete hello queue, run hello following **TSPSolver** (not **TSPClient**)  command.</span></span>
   
        java -jar TSPSolver.jar deletequeue
   
    <span data-ttu-id="c337e-236">o solver Olá será executado até terminar de examinar todas as rotas.</span><span class="sxs-lookup"><span data-stu-id="c337e-236">hello solver will run until it finishes examining all routes.</span></span>

## <a name="how-toostop-hello-java-applications"></a><span data-ttu-id="c337e-237">Como toostop Olá aplicativos Java</span><span class="sxs-lookup"><span data-stu-id="c337e-237">How toostop hello Java applications</span></span>
<span data-ttu-id="c337e-238">Para o solver hello e aplicativos cliente, você pode pressionar **Ctrl + C** tooexit se você quiser tooend toonormal anterior conclusão.</span><span class="sxs-lookup"><span data-stu-id="c337e-238">For both hello solver and client applications, you can press **Ctrl+C** tooexit if you want tooend prior toonormal completion.</span></span>

[solver_output]:media/java-run-compute-intensive-task/WA_JavaTSPSolver.png
[client_output]:media/java-run-compute-intensive-task/WA_JavaTSPClient.png
[svc_bus_node]:media/java-run-compute-intensive-task/SvcBusQueues_02_SvcBusNode.jpg
[create_namespace]:media/java-run-compute-intensive-task/SvcBusQueues_03_CreateNewSvcNamespace.jpg
[avail_namespaces]:media/java-run-compute-intensive-task/SvcBusQueues_04_SvcBusNode_AvailNamespaces.jpg
[namespace_list]:media/java-run-compute-intensive-task/SvcBusQueues_05_NamespaceList.jpg
[properties_pane]:media/java-run-compute-intensive-task/SvcBusQueues_06_PropertiesPane.jpg
[default_key]:media/java-run-compute-intensive-task/SvcBusQueues_07_DefaultKey.jpg
[add_ca_cert]: ../../../java-add-certificate-ca-store.md
