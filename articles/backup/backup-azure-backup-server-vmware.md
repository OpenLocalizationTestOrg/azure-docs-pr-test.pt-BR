---
title: aaaBack os servidores do VMware com o servidor de Backup do Azure | Microsoft Docs
description: "Use o Azure Backup Server tooback um VMware vCenter/ESX servidores tooAzure ou disco. Este artigo fornece instruções passo a passo para fazer backup (ou proteger) suas cargas de trabalho do VMware."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
ms.assetid: 6b131caf-de85-4eba-b8e6-d8a04545cd9d
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/24/2017
ms.author: markgal;
ms.openlocfilehash: 3edb6880a526ed0b18605fee0fac27196a608e7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-vmware-server-tooazure"></a><span data-ttu-id="26d1a-104">Fazer backup de um tooAzure de servidor do VMware</span><span class="sxs-lookup"><span data-stu-id="26d1a-104">Back up a VMware server tooAzure</span></span>

<span data-ttu-id="26d1a-105">Este artigo explica como tooconfigure Azure Backup Server toohelp proteger cargas de trabalho de servidor VMware.</span><span class="sxs-lookup"><span data-stu-id="26d1a-105">This article explains how tooconfigure Azure Backup Server toohelp protect VMware server workloads.</span></span> <span data-ttu-id="26d1a-106">Este artigo pressupõe que você já tenha o Servidor de Backup do Azure instalado.</span><span class="sxs-lookup"><span data-stu-id="26d1a-106">This article assumes you already have Azure Backup Server installed.</span></span> <span data-ttu-id="26d1a-107">Se você não tiver o Azure Backup Server instalado, consulte [preparar tooback cargas de trabalho usando o servidor de Backup do Azure](backup-azure-microsoft-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="26d1a-107">If you don't have Azure Backup Server installed, see [Prepare tooback up workloads using Azure Backup Server](backup-azure-microsoft-azure-backup.md).</span></span>

<span data-ttu-id="26d1a-108">O Servidor de Backup do Azure pode fazer backup ou ajudar a proteger o VMware vCenter Server versão 6.5, 6.0 e 5.5.</span><span class="sxs-lookup"><span data-stu-id="26d1a-108">Azure Backup Server can back up, or help protect, VMware vCenter Server version 6.5, 6.0 and 5.5.</span></span>


## <a name="create-a-secure-connection-toohello-vcenter-server"></a><span data-ttu-id="26d1a-109">Criar um servidor do vCenter toohello conexão segura</span><span class="sxs-lookup"><span data-stu-id="26d1a-109">Create a secure connection toohello vCenter Server</span></span>

<span data-ttu-id="26d1a-110">Por padrão, o Servidor de Backup do Azure se comunica com cada vCenter Server por um canal HTTPS.</span><span class="sxs-lookup"><span data-stu-id="26d1a-110">By default, Azure Backup Server communicates with each vCenter Server via an HTTPS channel.</span></span> <span data-ttu-id="26d1a-111">tooturn na comunicação segura hello, recomendamos que você instale o certificado de autoridade de certificação do VMware (CA) de saudação no servidor de Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="26d1a-111">tooturn on hello secure communication, we recommend that you install hello VMware Certificate Authority (CA) certificate on Azure Backup Server.</span></span> <span data-ttu-id="26d1a-112">Se você não exige comunicação segura e prefere requisito do toodisable Olá HTTPS, consulte [protocolo de comunicação seguro desabilitar](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol).</span><span class="sxs-lookup"><span data-stu-id="26d1a-112">If you don't require secure communication, and would prefer toodisable hello HTTPS requirement, see [Disable secure communication protocol](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol).</span></span> <span data-ttu-id="26d1a-113">toocreate uma conexão segura entre o servidor de Backup do Azure e Olá servidor vCenter, importe o certificado de confiança de saudação no servidor de Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="26d1a-113">toocreate a secure connection between Azure Backup Server and hello vCenter Server, import hello trusted certificate on Azure Backup Server.</span></span>

<span data-ttu-id="26d1a-114">Normalmente, você usa um navegador no hello Azure Backup Server máquina tooconnect toohello vCenter Server via Olá vSphere cliente Web.</span><span class="sxs-lookup"><span data-stu-id="26d1a-114">Typically, you use a browser on hello Azure Backup Server machine tooconnect toohello vCenter Server via hello vSphere Web Client.</span></span> <span data-ttu-id="26d1a-115">Olá primeira vez que você usar o hello Azure Backup Server navegador tooconnect toohello vCenter Server, conexão Olá não é segura.</span><span class="sxs-lookup"><span data-stu-id="26d1a-115">hello first time you use hello Azure Backup Server browser tooconnect toohello vCenter Server, hello connection isn't secure.</span></span> <span data-ttu-id="26d1a-116">Olá a imagem a seguir mostra uma conexão não segura de saudação.</span><span class="sxs-lookup"><span data-stu-id="26d1a-116">hello following image shows hello unsecured connection.</span></span>

![Exemplo de conexão não segura tooVMware servidor](./media/backup-azure-backup-server-vmware/unsecure-url.png)

<span data-ttu-id="26d1a-118">toofix esse problema e criar uma conexão segura, baixe os certificados da AC raiz confiável de saudação.</span><span class="sxs-lookup"><span data-stu-id="26d1a-118">toofix this issue, and create a secure connection, download hello trusted root CA certificates.</span></span>

1. <span data-ttu-id="26d1a-119">No navegador de saudação no servidor de Backup do Azure, digite Olá URL toohello vSphere cliente Web.</span><span class="sxs-lookup"><span data-stu-id="26d1a-119">In hello browser on Azure Backup Server, enter hello URL toohello vSphere Web Client.</span></span> <span data-ttu-id="26d1a-120">página de logon de cliente Web Hello vSphere é exibida.</span><span class="sxs-lookup"><span data-stu-id="26d1a-120">hello vSphere Web Client login page appears.</span></span>

    ![Cliente Web vSphere](./media/backup-azure-backup-server-vmware/vsphere-web-client.png)

    <span data-ttu-id="26d1a-122">Na parte inferior de saudação de informações de saudação para administradores e desenvolvedores, localize Olá **certificados de autoridade de certificação raiz confiável para Download** link.</span><span class="sxs-lookup"><span data-stu-id="26d1a-122">At hello bottom of hello information for administrators and developers, locate hello **Download trusted root CA certificates** link.</span></span>

    ![Certificados de CA raiz do link toodownload Olá confiável](./media/backup-azure-backup-server-vmware/vmware-download-ca-cert-prompt.png)

  <span data-ttu-id="26d1a-124">Se você não vir a página de logon de cliente Web hello vSphere, verifique as configurações de proxy do navegador.</span><span class="sxs-lookup"><span data-stu-id="26d1a-124">If you don't see hello vSphere Web Client login page, check your browser's proxy settings.</span></span>

2. <span data-ttu-id="26d1a-125">Clique em **Baixar certificados de autoridade de certificação raiz confiável**.</span><span class="sxs-lookup"><span data-stu-id="26d1a-125">Click **Download trusted root CA certificates**.</span></span>

    <span data-ttu-id="26d1a-126">Servidor do vCenter Olá baixa um computador local do arquivo tooyour.</span><span class="sxs-lookup"><span data-stu-id="26d1a-126">hello vCenter Server downloads a file tooyour local computer.</span></span> <span data-ttu-id="26d1a-127">Olá nome do arquivo é nomeado **baixar**.</span><span class="sxs-lookup"><span data-stu-id="26d1a-127">hello file's name is named **download**.</span></span> <span data-ttu-id="26d1a-128">Dependendo de seu navegador, você receberá uma mensagem perguntando se tooopen ou salvar o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="26d1a-128">Depending on your browser, you receive a message that asks whether tooopen or save hello file.</span></span>

    ![Baixar a mensagem quando certificados são baixados](./media/backup-azure-backup-server-vmware/download-certs.png)

3. <span data-ttu-id="26d1a-130">Olá arquivo tooa local para salvar no servidor de Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="26d1a-130">Save hello file tooa location on Azure Backup Server.</span></span> <span data-ttu-id="26d1a-131">Quando você salvar o arquivo hello, adicione a extensão de nome de arquivo hello. zip.</span><span class="sxs-lookup"><span data-stu-id="26d1a-131">When you save hello file, add hello .zip file name extension.</span></span>

    <span data-ttu-id="26d1a-132">arquivo Hello é um arquivo. zip que contém informações de saudação sobre certificados de saudação.</span><span class="sxs-lookup"><span data-stu-id="26d1a-132">hello file is a .zip file that contains hello information about hello certificates.</span></span> <span data-ttu-id="26d1a-133">Com a extensão. zip de hello, você pode usar ferramentas de extração de saudação.</span><span class="sxs-lookup"><span data-stu-id="26d1a-133">With hello .zip extension, you can use hello extraction tools.</span></span>

4. <span data-ttu-id="26d1a-134">Clique com botão direito **download.zip**e, em seguida, selecione **extrair tudo** tooextract conteúdo de saudação.</span><span class="sxs-lookup"><span data-stu-id="26d1a-134">Right-click **download.zip**, and then select **Extract All** tooextract hello contents.</span></span>

    <span data-ttu-id="26d1a-135">arquivo. zip de saudação extrai sua pasta de tooa conteúdo denominada **certificados**.</span><span class="sxs-lookup"><span data-stu-id="26d1a-135">hello .zip file extracts its contents tooa folder named **certs**.</span></span> <span data-ttu-id="26d1a-136">Dois tipos de arquivos aparecem na pasta de certificados de saudação.</span><span class="sxs-lookup"><span data-stu-id="26d1a-136">Two types of files appear in hello certs folder.</span></span> <span data-ttu-id="26d1a-137">arquivo do certificado raiz Olá tem uma extensão que começa com uma sequência numerada como.0 e.1.</span><span class="sxs-lookup"><span data-stu-id="26d1a-137">hello root certificate file has an extension that begins with a numbered sequence like .0 and .1.</span></span>
    
    <span data-ttu-id="26d1a-138">arquivo de lista de certificados Revogados Olá tem uma extensão que começa com uma sequência como .r0 ou .r1.</span><span class="sxs-lookup"><span data-stu-id="26d1a-138">hello CRL file has an extension that begins with a sequence like .r0 or .r1.</span></span> <span data-ttu-id="26d1a-139">arquivo de lista de certificados Revogados Hello está associado um certificado.</span><span class="sxs-lookup"><span data-stu-id="26d1a-139">hello CRL file is associated with a certificate.</span></span>

    ![<span data-ttu-id="26d1a-140">Baixar o arquivo extraído localmente</span><span class="sxs-lookup"><span data-stu-id="26d1a-140">Download file extracted locally</span></span> ](./media/backup-azure-backup-server-vmware/extracted-files-in-certs-folder.png)

5. <span data-ttu-id="26d1a-141">Em Olá **certificados** pasta, clique no arquivo do certificado raiz Olá e clique **Renomear**.</span><span class="sxs-lookup"><span data-stu-id="26d1a-141">In hello **certs** folder, right-click hello root certificate file, and then click **Rename**.</span></span>

    ![<span data-ttu-id="26d1a-142">Renomear o certificado raiz</span><span class="sxs-lookup"><span data-stu-id="26d1a-142">Rename root certificate</span></span> ](./media/backup-azure-backup-server-vmware/rename-cert.png)

    <span data-ttu-id="26d1a-143">Alteração extensão too.crt do certificado de raiz Olá.</span><span class="sxs-lookup"><span data-stu-id="26d1a-143">Change hello root certificate's extension too.crt.</span></span> <span data-ttu-id="26d1a-144">Quando você for questionado se deseja que a extensão de saudação toochange, clique em **Sim** ou **Okey**.</span><span class="sxs-lookup"><span data-stu-id="26d1a-144">When you're asked if you're sure you want toochange hello extension, click **Yes** or **OK**.</span></span> <span data-ttu-id="26d1a-145">Caso contrário, você pode alterar função pretendido do arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="26d1a-145">Otherwise, you change hello file's intended function.</span></span> <span data-ttu-id="26d1a-146">ícone Olá Olá alterações tooan ícone do arquivo que representa um certificado raiz.</span><span class="sxs-lookup"><span data-stu-id="26d1a-146">hello icon for hello file changes tooan icon that represents a root certificate.</span></span>

6. <span data-ttu-id="26d1a-147">Certificado de raiz hello e menu pop-up de saudação, selecione **Instalar certificado**.</span><span class="sxs-lookup"><span data-stu-id="26d1a-147">Right-click hello root certificate and from hello pop-up menu, select **Install Certificate**.</span></span>

    <span data-ttu-id="26d1a-148">Olá **Assistente de importação de certificado** caixa de diálogo é exibida.</span><span class="sxs-lookup"><span data-stu-id="26d1a-148">hello **Certificate Import Wizard** dialog box appears.</span></span>

7. <span data-ttu-id="26d1a-149">Em Olá **Assistente de importação de certificado** caixa de diálogo, selecione **Máquina Local** como destino Olá Olá certificado e clique **próximo** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="26d1a-149">In hello **Certificate Import Wizard** dialog box, select **Local Machine** as hello destination for hello certificate, and then click **Next** toocontinue.</span></span>

    ![<span data-ttu-id="26d1a-150">Opções de destino do armazenamento de certificados</span><span class="sxs-lookup"><span data-stu-id="26d1a-150">Certificate storage destination options</span></span> ](./media/backup-azure-backup-server-vmware/certificate-import-wizard1.png)

    <span data-ttu-id="26d1a-151">Se você for questionado se deseja que o computador de toohello do tooallow alterações, clique em **Sim** ou **Okey**, alterações de saudação tooall.</span><span class="sxs-lookup"><span data-stu-id="26d1a-151">If you're asked if you want tooallow changes toohello computer, click **Yes** or **OK**, tooall hello changes.</span></span>

8. <span data-ttu-id="26d1a-152">Em Olá **repositório de certificados** página, selecione **colocar todos os certificados no hello repositório a seguir**e, em seguida, clique em **procurar** toochoose repositório de certificados de saudação.</span><span class="sxs-lookup"><span data-stu-id="26d1a-152">On hello **Certificate Store** page, select **Place all certificates in hello following store**, and then click **Browse** toochoose hello certificate store.</span></span>

    ![Colocar os certificados em um ponto de armazenamento específico](./media/backup-azure-backup-server-vmware/cert-import-wizard-local-store.png)

    <span data-ttu-id="26d1a-154">Olá **Selecionar repositório de certificados** caixa de diálogo é exibida.</span><span class="sxs-lookup"><span data-stu-id="26d1a-154">hello **Select Certificate Store** dialog box appears.</span></span>

    ![Hierarquia de pastas do armazenamento de certificados](./media/backup-azure-backup-server-vmware/cert-store.png)

9. <span data-ttu-id="26d1a-156">Selecione **autoridades de certificação raiz confiáveis** como pasta de destino Olá para certificados hello e clique **Okey**.</span><span class="sxs-lookup"><span data-stu-id="26d1a-156">Select **Trusted Root Certification Authorities** as hello destination folder for hello certificates, and then click **OK**.</span></span>

    ![Pasta de destino do certificado](./media/backup-azure-backup-server-vmware/certificate-store-selected.png)

    <span data-ttu-id="26d1a-158">Olá **autoridades de certificação raiz confiáveis** pasta é confirmada como repositório de certificados de saudação.</span><span class="sxs-lookup"><span data-stu-id="26d1a-158">hello **Trusted Root Certification Authorities** folder is confirmed as hello certificate store.</span></span> <span data-ttu-id="26d1a-159">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="26d1a-159">Click **Next**.</span></span>

    ![Pasta de repositório de certificados](./media/backup-azure-backup-server-vmware/certificate-import-wizard2.png)

10. <span data-ttu-id="26d1a-161">Em Olá **Olá Concluindo o Assistente de importação de certificado** página, verifique se esse certificado Olá está na pasta desejada Olá e, em seguida, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="26d1a-161">On hello **Completing hello Certificate Import Wizard** page, verify that hello certificate is in hello desired folder, and then click **Finish**.</span></span>

    ![Verifique se o certificado está na pasta adequada Olá](./media/backup-azure-backup-server-vmware/cert-wizard-final-screen.png)

    <span data-ttu-id="26d1a-163">Importação de certificado bem-sucedida Olá aparecerá uma caixa de diálogo é confirmada.</span><span class="sxs-lookup"><span data-stu-id="26d1a-163">A dialog box appears, hello successful certificate import is confirmed.</span></span>

11. <span data-ttu-id="26d1a-164">Entrar no vCenter toohello tooconfirm de servidor que a conexão é segura.</span><span class="sxs-lookup"><span data-stu-id="26d1a-164">Sign in toohello vCenter Server tooconfirm that your connection is secure.</span></span>

  <span data-ttu-id="26d1a-165">Se a importação de certificados de saudação não for bem-sucedida, e você não pode estabelecer uma conexão segura, consulte documentação do hello VMware vSphere em [obter certificados de servidor](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).</span><span class="sxs-lookup"><span data-stu-id="26d1a-165">If hello certificate import is not successful, and you cannot establish a secure connection, consult hello VMware vSphere documentation on [obtaining server certificates](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).</span></span>

  <span data-ttu-id="26d1a-166">Se você tiver limites de segurança dentro da sua organização e não quiser tooturn em Olá protocolo HTTPS, use Olá proteger as comunicações para Olá toodisable procedimento a seguir.</span><span class="sxs-lookup"><span data-stu-id="26d1a-166">If you have secure boundaries within your organization, and don't want tooturn on hello HTTPS protocol, use hello following procedure toodisable hello secure communications.</span></span>

### <a name="disable-secure-communication-protocol"></a><span data-ttu-id="26d1a-167">Desabilite seu protocolo de comunicação segura</span><span class="sxs-lookup"><span data-stu-id="26d1a-167">Disable secure communication protocol</span></span>

<span data-ttu-id="26d1a-168">Se sua organização não exigir o protocolo HTTPS de saudação, use Olá etapas toodisable HTTPS a seguir.</span><span class="sxs-lookup"><span data-stu-id="26d1a-168">If your organization doesn't require hello HTTPS protocol, use hello following steps toodisable HTTPS.</span></span> <span data-ttu-id="26d1a-169">toodisable Olá comportamento padrão, crie uma chave do registro que ignora o comportamento padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="26d1a-169">toodisable hello default behavior, create a registry key that ignores hello default behavior.</span></span>

1. <span data-ttu-id="26d1a-170">Copie e cole Olá texto a seguir em um arquivo. txt.</span><span class="sxs-lookup"><span data-stu-id="26d1a-170">Copy and paste hello following text into a .txt file.</span></span>

  ```
  Windows Registry Editor Version 5.00
  [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\VMWare]
  "IgnoreCertificateValidation"=dword:00000001
  ```

2. <span data-ttu-id="26d1a-171">Salve o computador de servidor de Backup do Azure de tooyour de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="26d1a-171">Save hello file tooyour Azure Backup Server computer.</span></span> <span data-ttu-id="26d1a-172">Nome de arquivo hello, use DisableSecureAuthentication.reg.</span><span class="sxs-lookup"><span data-stu-id="26d1a-172">For hello file name, use DisableSecureAuthentication.reg.</span></span>

3. <span data-ttu-id="26d1a-173">Clique duas vezes em entrada de registro do hello arquivo tooactivate hello.</span><span class="sxs-lookup"><span data-stu-id="26d1a-173">Double-click hello file tooactivate hello registry entry.</span></span>


## <a name="create-a-role-and-user-account-on-hello-vcenter-server"></a><span data-ttu-id="26d1a-174">Criar uma conta de usuário e a função no servidor do vCenter Olá</span><span class="sxs-lookup"><span data-stu-id="26d1a-174">Create a role and user account on hello vCenter Server</span></span>

<span data-ttu-id="26d1a-175">No servidor do vCenter hello, uma função é um conjunto predefinido de privilégios.</span><span class="sxs-lookup"><span data-stu-id="26d1a-175">On hello vCenter Server, a role is a predefined set of privileges.</span></span> <span data-ttu-id="26d1a-176">Um administrador de servidor do vCenter cria funções hello.</span><span class="sxs-lookup"><span data-stu-id="26d1a-176">A vCenter Server administrator creates hello roles.</span></span> <span data-ttu-id="26d1a-177">permissões de tooassign administrador Olá pares contas de usuário com uma função.</span><span class="sxs-lookup"><span data-stu-id="26d1a-177">tooassign permissions, hello administrator pairs user accounts with a role.</span></span> <span data-ttu-id="26d1a-178">tooestablish Olá usuário necessárias credenciais tooback o computador de servidor do vCenter Olá, criar uma função com privilégios específicos e associar conta de usuário Olá função hello.</span><span class="sxs-lookup"><span data-stu-id="26d1a-178">tooestablish hello necessary user credentials tooback up hello vCenter Server computer, create a role with specific privileges, and then associate hello user account with hello role.</span></span>

<span data-ttu-id="26d1a-179">Servidor de Backup do Azure usa um nome de usuário e senha tooauthenticate com o servidor do vCenter hello.</span><span class="sxs-lookup"><span data-stu-id="26d1a-179">Azure Backup Server uses a username and password tooauthenticate with hello vCenter Server.</span></span> <span data-ttu-id="26d1a-180">O Servidor de Backup do Azure utiliza essas credenciais como autenticação para todas as operações de backup.</span><span class="sxs-lookup"><span data-stu-id="26d1a-180">Azure Backup Server uses these credentials as authentication for all backup operations.</span></span>

<span data-ttu-id="26d1a-181">tooadd um função de servidor do vCenter e seus privilégios para um administrador de backup:</span><span class="sxs-lookup"><span data-stu-id="26d1a-181">tooadd a vCenter Server role and its privileges for a backup administrator:</span></span>

1. <span data-ttu-id="26d1a-182">Entrar no servidor do vCenter toohello e, em seguida, no servidor do vCenter Olá **navegador** do painel, clique em **administração**.</span><span class="sxs-lookup"><span data-stu-id="26d1a-182">Sign in toohello vCenter Server, and then in hello vCenter Server **Navigator** panel, click **Administration**.</span></span>

    ![Opção de administração no painel Navegador do vCenter Server](./media/backup-azure-backup-server-vmware/vmware-navigator-panel.png)

2. <span data-ttu-id="26d1a-184">Em **administração** selecione **funções**e, em seguida, em Olá **funções** clique de painel Olá Adicionar ícone de função (Olá + símbolo).</span><span class="sxs-lookup"><span data-stu-id="26d1a-184">In **Administration** select **Roles**, and then in hello **Roles** panel click hello add role icon (hello + symbol).</span></span>

    ![Adicionar função](./media/backup-azure-backup-server-vmware/vmware-define-new-role.png)

    <span data-ttu-id="26d1a-186">Olá **Criar função** caixa de diálogo é exibida.</span><span class="sxs-lookup"><span data-stu-id="26d1a-186">hello **Create Role** dialog box appears.</span></span>

    ![Criar função](./media/backup-azure-backup-server-vmware/vmware-define-new-role-priv.png)

3. <span data-ttu-id="26d1a-188">Em Olá **Criar função** caixa de diálogo Olá **nome da função** , digite *BackupAdminRole*.</span><span class="sxs-lookup"><span data-stu-id="26d1a-188">In hello **Create Role** dialog box, in hello **Role name** box, enter *BackupAdminRole*.</span></span> <span data-ttu-id="26d1a-189">nome da função Hello pode ser como desejar, mas ele deve ser reconhecível para a finalidade da função hello.</span><span class="sxs-lookup"><span data-stu-id="26d1a-189">hello role name can be whatever you like, but it should be recognizable for hello role's purpose.</span></span>

4. <span data-ttu-id="26d1a-190">Selecione Olá privilégios para a versão apropriada de saudação do vCenter e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="26d1a-190">Select hello privileges for hello appropriate version of vCenter, and then click **OK**.</span></span> <span data-ttu-id="26d1a-191">Olá, a tabela a seguir identifica os privilégios de Olá necessária para vCenter 6.0 e vCenter 5.5.</span><span class="sxs-lookup"><span data-stu-id="26d1a-191">hello following table identifies hello required privileges for vCenter 6.0 and vCenter 5.5.</span></span>

  <span data-ttu-id="26d1a-192">Quando você seleciona privilégios hello, clique em Olá ícone próximo toohello pai rótulo tooexpand Olá pai e o modo de exibição Olá filho privilégios.</span><span class="sxs-lookup"><span data-stu-id="26d1a-192">When you select hello privileges, click hello icon next toohello parent label tooexpand hello parent and view hello child privileges.</span></span> <span data-ttu-id="26d1a-193">privilégios de máquina virtual de saudação tooselect, você precisa toogo vários níveis em Olá pai de hierarquia filho.</span><span class="sxs-lookup"><span data-stu-id="26d1a-193">tooselect hello VirtualMachine privileges, you need toogo several levels into hello parent child hierarchy.</span></span> <span data-ttu-id="26d1a-194">Você não precisa tooselect todos os privilégios do filho dentro de um privilégio de pai.</span><span class="sxs-lookup"><span data-stu-id="26d1a-194">You don't need tooselect all child privileges within a parent privilege.</span></span>

  ![Hierarquia de privilégios pai-filho](./media/backup-azure-backup-server-vmware/cert-add-privilege-expand.png)

  <span data-ttu-id="26d1a-196">Depois de clicar em **Okey**, Olá nova função é exibida na lista de saudação no painel de funções hello.</span><span class="sxs-lookup"><span data-stu-id="26d1a-196">After you click **OK**, hello new role appears in hello list on hello Roles panel.</span></span>

|<span data-ttu-id="26d1a-197">Privilégios do vCenter 6.0</span><span class="sxs-lookup"><span data-stu-id="26d1a-197">Privileges for vCenter 6.0</span></span>| <span data-ttu-id="26d1a-198">Privilégios do vCenter 5.5</span><span class="sxs-lookup"><span data-stu-id="26d1a-198">Privileges for vCenter 5.5</span></span>|
|--------------------------|---------------------------|
|<span data-ttu-id="26d1a-199">Datastore.AllocateSpace</span><span class="sxs-lookup"><span data-stu-id="26d1a-199">Datastore.AllocateSpace</span></span>   | <span data-ttu-id="26d1a-200">Datastore.AllocateSpace</span><span class="sxs-lookup"><span data-stu-id="26d1a-200">Datastore.AllocateSpace</span></span>|
|<span data-ttu-id="26d1a-201">Global.ManageCustomFields</span><span class="sxs-lookup"><span data-stu-id="26d1a-201">Global.ManageCustomFields</span></span> | <span data-ttu-id="26d1a-202">Global.ManageCustomerFields</span><span class="sxs-lookup"><span data-stu-id="26d1a-202">Global.ManageCustomerFields</span></span>|
|<span data-ttu-id="26d1a-203">Global.SetCustomFields</span><span class="sxs-lookup"><span data-stu-id="26d1a-203">Global.SetCustomFields</span></span>    |   |
|<span data-ttu-id="26d1a-204">Host.Local.CreateVM</span><span class="sxs-lookup"><span data-stu-id="26d1a-204">Host.Local.CreateVM</span></span>       | <span data-ttu-id="26d1a-205">Network.Assign</span><span class="sxs-lookup"><span data-stu-id="26d1a-205">Network.Assign</span></span> |
|<span data-ttu-id="26d1a-206">Network.Assign</span><span class="sxs-lookup"><span data-stu-id="26d1a-206">Network.Assign</span></span>            |  |
|<span data-ttu-id="26d1a-207">Resource.AssignVMToPool</span><span class="sxs-lookup"><span data-stu-id="26d1a-207">Resource.AssignVMToPool</span></span>   |  |
|<span data-ttu-id="26d1a-208">VirtualMachine.Config.AddNewDisk</span><span class="sxs-lookup"><span data-stu-id="26d1a-208">VirtualMachine.Config.AddNewDisk</span></span>  | <span data-ttu-id="26d1a-209">VirtualMachine.Config.AddNewDisk</span><span class="sxs-lookup"><span data-stu-id="26d1a-209">VirtualMachine.Config.AddNewDisk</span></span>   |
|<span data-ttu-id="26d1a-210">VirtualMachine.Config.AdvanceConfig</span><span class="sxs-lookup"><span data-stu-id="26d1a-210">VirtualMachine.Config.AdvanceConfig</span></span>| <span data-ttu-id="26d1a-211">VirtualMachine.Config.AdvancedConfig</span><span class="sxs-lookup"><span data-stu-id="26d1a-211">VirtualMachine.Config.AdvancedConfig</span></span>|
|<span data-ttu-id="26d1a-212">VirtualMachine.Config.ChangeTracking</span><span class="sxs-lookup"><span data-stu-id="26d1a-212">VirtualMachine.Config.ChangeTracking</span></span>| <span data-ttu-id="26d1a-213">VirtualMachine.Config.ChangeTracking</span><span class="sxs-lookup"><span data-stu-id="26d1a-213">VirtualMachine.Config.ChangeTracking</span></span> |
|<span data-ttu-id="26d1a-214">VirtualMachine.Config.HostUSBDevice</span><span class="sxs-lookup"><span data-stu-id="26d1a-214">VirtualMachine.Config.HostUSBDevice</span></span>||
|<span data-ttu-id="26d1a-215">VirtualMachine.Config.QueryUnownedFiles</span><span class="sxs-lookup"><span data-stu-id="26d1a-215">VirtualMachine.Config.QueryUnownedFiles</span></span>|    |
|<span data-ttu-id="26d1a-216">VirtualMachine.Config.SwapPlacement</span><span class="sxs-lookup"><span data-stu-id="26d1a-216">VirtualMachine.Config.SwapPlacement</span></span>| <span data-ttu-id="26d1a-217">VirtualMachine.Config.SwapPlacement</span><span class="sxs-lookup"><span data-stu-id="26d1a-217">VirtualMachine.Config.SwapPlacement</span></span> |
|<span data-ttu-id="26d1a-218">VirtualMachine.Interact.PowerOff</span><span class="sxs-lookup"><span data-stu-id="26d1a-218">VirtualMachine.Interact.PowerOff</span></span>| <span data-ttu-id="26d1a-219">VirtualMachine.Interact.PowerOff</span><span class="sxs-lookup"><span data-stu-id="26d1a-219">VirtualMachine.Interact.PowerOff</span></span> |
|<span data-ttu-id="26d1a-220">VirtualMachine.Inventory.Create</span><span class="sxs-lookup"><span data-stu-id="26d1a-220">VirtualMachine.Inventory.Create</span></span>| <span data-ttu-id="26d1a-221">VirtualMachine.Inventory.Create</span><span class="sxs-lookup"><span data-stu-id="26d1a-221">VirtualMachine.Inventory.Create</span></span> |
|<span data-ttu-id="26d1a-222">VirtualMachine.Provisioning.DiskRandomAccess</span><span class="sxs-lookup"><span data-stu-id="26d1a-222">VirtualMachine.Provisioning.DiskRandomAccess</span></span>| |
|<span data-ttu-id="26d1a-223">VirtualMachine.Provisioning.DiskRandomRead</span><span class="sxs-lookup"><span data-stu-id="26d1a-223">VirtualMachine.Provisioning.DiskRandomRead</span></span>|<span data-ttu-id="26d1a-224">VirtualMachine.Provisioning.DiskRandomRead</span><span class="sxs-lookup"><span data-stu-id="26d1a-224">VirtualMachine.Provisioning.DiskRandomRead</span></span> |
|<span data-ttu-id="26d1a-225">VirtualMachine.State.CreateSnapshot</span><span class="sxs-lookup"><span data-stu-id="26d1a-225">VirtualMachine.State.CreateSnapshot</span></span>| <span data-ttu-id="26d1a-226">VirtualMachine.State.CreateSnapshot</span><span class="sxs-lookup"><span data-stu-id="26d1a-226">VirtualMachine.State.CreateSnapshot</span></span>|
|<span data-ttu-id="26d1a-227">VirtualMachine.State.RemoveSnapshot</span><span class="sxs-lookup"><span data-stu-id="26d1a-227">VirtualMachine.State.RemoveSnapshot</span></span>|<span data-ttu-id="26d1a-228">VirtualMachine.State.RemoveSnapshot</span><span class="sxs-lookup"><span data-stu-id="26d1a-228">VirtualMachine.State.RemoveSnapshot</span></span> |
</br>



## <a name="create-a-vcenter-server-user-account-and-permissions"></a><span data-ttu-id="26d1a-229">Criar uma conta de usuário do vCenter Server e as permissões</span><span class="sxs-lookup"><span data-stu-id="26d1a-229">Create a vCenter Server user account and permissions</span></span>

<span data-ttu-id="26d1a-230">Depois de configurar a função hello com privilégios, crie uma conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="26d1a-230">After hello role with privileges is set up, create a user account.</span></span> <span data-ttu-id="26d1a-231">conta de usuário de saudação tem um nome e uma senha, que fornece credenciais de saudação que são usadas para autenticação.</span><span class="sxs-lookup"><span data-stu-id="26d1a-231">hello user account has a name and password, which provides hello credentials that are used for authentication.</span></span>

1. <span data-ttu-id="26d1a-232">toocreate uma conta de usuário no servidor do vCenter Olá **navegador** do painel, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="26d1a-232">toocreate a user account, in hello vCenter Server **Navigator** panel, click **Users and Groups**.</span></span>

    ![Opção de Usuários e Grupos](./media/backup-azure-backup-server-vmware/vmware-userandgroup-panel.png)

    <span data-ttu-id="26d1a-234">Olá **vCenter usuários e grupos** painel é exibido.</span><span class="sxs-lookup"><span data-stu-id="26d1a-234">hello **vCenter Users and Groups** panel appears.</span></span>

    ![Painel Usuários e Grupos do vCenter](./media/backup-azure-backup-server-vmware/usersandgroups.png)

2. <span data-ttu-id="26d1a-236">Em Olá **vCenter usuários e grupos** painel, selecione Olá **usuários** guia e, em seguida, clique em Olá Adicionar ícone de usuários (Olá + símbolo).</span><span class="sxs-lookup"><span data-stu-id="26d1a-236">In hello **vCenter Users and Groups** panel, select hello **Users** tab, and then click hello add users icon (hello + symbol).</span></span>

    <span data-ttu-id="26d1a-237">Olá **novo usuário** caixa de diálogo é exibida.</span><span class="sxs-lookup"><span data-stu-id="26d1a-237">hello **New User** dialog box appears.</span></span>

3. <span data-ttu-id="26d1a-238">Em Olá **novo usuário** caixa de diálogo caixa, adicione informações de saudação do usuário e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="26d1a-238">In hello **New User** dialog box, add hello user's information and then click **OK**.</span></span> <span data-ttu-id="26d1a-239">Neste procedimento, o nome de usuário de saudação é BackupAdmin.</span><span class="sxs-lookup"><span data-stu-id="26d1a-239">In this procedure, hello username is BackupAdmin.</span></span>

    ![Caixa de diálogo Novo Usuário](./media/backup-azure-backup-server-vmware/vmware-new-user-account.png)

    <span data-ttu-id="26d1a-241">nova conta de usuário Olá aparece na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="26d1a-241">hello new user account appears in hello list.</span></span>

4. <span data-ttu-id="26d1a-242">conta de usuário de saudação tooassociate na função hello, em Olá **navegador** do painel, clique em **permissões globais**.</span><span class="sxs-lookup"><span data-stu-id="26d1a-242">tooassociate hello user account with hello role, in hello **Navigator** panel, click **Global Permissions**.</span></span> <span data-ttu-id="26d1a-243">Em Olá **permissões globais** painel, selecione Olá **gerenciar** guia e, em seguida, clique em Olá Adicionar ícone (Olá + símbolo).</span><span class="sxs-lookup"><span data-stu-id="26d1a-243">In hello **Global Permissions** panel, select hello **Manage** tab, and then click hello add icon (hello + symbol).</span></span>

    ![Painel Permissões Globais](./media/backup-azure-backup-server-vmware/vmware-add-new-perms.png)

    <span data-ttu-id="26d1a-245">Olá **raiz de permissões globais - adicionar permissão** caixa de diálogo é exibida.</span><span class="sxs-lookup"><span data-stu-id="26d1a-245">hello **Global Permissions Root - Add Permission** dialog box appears.</span></span>

5. <span data-ttu-id="26d1a-246">Em Olá **raiz de permissão Global - adicionar permissão** caixa de diálogo, clique em **adicionar** toochoose Olá usuário ou grupo.</span><span class="sxs-lookup"><span data-stu-id="26d1a-246">In hello **Global Permission Root - Add Permission** dialog box, click **Add** toochoose hello user or group.</span></span>

    ![Escolher o usuário ou o grupo](./media/backup-azure-backup-server-vmware/vmware-add-new-global-perm.png)

    <span data-ttu-id="26d1a-248">Olá **selecionar usuários/grupos** caixa de diálogo é exibida.</span><span class="sxs-lookup"><span data-stu-id="26d1a-248">hello **Select Users/Groups** dialog box appears.</span></span>

6. <span data-ttu-id="26d1a-249">Em Olá **selecionar usuários/grupos** caixa de diálogo caixa, escolha **BackupAdmin** e, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="26d1a-249">In hello **Select Users/Groups** dialog box, choose **BackupAdmin** and then click **Add**.</span></span>

    <span data-ttu-id="26d1a-250">Em **usuários**, Olá *domínio \ nomedeusuário* formato é usado para a conta de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="26d1a-250">In **Users**, hello *domain\username* format is used for hello user account.</span></span> <span data-ttu-id="26d1a-251">Se você quiser toouse um domínio diferente, escolha-o no hello **domínio** lista.</span><span class="sxs-lookup"><span data-stu-id="26d1a-251">If you want toouse a different domain, choose it from hello **Domain** list.</span></span>

    ![Adicionar um usuário BackupAdmin](./media/backup-azure-backup-server-vmware/vmware-assign-account-to-role.png)

    <span data-ttu-id="26d1a-253">Clique em **Okey** tooadd Olá selecionado usuários toohello **adicionar permissão** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="26d1a-253">Click **OK** tooadd hello selected users toohello **Add Permission** dialog box.</span></span>

7. <span data-ttu-id="26d1a-254">Agora que você identificou que o usuário hello, atribua a função de toohello de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="26d1a-254">Now that you've identified hello user, assign hello user toohello role.</span></span> <span data-ttu-id="26d1a-255">Em **função atribuída**, na lista suspensa de Olá, selecione **BackupAdminRole**e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="26d1a-255">In **Assigned Role**, from hello drop-down list, select **BackupAdminRole**, and then click **OK**.</span></span>

    ![Atribuir o usuário toorole](./media/backup-azure-backup-server-vmware/vmware-choose-role.png)

  <span data-ttu-id="26d1a-257">Em Olá **gerenciar** guia Olá **permissões globais** painel, a nova conta de usuário hello e função hello associado aparecem na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="26d1a-257">On hello **Manage** tab in hello **Global Permissions** panel, hello new user account and hello associated role appear in hello list.</span></span>


## <a name="establish-vcenter-server-credentials-on-azure-backup-server"></a><span data-ttu-id="26d1a-258">Estabelecer as credenciais de servidor do vCenter no servidor de Backup do Azure</span><span class="sxs-lookup"><span data-stu-id="26d1a-258">Establish vCenter Server credentials on Azure Backup Server</span></span>

<span data-ttu-id="26d1a-259">Antes de adicionar Olá VMware server tooAzure fazer Backup do servidor, instale o [atualização 1 para o Azure Backup Server](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).</span><span class="sxs-lookup"><span data-stu-id="26d1a-259">Before you add hello VMware server tooAzure Backup Server, install [Update 1 for Azure Backup Server](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).</span></span>

1. <span data-ttu-id="26d1a-260">tooopen servidor de Backup do Azure, clique duas vezes o ícone de saudação na área de trabalho do hello Azure Backup Server.</span><span class="sxs-lookup"><span data-stu-id="26d1a-260">tooopen Azure Backup Server, double-click hello icon on hello Azure Backup Server desktop.</span></span>

    ![Ícone do Servidor de Backup do Azure](./media/backup-azure-backup-server-vmware/mabs-icon.png)

    <span data-ttu-id="26d1a-262">Se você não encontrar o ícone de saudação na área de trabalho hello, abra o Azure Backup Server da lista de saudação dos aplicativos instalados.</span><span class="sxs-lookup"><span data-stu-id="26d1a-262">If you can't find hello icon on hello desktop, open Azure Backup Server from hello list of installed apps.</span></span> <span data-ttu-id="26d1a-263">nome do aplicativo de servidor de Backup do Azure Olá é chamado de Backup do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="26d1a-263">hello Azure Backup Server app name is called Microsoft Azure Backup.</span></span>

2. <span data-ttu-id="26d1a-264">No console do servidor de Backup do Azure hello, clique em **gerenciamento**, clique em **servidores de produção**e clique na faixa de opções de ferramenta hello, **VMware gerenciar**.</span><span class="sxs-lookup"><span data-stu-id="26d1a-264">In hello Azure Backup Server console, click **Management**, click **Production Servers**, and then on hello tool ribbon, click **Manage VMware**.</span></span>

    ![Console do Servidor de Backup do Azure](./media/backup-azure-backup-server-vmware/add-vmware-credentials.png)

    <span data-ttu-id="26d1a-266">Olá **gerenciar credenciais** caixa de diálogo é exibida.</span><span class="sxs-lookup"><span data-stu-id="26d1a-266">hello **Manage Credentials** dialog box appears.</span></span>

    ![Caixa de diálogo Gerenciar Credenciais do Servidor de Backup do Azure](./media/backup-azure-backup-server-vmware/mabs-manage-credentials-dialog.png)

3. <span data-ttu-id="26d1a-268">Em Olá **gerenciar credenciais** caixa de diálogo, clique em **adicionar** tooopen Olá **Add Credential** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="26d1a-268">In hello **Manage Credentials** dialog box, click **Add** tooopen hello **Add Credential** dialog box.</span></span>

4. <span data-ttu-id="26d1a-269">Em Olá **Add Credential** caixa de diálogo, digite um nome e uma descrição para a nova credencial de saudação.</span><span class="sxs-lookup"><span data-stu-id="26d1a-269">In hello **Add Credential** dialog box, enter a name and a description for hello new credential.</span></span> <span data-ttu-id="26d1a-270">Em seguida, especifique Olá nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="26d1a-270">Then specify hello username and password.</span></span> <span data-ttu-id="26d1a-271">nome Hello, *Contoso Vcenter credencial* usado credencial de saudação tooidentify no procedimento a seguir Olá.</span><span class="sxs-lookup"><span data-stu-id="26d1a-271">hello name, *Contoso Vcenter credential* is used tooidentify hello credential in hello next procedure.</span></span> <span data-ttu-id="26d1a-272">Use Olá mesmo nome de usuário e senha que é usada para Olá vCenter Server.</span><span class="sxs-lookup"><span data-stu-id="26d1a-272">Use hello same username and password that is used for hello vCenter Server.</span></span> <span data-ttu-id="26d1a-273">Se o servidor do vCenter hello e servidor de Backup do Azure não estão no Olá mesmo domínio, em **nome de usuário**, especifique o domínio de saudação.</span><span class="sxs-lookup"><span data-stu-id="26d1a-273">If hello vCenter Server and Azure Backup Server are not in hello same domain, in **User name**, specify hello domain.</span></span>

    ![Caixa de diálogo Adicionar Credencial do Servidor de Backup do Azure](./media/backup-azure-backup-server-vmware/mabs-add-credential-dialog2.png)

    <span data-ttu-id="26d1a-275">Clique em **adicionar** tooadd Olá nova credencial tooAzure fazer Backup do servidor.</span><span class="sxs-lookup"><span data-stu-id="26d1a-275">Click **Add** tooadd hello new credential tooAzure Backup Server.</span></span> <span data-ttu-id="26d1a-276">nova credencial de saudação aparece na lista de saudação no hello **gerenciar credenciais** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="26d1a-276">hello new credential appears in hello list in hello **Manage Credentials** dialog box.</span></span>
    
    ![Caixa de diálogo Gerenciar Credenciais do Servidor de Backup do Azure](./media/backup-azure-backup-server-vmware/new-list-of-mabs-creds.png)

5. <span data-ttu-id="26d1a-278">Olá tooclose **gerenciar credenciais** caixa de diálogo, clique em Olá **X** no canto superior direito de saudação.</span><span class="sxs-lookup"><span data-stu-id="26d1a-278">tooclose hello **Manage Credentials** dialog box, click hello **X** in hello upper-right corner.</span></span>


## <a name="add-hello-vcenter-server-tooazure-backup-server"></a><span data-ttu-id="26d1a-279">Adicionar Olá vCenter Server tooAzure fazer Backup do servidor</span><span class="sxs-lookup"><span data-stu-id="26d1a-279">Add hello vCenter Server tooAzure Backup Server</span></span>

<span data-ttu-id="26d1a-280">Assistente de adição de servidor de produção é usado tooadd Olá vCenter Server tooAzure fazer Backup do servidor.</span><span class="sxs-lookup"><span data-stu-id="26d1a-280">Production Server Addition Wizard is used tooadd hello vCenter Server tooAzure Backup Server.</span></span>

<span data-ttu-id="26d1a-281">tooopen Assistente de adição de servidor de produção, Olá completa procedimento a seguir:</span><span class="sxs-lookup"><span data-stu-id="26d1a-281">tooopen Production Server Addition Wizard, complete hello following procedure:</span></span>

1. <span data-ttu-id="26d1a-282">No console do servidor de Backup do Azure hello, clique em **gerenciamento**, clique em **servidores de produção**e, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="26d1a-282">In hello Azure Backup Server console, click **Management**, click **Production Servers**, and then click **Add**.</span></span>

    ![Abra o Assistente de Adição de Servidor de Produção](./media/backup-azure-backup-server-vmware/add-vcenter-to-mabs.png)

    <span data-ttu-id="26d1a-284">Olá **Assistente de adição de servidor de produção** caixa de diálogo é exibida.</span><span class="sxs-lookup"><span data-stu-id="26d1a-284">hello **Production Server Addition Wizard** dialog box appears.</span></span>

    ![Assistente de Adição de Servidor de Produção](./media/backup-azure-backup-server-vmware/production-server-add-wizard.png)

2. <span data-ttu-id="26d1a-286">Em Olá **tipo Selecionar servidor de produção** , selecione **servidores VMware**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="26d1a-286">On hello **Select Production Server type** page, select **VMware Servers**, and then click **Next**.</span></span>

3. <span data-ttu-id="26d1a-287">Em **endereço IP/nome do servidor**, especifique o nome de domínio totalmente qualificado da saudação (FQDN) ou endereço IP do servidor do VMware hello.</span><span class="sxs-lookup"><span data-stu-id="26d1a-287">In **Server Name/IP Address**, specify hello fully qualified domain name (FQDN) or IP address of hello VMware server.</span></span> <span data-ttu-id="26d1a-288">Se todos os servidores de ESXi Olá são gerenciados pelo Olá mesmo vCenter, você pode usar o nome hello vCenter.</span><span class="sxs-lookup"><span data-stu-id="26d1a-288">If all hello ESXi servers are managed by hello same vCenter, you can use hello vCenter name.</span></span>

    ![Especificar o FQDN ou o endereço IP do servidor do VMware](./media/backup-azure-backup-server-vmware/add-vmware-server-provide-server-name.png)

4. <span data-ttu-id="26d1a-290">Em **porta SSL**, insira a porta Olá toocommunicate usado com o servidor do VMware hello.</span><span class="sxs-lookup"><span data-stu-id="26d1a-290">In **SSL Port**, enter hello port that is used toocommunicate with hello VMware server.</span></span> <span data-ttu-id="26d1a-291">Use a porta 443, que é a porta padrão de hello, a menos que você sabe que uma porta diferente é necessária.</span><span class="sxs-lookup"><span data-stu-id="26d1a-291">Use port 443, which is hello default port, unless you know that a different port is required.</span></span>

5. <span data-ttu-id="26d1a-292">Em **especificar credenciais**, selecione Olá credencial que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="26d1a-292">In **Specify Credential**, select hello credential that you created earlier.</span></span>

    ![Especificar credencial](./media/backup-azure-backup-server-vmware/identify-creds.png)

6. <span data-ttu-id="26d1a-294">Clique em **adicionar** tooadd Olá VMware toohello lista de servidor **adicionado servidores do VMware**e, em seguida, clique em **próximo** toomove toohello próxima página no Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="26d1a-294">Click **Add** tooadd hello VMware server toohello list of **Added VMware Servers**, and then click **Next** toomove toohello next page in hello wizard.</span></span>

    ![Adicionar servidor do VMware e a credencial](./media/backup-azure-backup-server-vmware/add-vmware-server-credentials.png)

7. <span data-ttu-id="26d1a-296">Em Olá **resumo** , clique em **adicionar** tooadd Olá especificado VMware tooAzure de servidor servidor de Backup.</span><span class="sxs-lookup"><span data-stu-id="26d1a-296">In hello **Summary** page, click **Add** tooadd hello specified VMware server tooAzure Backup Server.</span></span>

    ![Adicionar VMware tooAzure de servidor servidor de Backup](./media/backup-azure-backup-server-vmware/tasks-screen.png)

  <span data-ttu-id="26d1a-298">backup do servidor VMware Olá é um backup sem agente e Olá novo servidor é adicionado imediatamente.</span><span class="sxs-lookup"><span data-stu-id="26d1a-298">hello VMware server backup is an agentless backup, and hello new server is added immediately.</span></span> <span data-ttu-id="26d1a-299">Olá **concluir** página mostra Olá resultados.</span><span class="sxs-lookup"><span data-stu-id="26d1a-299">hello **Finish** page shows you hello results.</span></span>

  ![Página Concluir](./media/backup-azure-backup-server-vmware/summary-screen.png)

  <span data-ttu-id="26d1a-301">tooadd várias instâncias do vCenter Server tooAzure servidor de Backup, repita Olá anterior as etapas nesta seção.</span><span class="sxs-lookup"><span data-stu-id="26d1a-301">tooadd multiple instances of vCenter Server tooAzure Backup Server, repeat hello previous steps in this section.</span></span>

<span data-ttu-id="26d1a-302">Depois de adicionar Olá vCenter Server tooAzure servidor de Backup, Olá próxima etapa é toocreate um grupo de proteção.</span><span class="sxs-lookup"><span data-stu-id="26d1a-302">After you add hello vCenter Server tooAzure Backup Server, hello next step is toocreate a protection group.</span></span> <span data-ttu-id="26d1a-303">grupo de proteção de saudação especifica Olá diversos detalhes para a retenção de curto e longo prazo e é onde você pode define e aplica a política de backup hello.</span><span class="sxs-lookup"><span data-stu-id="26d1a-303">hello protection group specifies hello various details for short or long-term retention, and it is where you define and apply hello backup policy.</span></span> <span data-ttu-id="26d1a-304">política de backup Olá é agenda Olá para quando os backups ocorrem e o que é feito backup.</span><span class="sxs-lookup"><span data-stu-id="26d1a-304">hello backup policy is hello schedule for when backups occur, and what is backed up.</span></span>


## <a name="configure-a-protection-group"></a><span data-ttu-id="26d1a-305">Configurar grupo de proteção</span><span class="sxs-lookup"><span data-stu-id="26d1a-305">Configure a protection group</span></span>

<span data-ttu-id="26d1a-306">Se você não tiver usado o System Center Data Protection Manager ou o servidor de Backup do Azure antes, consulte [planejar backups em disco](https://technet.microsoft.com/library/hh758026.aspx) tooprepare seu ambiente de hardware.</span><span class="sxs-lookup"><span data-stu-id="26d1a-306">If you have not used System Center Data Protection Manager or Azure Backup Server before, see [Plan for disk backups](https://technet.microsoft.com/library/hh758026.aspx) tooprepare your hardware environment.</span></span> <span data-ttu-id="26d1a-307">Depois de verificar se você tem o armazenamento adequado, use máquinas virtuais VMware de tooadd do hello criar novo grupo de proteção Assistente.</span><span class="sxs-lookup"><span data-stu-id="26d1a-307">After you check that you have proper storage, use hello Create New Protection Group wizard tooadd VMware virtual machines.</span></span>

1. <span data-ttu-id="26d1a-308">No console do servidor de Backup do Azure hello, clique em **proteção**e na faixa de opções de ferramenta hello, clique em **novo** tooopen Assistente para criar novo grupo de proteção de saudação.</span><span class="sxs-lookup"><span data-stu-id="26d1a-308">In hello Azure Backup Server console, click **Protection**, and in hello tool ribbon, click **New** tooopen hello Create New Protection Group wizard.</span></span>

    ![Assistente para criar novo grupo de proteção de Olá aberto](./media/backup-azure-backup-server-vmware/open-protection-wizard.png)

    <span data-ttu-id="26d1a-310">Olá **criar novo grupo de proteção** caixa de diálogo do assistente será exibida.</span><span class="sxs-lookup"><span data-stu-id="26d1a-310">hello **Create New Protection Group** wizard dialog box appears.</span></span>

    ![Caixa de diálogo Assistente para Criar Novo Grupo de Proteção](./media/backup-azure-backup-server-vmware/protection-wizard.png)

    <span data-ttu-id="26d1a-312">Clique em **próximo** tooadvance toohello **Selecionar tipo de grupo de proteção** página.</span><span class="sxs-lookup"><span data-stu-id="26d1a-312">Click **Next** tooadvance toohello **Select protection group type** page.</span></span>

2. <span data-ttu-id="26d1a-313">Em Olá **tipo de grupo de proteção selecione** , selecione **servidores** e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="26d1a-313">On hello **Select Protection group type** page, select **Servers** and then click **Next**.</span></span> <span data-ttu-id="26d1a-314">Olá **selecionar membros do grupo** página será exibida.</span><span class="sxs-lookup"><span data-stu-id="26d1a-314">hello **Select group members** page appears.</span></span>

3. <span data-ttu-id="26d1a-315">Em Olá **selecionar membros do grupo** página, membros disponíveis hello e membros de saudação selecionado são exibidos.</span><span class="sxs-lookup"><span data-stu-id="26d1a-315">On hello **Select group members** page, hello available members and hello selected members appear.</span></span> <span data-ttu-id="26d1a-316">Selecione Olá membros que você deseja tooprotect e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="26d1a-316">Select hello members that you want tooprotect, and then click **Next**.</span></span>

    ![Selecionar membros do grupo](./media/backup-azure-backup-server-vmware/server-add-selected-members.png)

    <span data-ttu-id="26d1a-318">Ao selecionar um membro, se você selecionar uma pasta que contém outras pastas ou VMs, essas pastas e VMs também serão selecionadas.</span><span class="sxs-lookup"><span data-stu-id="26d1a-318">When you select a member, if you select a folder that contains other folders or VMs, those folders and VMs are also selected.</span></span> <span data-ttu-id="26d1a-319">inclusão de saudação de pastas de saudação e VMs na pasta pai de saudação é chamado de proteção em nível de pasta.</span><span class="sxs-lookup"><span data-stu-id="26d1a-319">hello inclusion of hello folders and VMs in hello parent folder is called folder-level protection.</span></span> <span data-ttu-id="26d1a-320">tooremove uma pasta ou a VM, a caixa de seleção Limpar hello.</span><span class="sxs-lookup"><span data-stu-id="26d1a-320">tooremove a folder or VM, clear hello check box.</span></span>

    <span data-ttu-id="26d1a-321">Se uma VM ou uma pasta que contém uma VM, já está protegido tooAzure, você não pode selecionar o VM novamente.</span><span class="sxs-lookup"><span data-stu-id="26d1a-321">If a VM, or a folder containing a VM, is already protected tooAzure, you cannot select that VM again.</span></span> <span data-ttu-id="26d1a-322">Ou seja, depois que uma VM for tooAzure protegido, ele não pode ser protegido novamente, que impede que pontos de recuperação duplicados sejam criadas para uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="26d1a-322">That is, after a VM is protected tooAzure, it cannot be protected again, which prevents duplicate recovery points from being created for one VM.</span></span> <span data-ttu-id="26d1a-323">Se você quiser toosee qual instância de servidor de Backup do Azure já protege um membro, um nome de saudação do toohello ponto membro toosee de saudação protegendo o servidor.</span><span class="sxs-lookup"><span data-stu-id="26d1a-323">If you want toosee which Azure Backup Server instance already protects a member, point toohello member toosee hello name of hello protecting server.</span></span>

4. <span data-ttu-id="26d1a-324">Em Olá **Selecionar método de proteção de dados** , insira um nome para o grupo de proteção de saudação.</span><span class="sxs-lookup"><span data-stu-id="26d1a-324">On hello **Select Data Protection Method** page, enter a name for hello protection group.</span></span> <span data-ttu-id="26d1a-325">Proteção de curto prazo (toodisk) e online são selecionadas.</span><span class="sxs-lookup"><span data-stu-id="26d1a-325">Short-term protection (toodisk) and online protection are selected.</span></span> <span data-ttu-id="26d1a-326">Se você quiser toouse de proteção online (tooAzure), você deve usar toodisk de proteção de curto prazo.</span><span class="sxs-lookup"><span data-stu-id="26d1a-326">If you want toouse online protection (tooAzure), you must use short-term protection toodisk.</span></span> <span data-ttu-id="26d1a-327">Clique em **próximo** tooproceed toohello curto período de proteção.</span><span class="sxs-lookup"><span data-stu-id="26d1a-327">Click **Next** tooproceed toohello short-term protection range.</span></span>

    ![Selecionar método de proteção de dados](./media/backup-azure-backup-server-vmware/name-protection-group.png)

5. <span data-ttu-id="26d1a-329">Em Olá **especificar objetivos de curto prazo** página, para **período de retenção**, especifique Olá número de dias que os pontos de recuperação tooretain que estão *armazenado toodisk*.</span><span class="sxs-lookup"><span data-stu-id="26d1a-329">On hello **Specify Short-Term Goals** page, for **Retention Range**, specify hello number of days that you want tooretain recovery points that are *stored toodisk*.</span></span> <span data-ttu-id="26d1a-330">Tempo de saudação toochange e quando os pontos de recuperação são obtidos de dias, clique em **modificar**.</span><span class="sxs-lookup"><span data-stu-id="26d1a-330">If you want toochange hello time and days when recovery points are taken, click **Modify**.</span></span> <span data-ttu-id="26d1a-331">pontos de recuperação de curto prazo de saudação são backups completos.</span><span class="sxs-lookup"><span data-stu-id="26d1a-331">hello short-term recovery points are full backups.</span></span> <span data-ttu-id="26d1a-332">Não são backups incrementais.</span><span class="sxs-lookup"><span data-stu-id="26d1a-332">They are not incremental backups.</span></span> <span data-ttu-id="26d1a-333">Quando estiver satisfeito com os objetivos de curto prazo hello, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="26d1a-333">When you are satisfied with hello short-term goals, click **Next**.</span></span>

    ![Especificar objetivos de curto prazo](./media/backup-azure-backup-server-vmware/short-term-goals.png)

6. <span data-ttu-id="26d1a-335">Em Olá **rever alocação do disco** página, revise e se necessário, modifique a espaço em disco Olá para Olá VMs.</span><span class="sxs-lookup"><span data-stu-id="26d1a-335">On hello **Review Disk Allocation** page, review and if necessary, modify hello disk space for hello VMs.</span></span> <span data-ttu-id="26d1a-336">Olá recomendados alocações de disco são com base no período de retenção de saudação que é especificado no hello **especificar objetivos de curto prazo** página, tipo de saudação de carga de trabalho e tamanho de saudação de saudação (identificados na etapa 3) de dados protegidos.</span><span class="sxs-lookup"><span data-stu-id="26d1a-336">hello recommended disk allocations are based on hello retention range that is specified in hello **Specify Short-Term Goals** page, hello type of workload, and hello size of hello protected data (identified in step 3).</span></span>  

  - <span data-ttu-id="26d1a-337">**Tamanho dos dados:** tamanho dos dados Olá Olá grupo de proteção.</span><span class="sxs-lookup"><span data-stu-id="26d1a-337">**Data size:** Size of hello data in hello protection group.</span></span>
  - <span data-ttu-id="26d1a-338">**Espaço em disco:** Olá recomendado a quantidade de espaço em disco para o grupo de proteção de saudação.</span><span class="sxs-lookup"><span data-stu-id="26d1a-338">**Disk space:** hello recommended amount of disk space for hello protection group.</span></span> <span data-ttu-id="26d1a-339">Se você quiser toomodify essa configuração, você deve alocar espaço total que é ligeiramente maior do que a quantidade de saudação que você estima que cada fonte de dados cresce.</span><span class="sxs-lookup"><span data-stu-id="26d1a-339">If you want toomodify this setting, you should allocate total space that is slightly larger than hello amount that you estimate each data source grows.</span></span>
  - <span data-ttu-id="26d1a-340">**Colocar os dados:** se você ativar a colocação, várias fontes de dados na proteção Olá podem mapear tooa única réplica e volume de ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="26d1a-340">**Colocate data:** If you turn on colocation, multiple data sources in hello protection can map tooa single replica and recovery point volume.</span></span> <span data-ttu-id="26d1a-341">A colocação não tem suporte para todas as cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="26d1a-341">Colocation isn't supported for all workloads.</span></span>
  - <span data-ttu-id="26d1a-342">**Aumentar automaticamente:** se você ativar essa configuração, se os dados no grupo de saudação protegido ultrapassarem alocação inicial hello, System Center Data Protection Manager tenta tamanho do disco Olá tooincrease em 25 por cento.</span><span class="sxs-lookup"><span data-stu-id="26d1a-342">**Automatically grow:** If you turn on this setting, if data in hello protected group outgrows hello initial allocation, System Center Data Protection Manager tries tooincrease hello disk size by 25 percent.</span></span>
  - <span data-ttu-id="26d1a-343">**Detalhes do pool de armazenamento:** mostra o status Olá Olá do pool de armazenamento, incluindo total e restante tamanho do disco.</span><span class="sxs-lookup"><span data-stu-id="26d1a-343">**Storage pool details:** Shows hello status of hello storage pool, including total and remaining disk size.</span></span>

    ![Examinar a alocação de disco](./media/backup-azure-backup-server-vmware/review-disk-allocation.png)

    <span data-ttu-id="26d1a-345">Quando estiver satisfeito com a alocação de espaço de saudação, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="26d1a-345">When you are satisfied with hello space allocation, click **Next**.</span></span>

7. <span data-ttu-id="26d1a-346">Em Olá **escolher método de criação de réplica** , especifique como você deseja que a cópia inicial toogenerate hello, ou réplica dos dados Olá protegido no servidor de Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="26d1a-346">On hello **Choose Replica Creation Method** page, specify how you want toogenerate hello initial copy, or replica, of hello protected data on Azure Backup Server.</span></span>

    <span data-ttu-id="26d1a-347">saudação padrão é **automaticamente pela rede Olá** e **agora**.</span><span class="sxs-lookup"><span data-stu-id="26d1a-347">hello default is **Automatically over hello network** and **Now**.</span></span> <span data-ttu-id="26d1a-348">Se você usar o padrão de saudação, recomendamos que você especifique um horário de pico.</span><span class="sxs-lookup"><span data-stu-id="26d1a-348">If you use hello default, we recommend that you specify an off-peak time.</span></span> <span data-ttu-id="26d1a-349">Escolha **Mair tarde** e especifique um dia e hora.</span><span class="sxs-lookup"><span data-stu-id="26d1a-349">Choose **Later** and specify a day and time.</span></span>

    <span data-ttu-id="26d1a-350">Para grandes quantidades de dados ou condições de rede menos ideal, considere a possibilidade de replicar dados Olá offline usando mídia removível.</span><span class="sxs-lookup"><span data-stu-id="26d1a-350">For large amounts of data or less-than-optimal network conditions, consider replicating hello data offline by using removable media.</span></span>

    <span data-ttu-id="26d1a-351">Depois de fazer suas escolhas, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="26d1a-351">After you have made your choices, click **Next**.</span></span>

    ![Escolher método de criação de réplica](./media/backup-azure-backup-server-vmware/replica-creation.png)

8. <span data-ttu-id="26d1a-353">Em Olá **opções de verificação de consistência** página, selecione como e quando as verificações de consistência de saudação do tooautomate.</span><span class="sxs-lookup"><span data-stu-id="26d1a-353">On hello **Consistency Check Options** page, select how and when tooautomate hello consistency checks.</span></span> <span data-ttu-id="26d1a-354">Você pode executar verificações de consistência quando dados de réplica se tornam inconsistentes ou de acordo com um agendamento definido.</span><span class="sxs-lookup"><span data-stu-id="26d1a-354">You can run consistency checks when replica data becomes inconsistent, or on a set schedule.</span></span>

    <span data-ttu-id="26d1a-355">Se você não quiser tooconfigure verificações de consistência automática, você pode executar uma verificação manual.</span><span class="sxs-lookup"><span data-stu-id="26d1a-355">If you don't want tooconfigure automatic consistency checks, you can run a manual check.</span></span> <span data-ttu-id="26d1a-356">Na área de proteção de saudação do console do servidor de Backup do Azure hello, clique o grupo de proteção hello e, em seguida, selecione **executar verificação de consistência**.</span><span class="sxs-lookup"><span data-stu-id="26d1a-356">In hello protection area of hello Azure Backup Server console, right-click hello protection group and then select **Perform Consistency Check**.</span></span>

    <span data-ttu-id="26d1a-357">Clique em **próximo** toomove toohello próxima página.</span><span class="sxs-lookup"><span data-stu-id="26d1a-357">Click **Next** toomove toohello next page.</span></span>

9. <span data-ttu-id="26d1a-358">Em Olá **especificar dados de proteção Online** , selecione uma ou mais fontes de dados que você deseja tooprotect.</span><span class="sxs-lookup"><span data-stu-id="26d1a-358">On hello **Specify Online Protection Data** page, select one or more data sources that you want tooprotect.</span></span> <span data-ttu-id="26d1a-359">Você pode selecionar membros Olá individualmente, ou clique em **Selecionar tudo** toochoose todos os membros.</span><span class="sxs-lookup"><span data-stu-id="26d1a-359">You can select hello members individually, or click **Select All** toochoose all members.</span></span> <span data-ttu-id="26d1a-360">Depois que você escolher membros hello, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="26d1a-360">After you choose hello members, click **Next**.</span></span>

    ![Especificar dados de proteção online](./media/backup-azure-backup-server-vmware/select-data-to-protect.png)

10. <span data-ttu-id="26d1a-362">Em Olá **especificar agendamento de Backup Online** , especifique os pontos de recuperação de toogenerate Olá agenda saudação do backup de disco.</span><span class="sxs-lookup"><span data-stu-id="26d1a-362">On hello **Specify Online Backup Schedule** page, specify hello schedule toogenerate recovery points from hello disk backup.</span></span> <span data-ttu-id="26d1a-363">Depois que o ponto de recuperação Olá é gerado, é transferido toohello Cofre de serviços de recuperação no Azure.</span><span class="sxs-lookup"><span data-stu-id="26d1a-363">After hello recovery point is generated, it is transferred toohello Recovery Services vault in Azure.</span></span> <span data-ttu-id="26d1a-364">Quando estiver satisfeito com o agendamento de backup online hello, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="26d1a-364">When you are satisfied with hello online backup schedule, click **Next**.</span></span>

    ![Especifique o cronograma do backup online](./media/backup-azure-backup-server-vmware/online-backup-schedule.png)

11. <span data-ttu-id="26d1a-366">Em Olá **especificar política de retenção Online** página, indique quanto tempo deseja que os dados de backup tooretain Olá no Azure.</span><span class="sxs-lookup"><span data-stu-id="26d1a-366">On hello **Specify Online Retention Policy** page, indicate how long you want tooretain hello backup data in Azure.</span></span> <span data-ttu-id="26d1a-367">Após a definição de política de saudação, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="26d1a-367">After hello policy is defined, click **Next**.</span></span>

    ![Especificar política de retenção online](./media/backup-azure-backup-server-vmware/retention-policy.png)

    <span data-ttu-id="26d1a-369">Não há um tempo limite para manter dados no Azure.</span><span class="sxs-lookup"><span data-stu-id="26d1a-369">There is no time limit for how long you can keep data in Azure.</span></span> <span data-ttu-id="26d1a-370">Quando você armazena dados de ponto de recuperação no Azure, hello limite só é que você não pode ter mais de 9999 pontos de recuperação por instância protegida.</span><span class="sxs-lookup"><span data-stu-id="26d1a-370">When you store recovery point data in Azure, hello only limit is that you cannot have more than 9999 recovery points per protected instance.</span></span> <span data-ttu-id="26d1a-371">Neste exemplo, instância protegida Olá é o hello VMware server.</span><span class="sxs-lookup"><span data-stu-id="26d1a-371">In this example, hello protected instance is hello VMware server.</span></span>

12. <span data-ttu-id="26d1a-372">Em Olá **resumo** página, examine os detalhes de saudação para os membros do grupo de proteção e as configurações e, em seguida, clique em **criar grupo**.</span><span class="sxs-lookup"><span data-stu-id="26d1a-372">On hello **Summary** page, review hello details for your protection group members and settings, and then click **Create Group**.</span></span>

    ![Resumo da configuração e do membro do grupo de proteção](./media/backup-azure-backup-server-vmware/protection-group-summary.png)

## <a name="next-steps"></a><span data-ttu-id="26d1a-374">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="26d1a-374">Next steps</span></span>
<span data-ttu-id="26d1a-375">Se você usar cargas de trabalho do Azure Backup Server tooprotect VMware, você pode estar interessado em usar o servidor de Backup do Azure toohelp proteger um [do Microsoft Exchange server](./backup-azure-exchange-mabs.md), um [farm do Microsoft SharePoint](./backup-azure-backup-sharepoint-mabs.md), ou um [Banco de dados do SQL Server](./backup-azure-sql-mabs.md).</span><span class="sxs-lookup"><span data-stu-id="26d1a-375">If you use Azure Backup Server tooprotect VMware workloads, you may be interested in using Azure Backup Server toohelp protect a [Microsoft Exchange server](./backup-azure-exchange-mabs.md), a [Microsoft SharePoint farm](./backup-azure-backup-sharepoint-mabs.md), or a [SQL Server database](./backup-azure-sql-mabs.md).</span></span>

<span data-ttu-id="26d1a-376">Para obter informações sobre problemas com registrar Olá agente, consulte Configurando o grupo de proteção hello, ou fazer backup de trabalhos, [solucionar problemas de servidor de Backup do Azure](./backup-azure-mabs-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="26d1a-376">For information on problems with registering hello agent, configuring hello protection group, or backing up jobs, see [Troubleshoot Azure Backup Server](./backup-azure-mabs-troubleshoot.md).</span></span>
