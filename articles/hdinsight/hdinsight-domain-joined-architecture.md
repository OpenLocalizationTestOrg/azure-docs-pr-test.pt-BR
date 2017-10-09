---
title: arquitetura de HDInsight do Azure associado aaaDomain | Microsoft Docs
description: "Saiba como tooplan domínio HDInsight."
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7dc6847d-10d4-4b5c-9c83-cc513cf91965
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/03/2017
ms.author: saurinsh
ms.openlocfilehash: 1c3ecedf3739b4f8fa54160225be9c1d6e2ca6cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="plan-azure-domain-joined-hadoop-clusters-in-hdinsight"></a>Planejar clusters Hadoop do Azure associados ao domínio no HDInsight

Olá Hadoop tradicional é um cluster de usuário único. Ele é adequado para a maioria das empresas que têm equipes de aplicativos menores que criam grandes cargas de trabalho de dados. À medida que o Hadoop ganha popularidade, muitas empresas estão mudando para um modelo em que clusters são gerenciados por equipes de TI, e várias equipes de aplicativo compartilham clusters. Assim, as funcionalidades que envolvem clusters multiusuários estão entre hello mais funcionalidades solicitadas no Azure HDInsight.

Em vez de criar seu próprio multiusuário autenticação e autorização, HDInsight depende do provedor de identidade mais popular do hello – AD (Active Directory). funcionalidade de segurança avançada do Hello no AD pode ser a autorização multiusuário toomanage usado no HDInsight. Integrando o HDInsight com o AD, você pode se comunicar com clusters hello usando suas credenciais do AD. HDInsight mapeia um AD usuário tooa Hadoop usuário local, para que todos os serviços em execução no HDInsight de hello (Ambari, Hive Spark thrift do servidor, Ranger, servidor e outros) diretamente para o usuário autenticado de saudação.

## <a name="integrate-hdinsight-with-ad-and-ad-on-iaas-vm"></a>Integrar o HDInsight com o AD e o AD em VM IaaS

Integrando o HDInsight com o Azure AD ou AD na VM de Iaas, nós de cluster do HDInsight Olá são domínio tooa ingressado no domínio. HDInsight cria entidades de serviço para Olá serviços Hadoop em execução no cluster hello e coloca dentro de uma unidade organizacional especificada (UO) no Azure AD ou AD na VM de IaaS. HDInsight também cria mapeamentos inversas de DNS no domínio Olá Olá endereços IP de nós Olá toohello ingressado no domínio.

Você pode obter essa configuração, usando várias arquiteturas. Você pode escolher entre Olá arquiteturas a seguir.

**HDInsight integrado ao AD em execução no Azure IaaS**

Esta é a arquitetura mais simples Olá para a integração de HDInsight com o Active Directory. saudação de controlador de domínio do AD é executado em uma (ou vários) máquinas de virtuais (VMs) no Azure. Essas VMs são normalmente em uma rede virtual. Configure outra rede virtual para o cluster do HDInsight hello. Para HDInsight toohave tooActive uma linha de visão diretório, você precisa a toopeer essas redes virtuais usando [emparelhamento VNet para VNet](../virtual-network/virtual-network-create-peering.md). Se você criar hello Active Directory no ARM, em seguida, você pode criar saudação do Active Directory e Olá de HDInsight na mesma rede virtual e não é necessário toodo emparelhamento. 

![Topologia de cluster do HDInsight de associação de domínio](./media/hdinsight-domain-joined-architecture/hdinsight-domain-joined-architecture_1.png)

> [!NOTE]
> Nessa arquitetura, você não pode usar o repositório Azure Data Lake com cluster do HDInsight hello.


Pré-requisitos para o Active Directory:

