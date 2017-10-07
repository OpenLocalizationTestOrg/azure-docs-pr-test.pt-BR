---
title: "Azure Active Directory Domain Services: Administrar a política de grupo em domínios gerenciados | Microsoft Docs"
description: "Administrar a política de grupo nos domínios gerenciados do Azure Active Directory Domain Services"
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
ms.openlocfilehash: d56ebf27e3015a7f3385ac5a4ddd77ea2c88387f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="administer-group-policy-on-an-azure-ad-domain-services-managed-domain"></a>Administrar a política de grupo em um domínio gerenciado do Azure AD Domain Services
Azure Active Directory Domain Services inclui objetos de política de grupo (GPOs) interno para contêineres de 'usuários AADDC' e 'AADDC computadores' hello. Você pode personalizar esses internos tooconfigure de GPOs de política de grupo no domínio gerenciado hello. Além disso, os membros Olá ' AAD DC' do grupo de administradores podem criar suas próprias UOs personalizados no domínio gerenciado hello. Pode também criar GPOs personalizadas e vinculá-los toothese personalizado UOs. Os usuários que pertencem a do grupo 'Administradores de controlador de domínio do AAD' toohello recebem os privilégios de administração de política de grupo no domínio gerenciado hello.

## <a name="before-you-begin"></a>Antes de começar
tarefas de saudação tooperform listadas neste artigo, você precisa:

1. Uma **assinatura do Azure**válida.
2. Um **diretório do AD do Azure** - seja sincronizado com um diretório local ou com um diretório somente na nuvem.
3. **Serviços de domínio do AD do Azure** devem estar habilitados para diretório de saudação do AD do Azure. Se você ainda não tiver feito isso, siga todas as tarefas de saudação descritas Olá [guia de Introdução](active-directory-ds-getting-started.md).
4. Um **domínio máquina de virtual** do qual você administrar Olá domínio gerenciado por serviços de domínio do AD do Azure. Se você não tiver tal uma máquina virtual, execute todas as tarefas de saudação descritas no artigo Olá intitulado [ingressar em um domínio gerenciado do Windows máquina virtual tooa](active-directory-ds-admin-guide-join-windows-vm.md).
5. Você precisa ter credenciais de saudação de um **usuário conta pertencentes toohello ' AAD controlador de domínio do grupo 'Administradores** em seu diretório, tooadminister política de grupo para o domínio gerenciado.

<br>

## <a name="task-1---provision-a-domain-joined-virtual-machine-tooremotely-administer-group-policy-for-hello-managed-domain"></a>Tarefa 1: provisionar uma tooremotely de domínio virtual machine administrar a política de grupo para o domínio gerenciado Olá
Domínios gerenciados de serviços de domínio do AD do Azure podem ser gerenciados remotamente usando ferramentas familiares de administrativo do Active Directory como Olá Active Directory Administrative ADAC (centro) ou o PowerShell do AD. Da mesma forma, a política de grupo do domínio gerenciado Olá podem ser administrada remotamente usando as ferramentas de administração de política de grupo Olá.

Os administradores em seu diretório do AD do Azure não têm controladores de toodomain tooconnect privilégios em Olá de domínio gerenciados por meio da área de trabalho remota. Membros Olá ' AAD DC' do grupo de administradores podem administrar a política de grupo para domínios gerenciados remotamente. Eles podem usar as ferramentas de diretiva de grupo em um domínio do Windows Server/cliente computador toohello unidas gerenciado. Ferramentas de diretiva de grupo podem ser instaladas como parte do recurso opcional do hello gerenciamento de política de grupo em computadores cliente e servidor Windows ingressados no domínio gerenciado toohello.

Olá primeira tarefa é tooprovision uma máquina virtual do Windows Server que é o domínio gerenciado toohello unidas. Para obter instruções, consulte o artigo toohello intitulado [ingressar em um domínio gerenciado do serviços de domínio do AD do Azure no Windows Server máquina virtual tooan](active-directory-ds-admin-guide-join-windows-vm.md).

## <a name="task-2---install-group-policy-tools-on-hello-virtual-machine"></a>Tarefa 2: ferramentas de diretiva de grupo de instalação na máquina virtual de saudação
Execute Olá ferramentas de administração de política de grupo etapas tooinstall Olá a seguir na máquina de virtual Olá ingressado no domínio.

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
9. Em Olá **recursos** página, selecione Olá **Group Policy Management** recurso.

    ![Página Recursos](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-gp-management.png)
10. Em Olá **confirmação** , clique em **instalar** recurso de gerenciamento de política de grupo de saudação tooinstall na máquina virtual de saudação. Quando a instalação do recurso for concluída com êxito, clique em **fechar** tooexit Olá **adicionar funções e recursos** assistente.

    ![Página de confirmação](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-gp-management-confirmation.png)

