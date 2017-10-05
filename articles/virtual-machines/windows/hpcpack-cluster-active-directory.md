---
title: Cluster HPC Pack com o Azure Active Directory | Microsoft Docs
description: Saiba como integrar um cluster HPC Pack 2016 no Azure ao Azure Active Directory
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
ms.openlocfilehash: c5a06a9c810349b1bcce01c7f73563941a5af0ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-an-hpc-pack-cluster-in-azure-using-azure-active-directory"></a><span data-ttu-id="c69f6-103">Gerenciar um cluster HPC Pack no Azure usando o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c69f6-103">Manage an HPC Pack cluster in Azure using Azure Active Directory</span></span>
<span data-ttu-id="c69f6-104">O [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) dá suporte à integração com o [Azure AD](../../active-directory/index.md) (Azure Active Directory) para administradores que implantam um cluster HPC Pack no Azure.</span><span class="sxs-lookup"><span data-stu-id="c69f6-104">[Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) supports integration with [Azure Active Directory](../../active-directory/index.md) (Azure AD) for administrators who deploy an HPC Pack cluster in Azure.</span></span>



<span data-ttu-id="c69f6-105">Siga as etapas neste artigo para as seguintes tarefas de alto nível:</span><span class="sxs-lookup"><span data-stu-id="c69f6-105">Follow the steps in this article for the following high level tasks:</span></span> 
* <span data-ttu-id="c69f6-106">Integrar manualmente o cluster HPC Pack ao locatário do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c69f6-106">Manually integrate your HPC Pack cluster with your Azure AD tenant</span></span>
* <span data-ttu-id="c69f6-107">Gerenciar e agendar trabalhos no cluster HPC Pack no Azure</span><span class="sxs-lookup"><span data-stu-id="c69f6-107">Manage and schedule jobs in your HPC Pack cluster in Azure</span></span> 

<span data-ttu-id="c69f6-108">A integração de uma solução de cluster HPC Pack ao Azure AD segue as etapas padrão para integrar outros aplicativos e serviços.</span><span class="sxs-lookup"><span data-stu-id="c69f6-108">Integrating an HPC Pack cluster solution with Azure AD follows standard steps to integrate other applications and services.</span></span> <span data-ttu-id="c69f6-109">Este artigo pressupõe que você esteja familiarizado com o gerenciamento básico de usuários no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c69f6-109">This article assumes you are familiar with basic user management in Azure AD.</span></span> <span data-ttu-id="c69f6-110">Para obter mais informações e detalhes, confira a [documentação do Azure Active Directory](../../active-directory/index.md) e a seção a seguir.</span><span class="sxs-lookup"><span data-stu-id="c69f6-110">For more information and background, see the [Azure Active Directory documentation](../../active-directory/index.md) and the following section.</span></span>

## <a name="benefits-of-integration"></a><span data-ttu-id="c69f6-111">Vantagens da integração</span><span class="sxs-lookup"><span data-stu-id="c69f6-111">Benefits of integration</span></span>


<span data-ttu-id="c69f6-112">O Azure AD (Azure Active Directory) é um serviço de gerenciamento de identidades e multilocatário baseado em nuvem diretórios que fornece acesso SSO (logon único) a soluções de nuvem.</span><span class="sxs-lookup"><span data-stu-id="c69f6-112">Azure Active Directory (Azure AD) is a multi-tenant cloud-based directory and identity management service that provides single sign-on (SSO) access to cloud solutions.</span></span>

<span data-ttu-id="c69f6-113">A integração de um cluster HPC Pack ao Azure AD pode ajudá-lo a atingir as seguintes metas:</span><span class="sxs-lookup"><span data-stu-id="c69f6-113">Integration of an HPC Pack cluster with Azure AD can help you achieve the following goals:</span></span>

