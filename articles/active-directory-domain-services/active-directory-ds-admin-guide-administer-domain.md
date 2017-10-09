---
title: "Azure Active Directory Domain Services: administrar um domínio gerenciado | Microsoft Docs"
description: "Administrar domínios gerenciados dos Serviços de Domínio do Azure Active Directory"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: d4fdbc75-3e6b-4e20-8494-5dcc3bf2220a
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 11acc79e06163e3193b1aa981f2cd28af812789d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="administer-an-azure-active-directory-domain-services-managed-domain"></a>Administrar um domínio gerenciado dos Serviços de Domínio do Azure Active Directory
Este artigo mostra como tooadminister um serviços de domínio do Azure Active Directory (AD) gerenciadas domínio.

## <a name="before-you-begin"></a>Antes de começar
tarefas de saudação tooperform listadas neste artigo, você precisa:

1. Uma **assinatura do Azure**válida.
2. Um **diretório do AD do Azure** - seja sincronizado com um diretório local ou com um diretório somente na nuvem.
3. **Serviços de domínio do AD do Azure** devem estar habilitados para diretório de saudação do AD do Azure. Se você ainda não tiver feito isso, siga todas as tarefas de saudação descritas Olá [guia de Introdução](active-directory-ds-getting-started.md).
4. Um **domínio máquina de virtual** do qual você administrar Olá domínio gerenciado por serviços de domínio do AD do Azure. Se você não tiver tal uma máquina virtual, execute todas as tarefas de saudação descritas no artigo Olá intitulado [ingressar em um domínio gerenciado do Windows máquina virtual tooa](active-directory-ds-admin-guide-join-windows-vm.md).
5. Você precisa ter credenciais de saudação de um **usuário conta pertencentes toohello ' AAD controlador de domínio do grupo 'Administradores** em seu diretório, tooadminister seu domínio gerenciado.

<br>

## <a name="administrative-tasks-you-can-perform-on-a-managed-domain"></a>Tarefas administrativas que você pode executar em um domínio gerenciado
Os membros Olá ' AAD DC' do grupo de administradores têm privilégios no domínio gerenciado Olá que lhes permitem tooperform tarefas como:

* Ingresse em domínio gerenciado do máquinas toohello.
* Configure o GPO internos de Olá para contêineres de 'AADDC computadores' e 'AADDC usuários' hello no domínio gerenciado Olá.
* Administre o DNS no domínio gerenciado hello.
* Criar e administrar personalizado OUs (unidades organizacionais) no domínio gerenciado hello.
* Obtenha acesso administrativo toocomputers ingressados no domínio gerenciado toohello.

## <a name="administrative-privileges-you-do-not-have-on-a-managed-domain"></a>Privilégios administrativos que você não tem em um domínio gerenciado
domínio de saudação é gerenciado pela Microsoft, incluindo atividades, como a aplicação de patches, monitoramento e, a execução de backups. Portanto, domínio hello está bloqueado e você não tem privilégios tooperform determinadas tarefas administrativas no domínio hello. Abaixo, alguns exemplos de tarefas que você não pode executar.

* Você não recebem privilégios de administrador de domínio ou administrador corporativo para o domínio gerenciado hello.
* Você não pode estender o esquema de saudação do domínio gerenciado hello.
* Você não pode se conectar toodomain controladores Olá gerenciado usando a área de trabalho remota.
* Não é possível adicionar controladores de domínio toohello domínio gerenciado.

## <a name="task-1---provision-a-domain-joined-windows-server-virtual-machine-tooremotely-administer-hello-managed-domain"></a>Tarefa 1: provisionar uma tooremotely de máquina virtual do Windows Server domínio administrar o domínio gerenciado Olá
Domínios gerenciados de serviços de domínio do AD do Azure podem ser gerenciados usando ferramentas familiares de administrativo do Active Directory como Olá Active Directory Administrative ADAC (centro) ou o PowerShell do AD. Administradores de inquilinos não possuem controladores de toodomain tooconnect privilégios Olá de domínio gerenciados por meio da área de trabalho remota. Portanto, membros de saudação do grupo 'Administradores de controlador de domínio do AAD' pode administrar remotamente usando as ferramentas administrativas do AD em um computador cliente/servidor do Windows que é o domínio gerenciado toohello unidas de domínios gerenciados. Ferramentas administrativas do AD podem ser instaladas como parte do recurso opcional do hello ferramentas de administração de servidor remoto (RSAT) em computadores cliente e servidor Windows ingressados no domínio toohello gerenciado.

Olá primeira etapa é tooset uma máquina virtual do Windows Server domínio Unido toohello gerenciado. Para obter instruções, consulte o artigo toohello intitulado [ingressar em um domínio gerenciado do serviços de domínio do AD do Azure no Windows Server máquina virtual tooan](active-directory-ds-admin-guide-join-windows-vm.md).

### <a name="remotely-administer-hello-managed-domain-from-a-client-computer-for-example-windows-10"></a>Administrar remotamente o domínio gerenciado Olá em um computador cliente (por exemplo, o Windows 10)
instruções Olá deste artigo usam uma saudação de tooadminister de máquina virtual do Windows Server AAD DS gerenciadas de domínio. No entanto, também é possível toouse um toodo de máquina virtual do Windows (por exemplo, o Windows 10) do cliente assim.

