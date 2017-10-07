---
title: "Azure Active Directory Domain Services: Administrar o DNS em domínios gerenciados | Microsoft Docs"
description: "Administrar o DNS nos domínios gerenciados do Azure Active Directory Domain Services"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: f2085283649eadd3c9e89f708b0eecf10b2d7d70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="administer-dns-on-an-azure-ad-domain-services-managed-domain"></a>Administrar o DNS em um domínio gerenciado dos Serviços de Domínio do Azure AD
Azure Active Directory Domain Services inclui um servidor DNS (resolução de nome de domínio) que fornece a resolução DNS para o domínio gerenciado hello. Ocasionalmente, talvez seja necessário tooconfigure DNS no domínio Olá gerenciado. Talvez seja necessário toocreate registros DNS para configurar endereços IP virtuais para balanceadores de carga de máquinas que não são toohello ingressado no domínio, ou configurar encaminhadores DNS externos. Por esse motivo, os usuários que pertencem a do grupo 'Administradores de controlador de domínio do AAD' toohello recebem privilégios de administração de DNS no domínio gerenciado hello.

## <a name="before-you-begin"></a>Antes de começar
tarefas de saudação tooperform listadas neste artigo, você precisa:

1. Uma **assinatura do Azure**válida.
2. Um **diretório do AD do Azure** - seja sincronizado com um diretório local ou com um diretório somente na nuvem.
3. **Serviços de domínio do AD do Azure** devem estar habilitados para diretório de saudação do AD do Azure. Se você ainda não tiver feito isso, siga todas as tarefas de saudação descritas Olá [guia de Introdução](active-directory-ds-getting-started.md).
4. Um **domínio máquina de virtual** do qual você administrar Olá domínio gerenciado por serviços de domínio do AD do Azure. Se você não tiver tal uma máquina virtual, execute todas as tarefas de saudação descritas no artigo Olá intitulado [ingressar em um domínio gerenciado do Windows máquina virtual tooa](active-directory-ds-admin-guide-join-windows-vm.md).
5. Você precisa ter credenciais de saudação de um **usuário conta pertencentes toohello ' AAD controlador de domínio do grupo 'Administradores** em seu diretório, tooadminister DNS para seu domínio gerenciado.

<br>

## <a name="task-1---provision-a-domain-joined-virtual-machine-tooremotely-administer-dns-for-hello-managed-domain"></a>Tarefa 1: provisionar uma tooremotely de domínio virtual machine administrar DNS do domínio gerenciado Olá
Domínios gerenciados de serviços de domínio do AD do Azure podem ser gerenciados remotamente usando ferramentas familiares de administrativo do Active Directory como Olá Active Directory Administrative ADAC (centro) ou o PowerShell do AD. Da mesma forma, o DNS do domínio gerenciado Olá podem ser administrado remotamente usando as ferramentas de administração de servidor DNS hello.

Os administradores em seu diretório do AD do Azure não têm controladores de toodomain tooconnect privilégios em Olá de domínio gerenciados por meio da área de trabalho remota. Membros Olá ' AAD DC' do grupo de administradores podem administrar o DNS para domínios gerenciados remotamente usando as ferramentas de servidor DNS de um computador de servidor/cliente do Windows que é o domínio gerenciado toohello unidas. Ferramentas do servidor DNS podem ser instaladas como parte do recurso opcional do hello ferramentas de administração de servidor remoto (RSAT) no Windows Server e computadores cliente ingressados no domínio toohello gerenciado.

Olá primeira tarefa é tooprovision uma máquina virtual do Windows Server que é o domínio gerenciado toohello unidas. Para obter instruções, consulte o artigo toohello intitulado [ingressar em um domínio gerenciado do serviços de domínio do AD do Azure no Windows Server máquina virtual tooan](active-directory-ds-admin-guide-join-windows-vm.md).

