---
title: "Glossário do aaaAzure - dicionário do Azure | Microsoft Docs"
description: "Use terminologia de nuvem Olá Glossário do Azure toounderstand Olá plataforma Windows Azure. Este pequeno dicionário do Azure oferece definições para termos comuns de nuvem do Azure."
keywords: "Dicionário do Azure, terminologia de nuvem, Glossário do Azure, definições de terminologia, termos de nuvem"
services: na
documentationcenter: na
author: MonicaRush
manager: jhubbard
editor: 
ms.assetid: d7ac12f7-24b5-4bcd-9e4d-3d76fbd8d297
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: monicar
ms.openlocfilehash: 486bbbfc71a48a6ebc39b14f7ab71f8604b7a6b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-glossary-a-dictionary-of-cloud-terminology-on-hello-azure-platform"></a>Glossário do Microsoft Azure: um dicionário de terminologia de nuvem em Olá plataforma Windows Azure

Glossário do Microsoft Azure Olá é um dicionário curto da terminologia de nuvem para Olá plataforma Windows Azure. Consulte também:

* [Microsoft Azure e Amazon Web Services](https://azure.microsoft.com/campaigns/azure-vs-aws/mapping/) – definições dos serviços do Azure e de suas contrapartes em AWS.<!-- I propose toolink toohttps://azure.microsoft.com/en-us/services/ instead of this -->
* [Termos de computação em nuvem](https://azure.microsoft.com/overview/cloud-computing-dictionary/) – termos gerais de nuvem do setor.

## <a name="account"></a>conta
Uma conta que tenha usado tooaccess e gerenciar uma assinatura do Azure. Ele geralmente referenciado tooas um Azure conta Embora uma conta pode ser um dos seguintes: um trabalho existente, escola, ou pessoais conta da Microsoft, ou um nome de usuário do Office 365 e senha. Você também pode criar uma conta toomanage uma assinatura do Azure quando você se inscrever para Olá [avaliação gratuita](https://azure.microsoft.com).  
Consulte [inscrever-se para uma assinatura do Azure com sua conta do Office 365](billing/billing-use-existing-office-365-account-azure-subscription.md) e [contas que você pode usar toosign em](active-directory/active-directory-how-subscriptions-associated-directory.md).

## <a name="api-app"></a>Aplicativo de API
Outro nome para o [aplicativo de Serviço de Aplicativo](#app-service-app).

## <a name="app-service-app"></a>Aplicativo de Serviço de Aplicativo
Olá recursos de computação que [do serviço de aplicativo do Azure](app-service/app-service-value-prop-what-is.md) fornece para hospedar um [site ou aplicativo web](app-service-web/app-service-web-overview.md), [web API](app-service-api/app-service-api-apps-why-best-platform.md), ou [back-end do aplicativo móvel](app-service-mobile/app-service-mobile-value-prop.md). Aplicativos de serviço de aplicativo também são chamados de tooas *serviços de aplicativos*, *aplicativos web*, *aplicativos de API*, e *aplicativos móveis*.

## <a name="availability-set"></a>conjunto de disponibilidade
Uma coleção de máquinas virtuais que são gerenciados juntos tooprovide redundância de aplicativos e confiabilidade. uso de saudação de um conjunto de disponibilidade garante que, durante um evento de manutenção planejada ou não planejada, pelo menos, uma máquina virtual está disponível.  
Consulte [gerenciar Olá disponibilidade de máquinas virtuais do Windows](virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) e [gerenciar Olá disponibilidade das máquinas virtuais Linux](virtual-machines/linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="classic-model"></a>modelo de implantação clássico do Azure
Um dos dois [modelos de implantação](resource-manager-deployment-model.md) toodeploy dos recursos usados no Azure (novo modelo de saudação é o Gerenciador de recursos do Azure). Alguns serviços do Azure só modelo de implantação de saudação Gerenciador de recursos de suporte, alguns suportam apenas o modelo de implantação clássico hello e alguns suportam ambos. documentação de saudação para cada serviço do Azure Especifica quais modelos dão suporte.

## <a name="cli"></a>CLI (interface de linha de comando) do Azure
Uma interface de linha de comando que pode ser usado toomanage serviços do Azure do Windows, macOS e Linux.  Alguns serviços ou recursos de serviço podem ser gerenciados somente por meio do PowerShell ou hello CLI. Veja [CLI do Azure 2.0](/cli/azure/overview)

## <a name="powershell"></a>PowerShell do Azure
Uma interface de linha de comando toomanage serviços do Azure por meio de uma linha de comando de computadores Windows. Alguns serviços ou recursos de serviço podem ser gerenciados somente por meio do PowerShell ou hello CLI.
Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview)

## <a name="arm-model"></a>modelo de implantação do Azure Resource Manager
Um dos dois [modelos de implantação](resource-manager-deployment-model.md) toodeploy dos recursos usados no Microsoft Azure (Olá outros é o modelo de implantação clássico Olá). Alguns serviços do Azure só modelo de implantação de saudação Gerenciador de recursos de suporte, alguns suportam apenas o modelo de implantação clássico hello e alguns suportam ambos. documentação de saudação para cada serviço do Azure Especifica quais modelos dão suporte.

## <a name="fault-domain"></a>domínio de falha
Olá coleção de máquinas virtuais em um conjunto de disponibilidade pode falhar em Olá mesmo tempo. Um exemplo disso é um grupo de máquinas em um rack que compartilham uma fonte de alimentação e um comutador de rede comum. No Azure, máquinas virtuais de saudação em um conjunto de disponibilidade são automaticamente separadas em vários domínios de falha.  
Consulte [gerenciar Olá disponibilidade de máquinas virtuais do Windows](virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ou [gerenciar Olá disponibilidade das máquinas virtuais Linux](virtual-machines/linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)  

## <a name="geo"></a>área geográfica
Um limite definido para a residência dos dados e que geralmente contém duas ou mais regiões. limites de saudação podem estar dentro de ou além das bordas nacionais e são influenciados pelo regulamentação do imposto. Cada área geográfica tem pelo menos uma região. Entre os exemplos de áreas geográficas estão Pacífico Asiático e Japão. Também é chamada de *geografia*.  
Veja [Regiões do Azure](best-practices-availability-paired-regions.md)

## <a name="geo-replication"></a>replicação geográfica
processo de saudação de replicação automaticamente conteúdo como blobs, tabelas e filas dentro de um par regional.  
Veja [Replicação Geográfica Ativa para o Banco de Dados SQL do Azure](sql-database/sql-database-geo-replication-overview.md)
<!-- hello meaning of "geo" in this term seems toobe different than hello meaning provided in hello "geo" entry -->

## <a name="image"></a>imagem
Um arquivo que contém o sistema operacional de saudação e configuração de aplicativo que pode ser usado toocreate qualquer número de máquinas virtuais. No Azure, há dois tipos de imagens: a imagem da VM e a imagem do SO. Uma imagem de VM inclui um sistema operacional e todos os discos anexados tooa VM quando Olá imagem é criada. Uma imagem do SO contém apenas um sistema operacional generalizado sem qualquer configuração de disco de dados.  
Consulte [navegue e selecionadas imagens de máquinas virtuais do Windows no Azure com o PowerShell ou hello CLI](virtual-machines/windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="limits"></a>limites
número de saudação de recursos que podem ser criados ou Olá parâmetro de comparação de desempenho que pode ser obtido. Geralmente, os limites estão associados a assinaturas, serviços e ofertas.  
Veja [Assinatura do Azure e limites de serviços, cotas e restrições](azure-subscription-service-limits.md)

## <a name="load-balancer"></a>balanceador de carga
Um recurso que distribui o tráfego recebido entre computadores em uma rede. No Azure, um balanceador de carga distribui máquinas do tráfego toovirtual definidas em um conjunto de Balanceador de carga. Um [balanceador de carga](load-balancer/load-balancer-overview.md) pode ser voltado à Internet ou interno.  

## <a name="mobile-app"></a>aplicativo móvel
Outro nome para o [Aplicativo de Serviço de Aplicativo](#app-service-app).

## <a name="offer"></a>oferta
saudação de preços, créditos e tooan aplicáveis de termos relacionados a assinatura do Azure.  
Consulte Olá [página de detalhes da oferta do Azure](https://azure.microsoft.com/support/legal/offer-details/)

## <a name="portal"></a>portal
portal da web segura de saudação usado toodeploy e gerenciar os serviços do Azure.  Há dois portais: Olá [portal do Azure](http://portal.azure.com/) e hello [portal clássico](http://manage.windowsazure.com/). Alguns serviços estão disponíveis em ambos os portais, enquanto outros só estão disponíveis em uma ou Olá outros. Olá [gráfico de disponibilidade do portal do Azure](https://azure.microsoft.com/features/azure-portal/availability/) listas quais serviços estão disponíveis no portal que.

## <a name="region"></a>region
Uma área dentro de uma área geográfica que não ultrapassa fronteiras nacionais e contém um ou mais datacenters. Preços, serviços regionais e tipos de oferta são expostos no nível de região hello. Normalmente, uma região é emparelhada com outra região, que pode ser o tooseveral centenas milhas de distância. Os pares regionais podem ser usados como um mecanismo para cenários de alta disponibilidade e de recuperação de desastres. Também chamado tooas *local*.  
Veja [Regiões do Azure](best-practices-availability-paired-regions.md)

## <a name="resource"></a>recurso
Um item que faz parte de sua solução do Azure. Cada serviço do Azure permite que você toodeploy diferentes tipos de recursos, como bancos de dados ou máquinas virtuais.   
Veja [Visão geral do Azure Resource Manager](azure-resource-manager/resource-group-overview.md)

## <a name="resource-group"></a>grupo de recursos
Um contêiner no Resource Manager que armazena os recursos relacionados para um aplicativo. grupo de recursos de saudação pode incluir todos os recursos de saudação para um aplicativo ou apenas os recursos que são agrupados logicamente. Você pode decidir como deseja que os recursos de tooallocate tooresource grupos com base no que torna hello mais sentido para sua organização.  
Veja [Visão geral do Azure Resource Manager](azure-resource-manager/resource-group-overview.md)

## <a name="arm-template"></a>modelo do Resource Manager
Um arquivo JSON que declarativamente define um ou mais recursos do Azure e que define dependências entre hello recursos implantados. modelo de saudação pode ser usado toodeploy Olá recursos consistente e repetidamente.  
Veja [Criando modelos do Azure Resource Manager](resource-group-authoring-templates.md)

## <a name="resource-provider"></a>provedor de recursos
Um serviço que fornece recursos de saudação, você pode implantar e gerenciar por meio do Gerenciador de recursos. Cada provedor de recursos oferece operações para trabalhar com recursos de saudação que são implantados. Provedores de recursos podem ser acessados por meio de saudação portal do Azure, o PowerShell do Azure e vários SDKs de programação.  
Veja [Visão geral do Azure Resource Manager](azure-resource-manager/resource-group-overview.md)

## <a name="role"></a>função
Um meio para controlar o acesso que pode ser atribuído toousers, grupos e serviços. As funções são tooperform capaz de ações como criar, gerenciar e lidos em recursos do Azure.  
Veja [RBAC: funções internas](active-directory/role-based-access-built-in-roles.md)

## <a name="sla"></a>SLA (contrato de nível de serviço)
contrato de saudação que descreve o compromisso da Microsoft para o tempo de atividade e conectividade. Cada serviço do Azure tem um SLA específico.  
Veja [Contratos de Nível de Serviço](https://azure.microsoft.com/support/legal/sla/)

## <a name="sas"></a>assinatura de acesso compartilhado (SAS)
Uma assinatura que permite que recursos de tooa de acesso toogrant limitado, sem expor sua chave de conta. Por exemplo, [armazenamento do Azure usa SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) toogrant tooobjects de acesso de cliente, como blobs. [IoT Hub usa SAS](iot-hub/iot-hub-devguide-security.md#security-tokens) toogrant telemetria de toosend de permissão de dispositivos.

## <a name="storage-account"></a>do Azure
Uma conta que fornece acesso toohello serviços de Blob do Azure, fila, tabela e arquivo no armazenamento do Azure. o nome de conta de armazenamento Olá define Olá espaço para nome exclusivo para objetos de dados de armazenamento do Azure.  
Veja [Sobre as contas de armazenamento do Azure](storage/common/storage-create-storage-account.md)

## <a name="subscription"></a>subscription
Contrato do cliente com a Microsoft que permite que eles tooobtain do Azure services. Olá assinatura preços e termos relacionados são governados pelas oferta Olá escolhida para a assinatura de saudação.
Veja [Contrato de Assinatura do Microsoft Online](https://azure.microsoft.com/support/legal/subscription-agreement/) e [Como as assinaturas do Azure estão associadas ao Azure Active Directory](active-directory/active-directory-how-subscriptions-associated-directory.md)

## <a name="tag"></a>marca
Um termo de indexação que permite que você toocategorize recursos de acordo com os requisitos de tooyour para gerenciar ou de cobrança. Quando você tiver um conjunto complexo de recursos, você pode usar marcas toovisualize esses ativos de maneira Olá que faz mais sentido de saudação. Por exemplo, você pode marcar os recursos que servem para uma função semelhante em sua organização ou pertencem toohello mesmo departamento.  
Consulte [usando marcas tooorganize seus recursos do Azure](resource-group-using-tags.md)

## <a name="update-domain"></a>domínio de atualização
Olá coleção de máquinas virtuais em um conjunto de disponibilidade que são atualizados a saudação simultaneamente. Máquinas virtuais no hello mesmo domínio de atualização são reiniciados juntas durante a manutenção planejada. O Azure nunca reinicia mais de um domínio de atualização por vez. Também chamado tooas um domínio de atualização.  
Consulte [gerenciar Olá disponibilidade de máquinas virtuais do Windows](virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) e [gerenciar Olá disponibilidade das máquinas virtuais Linux](virtual-machines/linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="vm"></a>máquina virtual
Olá implementação de software de um computador físico que executa um sistema operacional. Várias máquinas virtuais pode executar simultaneamente no mesmo hardware de hello. No Azure, as máquinas virtuais estão disponíveis em vários tamanhos.  
Veja [Documentação de Máquinas Virtuais](https://azure.microsoft.com/documentation/services/virtual-machines/)

## <a name="vm-extension"></a>extensão da máquina virtual
Um recurso que implementa comportamentos ou recursos que o ajudam a outros programas de trabalho ou fornecem a capacidade de saudação para você toointeract com um computador em execução. Por exemplo, você pode usar Olá tooreset de extensão de acesso da máquina virtual ou modifique os valores de acesso remoto em uma máquina virtual do Azure.
<!-- This definition seems obscure toome; maybe a list of examples would work better than a conceptual definition? -->
Veja [Sobre os recursos e extensões de máquina virtual (Windows)](virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ou [Sobre os recursos e extensões de máquina virtual (Linux)](virtual-machines/linux/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="vnet"></a>rede virtual
Uma rede que fornece conectividade entre seus recursos do Azure que estão isolados de todos os outros locatários do Azure. Um [Gateway de VPN do Azure](vpn-gateway/vpn-gateway-about-vpngateways.md) lhe permite estabelecer conexões entre redes virtuais e [entre uma rede virtual e uma rede local](vpn-gateway/vpn-gateway-plan-design.md). Você pode controlar totalmente blocos de endereços IP hello, configurações de DNS, políticas de segurança e tabelas de rotas em uma rede virtual.  
Veja [Visão geral da Rede Virtual](virtual-network/virtual-networks-overview.md)  

## <a name="web-app"></a>Aplicativo Web
Outro nome para o [Aplicativo de Serviço de Aplicativo](#app-service-app).

## <a name="see-also"></a>Consulte também

* [Introdução ao Azure](https://azure.microsoft.com/get-started/)
* [Centro de Recurso de Nuvem](https://azure.microsoft.com/resources/)  
* [Azure para seus aplicativos de negócios](https://azure.microsoft.com/overview/business-apps-on-azure/)
* [Azure em seu datacenter](https://azure.microsoft.com/overview/business-apps-on-azure/)

