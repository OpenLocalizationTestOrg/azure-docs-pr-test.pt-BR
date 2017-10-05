---
title: "Implantar a extensão do Painel de Acesso do Azure do IE usando um GPO | Microsoft Docs"
description: "Como usar a política de grupo para implantar o complemento do Internet Explorer para o portal de meus aplicativos."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 7c2d49c8-5be0-4e7e-abac-332f9dfda736
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b402ae326ab34ec71ad9de966e22be00045fee3e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-deploy-the-access-panel-extension-for-internet-explorer-using-group-policy"></a><span data-ttu-id="afd9e-103">Como implantar a Extensão do Painel de Acesso no Internet Explorer usando a Política de Grupo</span><span class="sxs-lookup"><span data-stu-id="afd9e-103">How to Deploy the Access Panel Extension for Internet Explorer using Group Policy</span></span>
<span data-ttu-id="afd9e-104">Este tutorial mostra como usar a política de grupo para instalar remotamente a extensão do Painel de Acesso para o Internet Explorer nos computadores dos usuários.</span><span class="sxs-lookup"><span data-stu-id="afd9e-104">This tutorial shows how to use group policy to remotely install the Access Panel extension for Internet Explorer on your users' machines.</span></span> <span data-ttu-id="afd9e-105">Essa extensão é necessária para os usuários do Internet Explorer que precisam entrar em aplicativos configurados usando o [logon único baseado em senha](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="afd9e-105">This extension is required for Internet Explorer users who need to sign into apps that are configured using [password-based single sign-on](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).</span></span>

