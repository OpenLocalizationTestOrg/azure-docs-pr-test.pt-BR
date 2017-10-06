---
title: aaaDeploy um balanceador de carga para a Internet com o IPv6 - modelo do Azure | Microsoft Docs
description: "Como toodeploy IPv6 dão suporte ao balanceador de carga do Azure e VMs com balanceamento de carga."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-resource-manager
keywords: "ipv6, azure load balancer, pilha dual, ip público, ipv6 nativo, móvel, iot"
ms.assetid: 2998e943-13fc-4ea9-a68c-875e53a08db3
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2016
ms.author: kumud
ms.openlocfilehash: 68b9ba874a50161243577b64c4a6d9c76b39156c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-internet-facing-load-balancer-solution-with-ipv6-using-a-template"></a>Implantar uma solução de balanceamento de carga voltada para a Internet com IPv6 usando um modelo

> [!div class="op_single_selector"]
> * [PowerShell](load-balancer-ipv6-internet-ps.md)
> * [CLI do Azure](load-balancer-ipv6-internet-cli.md)
> * [Modelo](load-balancer-ipv6-internet-template.md)

Um Azure Load Balancer é um balanceador de carga de Camada 4 (TCP, UDP). o balanceador de carga Olá fornece alta disponibilidade através da distribuição de tráfego de entrada entre instâncias do serviço de integridade em serviços de nuvem ou máquinas virtuais em um conjunto de Balanceador de carga. O Azure Load Balancer também pode apresentar esses serviços em várias portas, vários endereços IP ou ambos.

## <a name="example-deployment-scenario"></a>Exemplo de cenário de implantação

Olá, diagrama a seguir ilustra Olá solução balanceamento de carga que está sendo implantado usando o modelo de exemplo hello descrito neste artigo.

![Cenário com o balanceador de carga](./media/load-balancer-ipv6-internet-template/lb-ipv6-scenario.png)

Nesse cenário, você criará hello Azure recursos a seguir:

* uma interface de rede virtual para cada VM com endereços IPv4 e IPv6 atribuídos
* um balanceador de carga voltado para a Internet com um IPv4 e um endereço IP público IPv6
* dois carregar balanceamento regras toomap Olá VIPs toohello privados pontos de extremidade públicos
* um conjunto de disponibilidade que contém Olá duas VMs
* duas VMs (máquinas virtuais)

## <a name="deploying-hello-template-using-hello-azure-portal"></a>Implantando o modelo hello usando Olá portal do Azure

