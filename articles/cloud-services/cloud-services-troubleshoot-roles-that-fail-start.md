---
title: "Como solucionar problemas de funções com falha na inicialização | Microsoft Docs"
description: "Veja algumas razões comuns pelas quais uma função do Serviço de Nuvem pode falhar ao ser iniciada. Soluções para esses problemas também são fornecidas."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 674b2faf-26d7-4f54-99ea-a9e02ef0eb2f
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 7d956192e8b9c3688b8b6f0108bd9296f66fbd62
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-cloud-service-roles-that-fail-to-start"></a><span data-ttu-id="97c14-104">Solução de problemas de funções do serviço de nuvem com falha de inicialização</span><span class="sxs-lookup"><span data-stu-id="97c14-104">Troubleshoot Cloud Service roles that fail to start</span></span>
<span data-ttu-id="97c14-105">Veja alguns problemas comuns e soluções relacionadas às funções do serviço de nuvem do Azure com falha na inicialização.</span><span class="sxs-lookup"><span data-stu-id="97c14-105">Here are some common problems and solutions related to Azure Cloud Services roles that fail to start.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-dlls-or-dependencies"></a><span data-ttu-id="97c14-106">DLLs ou dependências ausentes</span><span class="sxs-lookup"><span data-stu-id="97c14-106">Missing DLLs or dependencies</span></span>
<span data-ttu-id="97c14-107">Funções sem resposta e funções que alternam entre os estados **Inicializando**, **Ocupado** e **Parando** podem ser causadas por DLLs ou assemblies ausentes.</span><span class="sxs-lookup"><span data-stu-id="97c14-107">Unresponsive roles and roles that are cycling between **Initializing**, **Busy**, and **Stopping** states can be caused by missing DLLs or assemblies.</span></span>

<span data-ttu-id="97c14-108">Os sintomas de DLLs ou assemblies ausentes podem ser:</span><span class="sxs-lookup"><span data-stu-id="97c14-108">Symptoms of missing DLLs or assemblies can be:</span></span>

* <span data-ttu-id="97c14-109">A instância de função está alternando entre os estados **Inicializando**, **Ocupado** e **Parando**.</span><span class="sxs-lookup"><span data-stu-id="97c14-109">Your role instance is cycling through **Initializing**, **Busy**, and **Stopping** states.</span></span>
* <span data-ttu-id="97c14-110">A instância de função foi movida para **Pronto** , mas, se você navegar até seu aplicativo Web, a página não será mostrada.</span><span class="sxs-lookup"><span data-stu-id="97c14-110">Your role instance has moved to **Ready** but if you navigate to your web application, the page does not appear.</span></span>

<span data-ttu-id="97c14-111">Há vários métodos recomendados para investigar esses problemas.</span><span class="sxs-lookup"><span data-stu-id="97c14-111">There are several recommended methods for investigating these issues.</span></span>

## <a name="diagnose-missing-dll-issues-in-a-web-role"></a><span data-ttu-id="97c14-112">Como diagnosticar problemas de DLL ausente em uma função Web</span><span class="sxs-lookup"><span data-stu-id="97c14-112">Diagnose missing DLL issues in a web role</span></span>
<span data-ttu-id="97c14-113">Quando você navega para um site que é implantado em uma função Web e o navegador exibe um erro de servidor semelhante ao mostrado abaixo, isso pode indicar que uma DLL está ausente.</span><span class="sxs-lookup"><span data-stu-id="97c14-113">When you navigate to a website that is deployed in a web role, and the browser displays a server error similar to the following, it may indicate that a DLL is missing.</span></span>

![Erro de servidor no aplicativo '/'.](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503388.png)

## <a name="diagnose-issues-by-turning-off-custom-errors"></a><span data-ttu-id="97c14-115">Diagnosticar problemas desativando erros personalizados</span><span class="sxs-lookup"><span data-stu-id="97c14-115">Diagnose issues by turning off custom errors</span></span>
<span data-ttu-id="97c14-116">Informações sobre erros mais completas podem ser exibidas pela configuração de web.config da função Web para definir o modo de erro personalizado como Desativado e pela reimplantação do serviço.</span><span class="sxs-lookup"><span data-stu-id="97c14-116">More complete error information can be viewed by configuring the web.config for the web role to set the custom error mode to Off and redeploying the service.</span></span>

