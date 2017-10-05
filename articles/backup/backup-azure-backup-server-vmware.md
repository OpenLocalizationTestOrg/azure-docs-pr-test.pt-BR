---
title: "Faça backup de servidores VMware com o Servidor de Backup do Azure | Microsoft Docs"
description: "Utilize o Servidor de Backup do Azure para fazer backup de servidores VMware vCenter/ESXi para o Azure ou disco. Este artigo fornece instruções passo a passo para fazer backup (ou proteger) suas cargas de trabalho do VMware."
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
ms.openlocfilehash: ad331dffb7c31d12290f4223967c568e4535fe3c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="back-up-a-vmware-server-to-azure"></a><span data-ttu-id="9b1dd-104">Fazer backup de um servidor do VMware no Azure</span><span class="sxs-lookup"><span data-stu-id="9b1dd-104">Back up a VMware server to Azure</span></span>

<span data-ttu-id="9b1dd-105">Este artigo explica como configurar um Servidor de Backup do Azure para ajudar a proteger cargas de trabalho do servidor do VMware.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-105">This article explains how to configure Azure Backup Server to help protect VMware server workloads.</span></span> <span data-ttu-id="9b1dd-106">Este artigo pressupõe que você já tenha o Servidor de Backup do Azure instalado.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-106">This article assumes you already have Azure Backup Server installed.</span></span> <span data-ttu-id="9b1dd-107">Se você não tiver o Servidor de Backup do Azure instalado, consulte [Preparar-se para fazer backup de cargas de trabalho usando o Servidor de Backup do Azure](backup-azure-microsoft-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="9b1dd-107">If you don't have Azure Backup Server installed, see [Prepare to back up workloads using Azure Backup Server](backup-azure-microsoft-azure-backup.md).</span></span>

<span data-ttu-id="9b1dd-108">O Servidor de Backup do Azure pode fazer backup ou ajudar a proteger o VMware vCenter Server versão 6.5, 6.0 e 5.5.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-108">Azure Backup Server can back up, or help protect, VMware vCenter Server version 6.5, 6.0 and 5.5.</span></span>


## <a name="create-a-secure-connection-to-the-vcenter-server"></a><span data-ttu-id="9b1dd-109">Criar uma conexão segura com o servidor vCenter</span><span class="sxs-lookup"><span data-stu-id="9b1dd-109">Create a secure connection to the vCenter Server</span></span>

<span data-ttu-id="9b1dd-110">Por padrão, o Servidor de Backup do Azure se comunica com cada vCenter Server por um canal HTTPS.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-110">By default, Azure Backup Server communicates with each vCenter Server via an HTTPS channel.</span></span> <span data-ttu-id="9b1dd-111">Para ativar a comunicação segura, recomendamos instalar o Certificado de Autoridade (AC) de Certificação do VMware no Servidor de Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-111">To turn on the secure communication, we recommend that you install the VMware Certificate Authority (CA) certificate on Azure Backup Server.</span></span> <span data-ttu-id="9b1dd-112">Se não precisar de uma comunicação segura e preferir desabilitar o requisito de HTTPS, consulte [Desabilitar o protocolo de comunicação segura](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol).</span><span class="sxs-lookup"><span data-stu-id="9b1dd-112">If you don't require secure communication, and would prefer to disable the HTTPS requirement, see [Disable secure communication protocol](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol).</span></span> <span data-ttu-id="9b1dd-113">Para criar uma conexão segura entre o Servidor de Backup do Azure e o vCenter Server, importe o certificado confiável para o Servidor de Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-113">To create a secure connection between Azure Backup Server and the vCenter Server, import the trusted certificate on Azure Backup Server.</span></span>

<span data-ttu-id="9b1dd-114">Normalmente, você usa um navegador no computador do Servidor de Backup do Azure para se conectar ao vCenter Server pelo Cliente Web vSphere.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-114">Typically, you use a browser on the Azure Backup Server machine to connect to the vCenter Server via the vSphere Web Client.</span></span> <span data-ttu-id="9b1dd-115">Na primeira vez que usar o navegador do Servidor de Backup do Azure para se conectar ao vCenter Server, a conexão não será segura.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-115">The first time you use the Azure Backup Server browser to connect to the vCenter Server, the connection isn't secure.</span></span> <span data-ttu-id="9b1dd-116">A imagem a seguir mostra a conexão não segura.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-116">The following image shows the unsecured connection.</span></span>

![Exemplo de conexão não segura ao servidor do VMware](./media/backup-azure-backup-server-vmware/unsecure-url.png)

<span data-ttu-id="9b1dd-118">Para corrigir esse problema e criar uma conexão segura, baixe os certificados CA de raiz confiável.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-118">To fix this issue, and create a secure connection, download the trusted root CA certificates.</span></span>

1. <span data-ttu-id="9b1dd-119">No navegador do Servidor de Backup do Azure, insira a URL do Cliente Web vSphere.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-119">In the browser on Azure Backup Server, enter the URL to the vSphere Web Client.</span></span> <span data-ttu-id="9b1dd-120">A página de logon do cliente Web vSphere aparece.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-120">The vSphere Web Client login page appears.</span></span>

    ![Cliente Web vSphere](./media/backup-azure-backup-server-vmware/vsphere-web-client.png)

    <span data-ttu-id="9b1dd-122">Na parte inferior das informações para administradores e desenvolvedores, localize o link **Baixar certificados AC raiz confiável**.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-122">At the bottom of the information for administrators and developers, locate the **Download trusted root CA certificates** link.</span></span>

    ![Link para baixar os Certificados de AC raiz confiável](./media/backup-azure-backup-server-vmware/vmware-download-ca-cert-prompt.png)

  <span data-ttu-id="9b1dd-124">Se você não vir a página de logon do cliente Web vSphere, verifique as configurações de proxy do navegador.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-124">If you don't see the vSphere Web Client login page, check your browser's proxy settings.</span></span>

2. <span data-ttu-id="9b1dd-125">Clique em **Baixar certificados de autoridade de certificação raiz confiável**.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-125">Click **Download trusted root CA certificates**.</span></span>

    <span data-ttu-id="9b1dd-126">O vCenter Server baixa um arquivo no computador local.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-126">The vCenter Server downloads a file to your local computer.</span></span> <span data-ttu-id="9b1dd-127">O nome do arquivo é **download**.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-127">The file's name is named **download**.</span></span> <span data-ttu-id="9b1dd-128">Dependendo do navegador, você recebe uma mensagem que pergunta se deseja abrir ou salvar o arquivo.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-128">Depending on your browser, you receive a message that asks whether to open or save the file.</span></span>

    ![Baixar a mensagem quando certificados são baixados](./media/backup-azure-backup-server-vmware/download-certs.png)

3. <span data-ttu-id="9b1dd-130">Salve o arquivo em um local no Servidor de Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-130">Save the file to a location on Azure Backup Server.</span></span> <span data-ttu-id="9b1dd-131">Ao salvar o arquivo, adicione a extensão de nome de arquivo .zip.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-131">When you save the file, add the .zip file name extension.</span></span>

    <span data-ttu-id="9b1dd-132">O arquivo é um arquivo. zip que contém as informações sobre os certificados.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-132">The file is a .zip file that contains the information about the certificates.</span></span> <span data-ttu-id="9b1dd-133">Com a extensão .zip, você pode usar as ferramentas de extração.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-133">With the .zip extension, you can use the extraction tools.</span></span>

4. <span data-ttu-id="9b1dd-134">Clique com o botão direito do mouse em **download.zip** e, depois, selecione **Extrair Tudo** para extrair o conteúdo.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-134">Right-click **download.zip**, and then select **Extract All** to extract the contents.</span></span>

    <span data-ttu-id="9b1dd-135">O arquivo .zip extrai o conteúdo para uma pasta chamada **certs**.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-135">The .zip file extracts its contents to a folder named **certs**.</span></span> <span data-ttu-id="9b1dd-136">Dois tipos de arquivos são exibidos na pasta certs.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-136">Two types of files appear in the certs folder.</span></span> <span data-ttu-id="9b1dd-137">O arquivo de certificado raiz tem uma extensão que começa com uma sequência numerada como .0 e .1.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-137">The root certificate file has an extension that begins with a numbered sequence like .0 and .1.</span></span>
    
    <span data-ttu-id="9b1dd-138">O arquivo da CRL tem uma extensão que começa com uma sequência como .r0 ou .r1.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-138">The CRL file has an extension that begins with a sequence like .r0 or .r1.</span></span> <span data-ttu-id="9b1dd-139">O arquivo da CRL é associado a um certificado.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-139">The CRL file is associated with a certificate.</span></span>

    ![<span data-ttu-id="9b1dd-140">Baixar o arquivo extraído localmente</span><span class="sxs-lookup"><span data-stu-id="9b1dd-140">Download file extracted locally</span></span> ](./media/backup-azure-backup-server-vmware/extracted-files-in-certs-folder.png)

5. <span data-ttu-id="9b1dd-141">Na pasta **certs**, clique com o botão direito do mouse no arquivo de certificado raiz e, depois, clique em **Renomear**.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-141">In the **certs** folder, right-click the root certificate file, and then click **Rename**.</span></span>

    ![<span data-ttu-id="9b1dd-142">Renomear o certificado raiz</span><span class="sxs-lookup"><span data-stu-id="9b1dd-142">Rename root certificate</span></span> ](./media/backup-azure-backup-server-vmware/rename-cert.png)

    <span data-ttu-id="9b1dd-143">Altere a extensão do certificado raiz para .crt.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-143">Change the root certificate's extension to .crt.</span></span> <span data-ttu-id="9b1dd-144">Quando for perguntado se tem certeza de que deseja alterar a extensão, clique em **Sim** ou em **OK**.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-144">When you're asked if you're sure you want to change the extension, click **Yes** or **OK**.</span></span> <span data-ttu-id="9b1dd-145">Caso contrário, você alterará a função pretendida do arquivo.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-145">Otherwise, you change the file's intended function.</span></span> <span data-ttu-id="9b1dd-146">O ícone do arquivo muda para um ícone que representa um certificado raiz.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-146">The icon for the file changes to an icon that represents a root certificate.</span></span>

6. <span data-ttu-id="9b1dd-147">Clique com o botão direito no certificado raiz e no menu pop-up, selecione **Instalar certificado**.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-147">Right-click the root certificate and from the pop-up menu, select **Install Certificate**.</span></span>

    <span data-ttu-id="9b1dd-148">A caixa de diálogo **Assistente para Importação de Certificados** é exibida.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-148">The **Certificate Import Wizard** dialog box appears.</span></span>

7. <span data-ttu-id="9b1dd-149">Na caixa de diálogo **Assistente para Importação de Certificados**, selecione **Computador Local** como o destino do certificado e, depois, clique em **Avançar** para continuar.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-149">In the **Certificate Import Wizard** dialog box, select **Local Machine** as the destination for the certificate, and then click **Next** to continue.</span></span>

    ![<span data-ttu-id="9b1dd-150">Opções de destino do armazenamento de certificados</span><span class="sxs-lookup"><span data-stu-id="9b1dd-150">Certificate storage destination options</span></span> ](./media/backup-azure-backup-server-vmware/certificate-import-wizard1.png)

    <span data-ttu-id="9b1dd-151">Se for solicitado se você deseja permitir alterações no computador, clique em **Sim** ou **OK**, para todas as alterações.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-151">If you're asked if you want to allow changes to the computer, click **Yes** or **OK**, to all the changes.</span></span>

8. <span data-ttu-id="9b1dd-152">Na página **Repositório de Certificados**, selecione **Colocar todos os certificados no repositório a seguir** e, depois, clique em **Procurar** para escolher o repositório de certificados.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-152">On the **Certificate Store** page, select **Place all certificates in the following store**, and then click **Browse** to choose the certificate store.</span></span>

    ![Colocar os certificados em um ponto de armazenamento específico](./media/backup-azure-backup-server-vmware/cert-import-wizard-local-store.png)

    <span data-ttu-id="9b1dd-154">A caixa de diálogo **Selecionar Repositório de Certificados** é exibida.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-154">The **Select Certificate Store** dialog box appears.</span></span>

    ![Hierarquia de pastas do armazenamento de certificados](./media/backup-azure-backup-server-vmware/cert-store.png)

9. <span data-ttu-id="9b1dd-156">Selecione **Autoridades de Certificação Confiáveis** como a pasta de destino para os certificados e, depois, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-156">Select **Trusted Root Certification Authorities** as the destination folder for the certificates, and then click **OK**.</span></span>

    ![Pasta de destino do certificado](./media/backup-azure-backup-server-vmware/certificate-store-selected.png)

    <span data-ttu-id="9b1dd-158">A pasta **Autoridades de Certificação Confiáveis** é confirmada como o repositório de certificados.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-158">The **Trusted Root Certification Authorities** folder is confirmed as the certificate store.</span></span> <span data-ttu-id="9b1dd-159">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-159">Click **Next**.</span></span>

    ![Pasta de repositório de certificados](./media/backup-azure-backup-server-vmware/certificate-import-wizard2.png)

10. <span data-ttu-id="9b1dd-161">Na página **Concluindo o Assistente para Importação de Certificados**, verifique se o certificado está na pasta desejada e, depois, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-161">On the **Completing the Certificate Import Wizard** page, verify that the certificate is in the desired folder, and then click **Finish**.</span></span>

    ![Verificar se o certificado está na pasta correta](./media/backup-azure-backup-server-vmware/cert-wizard-final-screen.png)

    <span data-ttu-id="9b1dd-163">Uma caixa de diálogo é exibida e a importação de certificado bem-sucedida é confirmada.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-163">A dialog box appears, the successful certificate import is confirmed.</span></span>

11. <span data-ttu-id="9b1dd-164">Entre no vCenter Server para confirmar que a conexão é segura.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-164">Sign in to the vCenter Server to confirm that your connection is secure.</span></span>

  <span data-ttu-id="9b1dd-165">Se a importação do certificado não for bem-sucedida e não for possível estabelecer uma conexão segura, consulte a documentação do VMware vSphere em [Obtendo certificados do servidor](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).</span><span class="sxs-lookup"><span data-stu-id="9b1dd-165">If the certificate import is not successful, and you cannot establish a secure connection, consult the VMware vSphere documentation on [obtaining server certificates](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).</span></span>

  <span data-ttu-id="9b1dd-166">Se você tiver limites de segurança em sua organização e não desejar ativar o protocolo HTTPS, use o procedimento a seguir para desabilitar a comunicação segura.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-166">If you have secure boundaries within your organization, and don't want to turn on the HTTPS protocol, use the following procedure to disable the secure communications.</span></span>

### <a name="disable-secure-communication-protocol"></a><span data-ttu-id="9b1dd-167">Desabilite seu protocolo de comunicação segura</span><span class="sxs-lookup"><span data-stu-id="9b1dd-167">Disable secure communication protocol</span></span>

<span data-ttu-id="9b1dd-168">Caso sua organização não exija o protocolo HTTPS, use as etapas a seguir para desabilitar o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-168">If your organization doesn't require the HTTPS protocol, use the following steps to disable HTTPS.</span></span> <span data-ttu-id="9b1dd-169">Para desabilitar o comportamento padrão, crie uma chave do registro que ignora o comportamento padrão.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-169">To disable the default behavior, create a registry key that ignores the default behavior.</span></span>

1. <span data-ttu-id="9b1dd-170">Copie e cole o texto a seguir em um aquivo .txt.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-170">Copy and paste the following text into a .txt file.</span></span>

  ```
  Windows Registry Editor Version 5.00
  [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\VMWare]
  "IgnoreCertificateValidation"=dword:00000001
  ```

2. <span data-ttu-id="9b1dd-171">Salve o arquivo no computador do Servidor de Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-171">Save the file to your Azure Backup Server computer.</span></span> <span data-ttu-id="9b1dd-172">Para o nome de arquivo, use DisableSecureAuthentication.reg.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-172">For the file name, use DisableSecureAuthentication.reg.</span></span>

3. <span data-ttu-id="9b1dd-173">Clique duas vezes no arquivo para ativar a entrada do registro.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-173">Double-click the file to activate the registry entry.</span></span>


## <a name="create-a-role-and-user-account-on-the-vcenter-server"></a><span data-ttu-id="9b1dd-174">Crie uma conta de usuário e a função no servidor vCenter</span><span class="sxs-lookup"><span data-stu-id="9b1dd-174">Create a role and user account on the vCenter Server</span></span>

<span data-ttu-id="9b1dd-175">No servidor vCenter, uma função é um conjunto predefinido de privilégios.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-175">On the vCenter Server, a role is a predefined set of privileges.</span></span> <span data-ttu-id="9b1dd-176">Um administrador do vCenter Server cria as funções.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-176">A vCenter Server administrator creates the roles.</span></span> <span data-ttu-id="9b1dd-177">Para atribuir permissões, o administrador emparelha contas de usuário com uma função.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-177">To assign permissions, the administrator pairs user accounts with a role.</span></span> <span data-ttu-id="9b1dd-178">Para estabelecer as credenciais de usuário necessárias para fazer backup do computador do vCenter Server, crie uma função com privilégios específicos e, depois, associe a conta de usuário à função.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-178">To establish the necessary user credentials to back up the vCenter Server computer, create a role with specific privileges, and then associate the user account with the role.</span></span>

<span data-ttu-id="9b1dd-179">O Servidor de Backup do Azure usa um nome de usuário e uma senha para se autenticar no vCenter Server.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-179">Azure Backup Server uses a username and password to authenticate with the vCenter Server.</span></span> <span data-ttu-id="9b1dd-180">O Servidor de Backup do Azure utiliza essas credenciais como autenticação para todas as operações de backup.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-180">Azure Backup Server uses these credentials as authentication for all backup operations.</span></span>

<span data-ttu-id="9b1dd-181">Para adicionar uma função do vCenter Server e seus privilégios a um administrador de backup:</span><span class="sxs-lookup"><span data-stu-id="9b1dd-181">To add a vCenter Server role and its privileges for a backup administrator:</span></span>

1. <span data-ttu-id="9b1dd-182">Entre no vCenter Server e, em seguida, no painel **Navegador** do vCenter Server, clique em **Administração**.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-182">Sign in to the vCenter Server, and then in the vCenter Server **Navigator** panel, click **Administration**.</span></span>

    ![Opção de administração no painel Navegador do vCenter Server](./media/backup-azure-backup-server-vmware/vmware-navigator-panel.png)

2. <span data-ttu-id="9b1dd-184">Em **Administração**, selecione **Funções** e, depois, no painel **Funções**, clique no ícone Adicionar função (o símbolo +).</span><span class="sxs-lookup"><span data-stu-id="9b1dd-184">In **Administration** select **Roles**, and then in the **Roles** panel click the add role icon (the + symbol).</span></span>

    ![Adicionar função](./media/backup-azure-backup-server-vmware/vmware-define-new-role.png)

    <span data-ttu-id="9b1dd-186">A caixa de diálogo **Criar Função** é exibida.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-186">The **Create Role** dialog box appears.</span></span>

    ![Criar função](./media/backup-azure-backup-server-vmware/vmware-define-new-role-priv.png)

3. <span data-ttu-id="9b1dd-188">Na caixa de diálogo **Criar Função**, na caixa **Nome da função**, insira *BackupAdminRole*.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-188">In the **Create Role** dialog box, in the **Role name** box, enter *BackupAdminRole*.</span></span> <span data-ttu-id="9b1dd-189">O nome da função pode ser o que você quiser, mas deve ser reconhecível para o objetivo da função.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-189">The role name can be whatever you like, but it should be recognizable for the role's purpose.</span></span>

4. <span data-ttu-id="9b1dd-190">Selecione os privilégios para a versão apropriada do vCenter e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-190">Select the privileges for the appropriate version of vCenter, and then click **OK**.</span></span> <span data-ttu-id="9b1dd-191">A tabela a seguir identifica os privilégios necessários para o vCenter 6.0 e o vCenter 5.5.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-191">The following table identifies the required privileges for vCenter 6.0 and vCenter 5.5.</span></span>

  <span data-ttu-id="9b1dd-192">Ao selecionar os privilégios, clique no ícone ao lado do rótulo pai para expandir o pai e exibir os privilégios filho.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-192">When you select the privileges, click the icon next to the parent label to expand the parent and view the child privileges.</span></span> <span data-ttu-id="9b1dd-193">Para selecionar os privilégios da VirtualMachine, você precisa acessar vários níveis da hierarquia pai-filho.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-193">To select the VirtualMachine privileges, you need to go several levels into the parent child hierarchy.</span></span> <span data-ttu-id="9b1dd-194">Você não precisa selecionar todos os privilégios do filho dentro de um privilégio pai.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-194">You don't need to select all child privileges within a parent privilege.</span></span>

  ![Hierarquia de privilégios pai-filho](./media/backup-azure-backup-server-vmware/cert-add-privilege-expand.png)

  <span data-ttu-id="9b1dd-196">Depois de clicar em **OK**, a nova função é exibida na lista no painel Funções.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-196">After you click **OK**, the new role appears in the list on the Roles panel.</span></span>

|<span data-ttu-id="9b1dd-197">Privilégios do vCenter 6.0</span><span class="sxs-lookup"><span data-stu-id="9b1dd-197">Privileges for vCenter 6.0</span></span>| <span data-ttu-id="9b1dd-198">Privilégios do vCenter 5.5</span><span class="sxs-lookup"><span data-stu-id="9b1dd-198">Privileges for vCenter 5.5</span></span>|
|--------------------------|---------------------------|
|<span data-ttu-id="9b1dd-199">Datastore.AllocateSpace</span><span class="sxs-lookup"><span data-stu-id="9b1dd-199">Datastore.AllocateSpace</span></span>   | <span data-ttu-id="9b1dd-200">Datastore.AllocateSpace</span><span class="sxs-lookup"><span data-stu-id="9b1dd-200">Datastore.AllocateSpace</span></span>|
|<span data-ttu-id="9b1dd-201">Global.ManageCustomFields</span><span class="sxs-lookup"><span data-stu-id="9b1dd-201">Global.ManageCustomFields</span></span> | <span data-ttu-id="9b1dd-202">Global.ManageCustomerFields</span><span class="sxs-lookup"><span data-stu-id="9b1dd-202">Global.ManageCustomerFields</span></span>|
|<span data-ttu-id="9b1dd-203">Global.SetCustomFields</span><span class="sxs-lookup"><span data-stu-id="9b1dd-203">Global.SetCustomFields</span></span>    |   |
|<span data-ttu-id="9b1dd-204">Host.Local.CreateVM</span><span class="sxs-lookup"><span data-stu-id="9b1dd-204">Host.Local.CreateVM</span></span>       | <span data-ttu-id="9b1dd-205">Network.Assign</span><span class="sxs-lookup"><span data-stu-id="9b1dd-205">Network.Assign</span></span> |
|<span data-ttu-id="9b1dd-206">Network.Assign</span><span class="sxs-lookup"><span data-stu-id="9b1dd-206">Network.Assign</span></span>            |  |
|<span data-ttu-id="9b1dd-207">Resource.AssignVMToPool</span><span class="sxs-lookup"><span data-stu-id="9b1dd-207">Resource.AssignVMToPool</span></span>   |  |
|<span data-ttu-id="9b1dd-208">VirtualMachine.Config.AddNewDisk</span><span class="sxs-lookup"><span data-stu-id="9b1dd-208">VirtualMachine.Config.AddNewDisk</span></span>  | <span data-ttu-id="9b1dd-209">VirtualMachine.Config.AddNewDisk</span><span class="sxs-lookup"><span data-stu-id="9b1dd-209">VirtualMachine.Config.AddNewDisk</span></span>   |
|<span data-ttu-id="9b1dd-210">VirtualMachine.Config.AdvanceConfig</span><span class="sxs-lookup"><span data-stu-id="9b1dd-210">VirtualMachine.Config.AdvanceConfig</span></span>| <span data-ttu-id="9b1dd-211">VirtualMachine.Config.AdvancedConfig</span><span class="sxs-lookup"><span data-stu-id="9b1dd-211">VirtualMachine.Config.AdvancedConfig</span></span>|
|<span data-ttu-id="9b1dd-212">VirtualMachine.Config.ChangeTracking</span><span class="sxs-lookup"><span data-stu-id="9b1dd-212">VirtualMachine.Config.ChangeTracking</span></span>| <span data-ttu-id="9b1dd-213">VirtualMachine.Config.ChangeTracking</span><span class="sxs-lookup"><span data-stu-id="9b1dd-213">VirtualMachine.Config.ChangeTracking</span></span> |
|<span data-ttu-id="9b1dd-214">VirtualMachine.Config.HostUSBDevice</span><span class="sxs-lookup"><span data-stu-id="9b1dd-214">VirtualMachine.Config.HostUSBDevice</span></span>||
|<span data-ttu-id="9b1dd-215">VirtualMachine.Config.QueryUnownedFiles</span><span class="sxs-lookup"><span data-stu-id="9b1dd-215">VirtualMachine.Config.QueryUnownedFiles</span></span>|    |
|<span data-ttu-id="9b1dd-216">VirtualMachine.Config.SwapPlacement</span><span class="sxs-lookup"><span data-stu-id="9b1dd-216">VirtualMachine.Config.SwapPlacement</span></span>| <span data-ttu-id="9b1dd-217">VirtualMachine.Config.SwapPlacement</span><span class="sxs-lookup"><span data-stu-id="9b1dd-217">VirtualMachine.Config.SwapPlacement</span></span> |
|<span data-ttu-id="9b1dd-218">VirtualMachine.Interact.PowerOff</span><span class="sxs-lookup"><span data-stu-id="9b1dd-218">VirtualMachine.Interact.PowerOff</span></span>| <span data-ttu-id="9b1dd-219">VirtualMachine.Interact.PowerOff</span><span class="sxs-lookup"><span data-stu-id="9b1dd-219">VirtualMachine.Interact.PowerOff</span></span> |
|<span data-ttu-id="9b1dd-220">VirtualMachine.Inventory.Create</span><span class="sxs-lookup"><span data-stu-id="9b1dd-220">VirtualMachine.Inventory.Create</span></span>| <span data-ttu-id="9b1dd-221">VirtualMachine.Inventory.Create</span><span class="sxs-lookup"><span data-stu-id="9b1dd-221">VirtualMachine.Inventory.Create</span></span> |
|<span data-ttu-id="9b1dd-222">VirtualMachine.Provisioning.DiskRandomAccess</span><span class="sxs-lookup"><span data-stu-id="9b1dd-222">VirtualMachine.Provisioning.DiskRandomAccess</span></span>| |
|<span data-ttu-id="9b1dd-223">VirtualMachine.Provisioning.DiskRandomRead</span><span class="sxs-lookup"><span data-stu-id="9b1dd-223">VirtualMachine.Provisioning.DiskRandomRead</span></span>|<span data-ttu-id="9b1dd-224">VirtualMachine.Provisioning.DiskRandomRead</span><span class="sxs-lookup"><span data-stu-id="9b1dd-224">VirtualMachine.Provisioning.DiskRandomRead</span></span> |
|<span data-ttu-id="9b1dd-225">VirtualMachine.State.CreateSnapshot</span><span class="sxs-lookup"><span data-stu-id="9b1dd-225">VirtualMachine.State.CreateSnapshot</span></span>| <span data-ttu-id="9b1dd-226">VirtualMachine.State.CreateSnapshot</span><span class="sxs-lookup"><span data-stu-id="9b1dd-226">VirtualMachine.State.CreateSnapshot</span></span>|
|<span data-ttu-id="9b1dd-227">VirtualMachine.State.RemoveSnapshot</span><span class="sxs-lookup"><span data-stu-id="9b1dd-227">VirtualMachine.State.RemoveSnapshot</span></span>|<span data-ttu-id="9b1dd-228">VirtualMachine.State.RemoveSnapshot</span><span class="sxs-lookup"><span data-stu-id="9b1dd-228">VirtualMachine.State.RemoveSnapshot</span></span> |
</br>



## <a name="create-a-vcenter-server-user-account-and-permissions"></a><span data-ttu-id="9b1dd-229">Criar uma conta de usuário do vCenter Server e as permissões</span><span class="sxs-lookup"><span data-stu-id="9b1dd-229">Create a vCenter Server user account and permissions</span></span>

<span data-ttu-id="9b1dd-230">Depois de configurar a função com privilégios, crie uma conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-230">After the role with privileges is set up, create a user account.</span></span> <span data-ttu-id="9b1dd-231">A conta de usuário tem um nome e uma senha, que fornece as credenciais usadas para autenticação.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-231">The user account has a name and password, which provides the credentials that are used for authentication.</span></span>

1. <span data-ttu-id="9b1dd-232">Para criar uma conta de usuário, no painel **Navegador** do vCenter Server, clique em **Usuários e Grupos**.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-232">To create a user account, in the vCenter Server **Navigator** panel, click **Users and Groups**.</span></span>

    ![Opção de Usuários e Grupos](./media/backup-azure-backup-server-vmware/vmware-userandgroup-panel.png)

    <span data-ttu-id="9b1dd-234">O painel **Usuários e Grupos do vCenter** é exibido.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-234">The **vCenter Users and Groups** panel appears.</span></span>

    ![Painel Usuários e Grupos do vCenter](./media/backup-azure-backup-server-vmware/usersandgroups.png)

2. <span data-ttu-id="9b1dd-236">No painel **Usuários e Grupos do vCenter**, selecione a guia **Usuários** e, depois, clique no ícone Adicionar usuários (o símbolo +).</span><span class="sxs-lookup"><span data-stu-id="9b1dd-236">In the **vCenter Users and Groups** panel, select the **Users** tab, and then click the add users icon (the + symbol).</span></span>

    <span data-ttu-id="9b1dd-237">A caixa de diálogo **Novo Usuário** é exibida.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-237">The **New User** dialog box appears.</span></span>

3. <span data-ttu-id="9b1dd-238">Na caixa de diálogo **Novo Usuário**, adicione as informações do usuário e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-238">In the **New User** dialog box, add the user's information and then click **OK**.</span></span> <span data-ttu-id="9b1dd-239">Neste procedimento, o nome de usuário é BackupAdmin.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-239">In this procedure, the username is BackupAdmin.</span></span>

    ![Caixa de diálogo Novo Usuário](./media/backup-azure-backup-server-vmware/vmware-new-user-account.png)

    <span data-ttu-id="9b1dd-241">A nova conta de usuário aparece na lista.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-241">The new user account appears in the list.</span></span>

4. <span data-ttu-id="9b1dd-242">Para associar a conta de usuário à função, no painel **Navegador**, clique em **Permissões Globais**.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-242">To associate the user account with the role, in the **Navigator** panel, click **Global Permissions**.</span></span> <span data-ttu-id="9b1dd-243">No painel **Permissões Globais**, selecione a guia **Gerenciar** e, em seguida, clique no ícone Adicionar (o símbolo +).</span><span class="sxs-lookup"><span data-stu-id="9b1dd-243">In the **Global Permissions** panel, select the **Manage** tab, and then click the add icon (the + symbol).</span></span>

    ![Painel Permissões Globais](./media/backup-azure-backup-server-vmware/vmware-add-new-perms.png)

    <span data-ttu-id="9b1dd-245">A caixa de diálogo **Permissões Globais Raiz – Adicionar Permissão** é exibida.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-245">The **Global Permissions Root - Add Permission** dialog box appears.</span></span>

5. <span data-ttu-id="9b1dd-246">Na caixa de diálogo **Permissão Global Raiz – Adicionar Permissão**, clique em **Adicionar** para escolher o usuário ou o grupo.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-246">In the **Global Permission Root - Add Permission** dialog box, click **Add** to choose the user or group.</span></span>

    ![Escolher o usuário ou o grupo](./media/backup-azure-backup-server-vmware/vmware-add-new-global-perm.png)

    <span data-ttu-id="9b1dd-248">A caixa de diálogo **Selecionar Usuários/Grupos** é exibida.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-248">The **Select Users/Groups** dialog box appears.</span></span>

6. <span data-ttu-id="9b1dd-249">Na caixa de diálogo **Selecionar Usuários/Grupos**, escolha **BackupAdmin** e, depois, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-249">In the **Select Users/Groups** dialog box, choose **BackupAdmin** and then click **Add**.</span></span>

    <span data-ttu-id="9b1dd-250">Em **Usuários**, o formato *domain\username* é usado para a conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-250">In **Users**, the *domain\username* format is used for the user account.</span></span> <span data-ttu-id="9b1dd-251">Se desejar usar outro domínio, escolha-o na lista **Domínios**.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-251">If you want to use a different domain, choose it from the **Domain** list.</span></span>

    ![Adicionar um usuário BackupAdmin](./media/backup-azure-backup-server-vmware/vmware-assign-account-to-role.png)

    <span data-ttu-id="9b1dd-253">Clique em **OK** para adicionar os usuários selecionados à caixa de diálogo **Adicionar Permissão**.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-253">Click **OK** to add the selected users to the **Add Permission** dialog box.</span></span>

7. <span data-ttu-id="9b1dd-254">Agora que você identificou o usuário, atribua o usuário à função.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-254">Now that you've identified the user, assign the user to the role.</span></span> <span data-ttu-id="9b1dd-255">Em **Função Atribuída**, na lista suspensa, selecione **BackupAdminRole** e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-255">In **Assigned Role**, from the drop-down list, select **BackupAdminRole**, and then click **OK**.</span></span>

    ![Atribuir o usuário à função ](./media/backup-azure-backup-server-vmware/vmware-choose-role.png)

  <span data-ttu-id="9b1dd-257">Na guia **Gerenciar** no painel **Permissões Globais**, a nova conta de usuário e a função associada são exibidas na lista.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-257">On the **Manage** tab in the **Global Permissions** panel, the new user account and the associated role appear in the list.</span></span>


## <a name="establish-vcenter-server-credentials-on-azure-backup-server"></a><span data-ttu-id="9b1dd-258">Estabelecer as credenciais de servidor do vCenter no servidor de Backup do Azure</span><span class="sxs-lookup"><span data-stu-id="9b1dd-258">Establish vCenter Server credentials on Azure Backup Server</span></span>

<span data-ttu-id="9b1dd-259">Antes de adicionar o servidor do VMware ao Servidor de Backup do Azure, instale a [Atualização 1 do Servidor de Backup do Azure](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).</span><span class="sxs-lookup"><span data-stu-id="9b1dd-259">Before you add the VMware server to Azure Backup Server, install [Update 1 for Azure Backup Server](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).</span></span>

1. <span data-ttu-id="9b1dd-260">Para abrir o servidor de Backup do Azure, clique duas vezes no ícone da área de trabalho do servidor de Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-260">To open Azure Backup Server, double-click the icon on the Azure Backup Server desktop.</span></span>

    ![Ícone do Servidor de Backup do Azure](./media/backup-azure-backup-server-vmware/mabs-icon.png)

    <span data-ttu-id="9b1dd-262">Se você não conseguir localizar o ícone na área de trabalho, poderá abrir o Servidor de Backup do Azure na lista de aplicativos instalados.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-262">If you can't find the icon on the desktop, open Azure Backup Server from the list of installed apps.</span></span> <span data-ttu-id="9b1dd-263">O nome de aplicativo do Servidor de Backup do Azure é Backup do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-263">The Azure Backup Server app name is called Microsoft Azure Backup.</span></span>

2. <span data-ttu-id="9b1dd-264">No console do Servidor de Backup do Azure, clique em **Gerenciamento**, em **Servidores de Produção** e, depois, na faixa de opções da ferramenta, clique em **Gerenciar VMware**.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-264">In the Azure Backup Server console, click **Management**, click **Production Servers**, and then on the tool ribbon, click **Manage VMware**.</span></span>

    ![Console do Servidor de Backup do Azure](./media/backup-azure-backup-server-vmware/add-vmware-credentials.png)

    <span data-ttu-id="9b1dd-266">A caixa de diálogo **Gerenciar Credenciais** é exibida.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-266">The **Manage Credentials** dialog box appears.</span></span>

    ![Caixa de diálogo Gerenciar Credenciais do Servidor de Backup do Azure](./media/backup-azure-backup-server-vmware/mabs-manage-credentials-dialog.png)

3. <span data-ttu-id="9b1dd-268">Na caixa de diálogo **Gerenciar Credenciais**, clique em **Adicionar** para abrir a caixa de diálogo **Adicionar Credencial**.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-268">In the **Manage Credentials** dialog box, click **Add** to open the **Add Credential** dialog box.</span></span>

4. <span data-ttu-id="9b1dd-269">Na caixa de diálogo **Adicionar Credencial**, insira um nome e uma descrição para a nova credencial.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-269">In the **Add Credential** dialog box, enter a name and a description for the new credential.</span></span> <span data-ttu-id="9b1dd-270">Em seguida, especifique o nome de usuário e a senha.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-270">Then specify the username and password.</span></span> <span data-ttu-id="9b1dd-271">O nome *credencial do Contoso Vcenter* é utilizado para identificar a credencial no próximo procedimento.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-271">The name, *Contoso Vcenter credential* is used to identify the credential in the next procedure.</span></span> <span data-ttu-id="9b1dd-272">Use o mesmo nome de usuário e a senha usados para o vCenter Server.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-272">Use the same username and password that is used for the vCenter Server.</span></span> <span data-ttu-id="9b1dd-273">Se o vCenter Server e o Servidor de Backup do Azure não estiverem no mesmo domínio, em **Nome de usuário**, especifique o domínio.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-273">If the vCenter Server and Azure Backup Server are not in the same domain, in **User name**, specify the domain.</span></span>

    ![Caixa de diálogo Adicionar Credencial do Servidor de Backup do Azure](./media/backup-azure-backup-server-vmware/mabs-add-credential-dialog2.png)

    <span data-ttu-id="9b1dd-275">Clique em **Adicionar** para adicionar a nova credencial para o Servidor de Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-275">Click **Add** to add the new credential to Azure Backup Server.</span></span> <span data-ttu-id="9b1dd-276">A nova credencial é exibida na lista da caixa de diálogo **Gerenciar Credenciais**.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-276">The new credential appears in the list in the **Manage Credentials** dialog box.</span></span>
    
    ![Caixa de diálogo Gerenciar Credenciais do Servidor de Backup do Azure](./media/backup-azure-backup-server-vmware/new-list-of-mabs-creds.png)

5. <span data-ttu-id="9b1dd-278">Para fechar a caixa de diálogo **Gerenciar Credenciais**, clique no **X** no canto superior direito.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-278">To close the **Manage Credentials** dialog box, click the **X** in the upper-right corner.</span></span>


## <a name="add-the-vcenter-server-to-azure-backup-server"></a><span data-ttu-id="9b1dd-279">Adicionar servidor VMware para o Servidor de Backup do Azure</span><span class="sxs-lookup"><span data-stu-id="9b1dd-279">Add the vCenter Server to Azure Backup Server</span></span>

<span data-ttu-id="9b1dd-280">O Assistente de Adição de Servidor de Produção é usado para adicionar o vCenter Server ao Servidor de Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-280">Production Server Addition Wizard is used to add the vCenter Server to Azure Backup Server.</span></span>

<span data-ttu-id="9b1dd-281">Para abrir o Assistente de Adição de Servidor de Produção, conclua o seguinte procedimento:</span><span class="sxs-lookup"><span data-stu-id="9b1dd-281">To open Production Server Addition Wizard, complete the following procedure:</span></span>

1. <span data-ttu-id="9b1dd-282">No console do Servidor de Backup do Azure, clique em **Gerenciamento**, em **Servidores de Produção** e, em seguida, em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-282">In the Azure Backup Server console, click **Management**, click **Production Servers**, and then click **Add**.</span></span>

    ![Abra o Assistente de Adição de Servidor de Produção](./media/backup-azure-backup-server-vmware/add-vcenter-to-mabs.png)

    <span data-ttu-id="9b1dd-284">A caixa de diálogo **Assistente de Adição de Servidor de Produção** é exibida.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-284">The **Production Server Addition Wizard** dialog box appears.</span></span>

    ![Assistente de Adição de Servidor de Produção](./media/backup-azure-backup-server-vmware/production-server-add-wizard.png)

2. <span data-ttu-id="9b1dd-286">Na página **Selecionar tipo de Servidor de Produção**, selecione **Servidores do VMware** e, depois, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-286">On the **Select Production Server type** page, select **VMware Servers**, and then click **Next**.</span></span>

3. <span data-ttu-id="9b1dd-287">Em **Nome do Servidor/Endereço IP**, especifique o FQDN (nome de domínio totalmente qualificado) ou o endereço IP do servidor do VMware.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-287">In **Server Name/IP Address**, specify the fully qualified domain name (FQDN) or IP address of the VMware server.</span></span> <span data-ttu-id="9b1dd-288">Se todos os servidores ESXi forem gerenciados pelo mesmo vCenter, você poderá usar o nome do vCenter.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-288">If all the ESXi servers are managed by the same vCenter, you can use the vCenter name.</span></span>

    ![Especificar o FQDN ou o endereço IP do servidor do VMware](./media/backup-azure-backup-server-vmware/add-vmware-server-provide-server-name.png)

4. <span data-ttu-id="9b1dd-290">Em **Porta SSL**, insira a porta usada para se comunicar com o servidor do VMware.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-290">In **SSL Port**, enter the port that is used to communicate with the VMware server.</span></span> <span data-ttu-id="9b1dd-291">Use a porta 443, que é a porta padrão, a menos que você saiba que uma porta diferente é necessária.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-291">Use port 443, which is the default port, unless you know that a different port is required.</span></span>

5. <span data-ttu-id="9b1dd-292">Em **Especificar Credencial**, selecione a credencial que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-292">In **Specify Credential**, select the credential that you created earlier.</span></span>

    ![Especificar credencial](./media/backup-azure-backup-server-vmware/identify-creds.png)

6. <span data-ttu-id="9b1dd-294">Clique em **Adicionar** para adicionar o servidor do VMware à lista de **Servidores do VMware Adicionados** e, depois, clique em **Avançar** para ir para a próxima página do assistente.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-294">Click **Add** to add the VMware server to the list of **Added VMware Servers**, and then click **Next** to move to the next page in the wizard.</span></span>

    ![Adicionar servidor do VMware e a credencial](./media/backup-azure-backup-server-vmware/add-vmware-server-credentials.png)

7. <span data-ttu-id="9b1dd-296">Na página **Resumo**, clique em **Adicionar** para adicionar o servidor do VMware especificado ao Servidor de Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-296">In the **Summary** page, click **Add** to add the specified VMware server to Azure Backup Server.</span></span>

    ![Adicionar servidor VMware para o Servidor de Backup do Azure](./media/backup-azure-backup-server-vmware/tasks-screen.png)

  <span data-ttu-id="9b1dd-298">O backup do servidor do VMware é um backup sem agente e o novo servidor é adicionado imediatamente.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-298">The VMware server backup is an agentless backup, and the new server is added immediately.</span></span> <span data-ttu-id="9b1dd-299">A página **Concluir** mostra os resultados.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-299">The **Finish** page shows you the results.</span></span>

  ![Página Concluir](./media/backup-azure-backup-server-vmware/summary-screen.png)

  <span data-ttu-id="9b1dd-301">Para adicionar várias instâncias do vCenter Server ao Servidor de Backup do Azure, repita as etapas anteriores nesta seção.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-301">To add multiple instances of vCenter Server to Azure Backup Server, repeat the previous steps in this section.</span></span>

<span data-ttu-id="9b1dd-302">Depois de adicionar o vCenter Server ao Servidor de Backup do Azure, a próxima etapa é criar um grupo de proteção.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-302">After you add the vCenter Server to Azure Backup Server, the next step is to create a protection group.</span></span> <span data-ttu-id="9b1dd-303">O grupo de proteção especifica os diversos detalhes para retenção de curto e longo prazo e é onde você pode definir e aplica a política de backup.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-303">The protection group specifies the various details for short or long-term retention, and it is where you define and apply the backup policy.</span></span> <span data-ttu-id="9b1dd-304">A política de backup é o agendamento para quando os backups ocorrem e o que é copiado em backup.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-304">The backup policy is the schedule for when backups occur, and what is backed up.</span></span>


## <a name="configure-a-protection-group"></a><span data-ttu-id="9b1dd-305">Configurar grupo de proteção</span><span class="sxs-lookup"><span data-stu-id="9b1dd-305">Configure a protection group</span></span>

<span data-ttu-id="9b1dd-306">Se você não usou o System Center Data Protection Manager nem o Servidor de Backup do Azure antes, consulte [Planejar backups de disco](https://technet.microsoft.com/library/hh758026.aspx) para preparar o ambiente de hardware.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-306">If you have not used System Center Data Protection Manager or Azure Backup Server before, see [Plan for disk backups](https://technet.microsoft.com/library/hh758026.aspx) to prepare your hardware environment.</span></span> <span data-ttu-id="9b1dd-307">Depois de verificar que você tem um armazenamento adequado, use o assistente para Criar Novo Grupo de Proteção para adicionar máquinas virtuais do VMware.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-307">After you check that you have proper storage, use the Create New Protection Group wizard to add VMware virtual machines.</span></span>

1. <span data-ttu-id="9b1dd-308">No console do Servidor de Backup do Azure, clique em **Proteção**e, na faixa de opções da ferramenta, clique em **Novo** para abrir o assistente Criar Novo Grupo de Proteção.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-308">In the Azure Backup Server console, click **Protection**, and in the tool ribbon, click **New** to open the Create New Protection Group wizard.</span></span>

    ![Abra o assistente para Criar Novo Grupo de Proteção](./media/backup-azure-backup-server-vmware/open-protection-wizard.png)

    <span data-ttu-id="9b1dd-310">A caixa de diálogo do assistente para **Criar Novo Grupo de Proteção** é exibida.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-310">The **Create New Protection Group** wizard dialog box appears.</span></span>

    ![Caixa de diálogo Assistente para Criar Novo Grupo de Proteção](./media/backup-azure-backup-server-vmware/protection-wizard.png)

    <span data-ttu-id="9b1dd-312">Clique em **Avançar** para ir para a página **Selecionar tipo de grupo de proteção**.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-312">Click **Next** to advance to the **Select protection group type** page.</span></span>

2. <span data-ttu-id="9b1dd-313">Na página **Selecionar tipo de grupo de Proteção**, selecione **Servidores** e, depois, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-313">On the **Select Protection group type** page, select **Servers** and then click **Next**.</span></span> <span data-ttu-id="9b1dd-314">A página **Selecionar membros do grupo** é exibida.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-314">The **Select group members** page appears.</span></span>

3. <span data-ttu-id="9b1dd-315">Na página **Selecionar membros do grupo**, os membros disponíveis e os membros selecionados são exibidos.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-315">On the **Select group members** page, the available members and the selected members appear.</span></span> <span data-ttu-id="9b1dd-316">Selecione os membros que você deseja proteger e, depois, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-316">Select the members that you want to protect, and then click **Next**.</span></span>

    ![Selecionar membros do grupo](./media/backup-azure-backup-server-vmware/server-add-selected-members.png)

    <span data-ttu-id="9b1dd-318">Ao selecionar um membro, se você selecionar uma pasta que contém outras pastas ou VMs, essas pastas e VMs também serão selecionadas.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-318">When you select a member, if you select a folder that contains other folders or VMs, those folders and VMs are also selected.</span></span> <span data-ttu-id="9b1dd-319">A inclusão das pastas e VMs na pasta pai é chamada de proteção de nível de pasta.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-319">The inclusion of the folders and VMs in the parent folder is called folder-level protection.</span></span> <span data-ttu-id="9b1dd-320">Para remover uma pasta ou VM, desmarque a caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-320">To remove a folder or VM, clear the check box.</span></span>

    <span data-ttu-id="9b1dd-321">Se uma VM ou uma pasta que contenha uma VM já estiver protegida no Azure, você não poderá selecionar essa VM novamente.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-321">If a VM, or a folder containing a VM, is already protected to Azure, you cannot select that VM again.</span></span> <span data-ttu-id="9b1dd-322">Ou seja, depois que uma VM é protegida no Azure, ela não pode ser protegida novamente, o que impede a criação de pontos de recuperação duplicados para uma VM.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-322">That is, after a VM is protected to Azure, it cannot be protected again, which prevents duplicate recovery points from being created for one VM.</span></span> <span data-ttu-id="9b1dd-323">Se desejar ver qual instância do Servidor de Backup do Azure já protege um membro, aponte para o membro para ver o nome do servidor de proteção.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-323">If you want to see which Azure Backup Server instance already protects a member, point to the member to see the name of the protecting server.</span></span>

4. <span data-ttu-id="9b1dd-324">Na página **Selecionar Método de Proteção de Dados**, insira um nome para o grupo de proteção.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-324">On the **Select Data Protection Method** page, enter a name for the protection group.</span></span> <span data-ttu-id="9b1dd-325">Proteção de curto prazo (no disco) e proteção online são selecionados.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-325">Short-term protection (to disk) and online protection are selected.</span></span> <span data-ttu-id="9b1dd-326">Se você quiser usar a proteção online (Azure), você deve usar a proteção de curto prazo em disco.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-326">If you want to use online protection (to Azure), you must use short-term protection to disk.</span></span> <span data-ttu-id="9b1dd-327">Clique em **Avançar** para prosseguir para o intervalo de proteção de curto prazo.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-327">Click **Next** to proceed to the short-term protection range.</span></span>

    ![Selecionar método de proteção de dados](./media/backup-azure-backup-server-vmware/name-protection-group.png)

5. <span data-ttu-id="9b1dd-329">Na página **Especificar Metas de Curto Prazo**, em **Intervalo de Retenção**, especifique o número de dias durante os quais deseja reter os pontos de recuperação *armazenados em disco*.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-329">On the **Specify Short-Term Goals** page, for **Retention Range**, specify the number of days that you want to retain recovery points that are *stored to disk*.</span></span> <span data-ttu-id="9b1dd-330">Se você quiser alterar o tempo e os dias quando os pontos de recuperação são criados, clique em **Modificar**.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-330">If you want to change the time and days when recovery points are taken, click **Modify**.</span></span> <span data-ttu-id="9b1dd-331">Os pontos de recuperação de curto prazo são backups completos.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-331">The short-term recovery points are full backups.</span></span> <span data-ttu-id="9b1dd-332">Não são backups incrementais.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-332">They are not incremental backups.</span></span> <span data-ttu-id="9b1dd-333">Quando estiver satisfeito com as metas de curto prazo, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-333">When you are satisfied with the short-term goals, click **Next**.</span></span>

    ![Especificar objetivos de curto prazo](./media/backup-azure-backup-server-vmware/short-term-goals.png)

6. <span data-ttu-id="9b1dd-335">Na página **Examinar Alocação de Disco**, examine e, se necessário, modifique o espaço em disco das VMs.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-335">On the **Review Disk Allocation** page, review and if necessary, modify the disk space for the VMs.</span></span> <span data-ttu-id="9b1dd-336">As alocações de disco recomendadas se baseiam no intervalo de retenção especificado na página **Especificar Metas de Curto Prazo**, no tipo de carga de trabalho e no tamanho dos dados protegidos (identificados na etapa 3).</span><span class="sxs-lookup"><span data-stu-id="9b1dd-336">The recommended disk allocations are based on the retention range that is specified in the **Specify Short-Term Goals** page, the type of workload, and the size of the protected data (identified in step 3).</span></span>  

  - <span data-ttu-id="9b1dd-337">**Tamanho dos dados:** tamanho dos dados no grupo de proteção.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-337">**Data size:** Size of the data in the protection group.</span></span>
  - <span data-ttu-id="9b1dd-338">**Espaço em disco:** a quantidade de espaço em disco recomendada para o grupo de proteção.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-338">**Disk space:** The recommended amount of disk space for the protection group.</span></span> <span data-ttu-id="9b1dd-339">Se você desejar modificar essa configuração, deverá alocar um espaço total ligeiramente maior do que o aumento estimado para cada fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-339">If you want to modify this setting, you should allocate total space that is slightly larger than the amount that you estimate each data source grows.</span></span>
  - <span data-ttu-id="9b1dd-340">**Colocar dados:** se você ativar a colocação, várias fontes de dados na proteção poderão ser mapeadas para um único volume de réplica e ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-340">**Colocate data:** If you turn on colocation, multiple data sources in the protection can map to a single replica and recovery point volume.</span></span> <span data-ttu-id="9b1dd-341">A colocação não tem suporte para todas as cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-341">Colocation isn't supported for all workloads.</span></span>
  - <span data-ttu-id="9b1dd-342">**Aumentar automaticamente:** se você ativar essa configuração, caso os dados no grupo protegido excedam a alocação inicial, o System Center Data Protection Manager tentará aumentar o tamanho do disco em 25%.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-342">**Automatically grow:** If you turn on this setting, if data in the protected group outgrows the initial allocation, System Center Data Protection Manager tries to increase the disk size by 25 percent.</span></span>
  - <span data-ttu-id="9b1dd-343">**Detalhes do pool de armazenamento:** mostra o status do pool de armazenamento, incluindo o tamanho do disco total e restante.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-343">**Storage pool details:** Shows the status of the storage pool, including total and remaining disk size.</span></span>

    ![Examinar a alocação de disco](./media/backup-azure-backup-server-vmware/review-disk-allocation.png)

    <span data-ttu-id="9b1dd-345">Quando estiver satisfeito com as metas de curto prazo, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-345">When you are satisfied with the space allocation, click **Next**.</span></span>

7. <span data-ttu-id="9b1dd-346">Na página **Escolher Método de Criação de Réplica**, especifique como deseja gerar a cópia inicial ou a réplica dos dados protegidos no Servidor de Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-346">On the **Choose Replica Creation Method** page, specify how you want to generate the initial copy, or replica, of the protected data on Azure Backup Server.</span></span>

    <span data-ttu-id="9b1dd-347">O padrão é **Automaticamente pela rede** e **Agora**.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-347">The default is **Automatically over the network** and **Now**.</span></span> <span data-ttu-id="9b1dd-348">Se você usar o padrão, é recomendável especificar um horário fora do horário de pico.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-348">If you use the default, we recommend that you specify an off-peak time.</span></span> <span data-ttu-id="9b1dd-349">Escolha **Mair tarde** e especifique um dia e hora.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-349">Choose **Later** and specify a day and time.</span></span>

    <span data-ttu-id="9b1dd-350">Para grandes quantidades de dados ou condições de rede abaixo do ideal, considere a possibilidade de replicar os dados offline usando uma mídia removível.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-350">For large amounts of data or less-than-optimal network conditions, consider replicating the data offline by using removable media.</span></span>

    <span data-ttu-id="9b1dd-351">Depois de fazer suas escolhas, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-351">After you have made your choices, click **Next**.</span></span>

    ![Escolher método de criação de réplica](./media/backup-azure-backup-server-vmware/replica-creation.png)

8. <span data-ttu-id="9b1dd-353">Na página **Opções de Verificação de Consistência**, selecione como e quando automatizar as verificações de consistência.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-353">On the **Consistency Check Options** page, select how and when to automate the consistency checks.</span></span> <span data-ttu-id="9b1dd-354">Você pode executar verificações de consistência quando dados de réplica se tornam inconsistentes ou de acordo com um agendamento definido.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-354">You can run consistency checks when replica data becomes inconsistent, or on a set schedule.</span></span>

    <span data-ttu-id="9b1dd-355">Se você não desejar configurar verificações de consistência automáticas, poderá executar uma verificação manual.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-355">If you don't want to configure automatic consistency checks, you can run a manual check.</span></span> <span data-ttu-id="9b1dd-356">Na área de proteção do console do Servidor de Backup do Azure, clique com o botão direito do mouse no grupo de proteção e, depois, selecione **Executar Verificação de Consistência**.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-356">In the protection area of the Azure Backup Server console, right-click the protection group and then select **Perform Consistency Check**.</span></span>

    <span data-ttu-id="9b1dd-357">Clique em **Avançar** para ir para a próxima página.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-357">Click **Next** to move to the next page.</span></span>

9. <span data-ttu-id="9b1dd-358">Na página **Especificar Dados de Proteção Online**, selecione uma ou mais fontes de dados que você deseja proteger.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-358">On the **Specify Online Protection Data** page, select one or more data sources that you want to protect.</span></span> <span data-ttu-id="9b1dd-359">Você pode selecionar os membros individualmente ou clicar em **Selecionar tudo** para escolher todos os membros.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-359">You can select the members individually, or click **Select All** to choose all members.</span></span> <span data-ttu-id="9b1dd-360">Depois de escolher os membros, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-360">After you choose the members, click **Next**.</span></span>

    ![Especificar dados de proteção online](./media/backup-azure-backup-server-vmware/select-data-to-protect.png)

10. <span data-ttu-id="9b1dd-362">Na página **Especificar Agendamento de Backup Online**, especifique o agendamento para gerar pontos de recuperação do backup de disco.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-362">On the **Specify Online Backup Schedule** page, specify the schedule to generate recovery points from the disk backup.</span></span> <span data-ttu-id="9b1dd-363">Quando o ponto de recuperação é gerado, ele é transferido para o cofre dos Serviços de Recuperação no Azure.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-363">After the recovery point is generated, it is transferred to the Recovery Services vault in Azure.</span></span> <span data-ttu-id="9b1dd-364">Quando estiver satisfeito com o agendamento de backup online, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-364">When you are satisfied with the online backup schedule, click **Next**.</span></span>

    ![Especifique o cronograma do backup online](./media/backup-azure-backup-server-vmware/online-backup-schedule.png)

11. <span data-ttu-id="9b1dd-366">Na página **Especificar Política de Retenção Online**, indique por quanto tempo deseja manter os dados de backup no Azure.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-366">On the **Specify Online Retention Policy** page, indicate how long you want to retain the backup data in Azure.</span></span> <span data-ttu-id="9b1dd-367">Depois que a política for definida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-367">After the policy is defined, click **Next**.</span></span>

    ![Especificar política de retenção online](./media/backup-azure-backup-server-vmware/retention-policy.png)

    <span data-ttu-id="9b1dd-369">Não há um tempo limite para manter dados no Azure.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-369">There is no time limit for how long you can keep data in Azure.</span></span> <span data-ttu-id="9b1dd-370">Ao armazenar dados de ponto de recuperação no Azure, o único limite é que você não pode ter mais de 9.999 pontos de recuperação por instância protegida.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-370">When you store recovery point data in Azure, the only limit is that you cannot have more than 9999 recovery points per protected instance.</span></span> <span data-ttu-id="9b1dd-371">Neste exemplo, a instância protegida é o servidor VMware.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-371">In this example, the protected instance is the VMware server.</span></span>

12. <span data-ttu-id="9b1dd-372">Na página **Resumo**, examine os detalhes dos membros do grupo de proteção e as configurações e, em seguida, clique em **Criar Grupo**.</span><span class="sxs-lookup"><span data-stu-id="9b1dd-372">On the **Summary** page, review the details for your protection group members and settings, and then click **Create Group**.</span></span>

    ![Resumo da configuração e do membro do grupo de proteção](./media/backup-azure-backup-server-vmware/protection-group-summary.png)

## <a name="next-steps"></a><span data-ttu-id="9b1dd-374">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9b1dd-374">Next steps</span></span>
<span data-ttu-id="9b1dd-375">Se você usar o Servidor de Backup do Azure para proteger cargas de trabalho do VMware, talvez esteja interessado em usar o Servidor de Backup do Azure para ajudar a proteger um [Microsoft Exchange Server](./backup-azure-exchange-mabs.md), um [farm do Microsoft SharePoint](./backup-azure-backup-sharepoint-mabs.md) ou um [banco de dados do SQL Server](./backup-azure-sql-mabs.md).</span><span class="sxs-lookup"><span data-stu-id="9b1dd-375">If you use Azure Backup Server to protect VMware workloads, you may be interested in using Azure Backup Server to help protect a [Microsoft Exchange server](./backup-azure-exchange-mabs.md), a [Microsoft SharePoint farm](./backup-azure-backup-sharepoint-mabs.md), or a [SQL Server database](./backup-azure-sql-mabs.md).</span></span>

<span data-ttu-id="9b1dd-376">Para obter informações sobre problemas ao registrar o agente, configurar o grupo de proteção ou fazer backup de trabalhos, consulte [Solucionar problemas do Servidor de Backup do Azure](./backup-azure-mabs-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="9b1dd-376">For information on problems with registering the agent, configuring the protection group, or backing up jobs, see [Troubleshoot Azure Backup Server](./backup-azure-mabs-troubleshoot.md).</span></span>
