---
title: "Habilitar Área de Trabalho Remota em um Serviço de Nuvem do Azure | Microsoft Docs"
description: "Como configurar seu aplicativo de serviço de nuvem do Azure para permitir conexões de área de trabalho remota"
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
ms.openlocfilehash: 413e72e9a39fcde84f56bfc61a6bc72dbadf1c97
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a><span data-ttu-id="48211-103">Habilitar a conexão de Área de Trabalho Remota para uma função nos Serviços de Nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="48211-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="48211-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="48211-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="48211-105">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="48211-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="48211-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="48211-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="48211-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="48211-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)

<span data-ttu-id="48211-108">Você pode habilitar uma conexão de Área de Trabalho Remota em sua função durante o desenvolvimento, incluindo os módulos de Área de Trabalho Remota em sua definição de serviço, ou você pode optar por habilitar a Área de Trabalho Remota por meio da Extensão de Área de Trabalho Remota.</span><span class="sxs-lookup"><span data-stu-id="48211-108">You can enable a Remote Desktop connection in your role during development by including the Remote Desktop modules in your service definition or you can choose to enable Remote Desktop through the Remote Desktop Extension.</span></span> <span data-ttu-id="48211-109">A abordagem preferida é usar a extensão de Área de Trabalho Remota, pois você poderá habilitar a Área de Trabalho Remota mesmo depois que o aplicativo for implantado, sem precisar reimplantar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="48211-109">The preferred approach is to use the Remote Desktop extension as you can enable Remote Desktop even after the application is deployed without having to redeploy your application.</span></span>

## <a name="configure-remote-desktop-from-the-azure-classic-portal"></a><span data-ttu-id="48211-110">Configurar a Área de Trabalho Remota do portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="48211-110">Configure Remote Desktop from the Azure classic portal</span></span>
<span data-ttu-id="48211-111">O portal clássico do Azure usa a abordagem da Extensão da Área de Trabalho Remota para que você possa habilitar a Área de Trabalho Remota, mesmo depois da implantação do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="48211-111">The Azure classic portal uses the Remote Desktop Extension approach so you can enable Remote Desktop even after the application is deployed.</span></span> <span data-ttu-id="48211-112">A página **Configurar** do seu Serviço de Nuvem permite habilitar a Área de Trabalho Remota, alterar a conta do administrador local usada para conexão às máquinas virtuais, o certificado usado na autenticação e definir a data de validade.</span><span class="sxs-lookup"><span data-stu-id="48211-112">The **Configure** page for your cloud service allows you to enable Remote Desktop, change the local Administrator account used to connect to the virtual machines, the certificate used in authentication and set the expiration date.</span></span>

1. <span data-ttu-id="48211-113">Clique em **Serviços de Nuvem**, no nome do serviço de nuvem e depois em **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="48211-113">Click **Cloud Services**, click the name of the cloud service, and then click **Configure**.</span></span>
2. <span data-ttu-id="48211-114">Clique no botão **Remover** na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="48211-114">Click the **Remote** button at the bottom.</span></span>

    ![Serviços de nuvem remotos](./media/cloud-services-role-enable-remote-desktop/CloudServices_Remote.png)

   > [!WARNING]
   > <span data-ttu-id="48211-116">Todas as instâncias de função serão reiniciadas quando você ativa área de trabalho remota pela primeira vez e clica em OK (marca de seleção).</span><span class="sxs-lookup"><span data-stu-id="48211-116">All role instances will be restarted when you first enable Remote Desktop and click OK (checkmark).</span></span> <span data-ttu-id="48211-117">Para evitar a reinicialização, o certificado usado para criptografar a senha deve estar instalado na função.</span><span class="sxs-lookup"><span data-stu-id="48211-117">To prevent a reboot, the certificate used to encrypt the password must be installed on the role.</span></span> <span data-ttu-id="48211-118">Para evitar uma reinicialização, [carregue um certificado para o serviço de nuvem](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) e retorne a esta caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="48211-118">To prevent a restart, [upload a certificate for the cloud service](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) and then return to this dialog.</span></span>

3. <span data-ttu-id="48211-119">Em **Funções**, selecione a função que você deseja atualizar ou selecione **Tudo** para todas as funções.</span><span class="sxs-lookup"><span data-stu-id="48211-119">In **Roles**, select the role you want to update or select **All** for all roles.</span></span>
4. <span data-ttu-id="48211-120">Faça algumas das seguintes alterações:</span><span class="sxs-lookup"><span data-stu-id="48211-120">Make any of the following changes:</span></span>

   * <span data-ttu-id="48211-121">Para habilitar a área de trabalho remota, marque a caixa de seleção de **Habilitar Área de Trabalho Remota** .</span><span class="sxs-lookup"><span data-stu-id="48211-121">To enable Remote Desktop, select the **Enable Remote Desktop** check box.</span></span> <span data-ttu-id="48211-122">Para desabilitar a área de trabalho remota, desmarque a caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="48211-122">To disable Remote Desktop, clear the check box.</span></span>
   * <span data-ttu-id="48211-123">Crie uma conta para usar nas conexões de área de trabalho remota para as instâncias de função.</span><span class="sxs-lookup"><span data-stu-id="48211-123">Create an account to use in Remote Desktop connections to the role instances.</span></span>
   * <span data-ttu-id="48211-124">Atualize a senha da conta existente.</span><span class="sxs-lookup"><span data-stu-id="48211-124">Update the password for the existing account.</span></span>
   * <span data-ttu-id="48211-125">Selecione um certificado carregado para usar para autenticação (carregue o certificado usando **Carregar** na página **Certificados**) ou crie um novo certificado.</span><span class="sxs-lookup"><span data-stu-id="48211-125">Select an uploaded certificate to use for authentication (upload the certificate using **Upload** on the **Certificates** page) or create a new certificate.</span></span>
   * <span data-ttu-id="48211-126">Altere a data de validade para a configuração da área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="48211-126">Change the expiration date for the Remote Desktop configuration.</span></span>