<span data-ttu-id="97c14-117">Para exibir erros mais completos sem usar a Área de Trabalho Remota:</span><span class="sxs-lookup"><span data-stu-id="97c14-117">To view more complete errors without using Remote Desktop:</span></span>

1. <span data-ttu-id="97c14-118">Abra a solução no Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="97c14-118">Open the solution in Microsoft Visual Studio.</span></span>
2. <span data-ttu-id="97c14-119">No **Gerenciador de Soluções**, localize o arquivo web.config e abri-lo.</span><span class="sxs-lookup"><span data-stu-id="97c14-119">In the **Solution Explorer**, locate the web.config file and open it.</span></span>
3. <span data-ttu-id="97c14-120">No arquivo web.config, localize a seção system.web e adicione a seguinte linha:</span><span class="sxs-lookup"><span data-stu-id="97c14-120">In the web.config file, locate the system.web section and add the following line:</span></span>

    ```xml
    <customErrors mode="Off" />
    ```
4. <span data-ttu-id="97c14-121">Salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="97c14-121">Save the file.</span></span>
5. <span data-ttu-id="97c14-122">Empacote e implante novamente o serviço.</span><span class="sxs-lookup"><span data-stu-id="97c14-122">Repackage and redeploy the service.</span></span>

<span data-ttu-id="97c14-123">Depois que o serviço for implantado novamente, você verá uma mensagem de erro com o nome do assembly ou DLL ausente.</span><span class="sxs-lookup"><span data-stu-id="97c14-123">Once the service is redeployed, you will see an error message with the name of the missing assembly or DLL.</span></span>

## <a name="diagnose-issues-by-viewing-the-error-remotely"></a><span data-ttu-id="97c14-124">Diagnosticar problemas exibindo o erro remotamente</span><span class="sxs-lookup"><span data-stu-id="97c14-124">Diagnose issues by viewing the error remotely</span></span>
<span data-ttu-id="97c14-125">Você pode usar a Área de Trabalho Remota para acessar a função e exibir informações de erros mais completas remotamente.</span><span class="sxs-lookup"><span data-stu-id="97c14-125">You can use Remote Desktop to access the role and view more complete error information remotely.</span></span> <span data-ttu-id="97c14-126">Use as seguintes etapas para exibir os erros usando a Área de Trabalho Remota:</span><span class="sxs-lookup"><span data-stu-id="97c14-126">Use the following steps to view the errors by using Remote Desktop:</span></span>

1. <span data-ttu-id="97c14-127">Verifique se o Azure SDK 1.3 ou posterior está instalado.</span><span class="sxs-lookup"><span data-stu-id="97c14-127">Ensure that Azure SDK 1.3 or later is installed.</span></span>
2. <span data-ttu-id="97c14-128">Durante a implantação da solução usando o Visual Studio, escolha "Configurar conexões da Área de Trabalho Remota...".</span><span class="sxs-lookup"><span data-stu-id="97c14-128">During the deployment of the solution by using Visual Studio, choose to “Configure Remote Desktop connections…”.</span></span> <span data-ttu-id="97c14-129">Para obter mais informações sobre como configurar a Conexão de Área de Trabalho Remota, confira [Usando a Área de Trabalho Remota com as Funções do Azure](../vs-azure-tools-remote-desktop-roles.md).</span><span class="sxs-lookup"><span data-stu-id="97c14-129">For more information on configuring the Remote Desktop connection, see [Using Remote Desktop with Azure Roles](../vs-azure-tools-remote-desktop-roles.md).</span></span>
3. <span data-ttu-id="97c14-130">No Portal Clássico do Microsoft Azure, depois que a instância mostrar um status de **Pronto**, clique em uma das instâncias de função.</span><span class="sxs-lookup"><span data-stu-id="97c14-130">In the Microsoft Azure classic portal, once the instance shows a status of **Ready**, click one of the role instances.</span></span>
4. <span data-ttu-id="97c14-131">Clique no ícone **Conectar** na área **Acesso Remoto** da faixa de opções.</span><span class="sxs-lookup"><span data-stu-id="97c14-131">Click the **Connect** icon in the **Remote Access** area of the ribbon.</span></span>
5. <span data-ttu-id="97c14-132">Entre na máquina virtual usando as credenciais especificadas durante a configuração da Área de Trabalho Remota.</span><span class="sxs-lookup"><span data-stu-id="97c14-132">Sign in to the virtual machine by using the credentials that were specified during the Remote Desktop configuration.</span></span>
6. <span data-ttu-id="97c14-133">Abra uma janela de comando.</span><span class="sxs-lookup"><span data-stu-id="97c14-133">Open a command window.</span></span>
7. <span data-ttu-id="97c14-134">Digite `IPconfig`.</span><span class="sxs-lookup"><span data-stu-id="97c14-134">Type `IPconfig`.</span></span>
8. <span data-ttu-id="97c14-135">Observe o valor do Endereço IPV4.</span><span class="sxs-lookup"><span data-stu-id="97c14-135">Note the IPV4 Address value.</span></span>
9. <span data-ttu-id="97c14-136">Abra o Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="97c14-136">Open Internet Explorer.</span></span>
10. <span data-ttu-id="97c14-137">Digite o endereço e o nome do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="97c14-137">Type the address and the name of the web application.</span></span> <span data-ttu-id="97c14-138">Por exemplo: `http://<IPV4 Address>/default.aspx`.</span><span class="sxs-lookup"><span data-stu-id="97c14-138">For example, `http://<IPV4 Address>/default.aspx`.</span></span>

