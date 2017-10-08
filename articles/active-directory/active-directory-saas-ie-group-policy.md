---
title: "Extensão do painel de acesso do Azure para o IE usando um GPO de aaaDeploy | Microsoft Docs"
description: "Como toouse agrupar complemento do política toodeploy saudação do Internet Explorer para o portal de meus aplicativos hello."
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
ms.openlocfilehash: 926f15950bbe81d2fbfe1b0b856470da40880d7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-hello-access-panel-extension-for-internet-explorer-using-group-policy"></a><span data-ttu-id="d6c93-103">Como tooDeploy Olá extensão do painel de acesso do Internet Explorer usando a diretiva de grupo</span><span class="sxs-lookup"><span data-stu-id="d6c93-103">How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy</span></span>
<span data-ttu-id="d6c93-104">Este tutorial mostra como toouse tooremotely de política de grupo instalar extensão do painel de acesso de saudação do Internet Explorer em computadores de seus usuários.</span><span class="sxs-lookup"><span data-stu-id="d6c93-104">This tutorial shows how toouse group policy tooremotely install hello Access Panel extension for Internet Explorer on your users' machines.</span></span> <span data-ttu-id="d6c93-105">Essa extensão é necessária para usuários do Internet Explorer que precisam de toosign em aplicativos que são configurados usando [com base em senha de logon único](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="d6c93-105">This extension is required for Internet Explorer users who need toosign into apps that are configured using [password-based single sign-on](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).</span></span>