Este artigo faz referência a um modelo que é publicado no hello [modelos de início rápido do Azure](https://azure.microsoft.com/documentation/templates/201-load-balancer-ipv6-create/) Galeria. Você pode baixar o modelo de saudação da Galeria de saudação ou iniciar a implantação de saudação no Azure diretamente da Galeria de saudação. Este artigo pressupõe que você baixou o computador local do hello modelo tooyour.

1. Abra Olá portal do Azure e entre com uma conta que tenha permissões toocreate VMs e recursos de rede dentro de uma assinatura do Azure. Além disso, a menos que você está usando recursos existentes, conta Olá precisa de permissão toocreate um grupo de recursos e uma conta de armazenamento.
2. Clique em "+ novo" do menu hello e digite "modelo" na caixa de pesquisa de saudação. Selecione "Implantação de modelo" hello dos resultados da pesquisa.

    ![lb-ipv6-portal-step2](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step2.png)

3. Em Olá tudo folha, clique em "Implantação de modelo".

    ![lb-ipv6-portal-step3](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step3.png)

4. Clique em "Criar".

    ![lb-ipv6-portal-step4](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step4.png)

5. Clique em "Editar modelo". Excluir o conteúdo existente de saudação e copiar/colar em todo o conteúdo do arquivo de modelo de Olá Olá (tooinclude Olá iniciar e terminar com {}), em seguida, clique em "Salvar".

    > [!NOTE]
    > Se você estiver usando o Microsoft Internet Explorer, quando você cola você receber uma caixa de diálogo solicitando que você tooallow acesso toohello Windows da área de transferência. Clique em "Permitir acesso".

    ![lb-ipv6-portal-step5](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step5.png)

6. Clique em "Editar parâmetros". Na folha de parâmetros hello, especificar valores hello segundo as diretrizes de Olá Olá seção de parâmetros de modelo, clique em "Salvar" tooclose Olá parâmetros folha. Na folha de implantação personalizada hello, selecione sua assinatura, um grupo de recursos existente ou crie um. Se você estiver criando um grupo de recursos, em seguida, selecione um local para o grupo de recursos de saudação. Em seguida, clique em **termos legais**, em seguida, clique em **compra** para os termos legais hello. Azure começa a implantar recursos de saudação. Ele usa várias toodeploy de minutos todos os recursos de saudação.

    ![lb-ipv6-portal-step6](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step6.png)

    Para obter mais informações sobre esses parâmetros, consulte Olá [variáveis e parâmetros do modelo](#template-parameters-and-variables) seção mais adiante neste artigo.

7. recursos de saudação toosee criados pelo modelo hello, clique em Procurar, role para baixo na lista de saudação até que você consulte "Grupos de recursos" e clique em.

    ![lb-ipv6-portal-step7](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step7.png)

8. Na folha de grupos de recursos hello, clique em nome Olá Olá do grupo de recursos especificado na etapa 6. Você ver uma lista de todos os recursos de saudação que foram implantados. Caso tudo tenha corrido bem, deverá aparecer "Êxito" em "Última implantação". Caso contrário, verifique se você estiver usando de conta de Olá tem permissões toocreate Olá recursos.

    ![lb-ipv6-portal-step8](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step8.png)

    > [!NOTE]
    > Se você procurar os grupos de recursos imediatamente após a conclusão da etapa 6, "Última implantação" exibirá status hello "Implantação" enquanto Olá recursos estão sendo implantados.

9. Clique em "myIPv6PublicIP" na lista de saudação de recursos. Você verá que ele tem um endereço IPv6 em endereço IP e seu nome DNS é valor Olá especificado para o parâmetro de dnsNameforIPv6LbIP Olá na etapa 6. Esse recurso é Olá público IPv6 endereço e nome do host que é acessíveis tooInternet-os clientes.

    ![lb-ipv6-portal-step9](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step9.png)

## <a name="validate-connectivity"></a>Validar a conectividade

Quando o modelo de saudação tiver implantado com êxito, você pode validar conectividade Concluindo Olá tarefas a seguir:

1. Entrar toohello portal do Azure e conecte-se tooeach de saudação máquinas virtuais criadas pela implantação de modelo hello. Se você implantou uma VM do Windows Server, execute ipconfig /all a partir de um prompt de comando. Você verá que VMs Olá tenham endereços IPv4 e IPv6. Se você implantou máquinas virtuais do Linux, você precisa tooconfigure Olá SO Linux tooreceive dinâmicos endereços IPv6 usando instruções Olá fornecidas para a distribuição de Linux.
2. Em um cliente conectado à Internet IPv6, inicie um conexão toohello IPv6 endereço saudação do balanceador de carga. balanceamento entre Olá duas VMs de tooconfirm que Olá balanceador de carga, você pode instalar um servidor web como o Microsoft Internet Information Services (IIS) em cada uma das VMs hello. página de web saudação padrão em cada servidor pode conter texto hello "Server0" ou "Server1" toouniquely identificá-lo. Em seguida, abra um navegador da Internet em um cliente conectado à Internet IPv6 e procurar o nome do host toohello especificado para o parâmetro de dnsNameforIPv6LbIP de saudação do hello carga balanceador tooconfirm ponta a ponta IPv6 conectividade tooeach VM. Se você vir apenas página da web de saudação de apenas um servidor, talvez seja necessário tooclear o cache do navegador. Abra várias sessões de navegação privadas. Você verá uma resposta de cada servidor.
3. Em um cliente conectado à Internet IPv4, inicie um endereço de IPv4 público do conexão toohello saudação do balanceador de carga. tooconfirm que Olá balanceador de carga é o balanceamento de carga Olá duas VMs, você poderia testar usando o IIS, conforme detalhado na etapa 2.
4. De cada VM, inicie uma conexão de saída tooan IPv6 ou dispositivo de Internet IPv4 conectados. Em ambos os casos, o IP de origem do hello visto pelo dispositivo de destino Olá for Olá público endereço IPv4 ou IPv6 saudação do balanceador de carga.

> [!NOTE]
> ICMP para IPv4 e IPv6 é bloqueada em Olá rede do Azure. Como resultado, as ferramentas ICMP, como ping, sempre falham. conectividade tootest, use uma alternativa TCP como TCPing ou Olá cmdlet do PowerShell Test-NetConnection. Observe que os endereços IP hello mostrados no diagrama de saudação são exemplos de valores que você pode ver. Como os endereços IPv6 de saudação são atribuídos dinamicamente, endereços Olá que receber serão diferentes e podem variar por região. Além disso, é comum Olá público endereço IPv6 Olá toostart de Balanceador de carga com um prefixo diferente de Olá endereços IPv6 no pool de back-end de saudação.

## <a name="template-parameters-and-variables"></a>Variáveis e parâmetros de modelo

Um modelo do Gerenciador de recursos do Azure contém diversas variáveis e parâmetros que você pode personalizar tooyour necessidades. Variáveis são usadas para que você não deseja que um usuário toochange de valores fixos. Parâmetros são usados para valores que você deseja tooprovide um usuário ao implantar o modelo de saudação. modelo de exemplo Hello está configurado para o cenário de saudação descrito neste artigo. Você pode personalizar essa tooneeds do seu ambiente.

exemplo Hello modelo usado neste artigo inclui o seguinte Olá variáveis e parâmetros:

| Parâmetro/variável | Observações |
| --- | --- |
| adminUsername |Especifica nome de saudação da conta de administrador de saudação usado toosign em máquinas virtuais de toohello com. |
| adminPassword |Especifica senha Olá para conta de administrador Olá usado toosign em máquinas virtuais de toohello com. |
| dnsNameforIPv4LbIP |Especifique o nome de host DNS Olá desejar tooassign como nome público do Olá Olá do balanceador de carga. Esse nome é resolvido endereço de IPv4 público do balanceador de carga toohello. nome de Olá deve estar em minúsculas e corresponder Olá regex: ^ [a-z][a-z0-9-]{1,61}[a-z0-9]$. |
| dnsNameforIPv6LbIP |Especifique o nome de host DNS Olá desejar tooassign como nome público do Olá Olá do balanceador de carga. Esse nome é resolvido endereço de IPv6 público do balanceador de carga toohello. nome de Olá deve estar em minúsculas e corresponder Olá regex: ^ [a-z][a-z0-9-]{1,61}[a-z0-9]$. Isso pode ser Olá mesmo nome como Olá endereço IPv4. Quando um cliente envia uma consulta DNS para esse nome do Azure retornará Olá A e registros AAAA quando Olá nome é compartilhado. |
| vmNamePrefix |Especifique o prefixo do nome VM hello. modelo de saudação anexará um número (0, 1, etc.) toohello nome quando hello máquinas virtuais são criados. |
| nicNamePrefix |Especifique o prefixo do nome de interface de rede de saudação. modelo de saudação anexará um número (0, 1, etc.) toohello nome quando as interfaces de rede de saudação são criadas. |
| storageAccountName |Insira nome de saudação de uma conta de armazenamento existente ou especifique nome de saudação de um novo um toobe criados pelo modelo de saudação. |
| availabilitySetName |Insira o nome da disponibilidade de saudação definido toobe usado com hello VMs |
| addressPrefix |prefixo de endereço Olá usado intervalo de endereços de saudação toodefine de saudação rede Virtual |
| subnetName |nome de saudação da sub-rede de saudação em criado para Olá VNet |
| subnetPrefix |prefixo de endereço Olá usado toodefine intervalo de endereços de saudação da sub-rede Olá |
| vnetName |Especifique nome Olá Olá redes usadas por Olá VMs. |
| ipv4PrivateIPAddressType |método de alocação Hello usado Olá privada endereço IP (estática ou dinâmica) |
| ipv6PrivateIPAddressType |método de alocação Hello usado Olá privada endereço IP (dinâmico). IPv6 só dá suporte à alocação dinâmica. |
| numberOfInstances |número de saudação de carga balanceada instâncias implantadas pelo modelo Olá |
| ipv4PublicIPAddressName |Especifique o nome DNS de saudação desejado toocommunicate toouse com o endereço IPv4 público de Olá Olá do balanceador de carga. |
| ipv4PublicIPAddressType |método de alocação Hello usado para o endereço IP público hello (estática ou dinâmica) |
| Ipv6PublicIPAddressName |Especifique o nome DNS de saudação desejado toocommunicate toouse com o endereço de IPv6 público Olá Olá do balanceador de carga. |
| ipv6PublicIPAddressType |método de alocação Hello usado para o endereço IP público hello (dinâmico). IPv6 só dá suporte à alocação dinâmica. |
| lbName |Especifique o nome de Olá Olá do balanceador de carga. Esse nome é exibido no portal de saudação ou usado para se referir a tooit com um comando CLI ou o PowerShell. |

variáveis de saudação restantes no modelo de saudação contêm valores derivados que são atribuídos quando o Azure cria recursos Olá. Não altere essas variáveis.
