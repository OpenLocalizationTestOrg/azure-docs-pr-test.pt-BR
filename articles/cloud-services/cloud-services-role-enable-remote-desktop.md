---
title: "aaaEnable área de trabalho remota em um serviço de nuvem do Azure | Microsoft Docs"
description: "Como tooconfigure do azure nuvem conexões de área de trabalho remota de tooallow aplicativo de serviço"
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: d3110ee8-6526-4585-aba5-d0bc9a713e9b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: b3c0180bf5ad29cb77e5303ccbd6f9ccc44b7b0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a><span data-ttu-id="f502a-103">Habilitar a conexão de Área de Trabalho Remota para uma função nos Serviços de Nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="f502a-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f502a-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f502a-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="f502a-105">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="f502a-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="f502a-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f502a-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="f502a-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f502a-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)

<span data-ttu-id="f502a-108">Você pode habilitar uma conexão de área de trabalho remota na sua função durante o desenvolvimento, incluindo módulos de área de trabalho remota de saudação em sua definição de serviço ou você pode escolher tooenable área de trabalho remota por meio de saudação extensão de área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="f502a-108">You can enable a Remote Desktop connection in your role during development by including hello Remote Desktop modules in your service definition or you can choose tooenable Remote Desktop through hello Remote Desktop Extension.</span></span> <span data-ttu-id="f502a-109">Olá abordagem preferencial é toouse Olá área de trabalho remota extensão como você pode habilitar área de trabalho remota, mesmo após a implantação do aplicativo hello sem ter que tooredeploy seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f502a-109">hello preferred approach is toouse hello Remote Desktop extension as you can enable Remote Desktop even after hello application is deployed without having tooredeploy your application.</span></span>

## <a name="configure-remote-desktop-from-hello-azure-classic-portal"></a><span data-ttu-id="f502a-110">Configurar área de trabalho remota a partir do hello portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="f502a-110">Configure Remote Desktop from hello Azure classic portal</span></span>
<span data-ttu-id="f502a-111">Olá portal clássico do Azure usa o método de extensão da área de trabalho remota de saudação para que você possa habilitar a área de trabalho remota mesmo após a implantação do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="f502a-111">hello Azure classic portal uses hello Remote Desktop Extension approach so you can enable Remote Desktop even after hello application is deployed.</span></span> <span data-ttu-id="f502a-112">Olá **configurar** página para seu serviço de nuvem permite que você tooenable área de trabalho remota, Olá alterar conta do administrador local usado tooconnect toohello VMs, certificado Olá usado na autenticação e defina Olá Data de expiração.</span><span class="sxs-lookup"><span data-stu-id="f502a-112">hello **Configure** page for your cloud service allows you tooenable Remote Desktop, change hello local Administrator account used tooconnect toohello virtual machines, hello certificate used in authentication and set hello expiration date.</span></span>

1. <span data-ttu-id="f502a-113">Clique em **serviços de nuvem**, clique em nome de Olá Olá do serviço de nuvem e, em seguida, clique em **configurar**.</span><span class="sxs-lookup"><span data-stu-id="f502a-113">Click **Cloud Services**, click hello name of hello cloud service, and then click **Configure**.</span></span>
2. <span data-ttu-id="f502a-114">Clique em Olá **remoto** botão na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="f502a-114">Click hello **Remote** button at hello bottom.</span></span>

    ![Serviços de nuvem remotos](./media/cloud-services-role-enable-remote-desktop/CloudServices_Remote.png)

   > [!WARNING]
   > <span data-ttu-id="f502a-116">Todas as instâncias de função serão reiniciadas quando você ativa área de trabalho remota pela primeira vez e clica em OK (marca de seleção).</span><span class="sxs-lookup"><span data-stu-id="f502a-116">All role instances will be restarted when you first enable Remote Desktop and click OK (checkmark).</span></span> <span data-ttu-id="f502a-117">tooprevent uma reinicialização, a senha de Olá Olá certificado tooencrypt usado deve ser instalado na função hello.</span><span class="sxs-lookup"><span data-stu-id="f502a-117">tooprevent a reboot, hello certificate used tooencrypt hello password must be installed on hello role.</span></span> <span data-ttu-id="f502a-118">tooprevent uma reinicialização, [carregar um certificado para o serviço de nuvem Olá](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) e, em seguida, retornar toothis caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f502a-118">tooprevent a restart, [upload a certificate for hello cloud service](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) and then return toothis dialog.</span></span>

