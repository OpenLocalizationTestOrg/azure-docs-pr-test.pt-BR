---
title: "funções de aaaTroubleshoot que falham toostart | Microsoft Docs"
description: "Aqui estão algumas razões comuns por que uma função de serviço de nuvem pode falhar toostart. Problemas de toothese soluções também são fornecidos."
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
ms.openlocfilehash: e2fbecb08a10984add79dfc74e73de6869bb314f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-service-roles-that-fail-toostart"></a><span data-ttu-id="6fbf7-104">Solucionar problemas de funções de serviço de nuvem que falham toostart</span><span class="sxs-lookup"><span data-stu-id="6fbf7-104">Troubleshoot Cloud Service roles that fail toostart</span></span>
<span data-ttu-id="6fbf7-105">Aqui estão alguns problemas comuns e funções de serviços de nuvem de tooAzure relacionados soluções que não toostart.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-105">Here are some common problems and solutions related tooAzure Cloud Services roles that fail toostart.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-dlls-or-dependencies"></a><span data-ttu-id="6fbf7-106">DLLs ou dependências ausentes</span><span class="sxs-lookup"><span data-stu-id="6fbf7-106">Missing DLLs or dependencies</span></span>
<span data-ttu-id="6fbf7-107">Funções sem resposta e funções que alternam entre os estados **Inicializando**, **Ocupado** e **Parando** podem ser causadas por DLLs ou assemblies ausentes.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-107">Unresponsive roles and roles that are cycling between **Initializing**, **Busy**, and **Stopping** states can be caused by missing DLLs or assemblies.</span></span>

<span data-ttu-id="6fbf7-108">Os sintomas de DLLs ou assemblies ausentes podem ser:</span><span class="sxs-lookup"><span data-stu-id="6fbf7-108">Symptoms of missing DLLs or assemblies can be:</span></span>

* <span data-ttu-id="6fbf7-109">A instância de função está alternando entre os estados **Inicializando**, **Ocupado** e **Parando**.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-109">Your role instance is cycling through **Initializing**, **Busy**, and **Stopping** states.</span></span>
* <span data-ttu-id="6fbf7-110">A instância de função foi movido muito**pronto** , mas se você navegar tooyour aplicativo de web, a página de saudação não será exibida.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-110">Your role instance has moved too**Ready** but if you navigate tooyour web application, hello page does not appear.</span></span>

<span data-ttu-id="6fbf7-111">Há vários métodos recomendados para investigar esses problemas.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-111">There are several recommended methods for investigating these issues.</span></span>

## <a name="diagnose-missing-dll-issues-in-a-web-role"></a><span data-ttu-id="6fbf7-112">Como diagnosticar problemas de DLL ausente em uma função Web</span><span class="sxs-lookup"><span data-stu-id="6fbf7-112">Diagnose missing DLL issues in a web role</span></span>
<span data-ttu-id="6fbf7-113">Quando você navegar pelo site de tooa que é implantado em uma função web e navegador Olá exibe a seguinte toohello semelhante do erro de servidor, isso pode indicar que uma DLL está ausente.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-113">When you navigate tooa website that is deployed in a web role, and hello browser displays a server error similar toohello following, it may indicate that a DLL is missing.</span></span>

![Erro de servidor no aplicativo '/'.](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503388.png)

## <a name="diagnose-issues-by-turning-off-custom-errors"></a><span data-ttu-id="6fbf7-115">Diagnosticar problemas desativando erros personalizados</span><span class="sxs-lookup"><span data-stu-id="6fbf7-115">Diagnose issues by turning off custom errors</span></span>
<span data-ttu-id="6fbf7-116">Informações de erro mais completas podem ser exibidas Configurando Olá Web. config para Olá web função tooset Olá erro personalizado modo tooOff e reimplantar o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-116">More complete error information can be viewed by configuring hello web.config for hello web role tooset hello custom error mode tooOff and redeploying hello service.</span></span>

