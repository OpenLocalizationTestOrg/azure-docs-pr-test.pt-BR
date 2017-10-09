---
title: aaaRemote Desktop tooa VM do Linux | Microsoft Docs
description: "Saiba como tooinstall e configurar a área de trabalho remota tooconnect tooa VM Linux do Microsoft Azure para o modelo de implantação clássico Olá"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 34348659-ddb7-41da-82d6-b5885859e7e4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: mingzhan
ms.openlocfilehash: aadd6e87883cf9cacf9d198b680669d594206e61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-remote-desktop-tooconnect-tooa-microsoft-azure-linux-vm"></a>Usando a área de trabalho remota tooconnect tooa VM Linux do Microsoft Azure
> [!IMPORTANT] 
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação. Para Olá atualizado a versão do Gerenciador de recursos deste artigo, consulte [aqui](../use-remote-desktop.md).

## <a name="overview"></a>Visão geral
O protocolo RDP é um protocolo proprietário usado para o Windows. Como podemos usar RDP tooconnect tooa VM (máquina virtual) do Linux remotamente?

Este guia fornecerá Olá resposta! Ele ajudará xrdp tooinstall e configuração em sua VM Linux do Microsoft Azure, que permite a conexão tooit com área de trabalho remota de um computador Windows. Usaremos a VM do Linux executando Ubuntu ou OpenSUSE como exemplo hello neste guia.

ferramenta de xrdp Olá é uma origem aberta no servidor RDP que permite a você tooconnect seu servidor Linux com área de trabalho remota de um computador Windows. O RDP tem um desempenho melhor do que a VNC (Computação de Rede Virtual). A VNC renderiza usando gráficos de qualidade de JPEG e pode ser lenta, enquanto o RDP é rápido e claro.

> [!NOTE]
> Você já deve ter uma VM do Microsoft Azure executando o Linux. toocreate e configurar uma VM do Linux, consulte Olá [tutorial de VM do Linux Azure](createportal.md).
> 
> 

## <a name="create-an-endpoint-for-remote-desktop"></a>Criar um ponto de extremidade para a Área de Trabalho Remota
Usaremos ponto de extremidade do saudação padrão 3389 para área de trabalho remota deste documento. Configurar o ponto de extremidade 3389 como `Remote Desktop` tooyour VM Linux como abaixo:

![imagem](./media/remote-desktop/endpoint-for-linux-server.png)

Se você não souber como tooset um ponto de extremidade para sua VM, consulte [neste guia](setup-endpoints.md).

## <a name="install-gnome-desktop"></a>Instalar o Gnome Desktop
Conecte-se tooyour VM Linux por meio de `putty`e instalar `Gnome Desktop`.

Para o Ubuntu, use:

    #sudo apt-get update
    #sudo apt-get install ubuntu-desktop


Para OpenSUSE, use:

    #sudo zypper install gnome-session

## <a name="install-xrdp"></a>Instalar o xrdp
Para o Ubuntu, use:

    #sudo apt-get install xrdp

Para OpenSUSE, use:

> [!NOTE]
> Atualize versão de OpenSUSE Olá com versão de hello que você está usando no hello comando a seguir. exemplo Hello abaixo é para `OpenSUSE 13.2`.
> 
> 

    #sudo zypper in http://download.opensuse.org/repositories/X11:/RemoteDesktop/openSUSE_13.2/x86_64/xrdp-0.9.0git.1401423964-2.1.x86_64.rpm
    #sudo zypper install tigervnc xorg-x11-Xvnc xterm remmina-plugin-vnc


## <a name="start-xrdp-and-set-xdrp-service-at-boot-up"></a>Inicie o xrdp e defina o serviço xdrp na inicialização
Para OpenSUSE, use:

    #sudo systemctl start xrdp
    #sudo systemctl enable xrdp

Para Ubuntu, o xrdp será iniciado e habilitado automaticamente na inicialização após a instalação.

## <a name="using-xfce-if-you-are-using-an-ubuntu-version-later-than-ubuntu-1204lts"></a>Usando xfce se você estiver usando uma versão do Ubuntu posterior ao Ubuntu 12.04LTS
Porque a versão atual Olá de xrdp não oferece suporte Desktop Gnome para Ubuntu versões posterior Ubuntu 12.04LTS, usaremos `xfce` área de trabalho em vez disso.

tooinstall `xfce`, use este comando:

    #sudo apt-get install xubuntu-desktop

Em seguida, habilite `xfce` usando este comando:

    #echo xfce4-session >~/.xsession

Editar o arquivo de configuração de saudação `/etc/xrdp/startwm.sh`:

    #sudo vi /etc/xrdp/startwm.sh   

Adicionar linha hello `xfce4-session` antes da linha de saudação `/etc/X11/Xsession`.

toorestart Olá xrdp serviço, use:

    #sudo service xrdp restart


## <a name="connect-your-linux-vm-from-a-windows-machine"></a>Conectar-se à VM Linux de uma máquina com Windows
Em um computador Windows, iniciar o cliente de área de trabalho remota hello e insira o nome DNS da VM Linux. Ou vá toohello painel da VM no portal do Azure de saudação e clique em `Connect` tooconnect sua VM do Linux. Nesse caso, você ver a janela de logon hello:

![imagem](./media/remote-desktop/no2.png)

Faça logon com o nome de usuário de saudação e a senha da sua VM do Linux.

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre o uso do xrdp, consulte [http://www.xrdp.org/](http://www.xrdp.org/).
