---
title: "recursos de segurança aaaAzure usados com máquinas virtuais do Azure | Microsoft Docs"
description: " Uma visão geral Olá principal do Azure dos recursos de segurança que podem ser usados com máquinas virtuais do Azure. Dê VMs do Azure Olá flexibilidade da virtualização sem a necessidade de toobuy e manter Olá hardware físico que executa Olá VM. "
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 467b2c83-0352-4e9d-9788-c77fb400fe54
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/04/2017
ms.author: terrylan
ms.openlocfilehash: 1a1b9f02bd82a2655f4e2e5d9f9ce7a6671f63fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-security-overview"></a>Visão geral de segurança de máquinas virtuais do Azure
As máquinas virtuais do Azure permitem que você implante uma ampla gama de soluções de computação de forma ágil. Com suporte para o Microsoft Windows, Linux, Microsoft SQL Server, Oracle, IBM, SAP e Serviços BizTalk do Azure, você pode implantar qualquer carga de trabalho e qualquer linguagem em praticamente qualquer sistema operacional.

Fornece uma máquina virtual do Azure Olá flexibilidade da virtualização sem a necessidade de toobuy e manter o hardware físico Olá que executa a máquina virtual de saudação.  Você pode criar e implantar aplicativos com garantia de saudação que seus dados sejam protegidos e seguros em nossos datacenters altamente seguros.

Com o Azure, você pode compilar soluções compatíveis, com segurança avançada, que:

* Protegem suas máquinas virtuais contra vírus e malwares
* Criptografam seus dados confidenciais
* Protegem o tráfego de rede
* Identificam e detectam ameaças
* Atendem os requisitos de conformidade

Olá objetivo deste artigo é tooprovide uma visão geral dos recursos de segurança do Azure do hello principais que podem ser usados com máquinas virtuais. Nós também fornecemos links tooarticles que forneça os detalhes de cada recurso para saber mais.  

Olá core Máquina Virtual do Azure segurança recursos toobe abordadas neste artigo:

* Antimalware
* Módulos de segurança de hardware
* Criptografia de disco da máquina virtual
* Backup de máquinas virtuais
* Azure Site Recovery
* Rede Virtual
* Gerenciamento de política de segurança e emissão de relatórios
* Conformidade

## <a name="antimalware"></a>Antimalware
Com o Azure, você pode usar o software antimalware de fornecedores de segurança, como Microsoft, Symantec, Trend Micro e Kaspersky tooprotect suas máquinas virtuais de arquivos mal-intencionados, adware e outras ameaças. Consulte Olá Saiba mais uma seção abaixo toofind artigos sobre soluções de parceiros.

O Microsoft Antimalware para Serviços de Nuvem e Máquinas Virtuais do Azure é uma funcionalidade de proteção em tempo real que ajuda a identificar e remover vírus, spyware e outros softwares mal-intencionados.  O Antimalware da Microsoft fornece alertas configuráveis conhecido tooinstall de tentativas de software mal-intencionado ou indesejado em si ou executar em seus sistemas do Azure.

O Antimalware da Microsoft é uma solução de agente único para aplicativos e ambientes de locatário, toorun projetado no plano de fundo de saudação sem intervenção humana. Você pode implantar proteção com base nas necessidades de saudação de suas cargas de trabalho do aplicativo, com o básico seguro por padrão ou avançadas de configuração personalizada, incluindo o monitoramento de antimalware.

Quando você implanta e habilitar o Antimalware da Microsoft, Olá principais recursos a seguir está disponível:

* Proteção em tempo real - atividade de monitores em serviços de nuvem e em máquinas virtuais toodetect e bloquear a execução de malware.
* A verificação agendada - executa periodicamente destino varredura toodetect tipos de malware, inclusive ativamente programas em execução.
* Remediação de Malware: atua automaticamente sobre o malware detectado, por exemplo, excluindo ou colocando arquivos mal-intencionados em quarentena e limpando entradas de Registro mal-intencionadas.
* Assinatura - automaticamente instala hello mais recente assinaturas (definições de vírus) tooensure proteção está atualizada em uma frequência predeterminada.
* Atualizações de mecanismo antimalware – automaticamente atualizações Olá mecanismo Antimalware da Microsoft.
* Atualizações de plataforma de antimalware – automaticamente atualizações Olá plataforma Antimalware da Microsoft.
* Proteção ativa - relatórios tooAzure telemetria metadados sobre ameaças detectadas e recursos suspeitas tooensure rápida resposta e permite assinatura síncrona em tempo real entrega por meio de saudação Microsoft Active Protection System (MAPS).
* Exemplos de relatórios - fornece e exemplos de relatórios toohelp de serviço de Antimalware da Microsoft toohello refinar serviço hello e solução de problemas de ativação.
* Exclusões – permite que aplicativos e tooconfigure de administradores de serviço certos arquivos, processos e unidades tooexclude da proteção e verificação por outros motivos de desempenho e.
* Coleta de eventos de antimalware - registra a integridade do serviço antimalware hello, atividades suspeitas e ações de correção realizadas no log de eventos do sistema operacional hello e coleta-los na conta de armazenamento do Azure do cliente hello.

