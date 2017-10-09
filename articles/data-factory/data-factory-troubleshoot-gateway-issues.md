---
title: problemas do Gateway de gerenciamento de dados de aaaTroubleshoot | Microsoft Docs
description: Fornece dicas tootroubleshoot problemas relacionados tooData Gateway de gerenciamento.
services: data-factory
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: c6756c37-4e5a-4d1e-ab52-365f149b4128
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
published: True
ms.openlocfilehash: 85dacc8a1e8d574d6e7d5b556c995cebdc148fde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-issues-with-using-data-management-gateway"></a><span data-ttu-id="89c8c-103">Solucionar problemas usando o Gateway de Gerenciamento de Dados</span><span class="sxs-lookup"><span data-stu-id="89c8c-103">Troubleshoot issues with using Data Management Gateway</span></span>
<span data-ttu-id="89c8c-104">Este artigo fornece informações sobre como solucionar problemas com o uso do Gateway de Gerenciamento de Dados.</span><span class="sxs-lookup"><span data-stu-id="89c8c-104">This article provides information on troubleshooting issues with using Data Management Gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="89c8c-105">Consulte Olá [Data Management Gateway](data-factory-data-management-gateway.md) artigo para obter informações detalhadas sobre o gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="89c8c-105">See hello [Data Management Gateway](data-factory-data-management-gateway.md) article for detailed information about hello gateway.</span></span> <span data-ttu-id="89c8c-106">Consulte Olá [mover dados entre locais e na nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo para obter uma explicação da movimentação de dados de um tooMicrosoft de banco de dados do SQL Server local armazenamento de BLOBs do Azure usando o gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="89c8c-106">See hello [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for a walkthrough of moving data from an on-premises SQL Server database tooMicrosoft Azure Blob storage by using hello gateway.</span></span>
>
>

## <a name="failed-tooinstall-or-register-gateway"></a><span data-ttu-id="89c8c-107">Gateway tooinstall ou register com falha</span><span class="sxs-lookup"><span data-stu-id="89c8c-107">Failed tooinstall or register gateway</span></span>
### <a name="1-problem"></a><span data-ttu-id="89c8c-108">1. Problema</span><span class="sxs-lookup"><span data-stu-id="89c8c-108">1. Problem</span></span>
<span data-ttu-id="89c8c-109">Você vir essa mensagem de erro ao instalar e registrar um gateway, especificamente, ao baixar o arquivo de instalação do gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="89c8c-109">You see this error message when installing and registering a gateway, specifically, while downloading hello gateway installation file.</span></span>

`Unable tooconnect toohello remote server". Please check your local settings (Error Code: 10003).`

#### <a name="cause"></a><span data-ttu-id="89c8c-110">Causa</span><span class="sxs-lookup"><span data-stu-id="89c8c-110">Cause</span></span>
<span data-ttu-id="89c8c-111">máquina Olá no qual você está tentando gateway de saudação tooinstall falhou toodownload hello mais recente gateway arquivo de instalação do Centro de download da saudação devido a problema de rede tooa.</span><span class="sxs-lookup"><span data-stu-id="89c8c-111">hello machine on which you are trying tooinstall hello gateway has failed toodownload hello latest gateway installation file from hello download center due tooa network issue.</span></span>

#### <a name="resolution"></a><span data-ttu-id="89c8c-112">Resolução</span><span class="sxs-lookup"><span data-stu-id="89c8c-112">Resolution</span></span>
<span data-ttu-id="89c8c-113">Verifique seu toosee de configurações de servidor de proxy de firewall se Olá impedirem que a conexão de rede de saudação do hello computador toohello [Centro de download](https://download.microsoft.com/)e atualizar as configurações de saudação adequadamente.</span><span class="sxs-lookup"><span data-stu-id="89c8c-113">Check your firewall proxy server settings toosee whether hello settings block hello network connection from hello computer toohello [download center](https://download.microsoft.com/), and update hello settings accordingly.</span></span>

<span data-ttu-id="89c8c-114">Como alternativa, você pode baixar o arquivo de instalação de Olá para o gateway mais recente de saudação do hello [Centro de download](https://www.microsoft.com/download/details.aspx?id=39717) em outros computadores que podem acessar o Centro de download da saudação.</span><span class="sxs-lookup"><span data-stu-id="89c8c-114">Alternatively, you can download hello installation file for hello latest gateway from hello [download center](https://www.microsoft.com/download/details.aspx?id=39717) on other machines that can access hello download center.</span></span> <span data-ttu-id="89c8c-115">Você pode então gateway de toohello arquivo do instalador de saudação cópia computador host e executá-lo manualmente tooinstall e atualização de gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="89c8c-115">You can then copy hello installer file toohello gateway host computer and run it manually tooinstall and update hello gateway.</span></span>

### <a name="2-problem"></a><span data-ttu-id="89c8c-116">2. Problema</span><span class="sxs-lookup"><span data-stu-id="89c8c-116">2. Problem</span></span>
<span data-ttu-id="89c8c-117">Você verá esse erro quando você estiver tentando tooinstall um gateway clicando **instalar diretamente no computador** em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="89c8c-117">You see this error when you're attempting tooinstall a gateway by clicking **install directly on this computer** in hello Azure portal.</span></span>

`Error:  Abort installing a new gateway on this computer because this computer has an existing installed gateway and a computer without any installed gateway is required for installing a new gateway.`  

#### <a name="cause"></a><span data-ttu-id="89c8c-118">Causa</span><span class="sxs-lookup"><span data-stu-id="89c8c-118">Cause</span></span>
<span data-ttu-id="89c8c-119">Um gateway já está instalado na máquina de saudação.</span><span class="sxs-lookup"><span data-stu-id="89c8c-119">A gateway is already installed on hello machine.</span></span>

#### <a name="resolution"></a><span data-ttu-id="89c8c-120">Resolução</span><span class="sxs-lookup"><span data-stu-id="89c8c-120">Resolution</span></span>
<span data-ttu-id="89c8c-121">Desinstalar o gateway existente na máquina de saudação do hello e clique em Olá **instalar diretamente no computador** link novamente.</span><span class="sxs-lookup"><span data-stu-id="89c8c-121">Uninstall hello existing gateway on hello machine and click hello **install directly on this computer** link again.</span></span>

### <a name="3-problem"></a><span data-ttu-id="89c8c-122">3. Problema</span><span class="sxs-lookup"><span data-stu-id="89c8c-122">3. Problem</span></span>
<span data-ttu-id="89c8c-123">Esse erro poderá ser exibido ao registrar um novo gateway.</span><span class="sxs-lookup"><span data-stu-id="89c8c-123">You might see this error when registering a new gateway.</span></span>

`Error: hello gateway has encountered an error during registration.`

#### <a name="cause"></a><span data-ttu-id="89c8c-124">Causa</span><span class="sxs-lookup"><span data-stu-id="89c8c-124">Cause</span></span>
<span data-ttu-id="89c8c-125">Você verá esta mensagem para uma saudação motivos a seguir:</span><span class="sxs-lookup"><span data-stu-id="89c8c-125">You might see this message for one of hello following reasons:</span></span>

* <span data-ttu-id="89c8c-126">formato de saudação da chave do gateway de saudação é inválido.</span><span class="sxs-lookup"><span data-stu-id="89c8c-126">hello format of hello gateway key is invalid.</span></span>
* <span data-ttu-id="89c8c-127">chave do gateway Olá foi invalidado.</span><span class="sxs-lookup"><span data-stu-id="89c8c-127">hello gateway key has been invalidated.</span></span>
* <span data-ttu-id="89c8c-128">chave do gateway Olá tiver sido regenerada do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="89c8c-128">hello gateway key has been regenerated from hello portal.</span></span>  

#### <a name="resolution"></a><span data-ttu-id="89c8c-129">Resolução</span><span class="sxs-lookup"><span data-stu-id="89c8c-129">Resolution</span></span>
<span data-ttu-id="89c8c-130">Verifique se você estiver usando a chave de certo de gateway de saudação do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="89c8c-130">Verify whether you are using hello right gateway key from hello portal.</span></span> <span data-ttu-id="89c8c-131">Se necessário, gerar novamente uma chave e usar Olá tooregister chave Olá gateway.</span><span class="sxs-lookup"><span data-stu-id="89c8c-131">If needed, regenerate a key and use hello key tooregister hello gateway.</span></span>

### <a name="4-problem"></a><span data-ttu-id="89c8c-132">4. Problema</span><span class="sxs-lookup"><span data-stu-id="89c8c-132">4. Problem</span></span>
<span data-ttu-id="89c8c-133">Talvez você veja Olá a seguinte mensagem de erro quando você estiver registrando um gateway.</span><span class="sxs-lookup"><span data-stu-id="89c8c-133">You might see hello following error message when you're registering a gateway.</span></span>

`Error: hello content or format of hello gateway key "{gatewayKey}" is invalid, please go tooazure portal toocreate one new gateway or regenerate hello gateway key.`



![O conteúdo ou o formato da chave é inválido](media/data-factory-troubleshoot-gateway-issues/invalid-format-gateway-key.png)

#### <a name="cause"></a><span data-ttu-id="89c8c-135">Causa</span><span class="sxs-lookup"><span data-stu-id="89c8c-135">Cause</span></span>
<span data-ttu-id="89c8c-136">Olá conteúdo ou formato de chave de gateway de entrada hello está incorreto.</span><span class="sxs-lookup"><span data-stu-id="89c8c-136">hello content or format of hello input gateway key is incorrect.</span></span> <span data-ttu-id="89c8c-137">Um dos motivos Olá pode ser copiados apenas uma parte da chave de saudação do portal de saudação ou você estiver usando uma chave inválida.</span><span class="sxs-lookup"><span data-stu-id="89c8c-137">One of hello reasons can be that you copied only a portion of hello key from hello portal or you're using an invalid key.</span></span>

#### <a name="resolution"></a><span data-ttu-id="89c8c-138">Resolução</span><span class="sxs-lookup"><span data-stu-id="89c8c-138">Resolution</span></span>
<span data-ttu-id="89c8c-139">Gerar uma chave do gateway no portal de saudação e usar Olá cópia botão toocopy Olá chave inteira.</span><span class="sxs-lookup"><span data-stu-id="89c8c-139">Generate a gateway key in hello portal, and use hello copy button toocopy hello whole key.</span></span> <span data-ttu-id="89c8c-140">Em seguida, cole-o no gateway de saudação do tooregister janela.</span><span class="sxs-lookup"><span data-stu-id="89c8c-140">Then paste it in this window tooregister hello gateway.</span></span>

### <a name="5-problem"></a><span data-ttu-id="89c8c-141">5. Problema</span><span class="sxs-lookup"><span data-stu-id="89c8c-141">5. Problem</span></span>
<span data-ttu-id="89c8c-142">Talvez você veja Olá a seguinte mensagem de erro quando você estiver registrando um gateway.</span><span class="sxs-lookup"><span data-stu-id="89c8c-142">You might see hello following error message when you're registering a gateway.</span></span>

`Error: hello gateway key is invalid or empty. Specify a valid gateway key from hello portal.`

![A chave do gateway é inválida ou está vazia](media/data-factory-troubleshoot-gateway-issues/gateway-key-is-invalid-or-empty.png)

#### <a name="cause"></a><span data-ttu-id="89c8c-144">Causa</span><span class="sxs-lookup"><span data-stu-id="89c8c-144">Cause</span></span>
<span data-ttu-id="89c8c-145">chave do gateway Olá tiver sido regenerada ou Olá gateway foi excluído no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="89c8c-145">hello gateway key has been regenerated or hello gateway has been deleted in hello Azure portal.</span></span> <span data-ttu-id="89c8c-146">Ele também pode ocorrer se a instalação do Gateway de gerenciamento de dados de saudação não é mais recente.</span><span class="sxs-lookup"><span data-stu-id="89c8c-146">It can also happen if hello Data Management Gateway setup is not latest.</span></span>

#### <a name="resolution"></a><span data-ttu-id="89c8c-147">Resolução</span><span class="sxs-lookup"><span data-stu-id="89c8c-147">Resolution</span></span>
<span data-ttu-id="89c8c-148">Verifique se a instalação do Gateway de gerenciamento de dados de saudação versão mais recente do hello, você pode encontrar a versão mais recente da saudação na Olá Microsoft [Centro de download](https://go.microsoft.com/fwlink/p/?LinkId=271260).</span><span class="sxs-lookup"><span data-stu-id="89c8c-148">Check if hello Data Management Gateway setup is hello latest version, you can find hello latest version on hello Microsoft [download center](https://go.microsoft.com/fwlink/p/?LinkId=271260).</span></span>

<span data-ttu-id="89c8c-149">Se a instalação for atual / mais recente e gateway ainda existe no Portal, regenerar chave do gateway Olá no hello portal do Azure e usar Olá Olá cópia botão toocopy toda chave e, em seguida, cole-o neste gateway de saudação do tooregister de janela.</span><span class="sxs-lookup"><span data-stu-id="89c8c-149">If setup is current/ latest and gateway still exists on Portal, regenerate hello gateway key in hello Azure portal, and use hello copy button toocopy hello whole key, and then paste it in this window tooregister hello gateway.</span></span> <span data-ttu-id="89c8c-150">Caso contrário, recrie o gateway hello e recomeçar.</span><span class="sxs-lookup"><span data-stu-id="89c8c-150">Otherwise, recreate hello gateway and start over.</span></span>

### <a name="6-problem"></a><span data-ttu-id="89c8c-151">6. Problema</span><span class="sxs-lookup"><span data-stu-id="89c8c-151">6. Problem</span></span>
<span data-ttu-id="89c8c-152">Talvez você veja Olá a seguinte mensagem de erro quando você estiver registrando um gateway.</span><span class="sxs-lookup"><span data-stu-id="89c8c-152">You might see hello following error message when you're registering a gateway.</span></span>

`Error: Gateway has been online for a while, then shows “Gateway is not registered” with hello status “Gateway key is invalid”`

![A chave do gateway é inválida ou está vazia](media/data-factory-troubleshoot-gateway-issues/gateway-not-registered-key-invalid.png)

#### <a name="cause"></a><span data-ttu-id="89c8c-154">Causa</span><span class="sxs-lookup"><span data-stu-id="89c8c-154">Cause</span></span>
<span data-ttu-id="89c8c-155">Esse erro pode acontecer porque Olá gateway foi excluído ou chave do gateway associado Olá tiver sido regenerada.</span><span class="sxs-lookup"><span data-stu-id="89c8c-155">This error might happen because either hello gateway has been deleted or hello associated gateway key has been regenerated.</span></span>

#### <a name="resolution"></a><span data-ttu-id="89c8c-156">Resolução</span><span class="sxs-lookup"><span data-stu-id="89c8c-156">Resolution</span></span>
<span data-ttu-id="89c8c-157">Se Olá gateway foi excluído, crie novamente o gateway de saudação do portal de saudação, clique em **registrar**, copie a chave de saudação do portal hello, cole-o e tente tooregister gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="89c8c-157">If hello gateway has been deleted, re-create hello gateway from hello portal, click **Register**, copy hello key from hello portal, paste it, and try tooregister hello gateway.</span></span>

<span data-ttu-id="89c8c-158">Se o gateway Olá ainda existe, mas sua chave tiver sido regenerada, use o hello novo tooregister chave Olá gateway.</span><span class="sxs-lookup"><span data-stu-id="89c8c-158">If hello gateway still exists but its key has been regenerated, use hello new key tooregister hello gateway.</span></span> <span data-ttu-id="89c8c-159">Se você não tiver chave hello, regenerar chave de saudação novamente do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="89c8c-159">If you don’t have hello key, regenerate hello key again from hello portal.</span></span>

### <a name="7-problem"></a><span data-ttu-id="89c8c-160">7. Problema</span><span class="sxs-lookup"><span data-stu-id="89c8c-160">7. Problem</span></span>
<span data-ttu-id="89c8c-161">Quando você estiver registrando um gateway, você pode precisar tooenter caminho e a senha de um certificado.</span><span class="sxs-lookup"><span data-stu-id="89c8c-161">When you're registering a gateway, you might need tooenter path and password for a certificate.</span></span>

![Especificar certificado](media/data-factory-troubleshoot-gateway-issues/specify-certificate.png)

#### <a name="cause"></a><span data-ttu-id="89c8c-163">Causa</span><span class="sxs-lookup"><span data-stu-id="89c8c-163">Cause</span></span>
<span data-ttu-id="89c8c-164">Olá gateway foi registrado em outros computadores antes.</span><span class="sxs-lookup"><span data-stu-id="89c8c-164">hello gateway has been registered on other machines before.</span></span> <span data-ttu-id="89c8c-165">Durante o registro inicial de saudação de um gateway, um certificado de criptografia foi associado ao gateway hello.</span><span class="sxs-lookup"><span data-stu-id="89c8c-165">During hello initial registration of a gateway, an encryption certificate has been associated with hello gateway.</span></span> <span data-ttu-id="89c8c-166">certificado Olá pode ser gerado automaticamente pelo gateway hello ou fornecido pelo usuário hello.</span><span class="sxs-lookup"><span data-stu-id="89c8c-166">hello certificate can either be self-generated by hello gateway or provided by hello user.</span></span>  <span data-ttu-id="89c8c-167">Esse certificado é usado tooencrypt credenciais saudação do repositório de dados (serviço vinculado).</span><span class="sxs-lookup"><span data-stu-id="89c8c-167">This certificate is used tooencrypt credentials of hello data store (linked service).</span></span>  

![Exportar o certificado](media/data-factory-troubleshoot-gateway-issues/export-certificate.png)

<span data-ttu-id="89c8c-169">Quando restaurar gateway Olá em uma máquina host diferente, solicita que o Assistente de registro Olá para esse certificado toodecrypt credenciais previamente criptografado com esse certificado.</span><span class="sxs-lookup"><span data-stu-id="89c8c-169">When restoring hello gateway on a different host machine, hello registration wizard asks for this certificate toodecrypt credentials previously encrypted with this certificate.</span></span>  <span data-ttu-id="89c8c-170">Sem esse certificado, credenciais Olá não podem ser descriptografadas pelo novo gateway de saudação e execuções de atividade de cópia subsequentes associadas com esse novo gateway falharão.</span><span class="sxs-lookup"><span data-stu-id="89c8c-170">Without this certificate, hello credentials cannot be decrypted by hello new gateway and subsequent copy activity executions associated with this new gateway will fail.</span></span>  

#### <a name="resolution"></a><span data-ttu-id="89c8c-171">Resolução</span><span class="sxs-lookup"><span data-stu-id="89c8c-171">Resolution</span></span>
<span data-ttu-id="89c8c-172">Se você exportou o certificado de credencial de saudação de máquina de gateway original Olá usando Olá **exportar** botão Olá **configurações** guia no Data Management Gateway Configuration Manager, use Olá certificado aqui.</span><span class="sxs-lookup"><span data-stu-id="89c8c-172">If you have exported hello credential certificate from hello original gateway machine by using hello **Export** button on hello **Settings** tab in Data Management Gateway Configuration Manager, use hello certificate here.</span></span>

<span data-ttu-id="89c8c-173">Não é possível ignorar este estágio ao recuperar um gateway.</span><span class="sxs-lookup"><span data-stu-id="89c8c-173">You cannot skip this stage when recovering a gateway.</span></span> <span data-ttu-id="89c8c-174">Se Olá certificado estiver ausente, você precisa toodelete Olá gateway do portal hello e recriar um novo gateway.</span><span class="sxs-lookup"><span data-stu-id="89c8c-174">If hello certificate is missing, you need toodelete hello gateway from hello portal and re-create a new gateway.</span></span>  <span data-ttu-id="89c8c-175">Além disso, atualize todos os serviços vinculados que são relacionadas toohello gateway por precisar reinserir suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="89c8c-175">In addition, update all linked services that are related toohello gateway by reentering their credentials.</span></span>

### <a name="8-problem"></a><span data-ttu-id="89c8c-176">8. Problema</span><span class="sxs-lookup"><span data-stu-id="89c8c-176">8. Problem</span></span>
<span data-ttu-id="89c8c-177">Talvez você veja Olá a seguinte mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="89c8c-177">You might see hello following error message.</span></span>

`Error: hello remote server returned an error: (407) Proxy Authentication Required.`

#### <a name="cause"></a><span data-ttu-id="89c8c-178">Causa</span><span class="sxs-lookup"><span data-stu-id="89c8c-178">Cause</span></span>
<span data-ttu-id="89c8c-179">Esse erro ocorre quando o gateway estiver em um ambiente que requer um proxy HTTP tooaccess recursos da Internet, ou a senha de autenticação do proxy for alterada, mas não é atualizado adequadamente no seu gateway.</span><span class="sxs-lookup"><span data-stu-id="89c8c-179">This error happens when your gateway is in an environment that requires an HTTP proxy tooaccess Internet resources, or your proxy's authentication password is changed but it's not updated accordingly in your gateway.</span></span>

#### <a name="resolution"></a><span data-ttu-id="89c8c-180">Resolução</span><span class="sxs-lookup"><span data-stu-id="89c8c-180">Resolution</span></span>
<span data-ttu-id="89c8c-181">Siga as instruções de Olá Olá [considerações sobre o servidor Proxy](#proxy-server-considerations) seção deste artigo e definir configurações de proxy com o Gerenciador de Gateway de gerenciamento de configuração do dados.</span><span class="sxs-lookup"><span data-stu-id="89c8c-181">Follow hello instructions in hello [Proxy server considerations](#proxy-server-considerations) section of this article, and configure proxy settings with Data Management Gateway Configuration Manager.</span></span>

## <a name="gateway-is-online-with-limited-functionality"></a><span data-ttu-id="89c8c-182">O gateway está online com funcionalidade limitada</span><span class="sxs-lookup"><span data-stu-id="89c8c-182">Gateway is online with limited functionality</span></span>
### <a name="1-problem"></a><span data-ttu-id="89c8c-183">1. Problema</span><span class="sxs-lookup"><span data-stu-id="89c8c-183">1. Problem</span></span>
<span data-ttu-id="89c8c-184">Você ver o status de saudação do gateway Olá online com funcionalidade limitada.</span><span class="sxs-lookup"><span data-stu-id="89c8c-184">You see hello status of hello gateway as online with limited functionality.</span></span>

#### <a name="cause"></a><span data-ttu-id="89c8c-185">Causa</span><span class="sxs-lookup"><span data-stu-id="89c8c-185">Cause</span></span>
<span data-ttu-id="89c8c-186">Consulte status de saudação do gateway Olá online com funcionalidade limitada para uma saudação motivos a seguir:</span><span class="sxs-lookup"><span data-stu-id="89c8c-186">You see hello status of hello gateway as online with limited functionality for one of hello following reasons:</span></span>

* <span data-ttu-id="89c8c-187">Gateway não pode se conectar a toocloud serviço por meio do barramento de serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="89c8c-187">Gateway cannot connect toocloud service through Azure Service Bus.</span></span>
* <span data-ttu-id="89c8c-188">Serviço de nuvem não pode se conectar a toogateway por meio do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="89c8c-188">Cloud service cannot connect toogateway through Service Bus.</span></span>

<span data-ttu-id="89c8c-189">Quando o gateway Olá estiver online com funcionalidade limitada, talvez não seja pipelines de dados de toocreate toouse capaz de saudação Assistente para cópia de fábrica de dados para copiar dados tooor de armazenamentos de dados local.</span><span class="sxs-lookup"><span data-stu-id="89c8c-189">When hello gateway is online with limited functionality, you might not be able toouse hello Data Factory Copy Wizard toocreate data pipelines for copying data tooor from on-premises data stores.</span></span> <span data-ttu-id="89c8c-190">Como alternativa, você pode usar o Editor de fábrica de dados no portal de hello, Visual Studio ou o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="89c8c-190">As a workaround, you can use Data Factory Editor in hello portal, Visual Studio, or Azure PowerShell.</span></span>

#### <a name="resolution"></a><span data-ttu-id="89c8c-191">Resolução</span><span class="sxs-lookup"><span data-stu-id="89c8c-191">Resolution</span></span>
<span data-ttu-id="89c8c-192">Resolução para esse problema (online com funcionalidade limitada) baseia-se gateway Olá não é possível conectar-se o serviço de nuvem toohello ou Olá outra maneira.</span><span class="sxs-lookup"><span data-stu-id="89c8c-192">Resolution for this issue (online with limited functionality) is based on whether hello gateway cannot connect toohello cloud service or hello other way.</span></span> <span data-ttu-id="89c8c-193">Olá seções a seguir fornece essas resoluções.</span><span class="sxs-lookup"><span data-stu-id="89c8c-193">hello following sections provide these resolutions.</span></span>

### <a name="2-problem"></a><span data-ttu-id="89c8c-194">2. Problema</span><span class="sxs-lookup"><span data-stu-id="89c8c-194">2. Problem</span></span>
<span data-ttu-id="89c8c-195">Você verá Olá erro a seguir.</span><span class="sxs-lookup"><span data-stu-id="89c8c-195">You see hello following error.</span></span>

`Error: Gateway cannot connect toocloud service through service bus`

![Gateway não pode se conectar a serviços toocloud](media/data-factory-troubleshoot-gateway-issues/gateway-cannot-connect-to-cloud-service.png)

#### <a name="cause"></a><span data-ttu-id="89c8c-197">Causa</span><span class="sxs-lookup"><span data-stu-id="89c8c-197">Cause</span></span>
<span data-ttu-id="89c8c-198">Gateway não é possível conectar o serviço de nuvem toohello por meio do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="89c8c-198">Gateway cannot connect toohello cloud service through Service Bus.</span></span>

#### <a name="resolution"></a><span data-ttu-id="89c8c-199">Resolução</span><span class="sxs-lookup"><span data-stu-id="89c8c-199">Resolution</span></span>
<span data-ttu-id="89c8c-200">Execute o gateway de saudação tooget essas etapas novamente online:</span><span class="sxs-lookup"><span data-stu-id="89c8c-200">Follow these steps tooget hello gateway back online:</span></span>

1. <span data-ttu-id="89c8c-201">Permitir que o endereço IP no computador do gateway hello e firewall corporativo Olá regras de saída.</span><span class="sxs-lookup"><span data-stu-id="89c8c-201">Allow IP address outbound rules on hello gateway machine and hello corporate firewall.</span></span> <span data-ttu-id="89c8c-202">Você pode localizar endereços IP de saudação Log de eventos do Windows (ID = = 401): uma tentativa foi feita tooaccess um soquete de uma maneira proibida pelas permissões de acesso XX. XX. XX. XX:9350.</span><span class="sxs-lookup"><span data-stu-id="89c8c-202">You can find IP addresses from hello Windows Event Log (ID == 401): An attempt was made tooaccess a socket in a way forbidden by its access permissions XX.XX.XX.XX:9350.</span></span>
* <span data-ttu-id="89c8c-203">Defina configurações de proxy no gateway hello.</span><span class="sxs-lookup"><span data-stu-id="89c8c-203">Configure proxy settings on hello gateway.</span></span> <span data-ttu-id="89c8c-204">Consulte Olá [considerações sobre o servidor Proxy](#proxy-server-considerations) seção para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="89c8c-204">See hello [Proxy server considerations](#proxy-server-considerations) section for details.</span></span>
* <span data-ttu-id="89c8c-205">Habilite portas de saída 5671 e 9350-9354 em ambos os Olá Firewall do Windows no computador do gateway hello e firewall corporativo hello.</span><span class="sxs-lookup"><span data-stu-id="89c8c-205">Enable outbound ports 5671 and 9350-9354 on both hello Windows Firewall on hello gateway machine and hello corporate firewall.</span></span> <span data-ttu-id="89c8c-206">Consulte Olá [portas e firewall](#ports-and-firewall) seção para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="89c8c-206">See hello [Ports and firewall](#ports-and-firewall) section for details.</span></span> <span data-ttu-id="89c8c-207">Esta etapa é opcional, mas recomendada devido a considerações sobre desempenho.</span><span class="sxs-lookup"><span data-stu-id="89c8c-207">This step is optional, but we recommend it for performance consideration.</span></span>

### <a name="3-problem"></a><span data-ttu-id="89c8c-208">3. Problema</span><span class="sxs-lookup"><span data-stu-id="89c8c-208">3. Problem</span></span>
<span data-ttu-id="89c8c-209">Você verá Olá erro a seguir.</span><span class="sxs-lookup"><span data-stu-id="89c8c-209">You see hello following error.</span></span>

`Error: Cloud service cannot connect toogateway through service bus.`

#### <a name="cause"></a><span data-ttu-id="89c8c-210">Causa</span><span class="sxs-lookup"><span data-stu-id="89c8c-210">Cause</span></span>
<span data-ttu-id="89c8c-211">Um erro transitório na conectividade de rede.</span><span class="sxs-lookup"><span data-stu-id="89c8c-211">A transient error in network connectivity.</span></span>

#### <a name="resolution"></a><span data-ttu-id="89c8c-212">Resolução</span><span class="sxs-lookup"><span data-stu-id="89c8c-212">Resolution</span></span>
<span data-ttu-id="89c8c-213">Execute o gateway de saudação tooget essas etapas novamente online:</span><span class="sxs-lookup"><span data-stu-id="89c8c-213">Follow these steps tooget hello gateway back online:</span></span>

1. <span data-ttu-id="89c8c-214">Aguarde alguns minutos, conectividade hello será recuperada automaticamente quando o erro Olá foi eliminado.</span><span class="sxs-lookup"><span data-stu-id="89c8c-214">Wait for a couple of minutes, hello connectivity will be automatically recovered when hello error is gone.</span></span>
* <span data-ttu-id="89c8c-215">Se Olá erro persistir, reinicie o serviço de gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="89c8c-215">If hello error persists, restart hello gateway service.</span></span>

## <a name="failed-tooauthor-linked-service"></a><span data-ttu-id="89c8c-216">Serviço vinculado de tooauthor com falha</span><span class="sxs-lookup"><span data-stu-id="89c8c-216">Failed tooauthor linked service</span></span>
### <a name="problem"></a><span data-ttu-id="89c8c-217">Problema</span><span class="sxs-lookup"><span data-stu-id="89c8c-217">Problem</span></span>
<span data-ttu-id="89c8c-218">Você poderá ver esse erro quando você tentar toouse Gerenciador de credenciais em credenciais da saudação tooinput portal para um novo serviço vinculado, ou atualizar as credenciais para um serviço vinculado existente.</span><span class="sxs-lookup"><span data-stu-id="89c8c-218">You might see this error when you try toouse Credential Manager in hello portal tooinput credentials for a new linked service, or update credentials for an existing linked service.</span></span>

`Error: hello data store '<Server>/<Database>' cannot be reached. Check connection settings for hello data source.`

<span data-ttu-id="89c8c-219">Quando você vir esse erro, a página de configurações de saudação do Data Management Gateway Configuration Manager pode parecer com hello captura de tela a seguir.</span><span class="sxs-lookup"><span data-stu-id="89c8c-219">When you see this error, hello settings page of Data Management Gateway Configuration Manager might look like hello following screenshot.</span></span>

![Não é possível acessar o banco de dados](media/data-factory-troubleshoot-gateway-issues/database-cannot-be-reached.png)

#### <a name="cause"></a><span data-ttu-id="89c8c-221">Causa</span><span class="sxs-lookup"><span data-stu-id="89c8c-221">Cause</span></span>
<span data-ttu-id="89c8c-222">certificado SSL Olá pode ter perdido no computador do gateway hello.</span><span class="sxs-lookup"><span data-stu-id="89c8c-222">hello SSL certificate might have been lost on hello gateway machine.</span></span> <span data-ttu-id="89c8c-223">computador do gateway Olá não é possível carregar o certificado Olá atualmente que é usado para criptografia SSL.</span><span class="sxs-lookup"><span data-stu-id="89c8c-223">hello gateway computer cannot load hello certificate currently that is used for SSL encryption.</span></span> <span data-ttu-id="89c8c-224">Você também poderá ver uma mensagem de erro no log de eventos de saudação que é semelhante toohello mensagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="89c8c-224">You might also see an error message in hello event log that is similar toohello following message.</span></span>

 `Unable tooget hello gateway settings from cloud service. Check hello gateway key and hello network connection. (Certificate with thumbprint cannot be loaded.)`

#### <a name="resolution"></a><span data-ttu-id="89c8c-225">Resolução</span><span class="sxs-lookup"><span data-stu-id="89c8c-225">Resolution</span></span>
<span data-ttu-id="89c8c-226">Siga o problema de saudação de toosolve essas etapas:</span><span class="sxs-lookup"><span data-stu-id="89c8c-226">Follow these steps toosolve hello problem:</span></span>

1. <span data-ttu-id="89c8c-227">Inicie o Gerenciador de Configuração do Gateway de Gerenciamento de Dados.</span><span class="sxs-lookup"><span data-stu-id="89c8c-227">Start Data Management Gateway Configuration Manager.</span></span>
2. <span data-ttu-id="89c8c-228">Alternar toohello **configurações** guia.</span><span class="sxs-lookup"><span data-stu-id="89c8c-228">Switch toohello **Settings** tab.</span></span>  
3. <span data-ttu-id="89c8c-229">Clique em Olá **alteração** certificado SSL do botão toochange hello.</span><span class="sxs-lookup"><span data-stu-id="89c8c-229">Click hello **Change** button toochange hello SSL certificate.</span></span>

   ![botão Alterar certificado](media/data-factory-troubleshoot-gateway-issues/change-button-ssl-certificate.png)
4. <span data-ttu-id="89c8c-231">Selecione um novo certificado como certificado SSL da saudação.</span><span class="sxs-lookup"><span data-stu-id="89c8c-231">Select a new certificate as hello SSL certificate.</span></span> <span data-ttu-id="89c8c-232">Use qualquer certificado SSL gerado por você mesmo ou por qualquer organização.</span><span class="sxs-lookup"><span data-stu-id="89c8c-232">You can use any SSL certificate that is generated by you or any organization.</span></span>

   ![Especificar certificado](media/data-factory-troubleshoot-gateway-issues/specify-http-end-point.png)

## <a name="copy-activity-fails"></a><span data-ttu-id="89c8c-234">Falha na atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="89c8c-234">Copy activity fails</span></span>
### <a name="problem"></a><span data-ttu-id="89c8c-235">Problema</span><span class="sxs-lookup"><span data-stu-id="89c8c-235">Problem</span></span>
<span data-ttu-id="89c8c-236">Você pode notar Olá após falha de "UserErrorFailedToConnectToSqlserver" depois de configurar um pipeline no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="89c8c-236">You might notice hello following "UserErrorFailedToConnectToSqlserver" failure after you set up a pipeline in hello portal.</span></span>

`Error: Copy activity encountered a user error: ErrorCode=UserErrorFailedToConnectToSqlServer,'Type=Microsoft.DataTransfer.Common.Shared.HybridDeliveryException,Message=Cannot connect tooSQL Server`

#### <a name="cause"></a><span data-ttu-id="89c8c-237">Causa</span><span class="sxs-lookup"><span data-stu-id="89c8c-237">Cause</span></span>
<span data-ttu-id="89c8c-238">Isso pode ocorrer por diferentes motivos e a mitigação varia de acordo.</span><span class="sxs-lookup"><span data-stu-id="89c8c-238">This can happen for different reasons, and mitigation varies accordingly.</span></span>

#### <a name="resolution"></a><span data-ttu-id="89c8c-239">Resolução</span><span class="sxs-lookup"><span data-stu-id="89c8c-239">Resolution</span></span>
<span data-ttu-id="89c8c-240">Permitir conexões TCP de saída pela porta TCP/1433 no saudação do lado do cliente de Gateway de gerenciamento de dados antes de se conectar tooan banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="89c8c-240">Allow outbound TCP connections over port TCP/1433 on hello Data Management Gateway client side before connecting tooan SQL database.</span></span>

<span data-ttu-id="89c8c-241">Se o banco de dados de destino de saudação é um banco de dados do SQL Azure, verificar SQL Server configurações do firewall para o Azure também.</span><span class="sxs-lookup"><span data-stu-id="89c8c-241">If hello target database is an Azure SQL database, check SQL Server firewall settings for Azure as well.</span></span>

<span data-ttu-id="89c8c-242">Consulte Olá seção tootest Olá conexão toohello dados o repositório local a seguir.</span><span class="sxs-lookup"><span data-stu-id="89c8c-242">See hello following section tootest hello connection toohello on-premises data store.</span></span>

## <a name="data-store-connection-or-driver-related-errors"></a><span data-ttu-id="89c8c-243">Erro de conexão com o armazenamento de dados ou erros relacionados a drivers</span><span class="sxs-lookup"><span data-stu-id="89c8c-243">Data store connection or driver-related errors</span></span>
<span data-ttu-id="89c8c-244">Se você ver dados armazenar conexão ou erros relacionados a drivers, conclua Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="89c8c-244">If you see data store connection or driver-related errors, complete hello following steps:</span></span>

1. <span data-ttu-id="89c8c-245">Inicie o Gerenciador de configuração de Gateway de gerenciamento de dados no computador do gateway hello.</span><span class="sxs-lookup"><span data-stu-id="89c8c-245">Start Data Management Gateway Configuration Manager on hello gateway machine.</span></span>
2. <span data-ttu-id="89c8c-246">Alternar toohello **diagnóstico** guia.</span><span class="sxs-lookup"><span data-stu-id="89c8c-246">Switch toohello **Diagnostics** tab.</span></span>
3. <span data-ttu-id="89c8c-247">Em **Conexão de teste**, adicionar valores de grupo de gateway hello.</span><span class="sxs-lookup"><span data-stu-id="89c8c-247">In **Test Connection**, add hello gateway group values.</span></span>
4. <span data-ttu-id="89c8c-248">Clique em **teste** toosee se você puder se conectar toohello local fonte de dados do computador do gateway hello usando Olá informações de conexão e credenciais.</span><span class="sxs-lookup"><span data-stu-id="89c8c-248">Click **Test** toosee if you can connect toohello on-premises data source from hello gateway machine by using hello connection information and credentials.</span></span> <span data-ttu-id="89c8c-249">Se a conexão de teste Olá ainda falhar depois de instalar um driver, reinicialização Olá gateway para que ele toopick a alteração mais recente hello.</span><span class="sxs-lookup"><span data-stu-id="89c8c-249">If hello test connection still fails after you install a driver, restart hello gateway for it toopick up hello latest change.</span></span>

![Testar a conexão na guia Diagnóstico](media/data-factory-troubleshoot-gateway-issues/test-connection-in-diagnostics-tab.png)

## <a name="gateway-logs"></a><span data-ttu-id="89c8c-251">Logs do gateway</span><span class="sxs-lookup"><span data-stu-id="89c8c-251">Gateway logs</span></span>
### <a name="send-gateway-logs-toomicrosoft"></a><span data-ttu-id="89c8c-252">Enviar tooMicrosoft de logs do gateway</span><span class="sxs-lookup"><span data-stu-id="89c8c-252">Send gateway logs tooMicrosoft</span></span>
<span data-ttu-id="89c8c-253">Entrar em contato com a Ajuda do Microsoft Support tooget com solução de problemas do gateway, você pode ser solicitado tooshare seus logs do gateway.</span><span class="sxs-lookup"><span data-stu-id="89c8c-253">When you contact Microsoft Support tooget help with troubleshooting gateway issues, you might be asked tooshare your gateway logs.</span></span> <span data-ttu-id="89c8c-254">Com versão de saudação do gateway hello, você pode compartilhar logs do gateway necessária com dois cliques de botão no Data Management Gateway Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="89c8c-254">With hello release of hello gateway, you can share required gateway logs with two button clicks in Data Management Gateway Configuration Manager.</span></span>    

1. <span data-ttu-id="89c8c-255">Alternar toohello **diagnóstico** guia no Data Management Gateway Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="89c8c-255">Switch toohello **Diagnostics** tab in Data Management Gateway Configuration Manager.</span></span>

    ![Gateway de Gerenciamento de Dados - guia Diagnóstico](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-diagnostics-tab.png)
2. <span data-ttu-id="89c8c-257">Clique em **enviar Logs** Olá toosee caixa de diálogo a seguir.</span><span class="sxs-lookup"><span data-stu-id="89c8c-257">Click **Send Logs** toosee hello following dialog box.</span></span>

    ![Envio de logs do Gateway de Gerenciamento de Dados](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-dialog.png)
3. <span data-ttu-id="89c8c-259">(Opcional) Clique em **exibir logs** tooreview logs no Visualizador de eventos de saudação.</span><span class="sxs-lookup"><span data-stu-id="89c8c-259">(Optional) Click **view logs** tooreview logs in hello event viewer.</span></span>
4. <span data-ttu-id="89c8c-260">(Opcional) Clique em **privacidade** tooreview Microsoft web services declaração de privacidade.</span><span class="sxs-lookup"><span data-stu-id="89c8c-260">(Optional) Click **privacy** tooreview Microsoft web services privacy statement.</span></span>
5. <span data-ttu-id="89c8c-261">Quando estiver satisfeito com o que você está prestes a tooupload, clique em **enviar Logs de** tooactually enviar logs de saudação do hello tooMicrosoft última de sete dias para solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="89c8c-261">When you are satisfied with what you are about tooupload, click **Send Logs** tooactually send hello logs from hello last seven days tooMicrosoft for troubleshooting.</span></span> <span data-ttu-id="89c8c-262">Você deve ver o status de Olá da operação de envio de logs Olá conforme Olá captura de tela a seguir.</span><span class="sxs-lookup"><span data-stu-id="89c8c-262">You should see hello status of hello send-logs operation as shown in hello following screenshot.</span></span>

    ![Gateway de Gerenciamento de Dados – status de Enviar logs](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-status.png)
6. <span data-ttu-id="89c8c-264">Após a conclusão da operação de hello, verá uma caixa de diálogo conforme Olá captura de tela a seguir.</span><span class="sxs-lookup"><span data-stu-id="89c8c-264">After hello operation is complete, you see a dialog box as shown in hello following screenshot.</span></span>

    ![Gateway de Gerenciamento de Dados – status de Enviar logs](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-result.png)
7. <span data-ttu-id="89c8c-266">Salvar Olá **relatório ID** e compartilhá-lo com o Microsoft Support.</span><span class="sxs-lookup"><span data-stu-id="89c8c-266">Save hello **Report ID** and share it with Microsoft Support.</span></span> <span data-ttu-id="89c8c-267">Olá relatório ID é usada toolocate logs do gateway Olá que você carregou para solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="89c8c-267">hello report ID is used toolocate hello gateway logs that you uploaded for troubleshooting.</span></span>  <span data-ttu-id="89c8c-268">ID do relatório Olá também serão salvos no Visualizador de eventos de saudação.</span><span class="sxs-lookup"><span data-stu-id="89c8c-268">hello report ID is also saved in hello event viewer.</span></span>  <span data-ttu-id="89c8c-269">Você pode encontrá-lo, observando a ID do evento hello "25" e verifique Olá data e hora.</span><span class="sxs-lookup"><span data-stu-id="89c8c-269">You can find it by looking at hello event ID “25”, and check hello date and time.</span></span>

    ![Gateway de Gerenciamento de Dados – ID de relatório de Enviar logs](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-report-id.png)    

### <a name="archive-gateway-logs-on-gateway-host-machine"></a><span data-ttu-id="89c8c-271">Arquivar logs de gateway no computador host de gateway</span><span class="sxs-lookup"><span data-stu-id="89c8c-271">Archive gateway logs on gateway host machine</span></span>
<span data-ttu-id="89c8c-272">Existem alguns cenários em que há problemas de gateway e não é possível compartilhar logs do gateway diretamente:</span><span class="sxs-lookup"><span data-stu-id="89c8c-272">There are some scenarios where you have gateway issues and you cannot share gateway logs directly:</span></span>

* <span data-ttu-id="89c8c-273">Você instala o gateway hello e registrar gateway Olá manualmente.</span><span class="sxs-lookup"><span data-stu-id="89c8c-273">You manually install hello gateway and register hello gateway.</span></span>
* <span data-ttu-id="89c8c-274">Tente o gateway de saudação tooregister com uma chave regenerada na Data Management Gateway Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="89c8c-274">You try tooregister hello gateway with a regenerated key in Data Management Gateway Configuration Manager.</span></span>
* <span data-ttu-id="89c8c-275">Tente toosend logs e o serviço de host do gateway de saudação não pode ser conectado.</span><span class="sxs-lookup"><span data-stu-id="89c8c-275">You try toosend logs and hello gateway host service cannot be connected.</span></span>

<span data-ttu-id="89c8c-276">Nesses casos, você pode salvar os logs de gateway como um arquivo zip e compartilhá-los quando contatar o suporte da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="89c8c-276">For these scenarios, you can save gateway logs as a zip file and share it when you contact Microsoft support.</span></span> <span data-ttu-id="89c8c-277">Por exemplo, se você receber um erro ao registrar o gateway hello como mostrado no hello captura de tela a seguir.</span><span class="sxs-lookup"><span data-stu-id="89c8c-277">For example, if you receive an error while you register hello gateway as shown in hello following screenshot.</span></span>   

![Gateway de Gerenciamento de Dados – Erro de registro](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-registration-error.png)

<span data-ttu-id="89c8c-279">Clique em Olá **arquivar os logs do gateway** link tooarchive salvar os logs e, em seguida, compartilhe o arquivo zip de saudação com o suporte da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="89c8c-279">Click hello **Archive gateway logs** link tooarchive and save logs, and then share hello zip file with Microsoft support.</span></span>

![Gateway de Gerenciamento de Dados - Arquivar logs](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-archive-logs.png)

### <a name="locate-gateway-logs"></a><span data-ttu-id="89c8c-281">Localizar os logs do gateway</span><span class="sxs-lookup"><span data-stu-id="89c8c-281">Locate gateway logs</span></span>
<span data-ttu-id="89c8c-282">Você pode encontrar informações de log detalhado de gateway nos logs de eventos do Windows hello.</span><span class="sxs-lookup"><span data-stu-id="89c8c-282">You can find detailed gateway log information in hello Windows event logs.</span></span>

1. <span data-ttu-id="89c8c-283">Inicie o **Visualizador de eventos** do Windows.</span><span class="sxs-lookup"><span data-stu-id="89c8c-283">Start Windows **Event Viewer**.</span></span>
2. <span data-ttu-id="89c8c-284">Localize os logs no hello **Logs de aplicativos e serviços** > **Data Management Gateway** pasta.</span><span class="sxs-lookup"><span data-stu-id="89c8c-284">Locate logs in hello **Application and Services Logs** > **Data Management Gateway** folder.</span></span>

 <span data-ttu-id="89c8c-285">Quando você estiver solucionando problemas relacionados ao gateway, procure eventos de nível de erro no Visualizador de eventos de saudação.</span><span class="sxs-lookup"><span data-stu-id="89c8c-285">When you're troubleshooting gateway-related issues, look for error level events in hello event viewer.</span></span>

![Gateway de Gerenciamento de Dados – Logs no visualizador de eventos](media/data-factory-troubleshoot-gateway-issues/gateway-logs-event-viewer.png)