<span data-ttu-id="d6c93-106">É recomendável que administradores automatizarem a implantação de saudação da extensão.</span><span class="sxs-lookup"><span data-stu-id="d6c93-106">It is recommended that admins automate hello deployment of this extension.</span></span> <span data-ttu-id="d6c93-107">Caso contrário, os usuários têm toodownload e instalarem extensão Olá por conta própria, que é toouser propensas a erros e requer permissões de administrador.</span><span class="sxs-lookup"><span data-stu-id="d6c93-107">Otherwise, users have toodownload and install hello extension themselves, which is prone toouser error and requires administrator permissions.</span></span> <span data-ttu-id="d6c93-108">Este tutorial apresenta um método de automatização de implantações de software usando a política de grupo.</span><span class="sxs-lookup"><span data-stu-id="d6c93-108">This tutorial covers one method of automating software deployments by using group policy.</span></span> [<span data-ttu-id="d6c93-109">Saiba mais sobre a política de grupo.</span><span class="sxs-lookup"><span data-stu-id="d6c93-109">Learn more about group policy.</span></span>](https://technet.microsoft.com/windowsserver/bb310732.aspx)

<span data-ttu-id="d6c93-110">Olá extensão do painel de acesso também está disponível para [Chrome](https://go.microsoft.com/fwLink/?LinkID=311859) e [Firefox](https://go.microsoft.com/fwLink/?LinkID=626998), nenhum deles exigem tooinstall de permissões de administrador.</span><span class="sxs-lookup"><span data-stu-id="d6c93-110">hello Access Panel extension is also available for [Chrome](https://go.microsoft.com/fwLink/?LinkID=311859) and [Firefox](https://go.microsoft.com/fwLink/?LinkID=626998), neither of which require administrator permissions tooinstall.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6c93-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d6c93-111">Prerequisites</span></span>
* <span data-ttu-id="d6c93-112">Você configurou o [serviços de domínio do Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), e você tiver ingressado domínio de tooyour máquinas dos usuários.</span><span class="sxs-lookup"><span data-stu-id="d6c93-112">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines tooyour domain.</span></span>
* <span data-ttu-id="d6c93-113">Você deve ter hello "Editar configurações de" permissão tooedit Olá objeto de política de grupo (GPO).</span><span class="sxs-lookup"><span data-stu-id="d6c93-113">You must have hello "Edit settings" permission tooedit hello Group Policy Object (GPO).</span></span> <span data-ttu-id="d6c93-114">Por padrão, membros da saudação grupos de segurança a seguir têm essa permissão: os administradores de domínio, administradores de empresa e proprietários de criadores de diretiva de grupo.</span><span class="sxs-lookup"><span data-stu-id="d6c93-114">By default, members of hello following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> [<span data-ttu-id="d6c93-115">Saiba mais.</span><span class="sxs-lookup"><span data-stu-id="d6c93-115">Learn more.</span></span>](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx)

## <a name="step-1-create-hello-distribution-point"></a><span data-ttu-id="d6c93-116">Etapa 1: Criar um ponto de distribuição de saudação</span><span class="sxs-lookup"><span data-stu-id="d6c93-116">Step 1: Create hello Distribution Point</span></span>
<span data-ttu-id="d6c93-117">Primeiro, você deve colocar o pacote do instalador Olá em um local de rede que pode ser acessado por máquinas de saudação que desejar extensão de saudação do tooremotely instalar em.</span><span class="sxs-lookup"><span data-stu-id="d6c93-117">First, you must place hello installer package on a network location that can be accessed by hello machines that you wish tooremotely install hello extension on.</span></span> <span data-ttu-id="d6c93-118">toodo isso, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="d6c93-118">toodo this, follow these steps:</span></span>

1. <span data-ttu-id="d6c93-119">Faça logon no servidor toohello como um administrador</span><span class="sxs-lookup"><span data-stu-id="d6c93-119">Log on toohello server as an administrator</span></span>
2. <span data-ttu-id="d6c93-120">Em Olá **Gerenciador do servidor** janela, ir muito**arquivos e serviços de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="d6c93-120">In hello **Server Manager** window, go too**Files and Storage Services**.</span></span>
   
    ![Abrir Serviços de Arquivo e Armazenamento](./media/active-directory-saas-ie-group-policy/files-services.png)
3. <span data-ttu-id="d6c93-122">Vá toohello **compartilhamentos** guia. Em seguida, clique em **Tarefas** > **Novo Compartilhamento...**</span><span class="sxs-lookup"><span data-stu-id="d6c93-122">Go toohello **Shares** tab. Then click **Tasks** > **New Share...**</span></span>
   
    ![Abrir Serviços de Arquivo e Armazenamento](./media/active-directory-saas-ie-group-policy/shares.png)
4. <span data-ttu-id="d6c93-124">Olá completa **Assistente de novo compartilhamento** e tooensure do conjunto de permissões que ele possa ser acessado de computadores dos usuários.</span><span class="sxs-lookup"><span data-stu-id="d6c93-124">Complete hello **New Share Wizard** and set permissions tooensure that it can be accessed from your users' machines.</span></span> [<span data-ttu-id="d6c93-125">Saiba mais sobre compartilhamentos.</span><span class="sxs-lookup"><span data-stu-id="d6c93-125">Learn more about shares.</span></span>](https://technet.microsoft.com/library/cc753175.aspx)
5. <span data-ttu-id="d6c93-126">Baixar Olá pacote do Microsoft Windows Installer (arquivo. msi) a seguir: [Extension.msi do painel de acesso](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi)</span><span class="sxs-lookup"><span data-stu-id="d6c93-126">Download hello following Microsoft Windows Installer package (.msi file): [Access Panel Extension.msi](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi)</span></span>
6. <span data-ttu-id="d6c93-127">Copie o local de tooa desejado no compartilhamento de saudação do pacote hello instalador.</span><span class="sxs-lookup"><span data-stu-id="d6c93-127">Copy hello installer package tooa desired location on hello share.</span></span>
   
    ![Copie o compartilhamento de toohello de arquivo hello. msi.](./media/active-directory-saas-ie-group-policy/copy-package.png)
7. <span data-ttu-id="d6c93-129">Verifique se as máquinas cliente tooaccess capaz de pacote do instalador de saudação do compartilhamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="d6c93-129">Verify that your client machines are able tooaccess hello installer package from hello share.</span></span> 

## <a name="step-2-create-hello-group-policy-object"></a><span data-ttu-id="d6c93-130">Etapa 2: Criar hello objeto de diretiva de grupo</span><span class="sxs-lookup"><span data-stu-id="d6c93-130">Step 2: Create hello Group Policy Object</span></span>
1. <span data-ttu-id="d6c93-131">Faça logon no servidor de toohello que hospeda sua instalação de serviços de domínio Active Directory (AD DS).</span><span class="sxs-lookup"><span data-stu-id="d6c93-131">Log on toohello server that hosts your Active Directory Domain Services (AD DS) installation.</span></span>
2. <span data-ttu-id="d6c93-132">No Gerenciador do servidor de saudação, vá muito**ferramentas** > **Group Policy Management**.</span><span class="sxs-lookup"><span data-stu-id="d6c93-132">In hello Server Manager, go too**Tools** > **Group Policy Management**.</span></span>
   
    ![Vá tooTools > Gerenciamento de diretiva de grupo](./media/active-directory-saas-ie-group-policy/tools-gpm.png)
3. <span data-ttu-id="d6c93-134">No painel esquerdo de saudação do hello **Group Policy Management** janela, exibir sua hierarquia de unidade organizacional (UO) e determinar em qual escopo você gostaria que a política de grupo tooapply hello.</span><span class="sxs-lookup"><span data-stu-id="d6c93-134">In hello left pane of hello **Group Policy Management** window, view your Organizational Unit (OU) hierarchy and determine at which scope you would like tooapply hello group policy.</span></span> <span data-ttu-id="d6c93-135">Por exemplo, você pode decidir toopick um pequeno toodeploy tooa da UO poucos usuários de teste, ou você pode escolher uma nível superior OU toodeploy tooyour toda a organização.</span><span class="sxs-lookup"><span data-stu-id="d6c93-135">For instance, you may decide toopick a small OU toodeploy tooa few users for testing, or you may pick a top-level OU toodeploy tooyour entire organization.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d6c93-136">Se você deseja toocreate ou editar suas unidades organizacionais (UOs), alternar toohello back Gerenciador do servidor e vá muito**ferramentas** > **computadores e usuários do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d6c93-136">If you would like toocreate or edit your Organization Units (OUs), switch back toohello Server Manager and go too**Tools** > **Active Directory Users and Computers**.</span></span>
   > 
   > 
4. <span data-ttu-id="d6c93-137">Depois de selecionar uma UO, clique com o botão direito do mouse nela e selecione **Criar um GPO neste domínio e vinculá-lo aqui...**</span><span class="sxs-lookup"><span data-stu-id="d6c93-137">Once you have selected an OU, right-click it and select **Create a GPO in this domain, and Link it here...**</span></span>
   
    ![Criar um novo GPO](./media/active-directory-saas-ie-group-policy/create-gpo.png)
5. <span data-ttu-id="d6c93-139">Em Olá **novo GPO** prompt, digite um nome para Olá novo objeto de diretiva de grupo.</span><span class="sxs-lookup"><span data-stu-id="d6c93-139">In hello **New GPO** prompt, type in a name for hello new Group Policy Object.</span></span>
   
    ![Nome hello novo GPO](./media/active-directory-saas-ie-group-policy/name-gpo.png)
6. <span data-ttu-id="d6c93-141">Com o botão direito Olá objeto de política de grupo que você criou e selecione **editar**.</span><span class="sxs-lookup"><span data-stu-id="d6c93-141">Right-click hello Group Policy Object that you created, and select **Edit**.</span></span>
   
    ![Editar saudação novo GPO](./media/active-directory-saas-ie-group-policy/edit-gpo.png)

## <a name="step-3-assign-hello-installation-package"></a><span data-ttu-id="d6c93-143">Etapa 3: Atribuir Olá pacote de instalação</span><span class="sxs-lookup"><span data-stu-id="d6c93-143">Step 3: Assign hello Installation Package</span></span>
1. <span data-ttu-id="d6c93-144">Determinar se você gostaria que a extensão de saudação toodeploy com base em **configuração do computador** ou **configuração do usuário**.</span><span class="sxs-lookup"><span data-stu-id="d6c93-144">Determine whether you would like toodeploy hello extension based on **Computer Configuration** or **User Configuration**.</span></span> <span data-ttu-id="d6c93-145">Ao usar [configuração do computador](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx), extensão hello está instalado no computador de hello, independentemente de qual os usuários fazem logon tooit.</span><span class="sxs-lookup"><span data-stu-id="d6c93-145">When using [computer configuration](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx), hello extension is installed on hello computer regardless of which users log on tooit.</span></span> <span data-ttu-id="d6c93-146">Com [configuração do usuário](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx), os usuários têm a extensão de saudação instalado para eles, independentemente de quais computadores fazem logon.</span><span class="sxs-lookup"><span data-stu-id="d6c93-146">With [user configuration](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx), users have hello extension installed for them regardless of which computers they log on to.</span></span>
2. <span data-ttu-id="d6c93-147">No painel esquerdo de saudação do hello **Editor de gerenciamento de política de grupo** janela, vá tooeither de saudação caminhos de pastas, dependendo do tipo de configuração que você escolheu a seguir:</span><span class="sxs-lookup"><span data-stu-id="d6c93-147">In hello left pane of hello **Group Policy Management Editor** window, go tooeither of hello following folder paths, depending on which type of configuration you chose:</span></span>
   
   * `Computer Configuration/Policies/Software Settings/`
   * `User Configuration/Policies/Software Settings/`
3. <span data-ttu-id="d6c93-148">Clique com o botão direito do mouse em **Instalação do software** e selecione **Novo** > **Pacote...**</span><span class="sxs-lookup"><span data-stu-id="d6c93-148">Right-click **Software installation**, then select **New** > **Package...**</span></span>
   
    ![Criar um novo pacote de instalação de software](./media/active-directory-saas-ie-group-policy/new-package.png)
4. <span data-ttu-id="d6c93-150">Vá toohello pasta compartilhada que contém o pacote do instalador de saudação do [etapa 1: criar um ponto de distribuição de saudação](#step-1-create-the-distribution-point), selecione o arquivo. msi de saudação e clique em **abrir**.</span><span class="sxs-lookup"><span data-stu-id="d6c93-150">Go toohello shared folder that contains hello installer package from [Step 1: Create hello Distribution Point](#step-1-create-the-distribution-point), select hello .msi file, and click **Open**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="d6c93-151">Se Olá compartilhamento esteja localizado no mesmo servidor, verifique se você está acessando o. msi de saudação por meio do caminho do arquivo de rede hello, em vez de caminho do arquivo local hello.</span><span class="sxs-lookup"><span data-stu-id="d6c93-151">If hello share is located on this same server, verify that you are accessing hello .msi through hello network file path, rather than hello local file path.</span></span>
   > 
   > 
   
    ![Selecione o pacote de instalação de saudação da pasta compartilhada hello.](./media/active-directory-saas-ie-group-policy/select-package.png)
5. <span data-ttu-id="d6c93-153">Em Olá **implantar Software** prompt, selecione **atribuído** para o método de implantação.</span><span class="sxs-lookup"><span data-stu-id="d6c93-153">In hello **Deploy Software** prompt, select **Assigned** for your deployment method.</span></span> <span data-ttu-id="d6c93-154">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="d6c93-154">Then click **OK**.</span></span>
   
    ![Selecione Atribuído e clique em OK.](./media/active-directory-saas-ie-group-policy/deployment-method.png)

<span data-ttu-id="d6c93-156">extensão de saudação agora está implantado toohello UO que você selecionou.</span><span class="sxs-lookup"><span data-stu-id="d6c93-156">hello extension is now deployed toohello OU that you selected.</span></span> [<span data-ttu-id="d6c93-157">Saiba mais sobre a instalação do Software de Política de Grupo.</span><span class="sxs-lookup"><span data-stu-id="d6c93-157">Learn more about Group Policy Software Installation.</span></span>](https://technet.microsoft.com/library/cc738858%28v=ws.10%29.aspx)

## <a name="step-4-auto-enable-hello-extension-for-internet-explorer"></a><span data-ttu-id="d6c93-158">Etapa 4: Saudação de ativação automática extensão para o Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="d6c93-158">Step 4: Auto-Enable hello Extension for Internet Explorer</span></span>
<span data-ttu-id="d6c93-159">Além disso toorunning Olá installer, todas as extensões para o Internet Explorer deve ser explicitamente ativado antes de ser usada.</span><span class="sxs-lookup"><span data-stu-id="d6c93-159">In addition toorunning hello installer, every extension for Internet Explorer must be explicitly enabled before it can be used.</span></span> <span data-ttu-id="d6c93-160">Siga as etapas de saudação abaixo tooenable Olá extensão do painel de acesso usando a política de grupo:</span><span class="sxs-lookup"><span data-stu-id="d6c93-160">Follow hello steps below tooenable hello Access Panel Extension using group policy:</span></span>

1. <span data-ttu-id="d6c93-161">Em Olá **Editor de gerenciamento de política de grupo** janela, vá tooeither de saudação seguintes caminhos, dependendo do tipo de configuração que você escolheu na [etapa 3: atribuir Olá pacote de instalação](#step-3-assign-the-installation-package):</span><span class="sxs-lookup"><span data-stu-id="d6c93-161">In hello **Group Policy Management Editor** window, go tooeither of hello following paths, depending on which type of configuration you chose in [Step 3: Assign hello Installation Package](#step-3-assign-the-installation-package):</span></span>
   
   * `Computer Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
2. <span data-ttu-id="d6c93-162">Clique com o botão direito do mouse em **Lista de Complementos** e selecione **Editar**.</span><span class="sxs-lookup"><span data-stu-id="d6c93-162">Right-click **Add-on List**, and select **Edit**.</span></span>
    <span data-ttu-id="d6c93-163">![Edite a Lista de Complementos.](./media/active-directory-saas-ie-group-policy/edit-add-on-list.png)</span><span class="sxs-lookup"><span data-stu-id="d6c93-163">![Edit Add-on List.](./media/active-directory-saas-ie-group-policy/edit-add-on-list.png)</span></span>
3. <span data-ttu-id="d6c93-164">Em Olá **lista de complementos** janela, selecione **habilitado**.</span><span class="sxs-lookup"><span data-stu-id="d6c93-164">In hello **Add-on List** window, select **Enabled**.</span></span> <span data-ttu-id="d6c93-165">Em seguida, em Olá **opções** seção, clique em **Mostrar...** .</span><span class="sxs-lookup"><span data-stu-id="d6c93-165">Then, under hello **Options** section, click **Show...**.</span></span>
   
    ![Clique em Habilitar e clique em Mostrar...](./media/active-directory-saas-ie-group-policy/edit-add-on-list-window.png)
4. <span data-ttu-id="d6c93-167">Em Olá **Mostrar conteúdo** janela, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d6c93-167">In hello **Show Contents** window, perform hello following steps:</span></span>
   
   1. <span data-ttu-id="d6c93-168">Para a coluna primeiro hello (Olá **nome do valor** campo), copiar e colar Olá identificação de classe a seguir:`{030E9A3F-7B18-4122-9A60-B87235E4F59E}`</span><span class="sxs-lookup"><span data-stu-id="d6c93-168">For hello first column (hello **Value Name** field), copy and paste hello following Class ID: `{030E9A3F-7B18-4122-9A60-B87235E4F59E}`</span></span>
   2. <span data-ttu-id="d6c93-169">Segunda coluna de hello (Olá **valor** campo), tipo no seguinte valor de saudação:`1`</span><span class="sxs-lookup"><span data-stu-id="d6c93-169">For hello second column (hello **Value** field), type in hello following value: `1`</span></span>
   3. <span data-ttu-id="d6c93-170">Clique em **Okey** tooclose Olá **Mostrar conteúdo** janela.</span><span class="sxs-lookup"><span data-stu-id="d6c93-170">Click **OK** tooclose hello **Show Contents** window.</span></span>
      
      ![Preencha os valores hello especificados acima.](./media/active-directory-saas-ie-group-policy/show-contents.png)
5. <span data-ttu-id="d6c93-172">Clique em **Okey** tooapply suas alterações e fechar Olá **lista de complementos** janela.</span><span class="sxs-lookup"><span data-stu-id="d6c93-172">Click **OK** tooapply your changes and close hello **Add-on List** window.</span></span>

<span data-ttu-id="d6c93-173">Olá extensão deve agora ser habilitada para máquinas Olá Olá selecionado UO.</span><span class="sxs-lookup"><span data-stu-id="d6c93-173">hello extension should now be enabled for hello machines in hello selected OU.</span></span> [<span data-ttu-id="d6c93-174">Saiba mais sobre como usar tooenable de diretiva de grupo ou desabilite complementos do Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="d6c93-174">Learn more about using group policy tooenable or disable Internet Explorer add-ons.</span></span>](https://technet.microsoft.com/library/dn454941.aspx)

## <a name="step-5-optional-disable-remember-password-prompt"></a><span data-ttu-id="d6c93-175">Etapa 5 (opcional): Desabilitar o prompt "Lembrar senha"</span><span class="sxs-lookup"><span data-stu-id="d6c93-175">Step 5 (Optional): Disable "Remember Password" Prompt</span></span>
<span data-ttu-id="d6c93-176">Quando usando Olá extensão do painel de acesso de usuários entrar toowebsites, Internet Explorer pode mostrar a seguir Olá prompt perguntando "deseja toostore sua senha?"</span><span class="sxs-lookup"><span data-stu-id="d6c93-176">When users sign-in toowebsites using hello Access Panel Extension, Internet Explorer may show hello following prompt asking "Would you like toostore your password?"</span></span>

![](./media/active-directory-saas-ie-group-policy/remember-password-prompt.png)

<span data-ttu-id="d6c93-177">Se você desejar tooprevent que os usuários vejam esse prompt, siga as etapas de saudação abaixo tooprevent preenchimento automático de senhas reconheçam:</span><span class="sxs-lookup"><span data-stu-id="d6c93-177">If you wish tooprevent your users from seeing this prompt, then follow hello steps below tooprevent auto-complete from remembering passwords:</span></span>

1. <span data-ttu-id="d6c93-178">Em Olá **Editor de gerenciamento de política de grupo** janela, vá toohello caminho listado abaixo.</span><span class="sxs-lookup"><span data-stu-id="d6c93-178">In hello **Group Policy Management Editor** window, go toohello path listed below.</span></span> <span data-ttu-id="d6c93-179">Essa configuração só está disponível em **Configuração do usuário**.</span><span class="sxs-lookup"><span data-stu-id="d6c93-179">This configuration setting is only available under **User Configuration**.</span></span>
   
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/`
2. <span data-ttu-id="d6c93-180">Localizar configuração Olá denominada **ativar o recurso de preenchimento automático de saudação para nomes de usuário e senhas em formulários**.</span><span class="sxs-lookup"><span data-stu-id="d6c93-180">Find hello setting named **Turn on hello auto-complete feature for user names and passwords on forms**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d6c93-181">Versões anteriores do Active Directory podem listar essa configuração com o nome da saudação **não permitir senha de preenchimento automático toosave**.</span><span class="sxs-lookup"><span data-stu-id="d6c93-181">Previous versions of Active Directory may list this setting with hello name **Do not allow auto-complete toosave passwords**.</span></span> <span data-ttu-id="d6c93-182">configuração Olá para essa configuração é diferente da saudação configuração descrito neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="d6c93-182">hello configuration for that setting differs from hello setting described in this tutorial.</span></span>
   > 
   > 
   
    ![Lembre-se toolook para isso em configurações de usuário.](./media/active-directory-saas-ie-group-policy/disable-auto-complete.png)
3. <span data-ttu-id="d6c93-184">Olá acima configuração clique com botão direito e selecione **editar**.</span><span class="sxs-lookup"><span data-stu-id="d6c93-184">Right click hello above setting, and select **Edit**.</span></span>
4. <span data-ttu-id="d6c93-185">Na janela de saudação intitulada **ativar o recurso de preenchimento automático de saudação para nomes de usuário e senhas em formulários**, selecione **desabilitado**.</span><span class="sxs-lookup"><span data-stu-id="d6c93-185">In hello window titled **Turn on hello auto-complete feature for user names and passwords on forms**, select **Disabled**.</span></span>
   
    ![Selecione Desabilitar](./media/active-directory-saas-ie-group-policy/disable-passwords.png)
5. <span data-ttu-id="d6c93-187">Clique em **Okey** tooapply essas alterações e a janela de saudação fechar.</span><span class="sxs-lookup"><span data-stu-id="d6c93-187">Click **OK** tooapply these changes and close hello window.</span></span>

<span data-ttu-id="d6c93-188">Usuários não serão ser capaz de toostore suas credenciais ou usar credenciais de preenchimento automático tooaccess armazenado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d6c93-188">Users will no longer be able toostore their credentials or use auto-complete tooaccess previously stored credentials.</span></span> <span data-ttu-id="d6c93-189">No entanto, essa política permitem que os usuários toocontinue toouse preenchimento automático para outros tipos de campos de formulário, como campos de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="d6c93-189">However, this policy does allow users toocontinue toouse auto-complete for other types of form fields, such as search fields.</span></span>

> [!WARNING]
> <span data-ttu-id="d6c93-190">Se essa política está habilitada depois que os usuários escolheu toostore algumas credenciais, a política será *não* Limpar credenciais Olá que já foram armazenadas.</span><span class="sxs-lookup"><span data-stu-id="d6c93-190">If this policy is enabled after users have chosen toostore some credentials, this policy will *not* clear hello credentials that have already been stored.</span></span>
> 
> 

## <a name="step-6-testing-hello-deployment"></a><span data-ttu-id="d6c93-191">Etapa 6: Teste implantação</span><span class="sxs-lookup"><span data-stu-id="d6c93-191">Step 6: Testing hello Deployment</span></span>
<span data-ttu-id="d6c93-192">Siga as etapas de saudação abaixo tooverify se Olá extensão implantação foi bem-sucedida:</span><span class="sxs-lookup"><span data-stu-id="d6c93-192">Follow hello steps below tooverify if hello extension deployment was successful:</span></span>

1. <span data-ttu-id="d6c93-193">Se você implantou usando **configuração do computador**, logon em um computador cliente que pertence a toohello UO que você selecionou na [etapa 2: criar hello GPO](#step-2-create-the-group-policy-object).</span><span class="sxs-lookup"><span data-stu-id="d6c93-193">If you deployed using **Computer Configuration**, sign into a client machine that belongs toohello OU that you selected in [Step 2: Create hello Group Policy Object](#step-2-create-the-group-policy-object).</span></span> <span data-ttu-id="d6c93-194">Se você implantou usando **configuração do usuário**, verifique se toosign em como um usuário que pertence a toothat UO.</span><span class="sxs-lookup"><span data-stu-id="d6c93-194">If you deployed using **User Configuration**, make sure toosign in as a user who belongs toothat OU.</span></span>
2. <span data-ttu-id="d6c93-195">Pode levar alguns sinal ins Olá de diretiva de grupo altera toofully atualização com esse computador.</span><span class="sxs-lookup"><span data-stu-id="d6c93-195">It may take a couple sign ins for hello group policy changes toofully update with this machine.</span></span> <span data-ttu-id="d6c93-196">atualização do tooforce hello, abra um **Prompt de comando** janela e execução hello comando a seguir:`gpupdate /force`</span><span class="sxs-lookup"><span data-stu-id="d6c93-196">tooforce hello update, open a **Command Prompt** window and run hello following command: `gpupdate /force`</span></span>
3. <span data-ttu-id="d6c93-197">Você deve reiniciar a máquina Olá para local de tootake instalação Olá.</span><span class="sxs-lookup"><span data-stu-id="d6c93-197">You must restart hello machine for hello installation tootake place.</span></span> <span data-ttu-id="d6c93-198">Inicialização pode levar consideravelmente mais tempo do que o normal ao extensão Olá instala.</span><span class="sxs-lookup"><span data-stu-id="d6c93-198">Bootup may take significantly more time than usual while hello extension installs.</span></span>
4. <span data-ttu-id="d6c93-199">Depois de reiniciar, abra o **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="d6c93-199">After restarting, open **Internet Explorer**.</span></span> <span data-ttu-id="d6c93-200">No hello canto direito superior da janela de saudação, clique em **ferramentas** (ícone de engrenagem Olá) e, em seguida, selecione **gerenciar complementos**.</span><span class="sxs-lookup"><span data-stu-id="d6c93-200">On hello upper-right corner of hello window, click **Tools** (hello gear icon), and then select **Manage add-ons**.</span></span>
   
    ![Vá tooTools > Gerenciar complementos](./media/active-directory-saas-ie-group-policy/manage-add-ons.png)
5. <span data-ttu-id="d6c93-202">Em Olá **gerenciar complementos** janela, verifique se esse Olá **extensão do painel de acesso** foi instalado e que seu **Status** foi definido muito**habilitado**.</span><span class="sxs-lookup"><span data-stu-id="d6c93-202">In hello **Manage Add-ons** window, verify that hello **Access Panel Extension** has been installed and that its **Status** has been set too**Enabled**.</span></span>
   
    ![Verifique se esse Olá extensão do painel de acesso está instalado e habilitado.](./media/active-directory-saas-ie-group-policy/verify-install.png)

## <a name="related-articles"></a><span data-ttu-id="d6c93-204">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="d6c93-204">Related Articles</span></span>
* [<span data-ttu-id="d6c93-205">Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="d6c93-205">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="d6c93-206">Acesso a aplicativos e logon único com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="d6c93-206">Application access and single sign-on with Azure Active Directory</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="d6c93-207">Solução de problemas Olá extensão do painel de acesso para o Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="d6c93-207">Troubleshooting hello Access Panel Extension for Internet Explorer</span></span>](active-directory-saas-ie-troubleshooting.md)

