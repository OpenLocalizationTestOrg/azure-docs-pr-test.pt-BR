---
title: aaaFrequently perguntado para VMs do Linux no Azure | Microsoft Docs
description: "Fornece toosome respostas das perguntas comuns sobre máquinas virtuais Linux criadas com o modelo do Gerenciador de recursos de saudação que hello."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-management
ms.assetid: 3648e09c-1115-4818-93c6-688d7a54a353
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: cynthn
ms.openlocfilehash: 0afd08123dddc408851065c46deedc3146dbec20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-question-about-linux-virtual-machines"></a>Perguntas frequentes sobre as Máquinas Virtuais Linux
Este artigo aborda algumas perguntas comuns sobre máquinas virtuais Linux criadas no Azure usando o modelo de implantação do Gerenciador de recursos de saudação. Para a versão do Windows hello deste tópico, consulte [perguntas frequentes sobre máquinas virtuais do Windows](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="what-can-i-run-on-an-azure-vm"></a>O que eu posso executar em uma VM do Azure?
Todos os assinantes podem executar software para servidores em uma máquina virtual do Azure. Para saber mais, veja [Linux em distribuições endossadas pelo Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a>Quanto armazenamento eu posso usar com uma máquina virtual?
Cada disco de dados pode ser até too1 TB. número de saudação de discos de dados, que você pode usar depende Olá tamanho da saudação máquina virtual. Para obter detalhes, consulte [Tamanhos das máquinas virtuais](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Uma conta de armazenamento do Azure fornece armazenamento para o disco do sistema operacional hello e eventuais discos de dados. Cada disco é um arquivo .vhd armazenado como um blob de páginas. Para obter detalhes sobre preços, veja [Detalhes de preços de armazenamento](https://azure.microsoft.com/pricing/details/storage/).

## <a name="how-can-i-access-my-virtual-machine"></a>Como posso acessar minha máquina virtual?
Estabelece um toolog de conexão remota na máquina virtual de toohello, usando Secure Shell (SSH). Consulte as instruções de saudação em como tooconnect [do Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [do Linux e Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Por padrão, o SSH permite um máximo de 10 conexões simultâneas. Você pode aumentar esse número editando o arquivo de configuração de saudação.

Se você estiver tendo problemas, confira [Solucionar problemas de conexões SSH (Secure Shell)](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="can-i-use-hello-temporary-disk-devsdb1-toostore-data"></a>É possível usar dados de toostore saudação em disco temporário (/dev/sdb1)?
Não use dados de toostore saudação em disco temporário (/dev/sdb1). Ele existe somente para armazenamento temporário. Você corre o risco de perder dados que não podem ser recuperados.

## <a name="can-i-copy-or-clone-an-existing-azure-vm"></a>Posso copiar ou clonar uma VM do Azure existente?
Sim. Para obter instruções, consulte [como toocreate uma cópia de uma máquina virtual do Linux no hello modelo de implantação do Gerenciador de recursos](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="why-am-i-not-seeing-canada-central-and-canada-east-regions-through-azure-resource-manager"></a>Por que não vejo as regiões Central e Leste do Canadá por meio do Azure Resource Manager?
Olá duas novas regiões da Central do Canadá e Leste do Canadá não são automaticamente registrados para a criação de máquina virtual de assinaturas do Azure existentes. Esse registro é feito automaticamente quando uma máquina virtual é implantada por meio de Olá tooany portal do Azure outra região usando o Gerenciador de recursos do Azure. Depois de uma máquina virtual é implantada tooany outra região do Azure, regiões novo Olá devem estar disponíveis para máquinas de virtuais subsequentes.

## <a name="can-i-add-a-nic-toomy-vm-after-its-created"></a>Adicionar um toomy NIC VM depois que ela é criada?
Sim, agora isso é possível. Olá VM primeiro necessidades toobe parada desalocada. Em seguida, você pode adicionar ou remover uma NIC (a menos que ele seja Olá última NIC Olá VM). 

## <a name="are-there-any-computer-name-requirements"></a>Há algum requisito de nome do computador?
Sim. nome do computador Olá pode ter no máximo 64 caracteres de comprimento. Confira [Regras e restrições de convenções de nomenclatura](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obter mais informações sobre como nomear recursos.

## <a name="are-there-any-resource-group-name-requirements"></a>Há algum requisito de nome de grupo de recursos?
Sim. nome do grupo de recursos Olá pode ter no máximo 90 caracteres de comprimento. Confira [Regras e restrições de convenções de nomenclatura](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obter mais informações sobre grupos de recursos.

## <a name="what-are-hello-username-requirements-when-creating-a-vm"></a>Quais são os requisitos de nome de usuário de saudação ao criar uma máquina virtual?
Os nomes de usuário devem ter de 1 a 64 caracteres.

Olá, nomes de usuário a seguir não é permitido:

<table>
    <tr>
        <td style="text-align:center">administrator </td><td style="text-align:center"> administrador </td><td style="text-align:center"> usuário </td><td style="text-align:center"> user1</td>
    </tr>
    <tr>
        <td style="text-align:center">test </td><td style="text-align:center"> user2 </td><td style="text-align:center"> test1 </td><td style="text-align:center"> user3</td>
    </tr>
    <tr>
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
Senhas devem ter de 6 a 72 caracteres e atendem 3 fora Olá seguindo os requisitos de complexidade de 4:

* Ter caracteres minúsculos
* Tem caracteres maiúsculos
* Tem um dígito
* Tem um caractere especial (Correspondência de regex [\W_])

Olá seguindo as senhas não é permitido:

<table>
    <tr>
        <td style="text-align:center">abc@123</td>
        <td style="text-align:center">P@$$w0rd</td>
        <td style="text-align:center">P@ssw0rd</td>
        <td style="text-align:center">P@ssword123</td>
        <td style="text-align:center">Pa$$word</td>
    </tr>
    <tr>
        <td style="text-align:center">pass@word1</td>
        <td style="text-align:center">Password!</td>
        <td style="text-align:center">Password1</td>
        <td style="text-align:center">Password22</td>
        <td style="text-align:center">iloveyou!</td>
    </tr>
</table>
