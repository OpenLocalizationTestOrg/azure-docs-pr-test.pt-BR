---
title: aaaMigrate VMs tooResource Manager usando a CLI do Azure | Microsoft Docs
description: "Este artigo o orienta por meio da migração de suporte de plataforma de saudação de recursos de tooAzure clássico Gerenciador de recursos usando a CLI do Azure"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d6f5a877-05b6-4127-a545-3f5bede4e479
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 0b11f4bb1b4658b3e88bf7629147ed953b678556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-iaas-resources-from-classic-tooazure-resource-manager-by-using-azure-cli"></a>Migrar recursos de IaaS de tooAzure clássico Gerenciador de recursos usando a CLI do Azure
Estas etapas mostram como toouse interface de linha de comando (CLI) do Azure comandos toomigrate infraestrutura como um recurso de serviço (IaaS) do modelo de implantação do hello implantação clássica modelo toohello Gerenciador de recursos do Azure. artigo Olá requer Olá [CLI do Azure](../../cli-install-nodejs.md).

> [!NOTE]
> Todas as operações de saudação descritas aqui são idempotentes. Se você tiver um problema que não seja um recurso sem suporte ou um erro de configuração, é recomendável que você repita Olá preparar, anular ou confirmar a operação. plataforma de saudação tente novamente a ação de saudação.
> 
> 

<br>
Aqui está uma ordem de saudação do fluxograma tooidentify nos quais etapas precisam toobe executado durante o processo de migração

