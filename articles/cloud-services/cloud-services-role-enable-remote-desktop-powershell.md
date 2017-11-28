---
title: "Habilitar a Conexão de Área de Trabalho Remota para uma função nos serviços de nuvem do Azure usando o PowerShell"
description: "Como configurar seu aplicativo de serviço de nuvem do Azure usando o PowerShell para permitir conexões de área de trabalho remota"
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: bf2f70a4-20dc-4302-a91a-38cd7a2baa62
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 171f27c92ee9de14301ebb664e9ba3bcd98c394d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services-using-powershell"></a><span data-ttu-id="97cc3-103">Habilitar a Conexão de Área de Trabalho Remota para uma função nos serviços de nuvem do Azure usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="97cc3-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="97cc3-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="97cc3-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="97cc3-105">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="97cc3-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="97cc3-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="97cc3-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="97cc3-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="97cc3-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)
>
>

<span data-ttu-id="97cc3-108">A área de trabalho remota permite que você acesse a área de trabalho de uma função em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="97cc3-108">Remote Desktop enables you to access the desktop of a role running in Azure.</span></span> <span data-ttu-id="97cc3-109">Você pode usar a conexão da área de trabalho remota para solucionar e diagnosticar problemas com seu aplicativo durante a execução.</span><span class="sxs-lookup"><span data-stu-id="97cc3-109">You can use a Remote Desktop connection to troubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="97cc3-110">Este artigo descreve como habilitar a área de trabalho remota em suas funções de serviço de nuvem usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="97cc3-110">This article describes how to enable remote desktop on your Cloud Service Roles using PowerShell.</span></span> <span data-ttu-id="97cc3-111">Consulte [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview) para os pré-requisitos necessários para este artigo.</span><span class="sxs-lookup"><span data-stu-id="97cc3-111">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for the prerequisites needed for this article.</span></span> <span data-ttu-id="97cc3-112">O PowerShell usa a Extensão da Área de Trabalho Remota para que você possa habilitar a Área de Trabalho Remota depois que o aplicativo for implantado.</span><span class="sxs-lookup"><span data-stu-id="97cc3-112">PowerShell utilizes the Remote Desktop Extension so you can enable Remote Desktop after the application is deployed.</span></span>