* Um [unidade organizacional](../active-directory-domain-services/active-directory-ds-admin-guide-create-ou.md) devem ser criados, em que você coloque Olá VMs do cluster HDInsight e Olá entidades de serviço usadas pelo cluster hello.
* [Protocolos de acesso de diretório leve](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md) (LDAPs) devem ser configurados para se comunicar com o AD. Olá certificado usado tooset backup LDAPS deve ser um certificado real (não um certificado autoassinado).
* Zonas DNS reversas devem ser criadas no domínio de saudação do intervalo de endereços IP hello da sub-rede de HDInsight hello (por exemplo, 10.2.0.0/24 na imagem anterior Olá).
* Uma conta de serviço ou uma conta de usuário é necessária. Use este cluster do HDInsight conta toocreate hello. Essa conta deve ter Olá as seguintes permissões:

    - Objetos principais do serviço de toocreate de permissões e objetos de computador na unidade organizacional Olá
    - Regras de proxy DNS reversas do permissões toocreate
    - Domínio do Active Directory do permissões toojoin máquinas toohello

**HDInsight integrado ao Azure AD somente de nuvem**

Para o Azure AD somente na nuvem, configure um controlador de domínio para que o HDInsight possa ser integrado ao Azure AD. Isso é feito usando o [Azure Active Directory Domain Services](../active-directory-domain-services/active-directory-ds-overview.md) (Azure AD DS). Azure AD DS cria máquinas de controlador de domínio na nuvem hello e fornece endereços IP para eles. Ele cria dois controladores de domínio para alta disponibilidade.

Atualmente, o Azure AD DS só existe em redes virtuais clássicas. Somente é acessível por meio de saudação portal clássico do Azure. Olá HDInsight rede virtual existe no hello portal do Azure, que deve toobe emparelhadas com a rede virtual clássica de saudação usando o emparelhamento de VNet para VNet.

> [!NOTE]
> Emparelhamento entre uma rede virtual clássica e uma rede virtual requer que ambas as redes virtuais estão no Azure Resource Manager Olá mesma região e Olá mesmo em assinatura do Azure.

![Topologia de cluster do HDInsight de associação de domínio](./media/hdinsight-domain-joined-architecture/hdinsight-domain-joined-architecture_2.png)

Pré-requisitos do Azure AD:

* Um [unidade organizacional](../active-directory-domain-services/active-directory-ds-admin-guide-create-ou.md) devem ser criados em que você coloque Olá VMs do cluster HDInsight e Olá entidades de serviço usadas pelo cluster hello.
* O [LDAPS](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md) deve ser configurado quando você configura o AD DS. Olá certificado usado tooset backup LDAPS deve ser um certificado real (não um certificado autoassinado).
* Zonas DNS reversas devem ser criadas no domínio de saudação do intervalo de endereços IP hello da sub-rede de HDInsight hello (por exemplo, 10.2.0.0/24 na imagem anterior Olá).
* [Hashes de senha](../active-directory-domain-services/active-directory-ds-getting-started-password-sync.md) devem ser sincronizados a partir do AD do Azure tooAzure AD DS.
* Uma conta de serviço ou uma conta de usuário é necessária. Use este cluster do HDInsight conta toocreate hello. Essa conta deve ter Olá as seguintes permissões:

    - Objetos principais do serviço de toocreate de permissões e objetos de computador na unidade organizacional Olá
    - Regras de proxy DNS reversas do permissões toocreate
    - Domínio do permissões toojoin máquinas toohello AD do Azure

## <a name="next-steps"></a>Próximas etapas
* tooconfigure um cluster HDInsight ingressado no domínio, consulte [configurar clusters de HDInsight domínio](hdinsight-domain-joined-configure.md).
* clusters de HDInsight domínio toomanage, consulte [gerenciar clusters de HDInsight domínio](hdinsight-domain-joined-manage.md).
* políticas de Hive tooconfigure e executadas consultas de Hive, consulte [Hive configurar políticas para clusters de HDInsight domínio](hdinsight-domain-joined-run-hive.md).
* consultas de Hive toorun usando SSH em clusters de HDInsight ingressado no domínio, consulte [usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).
