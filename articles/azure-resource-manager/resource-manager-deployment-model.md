---
title: "aaaResource Gerenciador e implantação clássica | Microsoft Docs"
description: "Descreve o modelo de implantação do hello diferenças entre o modelo de implantação do Gerenciador de recursos de saudação e Olá clássico (ou gerenciamento de serviço)."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 7ae0ffa3-c8da-4151-bdcc-8f4f69290fb4
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: tomfitz
ms.openlocfilehash: fbf1959991b100547a459bf88a29c0afbc8592e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-vs-classic-deployment-understand-deployment-models-and-hello-state-of-your-resources"></a>Azure Resource Manager versus implantação clássica: entender os modelos de implantação e Olá estado de seus recursos
Neste tópico, você aprenderá sobre o Gerenciador de recursos do Azure e modelos de implantação clássico, estado de saudação de seus recursos, e por que os recursos foram implantados com uma ou Olá outros. Olá Gerenciador de recursos e modelos de implantação clássico representam duas diferentes maneiras de implantar e gerenciar suas soluções do Azure. Trabalhar com eles por meio de dois conjuntos diferentes de API e recursos de saudação implantado podem conter diferenças importantes. Olá dois modelos não são totalmente compatíveis entre si. Este tópico descreve essas diferenças.

implantação de saudação toosimplify e gerenciamento de recursos, a Microsoft recomenda que você use o Gerenciador de recursos para todos os novos recursos. Se possível, a Microsoft recomenda que você reimplante os recursos existentes por meio do Gerenciador de Recursos.

Se você for novo tooResource Manager, convém terminologia de saudação de revisão toofirst definida no hello [visão geral do Gerenciador de recursos do Azure](resource-group-overview.md).

## <a name="history-of-hello-deployment-models"></a>Histórico de modelos de implantação de saudação
Somente o modelo de implantação clássico Olá originalmente fornecido pelo Azure. Nesse modelo, cada recurso existia independentemente; havia uma maneira toogroup recursos relacionados juntos. Em vez disso, você precisava toomanually controlar quais recursos constituídos de seu aplicativo ou solução e lembre-se de toomanage-los em uma abordagem de coordenada. toodeploy uma solução, você precisava tooeither criar cada recurso individualmente por meio do portal clássico do hello ou criar um script que todos os recursos de saudação na ordem correta, Olá implantados. toodelete uma solução, você precisava toodelete cada recurso individualmente. Não era possível aplicar e atualizar facilmente políticas de controle de acesso para recursos relacionados. Por fim, você não pode aplicar marcas tooresources toolabel-los com os termos que ajudarão-lo a monitoram seus recursos e gerenciar cobrança.

No 2014, o Azure introduziu o Gerenciador de recursos, que adicionado o conceito de saudação de um grupo de recursos. Um grupo de recursos é um contêiner de recursos que compartilham um ciclo de vida comum. modelo de implantação do Gerenciador de recursos de saudação oferece várias vantagens:

* Você pode implantar, gerenciar e monitorar todos os serviços de saudação para sua solução como um grupo, em vez de manipular esses serviços individualmente.
* Você pode implantar a solução repetidamente em todo seu ciclo de vida e com a confiança de que seus recursos serão implantados em um estado consistente.
* Você pode aplicar os recursos de tooall de controle de acesso em seu grupo de recursos, e essas políticas são aplicadas automaticamente quando novos recursos são adicionados toohello grupo de recursos.
* Você pode aplicar marcas tooresources toologically organizar todos os recursos de saudação em sua assinatura.
* Você pode usar a infraestrutura de saudação toodefine notação JSON (JavaScript Object) para sua solução. arquivo JSON de saudação é conhecido como um modelo do Gerenciador de recursos.
* Você pode definir dependências de saudação entre os recursos para que eles são implantados na ordem correta, Olá.

Quando o Gerenciador de recursos foi adicionado, todos os recursos retroativamente foram adicionados toodefault grupos de recursos. Se você criar um recurso por meio de implantação clássico agora, o recurso de saudação é criado automaticamente dentro de um grupo de recursos padrão para esse serviço, mesmo que você não especificar esse grupo de recursos na implantação. No entanto, apenas existentes em um grupo de recursos não significa que o recurso Olá foi modelo do Gerenciador de recursos de toohello convertido. Vamos examinar como a cada serviço lida com dois modelos de implantação Olá na próxima seção, Olá. 