<span data-ttu-id="6fbf7-117">tooview mais concluído erros sem usar a área de trabalho remota:</span><span class="sxs-lookup"><span data-stu-id="6fbf7-117">tooview more complete errors without using Remote Desktop:</span></span>

1. <span data-ttu-id="6fbf7-118">Abra a solução de saudação do Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-118">Open hello solution in Microsoft Visual Studio.</span></span>
2. <span data-ttu-id="6fbf7-119">Em Olá **Solution Explorer**, localize o arquivo Web. config de saudação e abri-lo.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-119">In hello **Solution Explorer**, locate hello web.config file and open it.</span></span>
3. <span data-ttu-id="6fbf7-120">No arquivo Web. config de hello, localize a seção System. Web hello e adicione Olá seguinte linha:</span><span class="sxs-lookup"><span data-stu-id="6fbf7-120">In hello web.config file, locate hello system.web section and add hello following line:</span></span>

    ```xml
    <customErrors mode="Off" />
    ```
4. <span data-ttu-id="6fbf7-121">Salve o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-121">Save hello file.</span></span>
5. <span data-ttu-id="6fbf7-122">Empacote novamente e reimplante o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-122">Repackage and redeploy hello service.</span></span>

<span data-ttu-id="6fbf7-123">Depois que o serviço Olá é reimplantado, você verá uma mensagem de erro com nome Olá Olá assembly ou DLL ausente.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-123">Once hello service is redeployed, you will see an error message with hello name of hello missing assembly or DLL.</span></span>

## <a name="diagnose-issues-by-viewing-hello-error-remotely"></a><span data-ttu-id="6fbf7-124">Diagnosticar problemas exibindo erros Olá remotamente</span><span class="sxs-lookup"><span data-stu-id="6fbf7-124">Diagnose issues by viewing hello error remotely</span></span>
<span data-ttu-id="6fbf7-125">Você pode usar a função de saudação do tooaccess de área de trabalho remota e exibir informações de erro mais completas remotamente.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-125">You can use Remote Desktop tooaccess hello role and view more complete error information remotely.</span></span> <span data-ttu-id="6fbf7-126">Use Olá erros de saudação do tooview as etapas a seguir usando a área de trabalho remota:</span><span class="sxs-lookup"><span data-stu-id="6fbf7-126">Use hello following steps tooview hello errors by using Remote Desktop:</span></span>

1. <span data-ttu-id="6fbf7-127">Verifique se o Azure SDK 1.3 ou posterior está instalado.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-127">Ensure that Azure SDK 1.3 or later is installed.</span></span>
2. <span data-ttu-id="6fbf7-128">Durante a implantação de saudação da solução hello usando o Visual Studio, escolha muito "Conexões configurar área de trabalho remota …".</span><span class="sxs-lookup"><span data-stu-id="6fbf7-128">During hello deployment of hello solution by using Visual Studio, choose too“Configure Remote Desktop connections…”.</span></span> <span data-ttu-id="6fbf7-129">Para obter mais informações sobre como configurar a conexão de área de trabalho remota hello, consulte [usando a área de trabalho remota com funções do Azure](../vs-azure-tools-remote-desktop-roles.md).</span><span class="sxs-lookup"><span data-stu-id="6fbf7-129">For more information on configuring hello Remote Desktop connection, see [Using Remote Desktop with Azure Roles](../vs-azure-tools-remote-desktop-roles.md).</span></span>
3. <span data-ttu-id="6fbf7-130">No portal clássico Olá Microsoft Azure, depois que a instância de saudação mostra um status de **pronto**, clique em uma das instâncias de função hello.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-130">In hello Microsoft Azure classic portal, once hello instance shows a status of **Ready**, click one of hello role instances.</span></span>
4. <span data-ttu-id="6fbf7-131">Clique em Olá **conectar** ícone Olá **acesso remoto** área da faixa de opções de saudação.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-131">Click hello **Connect** icon in hello **Remote Access** area of hello ribbon.</span></span>
5. <span data-ttu-id="6fbf7-132">Entre na máquina virtual de toohello usando credenciais de saudação que foram especificadas durante a configuração da área de trabalho remota hello.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-132">Sign in toohello virtual machine by using hello credentials that were specified during hello Remote Desktop configuration.</span></span>
6. <span data-ttu-id="6fbf7-133">Abra uma janela de comando.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-133">Open a command window.</span></span>
7. <span data-ttu-id="6fbf7-134">Digite `IPconfig`.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-134">Type `IPconfig`.</span></span>
8. <span data-ttu-id="6fbf7-135">Observe o valor do endereço IPV4 hello.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-135">Note hello IPV4 Address value.</span></span>
9. <span data-ttu-id="6fbf7-136">Abra o Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-136">Open Internet Explorer.</span></span>
10. <span data-ttu-id="6fbf7-137">Digite o endereço de saudação e nome de saudação do aplicativo da web hello.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-137">Type hello address and hello name of hello web application.</span></span> <span data-ttu-id="6fbf7-138">Por exemplo: `http://<IPV4 Address>/default.aspx`.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-138">For example, `http://<IPV4 Address>/default.aspx`.</span></span>