Você pode [instalar ferramentas de administração de servidor remoto (RSAT)](http://social.technet.microsoft.com/wiki/contents/articles/2202.remote-server-administration-tools-rsat-for-windows-client-and-windows-server-dsforum2wiki.aspx) em uma máquina virtual do Windows cliente seguindo as instruções de saudação em TechNet.

## <a name="task-2---install-active-directory-administration-tools-on-hello-virtual-machine"></a>Tarefa 2: ferramentas de administração do Active Directory de instalação na máquina virtual de saudação
Execute Olá ferramentas de administração do Active Directory de saudação de tooinstall etapas a seguir na máquina de virtual Olá ingressado no domínio. Consulte o Technet para obter mais [informações sobre como instalar e usar as Ferramentas de Administração de Servidor Remoto](https://technet.microsoft.com/library/hh831501.aspx).

1. Navegue muito**máquinas virtuais** nó Olá portal clássico do Azure. Selecione a máquina virtual de saudação criada na tarefa 1 e clique em **conectar** na barra de comandos de saudação na parte inferior da saudação da janela de saudação.

    ![Conecte-se a máquina virtual de tooWindows](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. portal clássico Olá solicita tooopen ou salvar um arquivo com uma extensão '. rdp', que é usado tooconnect toohello VM. Clique em arquivo de saudação tooopen quando o download for concluído.
3. No prompt de logon Olá, use credenciais de saudação de um usuário que pertence a toohello do grupo 'Administradores de controlador de domínio do AAD'. Por exemplo, usamos 'bob@domainservicespreview.onmicrosoft.com' em nosso caso.
4. Na tela de início do hello, abra **Gerenciador do servidor**. Clique em **adicionar funções e recursos** no painel central de saudação da janela do Gerenciador do servidor de saudação.

    ![Iniciar o Gerenciador do Servidor na máquina virtual](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager.png)
5. Em Olá **antes de começar** página de saudação **assistente Adicionar funções e recursos**, clique em **próximo**.

    ![Página Antes de Começar](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-begin.png)
6. Em Olá **tipo de instalação** , deixe Olá **instalação baseada em função ou recurso** opção marcada e clique em **próximo**.

    ![Página Tipo de Instalação](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-type.png)
7. Em Olá **seleção de servidor** página, selecione a máquina virtual atual de saudação do pool do servidor de saudação e clique em **próximo**.

    ![Página Seleção de Servidor](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-server.png)
8. Em Olá **funções de servidor** , clique em **próximo**. Podemos ignorar esta página como podemos não estiver instalando funções no servidor de saudação.
9. Em Olá **recursos** , clique em Olá tooexpand **ferramentas de administração de servidor remoto** nó e, em seguida, clique em Olá tooexpand **ferramentas de administração de função** nó. Selecione **AD DS e AD LDS** recurso na lista de saudação das ferramentas de administração de função.

    ![Página Recursos](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-ad-tools.png)
10. Em Olá **confirmação** , clique em **instalar** de recursos na máquina virtual de saudação do tooinstall Olá AD e ferramentas do AD LDS. Quando a instalação do recurso for concluída com êxito, clique em **fechar** tooexit Olá **adicionar funções e recursos** assistente.

    ![Página de confirmação](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-confirmation.png)

## <a name="task-3---connect-tooand-explore-hello-managed-domain"></a>Tarefa 3 - conectar tooand explorar domínio gerenciado Olá
Agora que ferramentas administrativas Olá AD estão instaladas em Olá ingressado no domínio máquina virtual, podemos usar essas ferramentas tooexplore e administrar o domínio gerenciado hello.

> [!NOTE]
> Você precisa toobe membro Olá ' AAD DC' do grupo de administradores, Olá tooadminister gerenciados domínio.
>
>

1. Na tela de início de saudação, clique em **ferramentas administrativas**. Você deve ver as ferramentas administrativas do AD de saudação instaladas na máquina virtual de saudação.

    ![Ferramentas Administrativas instaladas no servidor](./media/active-directory-domain-services-admin-guide/install-rsat-admin-tools-installed.png)
2. Clique em **Centro Administrativo do Active Directory**.

    ![Centro Administrativo do Active Directory](./media/active-directory-domain-services-admin-guide/adac-overview.png)
3. domínio de saudação tooexplore, clique em nome de domínio de saudação no painel esquerdo da saudação (por exemplo, ' contoso100.com'). Observe os dois contêineres chamados 'Computadores do AADDC' e 'Usuários do AADDC', respectivamente.

    ![ADAC - exibir domínio](./media/active-directory-domain-services-admin-guide/adac-domain-view.png)
4. Clique em contêiner Olá chamado **AADDC usuários** toosee todos os usuários e grupos que pertencem a toohello gerenciados domínio. Você deve ver as contas de usuário e grupos do seu locatário do Azure AD exibidas neste contêiner. Observe neste exemplo, uma conta de usuário para usuário Olá chamado 'bob' e um grupo chamado 'Administradores de controlador de domínio do AAD' estão disponíveis neste contêiner.

    ![ADAC - usuários de domínio](./media/active-directory-domain-services-admin-guide/adac-aaddc-users.png)
5. Clique em contêiner Olá chamado **AADDC computadores** computadores de saudação toosee ingressados no domínio gerenciado toothis. Você deve ver uma entrada para a máquina virtual atual Olá que é toohello ingressado no domínio. Contas de computador para todos os computadores que estão unidas toohello domínio gerenciado são armazenadas neste contêiner 'AADDC computadores' de serviços de domínio do AD do Azure.

    ![ADAC - computadores ingressados no domínio](./media/active-directory-domain-services-admin-guide/adac-aaddc-computers.png)

<br>

## <a name="related-content"></a>Conteúdo relacionado
* [Serviços de Domínio do Azure AD - guia de Introdução](active-directory-ds-getting-started.md)
* [Ingressar em um domínio gerenciado do Windows Server máquina virtual tooan serviços de domínio do AD do Azure](active-directory-ds-admin-guide-join-windows-vm.md)
* [Implantar as Ferramentas de Administração de Servidor Remoto](https://technet.microsoft.com/library/hh831501.aspx)
