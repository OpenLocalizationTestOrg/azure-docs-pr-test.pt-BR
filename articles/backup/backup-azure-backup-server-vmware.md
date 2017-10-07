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
# <a name="back-up-a-vmware-server-tooazure"></a>Fazer backup de um tooAzure de servidor do VMware

Este artigo explica como tooconfigure Azure Backup Server toohelp proteger cargas de trabalho de servidor VMware. Este artigo pressupõe que você já tenha o Servidor de Backup do Azure instalado. Se você não tiver o Azure Backup Server instalado, consulte [preparar tooback cargas de trabalho usando o servidor de Backup do Azure](backup-azure-microsoft-azure-backup.md).

O Servidor de Backup do Azure pode fazer backup ou ajudar a proteger o VMware vCenter Server versão 6.5, 6.0 e 5.5.


## <a name="create-a-secure-connection-toohello-vcenter-server"></a>Criar um servidor do vCenter toohello conexão segura

Por padrão, o Servidor de Backup do Azure se comunica com cada vCenter Server por um canal HTTPS. tooturn na comunicação segura hello, recomendamos que você instale o certificado de autoridade de certificação do VMware (CA) de saudação no servidor de Backup do Azure. Se você não exige comunicação segura e prefere requisito do toodisable Olá HTTPS, consulte [protocolo de comunicação seguro desabilitar](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol). toocreate uma conexão segura entre o servidor de Backup do Azure e Olá servidor vCenter, importe o certificado de confiança de saudação no servidor de Backup do Azure.

Normalmente, você usa um navegador no hello Azure Backup Server máquina tooconnect toohello vCenter Server via Olá vSphere cliente Web. Olá primeira vez que você usar o hello Azure Backup Server navegador tooconnect toohello vCenter Server, conexão Olá não é segura. Olá a imagem a seguir mostra uma conexão não segura de saudação.

![Exemplo de conexão não segura tooVMware servidor](./media/backup-azure-backup-server-vmware/unsecure-url.png)

toofix esse problema e criar uma conexão segura, baixe os certificados da AC raiz confiável de saudação.

1. No navegador de saudação no servidor de Backup do Azure, digite Olá URL toohello vSphere cliente Web. página de logon de cliente Web Hello vSphere é exibida.

    ![Cliente Web vSphere](./media/backup-azure-backup-server-vmware/vsphere-web-client.png)

    Na parte inferior de saudação de informações de saudação para administradores e desenvolvedores, localize Olá **certificados de autoridade de certificação raiz confiável para Download** link.

    ![Certificados de CA raiz do link toodownload Olá confiável](./media/backup-azure-backup-server-vmware/vmware-download-ca-cert-prompt.png)

  Se você não vir a página de logon de cliente Web hello vSphere, verifique as configurações de proxy do navegador.

2. Clique em **Baixar certificados de autoridade de certificação raiz confiável**.

    Servidor do vCenter Olá baixa um computador local do arquivo tooyour. Olá nome do arquivo é nomeado **baixar**. Dependendo de seu navegador, você receberá uma mensagem perguntando se tooopen ou salvar o arquivo hello.

    ![Baixar a mensagem quando certificados são baixados](./media/backup-azure-backup-server-vmware/download-certs.png)

3. Olá arquivo tooa local para salvar no servidor de Backup do Azure. Quando você salvar o arquivo hello, adicione a extensão de nome de arquivo hello. zip.

    arquivo Hello é um arquivo. zip que contém informações de saudação sobre certificados de saudação. Com a extensão. zip de hello, você pode usar ferramentas de extração de saudação.

4. Clique com botão direito **download.zip**e, em seguida, selecione **extrair tudo** tooextract conteúdo de saudação.

    arquivo. zip de saudação extrai sua pasta de tooa conteúdo denominada **certificados**. Dois tipos de arquivos aparecem na pasta de certificados de saudação. arquivo do certificado raiz Olá tem uma extensão que começa com uma sequência numerada como.0 e.1.
    
    arquivo de lista de certificados Revogados Olá tem uma extensão que começa com uma sequência como .r0 ou .r1. arquivo de lista de certificados Revogados Hello está associado um certificado.

    ![Baixar o arquivo extraído localmente ](./media/backup-azure-backup-server-vmware/extracted-files-in-certs-folder.png)

