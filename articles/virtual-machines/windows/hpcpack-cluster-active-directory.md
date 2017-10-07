---
title: aaaHPC pacote de cluster com o Active Directory do Azure | Microsoft Docs
description: Saiba como toointegrate uma 2016 do HPC Pack cluster no Azure com o Active Directory do Azure
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
ms.assetid: 9edf9559-db02-438b-8268-a6cba7b5c8b7
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 11/14/2016
ms.author: danlep
ms.openlocfilehash: 0806e544a468e27ca0567e18c55554811584fbc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-hpc-pack-cluster-in-azure-using-azure-active-directory"></a><span data-ttu-id="e188a-103">Gerenciar um cluster HPC Pack no Azure usando o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e188a-103">Manage an HPC Pack cluster in Azure using Azure Active Directory</span></span>
<span data-ttu-id="e188a-104">O [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) dá suporte à integração com o [Azure AD](../../active-directory/index.md) (Azure Active Directory) para administradores que implantam um cluster HPC Pack no Azure.</span><span class="sxs-lookup"><span data-stu-id="e188a-104">[Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) supports integration with [Azure Active Directory](../../active-directory/index.md) (Azure AD) for administrators who deploy an HPC Pack cluster in Azure.</span></span>



<span data-ttu-id="e188a-105">Siga as etapas de saudação neste artigo para as seguintes tarefas de nível alto de saudação:</span><span class="sxs-lookup"><span data-stu-id="e188a-105">Follow hello steps in this article for hello following high level tasks:</span></span> 
* <span data-ttu-id="e188a-106">Integrar manualmente o cluster HPC Pack ao locatário do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e188a-106">Manually integrate your HPC Pack cluster with your Azure AD tenant</span></span>
* <span data-ttu-id="e188a-107">Gerenciar e agendar trabalhos no cluster HPC Pack no Azure</span><span class="sxs-lookup"><span data-stu-id="e188a-107">Manage and schedule jobs in your HPC Pack cluster in Azure</span></span> 

<span data-ttu-id="e188a-108">Integrar uma solução de cluster de HPC Pack com o Azure AD segue as etapas padrão toointegrate outros aplicativos e serviços.</span><span class="sxs-lookup"><span data-stu-id="e188a-108">Integrating an HPC Pack cluster solution with Azure AD follows standard steps toointegrate other applications and services.</span></span> <span data-ttu-id="e188a-109">Este artigo pressupõe que você esteja familiarizado com o gerenciamento básico de usuários no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e188a-109">This article assumes you are familiar with basic user management in Azure AD.</span></span> <span data-ttu-id="e188a-110">Para obter mais informações e em segundo plano, consulte Olá [documentação do Active Directory do Azure](../../active-directory/index.md) e Olá seção a seguir.</span><span class="sxs-lookup"><span data-stu-id="e188a-110">For more information and background, see hello [Azure Active Directory documentation](../../active-directory/index.md) and hello following section.</span></span>

## <a name="benefits-of-integration"></a><span data-ttu-id="e188a-111">Vantagens da integração</span><span class="sxs-lookup"><span data-stu-id="e188a-111">Benefits of integration</span></span>


<span data-ttu-id="e188a-112">Azure Active Directory (AD do Azure) é um multilocatário baseado em nuvem identidades e diretórios serviço de gerenciamento que fornece acesso de logon único (SSO) toocloud soluções.</span><span class="sxs-lookup"><span data-stu-id="e188a-112">Azure Active Directory (Azure AD) is a multi-tenant cloud-based directory and identity management service that provides single sign-on (SSO) access toocloud solutions.</span></span>

<span data-ttu-id="e188a-113">Integração de um cluster de HPC Pack com o Azure AD pode ajudá-lo a atingir Olá seguintes metas:</span><span class="sxs-lookup"><span data-stu-id="e188a-113">Integration of an HPC Pack cluster with Azure AD can help you achieve hello following goals:</span></span>