<span data-ttu-id="97c14-139">Navegar até o site agora retornará mensagens de erro mais explícitas:</span><span class="sxs-lookup"><span data-stu-id="97c14-139">Navigating to the website will now return more explicit error messages:</span></span>

* <span data-ttu-id="97c14-140">Erro de servidor no aplicativo '/'.</span><span class="sxs-lookup"><span data-stu-id="97c14-140">Server Error in '/' Application.</span></span>
* <span data-ttu-id="97c14-141">Descrição: ocorreu uma exceção sem tratamento durante a execução da solicitação da Web atual.</span><span class="sxs-lookup"><span data-stu-id="97c14-141">Description: An unhandled exception occurred during the execution of the current web request.</span></span> <span data-ttu-id="97c14-142">Examine o rastreamento de pilha para obter mais informações sobre o erro e em que ponto ele ocorreu no código.</span><span class="sxs-lookup"><span data-stu-id="97c14-142">Please review the stack trace for more information about the error and where it originated in the code.</span></span>
* <span data-ttu-id="97c14-143">Detalhes da exceção: System.IO.FIleNotFoundException: não foi possível carregar o arquivo ou assembly ‘Microsoft.WindowsAzure.StorageClient, Version=1.1.0.0, Culture=neutral, PublicKeyToken=31bf856ad364e35’ ou uma de suas dependências.</span><span class="sxs-lookup"><span data-stu-id="97c14-143">Exception Details: System.IO.FIleNotFoundException: Could not load file or assembly ‘Microsoft.WindowsAzure.StorageClient, Version=1.1.0.0, Culture=neutral, PublicKeyToken=31bf856ad364e35’ or one of its dependencies.</span></span> <span data-ttu-id="97c14-144">O sistema não pode encontrar o arquivo especificado.</span><span class="sxs-lookup"><span data-stu-id="97c14-144">The system cannot find the file specified.</span></span>

<span data-ttu-id="97c14-145">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="97c14-145">For example:</span></span>

![Erro de servidor explícito no aplicativo '/'](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503389.png)

## <a name="diagnose-issues-by-using-the-compute-emulator"></a><span data-ttu-id="97c14-147">Diagnosticar problemas usando o emulador de computação</span><span class="sxs-lookup"><span data-stu-id="97c14-147">Diagnose issues by using the compute emulator</span></span>
<span data-ttu-id="97c14-148">Você pode usar o emulador de computação do Microsoft Azure para diagnosticar e solucionar problemas de dependências ausentes e erros de web.config.</span><span class="sxs-lookup"><span data-stu-id="97c14-148">You can use the Microsoft Azure compute emulator to diagnose and troubleshoot issues of missing dependencies and web.config errors.</span></span>

<span data-ttu-id="97c14-149">Para obter melhores resultados ao usar esse método de diagnóstico, você deve usar um computador ou uma máquina virtual com uma instalação limpa do Windows.</span><span class="sxs-lookup"><span data-stu-id="97c14-149">For best results in using this method of diagnosis, you should use a computer or virtual machine that has a clean installation of Windows.</span></span> <span data-ttu-id="97c14-150">Para simular melhor o ambiente do Azure, use o Windows Server 2008 R2 x64.</span><span class="sxs-lookup"><span data-stu-id="97c14-150">To best simulate the Azure environment, use Windows Server 2008 R2 x64.</span></span>

