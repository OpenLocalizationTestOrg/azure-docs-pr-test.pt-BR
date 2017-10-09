---
title: "problemas de conexão de SSH aaaTroubleshoot tooan VM do Azure | Microsoft Docs"
description: "Como tootroubleshoot problemas, como 'conexão SSH com falha' ou 'conexão SSH recusada' para uma VM do Azure executando o Linux."
keywords: "conexão ssh recusada, erro de ssh, ssh do azure, falha de conexão SSH"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: dcb82e19-29b2-47bb-99f2-900d4cfb5bbb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: iainfou
ms.openlocfilehash: dfb4e75e571c8306edf5f300c4e0f07a5fe7750a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-ssh-connections-tooan-azure-linux-vm-that-fails-errors-out-or-is-refused"></a>Solucionar problemas de conexões de SSH tooan VM do Linux do Azure que falhar, erros, ou foi recusada
Há vários motivos que você encontrar erros de Secure Shell (SSH), falhas de conexão SSH, ou SSH é recusada quando você tentar tooconnect tooa Linux VM (máquina virtual). Este artigo ajuda você a localizar e problemas de saudação correto. Você pode usar o hello portal do Azure, CLI do Azure ou extensão de acesso de VM para Linux tootroubleshoot e resolver problemas de conexão.

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Se você precisar de mais ajuda a qualquer momento neste artigo, você pode contatar hello Azure especialistas em [Olá fóruns MSDN Azure e o estouro de pilha](http://azure.microsoft.com/support/forums/). Como alternativa, você pode registrar um incidente de suporte do Azure. Vá toohello [site de suporte do Azure](http://azure.microsoft.com/support/options/) e selecione **obter suporte**. Para obter informações sobre como usar o suporte do Azure, leia Olá [perguntas frequentes sobre o suporte da Microsoft Azure](http://azure.microsoft.com/support/faq/).

## <a name="quick-troubleshooting-steps"></a>Etapas rápidas para solucionar problemas
Depois de cada etapa de solução de problemas, tente reconectar-se toohello VM.

1. Redefina a configuração de SSH de saudação.
2. Redefina credenciais de saudação do usuário hello.
3. Verifique se Olá [grupo de segurança de rede](../../virtual-network/virtual-networks-nsg.md) regras permitem o tráfego SSH.
   * Certifique-se de que o grupo de segurança de rede existe uma regra de tráfego SSH toopermit (por padrão, a porta TCP 22).
   * Você não pode usar o mapeamento/redirecionamento de porta sem usar um Azure Load Balancer.
4. Verificar Olá [integridade de recursos da VM](../../resource-health/resource-health-overview.md). 
   * Certifique-se de que Olá VM relatórios como íntegro.
   * Se você tiver habilitado o diagnóstico de inicialização, verifique se Olá VM não está relatando erros de inicialização nos logs de saudação.
5. Reinicie Olá VM.
6. Reimplante Olá VM.

Caso você precise de etapas e explicações mais detalhadas para solução de problemas, continue lendo.

## <a name="available-methods-tootroubleshoot-ssh-connection-issues"></a>Problemas de conexão métodos disponíveis tootroubleshoot SSH
Você pode redefinir as credenciais ou configuração de SSH usando um dos métodos a seguir de saudação:

* [Portal do Azure](#use-the-azure-portal) - ótimo se você precisar tooquickly redefinir a configuração de SSH hello ou chave SSH e você não tiver instaladas as ferramentas do Azure hello.
* [2.0 do CLI do Azure](#use-the-azure-cli-20) - se você já estiver na linha de comando hello, rapidamente configuração de SSH Olá redefinição ou credenciais. Você também pode usar o hello [1.0 da CLI do Azure](#use-the-azure-cli-10)
* [Extensão VMAccessForLinux do Azure](#use-the-vmaccess-extension) - crie e reutilizar json definição arquivos tooreset Olá SSH configuração ou credenciais do usuário.

Depois de cada etapa de solução de problemas, tente conectar-se tooyour VM novamente. Se você ainda não é possível se conectar, tente Olá próxima etapa.

## <a name="use-hello-azure-portal"></a>Use Olá portal do Azure
Olá portal do Azure fornece uma saudação tooreset de maneira rápida as credenciais de usuário ou a configuração de SSH sem instalar as ferramentas no computador local.

Selecione a VM em Olá portal do Azure. Role para baixo toohello **suporte + solução de problemas** seção e selecione **Redefinir senha** como Olá exemplo a seguir:

![Redefinir a configuração de SSH ou credenciais no hello portal do Azure](./media/troubleshoot-ssh-connection/reset-credentials-using-portal.png)

### <a name="reset-hello-ssh-configuration"></a>Redefinir a configuração de SSH Olá
Como uma primeira etapa, selecione `Reset configuration only` de saudação **modo** menu suspenso como na saudação anterior a captura de tela, e clique em Olá **redefinir** botão. Após concluir esta ação, tente tooaccess sua VM novamente.

### <a name="reset-ssh-credentials-for-a-user"></a>Redefinir credenciais SSH para um usuário
credenciais de saudação tooreset de um usuário existente, selecione `Reset SSH public key` ou `Reset password` de saudação **modo** menu suspenso como Olá anterior a captura de tela. Especificar nome de usuário hello e uma chave SSH ou nova senha e clique em Olá **redefinir** botão.

Você também pode criar um usuário com privilégios de sudo no hello VM nesse menu. Insira um novo nome de usuário e a senha associada ou a chave SSH e, em seguida, clique em Olá **redefinir** botão.

## <a name="use-hello-azure-cli-20"></a>Use Olá 2.0 do CLI do Azure
Se você ainda não fez isso, instale hello mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) e fazer logon na conta do Azure usando o tooan [logon az](/cli/azure/#login).

Se você criou e carregar uma imagem de disco Linux personalizada, verifique se Olá [agente Linux do Microsoft Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) versão 2.0.5 ou posterior está instalado. Para VMs criadas usando imagens da galeria, é possível que essa extensão de acesso já esteja instalada e configurada para você.

### <a name="reset-ssh-configuration"></a>Redefinir a configuração de SSH
Você pode inicialmente tente redefinindo Olá SSH configuração toodefault valores e o servidor SSH de hello está sendo reiniciado no Olá VM. Observe que isso não altera o nome de conta de usuário hello, a senha ou as chaves de SSH.
Olá exemplo a seguir usa [az vm usuário Redefinir-ssh](/cli/azure/vm/user#reset-ssh) tooreset configuração de SSH Olá em Olá VM denominada `myVM` em `myResourceGroup`. Use seus próprios valores, da seguinte maneira:

```azurecli
az vm user reset-ssh --resource-group myResourceGroup --name myVM
```

### <a name="reset-ssh-credentials-for-a-user"></a>Redefinir credenciais SSH para um usuário
Olá exemplo a seguir usa [atualização de usuário de vm az](/cli/azure/vm/user#update) tooreset Olá credenciais para `myUsername` toohello valor especificado em `myPassword`, em Olá VM denominada `myVM` em `myResourceGroup`. Use seus próprios valores, da seguinte maneira:

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
     --username myUsername --password myPassword
```

Se usando a autenticação de chave SSH, você pode redefinir a chave SSH Olá para um determinado usuário. Hello exemplo a seguir usa **az vm acesso de usuário do linux de conjunto** tooupdate Olá SSH chave armazenada em `~/.ssh/id_rsa.pub` de usuário Olá chamado `myUsername`, em Olá VM denominada `myVM` em `myResourceGroup`. Use seus próprios valores, da seguinte maneira:

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
    --username myUsername --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="use-hello-vmaccess-extension"></a>Usar a extensão VMAccess Olá
Olá extensão de acesso de VM para Linux lê um arquivo json que define ações toocarry-out. Essas ações incluem redefinir o SSHD, redefinir uma chave SSH ou adicionar um usuário. Você ainda usar Olá toocall da CLI do Azure Olá extensão VMAccess, mas você pode reutilizar arquivos json de saudação entre várias VMs, se desejado. Essa abordagem permite que você toocreate um repositório de arquivos de json que pode ser chamado para determinado cenários.

### <a name="reset-sshd"></a>Redefinir SSHD
Crie um arquivo chamado `settings.json` com hello conteúdo a seguir:

```json
{  
    "reset_ssh":"True"
}
```

Usando Olá CLI do Azure, você, em seguida, chamar hello `VMAccessForLinux` extensão tooreset sua conexão SSHD especificando o arquivo json. Olá exemplo a seguir usa [conjunto de extensão de vm az](/cli/azure/vm/extension#set) tooreset SSHD em Olá VM denominada `myVM` em `myResourceGroup`. Use seus próprios valores, da seguinte maneira:

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

### <a name="reset-ssh-credentials-for-a-user"></a>Redefinir credenciais SSH para um usuário
Se SSHD aparecer toofunction corretamente, você pode redefinir credenciais de saudação para um usuário doador. senha de saudação tooreset para um usuário, crie um arquivo chamado `settings.json`. Olá, exemplo a seguir redefine credenciais Olá para `myUsername` toohello valor especificado em `myPassword`. Digite hello seguintes linhas no seu `settings.json` de arquivo, usando seus próprios valores:

```json
{
    "username":"myUsername", "password":"myPassword"
}
```

Ou tooreset Olá chave SSH de um usuário, primeiro crie um arquivo chamado `settings.json`. Olá, exemplo a seguir redefine credenciais Olá para `myUsername` toohello valor especificado em `myPassword`, em Olá VM denominada `myVM` em `myResourceGroup`. Digite hello seguintes linhas no seu `settings.json` de arquivo, usando seus próprios valores:

```json
{
    "username":"myUsername", "ssh_key":"mySSHKey"
}
```

Após criar o arquivo json, use saudação do hello CLI do Azure toocall `VMAccessForLinux` tooreset extensão credenciais de usuário SSH, especificando o arquivo json. Olá, exemplo a seguir redefine credenciais em Olá VM denominada `myVM` em `myResourceGroup`. Use seus próprios valores, da seguinte maneira:

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

## <a name="use-hello-azure-cli-10"></a>Use Olá 1.0 da CLI do Azure
Se você ainda não o fez, [instalar Olá 1.0 da CLI do Azure e conecte-se tooyour assinatura do Azure](../../cli-install-nodejs.md). Certifique-se de que você esteja usando o modo Resource Manager da seguinte forma:

```azurecli
azure config mode arm
```

Se você criou e carregar uma imagem de disco Linux personalizada, verifique se Olá [agente Linux do Microsoft Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) versão 2.0.5 ou posterior está instalado. Para VMs criadas usando imagens da galeria, é possível que essa extensão de acesso já esteja instalada e configurada para você.

### <a name="reset-ssh-configuration"></a>Redefinir a configuração de SSH
configuração de SSHD Olá propriamente dita pode estar configurado incorretamente ou Olá serviço encontrou um erro. Você pode redefinir SSHD toomake-se de que a configuração de SSH Olá propriamente dita é válida. Redefinir SSHD deve ser Olá primeira etapa para solução de problemas que você tomar.

Olá, exemplo a seguir redefine SSHD em uma VM denominada `myVM` no grupo de recursos de saudação denominado `myResourceGroup`. Use seus próprios nomes de grupo de recursos e de VM, da seguinte maneira:

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --reset-ssh
```

### <a name="reset-ssh-credentials-for-a-user"></a>Redefinir credenciais SSH para um usuário
Se SSHD aparecer toofunction corretamente, você pode redefinir a senha de saudação para um usuário doador. Olá, exemplo a seguir redefine credenciais Olá para `myUsername` toohello valor especificado em `myPassword`, em Olá VM denominada `myVM` em `myResourceGroup`. Use seus próprios valores, da seguinte maneira:

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
     --user-name myUsername --password myPassword
```

Se usando a autenticação de chave SSH, você pode redefinir a chave SSH Olá para um determinado usuário. Olá atualizações de exemplo a seguir Olá chave SSH armazenada em `~/.ssh/id_rsa.pub` de usuário Olá chamado `myUsername`, em Olá VM denominada `myVM` em `myResourceGroup`. Use seus próprios valores, da seguinte maneira:

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --user-name myUsername --ssh-key-file ~/.ssh/id_rsa.pub
```


## <a name="restart-a-vm"></a>Reiniciar uma VM
Se você redefinir as credenciais de usuário e a configuração de SSH hello ou encontrou um erro ao fazer isso, você pode tentar reiniciar Olá VM tooaddress subjacente problemas de computação.

### <a name="azure-portal"></a>Portal do Azure
toorestart uma VM usando hello Azure selecione portal, a saudação VM e clique em **reiniciar** botão como Olá exemplo a seguir:

![Reiniciar uma VM em Olá portal do Azure](./media/troubleshoot-ssh-connection/restart-vm-using-portal.png)

### <a name="azure-cli-10"></a>CLI 1.0 do Azure
Olá reinicializações de exemplo a seguir Olá VM denominada `myVM` no grupo de recursos de saudação denominado `myResourceGroup`. Use seus próprios valores, da seguinte maneira:

```azurecli
azure vm restart --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a>CLI do Azure 2.0
Olá exemplo a seguir usa [reinicialização de vm az](/cli/azure/vm#restart) toorestart Olá VM denominada `myVM` no grupo de recursos de saudação denominado `myResourceGroup`. Use seus próprios valores, da seguinte maneira:

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```


## <a name="redeploy-a-vm"></a>Reimplantar uma VM
Você pode reutilizar um nó de tooanother VM no Azure, que pode corrigir problemas de rede subjacentes. Para obter informações sobre como reimplantar uma VM, consulte [reimplantar a máquina virtual toonew nó do Azure](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

> [!NOTE]
> Após concluir esta operação, disco efêmera, os dados serão perdidos e endereços IP dinâmicos que estão associados com a máquina virtual de saudação serão atualizados.
> 
> 

### <a name="azure-portal"></a>Portal do Azure
tooredeploy uma VM usando hello Azure selecione portal, a VM e role para baixo toohello **suporte + solução de problemas** seção. Clique em Olá **reimplantar** botão como Olá exemplo a seguir:

![Reimplantar uma VM em Olá portal do Azure](./media/troubleshoot-ssh-connection/redeploy-vm-using-portal.png)

### <a name="azure-cli-10"></a>CLI 1.0 do Azure
Olá reimplanta de exemplo a seguir Olá VM denominada `myVM` no grupo de recursos de saudação denominado `myResourceGroup`. Use seus próprios valores, da seguinte maneira:

```azurecli
azure vm redeploy --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a>CLI do Azure 2.0
Olá uso do exemplo a seguir [reimplantação da vm de az](/cli/azure/vm#redeploy) tooredeploy Olá VM denominada `myVM` no grupo de recursos de saudação denominado `myResourceGroup`. Use seus próprios valores, da seguinte maneira:

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM
```

## <a name="vms-created-by-using-hello-classic-deployment-model"></a>Máquinas virtuais criadas usando o modelo de implantação clássico Olá
Repita essas etapas tooresolve hello mais comuns SSH conexão falhas para VMs que foram criados usando o modelo de implantação clássico hello. Depois de cada etapa, tente reconectar-se toohello VM.

* Redefinir o acesso remoto de saudação [portal do Azure](https://portal.azure.com). Na Olá portal do Azure, selecione a VM e clique em Olá **redefinir remoto...**  botão.
* Reinicie Olá VM. Em Olá [portal do Azure](https://portal.azure.com), selecione a VM e clique Olá **reiniciar** botão.
    
* Reimplante Olá VM tooa novo nó do Azure. Para obter informações sobre como tooredeploy uma VM, consulte [reimplantar a máquina virtual toonew nó do Azure](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
  
    Após concluir esta operação, disco efêmera, os dados serão perdidos e endereços IP dinâmicos que estão associados com a máquina virtual de saudação serão atualizados.
* Siga as instruções de saudação em [como tooreset uma senha ou SSH para máquinas virtuais baseadas em Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) para:
  
  * Olá redefinição da senha ou chave SSH.
  * Criar uma nova conta de usuário *sudo*.
  * Redefina a configuração de SSH de saudação.
* Verifique a integridade dos recursos da VM Olá para quaisquer problemas de plataforma.<br>
     Selecione sua VM e role para baixo para **Configurações** > **Verificar Integridade**.

## <a name="additional-resources"></a>Recursos adicionais
* Se você ainda não é possível tooSSH tooyour VM depois de seguir Olá após etapas, consulte [obter as etapas de solução de problemas mais](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooreview adicional etapas tooresolve seu problema.
* Para obter mais informações sobre como solucionar problemas de acesso do aplicativo, consulte [aplicativos de tooan acesso de solução de problemas em execução em uma máquina virtual do Azure](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Para obter mais informações sobre como solucionar problemas de máquinas virtuais que foram criadas usando o modelo de implantação clássico hello, consulte [como tooreset uma senha ou SSH para máquinas virtuais baseadas em Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