* <span data-ttu-id="e188a-114">Remova controlador de domínio do Active Directory tradicional de saudação do cluster de HPC Pack hello.</span><span class="sxs-lookup"><span data-stu-id="e188a-114">Remove hello traditional Active Directory domain controller from hello HPC Pack cluster.</span></span> <span data-ttu-id="e188a-115">Isso pode ajudar a reduzir os custos de saudação de manutenção de cluster Olá se isso não é necessário para sua empresa e o processo de implantação de saudação acelerar.</span><span class="sxs-lookup"><span data-stu-id="e188a-115">This can help reduce hello costs of maintaining hello cluster if this is not necessary for your business, and speed-up hello deployment process.</span></span>
* <span data-ttu-id="e188a-116">Aproveitar Olá benefícios que são colocados pelo AD do Azure a seguir:</span><span class="sxs-lookup"><span data-stu-id="e188a-116">Leverage hello following benefits that are brought by Azure AD:</span></span>
    *   <span data-ttu-id="e188a-117">Logon único</span><span class="sxs-lookup"><span data-stu-id="e188a-117">Single sign-on</span></span> 
    *   <span data-ttu-id="e188a-118">Usando uma identidade do AD local para o cluster de HPC Pack Olá no Azure</span><span class="sxs-lookup"><span data-stu-id="e188a-118">Using a local AD identity for hello HPC Pack cluster in Azure</span></span> 

    ![Ambiente do Azure Active Directory](./media/hpcpack-cluster-active-directory/aad.png)


