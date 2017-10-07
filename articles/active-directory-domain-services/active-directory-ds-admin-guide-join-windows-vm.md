---
title: "Serviços do Azure Active Directory domínio: Ingressar em um domínio gerenciado de tooa de VM do Windows Server | Microsoft Docs"
description: "Ingressar em uma máquina virtual Windows Server tooAzure AD os serviços de domínio"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 74dbdb33-05db-4d47-badc-0d7bb6d0c8cb
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 1e85833b42bd51f3b3df067d6c5b69253459bec5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-windows-server-virtual-machine-tooa-managed-domain"></a>Ingressar em um domínio gerenciado de tooa de máquina virtual do Windows Server
> [!div class="op_single_selector"]
> * [Portal clássico do Azure - Windows](active-directory-ds-admin-guide-join-windows-vm.md)
> * [PowerShell - Windows](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

Este artigo mostra como toojoin uma máquina virtual em execução do Windows Server 2012 R2 tooan serviços de domínio do AD do Azure gerenciados domínio, usando Olá portal clássico do Azure.

## <a name="step-1-create-hello-windows-server-virtual-machine"></a>Etapa 1: Criar a máquina de virtual do Windows Server Olá
Siga as instruções de saudação em Olá [criar uma máquina virtual executando o Windows hello portal clássico do Azure](../virtual-machines/windows/classic/tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) tutorial. É importante tooensure essa máquina virtual recém-criado é Unido toohello mesma rede virtual no qual você habilitou os serviços de domínio do AD do Azure. Olá opção 'Criar rápida' não permite que você toojoin Olá tooa virtual rede de máquina virtual. Portanto, você precisa toouse Olá 'Da galeria' opção toocreate Olá VM.

Executar Olá toocreate as etapas a seguir em uma máquina virtual unida toohello rede virtual do Windows na qual você habilitou os serviços de domínio do AD do Azure.

1. No hello portal clássico do Azure, na barra de comandos de saudação na parte inferior da saudação da janela de saudação, clique em **novo**.
2. Em **Computação**, clique em **Máquina Virtua**l e em **Da Galeria**.
3. primeira tela de saudação permite **escolha uma imagem** para sua máquina virtual da lista de saudação de imagens disponíveis. Escolha a imagem apropriada hello.

    ![Selecionar a imagem](./media/active-directory-domain-services-admin-guide/create-windows-vm-select-image.png)
4. segunda tela do Hello permite escolher um nome de computador, o tamanho e o nome de usuário administrativo e a senha. Camada de saudação de uso e o tamanho necessário toorun seu aplicativo ou a carga de trabalho. nome de usuário Olá que você escolhe aqui é um usuário de administrador local no computador de saudação. Não digite as credenciais de uma conta usuário de domínio aqui.

    ![Configurar a máquina virtual](./media/active-directory-domain-services-admin-guide/create-windows-vm-config.png)
5. tela de terceiro Hello lhe permite configurar recursos de rede, armazenamento e disponibilidade. Certifique-se de selecionar Olá rede virtual no qual você habilitou os serviços de domínio do AD do Azure da saudação **afinidade região/grupo/Rede Virtual** lista suspensa. Especifique um **nome de DNS do serviço de nuvem** conforme apropriado para a máquina virtual de saudação.

    ![Selecionar a rede virtual para a máquina virtual](./media/active-directory-domain-services-admin-guide/create-windows-vm-select-vnet.png)

   > [!WARNING]
   > Certifique-se de que você ingressar Olá máquina virtual toohello mesma rede virtual no qual você habilitou os serviços de domínio do AD do Azure. Como resultado, máquina virtual de saudação pode 'consulte' domínio hello e executar tarefas como ingressar em domínio hello. Se você escolher máquina de virtual Olá toocreate em uma rede virtual diferente, se conecte a essa rede virtual de rede virtual toohello no qual você habilitou os serviços de domínio do AD do Azure.
   >
   >
6. tela quarta Hello permite instalar Olá agente de VM e configurar algumas extensões disponíveis hello.

    ![Concluído](./media/active-directory-domain-services-admin-guide/create-windows-vm-done.png)
7. Após a criação de máquina virtual de hello, portal clássico Olá lista Olá nova máquina virtual em Olá **máquinas virtuais** nó. Máquina virtual de saudação e o serviço de nuvem são iniciados automaticamente e seu status é listado como **executando**.

    ![A máquina virtual já está em funcionamento](./media/active-directory-domain-services-admin-guide/create-windows-vm-running.png)

## <a name="step-2-connect-toohello-windows-server-virtual-machine-using-hello-local-administrator-account"></a>Etapa 2: Conectar-se a máquina de virtual do Windows Server toohello usando a conta de administrador local Olá
Agora, nós nos conectamos a máquina virtual do Windows Server toohello recém-criado, toojoin-toohello domínio. Use credenciais de administrador local Olá que você especificou ao criar a máquina virtual de hello, tooconnect tooit.

Execute Olá etapas tooconnect toohello virtual máquina a seguir.

1. Navegue muito**máquinas virtuais** nó no portal clássico do hello. Selecione a máquina virtual de saudação criado na etapa 1 e clique em **conectar** na barra de comandos de saudação na parte inferior da saudação da janela de saudação.

    ![Conecte-se a máquina virtual de tooWindows](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. portal clássico Olá solicita tooopen ou salvar um arquivo com uma extensão '. rdp', que é usado tooconnect toohello VM. Clique em arquivo de saudação tooopen quando o download for concluído.
3. No prompt de logon hello, digite sua **credenciais de administrador local**, que você especificou ao criar a máquina virtual de saudação. Por exemplo, usamos 'localhost\mahesh' neste exemplo.

Neste ponto, você deve estar conectado toohello criado recentemente a máquina virtual do Windows usando credenciais de administrador locais. Olá próxima etapa é o domínio de toohello toojoin Olá máquina virtual.

## <a name="step-3-join-hello-windows-server-virtual-machine-toohello-aad-ds-managed-domain"></a>Etapa 3: Ingressar em domínio gerenciado de toohello AAD DS Olá de máquina virtual do Windows Server
Execute Olá seguindo as etapas toojoin Olá máquina virtual toohello AAD DS gerenciado domínio do Windows Server.

1. Conecte toohello do Windows Server, conforme mostrado na etapa 2. Na tela de início do hello, abra **Gerenciador do servidor**.
2. Clique em **servidor Local** no painel esquerdo de saudação da janela do Gerenciador do servidor de saudação.

    ![Iniciar o Gerenciador do Servidor na máquina virtual](./media/active-directory-domain-services-admin-guide/join-domain-server-manager.png)
3. Clique em **WORKGROUP** em Olá **propriedades** seção. Em Olá **propriedades do sistema** página de propriedades, clique em **alteração** toojoin domínio de saudação.

    ![Página Propriedades do Sistema](./media/active-directory-domain-services-admin-guide/join-domain-system-properties.png)
4. Especifique o nome de domínio de saudação do seu domínio gerenciado do serviços de domínio do AD do Azure no hello **domínio** caixa de texto e clique em **Okey**.

    ![Especifique a saudação toobe de domínio associado](./media/active-directory-domain-services-admin-guide/join-domain-system-properties-specify-domain.png)
5. Você é solicitada tooenter seu domínio de saudação toojoin credenciais. Certifique-se de que você **especificar credenciais de saudação para um toohello pertencentes de usuário administradores do controlador de domínio AAD** grupo. Somente os membros desse grupo têm privilégios toojoin máquinas toohello gerenciado domínio.

    ![Especificar credenciais para ingresso no domínio](./media/active-directory-domain-services-admin-guide/join-domain-system-properties-specify-credentials.png)
6. Você pode especificar as credenciais das Olá maneiras a seguir:

   * Formato UPN: especifique o sufixo UPN Olá Olá conta de usuário, conforme configurado no AD do Azure. Neste exemplo, o sufixo UPN de saudação do usuário Olá 'bob' é 'bob@domainservicespreview.onmicrosoft.com'.
   * Formato de SAMAccountName: você pode especificar o nome da conta de saudação em formato de SAMAccountName hello. Neste exemplo, o usuário Olá 'bob' precisaria tooenter 'CONTOSO100\bob'.

     > [!NOTE]
     > **Recomendamos o uso de credenciais de toospecify formato UPN hello.** Olá SAMAccountName pode ser gerada automaticamente se o prefixo UPN do usuário é muito longo (por exemplo, 'joereallylongnameuser'). Se vários usuários tiverem Olá mesmo prefixo UPN (por exemplo, ' bob') em seu locatário do AD do Azure, seu formato SAMAccountName pode ser gerado automaticamente pelo serviço de saudação. Nesses casos, formato UPN Olá pode ser usado com segurança toolog no domínio toohello.
     >
     >
7. Depois que o ingresso no domínio for bem-sucedida, você verá Olá a seguinte mensagem de boas-vindas toohello domínio. Reinicie máquina virtual Olá Olá toocomplete de operação de junção de domínio.

    ![Toohello bem-vindo ao domínio](./media/active-directory-domain-services-admin-guide/join-domain-done.png)

## <a name="troubleshooting-domain-join"></a>Solucionando problemas de ingresso no domínio
### <a name="connectivity-issues"></a>Problemas de conectividade
Se máquina virtual de saudação é domínio de saudação toofind não é possível, consulte toohello etapas de solução de problemas a seguir:

* Certifique-se de que a máquina virtual Olá é conectado toohello mesma rede virtual que você tiver habilitado o serviços de domínio em. Caso contrário, Olá virtual machine tooconnect não é possível toohello domínio e, portanto, não é possível toojoin domínio de saudação.
* Se Olá VM é a rede virtual do tooanother conectado, certifique-se de que essa rede virtual está conectada toohello rede virtual no qual você habilitou os serviços de domínio.
* Tente o domínio, Olá tooping usando o nome de domínio de saudação do domínio gerenciado da saudação (por exemplo, ' ping contoso100.com'). Se você estiver toodo não é possível, então, tente tooping Olá endereços IP domínio Olá exibido na página de saudação onde você habilitou os serviços de domínio do AD do Azure (por exemplo, ' ping 10.0.0.4'). Se você estiver tooping capaz de endereço IP de saudação, mas não o domínio hello, DNS pode estar configurado incorretamente. Você não pode ter configurado endereços IP de saudação do domínio hello como servidores DNS da rede virtual hello.
* Tente liberar Olá cache do resolvedor de DNS na máquina virtual de saudação ('ipconfig /flushdns').

Se você obtiver toohello caixa de diálogo que solicita o domínio de saudação toojoin credenciais, você não tem problemas de conectividade.

### <a name="credentials-related-issues"></a>Problemas de credenciais
Consulte toohello etapas a seguir se você estiver tendo problemas com as credenciais e não é possível toojoin Olá domínio.

* Tente usar credenciais de toospecify em formato Olá UPN. Olá SAMAccountName para sua conta pode ser gerada automaticamente se houver vários usuários com hello UPN mesmo prefixo no seu locatário ou se o prefixo do UPN é excessivamente longo. Portanto, o formato de SAMAccountName Olá para sua conta pode ser diferente do que você espera ou usa em seu domínio local.
* Tente toouse credenciais de saudação de uma conta de usuário que pertence a toohello 'Administradores do controlador de domínio do AAD' grupo toojoin máquinas toohello domínio gerenciado.
* Certifique-se de que você tenha [ativado a sincronização de senha](active-directory-ds-getting-started-password-sync.md) conforme Olá etapas descritas no guia de Introdução do hello.
* Certifique-se de que você use Olá UPN do usuário Olá conforme configurado no AD do Azure (por exemplo, 'bob@domainservicespreview.onmicrosoft.com') toosign no.
* Certifique-se de que já esperou tempo suficiente para toocomplete de sincronização de senha conforme especificado no guia de Introdução do hello.

## <a name="related-content"></a>Conteúdo relacionado
* [Serviços de Domínio do Azure AD - guia de Introdução](active-directory-ds-getting-started.md)
* [Administrar um domínio gerenciado dos Serviços de Domínio do Azure AD](active-directory-ds-admin-guide-administer-domain.md)
