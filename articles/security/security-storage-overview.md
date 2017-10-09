---
title: recursos de aaaSecurity que podem ser usados com o armazenamento do Azure | Microsoft Docs
description: " Este artigo fornece uma visão geral dos recursos de segurança do Azure do hello principais que podem ser usados com o armazenamento do Azure. "
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 521180dc-2cc9-43f1-ae87-2701de7ca6b8
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: 663cd2705527957d21ff9475a6322b42a16c95e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-security-overview"></a>Visão geral da segurança do armazenamento do Azure
Armazenamento do Azure é uma solução de armazenamento de nuvem Olá para aplicativos modernos que dependem de durabilidade, disponibilidade e escalabilidade toomeet Olá de seus clientes. O Armazenamento do Azure fornece um conjunto abrangente de funcionalidades de segurança:

* conta de armazenamento Olá pode ser protegida usando o controle de acesso baseado em função e o Active Directory do Azure.
* Os dados podem ser protegidos em trânsito, entre um aplicativo e o Azure usando a Criptografia do cliente, HTTPs ou SMB 3.0.
* Dados podem ser definidos toobe criptografado automaticamente quando gravados tooAzure armazenamento usando a criptografia do serviço de armazenamento.
* Sistema operacional e discos de dados usados por máquinas virtuais podem ser definidos toobe criptografado usando a criptografia de disco do Azure.
* Acesso delegado toohello objetos de dados no armazenamento do Azure podem ser concedidos usando assinaturas de acesso compartilhado.
* método de autenticação de saudação usado por alguém quando acessar o armazenamento pode ser acompanhado usando a análise de armazenamento.

Para obter uma visão mais detalhada de segurança no armazenamento do Azure, consulte Olá [guia de segurança do armazenamento do Azure](../storage/common/storage-security-guide.md). Este guia fornece um mergulho profundo em recursos de segurança de saudação do armazenamento do Azure, como chaves de conta de armazenamento, criptografia de dados em trânsito e em repouso e análise de armazenamento.

Este artigo fornece uma visão geral dos recursos de segurança do Azure que podem ser usados com o Armazenamento do Azure. Links são fornecidos tooarticles que forneça os detalhes de cada recurso para saber mais.

Aqui estão Olá principais recursos toobe abordada neste artigo:

* Controle de Acesso Baseado em Função
* Acesso delegado toostorage objetos
* Criptografia em trânsito
* Criptografia em repouso/criptografia do serviço de armazenamento
* Azure Disk Encryption
* Cofre da Chave do Azure

