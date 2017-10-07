---
title: tooLinux aaaIntroduction no Azure | Microsoft Docs
description: "Saiba como usar máquinas virtuais Linux no Azure."
services: virtual-machines-linux
documentationcenter: python
author: szarkos
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: b13bf305-87bf-4df3-815e-e8f6337aa6ea
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: szark
ms.openlocfilehash: 3a931447ee23ce7000174ca314c3e10abc6b8e74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toolinux-on-azure"></a>Introdução tooLinux no Azure
Este tópico fornece uma visão geral de alguns aspectos do uso de máquinas virtuais Linux em Olá nuvem do Azure. Implantar uma máquina virtual Linux é um processo simples usando uma imagem da Galeria de saudação.

## <a name="authentication-usernames-passwords-and-ssh-keys"></a>Autenticação: nomes de usuário, senhas e chaves SSH.
Ao criar uma máquina virtual do Linux usando Olá portal do Azure, você será solicitado tooprovide qualquer nome de usuário e senha ou uma chave pública SSH. Olá, escolha um nome de usuário para implantar uma máquina virtual do Linux no Azure é toohello assunto seguinte restrição: nomes de contas do sistema (UID < 100) já está presente no hello máquina virtual não são permitidos, 'root' por exemplo.

* Veja [Criar uma máquina virtual que executa Linux](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Consulte [como tooUse SSH com Linux no Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="obtaining-superuser-privileges-using-sudo"></a>Obtendo privilégios de superusuário usando o `sudo`
conta de usuário de saudação que é especificada durante a implantação de instância de máquina virtual no Azure é uma conta privilegiada. Essa conta é configurada por hello Azure Linux Agent toobe tooelevate capaz de privilégios tooroot (conta de superusuário) usando Olá `sudo` utilitário. Depois de conectado usando essa conta de usuário, você será toorun capaz de comandos como raiz usando sintaxe de comando hello:

    # sudo <COMMAND>

Opcionalmente, você pode obter um shell de root usando **sudo -s**.

* Veja [Usando privilégios de raiz em máquinas virtuais Linux do Azure](use-root-privileges.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="firewall-configuration"></a>Configuração do firewall
O Azure fornece um filtro de pacote de entrada que restringe a conectividade tooports especificado no hello portal do Azure. Por padrão, hello apenas porta permitido é SSH. Você pode abrir as portas do acesso tooadditional na máquina virtual Linux Configurando pontos de extremidade no hello portal do Azure:

* Consulte: [como pontos de extremidade de tooSet tooa Máquina Virtual](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

imagens Linux Olá Olá Galeria do Azure não habilitam Olá *iptables* firewall por padrão. Se desejar, pode ser configurado firewall Olá tooprovide de filtragem adicionais.

## <a name="hostname-changes"></a>Alterações de nome do host
Quando você implanta inicialmente uma instância de uma imagem do Linux, será necessário tooprovide um nome de host para a máquina virtual de saudação. Depois de máquina virtual de saudação estiver em execução, o nome do host é publicado toohello servidores DNS de plataforma para que vários tooeach máquinas virtuais conectadas outros possa executar pesquisas de endereço IP usando nomes de host.

Se as alterações de nome de host são desejadas após a implantação de uma máquina virtual, use o comando de saudação

    # sudo hostname <newname>

Olá agente Linux do Azure inclui a funcionalidade de tooautomatically detectar essa alteração de nome adequadamente configurar Olá máquina virtual toopersist essa alteração e publicar essa alteração os servidores DNS toohello plataforma.

* [Guia do usuário do agente Linux para o Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="cloud-init"></a>Inicialização de nuvem
As imagens do **Ubuntu** e **CoreOS** utilizam inicialização de nuvem no Azure, que fornece recursos adicionais para inicializar uma máquina virtual.

* [Como tooInject de dados personalizado](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Dados personalizados e inicialização de nuvem no Microsoft Azure](https://azure.microsoft.com/blog/2014/04/21/custom-data-and-cloud-init-on-windows-azure/)
* [Criar partições de troca do Azure usando a nuvem Init](https://wiki.ubuntu.com/AzureSwapPartitions)
* [Como tooUse CoreOS no Azure](https://coreos.com/os/docs/latest/booting-on-azure.html)

## <a name="virtual-machine-image-capture"></a>Captura de imagem da máquina virtual
O Azure fornece o estado de saudação do hello capacidade toocapture de uma máquina virtual existente em uma imagem que posteriormente pode ser usado toodeploy instâncias de máquina virtual adicional. Olá agente Linux do Azure pode ser usado toorollback alguns Olá personalização que foi executada durante o processo de provisionamento de saudação. Você pode seguir as próximas etapas, Olá toocapture uma máquina virtual como uma imagem:

1. Executar **waagent-deprovision** tooundo provisionamento personalização. Ou **waagent-deprovision + user** toooptionally excluir conta de usuário de saudação especificada durante o provisionamento e todos os respectivos dados.
2. Desligado para baixo/desligar a máquina de virtual hello.
3. Clique em **capturar** em hello Azure Olá portal ou use PowerShell ou CLI ferramentas toocapture Olá VM como uma imagem.
   
   * Consulte: [como tooCapture tooUse uma máquina Virtual Linux como um modelo](classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

## <a name="attaching-disks"></a>Anexando discos
Cada máquina virtual tem um *disco de recursos* anexado. Porque os dados em um disco de recurso não podem ser duráveis entre as reinicializações, geralmente é usado por aplicativos e processos em execução na máquina virtual Olá transitório e **temporário** armazenamento de dados. Também é usado toostore Olá página ou permuta arquivos Olá sistema operacional.

No Linux, disco de recurso de saudação é normalmente gerenciado pelo Olá agente Linux do Azure e montado automaticamente muito**/mnt/Retention/ recurso** (ou **/mnt** no Ubuntu imagens).

> [!NOTE]
> Observe que esse disco de recurso Olá é um **temporário** disco e pode ser excluído e reformatado quando hello VM é reiniciada.
> 
> 

Disco de dados Olá no Linux pode ser chamado pelo kernel hello como `/dev/sdc`, e os usuários precisarão toopartition, formatar e montar esse recurso. Isso é abordado passo a passo no tutorial Olá: [como tooAttach uma máquina Virtual de tooa do disco de dados](../windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

* **Veja também:** [Configurar o Software RAID no Linux](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) & [Configurar LVM em uma VM do Linux no Azure](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

