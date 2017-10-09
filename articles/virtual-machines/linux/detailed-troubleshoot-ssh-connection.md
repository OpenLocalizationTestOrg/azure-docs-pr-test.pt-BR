---
title: aaaDetailed Solucionando problemas de SSH para uma VM do Azure | Microsoft Docs
description: "Obter mais etapas de problemas para se conectar a máquina virtual do Azure de tooan de solução de problemas de SSH"
keywords: "conexão ssh recusada, erro de ssh, ssh do azure, falha de conexão SSH"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: b8e8be5f-e8a6-489d-9922-9df8de32e839
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: support-article
ms.date: 07/06/2017
ms.author: iainfou
ms.openlocfilehash: 3f711e53a8251f8c06dbb589a258222566a4ae1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="detailed-ssh-troubleshooting-steps-for-issues-connecting-tooa-linux-vm-in-azure"></a>Etapas para problemas de conexão tooa VM do Linux no Azure de solução de problemas de SSH detalhada
Há muitas razões possíveis que Olá SSH cliente não pode ser tooreach capaz de serviço SSH Olá em Olá VM. Se você tiver seguido por meio de hello mais [geral SSH etapas de solução de problemas](troubleshoot-ssh-connection.md), você precisa toofurther solucionar problema de conexão de saudação. Este artigo orienta você toodetermine de etapas de solução de problemas detalhada onde Olá conexão SSH está falhando e como tooresolve-lo.

## <a name="take-preliminary-steps"></a>Realizar etapas preliminares
Olá diagrama a seguir mostra os componentes de saudação que estão envolvidos.

![Diagrama que mostra os componentes de serviço SSH](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot1.png)

Hello etapas a seguir ajudarão a identificar a origem de saudação de falha de saudação e descobrir soluções ou soluções alternativas.

