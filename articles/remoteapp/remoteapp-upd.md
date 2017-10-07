---
title: "aaaHow é o Azure RemoteApp salvar as configurações e dados de usuário? | Microsoft Docs"
description: "Saiba como o Azure RemoteApp salva os dados do usuário usando o disco de perfil de usuário de saudação."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: e125af62-5c1a-4186-a238-52f537f7bb34
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: dccebc7861e8a0d87cb3ee174f399a2df7fe023c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-remoteapp-save-user-data-and-settings"></a>Como o Azure RemoteApp salva configurações e dados de usuário?
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

O Azure RemoteApp salva personalizações e a identidade do usuário em dispositivos e sessões. Esses dados de usuário são armazenados em um disco por coleção por usuário, conhecido como um disco de perfil de usuário (UDP). disco Olá segue usuário hello e garante usuário Olá tenha uma experiência consistente, independentemente de onde eles entrarem.

Discos de perfil de usuário são completamente transparentes toohello usuário – usuários salvar a pasta de documentos tootheir documentos (no qual aparece toobe uma unidade local) e alterar as configurações de aplicativo como de costume. AT Olá mesmo tempo, o pessoais de todas as configurações persistirem durante a conexão tooAzure RemoteApp de qualquer dispositivo. Todos os usuários de saudação vê seus dados em Olá mesmo lugar.

Cada UPD tem 50 GB de armazenamento persistente e contém as configurações de dados e aplicativos do usuário. 

Continue lendo para obter informações específicas sobre os dados de perfil do usuário.

> [!NOTE]
> Necessário toodisable Olá UPD? Você pode fazer isso agora - confira a postagem do blog de Pavithra, [Desabilitar Discos de Perfil de Usuário (UPDs) no Azure RemoteApp](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/), para obter detalhes.
> 
> 

## <a name="how-can-an-admin-get-toohello-data"></a>Como um administrador pode obter dados toohello?
Se precisar de tooaccess Olá dados para um dos seus usuários (para recuperação de desastre ou se usuário Olá deixa a empresa Olá), entre em contato com o suporte do Azure e fornecem informações de assinatura de saudação para coleção hello e identidade do usuário hello. equipe do Azure RemoteApp Olá fornecer uma URL toohello VHD. Baixe esse VHD e recupere quaisquer documentos ou arquivos que você precisa. Observe que Olá VHD é 50GB, portanto, levará um pouco toodownload-lo.

## <a name="is-hello-data-backed-up"></a>Saudação de dados é feita?
Sim, vamos salvar um backup de dados de usuário de saudação por localização geográfica. Olá dados é somente leitura e pode ser acessado no Olá mesma forma como dados regulares Olá seria (entre em contato com o Azure RemoteApp tooget ele), se Olá data center primário está inativo. dados de saudação são o local de backup copiado toohello em tempo real e não podemos manter cópias de versões diferentes. Assim, em dados corrompidos, não será capaz de toorestore-Olá de tooa conhecido anteriormente a versão válida, mas se Olá data center primário está inativo, você será capaz de tooget dados do usuário de outro local.

## <a name="how-do-users-see-hello-upd-on-hello-server-side"></a>Como os usuários verão Olá UPD no lado do servidor de saudação?
Cada usuário terá seu próprio diretório no servidor de saudação que mapeia tootheir UPD: c:\Users\username.

## <a name="whats-hello-best-way-toouse-outlook-and-upd"></a>O que é toouse de maneira melhor de saudação Outlook e UPD?
O Azure RemoteApp salva o estado de Outlook hello (caixas de correio, PSTs) entre as sessões. tooenable isso, é necessário Olá toobe PST armazenado nos dados de perfil de usuário de saudação (c:\users\<nome de usuário >). Este é o local padrão de saudação para dados hello, portanto desde que você não alterar o local de saudação, dados saudação persistirá entre sessões.

Também recomendamos que você use o modo "cache" no Outlook e o modo de "servidor/online" para pesquisar.

Confira [este artigo](remoteapp-outlook.md) para obter mais informações sobre como usar o Outlook e o Azure RemoteApp.

## <a name="what-about-redirection"></a>E quanto ao redirecionamento?
Você pode configurar o Azure RemoteApp toolet usuários acessarem dispositivos locais configurando [redirecionamento](remoteapp-redirection.md). Dispositivos locais será capaz de tooaccess dados Olá Olá UPD.