## <a name="prerequisites"></a><span data-ttu-id="e188a-120">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e188a-120">Prerequisites</span></span>
* <span data-ttu-id="e188a-121">**Cluster HPC Pack 2016 implantado em máquinas virtuais do Azure** - para obter as etapas, confira [Implantar um cluster HPC Pack 2016 no Azure](hpcpack-2016-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="e188a-121">**HPC Pack 2016 cluster deployed in Azure virtual machines** - For steps, see [Deploy an HPC Pack 2016 cluster in Azure](hpcpack-2016-cluster.md).</span></span> <span data-ttu-id="e188a-122">Você precisa nome DNS de saudação do nó principal hello e credenciais de saudação de um administrador de cluster para concluir as etapas neste artigo hello.</span><span class="sxs-lookup"><span data-stu-id="e188a-122">You need hello DNS name of hello head node and hello credentials of a cluster administrator to complete hello steps in this article.</span></span>

  > [!NOTE]
  > <span data-ttu-id="e188a-123">Não há suporte à integração do Azure Active Directory nas versões do HPC Pack anteriores ao HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="e188a-123">Azure Active Directory integration is not supported in versions of HPC Pack before HPC Pack 2016.</span></span>



* <span data-ttu-id="e188a-124">**Computador cliente** -você precisa de um Windows ou Windows Server cliente computador executado muito HPC Pack utilitários de cliente.</span><span class="sxs-lookup"><span data-stu-id="e188a-124">**Client computer** - You need a Windows or Windows Server client computer too run HPC Pack client utilities.</span></span> <span data-ttu-id="e188a-125">Se você desejar somente toouse Olá HPC Pack portal web ou trabalhos de toosubmit da API REST, você pode usar qualquer computador cliente de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="e188a-125">If you only want toouse hello HPC Pack web portal or REST API toosubmit jobs, you can use any client computer of your choice.</span></span>

* <span data-ttu-id="e188a-126">**Utilitários de cliente do HPC Pack** -instalar utilitários de cliente do HPC Pack Olá no computador do cliente hello, usando o pacote de instalação gratuita Olá disponível da saudação Microsoft Download Center.</span><span class="sxs-lookup"><span data-stu-id="e188a-126">**HPC Pack client utilities** - Install hello HPC Pack client utilities on hello client computer, using hello free installation package available from hello Microsoft Download Center.</span></span>


## <a name="step-1-register-hello-hpc-cluster-server-with-your-azure-ad-tenant"></a><span data-ttu-id="e188a-127">Etapa 1: Registrar o servidor de cluster HPC Olá com seu locatário do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e188a-127">Step 1: Register hello HPC cluster server with your Azure AD tenant</span></span>
1. <span data-ttu-id="e188a-128">Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="e188a-128">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="e188a-129">Clique em **do Active Directory** em Olá menus à esquerda e clique em diretório desejado de saudação em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="e188a-129">Click **Active Directory** in hello left menu, and then click hello desired directory in your subscription.</span></span> <span data-ttu-id="e188a-130">Você deve ter recursos de tooaccess de permissão no diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="e188a-130">You must have permission tooaccess resources in hello directory.</span></span>
3. <span data-ttu-id="e188a-131">Clique em **Usuários** e verifique se há contas de usuário já criadas ou configuradas.</span><span class="sxs-lookup"><span data-stu-id="e188a-131">Click **Users**, and make sure there are user accounts already created or configured.</span></span>
4. <span data-ttu-id="e188a-132">Clique em **Aplicativos** > **Adicionar** e clique em **Adicionar um aplicativo que minha organização está desenvolvendo**.</span><span class="sxs-lookup"><span data-stu-id="e188a-132">Click **Applications** > **Add**, and then click **Add an application my organization is developing**.</span></span> <span data-ttu-id="e188a-133">Digite hello informações no Assistente de saudação a seguir:</span><span class="sxs-lookup"><span data-stu-id="e188a-133">Enter hello following information in hello wizard:</span></span>
    * <span data-ttu-id="e188a-134">**Nome** - HPCPackClusterServer</span><span class="sxs-lookup"><span data-stu-id="e188a-134">**Name** - HPCPackClusterServer</span></span>
    * <span data-ttu-id="e188a-135">**Tipo** - selecione **Aplicativo Web e/ou API Web**</span><span class="sxs-lookup"><span data-stu-id="e188a-135">**Type** - Select **Web Application and/or Web API**</span></span>
    * <span data-ttu-id="e188a-136">**URL de logon**- Olá URL base para o exemplo hello, por padrão`https://hpcserver`</span><span class="sxs-lookup"><span data-stu-id="e188a-136">**Sign-on URL**- hello base URL for hello sample, which is by default `https://hpcserver`</span></span>
    * <span data-ttu-id="e188a-137">**URI da ID do aplicativo** - `https://<Directory_name>/<application_name>`.</span><span class="sxs-lookup"><span data-stu-id="e188a-137">**App ID URI** - `https://<Directory_name>/<application_name>`.</span></span> <span data-ttu-id="e188a-138">Substituir `<Directory_name`> com hello nome completo do seu locatário do AD do Azure, por exemplo, `hpclocal.onmicrosoft.com`e substitua `<application_name>` com nome hello escolhido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e188a-138">Replace `<Directory_name`> with hello full name of your Azure AD tenant, for example, `hpclocal.onmicrosoft.com`, and replace `<application_name>` with hello name you chose previously.</span></span>

5. <span data-ttu-id="e188a-139">Depois que o aplicativo hello foi adicionado, clique em **configurar**.</span><span class="sxs-lookup"><span data-stu-id="e188a-139">After hello app is added, click **Configure**.</span></span> <span data-ttu-id="e188a-140">Configure Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="e188a-140">Configure hello following properties:</span></span>
    * <span data-ttu-id="e188a-141">Selecione **Sim** para **O aplicativo é multilocatário**</span><span class="sxs-lookup"><span data-stu-id="e188a-141">Select **Yes** for **Application is multi-tenant**</span></span>
    * <span data-ttu-id="e188a-142">Selecione **Sim** para **usuário atribuição necessário tooaccess aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="e188a-142">Select **Yes** for **User assignment required tooaccess app**.</span></span>

6. <span data-ttu-id="e188a-143">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="e188a-143">Click **Save**.</span></span> <span data-ttu-id="e188a-144">Quando o salvamento for concluído, clique em **Gerenciar Manifesto**.</span><span class="sxs-lookup"><span data-stu-id="e188a-144">When saving completes, click **Manage Manifest**.</span></span> <span data-ttu-id="e188a-145">Essa ação baixa o arquivo de JavaScript Object Notation (JSON).</span><span class="sxs-lookup"><span data-stu-id="e188a-145">This action downloads your application’s manifest JavaScript object notation (JSON) file.</span></span> <span data-ttu-id="e188a-146">Editar saudação baixado manifesto Localizando Olá `appRoles` definindo e adicionando Olá função de aplicativo a seguir:</span><span class="sxs-lookup"><span data-stu-id="e188a-146">Edit hello downloaded manifest by locating hello `appRoles` setting and adding hello following application role:</span></span>
    ```json
    "appRoles": [
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "displayName": "HpcAdminMirror",
        "id": "61e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "description": "HpcAdminMirror",
        "value": "HpcAdminMirror"
        },
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "description": "HpcUsers",
        "displayName": "HpcUsers",
        "id": "91e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "value": "HpcUsers"
        }
    ],
    ```
7. <span data-ttu-id="e188a-147">Salve o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="e188a-147">Save hello file.</span></span> <span data-ttu-id="e188a-148">No portal de saudação, clique em **gerenciar manifesto** > **carregar manifesto**.</span><span class="sxs-lookup"><span data-stu-id="e188a-148">Then in hello portal, click **Manage Manifest** > **Upload Manifest**.</span></span> <span data-ttu-id="e188a-149">Em seguida, você pode carregar manifesto editado hello.</span><span class="sxs-lookup"><span data-stu-id="e188a-149">You can then upload hello edited manifest.</span></span>
8. <span data-ttu-id="e188a-150">Clique em **Usuários**, selecione um usuário e clique em **Atribuir**.</span><span class="sxs-lookup"><span data-stu-id="e188a-150">Click **Users**, select a user, and then click **Assign**.</span></span> <span data-ttu-id="e188a-151">Atribua um usuário de toohello Olá funções disponíveis (HpcUsers ou HpcAdminMirror).</span><span class="sxs-lookup"><span data-stu-id="e188a-151">Assign one of hello available roles (HpcUsers or HpcAdminMirror) toohello user.</span></span> <span data-ttu-id="e188a-152">Repita essa etapa com outros usuários no diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="e188a-152">Repeat this step with additional users in hello directory.</span></span> <span data-ttu-id="e188a-153">Para obter informações sobre os usuários de cluster, confira [Gerenciar usuários de cluster](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx).</span><span class="sxs-lookup"><span data-stu-id="e188a-153">For background information about cluster users, see [Managing Cluster Users](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx).</span></span>

   > [!NOTE] 
   > <span data-ttu-id="e188a-154">toomanage usuários, é recomendável usar folha de visualização do Azure Active Directory Olá em Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e188a-154">toomanage users, we recommend using hello Azure Active Directory preview blade in hello [Azure portal](https://portal.azure.com).</span></span>
   >


## <a name="step-2-register-hello-hpc-cluster-client-with-your-azure-ad-tenant"></a><span data-ttu-id="e188a-155">Etapa 2: Registrar o cliente de cluster HPC Olá com seu locatário do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e188a-155">Step 2: Register hello HPC cluster client with your Azure AD tenant</span></span>

1. <span data-ttu-id="e188a-156">Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="e188a-156">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="e188a-157">Clique em **do Active Directory** em Olá menus à esquerda e clique em diretório desejado de saudação em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="e188a-157">Click **Active Directory** in hello left menu, and then click hello desired directory in your subscription.</span></span> <span data-ttu-id="e188a-158">Você deve ter recursos de tooaccess de permissão no diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="e188a-158">You must have permission tooaccess resources in hello directory.</span></span>
3. <span data-ttu-id="e188a-159">Clique em **Aplicativos** > **Adicionar** e clique em **Adicionar um aplicativo que minha organização está desenvolvendo**.</span><span class="sxs-lookup"><span data-stu-id="e188a-159">Click **Applications** > **Add**, and then click **Add an application my organization is developing**.</span></span> <span data-ttu-id="e188a-160">Digite hello informações no Assistente de saudação a seguir:</span><span class="sxs-lookup"><span data-stu-id="e188a-160">Enter hello following information in hello wizard:</span></span>

    * <span data-ttu-id="e188a-161">**Nome** - HPCPackClusterClient</span><span class="sxs-lookup"><span data-stu-id="e188a-161">**Name** - HPCPackClusterClient</span></span>
    * <span data-ttu-id="e188a-162">**Tipo** – selecione **Aplicativo Cliente Nativo**</span><span class="sxs-lookup"><span data-stu-id="e188a-162">**Type** - Select **Native Client Application**</span></span>
    * <span data-ttu-id="e188a-163">**URI de redirecionamento** - `http://hpcclient`</span><span class="sxs-lookup"><span data-stu-id="e188a-163">**Redirect URI** - `http://hpcclient`</span></span>

4. <span data-ttu-id="e188a-164">Depois que o aplicativo hello foi adicionado, clique em **configurar**.</span><span class="sxs-lookup"><span data-stu-id="e188a-164">After hello app is added, click **Configure**.</span></span> <span data-ttu-id="e188a-165">Saudação de cópia **ID do cliente** valor e salve-o.</span><span class="sxs-lookup"><span data-stu-id="e188a-165">Copy hello **Client ID** value and save it.</span></span> <span data-ttu-id="e188a-166">Você precisará dele mais tarde ao configurar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e188a-166">You need this later when configuring your application.</span></span>

5. <span data-ttu-id="e188a-167">Em **permissões tooother aplicativos**, clique em **Adicionar aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="e188a-167">In **Permissions tooother applications**, click **Add Application**.</span></span> <span data-ttu-id="e188a-168">Pesquisar e adicionar o aplicativo de HpcPackClusterServer hello (criado na etapa 1).</span><span class="sxs-lookup"><span data-stu-id="e188a-168">Search and add hello  HpcPackClusterServer application (created in Step 1).</span></span>

6. <span data-ttu-id="e188a-169">Em Olá **permissões delegadas** lista suspensa, selecione **HpcClusterServer acesso**.</span><span class="sxs-lookup"><span data-stu-id="e188a-169">In hello **Delegated Permissions** dropdown, select **Access HpcClusterServer**.</span></span> <span data-ttu-id="e188a-170">Em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="e188a-170">Then click **Save**.</span></span>


## <a name="step-3-configure-hello-hpc-cluster"></a><span data-ttu-id="e188a-171">Etapa 3: Configurar o cluster HPC Olá</span><span class="sxs-lookup"><span data-stu-id="e188a-171">Step 3: Configure hello HPC cluster</span></span>

1. <span data-ttu-id="e188a-172">Conecte-se toohello HPC Pack 2016 o nó principal no Azure.</span><span class="sxs-lookup"><span data-stu-id="e188a-172">Connect toohello HPC Pack 2016 head node in Azure.</span></span>

2. <span data-ttu-id="e188a-173">Inicie o HPC PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e188a-173">Start HPC PowerShell.</span></span>

3. <span data-ttu-id="e188a-174">Execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e188a-174">Run hello following command:</span></span>

    ```powershell

    Set-HpcClusterRegistry -SupportAAD true -AADInstance https://login.microsoftonline.com/ -AADAppName HpcClusterServer -AADTenant <your AAD tenant name> -AADClientAppId <client ID> -AADClientAppRedirectUri http://hpcclient
    ```
    <span data-ttu-id="e188a-175">onde</span><span class="sxs-lookup"><span data-stu-id="e188a-175">where</span></span>

    * <span data-ttu-id="e188a-176">`AADTenant`Especifica o nome do locatário do AD do Azure hello, como`hpclocal.onmicrosoft.com`</span><span class="sxs-lookup"><span data-stu-id="e188a-176">`AADTenant` specifies hello Azure AD tenant name, such as `hpclocal.onmicrosoft.com`</span></span>
    * <span data-ttu-id="e188a-177">`AADClientAppId`Especifica a ID do cliente Olá para o aplicativo hello criado na etapa 2.</span><span class="sxs-lookup"><span data-stu-id="e188a-177">`AADClientAppId` specifies hello client ID for hello app created in Step 2.</span></span>

4. <span data-ttu-id="e188a-178">Reinicie o serviço de HpcSchedulerStateful hello.</span><span class="sxs-lookup"><span data-stu-id="e188a-178">Restart hello HpcSchedulerStateful service.</span></span>

    <span data-ttu-id="e188a-179">Em um cluster com vários nós de cabeçalho, você pode executar Olá comandos do PowerShell a seguir na Olá nó principal tooswitch Olá réplica primária para o serviço de HpcSchedulerStateful hello:</span><span class="sxs-lookup"><span data-stu-id="e188a-179">In a cluster with multiple head nodes, you can run hello following PowerShell commands on hello head node tooswitch hello primary replica for hello HpcSchedulerStateful service:</span></span>

    ```powershell
    Connect-ServiceFabricCluster

    Move-ServiceFabricPrimaryReplica –ServiceName “fabric:/HpcApplication/SchedulerStatefulService”

    ```

## <a name="step-4-manage-and-submit-jobs-from-hello-client"></a><span data-ttu-id="e188a-180">Etapa 4: Gerenciar e enviar trabalhos de cliente Olá</span><span class="sxs-lookup"><span data-stu-id="e188a-180">Step 4: Manage and submit jobs from hello client</span></span>

<span data-ttu-id="e188a-181">utilitários de cliente tooinstall Olá HPC Pack em seu computador, baixe os arquivos de instalação HPC Pack 2016 (instalação completa) de saudação Microsoft Download Center.</span><span class="sxs-lookup"><span data-stu-id="e188a-181">tooinstall hello HPC Pack client utilities on your computer, download the HPC Pack 2016 setup files (full installation) from hello Microsoft Download Center.</span></span> <span data-ttu-id="e188a-182">Quando você começar a instalação hello, escolha a opção de instalação de saudação para Olá **utilitários de cliente do HPC Pack**.</span><span class="sxs-lookup"><span data-stu-id="e188a-182">When you begin hello installation, choose hello setup option for hello **HPC Pack client utilities**.</span></span>

<span data-ttu-id="e188a-183">tooprepare Olá cliente computador, instale o certificado de Olá usado durante a [instalação de cluster HPC](hpcpack-2016-cluster.md) no computador do cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="e188a-183">tooprepare hello client computer, install hello certificate used during [HPC cluster setup](hpcpack-2016-cluster.md) on hello client computer.</span></span> <span data-ttu-id="e188a-184">Usar o Windows padrão de certificado gerenciamento procedimentos tooinstall Olá certificado público toohello **certificados – usuário atual** > **autoridades de certificação raiz confiáveis** armazenar.</span><span class="sxs-lookup"><span data-stu-id="e188a-184">Use standard Windows certificate management procedures tooinstall hello public certificate toohello **Certificates – Current user** > **Trusted Root Certification Authorities** store.</span></span> 

<span data-ttu-id="e188a-185">Agora execute comandos do HPC Pack hello ou use toosubmit Olá GUI do Gerenciador de trabalho do HPC Pack e gerenciar trabalhos de cluster usando a conta de saudação do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="e188a-185">You can now run hello HPC Pack commands or use hello HPC Pack Job manager GUI toosubmit and manage cluster jobs by using hello Azure AD account.</span></span> <span data-ttu-id="e188a-186">Para opções de envio de trabalho, consulte [cluster de HPC enviar trabalhos tooan HPC Pack no Azure](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster).</span><span class="sxs-lookup"><span data-stu-id="e188a-186">For job submission options, see [Submit HPC jobs tooan HPC Pack cluster in Azure](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster).</span></span>

> [!NOTE]
> <span data-ttu-id="e188a-187">Quando você tentar cluster de HPC Pack de toohello tooconnect no Azure para Olá primeira vez, uma janela pop-up será exibida.</span><span class="sxs-lookup"><span data-stu-id="e188a-187">When you try tooconnect toohello HPC Pack cluster in Azure for hello first time, a popup windows appears.</span></span> <span data-ttu-id="e188a-188">Insira seu toolog de credenciais do AD do Azure no.</span><span class="sxs-lookup"><span data-stu-id="e188a-188">Enter your Azure AD credentials toolog in.</span></span> <span data-ttu-id="e188a-189">Olá token, em seguida, é armazenado em cache.</span><span class="sxs-lookup"><span data-stu-id="e188a-189">hello token is then cached.</span></span> <span data-ttu-id="e188a-190">Posterior cluster toohello de conexões no uso do Azure Olá token armazenado em cache, a menos que as alterações de autenticação ou hello armazenado em cache é limpo.</span><span class="sxs-lookup"><span data-stu-id="e188a-190">Later connections toohello cluster in Azure use hello cached token unless authentication changes or hello cached is cleared.</span></span>
>
  
<span data-ttu-id="e188a-191">Por exemplo, depois de concluir as etapas anteriores hello, você pode consultar para trabalhos de um cliente local da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e188a-191">For example, after completing hello previous steps, you can query for jobs from an on-premises client as follows:</span></span>

```powershell 
Get-HpcJob –State All –Scheduler https://<Azure load balancer DNS name> -Owner <Azure AD account>
```

## <a name="useful-cmdlets-for-job-submission-with-azure-ad-integration"></a><span data-ttu-id="e188a-192">Cmdlets úteis para envio de trabalhos com a integração do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e188a-192">Useful cmdlets for job submission with Azure AD integration</span></span> 

### <a name="manage-hello-local-token-cache"></a><span data-ttu-id="e188a-193">Gerenciar o cache de token local Olá</span><span class="sxs-lookup"><span data-stu-id="e188a-193">Manage hello local token cache</span></span>

<span data-ttu-id="e188a-194">HPC Pack 2016 fornece dois novos cmdlets do PowerShell HPC cache de token local toomanage hello.</span><span class="sxs-lookup"><span data-stu-id="e188a-194">HPC Pack 2016 provides two new HPC PowerShell cmdlets toomanage hello local token cache.</span></span> <span data-ttu-id="e188a-195">Esses cmdlets são úteis para envio de trabalhos de forma não interativa.</span><span class="sxs-lookup"><span data-stu-id="e188a-195">These cmdlets are useful for submitting jobs non-interactively.</span></span> <span data-ttu-id="e188a-196">Consulte Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="e188a-196">See hello following example:</span></span>

```powershell
Remove-HpcTokenCache

$SecurePassword = "<password>" | ConvertTo-SecureString -AsPlainText -Force

Set-HpcTokenCache -UserName <AADUsername> -Password $SecurePassword -scheduler https://<Azure load balancer DNS name> 
```

### <a name="set-hello-credentials-for-submitting-jobs-using-hello-azure-ad-account"></a><span data-ttu-id="e188a-197">Definir credenciais hello para enviar trabalhos usando a conta de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e188a-197">Set hello credentials for submitting jobs using hello Azure AD account</span></span> 

<span data-ttu-id="e188a-198">Às vezes, talvez você queira toorun trabalho de saudação em usuário de cluster HPC hello (para um cluster HPC ingressado no domínio, executar como um usuário de domínio; para um cluster HPC ingressado no domínio, executar como um usuário local no nó de cabeçalho Olá).</span><span class="sxs-lookup"><span data-stu-id="e188a-198">Sometimes, you may want toorun hello job under hello HPC cluster user (for a domain-joined HPC cluster, run as one domain user; for a non-domain-joined HPC cluster, run as one local user on hello head node).</span></span>

1. <span data-ttu-id="e188a-199">Use Olá credenciais de saudação tooset comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="e188a-199">Use hello following commands tooset hello credentials:</span></span>

    ```powershell
    $localUser = “<username>”

    $localUserPassword=”<password>”

    $secpasswd = ConvertTo-SecureString $localUserPassword -AsPlainText -Force

    $mycreds = New-Object System.Management.Automation.PSCredential ($localUser, $secpasswd)

    Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name>
    ```

2. <span data-ttu-id="e188a-200">Em seguida, envie o trabalho de saudação da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="e188a-200">Then submit hello job as follows.</span></span> <span data-ttu-id="e188a-201">Olá/tarefa do trabalho é executado em $localUser em nós de computação hello.</span><span class="sxs-lookup"><span data-stu-id="e188a-201">hello job/task runs under $localUser on hello compute nodes.</span></span>

    ```powershell
    $emptycreds = New-Object System.Management.Automation.PSCredential ($localUser, (new-object System.Security.SecureString))
    ...
    $job = New-HpcJob –Scheduler https://<Azure load balancer DNS name>

    Add-HpcTask -Job $job -CommandLine "ping localhost" -Scheduler https://<Azure load balancer DNS name>

    Submit-HpcJob -Job $job -Scheduler https://<Azure load balancer DNS name> -Credential $emptycreds
    ```
    
   <span data-ttu-id="e188a-202">Se `–Credential` não for especificado com `Submit-HpcJob`, Olá trabalho ou tarefa é executado em um usuário mapeado local como Olá conta AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="e188a-202">If `–Credential` is not specified with `Submit-HpcJob`, hello job or task runs under a local mapped user as hello Azure AD account.</span></span> <span data-ttu-id="e188a-203">(cluster HPC Olá cria um usuário local com o mesmo nome como Olá tarefa de saudação do AD do Azure conta toorun de saudação.)</span><span class="sxs-lookup"><span data-stu-id="e188a-203">(hello HPC cluster creates a local user with hello same name as hello Azure AD account toorun hello task.)</span></span>
    
3. <span data-ttu-id="e188a-204">Definir dados estendidos de saudação conta AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="e188a-204">Set extended data for hello Azure AD account.</span></span> <span data-ttu-id="e188a-205">Isso é útil ao executar um trabalho MPI em nós do Linux usando a conta de saudação do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="e188a-205">This is useful when running an MPI job on Linux nodes using hello Azure AD account.</span></span>

   * <span data-ttu-id="e188a-206">Definir dados estendidos para Olá própria conta do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e188a-206">Set extended data for hello Azure AD account itself</span></span>

      ```powershell
      Set-HpcJobCredential -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data> -AadUser
      ```
      
   * <span data-ttu-id="e188a-207">Definir dados estendidos e executar como usuário do cluster HPC</span><span class="sxs-lookup"><span data-stu-id="e188a-207">Set extended data and run as HPC cluster user</span></span>
   
      ```powershell
      Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data>
      ```