<span data-ttu-id="6fbf7-139">Navegando toohello site agora irá retornar mensagens de erro mais explícitas:</span><span class="sxs-lookup"><span data-stu-id="6fbf7-139">Navigating toohello website will now return more explicit error messages:</span></span>

* <span data-ttu-id="6fbf7-140">Erro de servidor no aplicativo '/'.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-140">Server Error in '/' Application.</span></span>
* <span data-ttu-id="6fbf7-141">Descrição: Uma exceção não tratada ocorreu durante a execução de saudação da solicitação da web atual de saudação.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-141">Description: An unhandled exception occurred during hello execution of hello current web request.</span></span> <span data-ttu-id="6fbf7-142">Analise o rastreamento de pilha de saudação para obter mais informações sobre o erro hello e onde ele foi originado no código de saudação.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-142">Please review hello stack trace for more information about hello error and where it originated in hello code.</span></span>
* <span data-ttu-id="6fbf7-143">Detalhes da exceção: System.IO.FIleNotFoundException: não foi possível carregar o arquivo ou assembly ‘Microsoft.WindowsAzure.StorageClient, Version=1.1.0.0, Culture=neutral, PublicKeyToken=31bf856ad364e35’ ou uma de suas dependências.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-143">Exception Details: System.IO.FIleNotFoundException: Could not load file or assembly ‘Microsoft.WindowsAzure.StorageClient, Version=1.1.0.0, Culture=neutral, PublicKeyToken=31bf856ad364e35’ or one of its dependencies.</span></span> <span data-ttu-id="6fbf7-144">sistema Olá não é possível localizar o arquivo hello especificado.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-144">hello system cannot find hello file specified.</span></span>

<span data-ttu-id="6fbf7-145">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="6fbf7-145">For example:</span></span>

![Erro de servidor explícito no aplicativo '/'](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503389.png)

## <a name="diagnose-issues-by-using-hello-compute-emulator"></a><span data-ttu-id="6fbf7-147">Diagnosticar problemas usando o emulador de computação Olá</span><span class="sxs-lookup"><span data-stu-id="6fbf7-147">Diagnose issues by using hello compute emulator</span></span>
<span data-ttu-id="6fbf7-148">Você pode usar o hello Microsoft Azure compute emulator toodiagnose e solucionar problemas de dependências ausentes e erros de Web. config.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-148">You can use hello Microsoft Azure compute emulator toodiagnose and troubleshoot issues of missing dependencies and web.config errors.</span></span>