## <a name="can-i-use-my-upd-as-a-network-share"></a>Posso usar meu UPD como um compartilhamento de rede?
Não. Os UPDs não podem ser usados como um compartilhamento de rede. Um UDP está apenas disponível toohello usuário quando o usuário de saudação estiver ativamente conectado tooAzure RemoteApp.

## <a name="if-i-delete-a-user-from-a-collection-is-their-upd-deleted"></a>Se eu excluir um usuário de uma coleção, seu UPD é excluído?
Não, quando você exclui um usuário, nós não excluir automaticamente Olá UPD - em vez disso, podemos armazenar dados de Olá até que você excluir a coleção de saudação. 90 dias após a exclusão de coleção hello, excluímos todos os UPDs. 

Se você precisar toodelete um UPD de uma coleção, entre em contato com o Azure RemoteApp - podemos excluir UPD do nosso lado.

## <a name="can-i-access-my-users-upds-either-current-or-deleted-users"></a>Posso acessar os UPDs dos meus usuários (usuários atuais ou excluídos)?
Sim, se você contatar [Azure RemoteApp](mailto:remoteappforum@microsoft.com), podemos poderá configurá-las com uma URL tooaccess dados saudação. Você terá sobre toodownload 10 horas quaisquer arquivos de dados ou de saudação UPD antes de expira o acesso de saudação.

## <a name="are-upds-available-offline"></a>UPDs ficam disponíveis offline?
No momento, não oferecemos tooUPDs acesso offline, além da janela de acesso de 10 horas Olá descrita acima. Isso significa que, não temos atualmente uma tooprovide de maneira com acesso para tarefas longo o suficiente toocomplete mais complicado, como executar um software antivírus em UPDs hello ou acessar dados de uma auditoria.

## <a name="do-registry-key-settings-persist"></a>As configurações de chave do Registro são persistentes?
Sim, todos os elementos escritos tooHKEY_Current_User faz parte da saudação UPD.

## <a name="can-i-disable-upds-for-a-collection"></a>Posso desativar UPDs para uma coleção?
Sim, solicite Azure RemoteApp toodisable UPDs uma assinatura, mas você não pode fazer essa por conta própria. Isso significa que UPDs serão desabilitados para todos os conjuntos de assinatura de saudação.

Você pode desejar UPDs toodisable em qualquer uma das seguintes situações de saudação: 

* Você precisa concluir o acesso e o controle de dados do usuário (para fins de auditoria e de revisão, como instituições financeiras).
* Você tem 3ª parte usuário perfil soluções de gerenciamento local e deseja toocontinue usá-los em sua implantação do Azure RemoteApp ingressado no domínio. Isso exigiria Olá perfil agente toobe carregado na imagem Olá ouro. 
* Não é necessário qualquer armazenamento de dados local ou ter todos os dados no compartilhamento de arquivo ou nuvem hello e gostaria de salvar toocontrol dados localmente usando o Azure RemoteApp.

Veja [Desabilitar Discos de Perfil do Usuário (UPDs) no Azure RemoteApp](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/) para obter mais informações.

## <a name="can-i-restrict-users-from-saving-data-toohello-system-drive"></a>Pode restringir os usuários salvem a unidade do sistema toohello dados?
Sim, mas você precisará tooset que o modelo Olá antes de criar a coleção de saudação da imagem. Use Olá unidade do sistema toohello tooblock acesso da etapas a seguir:

1. Executar **gpedit. msc** na imagem de modelo hello.
2. Navegue muito**configuração do usuário > modelos administrativos > componentes do Windows > Explorer**.
3. Olá selecione as opções a seguir:
   * **Ocultar estas unidades especificadas em Meu Computador**
   * **Impedir acesso toodrives de Meu computador**

## <a name="can-i-seed-upds-i-want-tooput-some-data-in-hello-upd-thats-available-hello-first-time-hello-user-signs-in"></a>Eu posso propagar UPDs? Desejo tooput alguns dados Olá UPD está disponível Olá Olá usuário faz logon.
Sim, quando você criar a imagem de modelo hello, você pode adicionar informações de perfil de padrão de toohello. Essa informação é adicionada toohello UPD.

## <a name="can-i-change-hello-size-of-hello-upd-depending-on-how-much-data-i-want-toostore"></a>Posso alterar tamanho de saudação do hello UPD dependendo de quantos dados desejo toostore?
Não, todos os UPDs têm 50 GB de armazenamento. Se você quiser toostore diferentes quantidades de dados, tente o seguinte hello:

1. Desabilite UPDs para a coleção de saudação.
2. Configure um compartilhamento de arquivos para os usuários tooaccess.
3. Carga Olá o compartilhamento de arquivos usando um script de inicialização. Consulte abaixo para obter detalhes sobre scripts de inicialização no Azure RemoteApp.
4. Direcione usuários toosave todos os compartilhamento de arquivos toohello de dados.

## <a name="how-do-i-run-a-startup-script-in-azure-remoteapp"></a>Como posso executar um script de inicialização no Azure RemoteApp?
Se você quiser toorun um script de inicialização, iniciar, criando uma tarefa agendada na imagem de modelo Olá for toouse para a coleção de saudação. (Faça isso *antes* de executar o sysprep). 

![Criar uma tarefa do sistema](./media/remoteapp-upd/upd1.png)

![Criar uma tarefa do sistema que seja executada quando um usuário fizer logon](./media/remoteapp-upd/upd2.png)

Em Olá **geral** guia, ser Olá-se de toochange **conta de usuário** em segurança muito "BUILTIN \ usuários."

![Alterar o grupo de tooa de conta de usuário de saudação](./media/remoteapp-upd/upd4.png)

tarefa agendada Olá iniciará o seu script de inicialização, usando credenciais do usuário hello. Agendar Olá tarefa toorun toda vez que um usuário fizer logon.

![Conjunto Olá disparador de tarefa hello como "No logon"](./media/remoteapp-upd/upd3.png)

Você também pode usar [scripts de inicialização baseados na Política de Grupo](https://technet.microsoft.com/library/cc779329%28v=ws.10%29.aspx). 

## <a name="what-about-placing-a-startup-script-in-hello-start-menu-would-that-work"></a>Como colocar um script de inicialização em Olá menu Iniciar? Isso funcionaria?
Em outras palavras, posso criar um arquivo. bat que executa um script de configuração de janela e salvá-lo toohello c:\ProgramData\Microsoft\Windows\Start Iniciar\Programas\Inicializar pasta e, em seguida, solicitar que esse script executado sempre que um usuário inicia uma sessão de RemoteApp?

Não, que não é suportado com o Azure RemoteApp, que usa RDSH, que também não oferece suporte a scripts de inicialização no menu de início de saudação.

## <a name="can-i-use-mstscexe-hello-remote-desktop-program-tooconfigure-logon-scripts"></a>É possível usar scripts de logon de tooconfigure mstsc.exe (programa de área de trabalho remota Olá)?
Não, não há suporte para isso com o Azure RemoteApp.

## <a name="can-i-store-data-on-hello-vm-locally"></a>Pode armazenar dados em Olá VM localmente?
Não, os dados armazenados em qualquer lugar na Olá VM diferente no hello UPD serão perdidos. Não há um usuário de saudação chance de alta não obterá Olá Olá da mesma VM próxima vez que entrar no Azure RemoteApp. Nós não mantemos persistência de VM de usuário para usuário Olá não entrarão em Olá mesma VM e Olá dados serão perdidos. Além disso, quando podemos atualizar coleção hello, Olá que VMs existentes são substituídas por um novo conjunto de VMs - que significa que todos os dados armazenados em Olá própria máquina virtual é perdida. recomendação de saudação é toostore Olá UPD, armazenamento compartilhado, como arquivos do Azure, um servidor de arquivos dentro de uma rede virtual, ou na nuvem hello usando um sistema de armazenamento de nuvem como o DropBox.

## <a name="how-do-i-mount-an-azure-file-share-on-a-vm-using-powershell"></a>Como posso montar um compartilhamento de Arquivos do Azure em uma VM usando o PowerShell?
Você pode usar o hello unidade de saudação do Net-PSDrive cmdlet toomount, da seguinte maneira:

    New-PSDrive -Name <drive-name> -PSProvider FileSystem -Root \\<storage-account-name>.file.core.windows.net\<share-name> -Credential :<storage-account-name>


Você também pode salvar suas credenciais executando Olá seguinte:

    cmdkey /add:<storage-account-name>.file.core.windows.net /user:<storage-account-name> /pass:<storage-account-key>


Isso permite que você ignore Olá - parâmetro de credencial no cmdlet New-PSDrive de saudação.