## <a name="task-2---install-dns-server-tools-on-hello-virtual-machine"></a>Tarefa 2: ferramentas de instalar o servidor DNS na máquina virtual de saudação
Execute Olá ferramentas de administração do DNS de saudação de tooinstall etapas a seguir na máquina de virtual Olá ingressado no domínio. Para obter mais informações sobre como [instalar e usar Ferramentas de Administração de Servidor Remoto](https://technet.microsoft.com/library/hh831501.aspx), consulte o Technet.

1. Navegue muito**máquinas virtuais** nó Olá portal clássico do Azure. Selecione a máquina virtual de saudação criada na tarefa 1 e clique em **conectar** na barra de comandos de saudação na parte inferior da saudação da janela de saudação.

    ![Conecte-se a máquina virtual de tooWindows](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. portal clássico Olá solicita tooopen ou salvar um arquivo com uma extensão '. rdp', que é usado tooconnect toohello VM. Quando o download for concluído, clique em arquivo hello.
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
9. Em Olá **recursos** , clique em Olá tooexpand **ferramentas de administração de servidor remoto** nó e, em seguida, clique em Olá tooexpand **ferramentas de administração de função** nó. Selecione **ferramentas do servidor DNS** recurso na lista de saudação das ferramentas de administração de função.

    ![Página Recursos](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-dns-tools.png)
10. Em Olá **confirmação** , clique em **instalar** em recursos das ferramentas de servidor DNS de saudação tooinstall na máquina virtual de saudação. Quando a instalação do recurso for concluída com êxito, clique em **fechar** tooexit Olá **adicionar funções e recursos** assistente.

    ![Página de confirmação](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-dns-confirmation.png)

## <a name="task-3---launch-hello-dns-management-console-tooadminister-dns"></a>Tarefa 3 - tooadminister lançamento Olá DNS management console DNS
Agora que as ferramentas do servidor DNS Olá recurso é instalado em hello ingressado no domínio virtual machine, podemos usar Olá DNS ferramentas tooadminister DNS no domínio Olá gerenciado.

> [!NOTE]
> Você precisa de um membro do grupo de saudação 'Administradores do controlador de domínio do AAD', tooadminister DNS no domínio gerenciado Olá toobe.
>
>

1. Na tela de início de saudação, clique em **ferramentas administrativas**. Você deve ver Olá **DNS** instalado na máquina virtual de saudação do console.

    ![Ferramentas administrativas - Console DNS](./media/active-directory-domain-services-admin-guide/install-rsat-dns-tools-installed.png)
2. Clique em **DNS** toolaunch Olá DNS Management console.
3. Em Olá **conectar tooDNS servidor** caixa de diálogo, clique opção Olá intitulada **Olá seguinte computador**e digite o nome de domínio DNS Olá Olá gerenciado domínio (por exemplo, ' contoso100.com').

    ![O Console DNS - conectar toodomain](./media/active-directory-domain-services-admin-guide/dns-console-connect-to-domain.png)
4. Olá Console DNS conecta-se o domínio gerenciado toohello.

    ![Console DNS - administrar domínio](./media/active-directory-domain-services-admin-guide/dns-console-managed-domain.png)
5. Agora você pode usar as entradas DNS tooadd de console DNS Olá para computadores na rede virtual hello, no qual você habilitou os serviços de domínio do AAD.

> [!WARNING]
> Tenha cuidado ao administrar o DNS para Olá gerenciados usando as ferramentas de administração do DNS do domínio. Certifique-se de que você **não excluir ou modificar registros DNS internos Olá que são usados pelos serviços de domínio no domínio Olá**. Os registros DNS internos incluem registros DNS do domínio, registros de servidor de nome e outros registros usados para a localização do controlador de domínio. Se você modificar esses registros, serviços de domínio sejam interrompidos na rede virtual hello.
>
>

Consulte Olá [as ferramentas do DNS do artigo no Technet](https://technet.microsoft.com/library/cc753579.aspx) para obter mais informações sobre o gerenciamento de DNS.

## <a name="related-content"></a>Conteúdo relacionado
* [Serviços de Domínio do Azure AD - guia de Introdução](active-directory-ds-getting-started.md)
* [Ingressar em um domínio gerenciado do Windows Server máquina virtual tooan serviços de domínio do AD do Azure](active-directory-ds-admin-guide-join-windows-vm.md)
* [Administrar um domínio gerenciado dos Serviços de Domínio do Azure AD](active-directory-ds-admin-guide-administer-domain.md)
* [Ferramentas de administração do DNS](https://technet.microsoft.com/library/cc753579.aspx)
