---
title: "aaaFAQ sobre máquinas virtuais do Windows no Azure | Microsoft Docs"
description: "Fornece toosome respostas das perguntas comuns sobre máquinas virtuais do Windows criadas com o modelo do Gerenciador de recursos de saudação que hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-management
ms.assetid: 757da816-a050-4889-a010-6f75d7978eb7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: cynthn
ms.openlocfilehash: ee366a04bda347ce2be07bde4fc6bad306cc1da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-question-about-windows-virtual-machines"></a>Perguntas frequentes sobre as Máquinas Virtuais do Windows
Este artigo aborda algumas perguntas comuns sobre máquinas virtuais do Windows criadas no Azure usando o modelo de implantação do Gerenciador de recursos de saudação. Para a versão do Linux Olá deste tópico, consulte [perguntas frequentes sobre máquinas virtuais do Linux](../linux/faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="what-can-i-run-on-an-azure-vm"></a>O que eu posso executar em uma VM do Azure?
Todos os assinantes podem executar software para servidores em uma máquina virtual do Azure. Para obter informações sobre a política de suporte de saudação do software de servidor Microsoft em execução no Azure, consulte [suporte de software de servidor Microsoft para máquinas virtuais do Azure](https://support.microsoft.com/kb/2721672)

Determinadas versões do Windows 7, Windows 8.1 e Windows 10 são tooMSDN disponíveis do Azure beneficie assinantes e assinantes do MSDN de desenvolvimento e teste pré-pago, para tarefas de desenvolvimento e teste. Para obter detalhes, incluindo instruções e limitações, veja [Imagens do Windows Client para assinantes do MSDN](http://azure.microsoft.com/blog/2014/05/29/windows-client-images-on-azure/). 

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a>Quanto armazenamento eu posso usar com uma máquina virtual?
Cada disco de dados pode ser até too1 TB. número de saudação de discos de dados, que você pode usar depende Olá tamanho da saudação máquina virtual. Para obter detalhes, consulte [Tamanhos das máquinas virtuais](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Os discos do Azure gerenciados são Olá disco novo e recomendadas ofertas de armazenamento para uso com as máquinas virtuais do Azure para armazenamento persistente de dados. Em cada Máquina Virtual, é possível usar vários Managed Disks. Os Managed Disks oferecem dois tipos de opções de armazenamento durável: Managed Disks Premium e Standard. Para obter informações sobre preço, consulte [Preços do Managed Disks](https://azure.microsoft.com/pricing/details/managed-disks).

Contas de armazenamento do Azure também podem fornecer armazenamento para o disco do sistema operacional hello e eventuais discos de dados. Cada disco é um arquivo .vhd armazenado como um blob de páginas. Para obter detalhes sobre preços, veja [Detalhes de preços de armazenamento](https://azure.microsoft.com/pricing/details/storage/).

## <a name="how-can-i-access-my-virtual-machine"></a>Como posso acessar minha máquina virtual?
Estabeleça uma conexão remota usando o protocolo RDP (Conexão de Área de Trabalho Remota) para uma VM do Windows. Para obter instruções, consulte [como tooconnect e logon tooan virtuais do Azure do computador que executa o Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Um máximo de duas conexões simultâneas têm suporte, a menos que o servidor de saudação é configurado como um host de sessão de serviços de área de trabalho remota.  

Se você estiver tendo problemas com a área de trabalho remota, consulte [tooa conexões de solucionar problemas de área de trabalho remota baseado no Windows Azure Virtual Machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Se você estiver familiarizado com o Hyper-V, você poderá ser procurando um tooVMConnect semelhante de ferramenta. O Azure não oferece uma ferramenta semelhante, porque não há suporte para acessar o console tooa computador virtual.

## <a name="can-i-use-hello-temporary-disk-hello-d-drive-by-default-toostore-data"></a>É possível usar dados de toostore saudação em disco temporário (Olá unidade d: por padrão)?
Não use dados de toostore saudação em disco temporário. Ele é apenas um armazenamento temporário, você se arriscaria a perder dados que não podem ser recuperados. Perda de dados pode ocorrer quando a máquina virtual de saudação move tooa outro host. Redimensionamento de uma máquina virtual, atualizar host hello, ou uma falha de hardware no host de saudação é alguns dos motivos Olá que pode mover uma máquina virtual.

Se você tiver um aplicativo que necessite de letra da unidade toouse Olá d:, você pode reatribuir letras de unidade para que hello em disco temporário Use algo diferente de d:. Para obter instruções, consulte [alterar a letra da unidade saudação do disco temporário do Windows hello](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).


## <a name="how-can-i-change-hello-drive-letter-of-hello-temporary-disk"></a>Como alterar a letra da unidade de saudação do disco temporário Olá?
Você pode alterar a letra de unidade de saudação pelo arquivo de página móvel hello e reatribuindo letras de unidade, mas você precisa toomake-se de que você Olá etapas em uma ordem específica. Para obter instruções, consulte [alterar a letra da unidade saudação do disco temporário do Windows hello](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="can-i-add-an-existing-vm-tooan-availability-set"></a>É possível adicionar um conjunto de disponibilidade de tooan VM existente?
Não. Se você quiser que sua parte de toobe VM de um conjunto de disponibilidade, você precisa toocreate Olá VM no conjunto de saudação. Atualmente não há um tooadd de maneira uma disponibilidade de tooan VM definida depois que ela foi criada.

## <a name="can-i-upload-a-virtual-machine-tooazure"></a>Posso carregar tooAzure uma máquina virtual?
Sim. Para obter instruções, consulte [migrando VMs tooAzure local](on-prem-to-azure.md).

## <a name="can-i-resize-hello-os-disk"></a>Posso redimensionar um disco do sistema operacional Olá?
Sim. Para obter instruções, consulte [como tooexpand Olá unidade do sistema operacional de uma máquina Virtual em um grupo de recursos do Azure](expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="can-i-copy-or-clone-an-existing-azure-vm"></a>Posso copiar ou clonar uma VM do Azure existente?
Sim. Usando imagens gerenciadas, você pode criar uma imagem de uma máquina virtual e, em seguida, usar Olá imagem toobuild várias novas VMs. Para obter instruções, consulte [Criar uma imagem personalizada de uma VM](tutorial-custom-images.md).

## <a name="why-am-i-not-seeing-canada-central-and-canada-east-regions-through-azure-resource-manager"></a>Por que não vejo as regiões Central e Leste do Canadá por meio do Azure Resource Manager?

Olá duas novas regiões da Central do Canadá e Leste do Canadá não são automaticamente registrados para a criação de máquina virtual de assinaturas do Azure existentes. Esse registro é feito automaticamente quando uma máquina virtual é implantada por meio de Olá tooany portal do Azure outra região usando o Gerenciador de recursos do Azure. Depois de uma máquina virtual é implantada tooany outra região do Azure, regiões novo Olá devem estar disponíveis para máquinas de virtuais subsequentes.

## <a name="does-azure-support-linux-vms"></a>O Azure oferece suporte a VMs Linux?
Sim. tooquickly criar tootry uma VM do Linux-out, consulte [criar uma VM do Linux no Azure usando o Portal de saudação](../linux/quick-create-portal.md).

## <a name="can-i-add-a-nic-toomy-vm-after-its-created"></a>Adicionar um toomy NIC VM depois que ela é criada?
Sim, agora isso é possível. Olá VM primeiro necessidades toobe parada desalocada. Em seguida, você pode adicionar ou remover uma NIC (a menos que ele seja Olá última NIC Olá VM). 

## <a name="are-there-any-computer-name-requirements"></a>Há algum requisito de nome do computador?
Sim. nome do computador Olá pode ter no máximo 15 caracteres de comprimento. Confira [Regras e restrições de convenções de nomenclatura](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para obter mais informações sobre como nomear recursos.

## <a name="are-there-any-resource-group-name-requirements"></a>Há algum requisito de nome de grupo de recursos?
Sim. nome do grupo de recursos Olá pode ter no máximo 90 caracteres de comprimento. Confira [Regras e restrições de convenções de nomenclatura](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para obter mais informações sobre grupos de recursos.

## <a name="what-are-hello-username-requirements-when-creating-a-vm"></a>Quais são os requisitos de nome de usuário de saudação ao criar uma máquina virtual?

Nomes de usuário podem ter, no máximo, 20 caracteres e não podem terminar com um ponto (“.”). 


Olá, nomes de usuário a seguir não é permitido:
<table>
    <tr>
        <td style="text-align:center">administrator </td><td style="text-align:center"> administrador </td><td style="text-align:center"> usuário </td><td style="text-align:center"> user1</td>
    </tr>
    <tr>
        <td style="text-align:center">test </td><td style="text-align:center"> user2 </td><td style="text-align:center"> test1 </td><td style="text-align:center"> user3</td>
    </tr>    <tr>
        <td style="text-align:center">admin1 </td><td style="text-align:center"> 1 </td><td style="text-align:center"> 123 </td><td style="text-align:center"> a</td>
    </tr>
    <tr>
        <td style="text-align:center">actuser  </td><td style="text-align:center"> adm </td><td style="text-align:center"> admin2 </td><td style="text-align:center"> aspnet</td>
    </tr>
    <tr>
        <td style="text-align:center">backup </td><td style="text-align:center"> console </td><td style="text-align:center"> david </td><td style="text-align:center"> guest</td>
    </tr>
    <tr>
        <td style="text-align:center">julio </td><td style="text-align:center"> proprietário </td><td style="text-align:center"> root </td><td style="text-align:center"> server</td>
    </tr>
    <tr>
        <td style="text-align:center">sql </td><td style="text-align:center"> suporte </td><td style="text-align:center"> support_388945a0 </td><td style="text-align:center"> sys</td>
    </tr>
    <tr>
        <td style="text-align:center">test2 </td><td style="text-align:center"> test3 </td><td style="text-align:center"> user4 </td><td style="text-align:center"> user5</td>
    </tr>
</table>

## <a name="what-are-hello-password-requirements-when-creating-a-vm"></a>Quais são os requisitos de senha Olá durante a criação de uma máquina virtual?
As senhas devem ser 12 123 caracteres de comprimento e atender 3 fora Olá seguindo os requisitos de complexidade de 4:

* Ter caracteres minúsculos
* Tem caracteres maiúsculos
* Tem um dígito
* Tem um caractere especial (Correspondência de regex [\W_])

Olá seguindo as senhas não é permitido:

<table>
    <tr>
        <td>abc@123 </td>
        <td>P@$$w0rd </td>
        <td>P@ssw0rd </td>
        <td>P@ssword123 </td>
        <td>Pa$$word </td>
    </tr>
    <tr>
        <td>pass@word1 </td>
        <td>Password! </td>
        <td>Password1 </td>
        <td>Password22 </td>
        <td>iloveyou! </td>
    </tr>
</table>
