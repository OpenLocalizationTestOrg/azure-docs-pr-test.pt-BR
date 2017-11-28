---
title: "Pré-requisitos para acessar a API de relatório do Azure AD | Microsoft Docs"
description: "Aprenda sobre os pré-requisitos para acessar a API de relatório do Azure AD"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 5fafd83c337e3c73260d89cdad7409a01ce5855b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="prerequisites-to-access-the-azure-ad-reporting-api"></a><span data-ttu-id="1c193-103">Pré-requisitos para acessar a API de relatório do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c193-103">Prerequisites to access the Azure AD reporting API</span></span>

<span data-ttu-id="1c193-104">As [APIs de relatório do Azure AD](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) fornecem acesso programático aos dados através de um conjunto de APIs baseadas em REST.</span><span class="sxs-lookup"><span data-stu-id="1c193-104">The [Azure AD reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="1c193-105">Você pode chamar essas APIs de várias ferramentas e linguagens de programação.</span><span class="sxs-lookup"><span data-stu-id="1c193-105">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="1c193-106">A API de relatório usa [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) para autorizar o acesso às APIs da Web.</span><span class="sxs-lookup"><span data-stu-id="1c193-106">The reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) to authorize access to the web APIs.</span></span> 

<span data-ttu-id="1c193-107">Para obter acesso aos dados de relatórios por meio da API, você precisa ter uma das seguintes funções atribuídas:</span><span class="sxs-lookup"><span data-stu-id="1c193-107">To get access to the reporting data through the API, you need to have one of the following roles assigned:</span></span>

- <span data-ttu-id="1c193-108">Leitor de segurança</span><span class="sxs-lookup"><span data-stu-id="1c193-108">Security Reader</span></span>
- <span data-ttu-id="1c193-109">Administrador de Segurança</span><span class="sxs-lookup"><span data-stu-id="1c193-109">Security Admin</span></span>
- <span data-ttu-id="1c193-110">Administrador global</span><span class="sxs-lookup"><span data-stu-id="1c193-110">Global Admin</span></span>


<span data-ttu-id="1c193-111">Para preparar seu acesso à API de relatório, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="1c193-111">To prepare your access to the reporting API, you must:</span></span>

1. <span data-ttu-id="1c193-112">Registrar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="1c193-112">Register an application</span></span> 
2. <span data-ttu-id="1c193-113">Conceder permissões</span><span class="sxs-lookup"><span data-stu-id="1c193-113">Grant permissions</span></span> 
3. <span data-ttu-id="1c193-114">Reunir definições de configuração</span><span class="sxs-lookup"><span data-stu-id="1c193-114">Gather configuration settings</span></span> 

<span data-ttu-id="1c193-115">Em caso de dúvidas, problemas ou comentários, [registre um tíquete de suporte](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).</span><span class="sxs-lookup"><span data-stu-id="1c193-115">For questions, issues or feedback, please [file a support ticket](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).</span></span>

## <a name="register-an-azure-active-directory-application"></a><span data-ttu-id="1c193-116">Registrar um aplicativo do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1c193-116">Register an Azure Active Directory application</span></span>

<span data-ttu-id="1c193-117">Você precisa registrar um aplicativo mesmo que esteja acessando a API de relatório usando um script.</span><span class="sxs-lookup"><span data-stu-id="1c193-117">You need to register an app even if you are accessing the reporting API using a script.</span></span> <span data-ttu-id="1c193-118">Isso lhe dá uma **ID do aplicativo**, que é necessária para uma chamada de autorização e permite que seu código receba tokens.</span><span class="sxs-lookup"><span data-stu-id="1c193-118">This gives you an **Application ID**, which is required for an authorization call and it enables your code to receive tokens.</span></span>

<span data-ttu-id="1c193-119">Para configurar seu diretório para acessar a API de relatório do Azure AD, entre no Portal do Azure com uma conta de administrador do Azure que também seja membro da função de diretório de **Administrador Global** em seu locatário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1c193-119">To configure your directory to access the Azure AD reporting API, you must sign in to the Azure portal with an Azure administrator account that is also a member of the **Global Administrator** directory role in your Azure AD tenant.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c193-120">Aplicativos em execução com credenciais com privilégios de "admin" como esse podem ser muito poderosos, portanto certifique-se de proteger as credenciais de ID/segredo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1c193-120">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure to keep the application's ID/secret credentials secure.</span></span>
> 


