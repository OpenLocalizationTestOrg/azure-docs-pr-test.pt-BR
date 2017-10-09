---
title: Perguntas frequentes sobre criptografia de disco de aaaAzure | Microsoft Docs
description: Este artigo fornece respostas toofrequently perguntado para o Microsoft Azure disco criptografia para Windows e Linux VMs de IaaS.
services: security
documentationcenter: na
author: deventiwari
manager: avibm
editor: yuridio
ms.assetid: 7188da52-5540-421d-bf45-d124dee74979
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: devtiw
ms.openlocfilehash: 17f084628ba4ef22e9d37dd3052ef10f8eb2cd7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-frequently-asked-questions-faq"></a>FAQ (perguntas frequentes) sobre o Azure Disk Encryption

Estas Perguntas Frequentes respondem a perguntas sobre o Azure Disk Encryption para VMs IaaS Windows e Linux. Para saber mais sobre esse serviço, leia [Azure Disk Encryption para VMs IaaS Windows e Linux](https://docs.microsoft.com/azure/security/azure-security-disk-encryption).

## <a name="general-questions"></a>Perguntas gerais
**P.** Qual é a região do Azure Disk Encryption em GA?

**R:** O Azure Disk Encryption para VMs IaaS Windows e Linux está disponível em GA em todas as regiões públicas do Azure.

**P:** Quais experiências de usuário estão disponíveis com o Azure Disk Encryption?

**R:** O GA do Azure Disk Encryption dá suporte a modelos do Azure Resource Manager, ao Azure PowerShell e à CLI do Azure. Isso dá uma grande flexibilidade, pois você tem três opções diferentes para habilitar a criptografia de disco para as VMs IaaS. Mais detalhes sobre a experiência do usuário hello e orientações passo a passo está disponível em cenários de implantação de criptografia de disco do Azure de saudação e experiências.

**P:** Quanto custa o Azure Disk Encryption?

**R:** Não são cobradas taxas para a criptografia de discos de VM com o Azure Disk Encryption.

**P:** Em quais camadas de máquina virtual é possível usar o Azure Disk Encryption?

**R:** O Azure Disk Encryption está disponível somente em máquinas virtuais de camada padrão, incluindo [A, D, DS, G, GS, F](https://azure.microsoft.com/pricing/details/virtual-machines/) e assim por diante. VMs série IaaS, incluindo VMs com o armazenamento premium. Ele não está disponível para máquinas virtuais na Camada básica.

**P:** Quais distribuições do Linux têm suporte do Azure Disk Encryption?

**R:** criptografia de disco do Azure tem suporte em Olá versões e distribuições do Linux server a seguir:

| Distribuição Linux | Versão | Tipo de Volume com Suporte para Criptografia|
| --- | --- |--- |
| Ubuntu | 16.04-LTS-DIÁRIO | SO e Disco de Dados |
| Ubuntu | 14.04.5-LTS-DIÁRIO | SO e Disco de Dados |
| RHEL | 7.3 | SO e Disco de Dados |
| RHEL | 7,2 | SO e Disco de Dados |
| RHEL | 6,8 | SO e Disco de Dados |
| RHEL | 6.7 | Disco de dados |
| CentOS | 7.3 | SO e Disco de Dados |
| CentOS | 7.2n | SO e Disco de Dados |
| CentOS | 6,8 | SO e Disco de Dados |
| CentOS | 7.1 | Disco de dados |
| CentOS | 7.0 | Disco de dados |
| CentOS | 6.7 | Disco de dados |
| CentOS | 6.6 | Disco de dados |
| CentOS | 6.5 | Disco de dados |
| openSUSE | 13.2 | Disco de dados |
| SLES | 12 SP1 | Disco de dados |
| SLES | Prioridade: 12-SP1 | Disco de dados |
| SLES | HPC 12 | Disco de dados |
| SLES | Prioridade: 11-SP4 | Disco de dados |
| SLES | 11 SP4 | Disco de dados |

**P:** Como posso começar a usar o Azure Disk Encryption?

**R:** os clientes podem aprender como tooget iniciada leitura Olá white paper de criptografia de disco do Azure localizado [aqui](https://docs.microsoft.com/azure/security/azure-security-disk-encryption)

**P:** Posso criptografar volumes de dados e de inicialização com o Azure Disk Encryption?

**R:** Sim, você pode criptografar volumes de inicialização e de dados para VMs IaaS Windows e Linux. Para VMs do Windows, você não pode criptografar dados saudação sem primeiro encrpting Olá volume do sistema operacional. Para VMs do Linux, você pode criptografar o volume de dados de saudação sem encryptinng Olá volume do sistema operacional pela primeira vez. Depois que você criptografou o volume de saudação SO para Liux, desabilitando a criptografia em um volume do sistema operacional para as VMs de IaaS Linux não tem suporte

**P:** O Azure Disk Encryption permite o recurso BYOK (“bring your own key”)?

**R:** Sim, você pode fornecer suas próprias chaves de criptografia de chave. Essas chaves são protegidas no cofre de chaves do Azure, que é o repositório de chaves Olá para criptografia de disco do Azure. Para obter mais detalhes sobre a chave de criptografia de chave Olá dar suporte a cenários, consulte experiências e cenários de implantação de criptografia de disco do Azure Olá

**P:** Posso usar uma chave de criptografia de chave criada pelo Azure?

**R:** Sim, você pode usar a chave de criptografia de chave de toogenerate de Cofre de chave do Azure para uso de criptografia de disco do Azure. Essas chaves são protegidas no cofre de chaves do Azure, que é o repositório de chaves Olá para criptografia de disco do Azure. Para obter mais detalhes sobre a chave de criptografia de chave Olá dar suporte a cenários, consulte experiências e cenários de implantação de criptografia de disco do Azure Olá

**P:** posso usar as chaves de criptografia Olá de serviço/HSM toosafeguard gerenciamento de chaves local?

**R:** você não pode usar chaves de criptografia de Olá Olá local gerenciamento de chaves toosafeguard de serviço/HSM com criptografia de disco do Azure. Você só pode usar chaves de criptografia de Olá Olá Cofre de chaves do Azure serviço toosafeguard. Para obter mais detalhes sobre a chave de criptografia de chave Olá dar suporte a cenários, consulte experiências e cenários de implantação de criptografia de disco do Azure Olá

**P:** quais são criptografia de disco do Azure Olá pré-requisitos tooconfigure?

**R:** Olá disco Azure criptografia pré-requisito PowerShell toocreate AAD aplicativo de script, criar novo cofre de chaves ou Cofre de chave existente para o disco criptografia acesso tooenable criptografia e proteger segredos e a chave de instalação.  Para obter mais detalhes sobre a chave de criptografia de chave Olá dar suporte a cenários, consulte pré-requisitos de criptografia de disco do Azure hello e cenários de implantação e experiências

**P:** onde obter mais informações sobre como toouse do PowerShell para configurar a criptografia de disco do Azure?

**R:** Temos alguns ótimos artigos sobre como executar tarefas básicas do Azure Disk Encryption e cenários mais avançados. Para tarefas básicas de Olá, confira explorar [criptografia de disco do Azure com o Azure PowerShell - parte 1](https://blogs.msdn.microsoft.com/azuresecurity/2015/11/16/explore-azure-disk-encryption-with-azure-powershell/). Para cenários mais avançados, confira Explorar [Azure Disk Encryption com o Azure PowerShell - Parte 2](https://blogs.msdn.microsoft.com/azuresecurity/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2/)

**P:** Qual versão do Azure PowerShell tem suporte do Azure Disk Encryption?

**R:** Use Olá última versão do SDK do Azure PowerShell versão tooconfigure criptografia de disco do Azure. Baixar a versão mais recente de saudação do [Azure PowerShell](https://github.com/Azure/azure-powershell/releases). NÃO há suporte para o Azure Disk Encryption pelo SDK do Azure versão 1.1.0.

> [!NOTE]
> Olá extensão de visualização de criptografia de disco Linux Azure foi preterido. Para obter detalhes, consulte toodocumentation [aqui](https://blogs.msdn.microsoft.com/azuresecurity/2017/07/12/deprecating-azure-disk-encryption-preview-extension-for-linux-iaas-vms/)

**P:** Posso aplicar a criptografia de disco do Azure à minha imagem personalizada do Linux?

**R:** Você não pode aplicar a criptografia de disco do Azure à imagem personalizada do Linux. Há suporte para apenas imagens Linux da Galeria Olá para distribuições Olá suportada destacadas acima. Não há suporte para imagens personalizadas do Linux no momento

**P:** pode aplicar atualizações tooa Linux Red Hat VM usando atualização Yum?

**R:** Sim, você pode executar a atualização e/ou usar patch em uma VM Red Hat Linnux seguindo as orientações documentadas [aqui](https://blogs.msdn.microsoft.com/azuresecurity/2017/07/13/applying-updates-to-a-encrypted-azure-iaas-red-hat-vm-using-yum-update/)

**P:** onde posso ir tooask pergunta ou fornecer comentários

**R:** você pode fornecer faça perguntas ou comentários no Fórum de criptografia de disco do Azure Olá [aqui](https://social.msdn.microsoft.com/Forums/home?forum=AzureDiskEncryption)

## <a name="see-also"></a>Consulte também
Neste documento, você aprendeu mais hello mais frequentes perguntas relacionadas tooAzure criptografia de disco para obter mais informações sobre esse serviço e a capacidade de ler:

- [Aplicar a criptografia de disco na Central de Segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-apply-disk-encryption)
- [Criptografar uma Máquina Virtual do Azure](https://docs.microsoft.com/azure/security-center/security-center-disk-encryption)
- [Criptografia de dados em repouso no Azure](https://docs.microsoft.com/azure/security/azure-security-encryption-atrest)
