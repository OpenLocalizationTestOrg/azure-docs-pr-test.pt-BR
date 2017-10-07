---
title: "aaaConfigure SSHD em máquinas de virtuais de Linux do Azure | Microsoft Docs"
description: "Configure SSHD para práticas recomendadas de segurança e toolockdown SSH tooAzure máquinas virtuais do Linux."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/21/2016
ms.author: v-livech
ms.openlocfilehash: c2361be7199a24b129c06acfc899dd32f6e1d6fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-sshd-on-azure-linux-vms"></a>Configurar o SSHD em VMs do Linux do Azure

Este artigo mostra como toolockdown Olá servidor SSH no Linux, tooprovide segurança de práticas recomendada e também toospeed o processo de logon do hello SSH usando as chaves de SSH, em vez de senhas.  bloqueio toofurther SSHD vamos toodisable usuário de raiz de saudação de ser capaz de toologin, limitar Olá os usuários que têm permissão toologin por meio de uma lista de grupos aprovados, desabilitando o protocolo SSH versão 1, definir um bit de chave mínimo e configurar automaticamente logoff de usuários inativos.  Olá requisitos deste artigo são: uma conta do Azure ([obter uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/)) e [arquivos de chave públicos e privados SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="quick-commands"></a>Comandos rápidos

Configurar `/etc/ssh/sshd_config` com hello configurações a seguir:

### <a name="disable-password-logins"></a>Desabilitar logons de senha

```bash
PasswordAuthentication no
```

### <a name="disable-login-by-hello-root-user"></a>Desabilitar logon pelo usuário de raiz de saudação

```bash
PermitRootLogin no
```

### <a name="allowed-groups-list"></a>Lista de grupos permitidos

```bash
AllowGroups wheel
```

### <a name="allowed-users-list"></a>Lista de usuários permitidos

```bash
AllowUsers ahmet ralph
```

### <a name="disable-ssh-protocol-version-1"></a>Desabilitar o protocolo SSH versão 1

```bash
Protocol 2
```

### <a name="minimum-key-bits"></a>Bits de chave mínimos

```bash
ServerKeyBits 2048
```

### <a name="disconnect-idle-users"></a>Desconectar usuários ociosos

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="detailed-walkthrough"></a>Passo a passo detalhado

SSHD é hello SSH servidor que executa o hello VM do Linux.  O SSH é um cliente executado em um shell no MacBook, uma estação de trabalho do Linux ou um Bash no Windows.  SSH é também protocolo hello usado toosecure e criptografar a comunicação de saudação entre sua estação de trabalho e hello tornando SSH também uma VPN (rede Virtual privada) de VM do Linux.

Neste artigo, é muito importante tookeep logon tooyour abrir VM Linux para apresentação inteira hello.  Depois de estabelecer uma conexão SSH, ele permanece como uma sessão aberta como janela Olá não está fechada.  Tendo um terminal conectado, permite alterações toobe feita toohello service SSHD sem bloqueio se for feita uma alteração significativa.  Se você seja bloqueado da sua VM do Linux com uma configuração SSHD interrompida, o Azure oferece Olá capacidade tooreset uma configuração SSHD interrompida com hello [extensão de acesso do Azure VM](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Por esse motivo, abra dois terminais e SSH toohello VM do Linux de ambos.  Usamos Olá primeiro toomake terminal Olá alterações tooSSHDs arquivo de configuração e reiniciar o serviço SSHD hello.  Usamos Olá tootest terminal segundo as alterações depois que o serviço Olá for reiniciado.  Como desabilitar o SSH senhas e contar estritamente com chaves SSH, se as chaves SSH não estão corretas e fechar Olá conexão toohello VM, hello VM será permanentemente bloqueado e não será capaz de toologin tooit solicitá-la toobe excluído e recriado.

## <a name="disable-password-logins"></a>Desabilitar logons de senha

Olá toosecure de maneira mais rápida que a VM do Linux é toodisable logons de senha.  Quando os logons de senha são habilitados, bots rastreamento Olá web será iniciado imediatamente a tentar toobrute forçar senha de saudação de previsão para sua VM do Linux usando o SSH.  Desabilitar completamente os logons de senha, permite Olá SSH server tooignore todas as tentativas de logon de senha.

```bash
PasswordAuthentication no
```

## <a name="disable-login-by-hello-root-user"></a>Desabilitar logon pelo usuário de raiz de saudação

Seguindo práticas recomendadas do Linux, hello `root` usuário nunca deve ser conectado via SSH ou usando `sudo su`.  Todos os comandos que precisam de permissões no nível raiz devem sempre ser executados por meio de saudação `sudo` comando, que registra todas as ações de auditoria futuras.  Desabilitar Olá `root` usuário faça logon por meio do SSH é uma etapa práticas de segurança recomendada que garante que somente usuários autorizados podem tooSSH.

```bash
PermitRootLogin no
```

## <a name="allowed-groups-list"></a>Lista de grupos permitidos

O SSH oferece um método de restringir usuários e grupos que têm ou não permissão de logon via SSH.  Esse recurso usa listas tooapprove ou negar usuários e grupos específicos de fazer logon no.  Configuração Olá roda grupo toohello `AllowGroups` lista restringe logons aprovados em contas de usuário do SSH toojust que estão no grupo de roda hello.

```bash
AllowGroups wheel
```

## <a name="allowed-users-list"></a>Lista de usuários permitidos

Restringindo os usuários toojust de logons SSH é uma maneira mais específica tooaccomplish Olá a mesma tarefa que `AllowGroups` é.  

```bash
AllowUsers ahmet ralph
```

## <a name="disable-ssh-protocol-version-1"></a>Desabilitar o protocolo SSH versão 1

O protocolo SSH versão 1 não é seguro e deve ser desabilitado.  O protocolo SSH versão 2 é a versão de atual de saudação que oferece um servidor de tooyour de tooSSH de maneira segura.  Desabilitar SSH versão 1 nega a todos os clientes SSH que estão tentando tooestablish em uma conexão com servidor SSH Olá com SSH versão 1.  Apenas conexões do SSH versão 2 são permitidas toonegotiate uma conexão com o servidor SSH hello.

```bash
Protocol 2
```

## <a name="minimum-key-bits"></a>Bits de chave mínimos

Seguindo práticas recomendadas de segurança, logons SSH de senha são desabilitados e somente as chaves de SSH são permitidas toobe usado tooauthenticate com o servidor SSH hello.  Essas chaves SSH podem ser criadas usando chaves de comprimento diferente, medidas em bits.  Estados de chaves de 2048 bits de comprimento são intensidade da chave aceitável mínimo Olá de práticas recomendadas.  Em teoria, chaves com menos de 2048 bits poderiam ser violadas.  Saudação de configuração `ServerKeyBits` muito`2048` permite todas as conexões usando chaves de 2048 bits ou superior e negar conexões de menos de 2048 bits.

```bash
ServerKeyBits 2048
```

## <a name="disconnect-idle-users"></a>Desconectar usuários ociosos

SSH tem usuários de toodisconnect de capacidade de saudação que têm conexões abertas que permaneceram ociosas por mais de um período definido de segundos.  Mantendo sessões abertas tooonly os usuários que estão ativos limita a exposição de saudação do hello VM do Linux.

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="restart-sshd"></a>Reiniciar o SSHD

configurações de saudação tooenable no `/etc/ssh/sshd_config` reiniciar processo SSHD Olá que reinicia o servidor SSH hello.  janela do terminal Olá usar toorestart Olá SSH server permanecem abertos sem perder a sessão aberta de SSH hello.  configurações de servidor SSH novo do tootest Olá use uma segunda janela de terminal ou a guia.  Usar uma saudação separada tootest terminal SSH conexão permite que você toogo voltar e fazer alterações adicionais toohello `/etc/ssh/sshd_config` no terminal primeiro hello, sem que está sendo bloqueado por uma alteração SSHD significativa.  

### <a name="on-redhat-centos-and-fedora"></a>No Redhat, Centos e Fedora

```bash
service sshd restart
```

### <a name="on-debian--ubuntu"></a>No Debian e Ubuntu

```bash
service ssh restart
```

## <a name="reset-sshd-using-azure-reset-access"></a>Redefinir o SSHD usando o acesso de redefinição do Azure

Se bloqueada de uma configuração de SSHD toohello quebra de alteração, você pode usar Olá extensão de acesso da máquina virtual do Azure tooreset Olá SSHD toohello back original do configuration.

Substitua os nomes de exemplo pelos seus próprios.

```azurecli
azure vm reset-access \
--resource-group myResourceGroup \
--name myVM \
--reset-ssh
```

## <a name="install-fail2ban"></a>Instalar o Fail2ban

É altamente recomendável tooinstall e instalação Olá código-fonte aberto aplicativo Fail2ban, quais blocos repetidas tentativas toologin tooyour VM Linux via SSH usando força bruta.  Logs de Fail2ban repetidos falha tentativas toologin via SSH e, em seguida, cria regras de firewall de endereço IP do hello tooblock são provenientes de tentativas de saudação.

* [Home page do Fail2ban](http://www.fail2ban.org/wiki/index.php/Main_Page)

## <a name="next-steps"></a>Próximas etapas

Agora que você configurou e bloqueado servidor SSH de saudação em sua VM Linux há práticas recomendadas de segurança adicionais, que você pode seguir.  

* [Gerenciar usuários, SSH e seleção ou discos de reparo em máquinas virtuais do Linux do Azure usando Olá extensão VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [Criptografar discos em uma VM do Linux usando Olá CLI do Azure](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [Acesso e segurança em modelos do Azure Resource Manager](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
