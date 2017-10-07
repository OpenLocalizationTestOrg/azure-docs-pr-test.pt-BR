---
title: "Serviços do Azure Active Directory domínio: Ingressar em um domínio gerenciado do RHEL VM tooa | Microsoft Docs"
description: "Adicione uma máquina virtual de Red Hat Enterprise Linux tooAzure AD os serviços de domínio"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 87291c47-1280-43f8-8fb2-da1bd61a4942
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 41ca2aaf2eefbf9c403d2b834d61a1aa0943d950
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-red-hat-enterprise-linux-7-virtual-machine-tooa-managed-domain"></a>Ingressar em um domínio gerenciado do Red Hat Enterprise Linux 7 máquina virtual tooa
Este artigo mostra como toojoin uma tooan de máquina virtual do Red Hat Enterprise Linux (RHEL) 7 serviços de domínio do AD do Azure gerenciados domínio.

## <a name="provision-a-red-hat-enterprise-linux-virtual-machine"></a>Provisionar uma máquina virtual do Red Hat Enterprise Linux
Execute Olá seguindo as etapas tooprovision RHEL 7 VM usando Olá portal do Azure.

1. Entrar toohello [portal do Azure](https://portal.azure.com).

    ![Painel do portal do Azure](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-dashboard.png)
2. Clique em **novo** em Olá esquerda painel e digite **Red Hat** na barra de pesquisa Olá conforme Olá captura de tela a seguir. Entradas para Red Hat Enterprise Linux são exibidas nos resultados da pesquisa hello. Clique em **Red Hat Enterprise Linux 7.2**.

    ![Selecione RHEL nos resultados](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-find-rhel-image.png)
3. resultados da pesquisa de saudação em Olá **tudo** painel deve listar imagem Olá Red Hat Enterprise Linux 7.2. Clique em **Red Hat Enterprise Linux 7.2** tooview obter mais informações sobre a imagem de máquina virtual de saudação.

    ![Selecione RHEL nos resultados](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-rhel-image.png)
4. Em Olá **Red Hat Enterprise Linux 7.2** painel, você deve ver mais informações sobre a imagem de máquina virtual de saudação. Em Olá **selecionar um modelo de implantação** lista suspensa, selecione **clássico**. Em seguida, clique em Olá **criar** botão.

    ![Exibir detalhes da imagem](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-clicked.png)
5. Em hello **Noções básicas de** página de saudação **criar máquina virtual** assistente, digite Olá **nome de Host** para a máquina virtual da nova hello. Também especifique um nome de usuário de administrador local no hello **nome de usuário** campo e um **senha**. Você também pode escolher toouse um usuário de administrador local do SSH tooauthenticate chave hello. Selecione também um **preço** para a máquina virtual de saudação.

    ![Criar VM — página de noções básicas](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-basic-details.png)
6. Em Olá **tamanho** página de saudação **criar a máquina virtual** tamanho de saudação do assistente, selecione para a máquina virtual de saudação.

    ![Criar VM — selecionar tamanho](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-vm-size.png)

7. Em Olá **configurações** página de saudação **criar a máquina virtual** conta de armazenamento de saudação do assistente, selecione para a máquina virtual de saudação. Clique em **rede Virtual** tooselect Olá rede virtual toowhich Olá VM do Linux deve ser implantado. Em Olá **rede Virtual** folha, a rede virtual Olá selecione, no qual os serviços de domínio do AD do Azure está disponível. Neste exemplo, podemos escolher rede virtual do 'MyPreviewVNet' hello.

    ![Criar VM - selecionar rede virtual](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-select-vnet.png)
8. Em Olá **resumo** página de saudação **criar a máquina virtual** saudação do assistente, examine e clique em **Okey** botão.

    ![Criar VM - rede virtual selecionada](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-vnet-selected.png)
9. Implantação de máquina virtual nova Olá baseada em imagem Olá RHEL 7.2 deve começar.

    ![Criar VM - implantação iniciada](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployment-started.png)
10. Após alguns minutos, a máquina virtual de saudação deve ser implantado com êxito e está pronto para uso.

    ![Criar VM - implantada](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployed.png)

## <a name="connect-remotely-toohello-newly-provisioned-linux-virtual-machine"></a>Conectar-se remotamente toohello recentemente provisionado máquina de virtual do Linux
máquina virtual de saudação RHEL 7.2 tiver sido configurada no Azure. Olá próxima tarefa é tooconnect remotamente toohello VM.

**Conecte-se a máquina virtual de toohello RHEL 7.2** siga as instruções de saudação artigo Olá [como toolog na máquina virtual de tooa executando o Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

rest Olá das etapas de saudação suponha usar Olá PuTTY SSH cliente tooconnect toohello RHEL máquina virtual. Para obter mais informações, consulte Olá [página de Download do PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).

1. Olá abra PuTTY programa.
2. Digite hello **nome de Host** para Olá recém-criado RHEL VM. Neste exemplo, a nossa máquina virtual tem o nome de host de saudação 'contoso-rhel.cloudapp .net'. Se você não tiver certeza do nome de host de saudação da VM, consulte toohello painel da máquina virtual em Olá portal do Azure.

    ![Conectar no PuTTY](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-connect.png)
3. Faça logon na máquina virtual de toohello usando credenciais de administrador local Olá especificado quando a máquina virtual de saudação foi criada. Neste exemplo, usamos a conta de administrador local hello "mahesh".

    ![Logon no PuTTY](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-login.png)

## <a name="install-required-packages-on-hello-linux-virtual-machine"></a>Instalar pacotes necessários na máquina de virtual do Linux Olá
Depois de conectar máquina de virtual toohello, Olá próxima tarefa é tooinstall pacotes necessários para o ingresso no domínio na máquina virtual de saudação. Execute Olá etapas a seguir:

1. **Instalar realmd:** pacote de realmd Olá é usado para o ingresso no domínio. Em seu terminal PuTTY, digite Olá comando a seguir:

    sudo yum install realmd

    ![Instalar o realmd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-realmd.png)

    Depois de alguns minutos, o pacote de realmd de saudação deve obter instalado na máquina virtual de saudação.

    ![realmd instalado](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-installed.png)
2. **Instalar sssd:** pacote de realmd Olá depende de operações de junção de domínio sssd tooperform. Em seu terminal PuTTY, digite Olá comando a seguir:

    sudo yum install sssd

    ![Instalar o sssd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-sssd.png)

    Depois de alguns minutos, o pacote de sssd de saudação deve obter instalado na máquina virtual de saudação.

    ![realmd instalado](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-sssd-installed.png)
3. **Instalar o kerberos:** em seu terminal PuTTY, digite hello comando a seguir:

    sudo yum install krb5-workstation krb5-libs

    ![Instalar o kerberos](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-kerberos.png)

    Depois de alguns minutos, o pacote de realmd de saudação deve obter instalado na máquina virtual de saudação.

    ![Kerberos instalado](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kerberos-installed.png)

## <a name="join-hello-linux-virtual-machine-toohello-managed-domain"></a>Ingressar em domínio gerenciado de toohello Olá de máquina virtual Linux
Agora que pacotes Olá necessários estão instalados na máquina de virtual do Linux hello, Olá próxima tarefa é domínio gerenciado do toohello toojoin Olá máquina virtual.

1. Descobrir o domínio gerenciado do hello dos serviços de domínio do AAD. Em seu terminal PuTTY, digite Olá comando a seguir:

    sudo realm discover CONTOSO100.COM

    ![realm discover](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-discover.png)

    Se **realm descobrir** é toofind não é possível o domínio gerenciado, certifique-se de que esse domínio hello está acessível na máquina virtual de saudação (tente ping). Também, certifique-se de que a máquina virtual Olá foi realmente implantado toohello mesma rede virtual no qual Olá domínio gerenciado está disponível.
2. Inicialize o kerberos. Em seu terminal PuTTY, digite Olá comando a seguir. Certifique-se de que você especifique um usuário que pertence a toohello ' AAD controlador de domínio do grupo 'Administradores. Apenas esses usuários podem ingressar em domínio gerenciado toohello dos computadores.

    kinit bob@CONTOSO100.COM

    ![kinit ](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kinit.png)

    Certifique-se de que você especificar o nome de domínio de saudação em letras maiusculas, kinit else falha.
3. Ingresse Olá máquina toohello domínio. Em seu terminal PuTTY, digite Olá comando a seguir. Especifique a saudação mesmo usuário que você especificou na saudação anterior etapa ('kinit').

    sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM'

    ![Ingresso no realm](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-join.png)

Você deve receber uma mensagem ("registrado com êxito máquina no realm") quando a máquina de saudação é domínio gerenciado toohello unida com êxito.

## <a name="verify-domain-join"></a>Verificar o ingresso no domínio
Rapidamente, você pode verificar se a máquina de saudação foi domínio gerenciado toohello unida com êxito. Conecte-se toohello domínio recém-associados RHEL VM usando o SSH e uma conta de usuário de domínio e, em seguida, toosee de seleção se a conta de usuário Olá seja resolvida corretamente.

1. Em seu PuTTY terminal, Olá tipo após o comando tooconnect toohello recentemente ingressado no domínio RHEL virtual máquina usando o SSH. Usar uma conta de domínio que pertence o domínio gerenciado toohello (por exemplo, 'bob@CONTOSO100.COM' nesse caso.)

    ssh -l bob@CONTOSO100.COM contoso-rhel.cloudapp.net
2. Em seu terminal PuTTY, digite Olá após o comando toosee se o diretório base Olá foi inicializado corretamente.

    pwd
3. Em seu terminal PuTTY, digite Olá toosee de comando a seguir se membros do grupo Olá estão sendo resolvidos corretamente.

    ID

Abaixo temos uma saída de exemplo desses comandos:

![Verificar o ingresso no domínio](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-verify-domain-join.png)

## <a name="troubleshooting-domain-join"></a>Solucionando problemas de ingresso no domínio
Consulte toohello [junção de domínio de solução de problemas](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) artigo.

## <a name="related-content"></a>Conteúdo relacionado
* [Serviços de Domínio do Azure AD - guia de Introdução](active-directory-ds-getting-started.md)
* [Ingressar em um domínio gerenciado do Windows Server máquina virtual tooan serviços de domínio do AD do Azure](active-directory-ds-admin-guide-join-windows-vm.md)
* [Como toolog na máquina virtual de tooa executando o Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* [Installing Kerberos (Instalando o Kerberos)](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Smart_Cards/installing-kerberos.html)
* [Red Hat Enterprise Linux 7 - Windows Integration Guide (Red Hat Enterprise Linux 7: Guia de integração do Windows)](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/index.html)