## <a name="configure-remote-desktop-from-powershell"></a><span data-ttu-id="97cc3-113">Configurar a Área de Trabalho Remota por meio do PowerShell</span><span class="sxs-lookup"><span data-stu-id="97cc3-113">Configure Remote Desktop from PowerShell</span></span>
<span data-ttu-id="97cc3-114">O cmdlet [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) permite habilitar a Área de Trabalho Remota em funções especificadas ou todas as funções da implantação do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="97cc3-114">The [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet allows you to enable Remote Desktop on specified roles or all roles of your cloud service deployment.</span></span> <span data-ttu-id="97cc3-115">O cmdlet permite que você especifique o nome de usuário e a senha para o usuário da área de trabalho remota por meio do parâmetro *Credential* , que aceita um objeto PSCredential.</span><span class="sxs-lookup"><span data-stu-id="97cc3-115">The cmdlet lets you specify the Username and Password for the remote desktop user through the *Credential* parameter that accepts a PSCredential object.</span></span>

<span data-ttu-id="97cc3-116">Se estiver usando o PowerShell interativamente, você pode definir facilmente o objeto PSCredential chamando o cmdlet [Get-Credentials](https://technet.microsoft.com/library/hh849815.aspx) .</span><span class="sxs-lookup"><span data-stu-id="97cc3-116">If you are using PowerShell interactively, you can easily set the PSCredential object by calling the [Get-Credentials](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

```
$remoteusercredentials = Get-Credential
```

<span data-ttu-id="97cc3-117">Esse comando exibirá uma caixa de diálogo, permitindo que você insira o nome de usuário e a senha para o usuário remoto de modo seguro.</span><span class="sxs-lookup"><span data-stu-id="97cc3-117">This command displays a dialog box allowing you to enter the username and password for the remote user in a secure manner.</span></span>

<span data-ttu-id="97cc3-118">Já que o PowerShell ajuda em cenários de automação, você também pode configurar o objeto **PSCredential** de modo que não exija interação do usuário.</span><span class="sxs-lookup"><span data-stu-id="97cc3-118">Since PowerShell helps in automation scenarios, you can also set up the **PSCredential** object in a way that doesn't require user interaction.</span></span> <span data-ttu-id="97cc3-119">Primeiro, você precisa configurar uma senha de segurança.</span><span class="sxs-lookup"><span data-stu-id="97cc3-119">First, you need to set up a secure password.</span></span> <span data-ttu-id="97cc3-120">Comece com a especificação de uma senha de texto sem formatação e converta-a em uma cadeia de caracteres segura usando [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span><span class="sxs-lookup"><span data-stu-id="97cc3-120">You begin with specifying a plain text password convert it to a secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span> <span data-ttu-id="97cc3-121">Em seguida, você precisa converter essa cadeia de caracteres segura em uma cadeia de caracteres criptografada padrão usando [ConvertFrom-SecureString](https://technet.microsoft.com/library/hh849814.aspx).</span><span class="sxs-lookup"><span data-stu-id="97cc3-121">Next you need to convert this secure string into an encrypted standard string using [ConvertFrom-SecureString](https://technet.microsoft.com/library/hh849814.aspx).</span></span> <span data-ttu-id="97cc3-122">Agora você pode salvar essa cadeia de caracteres criptografada padrão em um arquivo, usando [Set-Content](https://technet.microsoft.com/library/ee176959.aspx).</span><span class="sxs-lookup"><span data-stu-id="97cc3-122">Now you can save this encrypted standard string to a file using [Set-Content](https://technet.microsoft.com/library/ee176959.aspx).</span></span>

<span data-ttu-id="97cc3-123">Você também pode criar um arquivo de senha segura para que não precise digitar a senha em todas as ocasiões.</span><span class="sxs-lookup"><span data-stu-id="97cc3-123">You can also create a secure password file so that you don't have to type in the password every time.</span></span> <span data-ttu-id="97cc3-124">Além disso, um arquivo de senha segura é melhor do que um arquivo de texto sem formatação.</span><span class="sxs-lookup"><span data-stu-id="97cc3-124">Also, a secure password file is better than a plain text file.</span></span> <span data-ttu-id="97cc3-125">Use o PowerShell a seguir para criar um arquivo de senha de segurança:</span><span class="sxs-lookup"><span data-stu-id="97cc3-125">Use the following PowerShell to create a secure password file:</span></span>

```
ConvertTo-SecureString -String "Password123" -AsPlainText -Force | ConvertFrom-SecureString | Set-Content "password.txt"
```

> [!IMPORTANT]
> <span data-ttu-id="97cc3-126">Ao definir a senha, atenda aos [requisitos de complexidade](https://technet.microsoft.com/library/cc786468.aspx).</span><span class="sxs-lookup"><span data-stu-id="97cc3-126">When setting the password, make sure that you meet the [complexity requirements](https://technet.microsoft.com/library/cc786468.aspx).</span></span>
>
>

<span data-ttu-id="97cc3-127">Para criar o objeto de credencial com base no arquivo de senha segura, você deve ler os conteúdos do arquivo e convertê-los novamente em uma cadeia de caracteres segura, usando [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span><span class="sxs-lookup"><span data-stu-id="97cc3-127">To create the credential object from the secure password file, you must read the file contents and convert them back to a secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span>

<span data-ttu-id="97cc3-128">O cmdlet [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) também aceita um parâmetro *Expiration* que especifica um **DateTime** (data e hora) em que a conta de usuário vai expirar.</span><span class="sxs-lookup"><span data-stu-id="97cc3-128">The [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet also accepts an *Expiration* parameter, which specifies a **DateTime** at which the user account expires.</span></span> <span data-ttu-id="97cc3-129">Por exemplo, você pode definir a conta a expirar em alguns dias após a data e hora atuais.</span><span class="sxs-lookup"><span data-stu-id="97cc3-129">For example, you could set the account to expire a few days from the current date and time.</span></span>

<span data-ttu-id="97cc3-130">Este PowerShell de exemplo mostra como definir a Extensão de Área de Trabalho Remota em um serviço de nuvem:</span><span class="sxs-lookup"><span data-stu-id="97cc3-130">This PowerShell example shows you how to set the Remote Desktop Extension on a cloud service:</span></span>

```
$servicename = "cloudservice"
$username = "RemoteDesktopUser"
$securepassword = Get-Content -Path "password.txt" | ConvertTo-SecureString
$expiry = $(Get-Date).AddDays(1)
$credential = New-Object System.Management.Automation.PSCredential $username,$securepassword
Set-AzureServiceRemoteDesktopExtension -ServiceName $servicename -Credential $credential -Expiration $expiry
```
<span data-ttu-id="97cc3-131">Você também pode especificar o slot de implantação e as funções em que deseja habilitar a área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="97cc3-131">You can also optionally specify the deployment slot and roles that you want to enable remote desktop on.</span></span> <span data-ttu-id="97cc3-132">Se esses parâmetros não forem especificados, o cmdlet habilitará a área de trabalho remota em todas as funções no slot de implantação de **Produção** .</span><span class="sxs-lookup"><span data-stu-id="97cc3-132">If these parameters are not specified, the cmdlet enables remote desktop on all roles in the **Production** deployment slot.</span></span>

<span data-ttu-id="97cc3-133">A extensão de Área de Trabalho Remota está associada uma implantação.</span><span class="sxs-lookup"><span data-stu-id="97cc3-133">The Remote Desktop extension is associated with a deployment.</span></span> <span data-ttu-id="97cc3-134">Se você criar uma nova implantação para o serviço, precisará habilitar novamente a área de trabalho remota nessa implantação.</span><span class="sxs-lookup"><span data-stu-id="97cc3-134">If you create a new deployment for the service, you have to enable remote desktop on that deployment.</span></span> <span data-ttu-id="97cc3-135">Se você sempre quiser ter a área de trabalho remota habilitada em suas implantações, deverá considerar a integração dos scripts do PowerShell em seu fluxo de trabalho de implantação.</span><span class="sxs-lookup"><span data-stu-id="97cc3-135">If you always want to have remote desktop enabled, then you should consider integrating the PowerShell scripts into your deployment workflow.</span></span>

## <a name="remote-desktop-into-a-role-instance"></a><span data-ttu-id="97cc3-136">Área de Trabalho Remota em uma instância de função</span><span class="sxs-lookup"><span data-stu-id="97cc3-136">Remote Desktop into a role instance</span></span>
<span data-ttu-id="97cc3-137">O cmdlet [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) é usado para a área de trabalho remota em uma instância de função específica do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="97cc3-137">The [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet is used to remote desktop into a specific role instance of your cloud service.</span></span> <span data-ttu-id="97cc3-138">Você pode usar o parâmetro *LocalPath* para baixar o arquivo RDP localmente.</span><span class="sxs-lookup"><span data-stu-id="97cc3-138">You can use the *LocalPath* parameter to download the RDP file locally.</span></span> <span data-ttu-id="97cc3-139">Ou você pode usar o parâmetro *Launch* para iniciar diretamente a caixa de diálogo Conexão de Área de Trabalho Remota para acessar a instância de função do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="97cc3-139">Or you can use the *Launch* parameter to directly launch the Remote Desktop Connection dialog to access the cloud service role instance.</span></span>

```
Get-AzureRemoteDesktopFile -ServiceName $servicename -Name "WorkerRole1_IN_0" -Launch
```


## <a name="check-if-remote-desktop-extension-is-enabled-on-a-service"></a><span data-ttu-id="97cc3-140">Verifique se a extensão de Área de Trabalho Remota está habilitada em um serviço</span><span class="sxs-lookup"><span data-stu-id="97cc3-140">Check if Remote Desktop extension is enabled on a service</span></span>
<span data-ttu-id="97cc3-141">O cmdlet [Get-AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) exibe se a área de trabalho remota está habilitada ou desabilitada em uma implantação de serviço.</span><span class="sxs-lookup"><span data-stu-id="97cc3-141">The [Get-AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet displays that remote desktop is enabled or disabled on a service deployment.</span></span> <span data-ttu-id="97cc3-142">O cmdlet retorna o nome de usuário para o usuário de área de trabalho remota e as funções nas quais a extensão de área de trabalho remota está habilitada.</span><span class="sxs-lookup"><span data-stu-id="97cc3-142">The cmdlet returns the username for the remote desktop user and the roles that the remote desktop extension is enabled for.</span></span> <span data-ttu-id="97cc3-143">Por padrão, isso ocorre no slot de implantação e você pode optar por usar o slot de preparo em vez disso.</span><span class="sxs-lookup"><span data-stu-id="97cc3-143">By default, this happens on the deployment slot and you can choose to use the staging slot instead.</span></span>

```
Get-AzureServiceRemoteDesktopExtension -ServiceName $servicename
```

## <a name="remove-remote-desktop-extension-from-a-service"></a><span data-ttu-id="97cc3-144">Remover a extensão de Área de Trabalho Remota de um serviço</span><span class="sxs-lookup"><span data-stu-id="97cc3-144">Remove Remote Desktop extension from a service</span></span>
<span data-ttu-id="97cc3-145">Se você já tiver habilitado a extensão de área de trabalho remota em uma implantação e se precisar atualizar as configurações de área de trabalho remota, primeiro remova a extensão.</span><span class="sxs-lookup"><span data-stu-id="97cc3-145">If you have already enabled the remote desktop extension on a deployment, and need to update the remote desktop settings, first remove the extension.</span></span> <span data-ttu-id="97cc3-146">E habilite-o novamente com as novas configurações.</span><span class="sxs-lookup"><span data-stu-id="97cc3-146">And enable it again with the new settings.</span></span> <span data-ttu-id="97cc3-147">Por exemplo, se você deseja definir uma nova senha para a conta de usuário remoto ou se a conta tiver expirado.</span><span class="sxs-lookup"><span data-stu-id="97cc3-147">For example, if you want to set a new password for the remote user account, or the account expired.</span></span> <span data-ttu-id="97cc3-148">Isso é necessário em implantações existentes com a extensão de área de trabalho remota habilitada.</span><span class="sxs-lookup"><span data-stu-id="97cc3-148">Doing this is required on existing deployments that have the remote desktop extension enabled.</span></span> <span data-ttu-id="97cc3-149">Para as novas implantações, você pode simplesmente aplicar a extensão de forma direta.</span><span class="sxs-lookup"><span data-stu-id="97cc3-149">For new deployments, you can simply apply the extension directly.</span></span>

<span data-ttu-id="97cc3-150">Para remover a extensão de área de trabalho remota de uma implantação, você poderá usar o cmdlet [Remove-AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) .</span><span class="sxs-lookup"><span data-stu-id="97cc3-150">To remove the remote desktop extension from the deployment, you can use the [Remove-AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet.</span></span> <span data-ttu-id="97cc3-151">Você também pode especificar o slot de implantação e a função dos quais você deseja remover a extensão da área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="97cc3-151">You can also optionally specify the deployment slot and role from which you want to remove the remote desktop extension.</span></span>

```
Remove-AzureServiceRemoteDesktopExtension -ServiceName $servicename -UninstallConfiguration
```

> [!NOTE]
> <span data-ttu-id="97cc3-152">Para remover completamente a configuração de extensão, você deve chamar o cmdlet *remove* com o parâmetro **UninstallConfiguration** .</span><span class="sxs-lookup"><span data-stu-id="97cc3-152">To completely remove the extension configuration, you should call the *remove* cmdlet with the **UninstallConfiguration** parameter.</span></span>
>
> <span data-ttu-id="97cc3-153">O parâmetro **UninstallConfiguration** desinstala qualquer configuração de extensão aplicada ao serviço.</span><span class="sxs-lookup"><span data-stu-id="97cc3-153">The **UninstallConfiguration** parameter uninstalls any extension configuration that is applied to the service.</span></span> <span data-ttu-id="97cc3-154">Todas as configurações de extensão estão associadas à configuração do serviço.</span><span class="sxs-lookup"><span data-stu-id="97cc3-154">Every extension configuration is associated with the service configuration.</span></span> <span data-ttu-id="97cc3-155">Chamar o cmdlet *remove* sem **UninstallConfiguration** dissocia a <mark>implantação</mark> da configuração de extensão, removendo assim efetivamente a extensão.</span><span class="sxs-lookup"><span data-stu-id="97cc3-155">Calling the *remove* cmdlet without **UninstallConfiguration** disassociates the <mark>deployment</mark> from the extension configuration, thus effectively removing the extension.</span></span> <span data-ttu-id="97cc3-156">No entanto, a configuração de extensão permanece associada ao serviço.</span><span class="sxs-lookup"><span data-stu-id="97cc3-156">However, the extension configuration remains associated with the service.</span></span>
>
>

## <a name="additional-resources"></a><span data-ttu-id="97cc3-157">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="97cc3-157">Additional resources</span></span>

<span data-ttu-id="97cc3-158">[Como configurar os Serviços de Nuvem](cloud-services-how-to-configure.md)
[Perguntas frequentes sobre os serviços de nuvem — Área de Trabalho Remota](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="97cc3-158">[How to Configure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
