---
title: aaaMigrate do Azure RemoteApp tooCitrix XenApp Essentials | Microsoft Docs
description: Como toomigrate do Azure RemoteApp tooCitrix XenApp Essentials
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 695a8165-3454-4855-8e21-f2eb2c61201b
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: aa3ce28bc5a86d5b1dd3408196d51935395f55c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-azure-remoteapp-toocitrix-xenapp-essentials"></a>Migrar do Azure RemoteApp tooCitrix XenApp Essentials

Se você usa o Azure RemoteApp e você desejar toomigrate tooCitrix XenApp Essentials, há alguns tookeep de pré-requisitos em mente. Leia primeiro o [Guia de implantação técnica passo a passo do Citrix XenApp Essentials](https://docs.citrix.com/content/dam/docs/en-us/citrix-cloud/downloads/xenapp-essentials-deployment-guide.pdf) da Citrix, bem como a sua [biblioteca técnica online](http://docs.citrix.com/en-us/citrix-cloud/xenapp-and-xendesktop-service/xenapp-essentials.html). 

## <a name="prerequisite-steps-for-migration"></a>Etapas de pré-requisito para a migração

1. Crie uma nova rede virtual ou determine a rede virtual do Azure no Azure Resource Manager na qual você implantará o Citrix XenApp Essentials. O Azure RemoteApp usa Olá portal clássico do Azure; Citrix XenApp Essentials só dá suporte ao Gerenciador de recursos do Azure.  
2. Verifique qual Olá a rede virtual selecionada tem o controlador de domínio de tooyour de acesso de rede porque Citrix só dá suporte a implantações híbridas. Se você estiver usando uma implantação de nuvem do Azure RemoteApp, certifique-se de que sua rede virtual tem o controlador de domínio do Active Directory de tooan de acesso de rede. Você também pode usar o Azure AD DS (Azure Active Directory Domain Services). 
3. Certifique-se de que Olá que DNS está configurado corretamente para a rede virtual do hello, para que essa associação de domínio foi bem-sucedido em sua primeira tentativa. Você pode criar uma máquina virtual (VM) na rede virtual de saudação selecionado e executar um tooverify de junção de domínio manual que Olá DNS e o ingresso no domínio funciona como esperado. Isso garante que você está Olá bem-sucedida a primeira vez que você implantar o Citrix XenApp Essentials. 
4. Se necessário, crie um emparelhamento de rede virtual entre uma rede virtual do Portal Clássico do Azure que você está usando com o Azure RemoteApp e a sua rede virtual do Azure Resource Manager. Esse processo emparelhamento funciona se redes Olá dois residem no hello mesma região. Se não tiverem, use redes virtuais do site a site VPN tooconnect Olá de rede. 
5. Se necessário, leia [como toomigrate dados dentro e fora do Azure RemoteApp](remoteapp-migrate.md). 
6. Atualizar seu saudação de tooinclude da imagem do Azure RemoteApp existente componente Citrix VDA (para obter instruções, consulte a documentação do Citrix Olá). 
7. Vá toohello Azure Marketplace e iniciar a implantação do Citrix XenApp Essentials.

## <a name="other-considerations"></a>Outras considerações

Esteja ciente das considerações adicionais a seguir quando você migra de saudação:
- O Citrix XenApp Essentials só oferece suporte a implantações híbridas. Em outras palavras, ele requer o controlador de domínio de tooa de acesso de rede no ingresso no domínio tooperform ordem. Se você estiver usando uma implantação de nuvem do Azure RemoteApp, usar o Azure AD DS ou certifique-se de que sua rede virtual tenha acesso tooActive diretório para ingresso no domínio. 
- toolearn como tooCitrix de dados de usuário toomove XenApp Essentials, consulte [como toomigrate dados dentro e fora do Azure RemoteApp](remoteapp-migrate.md). 
- O Citrix XenApp Essentials somente oferece suporte para contas do Active Directory. Ele não dá suporte a contas da Microsoft (tais como outlook.com, msn.com ou hotmail.com). 

## <a name="citrix-xenapp-essentials-billing"></a>Cobrança do Citrix XenApp Essentials

Para obter detalhes completos sobre preços, consulte Olá [perguntas frequentes sobre](https://www.citrix.com/global-partners/microsoft/resources/xenapp-essentials-faq.html#tab-30699) e [artigo de visão geral do Citrix](https://www.citrix.com/global-partners/microsoft/remote-app.html). Há três componentes de cobrança tooCitrix XenApp Essentials:

- Olá Citrix serviço custos adicionais, que é de US $12 por usuário por mês. Como todas as aquisições do Azure Marketplace, isso é toohello cobradas de pagamento associado à sua assinatura do Azure. Para clientes do EA (Contrato Enterprise), os créditos monetários do Azure não podem ser usados. 
- CALs (licenças de acesso para cliente) do RDS (Serviços de Dados Remotos). No momento, você pode comprar Olá taxa de acesso remoto que é fornecido com hello pagamento Citrix XenApp Essentials para US $6,25. Se você for um cliente EA, você pode usar toopay créditos monetários do Azure para isso. Se você quiser toouse as RDS CALs existentes, entre em contato conosco em [ arainfo@microsoft.com ](mailto:arainfo@microsoft.com), portanto, é possível aplicar este tooyour fatura. 
- Computação e armazenamento do Azure. Este é o custo de armazenamento do Azure hello e consumo de computação de VMs Olá consumida. Preste atenção aos preços quando seleciona seu tamanho e densidade de usuários da VM. Se você for um cliente EA, você pode usar toopay créditos monetários do Azure para isso.

Se você ainda tiver perguntas, você poderá:
- Envie-nos um email para [arainfo@microsoft.com](mailto:arainfo@microsoft.com).
- [Contate o suporte do Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). Iniciar o [abrir um caso de suporte do Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) toohelp com pré-requisito as etapas 1 a 5. Para obter as etapas 6 e 7, entre em contato com o Citrix abrindo um tíquete de suporte no portal de gerenciamento do Citrix hello. 
