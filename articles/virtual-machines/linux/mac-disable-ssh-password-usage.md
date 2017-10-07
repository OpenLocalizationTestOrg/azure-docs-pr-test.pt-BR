---
title: as senhas SSH aaaDisable em sua VM Linux Configurando SSHD | Microsoft Docs
description: Proteja sua VM Linux no Azure desabilitando logons de senha para SSH.
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: 
ms.assetid: 46137640-a7d2-40e5-a1e9-9effef7eb190
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/26/2016
ms.author: v-livech
ms.openlocfilehash: fb67b2f5b8b3bf2ba214858940b04f2ea9013fb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="disable-ssh-passwords-on-your-linux-vm-by-configuring-sshd"></a>Desabilitar senhas SSH na sua VM Linux configurando o SSHD
Este artigo se concentra em como toolock segurança de logon de saudação da VM Linux.  Como Olá porta SSH 22 é aberto toohello world bots iniciar tentar toologin através de adivinhação de senhas.  O que vamos fazer neste artigo é desabilitar os logons de senha via SSH.  Removendo completamente a capacidade de saudação toouse senhas protegemos Olá VM Linux neste tipo de bruta de ataque de força.  Olá adicionado bônus é configuraremos Linux SSHD tooonly permitir logons através de chaves SSH públicas e privadas, sem dúvida Olá tooLinux de toologin de maneira mais segura.  combinações possíveis de saudação do mesmo exigiria a chave privada do tooguess Olá é grande e, portanto, não recomenda robôs do mesmo incomodar chaves SSH tootry toobrute force.

## <a name="goals"></a>Metas
* Configure SSHD toodisallow:
  * Logons de senha
  * Logon de usuário raiz
  * Autenticação de desafio/resposta
* Configure SSHD tooallow:
  * Somente logons de chave SSH
* Reiniciar o SSHD enquanto ainda estiver conectado
* Configuração do teste Olá novo SSHD

## <a name="introduction"></a>Introdução
[Definido por SSH](https://en.wikipedia.org/wiki/Secure_Shell)

SSHD é hello SSH servidor que executa o hello VM do Linux.  O SSH é um cliente executado em um shell no seu MacBook ou estação de trabalho Linux.  SSH é também protocolo hello usado toosecure e criptografar a comunicação de saudação entre sua estação de trabalho e hello VM do Linux.

Para este artigo é muito importante tookeep um logon tooyour VM Linux aberta para Olá todo percorrer.  Por esse motivo, será aberta dois terminais e SSH toohello VM do Linux de ambos.  Vamos usar Olá primeiro toomake terminal Olá alterações tooSSHDs arquivo de configuração e reiniciar o serviço SSHD hello.  Usaremos Olá tootest terminal segundo as alterações depois que o serviço Olá for reiniciado.  Como desabilitar o SSH senhas e contar estritamente com chaves SSH, se as chaves SSH não estão corretas e fechar Olá conexão toohello VM, hello VM será permanentemente bloqueado e não será capaz de toologin tooit solicitá-la toobe excluído e recriado.

## <a name="prerequisites"></a>Pré-requisitos
* [Criar chaves SSH no Linux e Mac para VMs do Linux no Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Conta do Azure
  * [assinatura de avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/)
  * [Portal do Azure](http://portal.azure.com)
* VM Linux em execução no Azure
* Par de chaves pública e privada SSH em `~/.ssh/`
* A chave pública SSH no `~/.ssh/authorized_keys` em Olá VM do Linux
* Direitos do sudo no hello VM
* Porta 22 aberta

## <a name="quick-commands"></a>Comandos rápidos
*Administradores de Linux experientes que querem apenas a versão TLDR Olá comece aqui.  Para todos os outros que quer Olá explicações detalhadas e passo a passo ignore esta seção.*

```bash
sudo vim /etc/ssh/sshd_config
```

Edite o arquivo de configuração de saudação da seguinte maneira:

```sh
# Change PasswordAuthentication toothis:
PasswordAuthentication no

# Change PubkeyAuthentication toothis:
PubkeyAuthentication yes

# Change PermitRootLogin toothis:
PermitRootLogin no

# Change ChallengeResponseAuthentication toothis:
ChallengeResponseAuthentication no
```

Reinicie o serviço SSHD hello. Em distribuições com base em Debian:

```bash
sudo service ssh restart
```

Em distribuições com base em Red Hat:

```bash
sudo service sshd restart
```

## <a name="detailed-walk-through"></a>Passo a passo detalhado
Logon toohello VM do Linux no terminal 1 (T1).  Logon toohello VM do Linux em 2 de terminal (T2).

Em T2, vamos arquivo de configuração tooedit Olá SSHD.  

```bash
sudo vim /etc/ssh/sshd_config
```

Aqui vamos Editar Olá configurações toodisable senhas e habilitar os logons de chave SSH.  Há muitas configurações neste arquivo que você deve pesquisar e alterar toomake Linux & SSH como segura, conforme necessário.

#### <a name="disable-password-logins"></a>Desabilitar logons de senha

```sh
# Change PasswordAuthentication toothis:
PasswordAuthentication no
```

#### <a name="enable-public-key-authentication"></a>Habilitar a autenticação de chave pública

```sh
# Change PubkeyAuthentication toothis:
PubkeyAuthentication yes
```

#### <a name="disable-root-login"></a>Desabilitar logon de raiz

```sh
# Change PermitRootLogin toothis:
PermitRootLogin no
```

#### <a name="disable-challenge-response-authentication"></a>Desabilitar autenticação de desafio/resposta
```sh
# Change ChallengeResponseAuthentication toothis:
ChallengeResponseAuthentication no
```

### <a name="restart-sshd"></a>Reiniciar o SSHD
No shell de saudação T1, verifique se que você ainda está conectado.  Isso é essencial para que você não seja bloqueado na VM se suas chaves SSH não estiverem corretas, uma vez que as senhas agora estão desabilitadas.  Se qualquer configuração estiverem incorreta em sua VM do Linux que você pode usar T1 toofix sshd_config que ainda serão registrados no e SSH irá manter uma conexão hello atividade durante a saudação service SSHD reinicie.

No T2, execute:

##### <a name="on-hello-debian-family"></a>Em Olá família Debian
```bash
sudo service ssh restart
```

##### <a name="on-hello-redhat-family"></a>Em Olá RedHat família
```bash
sudo service sshd restart
```

As senhas agora estão desabilitadas na sua VM, protegendo-a contra tentativas de logon de senha por força bruta.  Com apenas SSH chaves permitidas será capaz de toologin muito mais rápido e seguro.

