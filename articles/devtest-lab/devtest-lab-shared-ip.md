---
title: "aaaUnderstand compartilhado endereços IP no Azure DevTest Labs | Microsoft Docs"
description: "Saiba como o Azure DevTest Labs usa a compartilhado IP endereços toominimize Olá pública IP endereços necessário tooaccess sua máquinas virtuais do laboratório."
services: devtest-lab
documentationcenter: na
author: camsoper
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: casoper
ms.openlocfilehash: 8756410117a9d550d567d372174bf1ea96703c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-shared-ip-addresses-in-azure-devtest-labs"></a>Entender os endereços IP compartilhados no Azure DevTest Labs

Laboratório de permite DevTest Labs Azure VMs compartilhamento Olá mesmo pública toominimize Olá número do endereço IP do público tooaccess necessário endereços IP laboratório VMs individual.  Este artigo descreve como funcionam os IPs compartilhados e suas opções de configuração relacionadas.

## <a name="shared-ip-setting"></a>Configuração de IP de compartilhado

Quando você cria um laboratório, ele reside em uma sub-rede de uma rede virtual.  Por padrão, essa sub-rede é criada com **habilitar compartilhada IP público** definido muito*Sim*.  Essa configuração cria um endereço IP público sub-rede inteira hello.  Para obter mais informações sobre como configurar redes virtuais e sub-redes, consulte [Configurar uma rede virtual no Azure DevTest Labs](devtest-lab-configure-vnet.md).

![Nova sub-rede do laboratório](media/devtest-lab-shared-ip/lab-subnet.png)

Em laboratórios existentes, você pode habilitar essa opção selecionando **Políticas e configurações > Redes Virtuais**. Em seguida, selecione uma rede virtual da lista de saudação e escolha **habilitar compartilhado IP público** para uma sub-rede selecionada. Você também pode desabilitar essa opção no laboratório de nenhuma se você não quiser tooshare um endereço IP público em máquinas virtuais do laboratório.

Todas as máquinas virtuais criados no toousing de padrão neste laboratório um IP compartilhado.  Ao criar hello VM, essa configuração pode ser observada no hello **configurações avançadas** folha sob **configuração do endereço IP**.

![Nova VM](media/devtest-lab-shared-ip/new-vm.png)

- **Compartilhado:** todas as VMs criadas como **Compartilhadas** são colocadas em um grupo de recursos (RG). Um único endereço IP é atribuído para que RG e todas as VMs em Olá RG usarão esse endereço IP.
- **Público:** cada uma das VMs que você cria tem seu próprio endereço IP e é criada em seu próprio grupo de recursos.
- **Privado:** todas as VMs que você criar usarão um endereço IP privado. Você não será capaz de tooconnect toothis VM diretamente da saudação internet com área de trabalho remota.

Sempre que uma VM com IP compartilhado habilitado é adicionada a sub-rede toohello, DevTest Labs automaticamente adiciona o balanceador de carga Olá VM tooa e atribui um número de porta TCP no endereço IP público de hello, encaminhamento toohello porta RDP em Olá VM.  

## <a name="using-hello-shared-ip"></a>Usando Olá compartilhado de IP

- **Os usuários do Linux:** SSH toohello VM usando o endereço IP de saudação ou nome de domínio totalmente qualificado, seguido por dois-pontos, seguido pela porta hello. Por exemplo, na imagem de saudação abaixo, Olá RDP endereços toohello tooconnect VM é `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.

  ![Exemplo de VM](media/devtest-lab-shared-ip/vm-info.png)

- **Os usuários do Windows:** Olá selecione **conectar** botão Olá toodownload portal do Azure um arquivo RDP pré-configurado e acessar Olá VM.

## <a name="next-steps"></a>Próximas etapas

* [Definir políticas de laboratório no Azure DevTest Labs](devtest-lab-set-lab-policy.md)
* [Configurar uma rede virtual no Azure DevTest Labs](devtest-lab-configure-vnet.md)





