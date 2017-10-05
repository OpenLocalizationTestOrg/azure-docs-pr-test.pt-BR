---
title: Solucionar problemas do Gateway de Gerenciamento de Dados | Microsoft Docs
description: Fornece dicas para solucionar problemas relacionados ao Gateway de Gerenciamento de Dados.
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
ms.openlocfilehash: b8e50a4e3c0b9c535ccc2344ff22261a356d5acc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-issues-with-using-data-management-gateway"></a><span data-ttu-id="29f52-103">Solucionar problemas usando o Gateway de Gerenciamento de Dados</span><span class="sxs-lookup"><span data-stu-id="29f52-103">Troubleshoot issues with using Data Management Gateway</span></span>
<span data-ttu-id="29f52-104">Este artigo fornece informações sobre como solucionar problemas com o uso do Gateway de Gerenciamento de Dados.</span><span class="sxs-lookup"><span data-stu-id="29f52-104">This article provides information on troubleshooting issues with using Data Management Gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="29f52-105">Consulte o artigo [Gateway de Gerenciamento de Dados](data-factory-data-management-gateway.md) para saber mais sobre o gateway.</span><span class="sxs-lookup"><span data-stu-id="29f52-105">See the [Data Management Gateway](data-factory-data-management-gateway.md) article for detailed information about the gateway.</span></span> <span data-ttu-id="29f52-106">Consulte o artigo [Mover dados entre local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) para obter um passo a passo de como mover dados de um banco de dados SQL Server local para um armazenamento de blobs do Microsoft Azure usando o gateway.</span><span class="sxs-lookup"><span data-stu-id="29f52-106">See the [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for a walkthrough of moving data from an on-premises SQL Server database to Microsoft Azure Blob storage by using the gateway.</span></span>
>
>

## <a name="failed-to-install-or-register-gateway"></a><span data-ttu-id="29f52-107">Falha ao instalar ou registrar o gateway</span><span class="sxs-lookup"><span data-stu-id="29f52-107">Failed to install or register gateway</span></span>
### <a name="1-problem"></a><span data-ttu-id="29f52-108">1. Problema</span><span class="sxs-lookup"><span data-stu-id="29f52-108">1. Problem</span></span>
<span data-ttu-id="29f52-109">Essa mensagem de erro é exibida ao instalar e registrar um gateway, especificamente, ao baixar o arquivo de instalação do gateway.</span><span class="sxs-lookup"><span data-stu-id="29f52-109">You see this error message when installing and registering a gateway, specifically, while downloading the gateway installation file.</span></span>

`Unable to connect to the remote server". Please check your local settings (Error Code: 10003).`

#### <a name="cause"></a><span data-ttu-id="29f52-110">Causa</span><span class="sxs-lookup"><span data-stu-id="29f52-110">Cause</span></span>
<span data-ttu-id="29f52-111">A máquina na qual você está tentando instalar o gateway falha ao baixar o arquivo de instalação do gateway mais recente do Centro de download devido a um problema de rede.</span><span class="sxs-lookup"><span data-stu-id="29f52-111">The machine on which you are trying to install the gateway has failed to download the latest gateway installation file from the download center due to a network issue.</span></span>

#### <a name="resolution"></a><span data-ttu-id="29f52-112">Resolução</span><span class="sxs-lookup"><span data-stu-id="29f52-112">Resolution</span></span>
<span data-ttu-id="29f52-113">Verifique suas configurações de firewall/servidor proxy para ver se elas bloqueiam a conexão de rede no computador com o [centro de download](https://download.microsoft.com/) e atualize as configurações de acordo.</span><span class="sxs-lookup"><span data-stu-id="29f52-113">Check your firewall proxy server settings to see whether the settings block the network connection from the computer to the [download center](https://download.microsoft.com/), and update the settings accordingly.</span></span>

<span data-ttu-id="29f52-114">Como alternativa, você pode baixar o arquivo de instalação para o gateway mais recente do [Centro de download](https://www.microsoft.com/download/details.aspx?id=39717) em outras máquinas que podem acessar o centro de download.</span><span class="sxs-lookup"><span data-stu-id="29f52-114">Alternatively, you can download the installation file for the latest gateway from the [download center](https://www.microsoft.com/download/details.aspx?id=39717) on other machines that can access the download center.</span></span> <span data-ttu-id="29f52-115">Em seguida, você pode copiar o arquivo instalador para o computador host do gateway e executá-lo manualmente para instalar e atualizar o gateway.</span><span class="sxs-lookup"><span data-stu-id="29f52-115">You can then copy the installer file to the gateway host computer and run it manually to install and update the gateway.</span></span>

### <a name="2-problem"></a><span data-ttu-id="29f52-116">2. Problema</span><span class="sxs-lookup"><span data-stu-id="29f52-116">2. Problem</span></span>
<span data-ttu-id="29f52-117">Esse erro é exibido ao tentar instalar um gateway clicando em **Instalar diretamente neste computador** no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="29f52-117">You see this error when you're attempting to install a gateway by clicking **install directly on this computer** in the Azure portal.</span></span>

`Error:  Abort installing a new gateway on this computer because this computer has an existing installed gateway and a computer without any installed gateway is required for installing a new gateway.`  

#### <a name="cause"></a><span data-ttu-id="29f52-118">Causa</span><span class="sxs-lookup"><span data-stu-id="29f52-118">Cause</span></span>
<span data-ttu-id="29f52-119">Um gateway já está instalado no computador.</span><span class="sxs-lookup"><span data-stu-id="29f52-119">A gateway is already installed on the machine.</span></span>

#### <a name="resolution"></a><span data-ttu-id="29f52-120">Resolução</span><span class="sxs-lookup"><span data-stu-id="29f52-120">Resolution</span></span>
<span data-ttu-id="29f52-121">Desinstale o gateway existente no computador e clique no link **Instalar diretamente neste computador** novamente.</span><span class="sxs-lookup"><span data-stu-id="29f52-121">Uninstall the existing gateway on the machine and click the **install directly on this computer** link again.</span></span>

### <a name="3-problem"></a><span data-ttu-id="29f52-122">3. Problema</span><span class="sxs-lookup"><span data-stu-id="29f52-122">3. Problem</span></span>
<span data-ttu-id="29f52-123">Esse erro poderá ser exibido ao registrar um novo gateway.</span><span class="sxs-lookup"><span data-stu-id="29f52-123">You might see this error when registering a new gateway.</span></span>

`Error: The gateway has encountered an error during registration.`

#### <a name="cause"></a><span data-ttu-id="29f52-124">Causa</span><span class="sxs-lookup"><span data-stu-id="29f52-124">Cause</span></span>
<span data-ttu-id="29f52-125">Esta mensagem poderá ser exibida por um dos seguintes motivos:</span><span class="sxs-lookup"><span data-stu-id="29f52-125">You might see this message for one of the following reasons:</span></span>

* <span data-ttu-id="29f52-126">O formato da chave do gateway é inválido.</span><span class="sxs-lookup"><span data-stu-id="29f52-126">The format of the gateway key is invalid.</span></span>
* <span data-ttu-id="29f52-127">A chave do gateway foi invalidada.</span><span class="sxs-lookup"><span data-stu-id="29f52-127">The gateway key has been invalidated.</span></span>
* <span data-ttu-id="29f52-128">A chave do gateway foi regenerada no portal.</span><span class="sxs-lookup"><span data-stu-id="29f52-128">The gateway key has been regenerated from the portal.</span></span>  

#### <a name="resolution"></a><span data-ttu-id="29f52-129">Resolução</span><span class="sxs-lookup"><span data-stu-id="29f52-129">Resolution</span></span>
<span data-ttu-id="29f52-130">Verifique se você está usando a chave de gateway correta do portal.</span><span class="sxs-lookup"><span data-stu-id="29f52-130">Verify whether you are using the right gateway key from the portal.</span></span> <span data-ttu-id="29f52-131">Se necessário, regenere uma chave e use-a para registrar o gateway.</span><span class="sxs-lookup"><span data-stu-id="29f52-131">If needed, regenerate a key and use the key to register the gateway.</span></span>

### <a name="4-problem"></a><span data-ttu-id="29f52-132">4. Problema</span><span class="sxs-lookup"><span data-stu-id="29f52-132">4. Problem</span></span>
<span data-ttu-id="29f52-133">A seguinte mensagem de erro poderá ser exibida ao registrar um gateway.</span><span class="sxs-lookup"><span data-stu-id="29f52-133">You might see the following error message when you're registering a gateway.</span></span>

`Error: The content or format of the gateway key "{gatewayKey}" is invalid, please go to azure portal to create one new gateway or regenerate the gateway key.`



![O conteúdo ou o formato da chave é inválido](media/data-factory-troubleshoot-gateway-issues/invalid-format-gateway-key.png)

#### <a name="cause"></a><span data-ttu-id="29f52-135">Causa</span><span class="sxs-lookup"><span data-stu-id="29f52-135">Cause</span></span>
<span data-ttu-id="29f52-136">O conteúdo ou o formato da chave do gateway de entrada está incorreto.</span><span class="sxs-lookup"><span data-stu-id="29f52-136">The content or format of the input gateway key is incorrect.</span></span> <span data-ttu-id="29f52-137">Um dos motivos pode ser que você copiou apenas parte da chave do portal ou está usando uma chave inválida.</span><span class="sxs-lookup"><span data-stu-id="29f52-137">One of the reasons can be that you copied only a portion of the key from the portal or you're using an invalid key.</span></span>

#### <a name="resolution"></a><span data-ttu-id="29f52-138">Resolução</span><span class="sxs-lookup"><span data-stu-id="29f52-138">Resolution</span></span>
<span data-ttu-id="29f52-139">Gere uma chave de gateway no portal e use o botão para copiar a chave completa.</span><span class="sxs-lookup"><span data-stu-id="29f52-139">Generate a gateway key in the portal, and use the copy button to copy the whole key.</span></span> <span data-ttu-id="29f52-140">Em seguida, cole-a nessa janela para registrar o gateway.</span><span class="sxs-lookup"><span data-stu-id="29f52-140">Then paste it in this window to register the gateway.</span></span>

### <a name="5-problem"></a><span data-ttu-id="29f52-141">5. Problema</span><span class="sxs-lookup"><span data-stu-id="29f52-141">5. Problem</span></span>
<span data-ttu-id="29f52-142">A seguinte mensagem de erro poderá ser exibida ao registrar um gateway.</span><span class="sxs-lookup"><span data-stu-id="29f52-142">You might see the following error message when you're registering a gateway.</span></span>

`Error: The gateway key is invalid or empty. Specify a valid gateway key from the portal.`

![A chave do gateway é inválida ou está vazia](media/data-factory-troubleshoot-gateway-issues/gateway-key-is-invalid-or-empty.png)

#### <a name="cause"></a><span data-ttu-id="29f52-144">Causa</span><span class="sxs-lookup"><span data-stu-id="29f52-144">Cause</span></span>
<span data-ttu-id="29f52-145">A chave do gateway foi regenerada ou o gateway foi excluído do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="29f52-145">The gateway key has been regenerated or the gateway has been deleted in the Azure portal.</span></span> <span data-ttu-id="29f52-146">Isso também pode ocorrer se a configuração do Gateway de Gerenciamento de Dados não for a mais recente.</span><span class="sxs-lookup"><span data-stu-id="29f52-146">It can also happen if the Data Management Gateway setup is not latest.</span></span>

#### <a name="resolution"></a><span data-ttu-id="29f52-147">Resolução</span><span class="sxs-lookup"><span data-stu-id="29f52-147">Resolution</span></span>
<span data-ttu-id="29f52-148">Verifique se a configuração do Gateway de Gerenciamento de Dados é a versão mais recente. Encontre a versão mais recente no [Centro de Download da Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=271260).</span><span class="sxs-lookup"><span data-stu-id="29f52-148">Check if the Data Management Gateway setup is the latest version, you can find the latest version on the Microsoft [download center](https://go.microsoft.com/fwlink/p/?LinkId=271260).</span></span>

<span data-ttu-id="29f52-149">Se a configuração for a atual/mais recente e o gateway ainda existir no Portal, gere novamente a chave do gateway no Portal do Azure e use o botão Copiar para copiar a chave inteira, e cole-a nesta janela para registrar o gateway.</span><span class="sxs-lookup"><span data-stu-id="29f52-149">If setup is current/ latest and gateway still exists on Portal, regenerate the gateway key in the Azure portal, and use the copy button to copy the whole key, and then paste it in this window to register the gateway.</span></span> <span data-ttu-id="29f52-150">Caso contrário, recrie o gateway e comece novamente.</span><span class="sxs-lookup"><span data-stu-id="29f52-150">Otherwise, recreate the gateway and start over.</span></span>

### <a name="6-problem"></a><span data-ttu-id="29f52-151">6. Problema</span><span class="sxs-lookup"><span data-stu-id="29f52-151">6. Problem</span></span>
<span data-ttu-id="29f52-152">A seguinte mensagem de erro poderá ser exibida ao registrar um gateway.</span><span class="sxs-lookup"><span data-stu-id="29f52-152">You might see the following error message when you're registering a gateway.</span></span>

`Error: Gateway has been online for a while, then shows “Gateway is not registered” with the status “Gateway key is invalid”`

![A chave do gateway é inválida ou está vazia](media/data-factory-troubleshoot-gateway-issues/gateway-not-registered-key-invalid.png)

#### <a name="cause"></a><span data-ttu-id="29f52-154">Causa</span><span class="sxs-lookup"><span data-stu-id="29f52-154">Cause</span></span>
<span data-ttu-id="29f52-155">Esse erro pode ocorrer porque o gateway foi excluído ou a chave do gateway associada foi regenerada.</span><span class="sxs-lookup"><span data-stu-id="29f52-155">This error might happen because either the gateway has been deleted or the associated gateway key has been regenerated.</span></span>

#### <a name="resolution"></a><span data-ttu-id="29f52-156">Resolução</span><span class="sxs-lookup"><span data-stu-id="29f52-156">Resolution</span></span>
<span data-ttu-id="29f52-157">Se o gateway foi excluído, recrie o gateway no portal, clique em **Registrar**, copie a chave do portal, cole-a e tente registrar o gateway.</span><span class="sxs-lookup"><span data-stu-id="29f52-157">If the gateway has been deleted, re-create the gateway from the portal, click **Register**, copy the key from the portal, paste it, and try to register the gateway.</span></span>

<span data-ttu-id="29f52-158">Se o gateway ainda existir, mas a chave tiver sido regenerada, use a nova chave para registrar o gateway.</span><span class="sxs-lookup"><span data-stu-id="29f52-158">If the gateway still exists but its key has been regenerated, use the new key to register the gateway.</span></span> <span data-ttu-id="29f52-159">Se você não tiver a chave, regenere-a novamente no portal.</span><span class="sxs-lookup"><span data-stu-id="29f52-159">If you don’t have the key, regenerate the key again from the portal.</span></span>

### <a name="7-problem"></a><span data-ttu-id="29f52-160">7. Problema</span><span class="sxs-lookup"><span data-stu-id="29f52-160">7. Problem</span></span>
<span data-ttu-id="29f52-161">Ao registrar um gateway, talvez seja necessário inserir o caminho e a senha de um certificado.</span><span class="sxs-lookup"><span data-stu-id="29f52-161">When you're registering a gateway, you might need to enter path and password for a certificate.</span></span>

![Especificar certificado](media/data-factory-troubleshoot-gateway-issues/specify-certificate.png)

#### <a name="cause"></a><span data-ttu-id="29f52-163">Causa</span><span class="sxs-lookup"><span data-stu-id="29f52-163">Cause</span></span>
<span data-ttu-id="29f52-164">O gateway foi registrado antes em outros computadores.</span><span class="sxs-lookup"><span data-stu-id="29f52-164">The gateway has been registered on other machines before.</span></span> <span data-ttu-id="29f52-165">Durante o registro inicial de um gateway, um certificado de criptografia foi associado ao gateway.</span><span class="sxs-lookup"><span data-stu-id="29f52-165">During the initial registration of a gateway, an encryption certificate has been associated with the gateway.</span></span> <span data-ttu-id="29f52-166">O certificado pode ser gerado automaticamente pelo gateway ou fornecido pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="29f52-166">The certificate can either be self-generated by the gateway or provided by the user.</span></span>  <span data-ttu-id="29f52-167">Esse certificado é usado para criptografar as credenciais do armazenamento de dados (serviço vinculado).</span><span class="sxs-lookup"><span data-stu-id="29f52-167">This certificate is used to encrypt credentials of the data store (linked service).</span></span>  

![Exportar o certificado](media/data-factory-troubleshoot-gateway-issues/export-certificate.png)

<span data-ttu-id="29f52-169">Ao restaurar o gateway em um computador host diferente, o assistente de registro solicita que este certificado descriptografe as credenciais anteriormente criptografadas com esse certificado.</span><span class="sxs-lookup"><span data-stu-id="29f52-169">When restoring the gateway on a different host machine, the registration wizard asks for this certificate to decrypt credentials previously encrypted with this certificate.</span></span>  <span data-ttu-id="29f52-170">Sem esse certificado, as credenciais não poderão ser descriptografadas pelo novo gateway e as próximas execuções de atividade de cópia associadas a esse novo gateway falharão.</span><span class="sxs-lookup"><span data-stu-id="29f52-170">Without this certificate, the credentials cannot be decrypted by the new gateway and subsequent copy activity executions associated with this new gateway will fail.</span></span>  

#### <a name="resolution"></a><span data-ttu-id="29f52-171">Resolução</span><span class="sxs-lookup"><span data-stu-id="29f52-171">Resolution</span></span>
<span data-ttu-id="29f52-172">Se você exportou o certificado de credencial do computador do gateway original usando o botão **Exportar** na guia **Configurações** do Gerenciador de Configuração do Gateway de Gerenciamento de Dados, use o certificado aqui.</span><span class="sxs-lookup"><span data-stu-id="29f52-172">If you have exported the credential certificate from the original gateway machine by using the **Export** button on the **Settings** tab in Data Management Gateway Configuration Manager, use the certificate here.</span></span>

<span data-ttu-id="29f52-173">Não é possível ignorar este estágio ao recuperar um gateway.</span><span class="sxs-lookup"><span data-stu-id="29f52-173">You cannot skip this stage when recovering a gateway.</span></span> <span data-ttu-id="29f52-174">Se o certificado estiver ausente, você precisará excluir o gateway do portal e criar um novo gateway.</span><span class="sxs-lookup"><span data-stu-id="29f52-174">If the certificate is missing, you need to delete the gateway from the portal and re-create a new gateway.</span></span>  <span data-ttu-id="29f52-175">Além disso, todos os serviços vinculados relacionados ao gateway precisarão ser atualizados com a nova inserção das credenciais.</span><span class="sxs-lookup"><span data-stu-id="29f52-175">In addition, update all linked services that are related to the gateway by reentering their credentials.</span></span>

### <a name="8-problem"></a><span data-ttu-id="29f52-176">8. Problema</span><span class="sxs-lookup"><span data-stu-id="29f52-176">8. Problem</span></span>
<span data-ttu-id="29f52-177">A seguinte mensagem de erro poderá ser exibida.</span><span class="sxs-lookup"><span data-stu-id="29f52-177">You might see the following error message.</span></span>

`Error: The remote server returned an error: (407) Proxy Authentication Required.`

#### <a name="cause"></a><span data-ttu-id="29f52-178">Causa</span><span class="sxs-lookup"><span data-stu-id="29f52-178">Cause</span></span>
<span data-ttu-id="29f52-179">Esse erro ocorre quando o seu gateway está em um ambiente que requer um proxy HTTP para acessar recursos da Internet, ou quando a senha de autenticação do proxy é alterada, mas não é atualizada adequadamente em seu gateway.</span><span class="sxs-lookup"><span data-stu-id="29f52-179">This error happens when your gateway is in an environment that requires an HTTP proxy to access Internet resources, or your proxy's authentication password is changed but it's not updated accordingly in your gateway.</span></span>

#### <a name="resolution"></a><span data-ttu-id="29f52-180">Resolução</span><span class="sxs-lookup"><span data-stu-id="29f52-180">Resolution</span></span>
<span data-ttu-id="29f52-181">Siga as instruções na seção [Considerações sobre o servidor proxy](#proxy-server-considerations) neste artigo e defina as configurações de proxy com o Gerenciador de Configuração de Gateway de Gerenciamento de Dados.</span><span class="sxs-lookup"><span data-stu-id="29f52-181">Follow the instructions in the [Proxy server considerations](#proxy-server-considerations) section of this article, and configure proxy settings with Data Management Gateway Configuration Manager.</span></span>

## <a name="gateway-is-online-with-limited-functionality"></a><span data-ttu-id="29f52-182">O gateway está online com funcionalidade limitada</span><span class="sxs-lookup"><span data-stu-id="29f52-182">Gateway is online with limited functionality</span></span>
### <a name="1-problem"></a><span data-ttu-id="29f52-183">1. Problema</span><span class="sxs-lookup"><span data-stu-id="29f52-183">1. Problem</span></span>
<span data-ttu-id="29f52-184">O status do gateway é exibido como online com funcionalidade limitada.</span><span class="sxs-lookup"><span data-stu-id="29f52-184">You see the status of the gateway as online with limited functionality.</span></span>

#### <a name="cause"></a><span data-ttu-id="29f52-185">Causa</span><span class="sxs-lookup"><span data-stu-id="29f52-185">Cause</span></span>
<span data-ttu-id="29f52-186">Você vê o status do gateway como online com funcionalidade limitada por um dos seguintes motivos:</span><span class="sxs-lookup"><span data-stu-id="29f52-186">You see the status of the gateway as online with limited functionality for one of the following reasons:</span></span>

* <span data-ttu-id="29f52-187">O gateway não pode se conectar ao serviço de nuvem por meio do Barramento de Serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="29f52-187">Gateway cannot connect to cloud service through Azure Service Bus.</span></span>
* <span data-ttu-id="29f52-188">O serviço de nuvem não pode se conectar ao gateway por meio do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="29f52-188">Cloud service cannot connect to gateway through Service Bus.</span></span>

<span data-ttu-id="29f52-189">Quando o gateway está online com funcionalidade limitada, você não pode usar o Assistente de Cópia do Data Factory para criar pipelines de dados a fim de copiar dados de/para armazenamentos de dados locais.</span><span class="sxs-lookup"><span data-stu-id="29f52-189">When the gateway is online with limited functionality, you might not be able to use the Data Factory Copy Wizard to create data pipelines for copying data to or from on-premises data stores.</span></span> <span data-ttu-id="29f52-190">Como solução alternativa, você pode usar o Editor do Data Factory no Portal do Azure, no Visual Studio ou no Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="29f52-190">As a workaround, you can use Data Factory Editor in the portal, Visual Studio, or Azure PowerShell.</span></span>

#### <a name="resolution"></a><span data-ttu-id="29f52-191">Resolução</span><span class="sxs-lookup"><span data-stu-id="29f52-191">Resolution</span></span>
<span data-ttu-id="29f52-192">A resolução para esse problema (online com funcionalidade limitada) depende da causa: se é o gateway que não pode se conectar ao serviço de nuvem ou vice-versa.</span><span class="sxs-lookup"><span data-stu-id="29f52-192">Resolution for this issue (online with limited functionality) is based on whether the gateway cannot connect to the cloud service or the other way.</span></span> <span data-ttu-id="29f52-193">As seções a seguir fornecem essas resoluções.</span><span class="sxs-lookup"><span data-stu-id="29f52-193">The following sections provide these resolutions.</span></span>

### <a name="2-problem"></a><span data-ttu-id="29f52-194">2. Problema</span><span class="sxs-lookup"><span data-stu-id="29f52-194">2. Problem</span></span>
<span data-ttu-id="29f52-195">Você obtém o erro a seguir.</span><span class="sxs-lookup"><span data-stu-id="29f52-195">You see the following error.</span></span>

`Error: Gateway cannot connect to cloud service through service bus`

![O gateway não pode se conectar ao serviço de nuvem](media/data-factory-troubleshoot-gateway-issues/gateway-cannot-connect-to-cloud-service.png)

#### <a name="cause"></a><span data-ttu-id="29f52-197">Causa</span><span class="sxs-lookup"><span data-stu-id="29f52-197">Cause</span></span>
<span data-ttu-id="29f52-198">O gateway não pode se conectar ao serviço de nuvem por meio do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="29f52-198">Gateway cannot connect to the cloud service through Service Bus.</span></span>

#### <a name="resolution"></a><span data-ttu-id="29f52-199">Resolução</span><span class="sxs-lookup"><span data-stu-id="29f52-199">Resolution</span></span>
<span data-ttu-id="29f52-200">Siga estas etapas para colocar o gateway novamente online:</span><span class="sxs-lookup"><span data-stu-id="29f52-200">Follow these steps to get the gateway back online:</span></span>

1. <span data-ttu-id="29f52-201">Permita as regras de saída do endereço IP no computador do gateway e no firewall corporativo.</span><span class="sxs-lookup"><span data-stu-id="29f52-201">Allow IP address outbound rules on the gateway machine and the corporate firewall.</span></span> <span data-ttu-id="29f52-202">É possível encontrar endereços IP no Log de Eventos do Windows (ID = = 401): Tentativa de acessar um soquete de uma maneira proibida pelas permissões de acesso XX.XX.XX.XX:9350.</span><span class="sxs-lookup"><span data-stu-id="29f52-202">You can find IP addresses from the Windows Event Log (ID == 401): An attempt was made to access a socket in a way forbidden by its access permissions XX.XX.XX.XX:9350.</span></span>
* <span data-ttu-id="29f52-203">Defina as configurações de proxy no gateway.</span><span class="sxs-lookup"><span data-stu-id="29f52-203">Configure proxy settings on the gateway.</span></span> <span data-ttu-id="29f52-204">Consulte a seção [Considerações sobre servidor proxy](#proxy-server-considerations) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="29f52-204">See the [Proxy server considerations](#proxy-server-considerations) section for details.</span></span>
* <span data-ttu-id="29f52-205">Habilite as portas de saída 5671 e 9350 a 9354 no Firewall do Windows, no computador do gateway e no firewall corporativo.</span><span class="sxs-lookup"><span data-stu-id="29f52-205">Enable outbound ports 5671 and 9350-9354 on both the Windows Firewall on the gateway machine and the corporate firewall.</span></span> <span data-ttu-id="29f52-206">Consulte a seção [Portas e firewall](#ports-and-firewall) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="29f52-206">See the [Ports and firewall](#ports-and-firewall) section for details.</span></span> <span data-ttu-id="29f52-207">Esta etapa é opcional, mas recomendada devido a considerações sobre desempenho.</span><span class="sxs-lookup"><span data-stu-id="29f52-207">This step is optional, but we recommend it for performance consideration.</span></span>

### <a name="3-problem"></a><span data-ttu-id="29f52-208">3. Problema</span><span class="sxs-lookup"><span data-stu-id="29f52-208">3. Problem</span></span>
<span data-ttu-id="29f52-209">Você obtém o erro a seguir.</span><span class="sxs-lookup"><span data-stu-id="29f52-209">You see the following error.</span></span>

`Error: Cloud service cannot connect to gateway through service bus.`

#### <a name="cause"></a><span data-ttu-id="29f52-210">Causa</span><span class="sxs-lookup"><span data-stu-id="29f52-210">Cause</span></span>
<span data-ttu-id="29f52-211">Um erro transitório na conectividade de rede.</span><span class="sxs-lookup"><span data-stu-id="29f52-211">A transient error in network connectivity.</span></span>

#### <a name="resolution"></a><span data-ttu-id="29f52-212">Resolução</span><span class="sxs-lookup"><span data-stu-id="29f52-212">Resolution</span></span>
<span data-ttu-id="29f52-213">Siga estas etapas para colocar o gateway novamente online:</span><span class="sxs-lookup"><span data-stu-id="29f52-213">Follow these steps to get the gateway back online:</span></span>

1. <span data-ttu-id="29f52-214">Aguarde alguns minutos e a conectividade será recuperada automaticamente quando o erro for eliminado.</span><span class="sxs-lookup"><span data-stu-id="29f52-214">Wait for a couple of minutes, the connectivity will be automatically recovered when the error is gone.</span></span>
* <span data-ttu-id="29f52-215">Se o erro persistir, reinicie o serviço do gateway.</span><span class="sxs-lookup"><span data-stu-id="29f52-215">If the error persists, restart the gateway service.</span></span>

## <a name="failed-to-author-linked-service"></a><span data-ttu-id="29f52-216">Falha ao criar serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="29f52-216">Failed to author linked service</span></span>
### <a name="problem"></a><span data-ttu-id="29f52-217">Problema</span><span class="sxs-lookup"><span data-stu-id="29f52-217">Problem</span></span>
<span data-ttu-id="29f52-218">Esse erro poderá ser exibido ao tentar usar o Gerenciador de Credenciais no portal para inserir credenciais de um novo serviço vinculado ou ao atualizar as credenciais de um serviço vinculado existente.</span><span class="sxs-lookup"><span data-stu-id="29f52-218">You might see this error when you try to use Credential Manager in the portal to input credentials for a new linked service, or update credentials for an existing linked service.</span></span>

`Error: The data store '<Server>/<Database>' cannot be reached. Check connection settings for the data source.`

<span data-ttu-id="29f52-219">Ao ver esse erro, a página Configurações do Gerenciador de Configuração de Gateway de Gerenciamento de Dados pode parecer com a captura de tela a seguir.</span><span class="sxs-lookup"><span data-stu-id="29f52-219">When you see this error, the settings page of Data Management Gateway Configuration Manager might look like the following screenshot.</span></span>

![Não é possível acessar o banco de dados](media/data-factory-troubleshoot-gateway-issues/database-cannot-be-reached.png)

#### <a name="cause"></a><span data-ttu-id="29f52-221">Causa</span><span class="sxs-lookup"><span data-stu-id="29f52-221">Cause</span></span>
<span data-ttu-id="29f52-222">O certificado SSL pode ter sido perdido no computador do gateway.</span><span class="sxs-lookup"><span data-stu-id="29f52-222">The SSL certificate might have been lost on the gateway machine.</span></span> <span data-ttu-id="29f52-223">O gateway não pode carregar o certificado usado no momento para a criptografia SSL.</span><span class="sxs-lookup"><span data-stu-id="29f52-223">The gateway computer cannot load the certificate currently that is used for SSL encryption.</span></span> <span data-ttu-id="29f52-224">Você também pode ver uma mensagem de erro no log de eventos que é semelhante à seguinte mensagem.</span><span class="sxs-lookup"><span data-stu-id="29f52-224">You might also see an error message in the event log that is similar to the following message.</span></span>

 `Unable to get the gateway settings from cloud service. Check the gateway key and the network connection. (Certificate with thumbprint cannot be loaded.)`

#### <a name="resolution"></a><span data-ttu-id="29f52-225">Resolução</span><span class="sxs-lookup"><span data-stu-id="29f52-225">Resolution</span></span>
<span data-ttu-id="29f52-226">Siga estas etapas para resolver o problema:</span><span class="sxs-lookup"><span data-stu-id="29f52-226">Follow these steps to solve the problem:</span></span>

1. <span data-ttu-id="29f52-227">Inicie o Gerenciador de Configuração do Gateway de Gerenciamento de Dados.</span><span class="sxs-lookup"><span data-stu-id="29f52-227">Start Data Management Gateway Configuration Manager.</span></span>
2. <span data-ttu-id="29f52-228">Alterne para a guia **Configurações** .</span><span class="sxs-lookup"><span data-stu-id="29f52-228">Switch to the **Settings** tab.</span></span>  
3. <span data-ttu-id="29f52-229">Clique no botão **Alterar** para alterar o certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="29f52-229">Click the **Change** button to change the SSL certificate.</span></span>

   ![botão Alterar certificado](media/data-factory-troubleshoot-gateway-issues/change-button-ssl-certificate.png)
4. <span data-ttu-id="29f52-231">Selecione um novo certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="29f52-231">Select a new certificate as the SSL certificate.</span></span> <span data-ttu-id="29f52-232">Use qualquer certificado SSL gerado por você mesmo ou por qualquer organização.</span><span class="sxs-lookup"><span data-stu-id="29f52-232">You can use any SSL certificate that is generated by you or any organization.</span></span>

   ![Especificar certificado](media/data-factory-troubleshoot-gateway-issues/specify-http-end-point.png)

## <a name="copy-activity-fails"></a><span data-ttu-id="29f52-234">Falha na atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="29f52-234">Copy activity fails</span></span>
### <a name="problem"></a><span data-ttu-id="29f52-235">Problema</span><span class="sxs-lookup"><span data-stu-id="29f52-235">Problem</span></span>
<span data-ttu-id="29f52-236">Você observa a falha “UserErrorFailedToConnectToSqlserver” após configurar um pipeline no portal.</span><span class="sxs-lookup"><span data-stu-id="29f52-236">You might notice the following "UserErrorFailedToConnectToSqlserver" failure after you set up a pipeline in the portal.</span></span>

`Error: Copy activity encountered a user error: ErrorCode=UserErrorFailedToConnectToSqlServer,'Type=Microsoft.DataTransfer.Common.Shared.HybridDeliveryException,Message=Cannot connect to SQL Server`

#### <a name="cause"></a><span data-ttu-id="29f52-237">Causa</span><span class="sxs-lookup"><span data-stu-id="29f52-237">Cause</span></span>
<span data-ttu-id="29f52-238">Isso pode ocorrer por diferentes motivos e a mitigação varia de acordo.</span><span class="sxs-lookup"><span data-stu-id="29f52-238">This can happen for different reasons, and mitigation varies accordingly.</span></span>

#### <a name="resolution"></a><span data-ttu-id="29f52-239">Resolução</span><span class="sxs-lookup"><span data-stu-id="29f52-239">Resolution</span></span>
<span data-ttu-id="29f52-240">Permita conexões TCP de saída pela porta TCP/1433 no lado do cliente do Gateway de Gerenciamento de Dados antes de se conectar ao banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="29f52-240">Allow outbound TCP connections over port TCP/1433 on the Data Management Gateway client side before connecting to an SQL database.</span></span>

<span data-ttu-id="29f52-241">Se o banco de dados de destino for um banco de dados SQL do Azure, verifique também as configurações de firewall do SQL Server do Azure.</span><span class="sxs-lookup"><span data-stu-id="29f52-241">If the target database is an Azure SQL database, check SQL Server firewall settings for Azure as well.</span></span>

<span data-ttu-id="29f52-242">Consulte a seção a seguir para testar a conexão com o armazenamento de dados local.</span><span class="sxs-lookup"><span data-stu-id="29f52-242">See the following section to test the connection to the on-premises data store.</span></span>

## <a name="data-store-connection-or-driver-related-errors"></a><span data-ttu-id="29f52-243">Erro de conexão com o armazenamento de dados ou erros relacionados a drivers</span><span class="sxs-lookup"><span data-stu-id="29f52-243">Data store connection or driver-related errors</span></span>
<span data-ttu-id="29f52-244">Caso visualize erros relacionados ao driver ou à conexão com o repositório de dados, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="29f52-244">If you see data store connection or driver-related errors, complete the following steps:</span></span>

1. <span data-ttu-id="29f52-245">Inicie o Gerenciador de Configurações do Gateway de Gerenciamento de Dados no computador do gateway.</span><span class="sxs-lookup"><span data-stu-id="29f52-245">Start Data Management Gateway Configuration Manager on the gateway machine.</span></span>
2. <span data-ttu-id="29f52-246">Alterne para a guia **Diagnóstico** .</span><span class="sxs-lookup"><span data-stu-id="29f52-246">Switch to the **Diagnostics** tab.</span></span>
3. <span data-ttu-id="29f52-247">Em **Teste a conexão**, adicione os valores de grupo de gateway.</span><span class="sxs-lookup"><span data-stu-id="29f52-247">In **Test Connection**, add the gateway group values.</span></span>
4. <span data-ttu-id="29f52-248">Clique em **Testar** para verificar se você pode se conectar à fonte de dados local do computador do gateway usando as informações e credenciais de conexão.</span><span class="sxs-lookup"><span data-stu-id="29f52-248">Click **Test** to see if you can connect to the on-premises data source from the gateway machine by using the connection information and credentials.</span></span> <span data-ttu-id="29f52-249">Se a conexão de teste continuar falhando depois que você instalar um driver, reinicie o gateway para que ele assimile a alteração mais recente.</span><span class="sxs-lookup"><span data-stu-id="29f52-249">If the test connection still fails after you install a driver, restart the gateway for it to pick up the latest change.</span></span>

![Testar a conexão na guia Diagnóstico](media/data-factory-troubleshoot-gateway-issues/test-connection-in-diagnostics-tab.png)

## <a name="gateway-logs"></a><span data-ttu-id="29f52-251">Logs do gateway</span><span class="sxs-lookup"><span data-stu-id="29f52-251">Gateway logs</span></span>
### <a name="send-gateway-logs-to-microsoft"></a><span data-ttu-id="29f52-252">Enviar logs de gateway para a Microsoft</span><span class="sxs-lookup"><span data-stu-id="29f52-252">Send gateway logs to Microsoft</span></span>
<span data-ttu-id="29f52-253">Ao contatar o Suporte da Microsoft para obter ajuda com soluções de problemas de gateway, pode ser necessário compartilhar seus logs de gateway.</span><span class="sxs-lookup"><span data-stu-id="29f52-253">When you contact Microsoft Support to get help with troubleshooting gateway issues, you might be asked to share your gateway logs.</span></span> <span data-ttu-id="29f52-254">A versão do gateway permite que você compartilhe facilmente logs do gateway necessários por meio de dois cliques de botão no Gerenciador de Configuração de Gateway de Gerenciamento de Dados.</span><span class="sxs-lookup"><span data-stu-id="29f52-254">With the release of the gateway, you can share required gateway logs with two button clicks in Data Management Gateway Configuration Manager.</span></span>    

1. <span data-ttu-id="29f52-255">Alterne para a guia **Diagnóstico** no Gerenciador de Configuração de Gateway de Gerenciamento de Dados.</span><span class="sxs-lookup"><span data-stu-id="29f52-255">Switch to the **Diagnostics** tab in Data Management Gateway Configuration Manager.</span></span>

    ![Gateway de Gerenciamento de Dados - guia Diagnóstico](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-diagnostics-tab.png)
2. <span data-ttu-id="29f52-257">Clique em **Enviar logs** para ver a caixa de diálogo a seguir.</span><span class="sxs-lookup"><span data-stu-id="29f52-257">Click **Send Logs** to see the following dialog box.</span></span>

    ![Envio de logs do Gateway de Gerenciamento de Dados](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-dialog.png)
3. <span data-ttu-id="29f52-259">(opcional) Clique em **Exibir logs** para examinar logs no visualizador de eventos.</span><span class="sxs-lookup"><span data-stu-id="29f52-259">(Optional) Click **view logs** to review logs in the event viewer.</span></span>
4. <span data-ttu-id="29f52-260">(opcional) Clique em **Privacidade** para examinar a declaração de privacidade dos serviços Web da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="29f52-260">(Optional) Click **privacy** to review Microsoft web services privacy statement.</span></span>
5. <span data-ttu-id="29f52-261">Quando estiver satisfeito com o que está prestes a carregar, clique em **Enviar logs** para realmente enviar os logs dos últimos sete dias para a Microsoft a fim de solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="29f52-261">When you are satisfied with what you are about to upload, click **Send Logs** to actually send the logs from the last seven days to Microsoft for troubleshooting.</span></span> <span data-ttu-id="29f52-262">Você deve ver o status da operação send-logs conforme mostrado na imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="29f52-262">You should see the status of the send-logs operation as shown in the following screenshot.</span></span>

    ![Gateway de Gerenciamento de Dados – status de Enviar logs](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-status.png)
6. <span data-ttu-id="29f52-264">Quando a operação for concluída, você verá uma caixa de diálogo como mostrado na imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="29f52-264">After the operation is complete, you see a dialog box as shown in the following screenshot.</span></span>

    ![Gateway de Gerenciamento de Dados – status de Enviar logs](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-result.png)
7. <span data-ttu-id="29f52-266">Anote a **ID do relatório** e compartilhe-a com o Suporte da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="29f52-266">Save the **Report ID** and share it with Microsoft Support.</span></span> <span data-ttu-id="29f52-267">A ID do relatório é usada para localizar os logs de gateway carregados para a solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="29f52-267">The report ID is used to locate the gateway logs that you uploaded for troubleshooting.</span></span>  <span data-ttu-id="29f52-268">A ID do relatório também será salva no visualizador de eventos.</span><span class="sxs-lookup"><span data-stu-id="29f52-268">The report ID is also saved in the event viewer.</span></span>  <span data-ttu-id="29f52-269">Você pode encontrá-la ao observar a ID do evento "25" e verificar a data e a hora.</span><span class="sxs-lookup"><span data-stu-id="29f52-269">You can find it by looking at the event ID “25”, and check the date and time.</span></span>

    ![Gateway de Gerenciamento de Dados – ID de relatório de Enviar logs](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-report-id.png)    

### <a name="archive-gateway-logs-on-gateway-host-machine"></a><span data-ttu-id="29f52-271">Arquivar logs de gateway no computador host de gateway</span><span class="sxs-lookup"><span data-stu-id="29f52-271">Archive gateway logs on gateway host machine</span></span>
<span data-ttu-id="29f52-272">Existem alguns cenários em que há problemas de gateway e não é possível compartilhar logs do gateway diretamente:</span><span class="sxs-lookup"><span data-stu-id="29f52-272">There are some scenarios where you have gateway issues and you cannot share gateway logs directly:</span></span>

* <span data-ttu-id="29f52-273">Você instala manualmente o gateway e o registra.</span><span class="sxs-lookup"><span data-stu-id="29f52-273">You manually install the gateway and register the gateway.</span></span>
* <span data-ttu-id="29f52-274">Você tenta registrar o gateway com uma chave regenerada no Gerenciador de Configuração de Gateway de Gerenciamento de Dados.</span><span class="sxs-lookup"><span data-stu-id="29f52-274">You try to register the gateway with a regenerated key in Data Management Gateway Configuration Manager.</span></span>
* <span data-ttu-id="29f52-275">Você tenta enviar logs e o serviço de host do gateway não consegue se conectar.</span><span class="sxs-lookup"><span data-stu-id="29f52-275">You try to send logs and the gateway host service cannot be connected.</span></span>

<span data-ttu-id="29f52-276">Nesses casos, você pode salvar os logs de gateway como um arquivo zip e compartilhá-los quando contatar o suporte da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="29f52-276">For these scenarios, you can save gateway logs as a zip file and share it when you contact Microsoft support.</span></span> <span data-ttu-id="29f52-277">Por exemplo, se você receber um erro ao registrar o gateway, conforme mostrado na imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="29f52-277">For example, if you receive an error while you register the gateway as shown in the following screenshot.</span></span>   

![Gateway de Gerenciamento de Dados – Erro de registro](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-registration-error.png)

<span data-ttu-id="29f52-279">Clique no link **Arquivar logs de gateway** para arquivar e salvar os logs e compartilhar o arquivo zip com o suporte da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="29f52-279">Click the **Archive gateway logs** link to archive and save logs, and then share the zip file with Microsoft support.</span></span>

![Gateway de Gerenciamento de Dados - Arquivar logs](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-archive-logs.png)

### <a name="locate-gateway-logs"></a><span data-ttu-id="29f52-281">Localizar os logs do gateway</span><span class="sxs-lookup"><span data-stu-id="29f52-281">Locate gateway logs</span></span>
<span data-ttu-id="29f52-282">Você pode encontrar informações detalhadas sobre os logs de gateway nos logs de eventos do Windows.</span><span class="sxs-lookup"><span data-stu-id="29f52-282">You can find detailed gateway log information in the Windows event logs.</span></span>

1. <span data-ttu-id="29f52-283">Inicie o **Visualizador de eventos** do Windows.</span><span class="sxs-lookup"><span data-stu-id="29f52-283">Start Windows **Event Viewer**.</span></span>
2. <span data-ttu-id="29f52-284">Localize os logs na pasta **Logs de aplicativos e serviços** > **Gateway de Gerenciamento de Dados**.</span><span class="sxs-lookup"><span data-stu-id="29f52-284">Locate logs in the **Application and Services Logs** > **Data Management Gateway** folder.</span></span>

 <span data-ttu-id="29f52-285">Ao solucionar problemas relacionados ao gateway, procure eventos no nível de erro no visualizador.</span><span class="sxs-lookup"><span data-stu-id="29f52-285">When you're troubleshooting gateway-related issues, look for error level events in the event viewer.</span></span>

![Gateway de Gerenciamento de Dados – Logs no visualizador de eventos](media/data-factory-troubleshoot-gateway-issues/gateway-logs-event-viewer.png)