<span data-ttu-id="afd9e-106">É recomendável que administradores automatizem a implantação dessa extensão.</span><span class="sxs-lookup"><span data-stu-id="afd9e-106">It is recommended that admins automate the deployment of this extension.</span></span> <span data-ttu-id="afd9e-107">Caso contrário, os usuários terão de baixar e instalar a extensão por conta própria, o que poderá causar erros do usuário e que exigirá permissões de administrador.</span><span class="sxs-lookup"><span data-stu-id="afd9e-107">Otherwise, users have to download and install the extension themselves, which is prone to user error and requires administrator permissions.</span></span> <span data-ttu-id="afd9e-108">Este tutorial apresenta um método de automatização de implantações de software usando a política de grupo.</span><span class="sxs-lookup"><span data-stu-id="afd9e-108">This tutorial covers one method of automating software deployments by using group policy.</span></span> [<span data-ttu-id="afd9e-109">Saiba mais sobre a política de grupo.</span><span class="sxs-lookup"><span data-stu-id="afd9e-109">Learn more about group policy.</span></span>](https://technet.microsoft.com/windowsserver/bb310732.aspx)

<span data-ttu-id="afd9e-110">A extensão do Painel de Acesso também está disponível para o [Chrome](https://go.microsoft.com/fwLink/?LinkID=311859) e o [Firefox](https://go.microsoft.com/fwLink/?LinkID=626998) e nenhum deles exige permissões de administrador para instalar.</span><span class="sxs-lookup"><span data-stu-id="afd9e-110">The Access Panel extension is also available for [Chrome](https://go.microsoft.com/fwLink/?LinkID=311859) and [Firefox](https://go.microsoft.com/fwLink/?LinkID=626998), neither of which require administrator permissions to install.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="afd9e-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="afd9e-111">Prerequisites</span></span>
* <span data-ttu-id="afd9e-112">Você configurou os [Serviços de Domínio do Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx)e os computadores dos usuários ingressaram no domínio.</span><span class="sxs-lookup"><span data-stu-id="afd9e-112">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines to your domain.</span></span>
* <span data-ttu-id="afd9e-113">Você deve ter a permissão "Editar configurações" para editar o GPO (Objeto de Política de Grupo).</span><span class="sxs-lookup"><span data-stu-id="afd9e-113">You must have the "Edit settings" permission to edit the Group Policy Object (GPO).</span></span> <span data-ttu-id="afd9e-114">Por padrão, os membros dos grupos de segurança a seguir têm esta permissão: Administradores de Domínio, Administradores de Empresa e Proprietários Criadores de Política de Grupo.</span><span class="sxs-lookup"><span data-stu-id="afd9e-114">By default, members of the following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> [<span data-ttu-id="afd9e-115">Saiba mais.</span><span class="sxs-lookup"><span data-stu-id="afd9e-115">Learn more.</span></span>](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx)

## <a name="step-1-create-the-distribution-point"></a><span data-ttu-id="afd9e-116">Etapa 1: Criar o ponto de distribuição</span><span class="sxs-lookup"><span data-stu-id="afd9e-116">Step 1: Create the Distribution Point</span></span>
<span data-ttu-id="afd9e-117">Primeiro, você deve colocar o pacote do instalador em um local de rede que possa ser acessado pelos computadores nos quais você deseja instalar remotamente a extensão.</span><span class="sxs-lookup"><span data-stu-id="afd9e-117">First, you must place the installer package on a network location that can be accessed by the machines that you wish to remotely install the extension on.</span></span> <span data-ttu-id="afd9e-118">Para fazer isso, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="afd9e-118">To do this, follow these steps:</span></span>

1. <span data-ttu-id="afd9e-119">Faça logon no servidor como um administrador</span><span class="sxs-lookup"><span data-stu-id="afd9e-119">Log on to the server as an administrator</span></span>
2. <span data-ttu-id="afd9e-120">Na janela **Gerenciador do Servidor**, vá para **Arquivos e Serviços de Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="afd9e-120">In the **Server Manager** window, go to **Files and Storage Services**.</span></span>
   
    ![Abrir Serviços de Arquivo e Armazenamento](./media/active-directory-saas-ie-group-policy/files-services.png)
3. <span data-ttu-id="afd9e-122">Vá para a guia **Compartilhamentos** . Em seguida, clique em **Tarefas** > **Novo Compartilhamento...**</span><span class="sxs-lookup"><span data-stu-id="afd9e-122">Go to the **Shares** tab. Then click **Tasks** > **New Share...**</span></span>
   
    ![Abrir Serviços de Arquivo e Armazenamento](./media/active-directory-saas-ie-group-policy/shares.png)
4. <span data-ttu-id="afd9e-124">Conclua o **Assistente de Novo Compartilhamento** e defina permissões para garantir que ele possa ser acessado dos computadores dos usuários.</span><span class="sxs-lookup"><span data-stu-id="afd9e-124">Complete the **New Share Wizard** and set permissions to ensure that it can be accessed from your users' machines.</span></span> [<span data-ttu-id="afd9e-125">Saiba mais sobre compartilhamentos.</span><span class="sxs-lookup"><span data-stu-id="afd9e-125">Learn more about shares.</span></span>](https://technet.microsoft.com/library/cc753175.aspx)
5. <span data-ttu-id="afd9e-126">Baixe o seguinte pacote do Microsoft Windows Installer (arquivo .msi): [Access Panel Extension.msi](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi)</span><span class="sxs-lookup"><span data-stu-id="afd9e-126">Download the following Microsoft Windows Installer package (.msi file): [Access Panel Extension.msi](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi)</span></span>
6. <span data-ttu-id="afd9e-127">Copie o pacote do instalador para um local desejado no compartilhamento.</span><span class="sxs-lookup"><span data-stu-id="afd9e-127">Copy the installer package to a desired location on the share.</span></span>
   
    ![Copie o arquivo .msi para o compartilhamento.](./media/active-directory-saas-ie-group-policy/copy-package.png)
7. <span data-ttu-id="afd9e-129">Verifique se os computadores do cliente podem acessar o pacote do instalador desde o compartilhamento.</span><span class="sxs-lookup"><span data-stu-id="afd9e-129">Verify that your client machines are able to access the installer package from the share.</span></span> 

## <a name="step-2-create-the-group-policy-object"></a><span data-ttu-id="afd9e-130">Etapa 2: Criar o Objeto de Política de Grupo</span><span class="sxs-lookup"><span data-stu-id="afd9e-130">Step 2: Create the Group Policy Object</span></span>
1. <span data-ttu-id="afd9e-131">Faça logon no servidor que hospeda sua instalação dos Serviços de Domínio do Active Directory (AD DS).</span><span class="sxs-lookup"><span data-stu-id="afd9e-131">Log on to the server that hosts your Active Directory Domain Services (AD DS) installation.</span></span>
2. <span data-ttu-id="afd9e-132">No Gerenciador do Servidor, vá para **Ferramentas** > **Gerenciamento de Política de Grupo**.</span><span class="sxs-lookup"><span data-stu-id="afd9e-132">In the Server Manager, go to **Tools** > **Group Policy Management**.</span></span>
   
    ![Vá para Ferramentas > Gerenciamento de Política de Grupo](./media/active-directory-saas-ie-group-policy/tools-gpm.png)
3. <span data-ttu-id="afd9e-134">No painel esquerdo da janela **Gerenciamento de Política de Grupo** , exiba sua hierarquia de UO (unidade organizacional) e determine em qual escopo você gostaria de aplicar a política de grupo.</span><span class="sxs-lookup"><span data-stu-id="afd9e-134">In the left pane of the **Group Policy Management** window, view your Organizational Unit (OU) hierarchy and determine at which scope you would like to apply the group policy.</span></span> <span data-ttu-id="afd9e-135">Por exemplo, você poderá optar por escolher uma UO pequena a ser implantada para alguns usuários para teste ou poderá escolher uma UO de nível superior a ser implantada em toda a sua organização.</span><span class="sxs-lookup"><span data-stu-id="afd9e-135">For instance, you may decide to pick a small OU to deploy to a few users for testing, or you may pick a top-level OU to deploy to your entire organization.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="afd9e-136">Se você quiser criar ou editar suas Unidades Organizacionais (UOs), volte para o Gerenciador do Servidor e vá para **Ferramentas** > **Usuários e Computadores do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="afd9e-136">If you would like to create or edit your Organization Units (OUs), switch back to the Server Manager and go to **Tools** > **Active Directory Users and Computers**.</span></span>
   > 
   > 
4. <span data-ttu-id="afd9e-137">Depois de selecionar uma UO, clique com o botão direito do mouse nela e selecione **Criar um GPO neste domínio e vinculá-lo aqui...**</span><span class="sxs-lookup"><span data-stu-id="afd9e-137">Once you have selected an OU, right-click it and select **Create a GPO in this domain, and Link it here...**</span></span>
   
    ![Criar um novo GPO](./media/active-directory-saas-ie-group-policy/create-gpo.png)
5. <span data-ttu-id="afd9e-139">No prompt **Novo GPO** , digite um nome para o novo Objeto de Política de Grupo.</span><span class="sxs-lookup"><span data-stu-id="afd9e-139">In the **New GPO** prompt, type in a name for the new Group Policy Object.</span></span>
   
    ![Dar um nome ao novo GPO](./media/active-directory-saas-ie-group-policy/name-gpo.png)
6. <span data-ttu-id="afd9e-141">Clique com o botão direito do mouse no Objeto de Política de Grupo criado e selecione **Editar**.</span><span class="sxs-lookup"><span data-stu-id="afd9e-141">Right-click the Group Policy Object that you created, and select **Edit**.</span></span>
   
    ![Editar o novo GPO](./media/active-directory-saas-ie-group-policy/edit-gpo.png)

## <a name="step-3-assign-the-installation-package"></a><span data-ttu-id="afd9e-143">Etapa 3: Atribuir o pacote de instalação</span><span class="sxs-lookup"><span data-stu-id="afd9e-143">Step 3: Assign the Installation Package</span></span>
1. <span data-ttu-id="afd9e-144">Determine se você deseja implantar a extensão com base na **Configuração do Computador** ou na **Configuração do Usuário**.</span><span class="sxs-lookup"><span data-stu-id="afd9e-144">Determine whether you would like to deploy the extension based on **Computer Configuration** or **User Configuration**.</span></span> <span data-ttu-id="afd9e-145">Ao usar a [configuração do computador](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx), a extensão será instalada no computador, independentemente dos usuários que fizerem logon.</span><span class="sxs-lookup"><span data-stu-id="afd9e-145">When using [computer configuration](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx), the extension is installed on the computer regardless of which users log on to it.</span></span> <span data-ttu-id="afd9e-146">Com a [configuração do usuário](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx), os usuários têm a extensão instalada para eles, independentemente dos computadores em que eles fizerem logon.</span><span class="sxs-lookup"><span data-stu-id="afd9e-146">With [user configuration](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx), users have the extension installed for them regardless of which computers they log on to.</span></span>
2. <span data-ttu-id="afd9e-147">No painel esquerdo da janela **Editor de Gerenciamento de Política de Grupo** , vá para qualquer um dos seguintes caminhos de pasta, dependendo do tipo de configuração escolhida:</span><span class="sxs-lookup"><span data-stu-id="afd9e-147">In the left pane of the **Group Policy Management Editor** window, go to either of the following folder paths, depending on which type of configuration you chose:</span></span>
   
   * `Computer Configuration/Policies/Software Settings/`
   * `User Configuration/Policies/Software Settings/`
3. <span data-ttu-id="afd9e-148">Clique com o botão direito do mouse em **Instalação do software** e selecione **Novo** > **Pacote...**</span><span class="sxs-lookup"><span data-stu-id="afd9e-148">Right-click **Software installation**, then select **New** > **Package...**</span></span>
   
    ![Criar um novo pacote de instalação de software](./media/active-directory-saas-ie-group-policy/new-package.png)
4. <span data-ttu-id="afd9e-150">Vá para a pasta compartilhada que contém o pacote do instalador da [Etapa 1: Criar o ponto de distribuição](#step-1-create-the-distribution-point), selecione o arquivo .msi e clique em **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="afd9e-150">Go to the shared folder that contains the installer package from [Step 1: Create the Distribution Point](#step-1-create-the-distribution-point), select the .msi file, and click **Open**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="afd9e-151">Se o compartilhamento estiver localizado no mesmo servidor, verifique se você está acessando o .msi por meio do caminho do arquivo de rede, em vez do caminho do arquivo local.</span><span class="sxs-lookup"><span data-stu-id="afd9e-151">If the share is located on this same server, verify that you are accessing the .msi through the network file path, rather than the local file path.</span></span>
   > 
   > 
   
    ![Selecione o pacote de instalação na pasta compartilhada.](./media/active-directory-saas-ie-group-policy/select-package.png)
5. <span data-ttu-id="afd9e-153">No prompt **Implantar Software**, selecione **Atribuído** para o método de implantação.</span><span class="sxs-lookup"><span data-stu-id="afd9e-153">In the **Deploy Software** prompt, select **Assigned** for your deployment method.</span></span> <span data-ttu-id="afd9e-154">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="afd9e-154">Then click **OK**.</span></span>
   
    ![Selecione Atribuído e clique em OK.](./media/active-directory-saas-ie-group-policy/deployment-method.png)

<span data-ttu-id="afd9e-156">Agora a extensão está implantada na UO que você selecionou.</span><span class="sxs-lookup"><span data-stu-id="afd9e-156">The extension is now deployed to the OU that you selected.</span></span> [<span data-ttu-id="afd9e-157">Saiba mais sobre a instalação do Software de Política de Grupo.</span><span class="sxs-lookup"><span data-stu-id="afd9e-157">Learn more about Group Policy Software Installation.</span></span>](https://technet.microsoft.com/library/cc738858%28v=ws.10%29.aspx)

## <a name="step-4-auto-enable-the-extension-for-internet-explorer"></a><span data-ttu-id="afd9e-158">Etapa 4: Habilitar automaticamente a extensão do Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="afd9e-158">Step 4: Auto-Enable the Extension for Internet Explorer</span></span>
<span data-ttu-id="afd9e-159">Além da execução do instalador, todas as extensões do Internet Explorer deverão ser habilitadas explicitamente antes de serem usadas.</span><span class="sxs-lookup"><span data-stu-id="afd9e-159">In addition to running the installer, every extension for Internet Explorer must be explicitly enabled before it can be used.</span></span> <span data-ttu-id="afd9e-160">Siga as etapas abaixo para habilitar a Extensão do Painel de Acesso usando a política de grupo:</span><span class="sxs-lookup"><span data-stu-id="afd9e-160">Follow the steps below to enable the Access Panel Extension using group policy:</span></span>

1. <span data-ttu-id="afd9e-161">Na janela **Editor de Gerenciamento de Política de Grupo** , vá para um dos caminhos a seguir, dependendo do tipo de configuração escolhida na [Etapa 3: Atribuir o pacote de instalação](#step-3-assign-the-installation-package):</span><span class="sxs-lookup"><span data-stu-id="afd9e-161">In the **Group Policy Management Editor** window, go to either of the following paths, depending on which type of configuration you chose in [Step 3: Assign the Installation Package](#step-3-assign-the-installation-package):</span></span>
   
   * `Computer Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
2. <span data-ttu-id="afd9e-162">Clique com o botão direito do mouse em **Lista de Complementos** e selecione **Editar**.</span><span class="sxs-lookup"><span data-stu-id="afd9e-162">Right-click **Add-on List**, and select **Edit**.</span></span>
    <span data-ttu-id="afd9e-163">![Edite a Lista de Complementos.](./media/active-directory-saas-ie-group-policy/edit-add-on-list.png)</span><span class="sxs-lookup"><span data-stu-id="afd9e-163">![Edit Add-on List.](./media/active-directory-saas-ie-group-policy/edit-add-on-list.png)</span></span>
3. <span data-ttu-id="afd9e-164">Na janela **Lista de Complementos**, selecione **Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="afd9e-164">In the **Add-on List** window, select **Enabled**.</span></span> <span data-ttu-id="afd9e-165">Em seguida, na seção **Opções**, clique em **Mostrar...**.</span><span class="sxs-lookup"><span data-stu-id="afd9e-165">Then, under the **Options** section, click **Show...**.</span></span>
   
    ![Clique em Habilitar e clique em Mostrar...](./media/active-directory-saas-ie-group-policy/edit-add-on-list-window.png)
4. <span data-ttu-id="afd9e-167">Na janela **Mostrar Conteúdo** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="afd9e-167">In the **Show Contents** window, perform the following steps:</span></span>
   
   1. <span data-ttu-id="afd9e-168">Na primeira coluna (o campo **Nome do Valor**), copie e cole a seguinte ID de Classe: `{030E9A3F-7B18-4122-9A60-B87235E4F59E}`</span><span class="sxs-lookup"><span data-stu-id="afd9e-168">For the first column (the **Value Name** field), copy and paste the following Class ID: `{030E9A3F-7B18-4122-9A60-B87235E4F59E}`</span></span>
   2. <span data-ttu-id="afd9e-169">Na segunda coluna (o campo **Valor**), digite o seguinte valor: `1`</span><span class="sxs-lookup"><span data-stu-id="afd9e-169">For the second column (the **Value** field), type in the following value: `1`</span></span>
   3. <span data-ttu-id="afd9e-170">Clique em **OK** para fechar a janela **Mostrar Conteúdo**.</span><span class="sxs-lookup"><span data-stu-id="afd9e-170">Click **OK** to close the **Show Contents** window.</span></span>
      
      ![Preencha os valores como especificado acima.](./media/active-directory-saas-ie-group-policy/show-contents.png)
5. <span data-ttu-id="afd9e-172">Clique em **OK** para aplicar as alterações e fechar a janela **Lista de Complementos**.</span><span class="sxs-lookup"><span data-stu-id="afd9e-172">Click **OK** to apply your changes and close the **Add-on List** window.</span></span>

<span data-ttu-id="afd9e-173">Agora a extensão deverá estar habilitada para os computadores na UO selecionada.</span><span class="sxs-lookup"><span data-stu-id="afd9e-173">The extension should now be enabled for the machines in the selected OU.</span></span> [<span data-ttu-id="afd9e-174">Saiba mais sobre como usar a política de grupo para habilitar ou desabilitar complementos do Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="afd9e-174">Learn more about using group policy to enable or disable Internet Explorer add-ons.</span></span>](https://technet.microsoft.com/library/dn454941.aspx)

## <a name="step-5-optional-disable-remember-password-prompt"></a><span data-ttu-id="afd9e-175">Etapa 5 (opcional): Desabilitar o prompt "Lembrar senha"</span><span class="sxs-lookup"><span data-stu-id="afd9e-175">Step 5 (Optional): Disable "Remember Password" Prompt</span></span>
<span data-ttu-id="afd9e-176">Quando os usuários entram em sites que usam a extensão do painel de acesso, o Internet Explorer mostra o seguinte prompt perguntando "Deseja armazenar sua senha?"</span><span class="sxs-lookup"><span data-stu-id="afd9e-176">When users sign-in to websites using the Access Panel Extension, Internet Explorer may show the following prompt asking "Would you like to store your password?"</span></span>

![](./media/active-directory-saas-ie-group-policy/remember-password-prompt.png)

<span data-ttu-id="afd9e-177">Se você quiser impedir que os usuários vejam esse prompt, siga as etapas abaixo para impedir o preenchimento automático de lembrar senhas:</span><span class="sxs-lookup"><span data-stu-id="afd9e-177">If you wish to prevent your users from seeing this prompt, then follow the steps below to prevent auto-complete from remembering passwords:</span></span>

1. <span data-ttu-id="afd9e-178">Na janela **Editor de gerenciamento de política de grupo** , vá para o caminho listado abaixo.</span><span class="sxs-lookup"><span data-stu-id="afd9e-178">In the **Group Policy Management Editor** window, go to the path listed below.</span></span> <span data-ttu-id="afd9e-179">Essa configuração só está disponível em **Configuração do usuário**.</span><span class="sxs-lookup"><span data-stu-id="afd9e-179">This configuration setting is only available under **User Configuration**.</span></span>
   
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/`
2. <span data-ttu-id="afd9e-180">Localize a configuração denominada **Ativar o recurso de preenchimento automático para nomes de usuário e senhas em formulários**.</span><span class="sxs-lookup"><span data-stu-id="afd9e-180">Find the setting named **Turn on the auto-complete feature for user names and passwords on forms**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="afd9e-181">Versões anteriores do Active Directory podem listar essa configuração com o nome **Não permitir o preenchimento automático para salvar senhas**.</span><span class="sxs-lookup"><span data-stu-id="afd9e-181">Previous versions of Active Directory may list this setting with the name **Do not allow auto-complete to save passwords**.</span></span> <span data-ttu-id="afd9e-182">Essa configuração é diferente da configuração descrita neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="afd9e-182">The configuration for that setting differs from the setting described in this tutorial.</span></span>
   > 
   > 
   
    ![Lembre-se de examinar isso em Configurações do usuário.](./media/active-directory-saas-ie-group-policy/disable-auto-complete.png)
3. <span data-ttu-id="afd9e-184">Clique com o botão direito na configuração acima e selecione **Editar**.</span><span class="sxs-lookup"><span data-stu-id="afd9e-184">Right click the above setting, and select **Edit**.</span></span>
4. <span data-ttu-id="afd9e-185">Na janela **Ativar o recurso de preenchimento automático para nomes de usuário e senhas em formulários**, selecione **Desabilitado**.</span><span class="sxs-lookup"><span data-stu-id="afd9e-185">In the window titled **Turn on the auto-complete feature for user names and passwords on forms**, select **Disabled**.</span></span>
   
    ![Selecione Desabilitar](./media/active-directory-saas-ie-group-policy/disable-passwords.png)
5. <span data-ttu-id="afd9e-187">Clique em **OK** para aplicar essas alterações e fechar a janela.</span><span class="sxs-lookup"><span data-stu-id="afd9e-187">Click **OK** to apply these changes and close the window.</span></span>

<span data-ttu-id="afd9e-188">Os usuários não poderão mais armazenar suas credenciais ou usar o preenchimento automático para acessar as credenciais armazenadas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="afd9e-188">Users will no longer be able to store their credentials or use auto-complete to access previously stored credentials.</span></span> <span data-ttu-id="afd9e-189">No entanto, essa política permite que os usuários continuem a usar o preenchimento automático para outros tipos de campos de formulário, como campos de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="afd9e-189">However, this policy does allow users to continue to use auto-complete for other types of form fields, such as search fields.</span></span>

> [!WARNING]
> <span data-ttu-id="afd9e-190">Se essa política for ativada depois que os usuários tiverem escolhido armazenar algumas credenciais, essa política *não* limpará as credenciais que já foram armazenadas.</span><span class="sxs-lookup"><span data-stu-id="afd9e-190">If this policy is enabled after users have chosen to store some credentials, this policy will *not* clear the credentials that have already been stored.</span></span>
> 
> 

## <a name="step-6-testing-the-deployment"></a><span data-ttu-id="afd9e-191">Etapa 6: Testar a implantação</span><span class="sxs-lookup"><span data-stu-id="afd9e-191">Step 6: Testing the Deployment</span></span>
<span data-ttu-id="afd9e-192">Siga as etapas abaixo para verificar se a implantação da extensão obteve êxito:</span><span class="sxs-lookup"><span data-stu-id="afd9e-192">Follow the steps below to verify if the extension deployment was successful:</span></span>

1. <span data-ttu-id="afd9e-193">Se você implantou usando **Configuração do computador**, faça logon em um computador cliente que pertence à UO que você selecionou na [Etapa 2: Criar o objeto de política de grupo](#step-2-create-the-group-policy-object).</span><span class="sxs-lookup"><span data-stu-id="afd9e-193">If you deployed using **Computer Configuration**, sign into a client machine that belongs to the OU that you selected in [Step 2: Create the Group Policy Object](#step-2-create-the-group-policy-object).</span></span> <span data-ttu-id="afd9e-194">Se você implantou usando **Configuração do usuário**, certifique-se de conectar-se como um usuário que pertence a essa UO.</span><span class="sxs-lookup"><span data-stu-id="afd9e-194">If you deployed using **User Configuration**, make sure to sign in as a user who belongs to that OU.</span></span>
2. <span data-ttu-id="afd9e-195">As alterações da política de grupo podem demorar algumas entradas para serem totalmente atualizadas no computador.</span><span class="sxs-lookup"><span data-stu-id="afd9e-195">It may take a couple sign ins for the group policy changes to fully update with this machine.</span></span> <span data-ttu-id="afd9e-196">Para forçar a atualização, abra um **Prompt de comando** e execute o seguinte comando: `gpupdate /force`</span><span class="sxs-lookup"><span data-stu-id="afd9e-196">To force the update, open a **Command Prompt** window and run the following command: `gpupdate /force`</span></span>
3. <span data-ttu-id="afd9e-197">Reinicie o computador para que a instalação ocorra.</span><span class="sxs-lookup"><span data-stu-id="afd9e-197">You must restart the machine for the installation to take place.</span></span> <span data-ttu-id="afd9e-198">A inicialização poderá demorar consideravelmente mais do que o normal durante a instalação da extensão.</span><span class="sxs-lookup"><span data-stu-id="afd9e-198">Bootup may take significantly more time than usual while the extension installs.</span></span>
4. <span data-ttu-id="afd9e-199">Depois de reiniciar, abra o **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="afd9e-199">After restarting, open **Internet Explorer**.</span></span> <span data-ttu-id="afd9e-200">No canto superior direito da janela, clique em **Ferramentas** (ícone de engrenagem) e, em seguida, selecione **Gerenciar complementos**.</span><span class="sxs-lookup"><span data-stu-id="afd9e-200">On the upper-right corner of the window, click **Tools** (the gear icon), and then select **Manage add-ons**.</span></span>
   
    ![Vá para Ferramentas > Gerenciar Complementos](./media/active-directory-saas-ie-group-policy/manage-add-ons.png)
5. <span data-ttu-id="afd9e-202">Na janela **Gerenciar Complementos**, verifique se a **Extensão do Painel de Acesso** foi instalada e se seu **Status** foi definido como **Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="afd9e-202">In the **Manage Add-ons** window, verify that the **Access Panel Extension** has been installed and that its **Status** has been set to **Enabled**.</span></span>
   
    ![Verifique se a Extensão do Painel de Acesso está instalada e habilitada.](./media/active-directory-saas-ie-group-policy/verify-install.png)

## <a name="related-articles"></a><span data-ttu-id="afd9e-204">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="afd9e-204">Related Articles</span></span>
* [<span data-ttu-id="afd9e-205">Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="afd9e-205">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="afd9e-206">Acesso a aplicativos e logon único com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="afd9e-206">Application access and single sign-on with Azure Active Directory</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="afd9e-207">Solucionando problemas da extensão do painel de acesso para o Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="afd9e-207">Troubleshooting the Access Panel Extension for Internet Explorer</span></span>](active-directory-saas-ie-troubleshooting.md)