5. Em Olá **certificados** pasta, clique no arquivo do certificado raiz Olá e clique **Renomear**.

    ![Renomear o certificado raiz ](./media/backup-azure-backup-server-vmware/rename-cert.png)

    Alteração extensão too.crt do certificado de raiz Olá. Quando você for questionado se deseja que a extensão de saudação toochange, clique em **Sim** ou **Okey**. Caso contrário, você pode alterar função pretendido do arquivo hello. ícone Olá Olá alterações tooan ícone do arquivo que representa um certificado raiz.

6. Certificado de raiz hello e menu pop-up de saudação, selecione **Instalar certificado**.

    Olá **Assistente de importação de certificado** caixa de diálogo é exibida.

7. Em Olá **Assistente de importação de certificado** caixa de diálogo, selecione **Máquina Local** como destino Olá Olá certificado e clique **próximo** toocontinue.

    ![Opções de destino do armazenamento de certificados ](./media/backup-azure-backup-server-vmware/certificate-import-wizard1.png)

    Se você for questionado se deseja que o computador de toohello do tooallow alterações, clique em **Sim** ou **Okey**, alterações de saudação tooall.

8. Em Olá **repositório de certificados** página, selecione **colocar todos os certificados no hello repositório a seguir**e, em seguida, clique em **procurar** toochoose repositório de certificados de saudação.

    ![Colocar os certificados em um ponto de armazenamento específico](./media/backup-azure-backup-server-vmware/cert-import-wizard-local-store.png)

    Olá **Selecionar repositório de certificados** caixa de diálogo é exibida.

    ![Hierarquia de pastas do armazenamento de certificados](./media/backup-azure-backup-server-vmware/cert-store.png)

9. Selecione **autoridades de certificação raiz confiáveis** como pasta de destino Olá para certificados hello e clique **Okey**.

    ![Pasta de destino do certificado](./media/backup-azure-backup-server-vmware/certificate-store-selected.png)

    Olá **autoridades de certificação raiz confiáveis** pasta é confirmada como repositório de certificados de saudação. Clique em **Avançar**.

    ![Pasta de repositório de certificados](./media/backup-azure-backup-server-vmware/certificate-import-wizard2.png)

10. Em Olá **Olá Concluindo o Assistente de importação de certificado** página, verifique se esse certificado Olá está na pasta desejada Olá e, em seguida, clique em **concluir**.

    ![Verifique se o certificado está na pasta adequada Olá](./media/backup-azure-backup-server-vmware/cert-wizard-final-screen.png)

    Importação de certificado bem-sucedida Olá aparecerá uma caixa de diálogo é confirmada.

11. Entrar no vCenter toohello tooconfirm de servidor que a conexão é segura.

  Se a importação de certificados de saudação não for bem-sucedida, e você não pode estabelecer uma conexão segura, consulte documentação do hello VMware vSphere em [obter certificados de servidor](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).

  Se você tiver limites de segurança dentro da sua organização e não quiser tooturn em Olá protocolo HTTPS, use Olá proteger as comunicações para Olá toodisable procedimento a seguir.

### <a name="disable-secure-communication-protocol"></a>Desabilite seu protocolo de comunicação segura

Se sua organização não exigir o protocolo HTTPS de saudação, use Olá etapas toodisable HTTPS a seguir. toodisable Olá comportamento padrão, crie uma chave do registro que ignora o comportamento padrão de saudação.

1. Copie e cole Olá texto a seguir em um arquivo. txt.

  ```
  Windows Registry Editor Version 5.00
  [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\VMWare]
  "IgnoreCertificateValidation"=dword:00000001
  ```

2. Salve o computador de servidor de Backup do Azure de tooyour de arquivo hello. Nome de arquivo hello, use DisableSecureAuthentication.reg.

3. Clique duas vezes em entrada de registro do hello arquivo tooactivate hello.


## <a name="create-a-role-and-user-account-on-hello-vcenter-server"></a>Criar uma conta de usuário e a função no servidor do vCenter Olá

No servidor do vCenter hello, uma função é um conjunto predefinido de privilégios. Um administrador de servidor do vCenter cria funções hello. permissões de tooassign administrador Olá pares contas de usuário com uma função. tooestablish Olá usuário necessárias credenciais tooback o computador de servidor do vCenter Olá, criar uma função com privilégios específicos e associar conta de usuário Olá função hello.

