---
title: "área de trabalho remota de aaaUse tooa VM do Linux no Azure | Microsoft Docs"
description: "Saiba como tooinstall e configurar a área de trabalho remota (xrdp) tooconnect tooa VM do Linux no Azure usando as ferramentas gráficas"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: iainfou
ms.openlocfilehash: 64d30be101ceeb49fc05bb10293ad63db358efe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-remote-desktop-tooconnect-tooa-linux-vm-in-azure"></a>Instalar e configurar a área de trabalho remota tooconnect tooa VM do Linux no Azure
Máquinas virtuais de Linux (VMs) no Azure geralmente são gerenciadas da linha de comando de saudação usando uma conexão SSH (secure shell). Quando novos tooLinux, ou para cenários de solução de problemas rápidos, uso de saudação da área de trabalho remota pode ser mais fácil. Este artigo detalhes como tooinstall e configurar um ambiente de desktop ([xfce](https://www.xfce.org)) e a área de trabalho remota ([xrdp](http://www.xrdp.org)) para sua VM do Linux usando o modelo de implantação do Gerenciador de recursos de saudação.


## <a name="prerequisites"></a>Pré-requisitos
Este artigo exige uma VM do Linux no Azure. Se você precisar toocreate uma máquina virtual, use um dos métodos a seguir de saudação:

- Olá [2.0 do CLI do Azure](quick-create-cli.md)
- Olá [portal do Azure](quick-create-portal.md)


## <a name="install-a-desktop-environment-on-your-linux-vm"></a>Instalar um ambiente de área de trabalho em sua VM do Linux
A maioria das VMs do Linux no Azure não tem um ambiente de área de trabalho instalado por padrão. As VMs do Linux são gerenciadas normalmente usando conexões SSH, em vez de um ambiente de área de trabalho. Há vários ambientes de área de trabalho no Linux para sua escolha. Dependendo de sua escolha de ambiente de desktop, pode consumir um too2 GB de espaço em disco e levar 5 tooinstall de minutos too10 e configure todos os pacotes de saudação necessário.

Olá, exemplo a seguir instala lightweight Olá [xfce4](https://www.xfce.org/) ambiente de área de trabalho em uma VM do Ubuntu. Comandos para outras distribuições variam ligeiramente (use `yum` tooinstall no Red Hat Enterprise Linux e configurar apropriado `selinux` regras ou use `zypper` tooinstall no SUSE, por exemplo).

Primeiro, SSH tooyour VM. exemplo a seguir Hello conecta toohello VM denominada *myvm.westus.cloudapp.azure.com* com nome de usuário de saudação do *azureuser*:

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

Se você estiver usando o Windows e precisa de mais informações sobre como usar SSH, consulte [como chaves de toouse SSH com o Windows](ssh-from-windows.md).

Em seguida, instale o xfce usando `apt` da seguinte maneira:

```bash
sudo apt-get update
sudo apt-get install xfce4
```

## <a name="install-and-configure-a-remote-desktop-server"></a>Instalar e configurar um servidor de área de trabalho remoto
Agora que você tem um ambiente de desktop instalado, configure um toolisten de serviços de área de trabalho remota para conexões de entrada. [xrdp](http://xrdp.org) é um servidor RDP (Protocolo de Área de Trabalho Remota) de código-fonte aberto que está disponível na maioria das distribuições Linux e funciona bem com xfce. Instale o xrdp em sua VM do Ubuntu da seguinte maneira:

```bash
sudo apt-get install xrdp
```

Conte-xrdp toouse o ambiente de desktop quando você iniciar a sessão. Configure xrdp toouse xfce como seu ambiente de área de trabalho da seguinte maneira:

```bash
echo xfce4-session >~/.xsession
```

Reinicie o serviço de xrdp de Olá Olá alterações tootake efeito da seguinte maneira:

```bash
sudo service xrdp restart
```


## <a name="set-a-local-user-account-password"></a>Definir a senha da conta de usuário local
Se você tiver criado uma senha para sua conta de usuário durante a criação de sua VM, ignore esta etapa. Se você só usa autenticação de chave SSH e não tem uma senha de conta local definido, especifique uma senha antes de usar xrdp toolog tooyour VM. O xrdp não pode aceitar chaves SSH para autenticação. Olá, exemplo a seguir especifica uma senha para a conta de usuário Olá *azureuser*:

```bash
sudo passwd azureuser
```

> [!NOTE]
> Especificando uma senha não atualizar seus logons de senha SSHD configuração toopermit se no momento não. De uma perspectiva de segurança, você pode desejar tooconnect tooyour VM com um túnel SSH usando a autenticação baseada em chave e, em seguida, conecte-se tooxrdp. Nesse caso, ignore Olá após a etapa na criação de um segurança grupo regra tooallow remote desktop tráfego de rede.


## <a name="create-a-network-security-group-rule-for-remote-desktop-traffic"></a>Criar uma regra de Grupo de Segurança de Rede para tráfego de Área de Trabalho Remota
tooreach de tráfego de área de trabalho remota tooallow sua VM do Linux, uma regra de grupo de segurança de rede precisa toobe criado que permita o TCP em tooreach de porta 3389 sua VM. Para saber mais sobre grupos de segurança de rede, confira [O que é um Grupo de Segurança de Rede?](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Você também pode [use Olá toocreate portal do Azure uma regra de grupo de segurança de rede](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Olá, exemplos a seguir criam uma regra de grupo de segurança de rede com [criar regra de nsg rede az](/cli/azure/network/nsg/rule#create) chamado *myNetworkSecurityGroupRule* muito*permitir* tráfego em *tcp* porta *3389*.

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1010 \
    --destination-port-range 3389
```


## <a name="connect-your-linux-vm-with-a-remote-desktop-client"></a>Conectar-se a sua VM do Linux com um cliente de Área de Trabalho Remota
Abra seu cliente local de área de trabalho remota e conecte-se toohello endereço IP ou nome DNS de sua VM do Linux. Insira Olá nome de usuário e senha para a conta de usuário de saudação na sua VM da seguinte maneira:

![Conecte-se tooxrdp usando seu cliente de área de trabalho remota](./media/use-remote-desktop/remote-desktop-client.png)

Depois de autenticar, ambiente de desktop saudação xfce serão carregadas e parecer semelhante toohello exemplo a seguir:

![Ambiente de área de trabalho xfce por meio de xrdp](./media/use-remote-desktop/xfce-desktop-environment.png)


## <a name="troubleshoot"></a>Solucionar problemas
Se você não conseguir conectar tooyour VM do Linux usando um cliente de área de trabalho remota, use `netstat` em tooverify sua VM do Linux que a VM está escutando conexões RDP da seguinte maneira:

```bash
sudo netstat -plnt | grep rdp
```

Olá mostrado no exemplo a seguir Olá VM escutando na porta TCP 3389 conforme o esperado:

```bash
tcp     0     0      127.0.0.1:3350     0.0.0.0:*     LISTEN     53192/xrdp-sesman
tcp     0     0      0.0.0.0:3389       0.0.0.0:*     LISTEN     53188/xrdp
```

Se o serviço de xrdp Olá não estiver escutando, em uma VM Ubuntu reinicie serviço de saudação da seguinte maneira:

```bash
sudo service xrdp restart
```

Examine logs */var/log*Thug na sua VM Ubuntu indicações de como o serviço de saudação toowhy pode não estar respondendo. Você também pode monitorar o syslog Olá durante um tooview de tentativa de conexão de área de trabalho remota erros:

```bash
tail -f /var/log/syslog
```

Outras distribuições do Linux como Red Hat Enterprise Linux e SUSE podem ter serviços toorestart de diferentes maneiras e tooreview de locais de arquivo de log alternativo.

Se você não receber nenhuma resposta no seu cliente de área de trabalho remota e não vir todos os eventos no log do sistema hello, esse comportamento indica que o tráfego de área de trabalho remoto não pode alcançar Olá VM. Revise seu tooensure regras do grupo da segurança de rede que você tenha uma regra toopermit TCP na porta 3389. Para saber mais, veja [Solucionar problemas de conectividade do aplicativo](../windows/troubleshoot-app-connection.md).


## <a name="next-steps"></a>Próximas etapas
Para saber mais sobre como criar e usar chaves SSH com VMs do Linux, veja [Criar chaves SSH para VMs do Linux no Azure](mac-create-ssh-keys.md).

Para obter informações sobre como usar SSH do Windows, consulte [como chaves de toouse SSH com o Windows](ssh-from-windows.md).