3. <span data-ttu-id="f502a-119">Em **funções**, selecione função hello desejado tooupdate ou selecione **todos os** para todas as funções.</span><span class="sxs-lookup"><span data-stu-id="f502a-119">In **Roles**, select hello role you want tooupdate or select **All** for all roles.</span></span>
4. <span data-ttu-id="f502a-120">Faça uma saudação as seguintes alterações:</span><span class="sxs-lookup"><span data-stu-id="f502a-120">Make any of hello following changes:</span></span>

   * <span data-ttu-id="f502a-121">tooenable área de trabalho remota, selecione Olá **habilitar área de trabalho remota** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="f502a-121">tooenable Remote Desktop, select hello **Enable Remote Desktop** check box.</span></span> <span data-ttu-id="f502a-122">toodisable área de trabalho remota, caixa de seleção Limpar hello.</span><span class="sxs-lookup"><span data-stu-id="f502a-122">toodisable Remote Desktop, clear hello check box.</span></span>
   * <span data-ttu-id="f502a-123">Crie uma conta toouse em conexões de área de trabalho remota toohello instâncias de função.</span><span class="sxs-lookup"><span data-stu-id="f502a-123">Create an account toouse in Remote Desktop connections toohello role instances.</span></span>
   * <span data-ttu-id="f502a-124">Atualize a senha de saudação conta existente do hello.</span><span class="sxs-lookup"><span data-stu-id="f502a-124">Update hello password for hello existing account.</span></span>
   * <span data-ttu-id="f502a-125">Selecione um toouse certificado carregado para autenticação (carregamento Olá certificado usando **carregar** em Olá **certificados** página) ou criar um novo certificado.</span><span class="sxs-lookup"><span data-stu-id="f502a-125">Select an uploaded certificate toouse for authentication (upload hello certificate using **Upload** on hello **Certificates** page) or create a new certificate.</span></span>
   * <span data-ttu-id="f502a-126">Alterar a data de vencimento de saudação para configuração da área de trabalho remota de saudação.</span><span class="sxs-lookup"><span data-stu-id="f502a-126">Change hello expiration date for hello Remote Desktop configuration.</span></span>

5. <span data-ttu-id="f502a-127">Ao concluir as atualizações da configuração, clique em **OK** (marca de seleção).</span><span class="sxs-lookup"><span data-stu-id="f502a-127">When you finish your configuration updates, click **OK** (checkmark).</span></span>

## <a name="remote-into-role-instances"></a><span data-ttu-id="f502a-128">Remoto em instâncias de função</span><span class="sxs-lookup"><span data-stu-id="f502a-128">Remote into role instances</span></span>
<span data-ttu-id="f502a-129">Depois que a área de trabalho remota está habilitada em funções hello poderá remoto para uma instância de função por meio de várias ferramentas.</span><span class="sxs-lookup"><span data-stu-id="f502a-129">Once Remote Desktop is enabled on hello roles you can remote into a role instance through various tools.</span></span>

<span data-ttu-id="f502a-130">instância de função tooconnect tooa de saudação portal clássico do Azure:</span><span class="sxs-lookup"><span data-stu-id="f502a-130">tooconnect tooa role instance from hello Azure classic portal:</span></span>

1. <span data-ttu-id="f502a-131">Clique em **instâncias** tooopen Olá **instâncias** página.</span><span class="sxs-lookup"><span data-stu-id="f502a-131">Click **Instances** tooopen hello **Instances** page.</span></span>
2. <span data-ttu-id="f502a-132">Selecione uma instância de função com a área de trabalho remota configurada.</span><span class="sxs-lookup"><span data-stu-id="f502a-132">Select a role instance that has Remote Desktop configured.</span></span>
3. <span data-ttu-id="f502a-133">Clique em **conectar**e siga a área de trabalho da saudação tooopen Olá instruções.</span><span class="sxs-lookup"><span data-stu-id="f502a-133">Click **Connect**, and follow hello instructions tooopen hello desktop.</span></span>
4. <span data-ttu-id="f502a-134">Clique em **abrir** e **conectar** toostart Olá conexão de área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="f502a-134">Click **Open** and then **Connect** toostart hello Remote Desktop connection.</span></span>