Servidor de Backup do Azure usa um nome de usuário e senha tooauthenticate com o servidor do vCenter hello. O Servidor de Backup do Azure utiliza essas credenciais como autenticação para todas as operações de backup.

tooadd um função de servidor do vCenter e seus privilégios para um administrador de backup:

1. Entrar no servidor do vCenter toohello e, em seguida, no servidor do vCenter Olá **navegador** do painel, clique em **administração**.

    ![Opção de administração no painel Navegador do vCenter Server](./media/backup-azure-backup-server-vmware/vmware-navigator-panel.png)

2. Em **administração** selecione **funções**e, em seguida, em Olá **funções** clique de painel Olá Adicionar ícone de função (Olá + símbolo).

    ![Adicionar função](./media/backup-azure-backup-server-vmware/vmware-define-new-role.png)

    Olá **Criar função** caixa de diálogo é exibida.

    ![Criar função](./media/backup-azure-backup-server-vmware/vmware-define-new-role-priv.png)

3. Em Olá **Criar função** caixa de diálogo Olá **nome da função** , digite *BackupAdminRole*. nome da função Hello pode ser como desejar, mas ele deve ser reconhecível para a finalidade da função hello.

4. Selecione Olá privilégios para a versão apropriada de saudação do vCenter e, em seguida, clique em **Okey**. Olá, a tabela a seguir identifica os privilégios de Olá necessária para vCenter 6.0 e vCenter 5.5.

  Quando você seleciona privilégios hello, clique em Olá ícone próximo toohello pai rótulo tooexpand Olá pai e o modo de exibição Olá filho privilégios. privilégios de máquina virtual de saudação tooselect, você precisa toogo vários níveis em Olá pai de hierarquia filho. Você não precisa tooselect todos os privilégios do filho dentro de um privilégio de pai.

  ![Hierarquia de privilégios pai-filho](./media/backup-azure-backup-server-vmware/cert-add-privilege-expand.png)

  Depois de clicar em **Okey**, Olá nova função é exibida na lista de saudação no painel de funções hello.

|Privilégios do vCenter 6.0| Privilégios do vCenter 5.5|
|--------------------------|---------------------------|
|Datastore.AllocateSpace   | Datastore.AllocateSpace|
|Global.ManageCustomFields | Global.ManageCustomerFields|
|Global.SetCustomFields    |   |
|Host.Local.CreateVM       | Network.Assign |
|Network.Assign            |  |
|Resource.AssignVMToPool   |  |
|VirtualMachine.Config.AddNewDisk  | VirtualMachine.Config.AddNewDisk   |
|VirtualMachine.Config.AdvanceConfig| VirtualMachine.Config.AdvancedConfig|
|VirtualMachine.Config.ChangeTracking| VirtualMachine.Config.ChangeTracking |
|VirtualMachine.Config.HostUSBDevice||
|VirtualMachine.Config.QueryUnownedFiles|    |
|VirtualMachine.Config.SwapPlacement| VirtualMachine.Config.SwapPlacement |
|VirtualMachine.Interact.PowerOff| VirtualMachine.Interact.PowerOff |
|VirtualMachine.Inventory.Create| VirtualMachine.Inventory.Create |
|VirtualMachine.Provisioning.DiskRandomAccess| |
|VirtualMachine.Provisioning.DiskRandomRead|VirtualMachine.Provisioning.DiskRandomRead |
|VirtualMachine.State.CreateSnapshot| VirtualMachine.State.CreateSnapshot|
|VirtualMachine.State.RemoveSnapshot|VirtualMachine.State.RemoveSnapshot |
</br>



## <a name="create-a-vcenter-server-user-account-and-permissions"></a>Criar uma conta de usuário do vCenter Server e as permissões

Depois de configurar a função hello com privilégios, crie uma conta de usuário. conta de usuário de saudação tem um nome e uma senha, que fornece credenciais de saudação que são usadas para autenticação.

1. toocreate uma conta de usuário no servidor do vCenter Olá **navegador** do painel, clique em **usuários e grupos**.

    ![Opção de Usuários e Grupos](./media/backup-azure-backup-server-vmware/vmware-userandgroup-panel.png)

    Olá **vCenter usuários e grupos** painel é exibido.

    ![Painel Usuários e Grupos do vCenter](./media/backup-azure-backup-server-vmware/usersandgroups.png)

