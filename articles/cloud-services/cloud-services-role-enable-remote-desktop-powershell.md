---
title: "aaaEnable Conexão de área de trabalho remota para uma função nos serviços de nuvem do Azure usando o PowerShell"
description: "Como tooconfigure do azure nuvem usando conexões de área de trabalho remota do PowerShell tooallow do aplicativo de serviço"
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
ms.openlocfilehash: 3f46b014f29f1c0be0e1b485d2f0152424162bb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services-using-powershell"></a><span data-ttu-id="64291-103">Habilitar a Conexão de Área de Trabalho Remota para uma função nos serviços de nuvem do Azure usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="64291-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="64291-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="64291-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="64291-105">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="64291-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="64291-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="64291-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="64291-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="64291-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)
>
>

<span data-ttu-id="64291-108">Área de trabalho remota permite que você tooaccess área de trabalho de saudação de uma função em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="64291-108">Remote Desktop enables you tooaccess hello desktop of a role running in Azure.</span></span> <span data-ttu-id="64291-109">Você pode usar um tootroubleshoot de conexão de área de trabalho remota e diagnosticar problemas com seu aplicativo enquanto ele está em execução.</span><span class="sxs-lookup"><span data-stu-id="64291-109">You can use a Remote Desktop connection tootroubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="64291-110">Este artigo descreve como tooenable área de trabalho remota em suas funções de serviço de nuvem usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="64291-110">This article describes how tooenable remote desktop on your Cloud Service Roles using PowerShell.</span></span> <span data-ttu-id="64291-111">Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) pré-requisitos Olá necessários para este artigo.</span><span class="sxs-lookup"><span data-stu-id="64291-111">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for hello prerequisites needed for this article.</span></span> <span data-ttu-id="64291-112">PowerShell utiliza Olá extensão de área de trabalho remota para que você possa habilitar a área de trabalho remota após a implantação do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="64291-112">PowerShell utilizes hello Remote Desktop Extension so you can enable Remote Desktop after hello application is deployed.</span></span>