![Captura de tela que mostra as etapas de migração de saudação](../windows/media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-prepare-for-migration"></a>Etapa 1: preparar para a migração
Aqui estão algumas práticas recomendadas que recomendamos durante a avaliação de migração de recursos de IaaS do clássico tooResource Manager:

* Leia Olá [lista de configurações sem suporte ou recursos](../windows/migration-classic-resource-manager-overview.md). Se você tiver máquinas virtuais que usam recursos ou configurações sem suporte, é recomendável que você aguarde toobe de suporte de configuração do recurso Olá anunciada. Como alternativa, você pode remover esse recurso ou sai migração configuração tooenable se ele atende às suas necessidades.
* Se você tiver automatizado scripts que implantar a infraestrutura e os aplicativos de hoje, tente toocreate uma configuração de teste semelhante usando esses scripts para a migração. Como alternativa, você pode configurar ambientes de exemplo usando Olá portal do Azure.

> [!IMPORTANT]
> Os Gateways de aplicativos não têm suporte atualmente para a migração de clássico tooResource Manager. toomigrate uma rede virtual clássica com um gateway de aplicativo, remova gateway Olá antes de executar uma rede Olá de toomove de operação de preparação. Depois de concluir a migração de hello, reconecte gateway Olá no Gerenciador de recursos do Azure. 
>
>Gateways de rota expressa conectando tooExpressRoute circuitos em outra assinatura não podem ser migrados automaticamente. Nesses casos, remover o gateway de rota expressa hello, migrar a rede virtual hello e recrie o gateway hello. Consulte [ExpressRoute migrar circuitos e associadas a redes virtuais do modelo de implantação do Gerenciador de recursos de toohello clássico de Olá](../../expressroute/expressroute-migration-classic-resource-manager.md) para obter mais informações.
> 
> 

## <a name="step-2-set-your-subscription-and-register-hello-provider"></a>Etapa 2: Definir sua assinatura e registrar o provedor de saudação
Para cenários de migração, você precisa tooset seu ambiente para ambos os clássico e o Gerenciador de recursos. [Instale a CLI do Azure](../../cli-install-nodejs.md) e [selecione sua assinatura](../../xplat-cli-connect.md).

Conta de logon tooyour.

    azure login

Selecione Olá assinatura do Azure usando o comando a seguir de saudação.

    azure account set "<azure-subscription-name>"

> [!NOTE]
> O registro é uma hora de uma etapa mas precisa toobe feito uma vez antes de tentar a migração. Sem registrar, você verá Olá a seguinte mensagem de erro 
> 
> *BadRequest: a assinatura não está registrada para migração.* 
> 
> 

Registrar com o provedor de recursos de migração de saudação usando o comando a seguir de saudação. Observe que, em alguns casos, esse comando atinge o tempo limite. No entanto, o registro de saudação será bem-sucedida.

    azure provider register Microsoft.ClassicInfrastructureMigrate

Aguarde cinco minutos para Olá toofinish de registro. Você pode verificar o status de saudação de aprovação de saudação usando o comando a seguir de saudação. Verifique se RegistrationState é `Registered` antes de continuar.

    azure provider show Microsoft.ClassicInfrastructureMigrate

Agora, alterne CLI toohello `asm` modo.

    azure config mode asm

## <a name="step-3-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-hello-azure-region-of-your-current-deployment-or-vnet"></a>Etapa 3: Verifique se que você tem suficiente núcleos de máquina Virtual do Azure Resource Manager no hello região do Azure de sua implantação atual ou a rede virtual
Para esta etapa será necessário tooswitch muito`arm` modo. Fazer isso com o comando a seguir de saudação.

```
azure config mode arm
```

Você pode usar o hello CLI comando toocheck Olá quantidade atual de núcleos que você tem no Gerenciador de recursos do Azure a seguir. toolearn mais sobre cotas de core, consulte [limites e hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)

```
azure vm list-usage -l "<Your VNET or Deployment's Azure region"
```

Quando terminar de verificar se esta etapa, você pode alternar de volta muito`asm` modo.

    azure config mode asm


## <a name="step-4-option-1---migrate-virtual-machines-in-a-cloud-service"></a>Etapa 4: Opção 1 – Migrar máquinas virtuais em um serviço de nuvem
Obter uma lista de serviços de nuvem usando o comando a seguir de saudação e, em seguida, escolha Olá serviço em nuvem que você deseja toomigrate hello. Observe que se Olá VMs no serviço de nuvem Olá está em uma rede virtual ou se eles têm funções web/de trabalho, você receberá uma mensagem de erro.

    azure service list

Olá execução após o nome da implantação do comando tooget Olá Olá serviço de nuvem de saída detalhada hello. Na maioria dos casos, nome da implantação Olá é Olá igual ao nome do serviço de nuvem hello.

    azure service show <serviceName> -vv

Primeiro, valide se você pode migrar o serviço de nuvem hello usando Olá comandos a seguir:

```shell
azure service deployment validate-migration <serviceName> <deploymentName> new "" "" ""
```

Prepare Olá VMs no serviço de nuvem Olá para migração. Você tem dois toochoose de opções do.

Se você quiser toomigrate Olá VMs tooa criado plataforma rede virtual, use Olá comando a seguir.

    azure service deployment prepare-migration <serviceName> <deploymentName> new "" "" ""

Se você quiser tooan toomigrate existentes de rede virtual no modelo de implantação do Gerenciador de recursos de hello, use Olá comando a seguir.

    azure service deployment prepare-migration <serviceName> <deploymentName> existing <destinationVNETResourceGroupName> <subnetName> <vnetName>

Depois de preparar Olá operação for bem-sucedida, você pode examinar o estado de migração de Olá Olá saída detalhada tooget de saudação VMs e certifique-se de que eles estejam em Olá `Prepared` estado.

    azure vm show <vmName> -vv

Verifique a configuração de saudação para Olá preparado recursos usando a CLI ou Olá portal do Azure. Se você não está pronto para migração e desejar toogo toohello back antigo estado, use Olá comando a seguir.

    azure service deployment abort-migration <serviceName> <deploymentName>

Se configuração preparada Olá parece bom, você pode Avançar e confirmar recursos hello usando o comando a seguir de saudação.

    azure service deployment commit-migration <serviceName> <deploymentName>



## <a name="step-4-option-2----migrate-virtual-machines-in-a-virtual-network"></a>Etapa 4: Opção 2 – Migrar máquinas virtuais em uma rede virtual
Escolha Olá rede virtual que você deseja toomigrate. Observe que, se a rede virtual Olá contém funções web/de trabalho ou máquinas virtuais com configurações sem suporte, você obterá uma mensagem de erro de validação.

Obter todas as redes virtuais de saudação na assinatura de saudação usando o comando a seguir de saudação.

    azure network vnet list

saída de Hello será parecida com isto:

![Captura de tela hello da linha de comando com o nome de toda a rede virtual Olá realçado.](../media/virtual-machines-linux-cli-migration-classic-resource-manager/vnet.png)

Em Olá exemplo acima, Olá **virtualNetworkName** é o nome completo da saudação **"Grupo classicubuntu16 classicubuntu16"**.

Primeiro, valide se migrar Olá rede virtual usando o comando a seguir de saudação:

```shell
azure network vnet validate-migration <virtualNetworkName>
```

Prepare a rede virtual Olá de sua escolha para a migração usando o comando a seguir de saudação.

    azure network vnet prepare-migration <virtualNetworkName>

Verifique a configuração de saudação para Olá preparado máquinas virtuais usando a CLI ou Olá portal do Azure. Se você não está pronto para migração e desejar toogo toohello back antigo estado, use Olá comando a seguir.

    azure network vnet abort-migration <virtualNetworkName>

Se configuração preparada Olá parece bom, você pode Avançar e confirmar recursos hello usando o comando a seguir de saudação.

    azure network vnet commit-migration <virtualNetworkName>

## <a name="step-5-migrate-a-storage-account"></a>Etapa 5: Migrar uma conta de armazenamento
Quando terminar de migração de máquinas virtuais Olá, é recomendável que migrar a conta de armazenamento hello.

Preparar a conta de armazenamento Olá para a migração usando o comando a seguir de saudação

    azure storage account prepare-migration <storageAccountName>

Verifique a configuração de saudação para Olá preparado conta de armazenamento usando a CLI ou Olá portal do Azure. Se você não está pronto para migração e desejar toogo toohello back antigo estado, use Olá comando a seguir.

    azure storage account abort-migration <storageAccountName>

Se configuração preparada Olá parece bom, você pode Avançar e confirmar recursos hello usando o comando a seguir de saudação.

    azure storage account commit-migration <storageAccountName>

## <a name="next-steps"></a>Próximas etapas

* [Visão geral da plataforma suportada migração de recursos de IaaS de tooAzure clássico Gerenciador de recursos](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Técnico mergulho profundo na plataforma suportada migração de clássico tooAzure Gerenciador de recursos](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Planejando a migração de recursos de IaaS de tooAzure clássico Gerenciador de recursos](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Usar recursos de IaaS PowerShell toomigrate de tooAzure clássico Gerenciador de recursos](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Ferramentas de comunidade para ajudar com a migração de recursos de IaaS de tooAzure clássico Gerenciador de recursos](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Examinar os erros de migração mais comuns](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Saudação de revisão mais perguntas frequentes sobre migração de recursos de IaaS do clássico tooAzure Gerenciador de recursos](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