2. Em Olá **vCenter usuários e grupos** painel, selecione Olá **usuários** guia e, em seguida, clique em Olá Adicionar ícone de usuários (Olá + símbolo).

    Olá **novo usuário** caixa de diálogo é exibida.

3. Em Olá **novo usuário** caixa de diálogo caixa, adicione informações de saudação do usuário e, em seguida, clique em **Okey**. Neste procedimento, o nome de usuário de saudação é BackupAdmin.

    ![Caixa de diálogo Novo Usuário](./media/backup-azure-backup-server-vmware/vmware-new-user-account.png)

    nova conta de usuário Olá aparece na lista de saudação.

4. conta de usuário de saudação tooassociate na função hello, em Olá **navegador** do painel, clique em **permissões globais**. Em Olá **permissões globais** painel, selecione Olá **gerenciar** guia e, em seguida, clique em Olá Adicionar ícone (Olá + símbolo).

    ![Painel Permissões Globais](./media/backup-azure-backup-server-vmware/vmware-add-new-perms.png)

    Olá **raiz de permissões globais - adicionar permissão** caixa de diálogo é exibida.

5. Em Olá **raiz de permissão Global - adicionar permissão** caixa de diálogo, clique em **adicionar** toochoose Olá usuário ou grupo.

    ![Escolher o usuário ou o grupo](./media/backup-azure-backup-server-vmware/vmware-add-new-global-perm.png)

    Olá **selecionar usuários/grupos** caixa de diálogo é exibida.

6. Em Olá **selecionar usuários/grupos** caixa de diálogo caixa, escolha **BackupAdmin** e, em seguida, clique em **adicionar**.

    Em **usuários**, Olá *domínio \ nomedeusuário* formato é usado para a conta de usuário de saudação. Se você quiser toouse um domínio diferente, escolha-o no hello **domínio** lista.

    ![Adicionar um usuário BackupAdmin](./media/backup-azure-backup-server-vmware/vmware-assign-account-to-role.png)

    Clique em **Okey** tooadd Olá selecionado usuários toohello **adicionar permissão** caixa de diálogo.

7. Agora que você identificou que o usuário hello, atribua a função de toohello de usuário de saudação. Em **função atribuída**, na lista suspensa de Olá, selecione **BackupAdminRole**e, em seguida, clique em **Okey**.

    ![Atribuir o usuário toorole](./media/backup-azure-backup-server-vmware/vmware-choose-role.png)

  Em Olá **gerenciar** guia Olá **permissões globais** painel, a nova conta de usuário hello e função hello associado aparecem na lista de saudação.


## <a name="establish-vcenter-server-credentials-on-azure-backup-server"></a>Estabelecer as credenciais de servidor do vCenter no servidor de Backup do Azure

Antes de adicionar Olá VMware server tooAzure fazer Backup do servidor, instale o [atualização 1 para o Azure Backup Server](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).

1. tooopen servidor de Backup do Azure, clique duas vezes o ícone de saudação na área de trabalho do hello Azure Backup Server.

    ![Ícone do Servidor de Backup do Azure](./media/backup-azure-backup-server-vmware/mabs-icon.png)

    Se você não encontrar o ícone de saudação na área de trabalho hello, abra o Azure Backup Server da lista de saudação dos aplicativos instalados. nome do aplicativo de servidor de Backup do Azure Olá é chamado de Backup do Microsoft Azure.

2. No console do servidor de Backup do Azure hello, clique em **gerenciamento**, clique em **servidores de produção**e clique na faixa de opções de ferramenta hello, **VMware gerenciar**.

    ![Console do Servidor de Backup do Azure](./media/backup-azure-backup-server-vmware/add-vmware-credentials.png)

    Olá **gerenciar credenciais** caixa de diálogo é exibida.

    ![Caixa de diálogo Gerenciar Credenciais do Servidor de Backup do Azure](./media/backup-azure-backup-server-vmware/mabs-manage-credentials-dialog.png)

3. Em Olá **gerenciar credenciais** caixa de diálogo, clique em **adicionar** tooopen Olá **Add Credential** caixa de diálogo.