<span data-ttu-id="1c193-121">**Para registrar um aplicativo do Azure Active Directory:**</span><span class="sxs-lookup"><span data-stu-id="1c193-121">**To register an Azure Active Directory application:**</span></span>

1. <span data-ttu-id="1c193-122">No [portal do Azure](https://portal.azure.com), no painel de navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1c193-122">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="1c193-124">Na folha **Azure Active Directory**, clique em **Registros do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="1c193-124">On the **Azure Active Directory** blade, click **App registrations**.</span></span>

    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/02.png) 

3. <span data-ttu-id="1c193-126">Na folha **Registros do aplicativo**, na barra de ferramentas na parte superior, clique em **Novo registro de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="1c193-126">On the **App registrations** blade, in the toolbar on the top, click **New application registration**.</span></span>

    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/03.png)

4. <span data-ttu-id="1c193-128">Na folha **Criar**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="1c193-128">On the **Create** blade, perform the following steps:</span></span>

    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/04.png)

    <span data-ttu-id="1c193-130">a.</span><span class="sxs-lookup"><span data-stu-id="1c193-130">a.</span></span> <span data-ttu-id="1c193-131">Na caixa de texto **Nome**, digite `Reporting API application`.</span><span class="sxs-lookup"><span data-stu-id="1c193-131">In the **Name** textbox, type `Reporting API application`.</span></span>

    <span data-ttu-id="1c193-132">b.</span><span class="sxs-lookup"><span data-stu-id="1c193-132">b.</span></span> <span data-ttu-id="1c193-133">Como **Tipo de aplicativo**, selecione **Aplicativo/API Web**.</span><span class="sxs-lookup"><span data-stu-id="1c193-133">As **Application type**, select **Web app / API**.</span></span>

    <span data-ttu-id="1c193-134">c.</span><span class="sxs-lookup"><span data-stu-id="1c193-134">c.</span></span> <span data-ttu-id="1c193-135">Na caixa de texto **URL de Entrada**, digite `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="1c193-135">In the **Sign-on URL** textbox, type `https://localhost`.</span></span>

    <span data-ttu-id="1c193-136">d.</span><span class="sxs-lookup"><span data-stu-id="1c193-136">d.</span></span> <span data-ttu-id="1c193-137">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="1c193-137">Click **Create**.</span></span> 


## <a name="grant-permissions"></a><span data-ttu-id="1c193-138">Conceder permissões</span><span class="sxs-lookup"><span data-stu-id="1c193-138">Grant permissions</span></span> 

<span data-ttu-id="1c193-139">O objetivo desta etapa é conceder ao seu aplicativo permissões para **Ler dados do diretório** para a API do **Microsoft Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1c193-139">The objective of this step is to grant your application **Read directory data** permissions to the **Windows Azure Active Directory** API.</span></span>

![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/16.png)
 

<span data-ttu-id="1c193-141">**Para conceder ao seu aplicativo permissão para usar a API:**</span><span class="sxs-lookup"><span data-stu-id="1c193-141">**To grant your application permission to use the API:**</span></span>

1. <span data-ttu-id="1c193-142">Na folha **Registros do aplicativo**, na lista de aplicativos, clique em **Aplicativo da API de relatório**.</span><span class="sxs-lookup"><span data-stu-id="1c193-142">On the **App registrations** blade, in the apps list, click **Reporting API application**.</span></span>

2. <span data-ttu-id="1c193-143">Na folha **Aplicativo da API de relatório**, na barra de ferramentas na parte superior, clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="1c193-143">On the **Reporting API application** blade, in the toolbar on the top, click **Settings**.</span></span> 

    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

3. <span data-ttu-id="1c193-145">Na folha **Configurações**, clique em **Permissões necessárias**.</span><span class="sxs-lookup"><span data-stu-id="1c193-145">On the **Settings** blade, click **Required permissions**.</span></span> 

    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/06.png)