## <a name="configure-remote-desktop-from-powershell"></a><span data-ttu-id="64291-113">Configurar a Área de Trabalho Remota por meio do PowerShell</span><span class="sxs-lookup"><span data-stu-id="64291-113">Configure Remote Desktop from PowerShell</span></span>
<span data-ttu-id="64291-114">Olá [AzureServiceRemoteDesktopExtension conjunto](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet permite tooenable área de trabalho remota em funções especificadas ou todas as funções de sua implantação do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="64291-114">hello [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet allows you tooenable Remote Desktop on specified roles or all roles of your cloud service deployment.</span></span> <span data-ttu-id="64291-115">Olá cmdlet permite que você especifique hello nome de usuário e senha de usuário de desktop remoto Olá por meio de saudação *credencial* parâmetro que aceita um objeto PSCredential.</span><span class="sxs-lookup"><span data-stu-id="64291-115">hello cmdlet lets you specify hello Username and Password for hello remote desktop user through hello *Credential* parameter that accepts a PSCredential object.</span></span>

<span data-ttu-id="64291-116">Se você estiver usando o PowerShell interativamente, você pode definir facilmente objeto PSCredential de saudação por chamada hello [Get-credenciais](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="64291-116">If you are using PowerShell interactively, you can easily set hello PSCredential object by calling hello [Get-Credentials](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

```
$remoteusercredentials = Get-Credential
```

<span data-ttu-id="64291-117">Este comando exibe uma caixa de diálogo que permite a você tooenter Olá nome de usuário e senha do usuário remoto Olá de forma segura.</span><span class="sxs-lookup"><span data-stu-id="64291-117">This command displays a dialog box allowing you tooenter hello username and password for hello remote user in a secure manner.</span></span>

<span data-ttu-id="64291-118">Desde que o PowerShell Ajuda em cenários de automação, você também pode configurar Olá **PSCredential** objeto de forma que não exige interação do usuário.</span><span class="sxs-lookup"><span data-stu-id="64291-118">Since PowerShell helps in automation scenarios, you can also set up hello **PSCredential** object in a way that doesn't require user interaction.</span></span> <span data-ttu-id="64291-119">Primeiro, é necessário tooset uma senha segura.</span><span class="sxs-lookup"><span data-stu-id="64291-119">First, you need tooset up a secure password.</span></span> <span data-ttu-id="64291-120">Começar com a especificação de uma senha de texto sem formatação convertê-lo a cadeia de caracteres segura tooa usando [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span><span class="sxs-lookup"><span data-stu-id="64291-120">You begin with specifying a plain text password convert it tooa secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span> <span data-ttu-id="64291-121">Em seguida você precisa tooconvert essa cadeia de caracteres segura em uma cadeia de caracteres criptografada padrão usando [ConvertFrom-SecureString](https://technet.microsoft.com/library/hh849814.aspx).</span><span class="sxs-lookup"><span data-stu-id="64291-121">Next you need tooconvert this secure string into an encrypted standard string using [ConvertFrom-SecureString](https://technet.microsoft.com/library/hh849814.aspx).</span></span> <span data-ttu-id="64291-122">Agora você pode salvar esse arquivo de tooa de cadeia de caracteres criptografada padrão usando [Set-Content](https://technet.microsoft.com/library/ee176959.aspx).</span><span class="sxs-lookup"><span data-stu-id="64291-122">Now you can save this encrypted standard string tooa file using [Set-Content](https://technet.microsoft.com/library/ee176959.aspx).</span></span>

<span data-ttu-id="64291-123">Você também pode criar um arquivo de senha segura para que você não tenha tootype senha Olá sempre.</span><span class="sxs-lookup"><span data-stu-id="64291-123">You can also create a secure password file so that you don't have tootype in hello password every time.</span></span> <span data-ttu-id="64291-124">Além disso, um arquivo de senha segura é melhor do que um arquivo de texto sem formatação.</span><span class="sxs-lookup"><span data-stu-id="64291-124">Also, a secure password file is better than a plain text file.</span></span> <span data-ttu-id="64291-125">Use Olá PowerShell toocreate um arquivo de senha de segurança a seguir:</span><span class="sxs-lookup"><span data-stu-id="64291-125">Use hello following PowerShell toocreate a secure password file:</span></span>

```
ConvertTo-SecureString -String "Password123" -AsPlainText -Force | ConvertFrom-SecureString | Set-Content "password.txt"
```

> [!IMPORTANT]
> <span data-ttu-id="64291-126">Ao definir senha Olá, certifique-se de que você atenda aos Olá [requisitos de complexidade](https://technet.microsoft.com/library/cc786468.aspx).</span><span class="sxs-lookup"><span data-stu-id="64291-126">When setting hello password, make sure that you meet hello [complexity requirements](https://technet.microsoft.com/library/cc786468.aspx).</span></span>
>
>

<span data-ttu-id="64291-127">objeto de credencial toocreate saudação do arquivo de senha segura hello, você deve ler o conteúdo do arquivo hello e convertê-los tooa back proteger a cadeia de caracteres usando [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span><span class="sxs-lookup"><span data-stu-id="64291-127">toocreate hello credential object from hello secure password file, you must read hello file contents and convert them back tooa secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span>

<span data-ttu-id="64291-128">Olá [conjunto AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet também aceita um *validade* parâmetro, que especifica um **DateTime** nos quais o usuário Olá vencimento da conta.</span><span class="sxs-lookup"><span data-stu-id="64291-128">hello [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet also accepts an *Expiration* parameter, which specifies a **DateTime** at which hello user account expires.</span></span> <span data-ttu-id="64291-129">Por exemplo, você pode definir Olá conta tooexpire alguns dias da saudação data e hora atuais.</span><span class="sxs-lookup"><span data-stu-id="64291-129">For example, you could set hello account tooexpire a few days from hello current date and time.</span></span>

<span data-ttu-id="64291-130">Este exemplo do PowerShell mostra como tooset Olá extensão de área de trabalho remota em um serviço de nuvem:</span><span class="sxs-lookup"><span data-stu-id="64291-130">This PowerShell example shows you how tooset hello Remote Desktop Extension on a cloud service:</span></span>

```
$servicename = "cloudservice"
$username = "RemoteDesktopUser"
$securepassword = Get-Content -Path "password.txt" | ConvertTo-SecureString
$expiry = $(Get-Date).AddDays(1)
$credential = New-Object System.Management.Automation.PSCredential $username,$securepassword
Set-AzureServiceRemoteDesktopExtension -ServiceName $servicename -Credential $credential -Expiration $expiry
```
<span data-ttu-id="64291-131">Você também pode especificar slot de implantação hello e funções que você deseja tooenable área de trabalho remota no.</span><span class="sxs-lookup"><span data-stu-id="64291-131">You can also optionally specify hello deployment slot and roles that you want tooenable remote desktop on.</span></span> <span data-ttu-id="64291-132">Se esses parâmetros não forem especificados, Olá habilita a área de trabalho remota em todas as funções hello **produção** slot de implantação.</span><span class="sxs-lookup"><span data-stu-id="64291-132">If these parameters are not specified, hello cmdlet enables remote desktop on all roles in hello **Production** deployment slot.</span></span>

<span data-ttu-id="64291-133">Olá extensão da área de trabalho remota está associado uma implantação.</span><span class="sxs-lookup"><span data-stu-id="64291-133">hello Remote Desktop extension is associated with a deployment.</span></span> <span data-ttu-id="64291-134">Se você criar uma nova implantação do serviço de hello, você tem a área de trabalho remota tooenable em que a implantação.</span><span class="sxs-lookup"><span data-stu-id="64291-134">If you create a new deployment for hello service, you have tooenable remote desktop on that deployment.</span></span> <span data-ttu-id="64291-135">Se você desejar toohave área de trabalho remota habilitada, você deve considerar a integração de scripts do PowerShell Olá ao seu fluxo de trabalho de implantação.</span><span class="sxs-lookup"><span data-stu-id="64291-135">If you always want toohave remote desktop enabled, then you should consider integrating hello PowerShell scripts into your deployment workflow.</span></span>

## <a name="remote-desktop-into-a-role-instance"></a><span data-ttu-id="64291-136">Área de Trabalho Remota em uma instância de função</span><span class="sxs-lookup"><span data-stu-id="64291-136">Remote Desktop into a role instance</span></span>
<span data-ttu-id="64291-137">Olá [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet é usado tooremote a área de trabalho em uma instância de função específica do seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="64291-137">hello [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet is used tooremote desktop into a specific role instance of your cloud service.</span></span> <span data-ttu-id="64291-138">Você pode usar o hello *LocalPath* Olá toodownload de parâmetro RDP arquivo localmente.</span><span class="sxs-lookup"><span data-stu-id="64291-138">You can use hello *LocalPath* parameter toodownload hello RDP file locally.</span></span> <span data-ttu-id="64291-139">Ou você pode usar o hello *iniciar* tooaccess de caixa de diálogo de Conexão de área de trabalho remota parâmetro toodirectly inicialização Olá Olá instância de função do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="64291-139">Or you can use hello *Launch* parameter toodirectly launch hello Remote Desktop Connection dialog tooaccess hello cloud service role instance.</span></span>

```
Get-AzureRemoteDesktopFile -ServiceName $servicename -Name "WorkerRole1_IN_0" -Launch
```


## <a name="check-if-remote-desktop-extension-is-enabled-on-a-service"></a><span data-ttu-id="64291-140">Verifique se a extensão de Área de Trabalho Remota está habilitada em um serviço</span><span class="sxs-lookup"><span data-stu-id="64291-140">Check if Remote Desktop extension is enabled on a service</span></span>
<span data-ttu-id="64291-141">Olá [AzureServiceRemoteDesktopExtension Get](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet exibe que área de trabalho remota está habilitada ou desabilitada em uma implantação de serviço.</span><span class="sxs-lookup"><span data-stu-id="64291-141">hello [Get-AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet displays that remote desktop is enabled or disabled on a service deployment.</span></span> <span data-ttu-id="64291-142">Olá cmdlet retorna o nome de usuário de saudação de usuário da área de trabalho remota hello e funções Olá Olá extensão de área de trabalho remota está habilitada para.</span><span class="sxs-lookup"><span data-stu-id="64291-142">hello cmdlet returns hello username for hello remote desktop user and hello roles that hello remote desktop extension is enabled for.</span></span> <span data-ttu-id="64291-143">Por padrão, isso ocorre no slot de implantação hello e você pode escolher Olá toouse em vez disso, o slot de preparo.</span><span class="sxs-lookup"><span data-stu-id="64291-143">By default, this happens on hello deployment slot and you can choose toouse hello staging slot instead.</span></span>

```
Get-AzureServiceRemoteDesktopExtension -ServiceName $servicename
```

## <a name="remove-remote-desktop-extension-from-a-service"></a><span data-ttu-id="64291-144">Remover a extensão de Área de Trabalho Remota de um serviço</span><span class="sxs-lookup"><span data-stu-id="64291-144">Remove Remote Desktop extension from a service</span></span>
<span data-ttu-id="64291-145">Se você tiver habilitado a extensão de área de trabalho remota Olá em uma implantação e precisa tooupdate Olá configurações de área de trabalho remota, primeiro remova a extensão hello.</span><span class="sxs-lookup"><span data-stu-id="64291-145">If you have already enabled hello remote desktop extension on a deployment, and need tooupdate hello remote desktop settings, first remove hello extension.</span></span> <span data-ttu-id="64291-146">E habilitá-lo novamente com novas configurações de saudação.</span><span class="sxs-lookup"><span data-stu-id="64291-146">And enable it again with hello new settings.</span></span> <span data-ttu-id="64291-147">Por exemplo, se você quiser tooset uma nova senha para a conta de usuário remoto hello ou Olá conta expirou.</span><span class="sxs-lookup"><span data-stu-id="64291-147">For example, if you want tooset a new password for hello remote user account, or hello account expired.</span></span> <span data-ttu-id="64291-148">Isso é necessário nas implantações existentes que têm Olá extensão da área de trabalho remota habilitada.</span><span class="sxs-lookup"><span data-stu-id="64291-148">Doing this is required on existing deployments that have hello remote desktop extension enabled.</span></span> <span data-ttu-id="64291-149">Para novas implantações, você pode simplesmente aplicar extensão Olá diretamente.</span><span class="sxs-lookup"><span data-stu-id="64291-149">For new deployments, you can simply apply hello extension directly.</span></span>

<span data-ttu-id="64291-150">tooremove Olá remoto da área de trabalho extensão da implantação hello, você pode usar o hello [AzureServiceRemoteDesktopExtension remover](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="64291-150">tooremove hello remote desktop extension from hello deployment, you can use hello [Remove-AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet.</span></span> <span data-ttu-id="64291-151">Você pode especificar também slot de implantação de saudação e a função da qual você deseja que a extensão da área de trabalho remota do tooremove Olá.</span><span class="sxs-lookup"><span data-stu-id="64291-151">You can also optionally specify hello deployment slot and role from which you want tooremove hello remote desktop extension.</span></span>

```
Remove-AzureServiceRemoteDesktopExtension -ServiceName $servicename -UninstallConfiguration
```

> [!NOTE]
> <span data-ttu-id="64291-152">configuração de extensão do toocompletely remover hello, você deve chamar hello *remover* cmdlet com hello **UninstallConfiguration** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="64291-152">toocompletely remove hello extension configuration, you should call hello *remove* cmdlet with hello **UninstallConfiguration** parameter.</span></span>
>
> <span data-ttu-id="64291-153">Olá **UninstallConfiguration** parâmetro desinstala qualquer configuração de extensão que é o serviço toohello aplicado.</span><span class="sxs-lookup"><span data-stu-id="64291-153">hello **UninstallConfiguration** parameter uninstalls any extension configuration that is applied toohello service.</span></span> <span data-ttu-id="64291-154">Todas as configurações de extensão está associada a configuração do serviço hello.</span><span class="sxs-lookup"><span data-stu-id="64291-154">Every extension configuration is associated with hello service configuration.</span></span> <span data-ttu-id="64291-155">Olá chamada *remover* cmdlet sem **UninstallConfiguration** desassocia Olá <mark>implantação</mark> da configuração de extensão hello, assim, removendo efetivamente extensão de saudação.</span><span class="sxs-lookup"><span data-stu-id="64291-155">Calling hello *remove* cmdlet without **UninstallConfiguration** disassociates hello <mark>deployment</mark> from hello extension configuration, thus effectively removing hello extension.</span></span> <span data-ttu-id="64291-156">No entanto, a configuração da extensão Olá permanece associada ao serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="64291-156">However, hello extension configuration remains associated with hello service.</span></span>
>
>

## <a name="additional-resources"></a><span data-ttu-id="64291-157">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="64291-157">Additional resources</span></span>

<span data-ttu-id="64291-158">[Como tooConfigure serviços de nuvem](cloud-services-how-to-configure.md)
[serviços em nuvem perguntas Frequentes – área de trabalho remota](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="64291-158">[How tooConfigure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