5. <span data-ttu-id="48211-127">Ao concluir as atualizações da configuração, clique em **OK** (marca de seleção).</span><span class="sxs-lookup"><span data-stu-id="48211-127">When you finish your configuration updates, click **OK** (checkmark).</span></span>

## <a name="remote-into-role-instances"></a><span data-ttu-id="48211-128">Remoto em instâncias de função</span><span class="sxs-lookup"><span data-stu-id="48211-128">Remote into role instances</span></span>
<span data-ttu-id="48211-129">Depois que a Área de Trabalho Remota estiver habilitada nas funções, você poderá conectar-se remotamente a uma instância de função por meio de várias ferramentas.</span><span class="sxs-lookup"><span data-stu-id="48211-129">Once Remote Desktop is enabled on the roles you can remote into a role instance through various tools.</span></span>

<span data-ttu-id="48211-130">Para conectar-se a uma instância de função do portal clássico do Azure:</span><span class="sxs-lookup"><span data-stu-id="48211-130">To connect to a role instance from the Azure classic portal:</span></span>

1. <span data-ttu-id="48211-131">Clique em **Instâncias** para abrir a página **Instâncias**.</span><span class="sxs-lookup"><span data-stu-id="48211-131">Click **Instances** to open the **Instances** page.</span></span>
2. <span data-ttu-id="48211-132">Selecione uma instância de função com a área de trabalho remota configurada.</span><span class="sxs-lookup"><span data-stu-id="48211-132">Select a role instance that has Remote Desktop configured.</span></span>
3. <span data-ttu-id="48211-133">Clique em **Conectar**e siga as instruções para abrir a área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="48211-133">Click **Connect**, and follow the instructions to open the desktop.</span></span>
4. <span data-ttu-id="48211-134">Clique em **Abrir** e em **Conectar** para iniciar a conexão de Área de Trabalho Remota.</span><span class="sxs-lookup"><span data-stu-id="48211-134">Click **Open** and then **Connect** to start the Remote Desktop connection.</span></span>

### <a name="use-visual-studio-to-remote-into-a-role-instance"></a><span data-ttu-id="48211-135">Use o Visual Studio para conectar-se remotamente a uma instância de função</span><span class="sxs-lookup"><span data-stu-id="48211-135">Use Visual Studio to remote into a role instance</span></span>
<span data-ttu-id="48211-136">No Visual Studio, Gerenciador de Servidores:</span><span class="sxs-lookup"><span data-stu-id="48211-136">In Visual Studio, Server Explorer:</span></span>

1. <span data-ttu-id="48211-137">Expanda o nó **Azure** > **Serviços de Nuvem** > **[nome do serviço de nuvem]**.</span><span class="sxs-lookup"><span data-stu-id="48211-137">Expand the **Azure** > **Cloud Services** > **[cloud service name]** node.</span></span>
2. <span data-ttu-id="48211-138">Expanda **Preparo** ou **Produção**.</span><span class="sxs-lookup"><span data-stu-id="48211-138">Expand either **Staging** or **Production**.</span></span>
3. <span data-ttu-id="48211-139">Expanda a função individual.</span><span class="sxs-lookup"><span data-stu-id="48211-139">Expand the individual role.</span></span>
4. <span data-ttu-id="48211-140">Clique em uma das instâncias de função, clique em **Conectar-se usando a Área de Trabalho Remota...**e insira o nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="48211-140">Right-click one of the role instances, click **Connect using Remote Desktop...**, and then enter the user name and password.</span></span>

![Área de trabalho remota do Gerenciador de Servidores](./media/cloud-services-role-enable-remote-desktop/ServerExplorer_RemoteDesktop.png)

### <a name="use-powershell-to-get-the-rdp-file"></a><span data-ttu-id="48211-142">Use o PowerShell para obter o arquivo RDP</span><span class="sxs-lookup"><span data-stu-id="48211-142">Use PowerShell to get the RDP file</span></span>
<span data-ttu-id="48211-143">Você pode usar o cmdlet [Get-AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) para recuperar o arquivo RDP.</span><span class="sxs-lookup"><span data-stu-id="48211-143">You can use the [Get-AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) cmdlet to retrieve the RDP file.</span></span> <span data-ttu-id="48211-144">Em seguida, você pode usar o arquivo RDP com a conexão de área de trabalho remota para acessar o serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="48211-144">You can then use the RDP file with Remote Desktop Connection to access the cloud service.</span></span>