* <span data-ttu-id="c69f6-114">Remover o controlador de domínio do Active Directory tradicional do cluster HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="c69f6-114">Remove the traditional Active Directory domain controller from the HPC Pack cluster.</span></span> <span data-ttu-id="c69f6-115">Isso poderá ajudar a reduzir os custos de manutenção do cluster se isso não for necessário para sua empresa, bem como acelerar o processo de implantação.</span><span class="sxs-lookup"><span data-stu-id="c69f6-115">This can help reduce the costs of maintaining the cluster if this is not necessary for your business, and speed-up the deployment process.</span></span>
* <span data-ttu-id="c69f6-116">Aproveitar os seguintes benefícios oferecidos pelo Azure AD:</span><span class="sxs-lookup"><span data-stu-id="c69f6-116">Leverage the following benefits that are brought by Azure AD:</span></span>
    *   <span data-ttu-id="c69f6-117">Logon único</span><span class="sxs-lookup"><span data-stu-id="c69f6-117">Single sign-on</span></span> 
    *   <span data-ttu-id="c69f6-118">Usar uma identidade do AD local para o cluster HPC Pack no Azure</span><span class="sxs-lookup"><span data-stu-id="c69f6-118">Using a local AD identity for the HPC Pack cluster in Azure</span></span> 

    ![Ambiente do Azure Active Directory](./media/hpcpack-cluster-active-directory/aad.png)