## <a name="understand-support-for-hello-models"></a>Entender o suporte para modelos de saudação
Ao decidir qual toouse do modelo de implantação para os seus recursos, há três cenários toobe atento:

1. serviço de saudação dá suporte ao Gerenciador de recursos e fornece um único tipo.
2. Olá serviço dá suporte ao Gerenciador de recursos, mas fornece dois tipos - uma para o Gerenciador de recursos e outra para clássico. Esta situação se aplica apenas toovirtual máquinas, as contas de armazenamento e redes virtuais.
3. serviço de saudação não oferece suporte para o Gerenciador de recursos.

toodiscover se um serviço oferece suporte ao Gerenciador de recursos, consulte [provedores de recursos e tipos de](resource-manager-supported-services.md).

Se o serviço Olá desejar toouse não oferece suporte para Gerenciador de recursos, você deve continuar usando a implantação clássica.

Se o serviço Olá dá suporte ao Gerenciador de recursos e **não** uma máquina virtual, a conta de armazenamento ou a rede virtual, você pode usar o Gerenciador de recursos sem qualquer complicações.

Para máquinas virtuais, contas de armazenamento e redes virtuais, se o recurso de saudação foi criado por meio de implantação clássico, você deve continuar toooperate nela por meio de operações clássicas. Se a máquina virtual de saudação, a conta de armazenamento ou a rede virtual foi criada por meio do Gerenciador de recursos de implantação, você deve continuar usando o Gerenciador de recursos de operações. Essa distinção pode ficar confusa quando sua assinatura contiver uma mistura de recursos criada por meio do Resource Manager e da implantação clássica. Essa combinação de recursos pode criar resultados inesperados porque não dão suporte a recursos de Olá Olá mesmas operações.

Em alguns casos, um comando do Gerenciador de recursos pode recuperar informações sobre um recurso criado por meio de implantação clássico ou pode executar uma tarefa administrativa como mover um grupo de recursos de tooanother recurso clássico. No entanto, esses casos não devem dar a impressão de saudação tipo hello dá suporte a operações do Gerenciador de recursos. Por exemplo, suponhamos que você tenha um grupo de recursos que contenha uma máquina virtual que foi criada com implantação clássica. Se você executar Olá comando do PowerShell do Gerenciador de recursos a seguir:

```powershell
Get-AzureRmResource -ResourceGroupName ExampleGroup -ResourceType Microsoft.ClassicCompute/virtualMachines
```

Ele retorna a máquina virtual de saudação:

```powershell
Name              : ExampleClassicVM
ResourceId        : /subscriptions/{guid}/resourceGroups/ExampleGroup/providers/Microsoft.ClassicCompute/virtualMachines/ExampleClassicVM
ResourceName      : ExampleClassicVM
ResourceType      : Microsoft.ClassicCompute/virtualMachines
ResourceGroupName : ExampleGroup
Location          : westus
SubscriptionId    : {guid}
```

No entanto, Olá cmdlet do Gerenciador de recursos de **Get-AzureRmVM** retorna apenas as máquinas virtuais implantadas por meio do Gerenciador de recursos. Olá comando a seguir não retorna Olá máquina de virtual criada por meio de implantação clássico.

```powershell
Get-AzureRmVM -ResourceGroupName ExampleGroup
```

Somente os recursos criados por meio do Gerenciador de Recursos oferecem suporte a marcas. Você não pode aplicar marcas tooclassic recursos.

## <a name="resource-manager-characteristics"></a>Características do Gerenciador de Recursos
toohelp entender Olá dois modelos, vamos analisar as características de saudação dos tipos de Gerenciador de recursos:

* Criado por meio de saudação [portal do Azure](https://portal.azure.com/).
  
     ![Portal do Azure](./media/resource-manager-deployment-model/portal.png)
  
     Para computação, armazenamento e recursos de rede, você tem opção de saudação do uso de implantação do Gerenciador de recursos ou clássico. Selecione **Gerenciador de Recursos**.
  
     ![Implantação do Gerenciador de Recursos](./media/resource-manager-deployment-model/select-resource-manager.png)
* Criado com a versão do Gerenciador de recursos de saudação do hello cmdlets do PowerShell do Azure. Esses comandos têm o formato de saudação *AzureRmNoun verbo*.

  ```powershell
  New-AzureRmResourceGroupDeployment
  ```

* Criado por meio de saudação [API de REST do Gerenciador de recursos do Azure](https://docs.microsoft.com/rest/api/resources/) para operações REST.
* Criado por meio de comandos de CLI do Azure executados em Olá **arm** modo.
  
  ```azurecli
  azure config mode arm
  azure group deployment create
  ```

* não inclui o tipo de recurso Olá **(clássico)** em nome de saudação. Olá, imagem a seguir mostra o tipo de saudação como **conta de armazenamento**.
  
    ![aplicativo web](./media/resource-manager-deployment-model/resource-manager-type.png)

## <a name="classic-deployment-characteristics"></a>Características da implantação clássica
Você também pode saber o modelo de implantação clássico hello como modelo de gerenciamento de serviço de saudação.

Recursos criados em Olá implantação clássica modelo compartilhamento Olá características a seguir:

* Criado por meio de saudação [portal clássico](https://manage.windowsazure.com)
  
     ![Portal Clássico](./media/resource-manager-deployment-model/classic-portal.png)
  
     Ou, Olá portal do Azure e você especificar **clássico** implantação (de computação, armazenamento e rede).
  
     ![Implantação Clássica](./media/resource-manager-deployment-model/select-classic.png)
* Criado por meio da versão de gerenciamento de serviços de saudação do hello cmdlets do PowerShell do Azure. Esses nomes de comando tem o formato de saudação *AzureNoun verbo*.

  ```powershell
  New-AzureVM
  ```

* Criado por meio de saudação [API de REST de gerenciamento de serviço](https://msdn.microsoft.com/library/azure/ee460799.aspx) para operações REST.
* Criado por meio de comandos da CLI do Azure executados no modo **asm** .

  ```azurecli
  azure config mode asm
  azure vm create
  ```
   
* tipo de recurso de saudação inclui **(clássico)** em nome de saudação. Olá, imagem a seguir mostra o tipo de saudação como **conta de armazenamento (clássico)**.
  
    ![tipo clássico](./media/resource-manager-deployment-model/classic-type.png)

Você pode usar os recursos de toomanage portal do Azure de saudação que foram criados por meio de implantação clássico.

## <a name="changes-for-compute-network-and-storage"></a>Alterações de computação, rede e armazenamento
Olá diagrama a seguir exibe os recursos de computação, rede e armazenamento implantados por meio do Gerenciador de recursos.

![Arquitetura do Resource Manager](./media/resource-manager-deployment-model/arm_arch3.png)

Saudação de observação a seguir relações entre os recursos de saudação:

* Todos os recursos de saudação existirem dentro de um grupo de recursos.
* máquina virtual de saudação depende de uma conta de armazenamento específico definida em toostore de provedor de recursos de armazenamento Olá seus discos no blob de armazenamento (obrigatório).
* máquina virtual de saudação faz referência a uma NIC específica definida no provedor de recursos de rede hello (obrigatório) e um conjunto definido no provedor de recursos de computação de saudação (opcional) de disponibilidade.
* Olá NIC referências Olá máquina virtual atribuído o endereço IP (obrigatório), sub-rede Olá da rede virtual de saudação para máquina virtual de saudação (obrigatório) e tooa grupo de segurança de rede (opcional).
* subrede Olá em uma rede virtual faz referência a um grupo de segurança de rede (opcional).
* instância de Balanceador de carga Olá referencia o pool de back-end de saudação de endereços IP que incluem hello NIC de uma máquina virtual (opcional) e faz referência a um endereço balanceador de carga público ou privado IP (opcional).

Aqui estão Olá componentes e suas relações de implantação clássico:

![arquitetura clássica](./media/resource-manager-deployment-model/arm_arch1.png)

a solução clássico Olá para hospedar uma máquina virtual inclui:

* Um serviço de nuvem necessário que atua como contêiner para hospedar máquinas virtuais (computação). Máquinas virtuais são fornecidas automaticamente com uma placa de interface de rede (NIC) e um endereço IP atribuído pelo Azure. Além disso, o serviço de nuvem Olá contém uma instância do balanceador de carga externo, um endereço IP público e pontos de extremidade tooallow remoto remoto e área de trabalho do PowerShell tráfego padrão para máquinas virtuais baseadas em Windows e tráfego do Secure Shell (SSH) para baseados em Linux máquinas virtuais.
* Uma conta de armazenamento necessária que armazena hello VHDs para uma máquina virtual, incluindo sistema operacional de hello, discos de dados temporários e adicionais (armazenamento).
* Uma rede virtual opcional que atua como um recipiente adicional, no qual você pode criar uma estrutura de sub-redes e designar sub-rede Olá no qual Olá máquina virtual está localizada (rede).

Olá a tabela a seguir descreve as alterações em como os provedores de recursos de computação, rede e armazenamento interagem:

| Item | Clássico | Gerenciador de Recursos |
| --- | --- | --- |
| Serviço de Nuvem para Máquinas Virtuais |Serviço de nuvem foi um recipiente de máquinas virtuais Olá necessário disponibilidade da plataforma hello e balanceamento de carga. |Serviço de nuvem não é mais um objeto necessário para a criação de uma máquina Virtual usando o novo modelo de saudação. |
| Redes Virtuais |Uma rede virtual é opcional para a máquina virtual de saudação. Se for incluído, a rede virtual Olá não pode ser implantado com o Gerenciador de recursos. |A máquina virtual requer uma rede virtual que foi implantada com o Gerenciador de Recursos. |
| Contas de armazenamento |máquina virtual de saudação requer uma conta de armazenamento que armazena Olá VHDs para o sistema operacional de hello, discos de dados temporários e adicionais. |Olá máquina virtual requer um toostore de conta de armazenamento seus discos no armazenamento de blob |
| Conjuntos de Disponibilidade |Plataforma de toohello de disponibilidade foi indicada Configurando hello "AvailabilitySetName" mesmo em Olá máquinas virtuais. contagem máxima de saudação de domínios de falha era 2. |O Conjunto de Disponibilidade é um recurso exposto pelo Provedor Microsoft.Compute. Máquinas virtuais que requerem alta disponibilidade deve ser incluídas no conjunto de disponibilidade de saudação. contagem máxima de domínios de falha de saudação agora é 3. |
| Grupos de afinidade |Grupos de Afinidade eram necessários para criar Redes Virtuais. No entanto, com a introdução de saudação de redes virtuais regionais, que não foi necessário mais. |toosimplify, o conceito de grupos de afinidade de saudação não existe no hello APIs expostas por meio do Gerenciador de recursos do Azure. |
| Balanceamento de Carga |Criação de um serviço de nuvem fornece um balanceador de carga implícita para Olá máquinas virtuais implantadas. |Olá balanceador de carga é um recurso exposto pelo provedor do Microsoft. Network hello. interface de rede primária Olá Olá máquinas virtuais que precisa de balanceamento de carga toobe deve fazer referência balanceador de carga de saudação. Os Balanceadores de Carga podem ser internos ou externos. Uma instância do balanceador de carga referencia o pool de back-end de saudação de endereços IP que incluem hello NIC de uma máquina virtual (opcional) e faz referência a um endereço balanceador de carga público ou privado IP (opcional). [Leia mais.](../virtual-network/resource-groups-networking.md) |
| Endereço IP Virtual |Serviços de nuvem obtém um padrão VIP (endereço IP Virtual) quando uma máquina virtual é adicionada tooa serviço de nuvem. Olá endereço IP Virtual é o endereço de saudação associado ao balanceador de carga implícita de saudação. |Endereço IP público é um recurso exposto pelo provedor do Microsoft. Network hello. O Endereço IP público pode ser Estático (Reservado) ou Dinâmico. IPs públicos dinâmicos podem ser atribuídos tooa balanceador de carga. IPs Públicos podem ser protegidos usando Grupos de Segurança. |
| Endereço IP Reservado |Você pode reservar um endereço IP no Azure e associe-o com um tooensure de serviço de nuvem que Olá endereço IP é fixa. |Endereço IP público que pode ser criado no modo "Estático" e ele oferece Olá mesmo recurso como um "endereço de IP reservado". IPs públicos estáticos só pode ser atribuída tooa balanceador de carga no momento. |
| Endereço IP Público (PIP) por VM |Endereços IP públicos também pode ser associado tooa VM diretamente. |Endereço IP público é um recurso exposto pelo provedor do Microsoft. Network hello. O Endereço IP público pode ser Estático (Reservado) ou Dinâmico. No entanto, apenas os IPs públicos dinâmicos pode ser atribuído tooa tooget de Interface de rede um IP público por VM agora. |
| Pontos de extremidade |Pontos de extremidade de entrada necessário toobe configurado em uma máquina Virtual toobe abrir a conectividade para determinadas portas. Um dos modos de saudação comuns de se conectar a máquinas toovirtual feitas Configurando pontos de extremidade de entrada. |Regras de NAT de entrada pode ser configuradas em balanceadores de carga tooachieve Olá a mesma funcionalidade de habilitar pontos de extremidade em portas específicas para a conexão toohello VMs. |
| Nome DNS |Um serviço de nuvem teria um Nome DNS exclusivo implícito. Por exemplo: `mycoffeeshop.cloudapp.net`. |Os nomes DNS são parâmetros opcionais que podem ser especificados em um recurso de Endereço IP Público. Olá FQDN é seguir Olá formato - `<domainlabel>.<region>.cloudapp.azure.com`. |
| Interfaces de Rede |A Interface de Rede Primária e Secundária e suas propriedades foram definidas como a configuração de rede de uma Máquina virtual. |A Interface de Rede é um recurso exposto pelo Provedor Microsoft.Network. ciclo de vida Olá Olá que interface de rede não está ligado tooa Máquina Virtual. Ele faz referência endereço IP atribuído da máquina de virtual Olá (obrigatório), sub-rede Olá da rede virtual de saudação para máquina virtual de saudação (obrigatório) e tooa grupo de segurança de rede (opcional). |

toolearn sobre como conectar redes virtuais de diferentes modelos de implantação, consulte [conectar redes virtuais de diferentes modelos de implantação no portal de saudação](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).

## <a name="migrate-from-classic-tooresource-manager"></a>Migração de clássico tooResource Manager
Se você estiver pronto toomigrate seus recursos de implantação clássico tooResource deployment Manager, consulte:

1. [Técnico mergulho profundo na plataforma suportada migração de clássico tooAzure Gerenciador de recursos](../virtual-machines/windows/migration-classic-resource-manager-deep-dive.md)
2. [Migração de recursos de IaaS de clássico tooAzure Gerenciador de recursos de suporte de plataforma](../virtual-machines/windows/migration-classic-resource-manager-overview.md)
3. [Migrar recursos de IaaS de tooAzure clássico Gerenciador de recursos usando o PowerShell do Azure](../virtual-machines/windows/migration-classic-resource-manager-ps.md)
4. [Migrar recursos de IaaS de tooAzure clássico Gerenciador de recursos usando a CLI do Azure](../virtual-machines/virtual-machines-linux-cli-migration-classic-resource-manager.md)

## <a name="frequently-asked-questions"></a>Perguntas frequentes
**Posso criar uma máquina virtual usando o Gerenciador de recursos do Azure toodeploy em uma rede virtual criada usando a implantação clássica?**

Não há suporte para isso. Você não pode usar o Gerenciador de recursos do Azure toodeploy uma máquina virtual em uma rede virtual que foi criada usando a implantação clássica.

**Posso criar uma máquina virtual usando hello Azure Resource Manager de uma imagem de usuário que foi criada usando Olá APIs de gerenciamento de serviço do Azure?**

Não há suporte para isso. No entanto, você pode copiar arquivos VHD de saudação de uma conta de armazenamento que foi criada usando Olá APIs de gerenciamento de serviços e adicioná-los tooa nova conta criada por meio do Gerenciador de recursos do Azure.

**Qual é o impacto de saudação cota Olá para minha assinatura?**

cotas de saudação para máquinas virtuais de hello, redes virtuais e contas de armazenamento criadas por meio de saudação do Azure Resource Manager são independentes das outras cotas. Cada assinatura obtém cotas toocreate Olá recursos usando Olá novas APIs. Você pode ler mais sobre cotas adicionais Olá [aqui](../azure-subscription-service-limits.md).

**Posso continuar toouse meus scripts automatizados para o provisionamento de máquinas virtuais, redes virtuais e contas de armazenamento por meio de APIs do Gerenciador de recursos de saudação?**

Todos os scripts criados e automação Olá continuam toowork Olá máquinas de virtuais existentes, redes virtuais criadas no modo de gerenciamento de serviços do Azure hello. No entanto, os scripts de saudação têm toobe toouse atualizado Olá novo esquema para a criação de saudação mesmos recursos por meio do modo do Gerenciador de recursos de saudação.

**Onde posso encontrar exemplos de modelos do Gerenciador de Recursos do Azure?**

Um conjunto abrangente de modelos iniciais pode ser encontrado em [Modelos de início rápido do Azure Resource Manager](https://azure.microsoft.com/documentation/templates/).

## <a name="next-steps"></a>Próximas etapas
* toowalk por meio da criação de saudação do modelo que define uma máquina virtual, conta de armazenamento e rede virtual, consulte [passo a passo do Gerenciador de recursos modelo](resource-manager-template-walkthrough.md).
* comandos de saudação toosee para implantar um modelo, consulte [implantar um aplicativo com o modelo do Azure Resource Manager](resource-group-template-deploy.md).