### <a name="use-visual-studio-tooremote-into-a-role-instance"></a><span data-ttu-id="f502a-135">Use o Visual Studio tooremote em uma instância de função</span><span class="sxs-lookup"><span data-stu-id="f502a-135">Use Visual Studio tooremote into a role instance</span></span>
<span data-ttu-id="f502a-136">No Visual Studio, Gerenciador de Servidores:</span><span class="sxs-lookup"><span data-stu-id="f502a-136">In Visual Studio, Server Explorer:</span></span>

1. <span data-ttu-id="f502a-137">Expanda Olá **Azure** > **serviços de nuvem** > **[nome do serviço de nuvem]** nó.</span><span class="sxs-lookup"><span data-stu-id="f502a-137">Expand hello **Azure** > **Cloud Services** > **[cloud service name]** node.</span></span>
2. <span data-ttu-id="f502a-138">Expanda **Preparo** ou **Produção**.</span><span class="sxs-lookup"><span data-stu-id="f502a-138">Expand either **Staging** or **Production**.</span></span>
3. <span data-ttu-id="f502a-139">Expanda a função individual hello.</span><span class="sxs-lookup"><span data-stu-id="f502a-139">Expand hello individual role.</span></span>
4. <span data-ttu-id="f502a-140">Uma das instâncias de função hello, clique **conectar usando a área de trabalho remota...** e, em seguida, digite Olá nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="f502a-140">Right-click one of hello role instances, click **Connect using Remote Desktop...**, and then enter hello user name and password.</span></span>

![Área de trabalho remota do Gerenciador de Servidores](./media/cloud-services-role-enable-remote-desktop/ServerExplorer_RemoteDesktop.png)

### <a name="use-powershell-tooget-hello-rdp-file"></a><span data-ttu-id="f502a-142">Use o arquivo RDP do PowerShell tooget Olá</span><span class="sxs-lookup"><span data-stu-id="f502a-142">Use PowerShell tooget hello RDP file</span></span>
<span data-ttu-id="f502a-143">Você pode usar o hello [Get-AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) arquivo RDP do cmdlet tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="f502a-143">You can use hello [Get-AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) cmdlet tooretrieve hello RDP file.</span></span> <span data-ttu-id="f502a-144">Você pode usar o arquivo RDP de saudação com serviço de nuvem de saudação de tooaccess de Conexão de área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="f502a-144">You can then use hello RDP file with Remote Desktop Connection tooaccess hello cloud service.</span></span>