4. <span data-ttu-id="1c193-147">Na folha **Permissões necessárias**, na lista **API**, clique em **Microsoft Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1c193-147">On the **Required permissions** blade, in the **API** list, click **Windows Azure Active Directory**.</span></span> 

    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/07.png)

5. <span data-ttu-id="1c193-149">Na folha **Habilitar Acesso**, selecione **Ler dados do diretório**.</span><span class="sxs-lookup"><span data-stu-id="1c193-149">On the **Enable Access** blade, select **Read directory data**.</span></span> 

    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/08.png)

6. <span data-ttu-id="1c193-151">Na barra de ferramentas na parte superior, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="1c193-151">In the toolbar on the top, click **Save**.</span></span>

    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/15.png)

## <a name="gather-configuration-settings"></a><span data-ttu-id="1c193-153">Reunir definições de configuração</span><span class="sxs-lookup"><span data-stu-id="1c193-153">Gather configuration settings</span></span> 
<span data-ttu-id="1c193-154">Esta seção mostra como obter as seguintes configurações de seu diretório:</span><span class="sxs-lookup"><span data-stu-id="1c193-154">This section shows you how to get the following settings from your directory:</span></span>

* <span data-ttu-id="1c193-155">Nome de domínio</span><span class="sxs-lookup"><span data-stu-id="1c193-155">Domain name</span></span>
* <span data-ttu-id="1c193-156">ID do cliente</span><span class="sxs-lookup"><span data-stu-id="1c193-156">Client ID</span></span>
* <span data-ttu-id="1c193-157">Segredo do cliente</span><span class="sxs-lookup"><span data-stu-id="1c193-157">Client secret</span></span>

<span data-ttu-id="1c193-158">Você precisa desses valores ao configurar chamadas para a API de relatórios.</span><span class="sxs-lookup"><span data-stu-id="1c193-158">You need these values when configuring calls to the reporting API.</span></span> 

### <a name="get-your-domain-name"></a><span data-ttu-id="1c193-159">Obter seu nome de domínio</span><span class="sxs-lookup"><span data-stu-id="1c193-159">Get your domain name</span></span>

<span data-ttu-id="1c193-160">**Para obter seu nome de domínio:**</span><span class="sxs-lookup"><span data-stu-id="1c193-160">**To get your domain name:**</span></span>

1. <span data-ttu-id="1c193-161">No [portal do Azure](https://portal.azure.com), no painel de navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1c193-161">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="1c193-163">Na folha **Azure Active Directory**, clique em **Nomes de domínio**.</span><span class="sxs-lookup"><span data-stu-id="1c193-163">On the **Azure Active Directory** blade, click **Domain names**.</span></span>

    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/09.png) 

3. <span data-ttu-id="1c193-165">Copie o nome do domínio da lista de domínios.</span><span class="sxs-lookup"><span data-stu-id="1c193-165">Copy your domain name from the list of domains.</span></span>


### <a name="get-your-applications-client-id"></a><span data-ttu-id="1c193-166">Obtenha a ID do cliente do aplicativo</span><span class="sxs-lookup"><span data-stu-id="1c193-166">Get your application's client ID</span></span>

<span data-ttu-id="1c193-167">**Para obter a ID do cliente do aplicativo:**</span><span class="sxs-lookup"><span data-stu-id="1c193-167">**To get your application's client ID:**</span></span>

1. <span data-ttu-id="1c193-168">No [portal do Azure](https://portal.azure.com), no painel de navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1c193-168">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="1c193-170">Na folha **Registros do aplicativo**, na lista de aplicativos, clique em **Aplicativo da API de relatório**.</span><span class="sxs-lookup"><span data-stu-id="1c193-170">On the **App registrations** blade, in the apps list, click **Reporting API application**.</span></span>

3. <span data-ttu-id="1c193-171">Na folha **Aplicativo da API de relatório**, em **ID do aplicativo**, clique em **Clique para copiar**.</span><span class="sxs-lookup"><span data-stu-id="1c193-171">On the **Reporting API application** blade, at the **Application ID**, click **Click to copy**.</span></span>

    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/11.png) 