## <a name="task-3---launch-hello-group-policy-management-console-tooadminister-group-policy"></a>Tarefa 3 - lançamento Olá política de grupo management console tooadminister política de grupo
Você pode usar o console de gerenciamento de diretiva de grupo de saudação em tooadminister de domínio virtual machine Olá política de grupo no domínio gerenciado hello.

> [!NOTE]
> É necessário toobe um membro do grupo de saudação 'Administradores do controlador de domínio do AAD', tooadminister política de grupo no domínio gerenciado hello.
>
>

1. Na tela de início de saudação, clique em **ferramentas administrativas**. Você deve ver Olá **Group Policy Management** instalado na máquina virtual de saudação do console.

    ![Iniciar o Gerenciamento de Política de Grupo](./media/active-directory-domain-services-admin-guide/gp-management-installed.png)
2. Clique em **Group Policy Management** toolaunch Olá GPMC.

    ![Console de Política de Grupo](./media/active-directory-domain-services-admin-guide/gp-management-console.png)

## <a name="task-4---customize-built-in-group-policy-objects"></a>Tarefa 4 - Personalizar objetos de política de grupo internos
Há dois internos objetos políticas de grupo (GPOs) - um para os contêineres de saudação 'AADDC computadores' e 'AADDC usuários' em seu domínio gerenciado. Você pode personalizar a política de grupo de tooconfigure esses GPOs no domínio gerenciado hello.

1. Em Olá **Group Policy Management** console, clique em Olá tooexpand **floresta: contoso100.com** e **domínios** nós toosee Olá as diretivas de grupo para o domínio gerenciado.

    ![GPOs internos](./media/active-directory-domain-services-admin-guide/builtin-gpos.png)
2. Você pode personalizar essas políticas de grupo internas GPOs tooconfigure no seu domínio gerenciado. Clique com botão direito Olá GPO e clique em **editar...**  toocustomize Olá internos GPO. ferramenta do Editor de configuração de política de grupo Olá permite que o GPO Olá toocustomize.

    ![Editar GPO interno](./media/active-directory-domain-services-admin-guide/edit-builtin-gpo.png)
3. Agora você pode usar o hello **Editor de gerenciamento de política de grupo** console tooedit Olá internos GPO. Por exemplo, Olá captura de tela a seguir mostra como toocustomize Olá GPO interna de 'AADDC computadores'.

    ![Personalizar GPO](./media/active-directory-domain-services-admin-guide/gp-editor.png)

## <a name="task-5---create-a-custom-group-policy-object-gpo"></a>Tarefa 5 – Criar um objeto de política de grupo (GPO) personalizado
Você pode criar ou importar seus próprios objetos de política de grupo personalizados. Também é possível vincular personalizada personalizada de tooa GPOs UO que você criou no seu domínio gerenciado. Para saber mais sobre como criar unidades organizacionais personalizadas, confira [Criar uma UO personalizada em um domínio gerenciado](active-directory-ds-admin-guide-create-ou.md).

> [!NOTE]
> É necessário toobe um membro do grupo de saudação 'Administradores do controlador de domínio do AAD', tooadminister política de grupo no domínio gerenciado hello.
>
>

1. Em Olá **Group Policy Management** console, clique em tooselect personalizada unidade organizacional (UO). Mouse Olá UO e clique em **criar um GPO neste domínio e vinculá-lo aqui...** .

    ![Criar um GPO personalizado](./media/active-directory-domain-services-admin-guide/gp-create-gpo.png)
2. Especifique um nome para Olá novo GPO e clique em **Okey**.

    ![Especifique um nome para o GPO](./media/active-directory-domain-services-admin-guide/gp-specify-gpo-name.png)
3. Um novo GPO é criado e vinculado tooyour personalizado UO. Clique com botão direito Olá GPO e clique em **editar...**  menu hello.

    ![GPO recém-criado](./media/active-directory-domain-services-admin-guide/gp-gpo-created.png)
4. Você pode personalizar o GPO Olá recém-criado usando Olá **Editor de gerenciamento de política de grupo**.

    ![Personalizar o novo GPO](./media/active-directory-domain-services-admin-guide/gp-customize-gpo.png)


Mais informações sobre como usar o [Console de Gerenciamento de Política de Grupo](https://technet.microsoft.com/library/cc753298.aspx) estão disponíveis no Technet.

## <a name="related-content"></a>Conteúdo relacionado
* [Serviços de Domínio do Azure AD - guia de Introdução](active-directory-ds-getting-started.md)
* [Ingressar em um domínio gerenciado do Windows Server máquina virtual tooan serviços de domínio do AD do Azure](active-directory-ds-admin-guide-join-windows-vm.md)
* [Administrar um domínio gerenciado dos Serviços de Domínio do Azure AD](active-directory-ds-admin-guide-administer-domain.md)
* [Console de Gerenciamento de Política de Grupo](https://technet.microsoft.com/library/cc753298.aspx)