4. Em Olá **Add Credential** caixa de diálogo, digite um nome e uma descrição para a nova credencial de saudação. Em seguida, especifique Olá nome de usuário e senha. nome Hello, *Contoso Vcenter credencial* usado credencial de saudação tooidentify no procedimento a seguir Olá. Use Olá mesmo nome de usuário e senha que é usada para Olá vCenter Server. Se o servidor do vCenter hello e servidor de Backup do Azure não estão no Olá mesmo domínio, em **nome de usuário**, especifique o domínio de saudação.

    ![Caixa de diálogo Adicionar Credencial do Servidor de Backup do Azure](./media/backup-azure-backup-server-vmware/mabs-add-credential-dialog2.png)

    Clique em **adicionar** tooadd Olá nova credencial tooAzure fazer Backup do servidor. nova credencial de saudação aparece na lista de saudação no hello **gerenciar credenciais** caixa de diálogo.
    
    ![Caixa de diálogo Gerenciar Credenciais do Servidor de Backup do Azure](./media/backup-azure-backup-server-vmware/new-list-of-mabs-creds.png)

5. Olá tooclose **gerenciar credenciais** caixa de diálogo, clique em Olá **X** no canto superior direito de saudação.


## <a name="add-hello-vcenter-server-tooazure-backup-server"></a>Adicionar Olá vCenter Server tooAzure fazer Backup do servidor

Assistente de adição de servidor de produção é usado tooadd Olá vCenter Server tooAzure fazer Backup do servidor.

tooopen Assistente de adição de servidor de produção, Olá completa procedimento a seguir:

1. No console do servidor de Backup do Azure hello, clique em **gerenciamento**, clique em **servidores de produção**e, em seguida, clique em **adicionar**.

    ![Abra o Assistente de Adição de Servidor de Produção](./media/backup-azure-backup-server-vmware/add-vcenter-to-mabs.png)

    Olá **Assistente de adição de servidor de produção** caixa de diálogo é exibida.

    ![Assistente de Adição de Servidor de Produção](./media/backup-azure-backup-server-vmware/production-server-add-wizard.png)

2. Em Olá **tipo Selecionar servidor de produção** , selecione **servidores VMware**e, em seguida, clique em **próximo**.

3. Em **endereço IP/nome do servidor**, especifique o nome de domínio totalmente qualificado da saudação (FQDN) ou endereço IP do servidor do VMware hello. Se todos os servidores de ESXi Olá são gerenciados pelo Olá mesmo vCenter, você pode usar o nome hello vCenter.

    ![Especificar o FQDN ou o endereço IP do servidor do VMware](./media/backup-azure-backup-server-vmware/add-vmware-server-provide-server-name.png)

4. Em **porta SSL**, insira a porta Olá toocommunicate usado com o servidor do VMware hello. Use a porta 443, que é a porta padrão de hello, a menos que você sabe que uma porta diferente é necessária.

5. Em **especificar credenciais**, selecione Olá credencial que você criou anteriormente.

    ![Especificar credencial](./media/backup-azure-backup-server-vmware/identify-creds.png)

6. Clique em **adicionar** tooadd Olá VMware toohello lista de servidor **adicionado servidores do VMware**e, em seguida, clique em **próximo** toomove toohello próxima página no Assistente de saudação.

    ![Adicionar servidor do VMware e a credencial](./media/backup-azure-backup-server-vmware/add-vmware-server-credentials.png)

7. Em Olá **resumo** , clique em **adicionar** tooadd Olá especificado VMware tooAzure de servidor servidor de Backup.

    ![Adicionar VMware tooAzure de servidor servidor de Backup](./media/backup-azure-backup-server-vmware/tasks-screen.png)

  backup do servidor VMware Olá é um backup sem agente e Olá novo servidor é adicionado imediatamente. Olá **concluir** página mostra Olá resultados.

  ![Página Concluir](./media/backup-azure-backup-server-vmware/summary-screen.png)

  tooadd várias instâncias do vCenter Server tooAzure servidor de Backup, repita Olá anterior as etapas nesta seção.

Depois de adicionar Olá vCenter Server tooAzure servidor de Backup, Olá próxima etapa é toocreate um grupo de proteção. grupo de proteção de saudação especifica Olá diversos detalhes para a retenção de curto e longo prazo e é onde você pode define e aplica a política de backup hello. política de backup Olá é agenda Olá para quando os backups ocorrem e o que é feito backup.