Saiba mais: toolearn mais sobre tooprotect de software antimalware as máquinas virtuais, consulte:

* [Microsoft Antimalware para Serviços de Nuvem do Azure e máquinas virtuais](azure-security-antimalware.md)
* [Implantando soluções antimalware em máquinas virtuais do Azure](https://azure.microsoft.com/blog/deploying-antimalware-solutions-on-azure-virtual-machines/)
* [Como tooinstall e configurar o Trend Micro Deep Security como um serviço em uma VM do Windows](../virtual-machines/windows/classic/install-trend.md)
* [Como tooinstall e configurar o Symantec Endpoint Protection em uma VM do Windows](../virtual-machines/windows/classic/install-symantec.md)
* [Soluções de segurança no hello Azure Marketplace](https://azure.microsoft.com/marketplace/?term=security)

## <a name="hardware-security-module"></a>Módulos de segurança de hardware
As proteções de criptografia e autenticação podem ser aprimoradas, melhorando a segurança da chave. Você pode simplificar o gerenciamento de saudação e segurança de chaves e segredos críticos, armazenando-os no cofre de chaves do Azure. Cofre de chaves fornece Olá opção toostore suas chaves nos padrões do hardware segurança tooFIPS certificada de HSMs (módulos) 140-2 nível 2. Suas chaves de criptografia do SQL Server para backup ou [Transparent Data Encryption](https://msdn.microsoft.com/library/bb934049.aspx) podem ser armazenadas no Cofre de Chaves com quaisquer chaves ou segredos dos seus aplicativos. Permissões e acesso toothese protegido itens são gerenciados por meio de [Active Directory do Azure](https://azure.microsoft.com/documentation/services/active-directory/).

Saiba mais:

* [O que é o Cofre da Chave do Azure?](../key-vault/key-vault-whatis.md)
* [Introdução ao Cofre da Chave do Azure](../key-vault/key-vault-get-started.md)
* [Blog do Cofre de Chaves do Azure](https://blogs.technet.microsoft.com/kv/)

## <a name="virtual-machine-disk-encryption"></a>Criptografia de disco da máquina virtual
O Azure Disk Encryption é uma nova funcionalidade que permite criptografar os discos de suas máquinas virtuais Windows e Linux do Azure. Criptografia de disco do Azure usa saudação padrão [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) recurso do Windows e hello [dm crypt](https://en.wikipedia.org/wiki/Dm-crypt) recurso de criptografia de volume tooprovide Linux para hello SO e discos de dados de saudação.

solução de saudação é integrada ao Azure Key Vault toohelp controlar e gerenciar chaves de criptografia de disco hello e segredos em sua assinatura do Cofre de chaves, garantindo que todos os dados em discos da máquina virtual Olá sejam criptografados em repouso no armazenamento do Azure.

Saiba mais:

* [Criptografia de Disco do Azure para VMs IaaS Windows e Linux](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0)
* [Azure Disk Encryption for Linux and Windows Virtual Machines (Azure Disk Encryption para máquinas virtuais Windows e Linux)](https://blogs.msdn.microsoft.com/azuresecurity/2015/11/16/azure-disk-encryption-for-linux-and-windows-virtual-machines-public-preview-now-available/)
* [Criptografar uma máquina virtual](../security-center/security-center-disk-encryption.md)

## <a name="virtual-machine-backup"></a>Backup de máquinas virtuais
O Backup do Azure é uma solução escalonável que protege os dados do seu aplicativo com zero investimento de capital e custos operacionais mínimos. Erros de aplicativo podem corromper seus dados e erros humanos podem introduzir bugs em seus aplicativos. Com o Backup do Azure, suas máquinas virtuais executando Windows e Linux estão protegidas.

Saiba mais:

* [O que é o Backup do Azure?](../backup/backup-introduction-to-azure-backup.md)
* [Roteiro de aprendizagem do Backup do Azure](https://azure.microsoft.com/documentation/learning-paths/backup/)
* [Serviço de Backup do Azure - Perguntas frequentes](../backup/backup-azure-backup-faq.md)

## <a name="azure-site-recovery"></a>Azure Site Recovery
Uma parte importante da estratégia BCDR da sua organização é descobrir como tookeep cargas de trabalho corporativa e aplicativos de backup e em execução quando planejado e não planejado ocorre. O Azure Site Recovery ajuda a orquestrar a replicação, failover e recuperação dos aplicativos e cargas de trabalho para que eles estejam disponíveis a partir de um local secundário, caso o local principal fique inativo.

Recuperação de Site:

* **Simplifica a sua estratégia BCDR** – recuperação de Site torna fácil toohandle replicação, failover e recuperação de várias cargas de trabalho de negócios e aplicativos de um único local. A Recuperação de Site orquestra a replicação e o failover, mas não intercepta os dados do aplicativo ou tem quaisquer informações sobre ele.
* **Fornece replicação flexível** : com a Recuperação de Site, você pode replicar cargas de trabalho em execução em máquinas virtuais Hyper-V, máquinas virtuais VMware e servidores físicos com Windows/Linux.
* **Oferece suporte a failover e recuperação** – recuperação de Site fornece recuperação de desastre toosupport failovers de teste sem afetar os ambientes de produção. Você também pode executar failovers planejados sem perder qualquer dado durante interrupções esperadas, ou failovers não planejados com perda mínima de dados (dependendo da frequência de replicação) para desastres inesperados. Após o failover, você pode sites primários do failback tooyour. A Recuperação de Site fornece planos de recuperação que podem incluir scripts e pastas de trabalho de automação do Azure, para que você possa personalizar o failover e a recuperação de aplicativos de várias camadas.
* **Elimina o datacenter secundário** — você pode replicar tooa secundário no site local ou tooAzure. Usando o Azure como um destino de recuperação de desastres elimina Olá custo e a complexidade de manter um site secundário. Os dados replicados são colocados no Armazenamento do Azure.
* **Integra com tecnologias de BCDR existentes** : a Recuperação de Site estabelece uma parceria com outros recursos de BCDR do aplicativo. Por exemplo, você pode usar a recuperação de Site tooprotect saudação do SQL Server back-end de cargas de trabalho corporativas. Isso inclui o suporte nativo para o SQL Server AlwaysOn toomanage Olá failover de grupos de disponibilidade.

Saiba mais:

* [O que é o Azure Site Recovery?](../site-recovery/site-recovery-overview.md)
* [Como funciona o Azure Site Recovery?](../site-recovery/site-recovery-components.md)
* [Quais cargas de trabalho são protegidas pelo Azure Site Recovery?](../site-recovery/site-recovery-workload.md)

## <a name="virtual-networking"></a>Rede Virtual
As máquinas virtuais precisam de conectividade de rede. toosupport esse requisito, o Azure requer toobe de máquinas virtuais conectada tooan rede Virtual do Azure. Uma rede Virtual do Azure é um constructo lógico criado com base em malha de rede do Azure física hello. Cada Rede Virtual do Azure lógica é isolada das todas as outras Redes Virtuais do Azure. Esse isolamento ajuda a garantir que o tráfego de rede em suas implantações não é os clientes do Microsoft Azure tooother acessível.

Saiba mais:

* [Azure Network Security Overview (Visão geral da segurança de rede do Azure)](security-network-overview.md)
* [Visão geral da Rede Virtual](../virtual-network/virtual-networks-overview.md)
* [Networking features and partnerships for Enterprise scenarios (Recursos de rede e parcerias para cenários empresariais)](https://azure.microsoft.com/blog/networking-enterprise/)

## <a name="security-policy-management-and-reporting"></a>Gerenciamento de política de segurança e emissão de relatórios
Central de segurança do Azure ajuda a evitar, detectar e responder toothreats e fornece que maior visibilidade e controle, segurança de saudação de seus recursos do Azure. Ela permite o gerenciamento de políticas e o monitoramento da segurança integrada entre suas assinaturas do Azure, ajuda a detectar ameaças que poderiam passar despercebidas e funciona com uma enorme variedade de soluções de segurança.

A Central de Segurança do Azure ajuda a otimizar e a monitorar a segurança da máquina virtual:

* Fornecendo [recomendações de segurança](../security-center/security-center-recommendations.md) para a máquina virtual, como aplicar atualizações do sistema, configurar pontos de extremidade de ACLs, habilitar o antimalware, habilitar grupos de segurança de rede e aplicar a criptografia de disco.
* Monitoramento de estado de saudação de suas máquinas virtuais

Saiba mais:

* [Introdução tooAzure Central de segurança](../security-center/security-center-intro.md)
* [Perguntas frequentes sobre a Central de Segurança do Azure](../security-center/security-center-faq.md)
* [Planejamento e operações da Central de Segurança do Azure](../security-center/security-center-planning-and-operations-guide.md)

## <a name="compliance"></a>Conformidade
As Máquinas Virtuais do Azure são certificados para FISMA, FedRAMP, HIPAA, PCI DSS Nível 1 e outros programas de conformidade de chaves. Essa certificação torna mais fácil para seus próprios requisitos de conformidade toomeet aplicativos do Azure e para seus negócios tooaddress uma ampla variedade de requisitos normativos nacionais e internacionais.

Saiba mais:

* [Microsoft Trust Center: Compliance (Central de Confiabilidade da Microsoft: conformidade)](https://www.microsoft.com/TrustCenter/Compliance/default.aspx)
* [Trusted Cloud: Microsoft Azure Security, Privacy, and Compliance (A nuvem confiável: segurança, privacidade e conformidade do Microsoft Azure)](http://download.microsoft.com/download/1/6/0/160216AA-8445-480B-B60F-5C8EC8067FCA/WindowsAzure-SecurityPrivacyCompliance.pdf)