1. Verificar status de saudação do hello VM no portal de saudação.
   Em Olá [portal do Azure](https://portal.azure.com), selecione **máquinas virtuais** > *nome da VM*.

   Olá painel de status para Olá VM deve mostrar **executando**. Role para baixo a atividade recente tooshow de computação, armazenamento e recursos de rede.

2. Selecione **configurações** tooexamine pontos de extremidade, endereços IP, grupos de segurança de rede e outras configurações.

   Olá VM deve ter um ponto de extremidade definido para o tráfego SSH que você pode exibir no **pontos de extremidade** ou  **[grupo de segurança de rede](../../virtual-network/virtual-networks-nsg.md)**. Os pontos de extremidade nas VMs que foram criados usando o Resource Manager são armazenados em um grupo de segurança de rede. Além disso, verifique se que regras de saudação tem sido aplicada toohello grupo de segurança de rede e que eles sejam referenciados na sub-rede Olá.

tooverify conectividade de rede, verifique os pontos de extremidade de saudação configurado e se você pode acessar Olá VM por meio de outro protocolo, como HTTP ou outro serviço.

Após estas etapas, tente a conexão novamente do hello SSH.

## <a name="find-hello-source-of-hello-issue"></a>Localizar origem de saudação do problema Olá
cliente SSH Olá em seu computador pode falhar SSH serviço Olá tooreach Olá VM do Azure devido tooissues ou configurações incorretas em Olá áreas a seguir:

* [Computador cliente de SSH](#source-1-ssh-client-computer)
* [Dispositivo de borda da organização](#source-2-organization-edge-device)
* [Ponto de extremidade de serviço de nuvem e ACL (lista de controle de acesso)](#source-3-cloud-service-endpoint-and-acl)
* [Grupos de segurança de rede](#source-4-network-security-groups)
* [VM baseada em Linux no Azure](#source-5-linux-based-azure-virtual-machine)

## <a name="source-1-ssh-client-computer"></a>Fonte 1: computador cliente de SSH
tooeliminate seu computador como fonte de saudação de falha de saudação, verifique se que ele pode fazer SSH conexões tooanother no local, computador baseado em Linux.

![Diagrama que realça os componentes do computador cliente SSH](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot2.png)

Se a conexão de saudação falhar, verifique Olá problemas a seguir em seu computador:

* Uma configuração de firewall local que está bloqueando o tráfego SSH de entrada ou de saída (TCP 22)
* Um software de proxy cliente instalado localmente que está impedindo conexões de SSH
* Um software de monitoramento de rede instalado localmente que está impedindo conexões SSH
* Outros tipos de software de segurança que monitoram o tráfego ou que permitem/não permitem tipos específicos de tráfego

Se uma das seguintes condições se aplicar, temporariamente desabilitar software hello e tente um toofind SSH conexão tooan local computador out motivo Olá conexão hello está sendo bloqueado no seu computador. Em seguida, trabalhar com seu administrador toocorrect Olá software configurações tooallow SSH conexões de rede.

Se você estiver usando autenticação de certificado, verifique se essas pastas de .ssh toohello permissões em seu diretório base:

* Chmod 700 ~/.ssh
* Chmod 644 ~/.ssh/\*.pub
* Chmod 600 ~/.ssh/id_rsa (ou quaisquer outros arquivos que têm suas chaves privadas armazenadas)
* Chmod 644 ~/.ssh/known_hosts (contém hosts que você se conectou toovia SSH)

## <a name="source-2-organization-edge-device"></a>Fonte 2: dispositivo de borda da organização
tooeliminate seu dispositivo de borda de organização como fonte de saudação de falha de hello, verifique se um computador que está diretamente conectado toohello Internet pode fazer conexões de SSH tooyour VM do Azure. Se você estiver acessando Olá VM em uma conexão de rota expressa do Azure ou de VPN site a site, ignorar muito[fonte 4: grupos de segurança de rede](#nsg).

![Diagrama que realça o dispositivo de borda da organização](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot3.png)

Se você não tiver um computador que está toohello diretamente conectado à Internet, crie uma nova VM do Azure em seu próprio serviço de nuvem ou o grupo de recursos e usá-lo. Para saber mais, consulte [Criar uma máquina virtual que execute o Linux no Azure](quick-create-cli.md). Exclua serviço de nuvem ou VM e grupo de recursos de hello quando você concluiu o teste.

Se você pode criar uma conexão SSH com um computador que está diretamente conectado toohello da Internet, verifique o dispositivo de borda da organização para:

* Um firewall interno que está bloqueando o tráfego SSH com hello da Internet
* Um servidor proxy que está impedindo conexões SSH
* Software de detecção de invasão ou de monitoramento de rede em execução em dispositivos em sua rede de borda que está impedindo conexões SSH

Trabalhe com seu administrador toocorrect Olá as configurações de rede do tráfego organização borda dispositivos tooallow SSH com hello da Internet.

## <a name="source-3-cloud-service-endpoint-and-acl"></a>Fonte 3: ponto de extremidade de serviço de nuvem e ACL
> [!NOTE]
> Esta fonte se aplica apenas tooVMs que foram criados usando o modelo de implantação clássico hello. Para VMs que foram criadas usando o Gerenciador de recursos, ignorar muito[fonte 4: grupos de segurança de rede](#nsg).

ACL como fonte de saudação de falha de Olá e extremidade de serviço de nuvem tooeliminate Olá verificar que outra VM do Azure no hello mesmo rede virtual pode fazer conexões de SSH tooyour VM.

![Diagrama que realça a ACL e o ponto de extremidade do serviço de nuvem](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot4.png)

Se você não tiver outra VM em Olá mesma rede virtual, você pode facilmente criar um. Para obter mais informações, consulte [criar uma VM do Linux no Azure usando Olá CLI](quick-create-cli.md). Excluir Olá VM extra, quando você concluir o teste.

Se você pode criar uma conexão SSH com uma VM em Olá mesmo virtual de rede, verifique Olá áreas a seguir:

* **configuração de ponto de extremidade Olá para o tráfego SSH no destino Olá VM.** a porta TCP privada saudação do ponto de extremidade de saudação deve corresponder em qual Olá SSH serviço Olá VM está escutando a porta TCP hello. (a porta padrão de saudação é 22). Verifique se o número da porta SSH TCP Olá no portal do Azure de saudação selecionando **máquinas virtuais** > *nome da VM* > **configurações**  >  **Pontos de extremidade**.
* **saudação ACL do ponto de extremidade de tráfego Olá SSH na máquina de virtual de destino hello.** Uma ACL permite toospecify permitido ou negado o tráfego de entrada de saudação da Internet, com base em seu endereço IP de origem. As ACLs configuradas incorretamente podem impedir que o ponto de extremidade toohello tráfego de entrada SSH. Verifique seu tooensure ACLs que o tráfego de entrada de endereços IP públicos de saudação do seu proxy ou outro servidor de borda é permitido. Para obter mais informações, veja [Sobre ACLs (listas de controle de acesso) de rede](../../virtual-network/virtual-networks-acl.md).

ponto de extremidade do tooeliminate Olá como uma fonte de problema hello, remover o ponto de extremidade atual hello, criar outro ponto de extremidade e especifique Olá SSH nome (porta TCP 22 para o número de porta pública e privada Olá). Para obter mais informações, consulte [Configurar pontos de extremidade em uma máquina virtual no Azure](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

<a id="nsg"></a>

## <a name="source-4-network-security-groups"></a>Fonte 4: Grupos de segurança de rede
Grupos de segurança de rede permitem que você toohave controle mais granular do tráfego de entrada e saído permitido. Você pode criar regras que abrangem sub-redes e serviços de nuvem em uma rede virtual do Azure. Verifique seu tooensure de regras de grupo de segurança de rede que tooand de tráfego SSH de saudação que à Internet é permitida.
Para saber mais, confira [Sobre grupos de segurança de rede](../../virtual-network/virtual-networks-nsg.md).

Você também pode usar o IP verificar a configuração do toovalidate Olá NSG. Para saber mais, veja [Visão geral do monitoramento de rede do Azure](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview). 

## <a name="source-5-linux-based-azure-virtual-machine"></a>Fonte 5: máquina virtual do Azure baseada no Linux
fonte de última Olá de possíveis problemas é hello Azure própria máquina virtual.

![Diagrama que realça uma VM do Azure baseada em Linux](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot5.png)

Se você ainda não tiver feito isso, siga as instruções de saudação [tooreset uma senha ou SSH para máquinas virtuais baseadas em Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

Tente se conectar novamente do seu computador. Se ele ainda falhar, Olá seguem alguns dos problemas possíveis hello:

* Olá serviço SSH não está em execução na máquina de virtual de destino hello.
* Olá serviço SSH não está escutando na porta TCP 22. tootest, instalar um cliente telnet no computador local e execute "telnet *cloudServiceName*. cloudapp.net 22". Esta etapa determina se Olá VM permite que o ponto de extremidade de SSH de toohello comunicação de entrada e saída.
* local de firewall na máquina de virtual de destino Olá Olá tem regras que estão impedindo o tráfego SSH de entrada ou saído.
* Detecção de intrusão ou software que está em execução na máquina virtual do Azure de saudação de monitoramento de rede está impedindo conexões SSH.

## <a name="additional-resources"></a>Recursos adicionais
Para obter mais informações sobre como solucionar problemas de acesso do aplicativo, consulte [aplicativos de tooan acesso de solução de problemas em execução em uma máquina virtual do Azure](troubleshoot-app-connection.md)