## <a name="configure-a-protection-group"></a>Configurar grupo de proteção

Se você não tiver usado o System Center Data Protection Manager ou o servidor de Backup do Azure antes, consulte [planejar backups em disco](https://technet.microsoft.com/library/hh758026.aspx) tooprepare seu ambiente de hardware. Depois de verificar se você tem o armazenamento adequado, use máquinas virtuais VMware de tooadd do hello criar novo grupo de proteção Assistente.

1. No console do servidor de Backup do Azure hello, clique em **proteção**e na faixa de opções de ferramenta hello, clique em **novo** tooopen Assistente para criar novo grupo de proteção de saudação.

    ![Assistente para criar novo grupo de proteção de Olá aberto](./media/backup-azure-backup-server-vmware/open-protection-wizard.png)

    Olá **criar novo grupo de proteção** caixa de diálogo do assistente será exibida.

    ![Caixa de diálogo Assistente para Criar Novo Grupo de Proteção](./media/backup-azure-backup-server-vmware/protection-wizard.png)

    Clique em **próximo** tooadvance toohello **Selecionar tipo de grupo de proteção** página.

2. Em Olá **tipo de grupo de proteção selecione** , selecione **servidores** e, em seguida, clique em **próximo**. Olá **selecionar membros do grupo** página será exibida.

3. Em Olá **selecionar membros do grupo** página, membros disponíveis hello e membros de saudação selecionado são exibidos. Selecione Olá membros que você deseja tooprotect e, em seguida, clique em **próximo**.

    ![Selecionar membros do grupo](./media/backup-azure-backup-server-vmware/server-add-selected-members.png)

    Ao selecionar um membro, se você selecionar uma pasta que contém outras pastas ou VMs, essas pastas e VMs também serão selecionadas. inclusão de saudação de pastas de saudação e VMs na pasta pai de saudação é chamado de proteção em nível de pasta. tooremove uma pasta ou a VM, a caixa de seleção Limpar hello.

    Se uma VM ou uma pasta que contém uma VM, já está protegido tooAzure, você não pode selecionar o VM novamente. Ou seja, depois que uma VM for tooAzure protegido, ele não pode ser protegido novamente, que impede que pontos de recuperação duplicados sejam criadas para uma máquina virtual. Se você quiser toosee qual instância de servidor de Backup do Azure já protege um membro, um nome de saudação do toohello ponto membro toosee de saudação protegendo o servidor.

4. Em Olá **Selecionar método de proteção de dados** , insira um nome para o grupo de proteção de saudação. Proteção de curto prazo (toodisk) e online são selecionadas. Se você quiser toouse de proteção online (tooAzure), você deve usar toodisk de proteção de curto prazo. Clique em **próximo** tooproceed toohello curto período de proteção.

    ![Selecionar método de proteção de dados](./media/backup-azure-backup-server-vmware/name-protection-group.png)

5. Em Olá **especificar objetivos de curto prazo** página, para **período de retenção**, especifique Olá número de dias que os pontos de recuperação tooretain que estão *armazenado toodisk*. Tempo de saudação toochange e quando os pontos de recuperação são obtidos de dias, clique em **modificar**. pontos de recuperação de curto prazo de saudação são backups completos. Não são backups incrementais. Quando estiver satisfeito com os objetivos de curto prazo hello, clique em **próximo**.

    ![Especificar objetivos de curto prazo](./media/backup-azure-backup-server-vmware/short-term-goals.png)

6. Em Olá **rever alocação do disco** página, revise e se necessário, modifique a espaço em disco Olá para Olá VMs. Olá recomendados alocações de disco são com base no período de retenção de saudação que é especificado no hello **especificar objetivos de curto prazo** página, tipo de saudação de carga de trabalho e tamanho de saudação de saudação (identificados na etapa 3) de dados protegidos.  

  - **Tamanho dos dados:** tamanho dos dados Olá Olá grupo de proteção.
  - **Espaço em disco:** Olá recomendado a quantidade de espaço em disco para o grupo de proteção de saudação. Se você quiser toomodify essa configuração, você deve alocar espaço total que é ligeiramente maior do que a quantidade de saudação que você estima que cada fonte de dados cresce.
  - **Colocar os dados:** se você ativar a colocação, várias fontes de dados na proteção Olá podem mapear tooa única réplica e volume de ponto de recuperação. A colocação não tem suporte para todas as cargas de trabalho.
  - **Aumentar automaticamente:** se você ativar essa configuração, se os dados no grupo de saudação protegido ultrapassarem alocação inicial hello, System Center Data Protection Manager tenta tamanho do disco Olá tooincrease em 25 por cento.
  - **Detalhes do pool de armazenamento:** mostra o status Olá Olá do pool de armazenamento, incluindo total e restante tamanho do disco.

    ![Examinar a alocação de disco](./media/backup-azure-backup-server-vmware/review-disk-allocation.png)

    Quando estiver satisfeito com a alocação de espaço de saudação, clique em **próximo**.

7. Em Olá **escolher método de criação de réplica** , especifique como você deseja que a cópia inicial toogenerate hello, ou réplica dos dados Olá protegido no servidor de Backup do Azure.

    saudação padrão é **automaticamente pela rede Olá** e **agora**. Se você usar o padrão de saudação, recomendamos que você especifique um horário de pico. Escolha **Mair tarde** e especifique um dia e hora.

    Para grandes quantidades de dados ou condições de rede menos ideal, considere a possibilidade de replicar dados Olá offline usando mídia removível.

    Depois de fazer suas escolhas, clique em **Avançar**.

    ![Escolher método de criação de réplica](./media/backup-azure-backup-server-vmware/replica-creation.png)

8. Em Olá **opções de verificação de consistência** página, selecione como e quando as verificações de consistência de saudação do tooautomate. Você pode executar verificações de consistência quando dados de réplica se tornam inconsistentes ou de acordo com um agendamento definido.

    Se você não quiser tooconfigure verificações de consistência automática, você pode executar uma verificação manual. Na área de proteção de saudação do console do servidor de Backup do Azure hello, clique o grupo de proteção hello e, em seguida, selecione **executar verificação de consistência**.

    Clique em **próximo** toomove toohello próxima página.

9. Em Olá **especificar dados de proteção Online** , selecione uma ou mais fontes de dados que você deseja tooprotect. Você pode selecionar membros Olá individualmente, ou clique em **Selecionar tudo** toochoose todos os membros. Depois que você escolher membros hello, clique em **próximo**.

    ![Especificar dados de proteção online](./media/backup-azure-backup-server-vmware/select-data-to-protect.png)

10. Em Olá **especificar agendamento de Backup Online** , especifique os pontos de recuperação de toogenerate Olá agenda saudação do backup de disco. Depois que o ponto de recuperação Olá é gerado, é transferido toohello Cofre de serviços de recuperação no Azure. Quando estiver satisfeito com o agendamento de backup online hello, clique em **próximo**.

    ![Especifique o cronograma do backup online](./media/backup-azure-backup-server-vmware/online-backup-schedule.png)

11. Em Olá **especificar política de retenção Online** página, indique quanto tempo deseja que os dados de backup tooretain Olá no Azure. Após a definição de política de saudação, clique em **próximo**.

    ![Especificar política de retenção online](./media/backup-azure-backup-server-vmware/retention-policy.png)

    Não há um tempo limite para manter dados no Azure. Quando você armazena dados de ponto de recuperação no Azure, hello limite só é que você não pode ter mais de 9999 pontos de recuperação por instância protegida. Neste exemplo, instância protegida Olá é o hello VMware server.

12. Em Olá **resumo** página, examine os detalhes de saudação para os membros do grupo de proteção e as configurações e, em seguida, clique em **criar grupo**.

    ![Resumo da configuração e do membro do grupo de proteção](./media/backup-azure-backup-server-vmware/protection-group-summary.png)

## <a name="next-steps"></a>Próximas etapas
Se você usar cargas de trabalho do Azure Backup Server tooprotect VMware, você pode estar interessado em usar o servidor de Backup do Azure toohelp proteger um [do Microsoft Exchange server](./backup-azure-exchange-mabs.md), um [farm do Microsoft SharePoint](./backup-azure-backup-sharepoint-mabs.md), ou um [Banco de dados do SQL Server](./backup-azure-sql-mabs.md).

Para obter informações sobre problemas com registrar Olá agente, consulte Configurando o grupo de proteção hello, ou fazer backup de trabalhos, [solucionar problemas de servidor de Backup do Azure](./backup-azure-mabs-troubleshoot.md).
