---
title: aplicativos de PaaS aaaSecuring usando o armazenamento do Azure | Microsoft Docs
description: " Conheça as melhores práticas de segurança do Armazenamento do Azure para proteger aplicativos móveis e Web de PaaS. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: TomShinder
ms.openlocfilehash: 3fed75cb121e7f32eb8b948ee12ca35fb25eca7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-paas-web-and-mobile-applications-using-azure-storage"></a>Proteger aplicativos móveis e Web de PaaS usando o Armazenamento do Azure
Neste artigo, discutiremos um conjunto de práticas recomendadas de segurança do Armazenamento do Azure para proteger seus aplicativos móveis e Web de PaaS. Essas práticas recomendadas são derivadas da nossa experiência com o Azure e experiências de saudação de clientes, como por conta própria.

Olá [guia de segurança do armazenamento do Azure](../storage/common/storage-security-guide.md) é uma ótima fonte para obter informações detalhadas sobre a segurança e o armazenamento do Azure.  Este artigo aborda em um nível alto alguns dos conceitos de saudação encontrados no guia de segurança do hello e guia de segurança de toohello links, bem como outras fontes, para obter mais informações.

## <a name="azure-storage"></a>Armazenamento do Azure
Azure torna possível armazenamento toodeploy e uso de maneiras não facilmente alcançáveis local. Com o Armazenamento do Azure, você pode alcançar altos níveis de escalabilidade e disponibilidade com relativamente pouco esforço. Não é apenas foundation de saudação do armazenamento do Azure para Windows e máquinas virtuais do Linux do Azure, ela também pode suportar grandes aplicativos distribuídos.

Armazenamento do Azure fornece Olá quatro serviços a seguir: armazenamento de Blob, o armazenamento de tabela, armazenamento de fila e o armazenamento de arquivos. mais, consulte toolearn [tooMicrosoft Introdução armazenamento do Azure](../storage/storage-introduction.md).

## <a name="best-practices"></a>Práticas recomendadas
Este artigo aborda Olá práticas recomendadas a seguir:

- Proteção de acesso:
   - SAS (Assinaturas de Acesso Compartilhado)
   - Disco gerenciado
   - RBAC (Controle de Acesso Baseado em Função)

- Criptografia de armazenamento:
   - Criptografia do lado do cliente para dados de alto valor
   - Azure Disk Encryption para VMs (máquinas virtuais)
   - Criptografia do Serviço de Armazenamento

## <a name="access-protection"></a>Proteção de acesso
### <a name="use-shared-access-signature-instead-of-a-storage-account-key"></a>Use a Assinatura de Acesso Compartilhado em vez de uma chave de conta de armazenamento