1. <span data-ttu-id="97c14-151">Instalar a versão autônoma do [SDK do Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="97c14-151">Install the standalone version of the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="97c14-152">No computador de desenvolvimento, compile o projeto do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="97c14-152">On the development machine, build the cloud service project.</span></span>
3. <span data-ttu-id="97c14-153">No Windows Explorer, navegue até a pasta bin\debug do projeto do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="97c14-153">In Windows Explorer, navigate to the bin\debug folder of the cloud service project.</span></span>
4. <span data-ttu-id="97c14-154">Copie a pasta .csx e o arquivo .cscfg para o computador que você está usando para depurar os problemas.</span><span class="sxs-lookup"><span data-stu-id="97c14-154">Copy the .csx folder and .cscfg file to the computer that you are using to debug the issues.</span></span>
5. <span data-ttu-id="97c14-155">No computador limpo, abra uma janela de prompt de comando do SDK do Azure e digite `csrun.exe /devstore:start`.</span><span class="sxs-lookup"><span data-stu-id="97c14-155">On the clean machine, open an Azure SDK Command Prompt window and type `csrun.exe /devstore:start`.</span></span>
6. <span data-ttu-id="97c14-156">No prompt de comando, digite `run csrun <path to .csx folder> <path to .cscfg file> /launchBrowser`.</span><span class="sxs-lookup"><span data-stu-id="97c14-156">At the command prompt, type `run csrun <path to .csx folder> <path to .cscfg file> /launchBrowser`.</span></span>
7. <span data-ttu-id="97c14-157">Quando a função for iniciada, você verá as informações de erro detalhadas no Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="97c14-157">When the role starts, you will see detailed error information in Internet Explorer.</span></span> <span data-ttu-id="97c14-158">Você também pode usar ferramentas de solução de problemas padrão do Windows para ajudar a diagnosticar o problema.</span><span class="sxs-lookup"><span data-stu-id="97c14-158">You can also use standard Windows troubleshooting tools to further diagnose the problem.</span></span>

## <a name="diagnose-issues-by-using-intellitrace"></a><span data-ttu-id="97c14-159">Diagnosticar problemas usando o IntelliTrace</span><span class="sxs-lookup"><span data-stu-id="97c14-159">Diagnose issues by using IntelliTrace</span></span>
<span data-ttu-id="97c14-160">Para as funções Web e de trabalho que usam o .NET Framework 4, você pode usar o [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), que está disponível no Microsoft Visual Studio Enterprise.</span><span class="sxs-lookup"><span data-stu-id="97c14-160">For worker and web roles that use .NET Framework 4, you can use [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), which is available in Microsoft Visual Studio Enterprise.</span></span>

<span data-ttu-id="97c14-161">Siga estas etapas para implantar o serviço com o IntelliTrace habilitado:</span><span class="sxs-lookup"><span data-stu-id="97c14-161">Follow these steps to deploy the service with IntelliTrace enabled:</span></span>

1. <span data-ttu-id="97c14-162">Confirme se o Azure SDK 1.3 ou posterior está instalado.</span><span class="sxs-lookup"><span data-stu-id="97c14-162">Confirm that Azure SDK 1.3 or later is installed.</span></span>
2. <span data-ttu-id="97c14-163">Implante a solução usando o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="97c14-163">Deploy the solution by using Visual Studio.</span></span> <span data-ttu-id="97c14-164">Durante a implantação, marque a caixa de seleção **Habilitar IntelliTrace para funções do .NET 4** .</span><span class="sxs-lookup"><span data-stu-id="97c14-164">During deployment, check the **Enable IntelliTrace for .NET 4 roles** check box.</span></span>
3. <span data-ttu-id="97c14-165">Quando a instância for iniciada, abra o **Gerenciador de Servidores**.</span><span class="sxs-lookup"><span data-stu-id="97c14-165">Once the instance starts, open the **Server Explorer**.</span></span>
4. <span data-ttu-id="97c14-166">Expanda o nó **Azure\\Serviços de Nuvem** e localize a implantação.</span><span class="sxs-lookup"><span data-stu-id="97c14-166">Expand the **Azure\\Cloud Services** node and locate the deployment.</span></span>
5. <span data-ttu-id="97c14-167">Expanda a implantação até ver as instâncias de função.</span><span class="sxs-lookup"><span data-stu-id="97c14-167">Expand the deployment until you see the role instances.</span></span> <span data-ttu-id="97c14-168">Clique com o botão direito do mouse em uma das instâncias.</span><span class="sxs-lookup"><span data-stu-id="97c14-168">Right-click on one of the instances.</span></span>
6. <span data-ttu-id="97c14-169">Escolha **Exibir logs do IntelliTrace**.</span><span class="sxs-lookup"><span data-stu-id="97c14-169">Choose **View IntelliTrace logs**.</span></span> <span data-ttu-id="97c14-170">O **Resumo do IntelliTrace** será aberto.</span><span class="sxs-lookup"><span data-stu-id="97c14-170">The **IntelliTrace Summary** will open.</span></span>
7. <span data-ttu-id="97c14-171">Localize a seção de exceções do resumo.</span><span class="sxs-lookup"><span data-stu-id="97c14-171">Locate the exceptions section of the summary.</span></span> <span data-ttu-id="97c14-172">Se houver exceções, a seção será rotulada como **Dados de Exceção**.</span><span class="sxs-lookup"><span data-stu-id="97c14-172">If there are exceptions, the section will be labeled **Exception Data**.</span></span>
8. <span data-ttu-id="97c14-173">Expanda os **Dados de Exceção** e procure erros **System.IO.FileNotFoundException** semelhantes ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="97c14-173">Expand the **Exception Data** and look for **System.IO.FileNotFoundException** errors similar to the following:</span></span>

![Dados de exceção, arquivo ou assembly ausente](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503390.png)

## <a name="address-missing-dlls-and-assemblies"></a><span data-ttu-id="97c14-175">Lidar com DLLs e assemblies ausentes</span><span class="sxs-lookup"><span data-stu-id="97c14-175">Address missing DLLs and assemblies</span></span>
<span data-ttu-id="97c14-176">Para resolver erros de DLL e assembly ausente, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="97c14-176">To address missing DLL and assembly errors, follow these steps:</span></span>

1. <span data-ttu-id="97c14-177">Abra a solução no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="97c14-177">Open the solution in Visual Studio.</span></span>
2. <span data-ttu-id="97c14-178">No **Gerenciador de Soluções**, abra a pasta **Referências**.</span><span class="sxs-lookup"><span data-stu-id="97c14-178">In **Solution Explorer**, open the **References** folder.</span></span>
3. <span data-ttu-id="97c14-179">Clique no assembly identificado no erro.</span><span class="sxs-lookup"><span data-stu-id="97c14-179">Click the assembly identified in the error.</span></span>
4. <span data-ttu-id="97c14-180">No painel **Propriedades**, localize a **propriedade Copy Local** e defina o valor como **True**.</span><span class="sxs-lookup"><span data-stu-id="97c14-180">In the **Properties** pane, locate **Copy Local property** and set the value to **True**.</span></span>
5. <span data-ttu-id="97c14-181">Reimplante o serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="97c14-181">Redeploy the cloud service.</span></span>

<span data-ttu-id="97c14-182">Após verificar se todos os erros foram corrigidos, você poderá implantar o serviço sem marcar a caixa de seleção **Habilitar IntelliTrace para funções do .NET 4** .</span><span class="sxs-lookup"><span data-stu-id="97c14-182">Once you have verified that all errors have been corrected, you can deploy the service without checking the **Enable IntelliTrace for .NET 4 roles** check box.</span></span>

## <a name="next-steps"></a><span data-ttu-id="97c14-183">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="97c14-183">Next steps</span></span>
<span data-ttu-id="97c14-184">Confira mais [artigos sobre solução de problemas](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) para serviços de nuvem.</span><span class="sxs-lookup"><span data-stu-id="97c14-184">View more [troubleshooting articles](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="97c14-185">Para saber como solucionar problemas das funções do serviço de nuvem usando os dados de diagnóstico do computador Azure PaaS, confira a [série de blogs de Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span><span class="sxs-lookup"><span data-stu-id="97c14-185">To learn how to troubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, see [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