<span data-ttu-id="6fbf7-149">Para obter melhores resultados ao usar esse método de diagnóstico, você deve usar um computador ou uma máquina virtual com uma instalação limpa do Windows.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-149">For best results in using this method of diagnosis, you should use a computer or virtual machine that has a clean installation of Windows.</span></span> <span data-ttu-id="6fbf7-150">toobest simular Olá ambiente do Azure, use o Windows Server 2008 R2 x64.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-150">toobest simulate hello Azure environment, use Windows Server 2008 R2 x64.</span></span>

1. <span data-ttu-id="6fbf7-151">Instalar versão autônoma Olá Olá [SDK do Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="6fbf7-151">Install hello standalone version of hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="6fbf7-152">No computador de desenvolvimento Olá, compile o projeto de serviço de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-152">On hello development machine, build hello cloud service project.</span></span>
3. <span data-ttu-id="6fbf7-153">No Windows Explorer, navegue toohello bin\debug pasta do projeto de serviço de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-153">In Windows Explorer, navigate toohello bin\debug folder of hello cloud service project.</span></span>
4. <span data-ttu-id="6fbf7-154">Copiar a pasta hello. CSx e. cscfg toohello computador que você está usando toodebug problemas de saudação do arquivo.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-154">Copy hello .csx folder and .cscfg file toohello computer that you are using toodebug hello issues.</span></span>
5. <span data-ttu-id="6fbf7-155">No hello computador limpo, abra uma janela de Prompt de comando do SDK do Azure e digite `csrun.exe /devstore:start`.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-155">On hello clean machine, open an Azure SDK Command Prompt window and type `csrun.exe /devstore:start`.</span></span>
6. <span data-ttu-id="6fbf7-156">No prompt de comando hello, digite `run csrun <path too.csx folder> <path too.cscfg file> /launchBrowser`.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-156">At hello command prompt, type `run csrun <path too.csx folder> <path too.cscfg file> /launchBrowser`.</span></span>
7. <span data-ttu-id="6fbf7-157">Quando a função hello é iniciado, você verá informações detalhadas do erro no Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-157">When hello role starts, you will see detailed error information in Internet Explorer.</span></span> <span data-ttu-id="6fbf7-158">Você também pode usar ferramentas de solução de problemas padrão do Windows toofurther diagnosticar o problema de saudação.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-158">You can also use standard Windows troubleshooting tools toofurther diagnose hello problem.</span></span>

## <a name="diagnose-issues-by-using-intellitrace"></a><span data-ttu-id="6fbf7-159">Diagnosticar problemas usando o IntelliTrace</span><span class="sxs-lookup"><span data-stu-id="6fbf7-159">Diagnose issues by using IntelliTrace</span></span>
<span data-ttu-id="6fbf7-160">Para as funções Web e de trabalho que usam o .NET Framework 4, você pode usar o [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), que está disponível no Microsoft Visual Studio Enterprise.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-160">For worker and web roles that use .NET Framework 4, you can use [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), which is available in Microsoft Visual Studio Enterprise.</span></span>

<span data-ttu-id="6fbf7-161">Execute o serviço de saudação de toodeploy essas etapas com o IntelliTrace habilitado:</span><span class="sxs-lookup"><span data-stu-id="6fbf7-161">Follow these steps toodeploy hello service with IntelliTrace enabled:</span></span>

1. <span data-ttu-id="6fbf7-162">Confirme se o Azure SDK 1.3 ou posterior está instalado.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-162">Confirm that Azure SDK 1.3 or later is installed.</span></span>
2. <span data-ttu-id="6fbf7-163">Implante solução de saudação usando o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-163">Deploy hello solution by using Visual Studio.</span></span> <span data-ttu-id="6fbf7-164">Durante a implantação, verifique Olá **habilitar IntelliTrace para funções do .NET 4** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-164">During deployment, check hello **Enable IntelliTrace for .NET 4 roles** check box.</span></span>
3. <span data-ttu-id="6fbf7-165">Depois de iniciada a instância hello, abra Olá **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-165">Once hello instance starts, open hello **Server Explorer**.</span></span>
4. <span data-ttu-id="6fbf7-166">Expanda Olá **Azure\\serviços de nuvem** nó e localize a implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-166">Expand hello **Azure\\Cloud Services** node and locate hello deployment.</span></span>
5. <span data-ttu-id="6fbf7-167">Expanda a implantação de saudação até que você veja instâncias de função hello.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-167">Expand hello deployment until you see hello role instances.</span></span> <span data-ttu-id="6fbf7-168">Clique em uma das instâncias de saudação.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-168">Right-click on one of hello instances.</span></span>
6. <span data-ttu-id="6fbf7-169">Escolha **Exibir logs do IntelliTrace**.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-169">Choose **View IntelliTrace logs**.</span></span> <span data-ttu-id="6fbf7-170">Olá **resumo do IntelliTrace** será aberto.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-170">hello **IntelliTrace Summary** will open.</span></span>
7. <span data-ttu-id="6fbf7-171">Localize a seção de exceções de saudação do hello resumo.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-171">Locate hello exceptions section of hello summary.</span></span> <span data-ttu-id="6fbf7-172">Se houver exceções, seção hello será rotulada **dados de exceção**.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-172">If there are exceptions, hello section will be labeled **Exception Data**.</span></span>
8. <span data-ttu-id="6fbf7-173">Expanda Olá **dados de exceção** e procure **System.IO. FileNotFoundException** a seguir toohello semelhante erros:</span><span class="sxs-lookup"><span data-stu-id="6fbf7-173">Expand hello **Exception Data** and look for **System.IO.FileNotFoundException** errors similar toohello following:</span></span>

![Dados de exceção, arquivo ou assembly ausente](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503390.png)

## <a name="address-missing-dlls-and-assemblies"></a><span data-ttu-id="6fbf7-175">Lidar com DLLs e assemblies ausentes</span><span class="sxs-lookup"><span data-stu-id="6fbf7-175">Address missing DLLs and assemblies</span></span>
<span data-ttu-id="6fbf7-176">tooaddress tem erros DLL e assembly, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="6fbf7-176">tooaddress missing DLL and assembly errors, follow these steps:</span></span>

1. <span data-ttu-id="6fbf7-177">Abra a solução de saudação no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-177">Open hello solution in Visual Studio.</span></span>
2. <span data-ttu-id="6fbf7-178">Em **Solution Explorer**, abra Olá **referências** pasta.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-178">In **Solution Explorer**, open hello **References** folder.</span></span>
3. <span data-ttu-id="6fbf7-179">Clique em assembly hello identificado no erro hello.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-179">Click hello assembly identified in hello error.</span></span>
4. <span data-ttu-id="6fbf7-180">Em Olá **propriedades** painel, localize **propriedade Copy Local** e defina o valor de saudação muito**True**.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-180">In hello **Properties** pane, locate **Copy Local property** and set hello value too**True**.</span></span>
5. <span data-ttu-id="6fbf7-181">Reimplante o serviço de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-181">Redeploy hello cloud service.</span></span>

<span data-ttu-id="6fbf7-182">Depois de ter verificado que todos os erros foram corrigidos, você pode implantar o serviço de saudação sem verificar Olá **habilitar IntelliTrace para funções do .NET 4** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-182">Once you have verified that all errors have been corrected, you can deploy hello service without checking hello **Enable IntelliTrace for .NET 4 roles** check box.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6fbf7-183">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6fbf7-183">Next steps</span></span>
<span data-ttu-id="6fbf7-184">Confira mais [artigos sobre solução de problemas](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) para serviços de nuvem.</span><span class="sxs-lookup"><span data-stu-id="6fbf7-184">View more [troubleshooting articles](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="6fbf7-185">toolearn como função de serviço de nuvem tootroubleshoot problemas usando dados de diagnóstico do computador de PaaS do Azure, consulte [série do blog de Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span><span class="sxs-lookup"><span data-stu-id="6fbf7-185">toolearn how tootroubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, see [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
