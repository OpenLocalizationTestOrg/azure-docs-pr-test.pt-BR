---
title: "aaaAzure início rápido - criar Portal de VM do Windows | Microsoft Docs"
description: "Início Rápido do Azure – Portal Criar VM do Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5646ad51244db6d214c0121d1f7cc45c59f9a78b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-hello-azure-portal"></a>Criar uma máquina virtual do Windows com hello portal do Azure

Máquinas virtuais do Azure podem ser criadas por meio de saudação portal do Azure. Esse método fornece uma interface do usuário baseada em navegador para a criação e configuração de máquinas virtuais e todos os recursos relacionados. Este guia de início rápido percorre criando uma máquina virtual e instalar um servidor Web no hello VM.

Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.

## <a name="log-in-tooazure"></a>Faça logon no tooAzure

Faça logon em toohello portal do Azure em http://portal.azure.com.

## <a name="create-virtual-machine"></a>Criar máquina virtual

1. Clique em Olá **novo** botão localizado no canto superior esquerdo de saudação do hello portal do Azure.

2. Selecione **Computação** e, em seguida, selecione **Windows Server 2016 Datacenter**. 

3. Insira informações da máquina virtual hello. nome de usuário de saudação e a senha digitada aqui é toolog usada na máquina virtual de toohello. Ao concluir, clique em **OK**.

    ![Insira as informações básicas sobre sua VM na folha portal Olá](./media/quick-create-portal/create-windows-vm-portal-basic-blade.png)  

4. Selecione um tamanho para Olá VM. toosee mais tamanhos, selecione **exibir todos os** ou alterar Olá **suporte para o tipo de disco** filtro. 

    ![A captura de tela que mostra os tamanhos da VM](./media/quick-create-portal/create-windows-vm-portal-sizes.png)  

5. Na folha de configurações hello, lembre-Olá padrões e clique em **Okey**.

6. Na página de resumo de saudação, clique em **Okey** toostart implantação da máquina virtual hello.

7. Olá VM será fixado toohello painel do portal do Azure. Após a conclusão da implantação hello, folha de resumo de VM Olá é aberto automaticamente.


## <a name="connect-toovirtual-machine"></a>Conectar máquina toovirtual

Crie uma máquina de virtual de toohello de conexão de área de trabalho remota.

1. Clique em Olá **conectar** botão nas propriedades de máquina virtual de saudação. Um arquivo do protocolo RDP (.rdp) é criado e baixado.

    ![Portal 9](./media/quick-create-portal/quick-create-portal/portal-quick-start-9.png) 

2. tooconnect tooyour VM, abra Olá baixado o arquivo RDP. Se solicitado, clique em **Conectar**. Em um Mac, você precisa de um cliente RDP como esta [área de trabalho remota](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12) de saudação Mac App Store.

3. Insira o nome de usuário de saudação e senha que você especificou ao criar a máquina virtual de saudação, clique em **Okey**.

4. Você receberá um aviso de certificado durante o processo de entrada hello. Clique em **Sim** ou **continuar** tooproceed com conexão hello.


## <a name="install-iis-using-powershell"></a>Instalar o IIS usando o PowerShell

Na máquina virtual de hello, iniciar uma sessão do PowerShell e execute Olá tooinstall comando IIS a seguir.

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

Quando terminar, sair da sessão RDP hello e retornam propriedades da VM Olá em Olá portal do Azure.

## <a name="open-port-80-for-web-traffic"></a>Abra a porta 80 para tráfego da Web 

Um Grupo de Segurança de Rede (NSG) protege o tráfego de entrada e saída. Quando uma máquina virtual é criada a partir Olá portal do Azure, uma regra de entrada é criada na porta 3389 para conexões RDP. Como essa VM hospeda um servidor Web, uma regra NSG necessita toobe criado para a porta 80.

1. Na máquina virtual de Olá, clique em nome de saudação do hello **grupo de recursos**.
2. Selecione Olá **grupo de segurança de rede**. Olá NSG pode ser identificado usando Olá **tipo** coluna. 
3. No menu esquerdo hello, em configurações, clique em **regras de segurança de entrada**.
4. Clique em **Adicionar**.
5. Em **Nome**, digite **http**. Certifique-se de **intervalo de portas** é definir too80 e **ação** está definido muito**permitir**. 
6. Clique em **OK**.


## <a name="view-hello-iis-welcome-page"></a>Olá exibir página de boas-vindas do IIS

Com o IIS instalado e a porta 80 abra tooyour VM, Olá servidorweb agora pode ser acessado de saudação à internet. Abra um navegador da web e digite o endereço IP público de saudação do hello VM. endereço IP público de saudação pode ser encontrado na folha VM Olá no hello portal do Azure.

![Site do IIS padrão](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a>Limpar recursos

Quando não é mais necessário, exclua o grupo de recursos de saudação, máquina virtual e todos os recursos relacionados. toodo, portanto, selecione o grupo de recursos de saudação da folha de máquina virtual hello e clique em **excluir**.

## <a name="next-steps"></a>Próximas etapas

Neste início rápido, você implantou uma máquina virtual simples, uma regra de grupo de segurança de rede e instalou um servidor Web. toolearn mais sobre máquinas virtuais do Azure, continuar toohello tutorial para VMs do Windows.

> [!div class="nextstepaction"]
> [Tutoriais de máquina virtual do Windows Azure](./tutorial-manage-vm.md)