### <a name="programmatically-download-the-rdp-file-through-the-service-management-rest-api"></a><span data-ttu-id="48211-145">Baixar programaticamente o arquivo RDP por meio da API REST do gerenciamento de serviços</span><span class="sxs-lookup"><span data-stu-id="48211-145">Programmatically download the RDP file through the Service Management REST API</span></span>
<span data-ttu-id="48211-146">Você pode usar a operação REST [Baixar arquivo RDP](https://msdn.microsoft.com/library/jj157183.aspx) para baixar o arquivo RDP.</span><span class="sxs-lookup"><span data-stu-id="48211-146">You can use the [Download RDP File](https://msdn.microsoft.com/library/jj157183.aspx) REST operation to download the RDP file.</span></span>

## <a name="to-configure-remote-desktop-in-the-service-definition-file"></a><span data-ttu-id="48211-147">Para configurar a Área de Trabalho Remota no novo arquivo de definição de serviço</span><span class="sxs-lookup"><span data-stu-id="48211-147">To configure Remote Desktop in the service definition file</span></span>
<span data-ttu-id="48211-148">Esse método permite habilitar a Área de Trabalho Remota para o aplicativo durante o desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="48211-148">This method allows you to enable Remote Desktop for the application during development.</span></span> <span data-ttu-id="48211-149">Essa abordagem requer que senhas criptografadas sejam armazenadas em seu arquivo de configuração de serviço e todas as atualizações na configuração de Área de Trabalho Remota exigiriam uma reimplantação do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="48211-149">This approach requires encrypted passwords be stored in your service configuration file and any updates to the remote desktop configuration would require a redeployment of the application.</span></span> <span data-ttu-id="48211-150">Se você quiser evitar essas desvantagens, use a abordagem com base em extensão da Área de Trabalho Remota descrita acima.</span><span class="sxs-lookup"><span data-stu-id="48211-150">If you want to avoid these downsides you should use the remote desktop extension based approach described above.</span></span>  

<span data-ttu-id="48211-151">Você pode usar o Visual Studio para [habilitar uma conexão de Área de Trabalho Remota](../vs-azure-tools-remote-desktop-roles.md) usando a abordagem de arquivo de definição de serviço.</span><span class="sxs-lookup"><span data-stu-id="48211-151">You can use Visual Studio to [enable a remote desktop connection](../vs-azure-tools-remote-desktop-roles.md) using the service definition file approach.</span></span>  
<span data-ttu-id="48211-152">As etapas a seguir descrevem as alterações necessárias para os arquivos de modelo de serviço habilitarem a Área de Trabalho Remota.</span><span class="sxs-lookup"><span data-stu-id="48211-152">The steps below describe the changes needed to the service model files to enable remote desktop.</span></span> <span data-ttu-id="48211-153">O Visual Studio fará automaticamente essas alterações durante a publicação.</span><span class="sxs-lookup"><span data-stu-id="48211-153">Visual Studio will automatically makes these changes when publishing.</span></span>

### <a name="set-up-the-connection-in-the-service-model"></a><span data-ttu-id="48211-154">Configurar a conexão no modelo de serviço</span><span class="sxs-lookup"><span data-stu-id="48211-154">Set up the connection in the service model</span></span>
<span data-ttu-id="48211-155">Use o elemento **Imports** para importar o módulo **RemoteAccess** e o módulo **RemoteForwarder** para o arquivo [ServiceDefinition.csdef](cloud-services-model-and-package.md#csdef).</span><span class="sxs-lookup"><span data-stu-id="48211-155">Use the **Imports** element to import the **RemoteAccess** module and the **RemoteForwarder** module to the [ServiceDefinition.csdef](cloud-services-model-and-package.md#csdef) file.</span></span>

<span data-ttu-id="48211-156">O arquivo de definição de serviço deve ser semelhante ao exemplo a seguir com o elemento `<Imports>` adicionado.</span><span class="sxs-lookup"><span data-stu-id="48211-156">The service definition file should be similar to the following example with the `<Imports>` element added.</span></span>

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
<span data-ttu-id="48211-157">O arquivo [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#cscfg) deve ser semelhante ao exemplo a seguir, observe os elementos `<ConfigurationSettings>` e `<Certificates>`.</span><span class="sxs-lookup"><span data-stu-id="48211-157">The [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#cscfg) file should be similar to the following example, note the `<ConfigurationSettings>` and `<Certificates>` elements.</span></span> <span data-ttu-id="48211-158">O certificado especificado deve ser [carregado no serviço de nuvem](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="48211-158">The Certificate specified must be [uploaded to the cloud service](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service).</span></span>

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


## <a name="additional-resources"></a><span data-ttu-id="48211-159">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="48211-159">Additional Resources</span></span>
<span data-ttu-id="48211-160">[Como configurar os Serviços de Nuvem](cloud-services-how-to-configure.md)
[Perguntas frequentes sobre os serviços de nuvem — Área de Trabalho Remota](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="48211-160">[How to Configure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