Em uma solução de IaaS, geralmente executando máquinas virtuais do Windows Server ou Linux, os arquivos são protegidos contra ameaças de divulgação e violação usando mecanismos de controle de acesso. No Windows, você usaria [ACLs (listas de controle de acesso)](../virtual-network/virtual-networks-acl.md) e, no Linux, provavelmente usaria [chmod](https://en.wikipedia.org/wiki/Chmod). Essencialmente, é exatamente isso o que você faria se estivesse protegendo arquivos em um servidor em seu próprio data center hoje.

Com PaaS, é diferente. Um dos arquivos toostore maneiras de hello mais comuns no Microsoft Azure é toouse [armazenamento de BLOBs do Azure](../storage/storage-dotnet-how-to-use-blobs.md). Uma diferença entre o armazenamento de Blob e outros arquivos é Olá métodos de proteção que vêm com e/s de arquivo e e/s de arquivo hello.

O controle de acesso é fundamental. toohelp controlar acesso tooAzure armazenamento, Olá sistema irá gerar duas chaves de conta de armazenamento de 512 bits (SAKs) quando você [criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md). nível de saudação de redundância de chave possibilita que você tooavoid serviço interrupção durante a rotação de chave de rotina.

Teclas de acesso de armazenamento são segredos de alta prioridade e só devem ser acessível toothose responsável pelo controle de acesso de armazenamento. Se pessoas erradas Olá obtém acesso a chaves toothese, eles serão ter controle total de armazenamento e pode substituir, excluir ou adicionar toostorage de arquivos. Isso inclui malware e outros tipos de conteúdo com potencial para comprometer seus clientes ou sua organização.

Você ainda precisa tooobjects de acesso de tooprovide uma forma no armazenamento. tooprovide mais granular acesso, você pode tirar proveito do [assinatura de acesso compartilhado](../storage/common/storage-dotnet-shared-access-signature-part-1.md) (SAS). Olá SAS torna possível para você tooshare a objetos específicos no armazenamento para um intervalo de tempo predefinido e com permissões específicas. Uma assinatura de acesso compartilhado permite que você toodefine:

- intervalo de saudação sobre quais Olá SAS é válido, incluindo hora de início do hello e tempo de expiração de saudação.
- Olá permissões por Olá SAS. Por exemplo, uma SAS em um blob pode conceder a uma usuário de leitura e gravar permissões toothat blob, mas não excluir permissões.
- Intervalo de endereços IP ou um endereço IP opcional do qual o armazenamento do Azure aceita Olá SAS. Por exemplo, você pode especificar um intervalo de endereços IP que pertencem a organização tooyour. Isso fornece outra medida de segurança para a SAS.
- protocolo de saudação durante o qual o armazenamento do Azure aceita Olá SAS. Você pode usar este parâmetro opcional toorestrict acesso tooclients que usando HTTPS.

SAS permite que você tooshare maneira de saudação conteúdo você deseja tooshare-lo sem dar as chaves de conta de armazenamento. Sempre usar SAS em seu aplicativo é uma maneira segura tooshare seus recursos de armazenamento sem comprometer as chaves de conta de armazenamento.

mais, consulte toolearn [usando assinaturas de acesso compartilhado](../storage/common/storage-dotnet-shared-access-signature-part-1.md) (SAS). mais informações sobre possível toomitigate riscos e as recomendações de toolearn esses riscos, consulte [de práticas recomendadas ao usar SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

### <a name="use-managed-disks-for-vms"></a>Usar discos gerenciados para VMs

Quando você escolhe [discos gerenciado do Azure](../storage/storage-managed-disks-overview.md), o Azure gerencia contas de armazenamento Olá que você pode usar para os discos VM. Você só precisa toodo é escolher tipo de saudação do disco (Premium ou padrão) e o tamanho do disco Olá; Armazenamento do Azure fará Olá rest. Você não tem tooworry sobre limites de escalabilidade do que outra forma exigiam tooyou toomultiple as contas de armazenamento.

mais, consulte toolearn [perguntas frequentes sobre gerenciados e discos premium](../storage/storage-faq-for-disks.md).

### <a name="use-role-based-access-control"></a>Usar o controle de acesso baseado em função

Discutimos anteriormente usando tooobjects de acesso de toogrant limitado de assinatura de acesso compartilhado (SAS) em seus clientes tooother de conta de armazenamento, sem expor sua chave de conta de armazenamento de conta. Às vezes, o riscos de saudação associados a uma determinada operação em sua conta de armazenamento superam os benefícios de saudação da SAS. Às vezes é mais simples acesso toomanage de outras maneiras.

Acesso de toomanage outra maneira é toouse [o controle de acesso](../active-directory/role-based-access-control-what-is.md) (RBAC). Com o RBAC, você se concentre nos fornecendo aos funcionários permissões exatas de saudação que precisam, com base em Olá necessidade tooknow e princípios de segurança de privilégio mínimo. Número excessivo de permissões pode expor uma tooattackers de conta. Permissões insuficientes significa que os funcionários não podem ter seu trabalho feito com eficiência. O RBAC ajuda a resolver esse problema oferecendo gerenciamento de acesso refinado ao Azure. Isso é essencial para as organizações que desejam tooenforce políticas de segurança para acesso a dados.

Você pode aproveitar as funções internas de RBAC no Azure tooassign toousers de privilégios. Considere o uso de colaborador da conta de armazenamento para os operadores de nuvem que precisam de contas de armazenamento toomanage e contas de armazenamento clássicas de toomanage de função de Colaborador clássico de conta de armazenamento. Operadores de nuvem que precisam toomanage VMs, mas a rede virtual não Olá ou toowhich de conta de armazenamento que estão conectados, considere adicioná-los toohello função de Colaborador de máquina Virtual.

As organizações que não impõem o controle de acesso de dados utilizando recursos como o RBAC podem estar dando mais privilégios do que o necessário para seus usuários. Isso pode levar toodata comprometimento, permitindo algumas toodata de acesso de usuários eles não deveriam ter em primeiro lugar de saudação.

toolearn que mais sobre o RBAC, consulte:

- [Controle de Acesso Baseado em Função do Azure](../active-directory/role-based-access-control-configure.md)
- [Funções internas para controle de acesso baseado em função do Azure](../active-directory/role-based-access-built-in-roles.md)
- [Guia de segurança do armazenamento do Azure](../storage/common/storage-security-guide.md) para obter detalhes sobre como toosecure sua conta de armazenamento com RBAC

## <a name="storage-encryption"></a>Criptografia do armazenamento
### <a name="use-client-side-encryption-for-high-value-data"></a>Use a criptografia do lado do cliente para dados de alto valor

Habilita a criptografia do lado do cliente tooprogrammatically você criptografar dados em trânsito antes de carregar tooAzure armazenamento e descriptografar os dados por meio de programação quando recuperá-los do armazenamento.  Isso fornece criptografia de dados em trânsito, mas também fornece criptografia de dados em repouso.  Criptografia do lado do cliente é o método mais seguro de saudação de criptografar os dados, mas exigir aplicativos de tooyour alterações programático toomake e implementar processos de gerenciamento de chaves.

Criptografia do lado do cliente também permite que você toohave o controle exclusivo sobre as chaves de criptografia.  Você pode gerar e gerenciar suas próprias chaves de criptografia.  Criptografia do lado do cliente usa uma técnica de envelope onde hello biblioteca de cliente de armazenamento do Azure gera uma criptografia de conteúdo CEK (chave) que é fornecida (criptografada) usando a chave de criptografia de chave da saudação (KEK). Hello KEK é identificada por um identificador de chave e pode ser um par de chaves assimétricas ou uma chave simétrica e podem ser gerenciado localmente ou armazenado em [Azure Key Vault](../key-vault/key-vault-whatis.md).

Criptografia do lado do cliente é criada em Java hello e bibliotecas de cliente de armazenamento Olá .NET.  Consulte [Criptografia do lado do cliente e Azure Key Vault para o Armazenamento do Microsoft Azure](../storage/storage-client-side-encryption.md) para obter informações sobre a criptografia de dados em aplicativos cliente e sobre como gerar e gerenciar suas próprias chaves de criptografia.

### <a name="azure-disk-encryption-for-vms"></a>Azure Disk Encryption para máquinas virtuais
O Azure Disk Encryption é uma capacidade que ajuda você a criptografar seus discos de máquina virtual IaaS Windows e Linux. Criptografia de disco do Azure utiliza Olá setor padrão BitLocker recursos do Windows e Olá DM Crypt Linux tooprovide da criptografia do volume para Olá SO e discos de dados de saudação. solução de saudação é integrada ao Azure Key Vault toohelp controlar e gerenciar chaves de criptografia de disco hello e segredos em sua assinatura do Cofre de chaves. solução de saudação também garante que todos os dados em discos de máquina virtual Olá sejam criptografados em repouso no armazenamento do Azure.

Consulte [Azure Disk Encryption para VMs IaaS Windows e Linux](azure-security-disk-encryption.md).

### <a name="storage-service-encryption"></a>Criptografia do Serviço de Armazenamento
Quando [criptografia do serviço de armazenamento](../storage/storage-service-encryption.md) para armazenamento de arquivos estiver habilitado, os dados de saudação são criptografados automaticamente usando a criptografia AES-256. Microsoft manipula toda a criptografia de hello, descriptografia e gerenciamento de chaves. Este recurso está disponível para os tipos de redundância LRS e GRS.

## <a name="next-steps"></a>Próximas etapas
Este artigo introduzido coleção tooa das práticas recomendadas de segurança de armazenamento do Azure para proteger seu PaaS aplicativos web e móveis. toolearn mais sobre como proteger suas implantações de PaaS, consulte:

- [Proteção das implantações PaaS](security-paas-deployments.md)
- [Securing PaaS web and mobile applications using Azure App Services](security-paas-applications-using-app-services.md) (Proteção dos aplicativos Web e móveis de PaaS usando os Serviços de Aplicativos do Azure)
- [Protegendo bancos de dados de PaaS no Azure](security-paas-applications-using-sql.md)
