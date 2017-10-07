---
title: controle de acesso de suporte ao firewall de banco de dados do Cosmos aaaAzure & IP | Microsoft Docs
description: "Saiba como suportam a políticas de controle de acesso toouse IP para o firewall em contas de banco de dados do banco de dados do Azure Cosmos."
keywords: Controle de acesso de IP, suporte ao firewall
services: cosmos-db
author: shahankur11
manager: jhubbard
editor: 
tags: azure-resource-manager
documentationcenter: 
ms.assetid: c1b9ede0-ed93-411a-ac9a-62c113a8e887
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: ankshah
ms.openlocfilehash: b5cdbdb28e9d7ee0fd0ea54aad277167b699929f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-firewall-support"></a>Suporte ao firewall do Azure Cosmos DB
toosecure dados armazenados em uma conta de banco de dados do banco de dados do Azure Cosmos Cosmos do Azure DB forneceu suporte para um segredo com base em [modelo de autorização](https://msdn.microsoft.com/library/azure/dn783368.aspx) que utiliza um código de autenticação de alta segurança de mensagens baseada em Hash (HMAC). Agora, além de segredo toohello com base em modelo de autorização, o banco de dados do Azure Cosmos dá suporte à política controlada por controles de acesso baseado em IP para suporte de firewall de entrada. Esse modelo é muito semelhante regras de firewall toohello de um sistema de banco de dados tradicional e fornece um nível adicional de segurança toohello conta de banco de dados do banco de dados do Azure Cosmos. Com esse modelo, você pode agora configurar toobe de conta de banco de dados um banco de dados do Azure Cosmos acessível somente a partir de um conjunto aprovado das máquinas e/ou serviços em nuvem. Acessar recursos de banco de dados do Cosmos de tooAzure desses conjuntos aprovados de serviços e máquinas exigirão Olá chamador toopresent um token de autorização válido.

## <a name="ip-access-control-overview"></a>Visão geral do controle de acesso de IP
Por padrão, uma conta de banco de dados do banco de dados do Azure Cosmos é acessível pela internet pública, como solicitação de saudação é acompanhada por um token de autorização válido. tooconfigure controle de acesso baseado em política IP, o usuário Olá deve fornecer o conjunto de saudação de endereços IP ou intervalos de endereços IP no toobe de formulário CIDR incluídos como Olá permitido a lista de IPs de cliente para uma conta de banco de dados especificado. Quando essa configuração for aplicada, todas as solicitações originadas máquinas fora essa lista permitida serão bloqueadas pelo servidor de saudação.  conexão Olá fluxo de processamento para hello controle de acesso baseado em IP está descrito nos Olá diagrama a seguir.

![Diagrama mostrando o processo de conexão Olá para controle de acesso baseado em IP](./media/firewall-support/firewall-support-flow.png)

## <a name="connections-from-cloud-services"></a>Conexões dos serviços de nuvem
No Azure, os serviços de nuvem são uma maneira muito comum de hospedar a lógica do serviço de camada intermediária usando o Azure Cosmos DB. tooenable acesso tooan conta de banco de dados do banco de dados do Azure Cosmos de um serviço de nuvem, o endereço IP público de Olá Olá do serviço de nuvem deve ser adicionado toohello permitido a lista de endereços IP associados à sua conta de banco de dados do banco de dados do Azure Cosmos por [Configurando Olá política de controle de acesso IP](#configure-ip-policy).  Isso garante que todas as instâncias de função dos serviços de nuvem tenham acesso tooyour conta de banco de dados do banco de dados do Azure Cosmos. Você pode recuperar endereços IP para os serviços de nuvem em Olá portal do Azure, conforme mostrado no hello captura de tela a seguir.

![Captura de tela mostrando o endereço IP público de saudação para um serviço de nuvem exibido no portal do Azure de saudação](./media/firewall-support/public-ip-addresses.png)

Quando você expandir seu serviço de nuvem adicionando instâncias de função adicionais, essas novas instâncias terão conta de banco de dados do access toohello Azure Cosmos DB automaticamente desde que fazem parte da saudação mesmo serviço de nuvem.

## <a name="connections-from-virtual-machines"></a>Conexões de máquinas virtuais
[Máquinas virtuais](https://azure.microsoft.com/services/virtual-machines/) ou [conjuntos de escala de máquina virtual](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) também pode ser usado toohost serviços de camada intermediária usando o banco de dados do Azure Cosmos.  Olá tooconfigure acesso à tooallow de conta de banco de dados do banco de dados do Azure Cosmos de máquinas virtuais, os endereços IP públicos de máquina virtual e/ou conjunto de escalas da máquina virtual deve ser configurado como uma saudação endereços IP para a sua conta de banco de dados do banco de dados do Azure Cosmos por permitidos [configurar política de controle de acesso IP hello](#configure-ip-policy). Você pode recuperar endereços IP para máquinas virtuais no hello portal do Azure, conforme mostrado no hello captura de tela a seguir.

![Captura de tela mostrando um endereço IP público para uma máquina virtual exibida em Olá portal do Azure](./media/firewall-support/public-ip-addresses-dns.png)

Quando você adiciona o grupo de toohello de instâncias de máquinas virtuais adicionais, eles são fornecidos automaticamente conta de banco de dados do access tooyour Azure Cosmos DB.

## <a name="connections-from-hello-internet"></a>Olá de conexões da internet
Quando você acessa um banco de dados do Azure Cosmos conta banco de dados de um computador em hello da internet, hello endereço IP do cliente ou o intervalo de endereços IP da máquina Olá deve ser adicionado toohello lista de endereços IP do hello conta de banco de dados do banco de dados do Azure Cosmos permitido. 

## <a id="configure-ip-policy"></a>Configurar política de controle de acesso IP Olá
política de controle de acesso IP Hello pode ser definida em Olá portal do Azure, ou programaticamente por meio [CLI do Azure](cli-samples.md), [Azure Powershell](powershell-samples.md), ou hello [API REST](/rest/api/documentdb/) atualizando Olá `ipRangeFilter` propriedade. Os intervalos/endereços IP devem ser separados por vírgula e não devem conter espaços. Exemplo: "13.91.6.132,13.91.6.1/24". Ao atualizar sua conta do banco de dados por meio desses métodos, ser toopopulate-se de que todos os Olá propriedades tooprevent redefinir as configurações de toodefault.

> [!NOTE]
> Habilitando uma política de controle de acesso IP para sua conta de banco de dados do banco de dados do Azure Cosmos, todo acesso tooyour conta de banco de dados do banco de dados do Azure Cosmos máquinas fora Olá configurado permitido lista de intervalos de endereços IP estão bloqueados. Em virtude de nesse modelo, a navegação de operação de plano de dados de saudação do portal de saudação também será bloqueado tooensure Olá integridade de controle de acesso.

desenvolvimento de toosimplify, Olá portal do Azure ajuda a identificar e adicionar IP de saudação do seu toohello de máquina do cliente, lista de permitidos para que aplicativos em execução de seu computador podem acessar Olá conta de banco de dados do Azure Cosmos. Observe que Olá endereço IP do cliente aqui é detectado como visto pelo portal de saudação. Ele pode ser um endereço IP do cliente de saudação do seu computador, mas também pode ser um endereço IP de saudação do seu gateway de rede. Não se esqueça de tooremove antes tooproduction contínuo.

política de controle de acesso tooset Olá IP em Olá portal do Azure, navegue folha de conta do banco de dados do Azure Cosmos toohello, clique em **Firewall** no menu de navegação hello, em seguida, clique em **ON** 

![Captura de tela mostrando como tooopen Olá folha de Firewall no hello portal do Azure](./media/firewall-support/azure-portal-firewall.png)

No painel de novo hello, especifique se hello portal do Azure pode acessar a conta de hello, adicione outros intervalos e endereços conforme apropriado e clique em **salvar**.  

> [!NOTE]
> Quando você habilita uma política de controle de acesso IP, é necessário o endereço IP de saudação do tooadd para Olá acesso toomaintain portal do Azure. Olá portais endereços IP são:
> |Região|Endereço IP|
> |------|----------|
> |Todas as regiões, exceto aquelas especificadas abaixo| 104.42.195.92|
> |Alemanha|51.4.229.218|
> |China|139.217.8.252|
> |Governo dos EUA do Arizona|52.244.48.71|
>

![Captura de tela mostrando um como configurações de firewall tooconfigure em Olá portal do Azure](./media/firewall-support/azure-portal-firewall-configure.png)

## <a name="troubleshooting-hello-ip-access-control-policy"></a>Solucionando problemas de política de controle de acesso IP Olá
### <a name="portal-operations"></a>Operações no Portal
Habilitando uma política de controle de acesso IP para sua conta de banco de dados do banco de dados do Azure Cosmos, todo acesso tooyour conta de banco de dados do banco de dados do Azure Cosmos máquinas fora Olá configurado permitido lista de intervalos de endereços IP estão bloqueados. Portanto, se você quiser tooenable dados portal plano operações, como coleções e documentos de consulta de navegação, você precisa tooexplicitly permitir acesso ao portal do Azure usando Olá **Firewall** folha no portal de saudação. 

![Captura de tela mostrando um como tooenable acesso toohello portal do Azure](./media/firewall-support/azure-portal-access-firewall.png)

### <a name="sdk--rest-api"></a>SDK e API Rest
Para motivos de segurança, o acesso por meio de SDK ou a API REST de máquinas não Olá lista de permitidos retornará uma genérico 404 não encontrado resposta sem detalhes adicionais. Verifique se o que IP hello permitido lista configurada seu banco de dados do Azure Cosmos banco de dados conta tooensure Olá correta de configuração de política é aplicada tooyour conta de banco de dados do banco de dados do Azure Cosmos.

## <a name="next-steps"></a>Próximas etapas
Para obter informações sobre dicas de desempenho relacionadas à rede, consulte [Dicas de desempenho](performance-tips.md).