## <a name="role-based-access-control-rbac"></a>RBAC (Controle de Acesso Baseado em Função)
Você pode proteger a conta de armazenamento com o RBAC (Controle de Acesso Baseado em Função). Restringindo o acesso com base em Olá [necessário tooknow](https://en.wikipedia.org/wiki/Need_to_know) e [privilégio mínimo](https://en.wikipedia.org/wiki/Principle_of_least_privilege) princípios de segurança é fundamental para as organizações que desejam tooenforce políticas de segurança para acesso a dados. Esses direitos de acesso são concedidos atribuindo Olá apropriado RBAC função toogroups e aplicativos em um determinado escopo. Você pode usar [funções internas de RBAC](../active-directory/role-based-access-built-in-roles.md), como colaborador da conta de armazenamento, tooassign privilégios toousers.

Saiba mais:

* [Controle de acesso baseado em função do Active Directory do Azure](../active-directory/role-based-access-control-configure.md)

## <a name="delegated-access-toostorage-objects"></a>Acesso delegado toostorage objetos
Uma assinatura de acesso compartilhado (SAS) fornece acesso delegado tooresources na sua conta de armazenamento. Olá SAS significa que você pode conceder a que um cliente limitada tooobjects permissões na conta de armazenamento para um determinado período de tempo e com um conjunto de permissões especificado. Você pode conceder essas permissões limitadas sem ter que tooshare suas chaves de acesso da conta. Olá SAS é um URI que abrange em seus parâmetros de consulta todas as informações de saudação necessárias para o recurso de armazenamento de tooa acesso autenticado. tooaccess recursos de armazenamento com hello SAS, Olá cliente só precisa tooprovide Olá SAS toohello apropriado construtor ou método.

Saiba mais:

* [Modelo SAS Olá Noções básicas sobre](../storage/common/storage-dotnet-shared-access-signature-part-1.md)
* [Criar e usar um SAS com o armazenamento de Blobs](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md)

## <a name="encryption-in-transit"></a>Criptografia em trânsito
A criptografia em trânsito é um mecanismo de proteção de dados quando eles são transmitidos entre redes. Com o Armazenamento do Azure, você pode proteger dados usando:

* [Criptografia de nível de transporte](../storage/common/storage-security-guide.md#encryption-in-transit), como HTTPS ao transferir dados dentro ou fora do Armazenamento do Azure.
* [Criptografia na transmissão](../storage/common/storage-security-guide.md#using-encryption-during-transit-with-azure-file-shares), como a criptografia SMB 3.0 para compartilhamentos de Arquivo do Azure.
* [Criptografia do lado do cliente](../storage/common/storage-security-guide.md#using-client-side-encryption-to-secure-data-that-you-send-to-storage), dados de saudação tooencrypt antes que sejam transferidos em dados de saudação do armazenamento e toodecrypt depois que ela é transferida do armazenamento.

Saiba mais sobre a criptografia do cliente:

* [Client-Side Encryption for Microsoft Azure Storage (Criptografia do cliente para o Armazenamento do Microsoft Azure)](https://blogs.msdn.microsoft.com/windowsazurestorage/2015/04/28/client-side-encryption-for-microsoft-azure-storage-preview/)
* [Cloud security controls series: Encrypting Data in Transit (Série sobre controles de segurança de nuvem: criptografando dados em trânsito)](http://blogs.microsoft.com/cybertrust/2015/08/10/cloud-security-controls-series-encrypting-data-in-transit/)

## <a name="encryption-at-rest"></a>Criptografia em repouso
Para muitas organizações, a [criptografia de dados em repouso](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/) é uma etapa obrigatória no sentido de garantir a soberania, a privacidade e a conformidade dos dados. Há três recursos do Azure que fornecem criptografia de dados que estão “em repouso”:

* [Criptografia do serviço de armazenamento](../storage/common/storage-security-guide.md#encryption-at-rest) permite que o serviço de armazenamento de saudação criptografa automaticamente os dados quando escrever tooAzure armazenamento de toorequest.
* [Criptografia do lado do cliente](../storage/common/storage-security-guide.md#client-side-encryption) também fornece o recurso de saudação de criptografia em repouso.
* [Criptografia de disco do Azure](../storage/common/storage-security-guide.md#using-azure-disk-encryption-to-encrypt-disks-used-by-your-virtual-machines) permite que você tooencrypt Olá OS discos e dados usados por uma máquina virtual IaaS.

Saiba mais sobre a Criptografia do Serviço de Armazenamento:

* A [Criptografia do Serviço Azure Storage](https://azure.microsoft.com/services/storage/) está disponível para [Azure Blob Storage](https://azure.microsoft.com/services/storage/blobs/). Para obter detalhes sobre outros tipos de armazenamento do Azure, confira [Arquivo](https://azure.microsoft.com/services/storage/files/), [Disco (Armazenamento Premium)](https://azure.microsoft.com/services/storage/premium-storage/), [Tabela](https://azure.microsoft.com/services/storage/tables/) e [Fila](https://azure.microsoft.com/services/storage/queues/).
* [Criptografia do Serviço de Armazenamento do Azure para dados em repouso](../storage/common/storage-service-encryption.md)

## <a name="azure-disk-encryption"></a>Azure Disk Encryption
O Azure Disk Encryption para VMs (Máquinas Virtuais) o ajuda a atender aos requisitos de conformidade e segurança organizacionais criptografando os discos de VM (incluindo discos de dados e de inicialização) com chaves e políticas controladas no [Cofre de Chaves do Azure](https://azure.microsoft.com/services/key-vault/).

A criptografia de disco para VMs funciona para sistemas operacionais Windows e Linux. Ele também usa o Cofre de chaves toohelp proteger, gerenciar e auditar o uso de suas chaves de criptografia de disco. Todos os dados de saudação em seus discos VM são criptografados em repouso usando a tecnologia de criptografia padrão da indústria em suas contas de armazenamento do Azure. Olá solução de criptografia de disco para o Windows é baseado no [Microsoft BitLocker Drive Encryption](https://technet.microsoft.com/library/cc732774.aspx), e Olá Linux solução se baseia em [dm crypt](https://en.wikipedia.org/wiki/Dm-crypt).

Saiba mais:

* [Azure Disk Encryption for Windows and Linux IaaS Virtual Machines (Azure Disk Encryption para máquinas virtuais IaaS Windows e Linux)](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0)

## <a name="azure-key-vault"></a>Cofre da Chave do Azure
Criptografia de disco do Azure usa [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) toohelp controlar e gerenciar chaves de criptografia de disco e segredos em sua assinatura do Cofre de chaves, garantindo que todos os dados em discos da máquina virtual Olá sejam criptografados em repouso do Azure Armazenamento. Você deve usar as chaves do Cofre de chaves tooaudit e uso de política.

Saiba mais:

* [O que é o Cofre da Chave do Azure?](../key-vault/key-vault-whatis.md)
* [Introdução ao Cofre da Chave do Azure](../key-vault/key-vault-get-started.md)