### <a name="get-your-applications-client-secret"></a><span data-ttu-id="1c193-173">Obter seu segredo do cliente do aplicativo</span><span class="sxs-lookup"><span data-stu-id="1c193-173">Get your application's client secret</span></span>
<span data-ttu-id="1c193-174">Para obter o segredo do cliente do aplicativo, você precisa criar uma nova chave e salvar seu valor ao salvar a nova chave, pois não é possível recuperar este valor posteriormente.</span><span class="sxs-lookup"><span data-stu-id="1c193-174">To get your application's client secret, you need to create a new key and save its value upon saving the new key because it is not possible to retrieve this value later anymore.</span></span>

<span data-ttu-id="1c193-175">**Para obter seu segredo do cliente do aplicativo:**</span><span class="sxs-lookup"><span data-stu-id="1c193-175">**To get your application's client secret:**</span></span>

1. <span data-ttu-id="1c193-176">No [portal do Azure](https://portal.azure.com), no painel de navegação à esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1c193-176">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="1c193-178">Na folha **Registros do aplicativo**, na lista de aplicativos, clique em **Aplicativo da API de relatório**.</span><span class="sxs-lookup"><span data-stu-id="1c193-178">On the **App registrations** blade, in the apps list, click **Reporting API application**.</span></span>


3. <span data-ttu-id="1c193-179">Na folha **Aplicativo da API de relatório**, na barra de ferramentas na parte superior, clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="1c193-179">On the **Reporting API application** blade, in the toolbar on the top, click **Settings**.</span></span> 

    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

4. <span data-ttu-id="1c193-181">Na folha **Configurações**, na seção **Acesso APIR**, clique em **Chaves**.</span><span class="sxs-lookup"><span data-stu-id="1c193-181">On the **Settings** blade, in the **APIR Access** section, click **Keys**.</span></span> 

    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/12.png)


5. <span data-ttu-id="1c193-183">Na folha **Chaves**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="1c193-183">On the **Keys** blade, perform the following steps:</span></span>

    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites-azure-portal/14.png)

    <span data-ttu-id="1c193-185">a.</span><span class="sxs-lookup"><span data-stu-id="1c193-185">a.</span></span> <span data-ttu-id="1c193-186">Na caixa de texto **Descrição**, digite `Reporting API`.</span><span class="sxs-lookup"><span data-stu-id="1c193-186">In the **Description** textbox, type `Reporting API`.</span></span>

    <span data-ttu-id="1c193-187">b.</span><span class="sxs-lookup"><span data-stu-id="1c193-187">b.</span></span> <span data-ttu-id="1c193-188">Como **Expira**, selecione **Em 2 anos**.</span><span class="sxs-lookup"><span data-stu-id="1c193-188">As **Expires**, select **In 2 years**.</span></span>

    <span data-ttu-id="1c193-189">c.</span><span class="sxs-lookup"><span data-stu-id="1c193-189">c.</span></span> <span data-ttu-id="1c193-190">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="1c193-190">Click **Save**.</span></span>

    <span data-ttu-id="1c193-191">d.</span><span class="sxs-lookup"><span data-stu-id="1c193-191">d.</span></span> <span data-ttu-id="1c193-192">Copie o valor da chave.</span><span class="sxs-lookup"><span data-stu-id="1c193-192">Copy the key value.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1c193-193">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1c193-193">Next Steps</span></span>
* <span data-ttu-id="1c193-194">Você gostaria de acessar os dados da API de relatório do Azure AD de uma maneira programática?</span><span class="sxs-lookup"><span data-stu-id="1c193-194">Would you like to access the data from the Azure AD reporting API in a programmatic manner?</span></span> <span data-ttu-id="1c193-195">Confira [Introdução à API de Relatório do Azure Active Directory](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="1c193-195">Check out [Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="1c193-196">Se você quiser saber mais sobre os relatórios do Azure Active Directory, confira o [Guia de relatórios do Azure Active Directory](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="1c193-196">If you would like to find out more about Azure Active Directory reporting, see the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