### <a name="programmatically-download-hello-rdp-file-through-hello-service-management-rest-api"></a><span data-ttu-id="f502a-145">Baixar o arquivo RDP de Olá por meio de saudação API de REST de gerenciamento de serviços programaticamente</span><span class="sxs-lookup"><span data-stu-id="f502a-145">Programmatically download hello RDP file through hello Service Management REST API</span></span>
<span data-ttu-id="f502a-146">Você pode usar o hello [Download RDP File](https://msdn.microsoft.com/library/jj157183.aspx) arquivo RDP do REST operação toodownload hello.</span><span class="sxs-lookup"><span data-stu-id="f502a-146">You can use hello [Download RDP File](https://msdn.microsoft.com/library/jj157183.aspx) REST operation toodownload hello RDP file.</span></span>

## <a name="tooconfigure-remote-desktop-in-hello-service-definition-file"></a><span data-ttu-id="f502a-147">tooconfigure área de trabalho remota no arquivo de definição de serviço Olá</span><span class="sxs-lookup"><span data-stu-id="f502a-147">tooconfigure Remote Desktop in hello service definition file</span></span>
<span data-ttu-id="f502a-148">Esse método permite que você tooenable área de trabalho remota para o aplicativo hello durante o desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="f502a-148">This method allows you tooenable Remote Desktop for hello application during development.</span></span> <span data-ttu-id="f502a-149">Essa abordagem requer senhas criptografadas armazenados em sua configuração de serviço de arquivo e qualquer configuração de área de trabalho remota do toohello atualizações exigem uma reimplantação do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="f502a-149">This approach requires encrypted passwords be stored in your service configuration file and any updates toohello remote desktop configuration would require a redeployment of hello application.</span></span> <span data-ttu-id="f502a-150">Se você quiser tooavoid essas desvantagens, você deve usar a extensão de área de trabalho remota Olá baseado abordagem descrita acima.</span><span class="sxs-lookup"><span data-stu-id="f502a-150">If you want tooavoid these downsides you should use hello remote desktop extension based approach described above.</span></span>  

<span data-ttu-id="f502a-151">Você pode usar o Visual Studio muito[habilitar uma conexão de área de trabalho remota](../vs-azure-tools-remote-desktop-roles.md) usando a abordagem de arquivo de definição de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="f502a-151">You can use Visual Studio too[enable a remote desktop connection](../vs-azure-tools-remote-desktop-roles.md) using hello service definition file approach.</span></span>  
<span data-ttu-id="f502a-152">Olá etapas a seguir descrevem Olá alterações necessárias toohello serviço modelo arquivos tooenable área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="f502a-152">hello steps below describe hello changes needed toohello service model files tooenable remote desktop.</span></span> <span data-ttu-id="f502a-153">O Visual Studio fará automaticamente essas alterações durante a publicação.</span><span class="sxs-lookup"><span data-stu-id="f502a-153">Visual Studio will automatically makes these changes when publishing.</span></span>

### <a name="set-up-hello-connection-in-hello-service-model"></a><span data-ttu-id="f502a-154">Configurar conexão Olá no modelo de serviço Olá</span><span class="sxs-lookup"><span data-stu-id="f502a-154">Set up hello connection in hello service model</span></span>
<span data-ttu-id="f502a-155">Saudação de uso **Imports** saudação do elemento tooimport **RemoteAccess** módulo e hello **RemoteForwarder** módulo toohello [servicedefinition. Csdef](cloud-services-model-and-package.md#csdef) arquivo.</span><span class="sxs-lookup"><span data-stu-id="f502a-155">Use hello **Imports** element tooimport hello **RemoteAccess** module and hello **RemoteForwarder** module toohello [ServiceDefinition.csdef](cloud-services-model-and-package.md#csdef) file.</span></span>

<span data-ttu-id="f502a-156">Olá arquivo de definição de serviço deve ser semelhante toohello seguinte exemplo com hello `<Imports>` elemento adicionado.</span><span class="sxs-lookup"><span data-stu-id="f502a-156">hello service definition file should be similar toohello following example with hello `<Imports>` element added.</span></span>

```xml
<ServiceDefinition name="<name-of-cloud-service>" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" schemaVersion="2013-03.2.0">
    <WebRole name="WebRole1" vmsize="Small">
        <Sites>
            <Site name="Web">
                <Bindings>
                    <Binding name="Endpoint1" endpointName="Endpoint1" />
                </Bindings>
            </Site>
        </Sites>
        <Endpoints>
            <InputEndpoint name="Endpoint1" protocol="http" port="80" />
        </Endpoints>
        <Imports>
            <Import moduleName="Diagnostics" />
            <Import moduleName="RemoteAccess" />
            <Import moduleName="RemoteForwarder" />
        </Imports>
    </WebRole>
</ServiceDefinition>
```
<span data-ttu-id="f502a-157">Olá [ServiceConfiguration](cloud-services-model-and-package.md#cscfg) arquivo deve ser semelhante toohello exemplo a seguir, observe Olá `<ConfigurationSettings>` e `<Certificates>` elementos.</span><span class="sxs-lookup"><span data-stu-id="f502a-157">hello [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#cscfg) file should be similar toohello following example, note hello `<ConfigurationSettings>` and `<Certificates>` elements.</span></span> <span data-ttu-id="f502a-158">Olá certificado especificado deve ser [carregado o serviço de nuvem toohello](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="f502a-158">hello Certificate specified must be [uploaded toohello cloud service](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceConfiguration serviceName="<name-of-cloud-service>" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="3" osVersion="*" schemaVersion="2013-03.2.0">
    <Role name="WebRole1">
        <Instances count="2" />
        <ConfigurationSettings>
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.Enabled" value="true" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountUsername" value="[name-of-user-account]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountEncryptedPassword" value="[base-64-encrypted-user-password]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountExpiration" value="[certificate-expiration]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteForwarder.Enabled" value="true" />
        </ConfigurationSettings>
        <Certificates>
            <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="[certificate-thumbprint]" thumbprintAlgorithm="sha1" />
        </Certificates>
    </Role>
</ServiceConfiguration>
```


## <a name="additional-resources"></a><span data-ttu-id="f502a-159">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="f502a-159">Additional Resources</span></span>
<span data-ttu-id="f502a-160">[Como tooConfigure serviços de nuvem](cloud-services-how-to-configure.md)
[serviços em nuvem perguntas Frequentes – área de trabalho remota](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="f502a-160">[How tooConfigure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