## <a name="prerequisites"></a><span data-ttu-id="c69f6-120">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c69f6-120">Prerequisites</span></span>
* <span data-ttu-id="c69f6-121">**Cluster HPC Pack 2016 implantado em máquinas virtuais do Azure** - para obter as etapas, confira [Implantar um cluster HPC Pack 2016 no Azure](hpcpack-2016-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="c69f6-121">**HPC Pack 2016 cluster deployed in Azure virtual machines** - For steps, see [Deploy an HPC Pack 2016 cluster in Azure](hpcpack-2016-cluster.md).</span></span> <span data-ttu-id="c69f6-122">Você precisa do nome DNS do nó principal e as credenciais de um administrador de cluster para concluir as etapas neste artigo.</span><span class="sxs-lookup"><span data-stu-id="c69f6-122">You need the DNS name of the head node and the credentials of a cluster administrator to complete the steps in this article.</span></span>

  > [!NOTE]
  > <span data-ttu-id="c69f6-123">Não há suporte à integração do Azure Active Directory nas versões do HPC Pack anteriores ao HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="c69f6-123">Azure Active Directory integration is not supported in versions of HPC Pack before HPC Pack 2016.</span></span>



* <span data-ttu-id="c69f6-124">**Computador cliente** - você precisa de um computador cliente Windows ou Windows Server para executar utilitários clientes do HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="c69f6-124">**Client computer** - You need a Windows or Windows Server client computer to  run HPC Pack client utilities.</span></span> <span data-ttu-id="c69f6-125">Se você quiser usar a API REST ou o portal da Web do Pacote HPC para enviar trabalhos, poderá usar qualquer computador cliente de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="c69f6-125">If you only want to use the HPC Pack web portal or REST API to submit jobs, you can use any client computer of your choice.</span></span>

* <span data-ttu-id="c69f6-126">**Utilitários clientes do HPC Pack** - instale os utilitários clientes do HPC Pack no computador cliente, usando o pacote de instalação gratuita disponível no Centro de Download da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c69f6-126">**HPC Pack client utilities** - Install the HPC Pack client utilities on the client computer, using the free installation package available from the Microsoft Download Center.</span></span>


## <a name="step-1-register-the-hpc-cluster-server-with-your-azure-ad-tenant"></a><span data-ttu-id="c69f6-127">Etapa 1: registrar o servidor de cluster HPC no locatário do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c69f6-127">Step 1: Register the HPC cluster server with your Azure AD tenant</span></span>
1. <span data-ttu-id="c69f6-128">Entre no [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="c69f6-128">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="c69f6-129">Clique em **Active Directory** no menu à esquerda e clique no diretório desejado em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="c69f6-129">Click **Active Directory** in the left menu, and then click the desired directory in your subscription.</span></span> <span data-ttu-id="c69f6-130">Você deve ter permissão para acessar recursos no diretório.</span><span class="sxs-lookup"><span data-stu-id="c69f6-130">You must have permission to access resources in the directory.</span></span>
3. <span data-ttu-id="c69f6-131">Clique em **Usuários** e verifique se há contas de usuário já criadas ou configuradas.</span><span class="sxs-lookup"><span data-stu-id="c69f6-131">Click **Users**, and make sure there are user accounts already created or configured.</span></span>
4. <span data-ttu-id="c69f6-132">Clique em **Aplicativos** > **Adicionar** e clique em **Adicionar um aplicativo que minha organização está desenvolvendo**.</span><span class="sxs-lookup"><span data-stu-id="c69f6-132">Click **Applications** > **Add**, and then click **Add an application my organization is developing**.</span></span> <span data-ttu-id="c69f6-133">Insira as seguintes informações no assistente:</span><span class="sxs-lookup"><span data-stu-id="c69f6-133">Enter the following information in the wizard:</span></span>
    * <span data-ttu-id="c69f6-134">**Nome** - HPCPackClusterServer</span><span class="sxs-lookup"><span data-stu-id="c69f6-134">**Name** - HPCPackClusterServer</span></span>
    * <span data-ttu-id="c69f6-135">**Tipo** - selecione **Aplicativo Web e/ou API Web**</span><span class="sxs-lookup"><span data-stu-id="c69f6-135">**Type** - Select **Web Application and/or Web API**</span></span>
    * <span data-ttu-id="c69f6-136">**URL de logon** - a URL base para o exemplo, que, por padrão, é `https://hpcserver`</span><span class="sxs-lookup"><span data-stu-id="c69f6-136">**Sign-on URL**- The base URL for the sample, which is by default `https://hpcserver`</span></span>
    * <span data-ttu-id="c69f6-137">**URI da ID do aplicativo** - `https://<Directory_name>/<application_name>`.</span><span class="sxs-lookup"><span data-stu-id="c69f6-137">**App ID URI** - `https://<Directory_name>/<application_name>`.</span></span> <span data-ttu-id="c69f6-138">Substitua `<Directory_name`> pelo nome completo do locatário do Azure AD, por exemplo, `hpclocal.onmicrosoft.com` e substitua `<application_name>` pelo nome escolhido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c69f6-138">Replace `<Directory_name`> with the full name of your Azure AD tenant, for example, `hpclocal.onmicrosoft.com`, and replace `<application_name>` with the name you chose previously.</span></span>

5. <span data-ttu-id="c69f6-139">Depois que o aplicativo for adicionado, clique em **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="c69f6-139">After the app is added, click **Configure**.</span></span> <span data-ttu-id="c69f6-140">Configure as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="c69f6-140">Configure the following properties:</span></span>
    * <span data-ttu-id="c69f6-141">Selecione **Sim** para **O aplicativo é multilocatário**</span><span class="sxs-lookup"><span data-stu-id="c69f6-141">Select **Yes** for **Application is multi-tenant**</span></span>
    * <span data-ttu-id="c69f6-142">Selecione **Sim** para **Atribuição de usuário necessária para acessar o aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="c69f6-142">Select **Yes** for **User assignment required to access app**.</span></span>

6. <span data-ttu-id="c69f6-143">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="c69f6-143">Click **Save**.</span></span> <span data-ttu-id="c69f6-144">Quando o salvamento for concluído, clique em **Gerenciar Manifesto**.</span><span class="sxs-lookup"><span data-stu-id="c69f6-144">When saving completes, click **Manage Manifest**.</span></span> <span data-ttu-id="c69f6-145">Essa ação baixa o arquivo de JavaScript Object Notation (JSON).</span><span class="sxs-lookup"><span data-stu-id="c69f6-145">This action downloads your application’s manifest JavaScript object notation (JSON) file.</span></span> <span data-ttu-id="c69f6-146">Edite o manifesto baixado localizando a configuração `appRoles` e adicionando a seguinte função de aplicativo:</span><span class="sxs-lookup"><span data-stu-id="c69f6-146">Edit the downloaded manifest by locating the `appRoles` setting and adding the following application role:</span></span>
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
7. <span data-ttu-id="c69f6-147">Salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="c69f6-147">Save the file.</span></span> <span data-ttu-id="c69f6-148">No portal, clique em **Gerenciar Manifesto** > **Carregar Manifesto**.</span><span class="sxs-lookup"><span data-stu-id="c69f6-148">Then in the portal, click **Manage Manifest** > **Upload Manifest**.</span></span> <span data-ttu-id="c69f6-149">Em seguida, você pode carregar o manifesto editado.</span><span class="sxs-lookup"><span data-stu-id="c69f6-149">You can then upload the edited manifest.</span></span>
8. <span data-ttu-id="c69f6-150">Clique em **Usuários**, selecione um usuário e clique em **Atribuir**.</span><span class="sxs-lookup"><span data-stu-id="c69f6-150">Click **Users**, select a user, and then click **Assign**.</span></span> <span data-ttu-id="c69f6-151">Atribua uma das funções disponíveis (HpcUsers ou HpcAdminMirror) ao usuário.</span><span class="sxs-lookup"><span data-stu-id="c69f6-151">Assign one of the available roles (HpcUsers or HpcAdminMirror) to the user.</span></span> <span data-ttu-id="c69f6-152">Repita essa etapa com outros usuários no diretório.</span><span class="sxs-lookup"><span data-stu-id="c69f6-152">Repeat this step with additional users in the directory.</span></span> <span data-ttu-id="c69f6-153">Para obter informações sobre os usuários de cluster, confira [Gerenciar usuários de cluster](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx).</span><span class="sxs-lookup"><span data-stu-id="c69f6-153">For background information about cluster users, see [Managing Cluster Users](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx).</span></span>

   > [!NOTE] 
   > <span data-ttu-id="c69f6-154">Para gerenciar usuários, é recomendável usar a folha de visualização do Azure Active Directory no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c69f6-154">To manage users, we recommend using the Azure Active Directory preview blade in the [Azure portal](https://portal.azure.com).</span></span>
   >


## <a name="step-2-register-the-hpc-cluster-client-with-your-azure-ad-tenant"></a><span data-ttu-id="c69f6-155">Etapa 2: registrar o cliente de cluster HPC no locatário do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c69f6-155">Step 2: Register the HPC cluster client with your Azure AD tenant</span></span>

1. <span data-ttu-id="c69f6-156">Entre no [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="c69f6-156">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="c69f6-157">Clique em **Active Directory** no menu à esquerda e clique no diretório desejado em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="c69f6-157">Click **Active Directory** in the left menu, and then click the desired directory in your subscription.</span></span> <span data-ttu-id="c69f6-158">Você deve ter permissão para acessar recursos no diretório.</span><span class="sxs-lookup"><span data-stu-id="c69f6-158">You must have permission to access resources in the directory.</span></span>
3. <span data-ttu-id="c69f6-159">Clique em **Aplicativos** > **Adicionar** e clique em **Adicionar um aplicativo que minha organização está desenvolvendo**.</span><span class="sxs-lookup"><span data-stu-id="c69f6-159">Click **Applications** > **Add**, and then click **Add an application my organization is developing**.</span></span> <span data-ttu-id="c69f6-160">Insira as seguintes informações no assistente:</span><span class="sxs-lookup"><span data-stu-id="c69f6-160">Enter the following information in the wizard:</span></span>

    * <span data-ttu-id="c69f6-161">**Nome** - HPCPackClusterClient</span><span class="sxs-lookup"><span data-stu-id="c69f6-161">**Name** - HPCPackClusterClient</span></span>
    * <span data-ttu-id="c69f6-162">**Tipo** – selecione **Aplicativo Cliente Nativo**</span><span class="sxs-lookup"><span data-stu-id="c69f6-162">**Type** - Select **Native Client Application**</span></span>
    * <span data-ttu-id="c69f6-163">**URI de redirecionamento** - `http://hpcclient`</span><span class="sxs-lookup"><span data-stu-id="c69f6-163">**Redirect URI** - `http://hpcclient`</span></span>

4. <span data-ttu-id="c69f6-164">Depois que o aplicativo for adicionado, clique em **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="c69f6-164">After the app is added, click **Configure**.</span></span> <span data-ttu-id="c69f6-165">Copie o valor de **ID do cliente** e salve-o.</span><span class="sxs-lookup"><span data-stu-id="c69f6-165">Copy the **Client ID** value and save it.</span></span> <span data-ttu-id="c69f6-166">Você precisará dele mais tarde ao configurar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c69f6-166">You need this later when configuring your application.</span></span>

5. <span data-ttu-id="c69f6-167">Em **Permissões para outros aplicativos**, clique em **Adicionar aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="c69f6-167">In **Permissions to other applications**, click **Add Application**.</span></span> <span data-ttu-id="c69f6-168">Pesquisar e adicionar o aplicativo HpcPackClusterServer (criado na Etapa 1).</span><span class="sxs-lookup"><span data-stu-id="c69f6-168">Search and add the  HpcPackClusterServer application (created in Step 1).</span></span>

6. <span data-ttu-id="c69f6-169">No menu suspenso **Permissões Delegadas**, selecione **Acessar HpcClusterServer**.</span><span class="sxs-lookup"><span data-stu-id="c69f6-169">In the **Delegated Permissions** dropdown, select **Access HpcClusterServer**.</span></span> <span data-ttu-id="c69f6-170">Em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="c69f6-170">Then click **Save**.</span></span>


## <a name="step-3-configure-the-hpc-cluster"></a><span data-ttu-id="c69f6-171">Etapa 3: configurar o cluster HPC</span><span class="sxs-lookup"><span data-stu-id="c69f6-171">Step 3: Configure the HPC cluster</span></span>

1. <span data-ttu-id="c69f6-172">Conecte-se ao nó principal do HPC Pack 2016 no Azure.</span><span class="sxs-lookup"><span data-stu-id="c69f6-172">Connect to the HPC Pack 2016 head node in Azure.</span></span>

2. <span data-ttu-id="c69f6-173">Inicie o HPC PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c69f6-173">Start HPC PowerShell.</span></span>

3. <span data-ttu-id="c69f6-174">Execute o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="c69f6-174">Run the following command:</span></span>

    ```powershell

    Set-HpcClusterRegistry -SupportAAD true -AADInstance https://login.microsoftonline.com/ -AADAppName HpcClusterServer -AADTenant <your AAD tenant name> -AADClientAppId <client ID> -AADClientAppRedirectUri http://hpcclient
    ```
    <span data-ttu-id="c69f6-175">onde</span><span class="sxs-lookup"><span data-stu-id="c69f6-175">where</span></span>

    * <span data-ttu-id="c69f6-176">`AADTenant` especifica o nome do locatário do Azure AD, como `hpclocal.onmicrosoft.com`</span><span class="sxs-lookup"><span data-stu-id="c69f6-176">`AADTenant` specifies the Azure AD tenant name, such as `hpclocal.onmicrosoft.com`</span></span>
    * <span data-ttu-id="c69f6-177">`AADClientAppId` especifica a ID do cliente para o aplicativo criado na Etapa 2.</span><span class="sxs-lookup"><span data-stu-id="c69f6-177">`AADClientAppId` specifies the client ID for the app created in Step 2.</span></span>

4. <span data-ttu-id="c69f6-178">Reinicie o serviço HpcSchedulerStateful.</span><span class="sxs-lookup"><span data-stu-id="c69f6-178">Restart the HpcSchedulerStateful service.</span></span>

    <span data-ttu-id="c69f6-179">Em um cluster com vários nós principais, você pode executar os seguintes comandos do PowerShell no nó principal para alternar a réplica principal para o serviço HpcSchedulerStateful:</span><span class="sxs-lookup"><span data-stu-id="c69f6-179">In a cluster with multiple head nodes, you can run the following PowerShell commands on the head node to switch the primary replica for the HpcSchedulerStateful service:</span></span>

    ```powershell
    Connect-ServiceFabricCluster

    Move-ServiceFabricPrimaryReplica –ServiceName “fabric:/HpcApplication/SchedulerStatefulService”

    ```

## <a name="step-4-manage-and-submit-jobs-from-the-client"></a><span data-ttu-id="c69f6-180">Etapa 4: gerenciar e enviar trabalhos do cliente</span><span class="sxs-lookup"><span data-stu-id="c69f6-180">Step 4: Manage and submit jobs from the client</span></span>

<span data-ttu-id="c69f6-181">Para instalar os utilitários do Pacote HPC no computador cliente, baixe os arquivos de instalação do Pacote HPC 2016 (instalação completa) pelo Centro de Download da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c69f6-181">To install the HPC Pack client utilities on your computer, download the HPC Pack 2016 setup files (full installation) from the Microsoft Download Center.</span></span> <span data-ttu-id="c69f6-182">Quando você começar a instalação, escolha a opção de instalação dos **utilitários cliente do Pacote HPC**.</span><span class="sxs-lookup"><span data-stu-id="c69f6-182">When you begin the installation, choose the setup option for the **HPC Pack client utilities**.</span></span>

<span data-ttu-id="c69f6-183">Para preparar o computador cliente, instale o certificado usado durante a [instalação do cluster HPC](hpcpack-2016-cluster.md) no computador cliente.</span><span class="sxs-lookup"><span data-stu-id="c69f6-183">To prepare the client computer, install the certificate used during [HPC cluster setup](hpcpack-2016-cluster.md) on the client computer.</span></span> <span data-ttu-id="c69f6-184">Use procedimentos padrão de gerenciamento de certificados do Windows para instalar o certificado público no repositório **Certificados – usuário atual** > **Autoridades de Certificação Raiz Confiáveis**.</span><span class="sxs-lookup"><span data-stu-id="c69f6-184">Use standard Windows certificate management procedures to install the public certificate to the **Certificates – Current user** > **Trusted Root Certification Authorities** store.</span></span> 

<span data-ttu-id="c69f6-185">Agora você pode executar os comandos do HPC Pack ou usar a GUI do Gerenciador de trabalhos do HPC Pack para enviar e gerenciar trabalhos de cluster usando a conta do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c69f6-185">You can now run the HPC Pack commands or use the HPC Pack Job manager GUI to submit and manage cluster jobs by using the Azure AD account.</span></span> <span data-ttu-id="c69f6-186">Para obter as opções de envio de trabalhos, consulte [Enviar trabalhos HPC de um computador local para um cluster HPC Pack implantado no Azure](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster).</span><span class="sxs-lookup"><span data-stu-id="c69f6-186">For job submission options, see [Submit HPC jobs to an HPC Pack cluster in Azure](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster).</span></span>

> [!NOTE]
> <span data-ttu-id="c69f6-187">Quando você tenta se conectar ao cluster HPC Pack no Azure pela primeira vez, uma janela pop-up é exibida.</span><span class="sxs-lookup"><span data-stu-id="c69f6-187">When you try to connect to the HPC Pack cluster in Azure for the first time, a popup windows appears.</span></span> <span data-ttu-id="c69f6-188">Insira suas credenciais do Azure AD para fazer logon.</span><span class="sxs-lookup"><span data-stu-id="c69f6-188">Enter your Azure AD credentials to log in.</span></span> <span data-ttu-id="c69f6-189">O token é armazenado em cache.</span><span class="sxs-lookup"><span data-stu-id="c69f6-189">The token is then cached.</span></span> <span data-ttu-id="c69f6-190">Conexões posteriores ao cluster no Azure usam o token em cache, a menos que a autenticação seja alterada ou o cache seja limpo.</span><span class="sxs-lookup"><span data-stu-id="c69f6-190">Later connections to the cluster in Azure use the cached token unless authentication changes or the cached is cleared.</span></span>
>
  
<span data-ttu-id="c69f6-191">Por exemplo, após concluir as etapas anteriores, você pode consultar trabalhos de um cliente local da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="c69f6-191">For example, after completing the previous steps, you can query for jobs from an on-premises client as follows:</span></span>

```powershell 
Get-HpcJob –State All –Scheduler https://<Azure load balancer DNS name> -Owner <Azure AD account>
```

## <a name="useful-cmdlets-for-job-submission-with-azure-ad-integration"></a><span data-ttu-id="c69f6-192">Cmdlets úteis para envio de trabalhos com a integração do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c69f6-192">Useful cmdlets for job submission with Azure AD integration</span></span> 

### <a name="manage-the-local-token-cache"></a><span data-ttu-id="c69f6-193">Gerenciar o cache de token local</span><span class="sxs-lookup"><span data-stu-id="c69f6-193">Manage the local token cache</span></span>

<span data-ttu-id="c69f6-194">O HPC Pack 2016 fornece dois novos cmdlets do PowerShell HPC para gerenciar o cache de token local.</span><span class="sxs-lookup"><span data-stu-id="c69f6-194">HPC Pack 2016 provides two new HPC PowerShell cmdlets to manage the local token cache.</span></span> <span data-ttu-id="c69f6-195">Esses cmdlets são úteis para envio de trabalhos de forma não interativa.</span><span class="sxs-lookup"><span data-stu-id="c69f6-195">These cmdlets are useful for submitting jobs non-interactively.</span></span> <span data-ttu-id="c69f6-196">Veja os exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="c69f6-196">See the following example:</span></span>

```powershell
Remove-HpcTokenCache

$SecurePassword = "<password>" | ConvertTo-SecureString -AsPlainText -Force

Set-HpcTokenCache -UserName <AADUsername> -Password $SecurePassword -scheduler https://<Azure load balancer DNS name> 
```

### <a name="set-the-credentials-for-submitting-jobs-using-the-azure-ad-account"></a><span data-ttu-id="c69f6-197">Definir as credenciais para enviar trabalhos usando a conta do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c69f6-197">Set the credentials for submitting jobs using the Azure AD account</span></span> 

<span data-ttu-id="c69f6-198">Às vezes, é recomendável executar o trabalho no usuário do cluster HPC (para um cluster HPC ingressado em domínio, execute como um usuário de domínio; para um cluster HPC não ingressado em domínio, execute como um usuário local no nó de cabeçalho).</span><span class="sxs-lookup"><span data-stu-id="c69f6-198">Sometimes, you may want to run the job under the HPC cluster user (for a domain-joined HPC cluster, run as one domain user; for a non-domain-joined HPC cluster, run as one local user on the head node).</span></span>

1. <span data-ttu-id="c69f6-199">Use os seguintes comandos para definir as credenciais:</span><span class="sxs-lookup"><span data-stu-id="c69f6-199">Use the following commands to set the credentials:</span></span>

    ```powershell
    $localUser = “<username>”

    $localUserPassword=”<password>”

    $secpasswd = ConvertTo-SecureString $localUserPassword -AsPlainText -Force

    $mycreds = New-Object System.Management.Automation.PSCredential ($localUser, $secpasswd)

    Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name>
    ```

2. <span data-ttu-id="c69f6-200">Depois, envie o trabalho da maneira a seguir.</span><span class="sxs-lookup"><span data-stu-id="c69f6-200">Then submit the job as follows.</span></span> <span data-ttu-id="c69f6-201">O trabalho/tarefa é executado em $localUser nos nós de computação.</span><span class="sxs-lookup"><span data-stu-id="c69f6-201">The job/task runs under $localUser on the compute nodes.</span></span>

    ```powershell
    $emptycreds = New-Object System.Management.Automation.PSCredential ($localUser, (new-object System.Security.SecureString))
    ...
    $job = New-HpcJob –Scheduler https://<Azure load balancer DNS name>

    Add-HpcTask -Job $job -CommandLine "ping localhost" -Scheduler https://<Azure load balancer DNS name>

    Submit-HpcJob -Job $job -Scheduler https://<Azure load balancer DNS name> -Credential $emptycreds
    ```
    
   <span data-ttu-id="c69f6-202">Se `–Credential` não for especificado com `Submit-HpcJob`, o trabalho ou a tarefa será executado em um usuário mapeado local como a conta do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c69f6-202">If `–Credential` is not specified with `Submit-HpcJob`, the job or task runs under a local mapped user as the Azure AD account.</span></span> <span data-ttu-id="c69f6-203">(O cluster HPC cria um usuário local com o mesmo nome que a conta do Azure AD para executar a tarefa.)</span><span class="sxs-lookup"><span data-stu-id="c69f6-203">(The HPC cluster creates a local user with the same name as the Azure AD account to run the task.)</span></span>
    
3. <span data-ttu-id="c69f6-204">Defina dados estendidos para a conta do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c69f6-204">Set extended data for the Azure AD account.</span></span> <span data-ttu-id="c69f6-205">Isso é útil ao executar um trabalho MPI em nós do Linux usando a conta do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c69f6-205">This is useful when running an MPI job on Linux nodes using the Azure AD account.</span></span>

   * <span data-ttu-id="c69f6-206">Definir dados estendidos para a própria conta do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c69f6-206">Set extended data for the Azure AD account itself</span></span>

      ```powershell
      Set-HpcJobCredential -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data> -AadUser
      ```
      
   * <span data-ttu-id="c69f6-207">Definir dados estendidos e executar como usuário do cluster HPC</span><span class="sxs-lookup"><span data-stu-id="c69f6-207">Set extended data and run as HPC cluster user</span></span>
   
      ```powershell
      Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data>
      ```

