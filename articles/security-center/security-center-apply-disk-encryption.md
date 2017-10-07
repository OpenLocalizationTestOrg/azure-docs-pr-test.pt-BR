---
title: "criptografia de disco aaaApply na Central de segurança do Azure | Microsoft Docs"
description: "Este documento mostra como tooimplement Olá recomendação da Central de segurança do Azure * * aplicar criptografia de disco * *."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 6cc7824a-8d6b-4a5f-ab40-e3bbaebc4a91
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: cd803f1120018c5c86da91186eec1e59d425ede7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="apply-disk-encryption-in-azure-security-center"></a>Aplicar a criptografia de disco na Central de Segurança do Azure
A Central de Segurança do Azure recomenda que você aplique a criptografia de disco caso haja discos de VM do Windows ou Linux que não estejam criptografados com o Azure Disk Encryption. A Criptografia de Disco permite que você criptografe os discos de VM IaaS do Windows e do Linux.  Criptografia é recomendada para Olá SO e os volumes de dados na sua VM.

Criptografia de disco usa saudação padrão [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) recurso do Windows e hello [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) recurso do Linux. Esses recursos fornecem um sistema operacional e proteger toohelp de criptografia de dados e proteger seus dados e atender os compromissos de conformidade e segurança organizacional. Criptografia de disco é integrada com [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) toohelp controlar e gerenciar chaves de criptografia de disco hello e segredos em sua assinatura do Cofre de chaves, garantindo que todos os dados em discos de VM Olá sejam criptografados em repouso em sua [ Armazenamento do Azure](https://azure.microsoft.com/documentation/services/storage/).

> [!NOTE]
> Há suporte para criptografia de disco do Azure Olá seguintes sistemas operacionais Windows server - Windows Server 2008 R2, Windows Server 2012 e Windows Server 2012 R2. Há suporte para criptografia de disco Olá sistemas operacionais Linux server - Ubuntu, CentOS, SUSE e SUSE Linux Enterprise Server (SLES) a seguir.
>
>

## <a name="implement-hello-recommendation"></a>Implementar a recomendação de saudação
1. Em Olá **recomendações** folha, selecione **aplicar a criptografia de disco**.
2. Em Olá **aplicar a criptografia de disco** folha, verá uma lista de máquinas virtuais para o qual a criptografia de disco é recomendada.
3. Execute toothese de criptografia do hello instruções tooapply VMs.

![][1]

tooencrypt máquinas virtuais do Azure que foram identificados pela Central de segurança que precisam de criptografia, é recomendável Olá etapas a seguir:

* Instalar e configurar o PowerShell do Azure. Isso permite que você toorun Olá PowerShell comandos necessário tooset a saudação de pré-requisitos necessários tooencrypt máquinas virtuais do Azure.
* Obter e executar o script do PowerShell do Azure disco criptografia pré-requisitos do Azure hello.
* Criptografar suas máquinas virtuais.

[Criptografar uma Máquina Virtual do Azure](security-center-disk-encryption.md) explica essas etapas.  Este tópico pressupõe que você está usando o Windows 10 como máquina de cliente de saudação do qual você configurar a criptografia de disco.

Há várias abordagens que podem ser usadas para as Máquinas Virtuais do Azure. Se você já estiver bem familiarizado com Azure PowerShell ou CLI do Azure, talvez você prefira abordagens alternativas toouse. toolearn sobre esses outros métodos, consulte [criptografia de disco do Azure](../security/azure-security-disk-encryption.md).

## <a name="see-also"></a>Consulte também
Este documento lhe mostrou como tooimplement Olá Central de segurança recomendação "aplicar criptografia de disco." toolearn mais informações sobre criptografia de disco, consulte o seguinte hello:

* [Criptografia e gerenciamento de chaves com Cofre de chaves do Azure](https://azure.microsoft.com/documentation/videos/azurecon-2015-encryption-and-key-management-with-azure-key-vault/) (vídeo, 36 minutos 39 segundos) – Saiba como toouse disco o gerenciamento de criptografia para as VMs de IaaS e o Azure Key Vault toohelp proteger e proteger seus dados.
* [Criptografar uma máquina Virtual Azure](security-center-disk-encryption.md) (documento) – Saiba como tooencrypt máquinas virtuais do Azure.
* [Criptografia de disco do Azure](../security/azure-security-disk-encryption.md) (documento) – Saiba como tooenable disco criptografia para o Windows e VMs do Linux.

toolearn mais sobre o Centro de segurança, consulte o seguinte hello:

* [Definir políticas de segurança na Central de segurança do Azure](security-center-policies.md) – Saiba como tooconfigure as políticas de segurança.
* [Monitoramento de integridade de segurança na Central de segurança do Azure](security-center-monitoring.md) – Saiba como toomonitor Olá a integridade de seus recursos do Azure.
* [Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md) – Saiba como alertas de toosecurity toomanage e responder.
* [Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md) : saiba como as recomendações ajudam a proteger os recursos do Azure.
* [Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md) – localizar perguntas frequentes sobre como usar o serviço de saudação.
* [Blog de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) – encontre postagens no blog sobre conformidade e segurança do Azure.

<!--Image references-->
[1]: ./media/security-center-apply-disk-encryption/apply-disk-encryption.png
