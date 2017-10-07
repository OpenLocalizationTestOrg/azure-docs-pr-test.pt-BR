---
title: aaaMicrosoft dados do Azure com criptografia em repouso | Microsoft Docs
description: "Este artigo fornece uma visão geral da criptografia de dados do Microsoft Azure em repouso, Olá recursos gerais e considerações gerais."
services: security
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: TomSh
ms.assetid: 9dcb190e-e534-4787-bf82-8ce73bf47dba
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: yurid
ms.openlocfilehash: d74d103e4fd7585543b4f039877af7d742a6b2e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-encryption-at-rest"></a>Criptografia de dados em repouso no Azure
Há várias ferramentas de dados do Microsoft Azure toosafeguard de acordo com necessidades de segurança e conformidade da empresa tooyour. Este documento se concentra em como dados protegidos em repouso no Microsoft Azure, discute Olá vários componentes que faz parte da implementação de proteção de dados hello e analisa os prós e contras das abordagens de proteção de gerenciamento de chave diferentes Olá. 

A criptografia em repouso é um requisito de segurança comum. Um benefício do Microsoft Azure é que as organizações podem atingir a criptografia em repouso sem a necessidade de custo de saudação de implementação e o risco de hello e gerenciamento de uma solução de gerenciamento de chaves personalizado. As organizações têm a opção de saudação de permitir que o Azure gerencie completamente a criptografia em repouso. Além disso, as organizações têm tooclosely de várias opções gerenciar chaves de criptografia ou de criptografia.

## <a name="what-is-encryption-at-rest"></a>O que é criptografia em repouso?
Criptografia em repouso refere-se toohello criptográfico codificação (criptografia) de dados quando ele é mantido. Olá criptografia em designs de Rest do Azure use tooencrypt de criptografia simétrica e descriptografar grandes quantidades de dados rapidamente de acordo com o modelo conceitual simples de tooa:

- Uma chave de criptografia simétrica é usada tooencrypt dados conforme são persistidos 
- Olá a mesma chave de criptografia é usada toodecrypt que os dados como ele estiver preparado para uso na memória
- Os dados podem ser particionados e diferentes chaves podem ser utilizadas para cada partição
- As chaves devem ser armazenadas em um local seguro com políticas de controle de acesso, limitando o acesso toocertain identidades e uso de chave de registro em log. Chaves de criptografia de dados geralmente são criptografadas com limitar acesso de criptografia assimétrica toofurther (discutido Olá *chave hierarquia*, mais adiante neste artigo)

Olá acima descreve os elementos de alto nível comum Olá de criptografia em repouso. Na prática, os principais cenários de controle e gerenciamento, assim como garantias de disponibilidade e escala, requerem construções adicionais. Os conceitos e componentes de Criptografia em Repouso no Microsoft Azure são descritos abaixo.

## <a name="hello-purpose-of-encryption-at-rest"></a>finalidade de saudação de criptografia em repouso
Criptografia em repouso é pretendido tooprovide proteção de dados para dados em repouso (conforme descrito acima.) Ataques contra os dados em repouso incluem o hardware de toohello do tentativas tooobtain acesso físico no qual Olá os dados são armazenados, e, em seguida, o comprometimento Olá continha dados. Em um ataque assim, disco rígido do servidor pode ter foi manipulado incorretamente durante a manutenção, permitindo que um invasor disco rígido Olá tooremove. Posterior invasor de saudação colocaria o disco rígido Olá em um computador em seus dados do controle tooattempt tooaccess hello. 

Criptografia em repouso é projetado tooprevent invasor de saudação acessem dados descriptografado de saudação assegurando Olá dados são criptografados quando no disco. Se um invasor tooobtain um disco rígido com tais criptografados dados e chaves de criptografia sem acesso toohello, invasor Olá não poderia comprometer os dados de saudação sem grande dificuldade. Nesse cenário, um invasor tem tooattempt ataques contra os dados criptografados que são muito mais complexos e consumo de recursos que o acesso sem criptografia de dados em um disco rígido. Por esse motivo, a criptografia em repouso é altamente recomendada e é um requisito de alta prioridade para muitas organizações. 

Em alguns casos, a criptografia em repouso também é requerida pela necessidade de uma organização para governança de dados e esforços de conformidade. As regulamentações governamentais e do setor como HIPAA, PCI e FedRAMP, e os requisitos regulamentares internacionais, estabelecem proteções específicas por meio de processos e políticas relacionados à proteção de dados e requisitos de criptografia. Para muitos dessas regulamentações, a criptografia em repouso é uma medida obrigatória necessária para proteção e gerenciamento de dados compatíveis. 

Além disso toocompliance e os requisitos normativos, criptografia em repouso deve ser percebida como um recurso de plataforma de defesa em profundidade. Embora a Microsoft fornece uma plataforma compatível para serviços, aplicativos, e dados, o recurso abrangente e segurança física, dados de controle de acesso e auditoria, é importante tooprovide adicionais "sobreposta" medidas de segurança caso uma saudação outros segurança mede falhar. A criptografia em repouso fornece esse mecanismo de defesa adicional.

Microsoft é confirmada tooproviding criptografia opções rest em serviços de nuvem e tooprovide clientes adequado capacidade de gerenciamento de chaves de criptografia e acesso toologs mostrando quando as chaves de criptografia são usadas. Além disso, a Microsoft está trabalhando objetivo Olá de fazer com que todos os dados criptografados em repouso por padrão.

## <a name="azure-encryption-at-rest-components"></a>Componentes da Criptografia em Repouso no Azure

Conforme descrito anteriormente, a meta de saudação de criptografia em repouso é que os dados são persistidos no disco são criptografados com uma chave secreta de criptografia. tooachieve essa meta proteger a criação da chave de armazenamento, controle de acesso e gerenciamento de criptografia Olá chaves devem ser fornecidas. Embora os detalhes podem variar, criptografia de serviços do Azure em implementações de Rest podem ser descritos em termos de saudação abaixo conceitos que, em seguida, são ilustradas no diagrama a seguir de saudação.

![Componentes](./media/azure-security-encryption-atrest/azure-security-encryption-atrest-fig1.png)

### <a name="azure-key-vault"></a>Cofre da Chave do Azure

local de armazenamento de saudação de chaves de criptografia hello e chaves de toothose de controle de acesso é criptografia tooan central no modelo de rest. chaves de saudação necessário toobe altamente protegida mas gerenciável pelos usuários especificados e os serviços de toospecific disponíveis. Para serviços do Azure, Azure Key Vault é hello recomendado de solução de armazenamento de chaves e fornece uma experiência de gerenciamento comum em serviços. Chaves são armazenadas e gerenciadas no cofre de chave e o Cofre de chaves acesso tooa pode receber toousers ou serviços. O Azure Key Vault fornece suporte a criação de chaves do cliente ou importação de chaves do cliente para uso em cenários de chave de criptografia de cliente gerenciado.

### <a name="azure-active-directory"></a>Azure Active Directory

Chaves de saudação toouse permissões armazenada no cofre de chaves do Azure, toomanage ou tooaccess-los para a criptografia em Rest criptografia e descriptografia, contas do Active Directory tooAzure pode ser fornecido. 

### <a name="key-hierarchy"></a>Hierarquia de Chave

Geralmente, mais de uma chave de criptografia é utilizada em uma implementação de criptografia em repouso. A criptografia assimétrica é útil para estabelecer confiança hello e autenticação necessária para o gerenciamento e o acesso à chave. A criptografia simétrica é mais eficiente para criptografia e descriptografia em massa, permitindo uma criptografia mais forte e melhor desempenho. Além disso, limitar o uso de saudação de um diminui de chave de criptografia única risco Olá Olá chave ficarão comprometido e Olá custo de nova criptografia quando uma chave deve ser substituída. benefícios de saudação tooleverage de criptografia simétrica e assimétrica e o uso de saudação do limite e exposição de uma única chave, a criptografia do Azure em modelos do rest usar uma hierarquia de chave composta de saudação seguintes tipos de chaves:

- **Chave de criptografia de dados (DEK)** – uma chave simétrica de AES256 usados tooencrypt uma partição ou um bloco de dados.  Um recurso único pode ter muitas partições e muitas Chaves de Criptografia de Dados. Criptografar cada bloco de dados com uma chave diferente torna os ataques de análise de criptografia mais difíceis. Acesso tooDEKs necessita Olá aplicativo ou provedor de instância do recurso que está criptografando e descriptografando um bloco específico. Quando uma DEK é substituída por uma nova chave somente hello dados no seu bloco associado devem ser criptografados novamente com a nova chave de saudação.
- **Chave de criptografia de chave (KEK)** – uma chave de criptografia assimétrica usado tooencrypt Olá chaves de criptografia de dados. Uso de uma chave de criptografia de chave permite Olá chaves de criptografia de dados próprios toobe criptografado e controlado. entidade de saudação que tem acesso toohello KEK pode ser diferente da entidade de saudação que exige Olá DEK. Isso permite que uma entidade toobroker acesso toohello DEK para finalidade de saudação de garantir o acesso limitado de cada partição de toospecific DEK. Como Olá KEK é necessário toodecrypt Olá DEKs, Olá KEK é efetivamente um único ponto pelo qual DEKs podem ser efetivamente excluídos pela exclusão de saudação KEK.

Olá chaves de criptografia de dados, criptografada com hello chaves de criptografia de chave são armazenadas separadamente e apenas uma entidade com acesso toohello que chave de criptografia pode obter quaisquer chaves de criptografia de dados criptografados com essa chave. Há suporte para diferentes modelos de armazenamento de chaves. Vamos discutir cada modelo em mais detalhes posteriormente na próxima seção, Olá.

## <a name="data-encryption-models"></a>Modelos de Criptografia de Dados

Noções básicas sobre Olá vários modelos de criptografia e seus prós e contras é essencial para Noções básicas sobre como Olá vários provedores de recursos no Azure implementar criptografia em repouso. Essas definições são compartilhadas entre todos os provedores de recursos taxonomia e linguagem comum tooensure do Azure. 

Há três cenários para criptografia do lado do servidor:

- Criptografia do lado do servidor utilizando chaves de Serviço Gerenciado
    - Provedores de recursos do Azure executar operações de criptografia e descriptografia de saudação
    - A Microsoft gerencia chaves Olá
    - Funcionalidade completa na nuvem

- Criptografia do lado do servidor usando chaves gerenciadas pelo cliente no Azure Key Vault
    - Provedores de recursos do Azure executar operações de criptografia e descriptografia de saudação
    - O cliente controla as chaves por meio do Azure Key Vault
    - Funcionalidade completa na nuvem

- Criptografia do lado do servidor utilizando chaves gerenciadas pelo cliente em hardware controlado pelo cliente
    - Provedores de recursos do Azure executar operações de criptografia e descriptografia de saudação
    - Chaves de controle do cliente no hardware controlado pelo cliente
    - Funcionalidade completa na nuvem

Para a criptografia do lado do cliente, considere o seguinte de saudação:

- Os serviços do Azure não podem ver dados descriptografados
- Os clientes gerenciam e armazenam chaves no local (ou em outros repositórios seguros). As chaves não são serviços tooAzure disponíveis
- Funcionalidade reduzida na nuvem

modelos de criptografia Olá com suporte no Azure dividido em dois grupos principais: "Cliente criptografias" e "servidor" como mencionado anteriormente. Observe que, independentemente da criptografia Olá no modelo de rest serviços do Azure usados sempre recomendam Olá uso de um transporte seguro, como TLS ou HTTPS. Portanto, a criptografia no transporte deve ser resolvida pelo protocolo de transporte hello e não deve ser um fator preponderante determinar que a criptografia em rest modelo toouse.

### <a name="client-encryption-model"></a>Modelo de criptografia de cliente

Modelo de criptografia do cliente refere-se tooencryption que é executada fora Olá provedor de recursos ou do Azure pelo serviço de saudação ou aplicativo de chamada. criptografia de saudação pode ser executada pelo aplicativo de serviço Olá no Azure, ou por um aplicativo em execução no Centro de dados de clientes hello. Em ambos os casos, ao aproveitar esse modelo de criptografia, Olá provedor de recursos do Azure recebe um blob criptografado de dados sem dados de saudação do hello capacidade toodecrypt de qualquer forma ou ter as chaves de criptografia de toohello de acesso. Nesse modelo, o gerenciamento de chaves de saudação é feito através da saudação chamando o aplicativo do serviço e é completamente opaco toohello serviço do Azure.

![Cliente](./media/azure-security-encryption-atrest/azure-security-encryption-atrest-fig2.png)

### <a name="server-side-encryption-model"></a>Modelo de criptografia do lado do servidor

Modelos de criptografia do lado do servidor Consulte tooencryption que é executada pelo saudação do serviço do Azure. Nesse modelo, Olá provedor de recursos executa Olá criptografar e descriptografar as operações. Por exemplo, o armazenamento do Azure podem receber dados em operações de texto sem formatação e executará Olá criptografia e descriptografia internamente. Olá provedor de recursos pode usar chaves de criptografia que são gerenciadas pela Microsoft ou por cliente Olá dependendo Olá fornecido a configuração. 

![Servidor](./media/azure-security-encryption-atrest/azure-security-encryption-atrest-fig3.png)

### <a name="server-side-encryption-key-management-models"></a>Modelos de gerenciamento de chave de criptografia do lado do servidor

Cada criptografia do servidor de saudação em modelos do rest implica características diferentes de gerenciamento de chaves. Isso inclui onde e como chaves de criptografia são criadas e armazenadas como bem como modelos de acesso de saudação e Olá procedimentos de rotação de chaves. 

#### <a name="server-side-encryption-using-service-managed-keys"></a>Criptografia do lado do servidor utilizando chaves de serviço gerenciado

Para muitos clientes, o requisito essencial Olá é tooensure que Olá dados é criptografado sempre que ele está inativo. Criptografia do lado do servidor usando chaves de serviço gerenciado permite que esse modelo permitindo que os clientes toomark Olá determinado recurso (conta de armazenamento, banco de dados SQL, etc.) para criptografia e deixando todos os aspectos de gerenciamento de chaves, como backup, rotação e emissão de chave tooMicrosoft. A maioria dos serviços do Azure que oferecem suporte à criptografia em repouso geralmente oferecem suporte a esse modelo de descarregamento de gerenciamento de saudação do hello tooAzure de chaves de criptografia. provedor de recursos do Azure Olá cria chaves hello, coloca em armazenamento seguro e recuperá-los quando necessário. Isso significa que o serviço Olá tem chaves de toohello acesso completo e serviço Olá tem controle total sobre o gerenciamento de ciclo de vida de credenciais hello.

![gerenciado](./media/azure-security-encryption-atrest/azure-security-encryption-atrest-fig4.png)

Criptografia do lado do servidor usando as chaves de serviço gerenciado, portanto, rapidamente endereços Olá necessidade toohave a criptografia em repouso com cliente toohello sobrecarga baixa. Quando disponível um cliente normalmente abre Olá portal do Azure para assinatura de destino hello e provedor de recursos e verifica se uma caixa indicando gostariam Olá toobe de dados criptografado. Em algumas criptografias do lado do servidor de Gerenciadores de Recursos com chaves de serviço gerenciado são ativadas por padrão. 

Criptografia do lado do servidor com Microsoft gerenciada chaves implicam serviço Olá tem acesso completo toostore e gerencia chaves de saudação. Embora alguns clientes podem querer chaves de saudação toomanage porque acham podem assegurar maior segurança, hello custos e os riscos associados a uma solução de armazenamento de chaves personalizado devem ser considerados ao avaliar este modelo. Em muitos casos, uma organização pode determinar riscos de uma solução local ou restrições de recursos podem maior risco de saudação do gerenciamento de nuvem de criptografia de saudação em chaves de rest.  No entanto, esse modelo pode não ser suficiente para as organizações que têm a criação de saudação toocontrol requisitos ou ciclo de vida de chaves de criptografia de saudação ou equipe diferente toohave gerenciar chaves de criptografia do serviço daqueles gerenciando serviço hello (ou seja, Segregação de gerenciamento de chaves da saudação modelo geral de gerenciamento para o serviço de saudação).

##### <a name="key-access"></a>Acesso à chave

Quando a criptografia do lado do servidor com chaves de serviço gerenciado é usada, Olá criação da chave, armazenamento e serviço de acesso são todos gerenciados pelo serviço hello. Normalmente, provedores de recursos do Azure básico Olá armazenará Olá chaves de criptografia de dados em um repositório de dados toohello fechados e rapidamente disponível e acessível Olá chaves de criptografia de chave são armazenadas em um repositório interno seguro.

**Vantagens**

- Configuração simples
- A Microsoft gerencia backup, redundância e rotação de chave
- Cliente não tiver Olá custo associado à implementação ou Olá o risco de um esquema de gerenciamento de chaves personalizado.

**Desvantagens**

- Não há controle do cliente sobre as chaves de criptografia da saudação (especificação de chave do ciclo de vida, revogação, etc.)
- Gerenciamento de chaves não toosegregate capacidade do modelo de gerenciamento geral do serviço Olá

#### <a name="server-side-encryption-using-customer-managed-keys-in-azure-key-vault"></a>Criptografia do lado do servidor utilizando chaves de cliente gerenciado no Azure Key Vault 

Para cenários em que o requisito de saudação é dados de saudação do tooencrypt em repouso e clientes de chaves de criptografia do controle Olá podem usar a criptografia do lado do servidor usando o cliente gerenciado chaves no cofre de chaves. Alguns serviços podem armazenar somente raiz Olá chave de criptografia de chave no cofre de chaves do Azure e saudação do repositório criptografados chave de criptografia de dados em um dado toohello mais próximo do local interno. Em que os clientes do cenário podem colocar suas próprias chaves tooKey cofre (BYOK – Traga sua própria chave), ou gerar novos e usá-los tooencrypt recursos de saudação desejado. Enquanto Olá provedor de recursos executa operações de criptografia e descriptografia de saudação ele usa chave Olá configurado como chave de raiz de saudação para todas as operações de criptografia. 

##### <a name="key-access"></a>Acesso à chave

Olá modelo de criptografia do servidor com chaves de cliente gerenciado no cofre de chaves do Azure envolve Olá serviço acessando Olá chaves tooencrypt e descriptografar conforme necessário. Criptografia em chaves rest são feitas serviço tooa acessível por meio de uma política de controle de acesso concedendo essa identidade tooreceive Olá chave do serviço. Um serviço do Azure executado em nome de uma assinatura associada pode ser configurado com uma identidade para esse serviço dentro dessa assinatura. serviço Olá pode realizar a autenticação do Active Directory do Azure e receber um token de autenticação se identificando como serviço atuando em nome de assinatura de saudação. Esse token pode ser apresentada tooKey cofre tooobtain uma chave ele tem acesso ao.

Para operações usando chaves de criptografia, uma identidade de serviço pode ser concedida tooany de acesso de saudação seguintes operações: descriptografar, encrypt, unwrapKey, wrapKey, verifique, entrar, obter, listar, atualizar, criar, importar, excluir, backup e restauração.

tooobtain uma chave para uso em criptografar ou descriptografar dados na identidade do serviço rest Olá que Olá Gerenciador de recursos de instância de serviço será executado devem ter UnwrapKey (chave de tooget Olá para descriptografia) e WrapKey (tooinsert uma chave no cofre de chaves ao criar uma nova chave).


>[!NOTE] 
>Para obter mais detalhes sobre o Cofre de chaves autorização Consulte Olá proteger sua página de Cofre de chaves no hello [documentação do Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault). 

**Vantagens**

- Controle total sobre chaves Olá usado – criptografia de chaves são gerenciadas no cofre de chaves do cliente Olá sob controle do cliente hello.
- Capacidade tooencrypt mestre de tooone vários serviços
- Pode separar o gerenciamento de chaves do modelo de gerenciamento geral do serviço Olá
- É possível definir o serviço e a localização de chave entre regiões

**Desvantagens**

- O cliente tem total responsabilidade pelo gerenciamento de acesso de chave
- O cliente tem total responsabilidade pelo gerenciamento do ciclo de vida da chave
- Configuração adicional e sobrecarga de configuração

#### <a name="server-side-encryption-using-service-managed-keys-in-customer-controlled-hardware"></a>Criptografia do lado do servidor utilizando chaves de serviço gerenciado em hardware controlado pelo cliente

Para cenários em que o requisito de saudação tooencrypt Olá dados em repouso e gerenciar chaves de saudação em um repositório proprietária fora do controle da Microsoft, alguns serviços do Azure permitem o modelo de gerenciamento de chaves de Host sua própria chave (HYOK) hello. Nesse modelo, serviço Olá deve recuperar a chave de saudação de um site externo e, portanto, as garantias de desempenho e disponibilidade são afetadas e configuração é mais complexa. Além disso, como serviço Olá tenham acesso toohello DEK durante criptografia Olá e operações de descriptografia Olá garantias de segurança geral desse modelo são semelhantes Olá toowhen chaves são gerenciados pelo cliente no cofre de chaves do Azure.  Como resultado, esse modelo não é apropriado para a maioria das organizações, exceto se possuírem requisitos específicos de gerenciamento de chaves que o exijam. Devido a limitações de toothese, a maioria dos serviços do Azure não dão suporte a criptografia do lado do servidor usando chaves de servidor gerenciado no hardware do cliente controlado.

##### <a name="key-access"></a>Acesso à chave

Quando é usada a criptografia do lado do servidor usando chaves de serviço gerenciado no hardware do cliente controlado chaves Olá são mantidas em um sistema configurado pelo cliente hello. Os serviços do Azure que oferecem suporte a esse modelo fornecem um meio de um cliente de tooa conexão segura de estabelecer fornecido pelo repositório de chaves.

**Vantagens**

- Controle total sobre a chave de raiz de saudação usado – criptografia de chaves são gerenciadas por um repositório fornecidos pelo cliente
- Capacidade tooencrypt mestre de tooone vários serviços
- Pode separar o gerenciamento de chaves do modelo de gerenciamento geral do serviço Olá
- É possível definir o serviço e a localização de chave entre regiões

**Desvantagens**

- Total responsabilidade pela segurança, desempenho, disponibilidade e armazenamento de chaves
- Total responsabilidade pelo gerenciamento de acesso à chave
- Total responsabilidade pelo gerenciamento do ciclo de vida da chave
- Configuração significativa, configuração e custos de manutenção contínuos
- Dependência maior disponibilidade de rede entre Olá cliente datacenter e datacenters do Azure.

## <a name="encryption-at-rest-in-microsoft-cloud-services"></a>Criptografia em repouso em serviços em nuvem da Microsoft

Os serviços do Microsoft Cloud são utilizados em todos os três modelos de nuvem: IaaS, PaaS, SaaS. A seguir, são apresentados exemplos de como ajustam-se em cada modelo:

- Serviços de software, chamado tooas Software como um servidor ou SaaS, que têm o aplicativo fornecido pela nuvem hello como o Office 365.
- Serviços da plataforma quais clientes aproveitam nuvem Olá em seus aplicativos usando a nuvem de saudação para coisas como a funcionalidade do barramento de serviço, análise e armazenamento.
- Serviços de infraestrutura ou infraestrutura como serviço (IaaS) no qual o cliente implantar sistemas operacionais e aplicativos que são hospedados em Olá nuvem e possivelmente aproveitando outros serviços em nuvem.

### <a name="encryption-at-rest-for-saas-customers"></a>Criptografia em repouso para clientes SaaS

Os clientes de Software como Serviço (SaaS), geralmente possuem criptografia em repouso habilitada ou disponível em cada serviço. Serviços do Office 365 tem várias opções para os clientes tooverify ou habilitar uma criptografia em repouso. Para obter informações sobre os serviços do Office 365, consulte Tecnologias de Criptografia de Dados para Office 365.

### <a name="encryption-at-rest-for-paas-customers"></a>Criptografia em repouso para clientes de PaaS

Plataforma como serviço (PaaS) dados de um cliente geralmente reside em um ambiente de execução do aplicativo e os provedores de recursos do Azure usado toostore os dados do cliente. criptografia de saudação do toosee em rest opções disponíveis tooyou examinar a tabela de saudação abaixo para plataformas de armazenamento e o aplicativo hello que você usa. Onde houver suporte, os links tooinstructions sobre como habilitar a criptografia em repouso são fornecidos para cada provedor de recursos. 

### <a name="encryption-at-rest-for-iaas-customers"></a>Criptografia em repouso para clientes de IaaS

Os clientes de Infraestrutura como Serviço (IaaS) podem ter uma variedade de serviços e aplicativos em uso. Os serviços de IaaS podem habilitar a criptografia em repouso em suas máquinas virtuais hospedadas no Azure e VHDs utilizando o Azure Disk Encryption. 

#### <a name="encrypted-storage"></a>Armazenamento criptografado

Como PaaS, as soluções de IaaS podem aproveitar outros serviços do Azure que armazenam dados criptografados em repouso. Nesses casos, você pode habilitar Olá criptografia no suporte a Rest, conforme fornecido por cada serviço do Azure consumido. Olá a tabela a seguir enumera o armazenamento principal hello, serviços e plataformas de aplicativos e modelo de saudação de criptografia em repouso com suporte. Onde houver suporte, são fornecidos links tooinstructions sobre como habilitar a criptografia em repouso. 

#### <a name="encrypted-compute"></a>Computação criptografada

Uma criptografia completa solução de Rest requer que Olá dados nunca são persistidos no formato descriptografado. Enquanto estiver em uso, em uma saudação do servidor ao carregar dados na memória, dados podem ser persistentes localmente de várias maneiras, incluindo arquivo de paginação do Windows hello, um despejo de memória e qualquer saudação do log de aplicativo pode executar. tooensure esses dados são criptografados em repouso aplicativos IaaS podem usar a criptografia de disco do Azure em uma máquina virtual de IaaS do Azure (Windows ou Linux) e o disco virtual. 

#### <a name="custom-encryption-at-rest"></a>Criptografia em repouso personalizada

É recomendável, sempre que possível, que os aplicativos de IaaS utilizem as opções de Criptografia em Repouso e o Azure Disk Encryption fornecidos por quaisquer serviços do Azure consumidos. Em alguns casos, como requisitos de criptografia irregulares ou armazenamento do Azure não baseado em, um desenvolvedor de um aplicativo de IaaS talvez seja necessário tooimplement criptografia em rest próprios. Os desenvolvedores das soluções de IaaS podem integra-se melhor com o gerenciamento do Azure e as expectativas dos clientes, aproveitando determinados componentes do Azure. Especificamente, os desenvolvedores devem usar hello Azure Key Vault serviço tooprovide armazenamento seguro de chaves, bem como fornecer a seus clientes com opções de gerenciamento de chaves consistente com que os serviços de plataforma mais do Azure. Além disso, soluções personalizadas devem usar chaves de criptografia tooaccess do contas de serviço de tooenable identidades de serviço gerenciado do Azure. Para informações de desenvolvedor sobre o Azure Key Vault e as Identidades de Serviço Gerenciado, consulte seus respectivos SDKs.

## <a name="azure-resource-providers-encryption-model-support"></a>Suporte ao modelo de criptografia dos provedores de recursos do Azure

Serviços do Microsoft Azure cada suporta uma ou mais de criptografia de saudação em modelos de rest. Para alguns serviços, no entanto, um ou mais modelos de criptografia Olá podem não ser aplicável. Além disso, os serviços podem liberar suporte para esses cenários em horários diferentes. Esta seção descreve criptografia Olá no site de suporte em tempo de saudação da redação deste artigo para cada um dos serviços de armazenamento de dados do Azure principais Olá rest.

### <a name="azure-disk-encryption"></a>Criptografia de disco do Azure

Qualquer cliente que utiliza recursos de IaaS (Infraestrutura como Serviço) pode alcançar criptografia em repouso para seus discos e VMs de IaaS através do Azure Disk Encryption. Para obter mais informações sobre o disco do Azure criptografia Consulte Olá [documentação de criptografia de disco do Azure](https://docs.microsoft.com/azure/security/azure-security-disk-encryption).

#### <a name="azure-storage"></a>Armazenamento do Azure

O Arquivo e Blob do Azure oferecem suporte de criptografia em repouso para cenários criptografados do lado do servidor, assim como dados criptografados do cliente (criptografia do lado do cliente).

- Lado do servidor: os clientes que utilizam o armazenamento de Blobs do Azure podem habilitar a criptografia em repouso em cada conta do recurso de armazenamento do Azure. Uma vez habilitada a criptografia do lado do servidor é feita de forma transparente toohello aplicativo. Para obter mais informações, consulte [Criptografia de serviço do Armazenamento do Azure para dados em repouso ](https://docs.microsoft.com/azure/storage/storage-service-encryption).
- Lado do cliente: a criptografia do lado do cliente de Blobs do Azure tem suporte. Ao usar a criptografia de cliente clientes criptografar Olá dados e carregar dados de saudação como um blob criptografado. Gerenciamento de chaves é feito pelo cliente hello. Para obter mais informações, consulte [Criptografia do lado do cliente e Azure Key Vault para Armazenamento do Microsoft Azure](https://docs.microsoft.com/azure/storage/storage-client-side-encryption).


#### <a name="sql-azure"></a>SQL Azure

Atualmente, o SQL Azure oferece suporte para criptografia em repouso para cenários de criptografia do lado do cliente e lado do serviço gerenciado da Microsoft.

Suporte para servidor no momento, a criptografia é fornecida por meio do recurso SQL Olá chamado criptografia transparente de dados. Quando um cliente SQL Azure habilita a chave de TDE, são criadas e gerenciadas automaticamente. Criptografia em repouso pode ser habilitada nos níveis de banco de dados e servidor de saudação. A partir de junho de 2017, a [TDE (Transparent Data Encryption)](https://msdn.microsoft.com/library/bb934049.aspx) estará habilitada por padrão em bancos de dados recém-criados.

Cliente de criptografia de dados do SQL Azure tem suporte por meio de saudação [sempre criptografado](https://msdn.microsoft.com/library/mt163865.aspx) recurso. Sempre criptografado usa uma chave que são criados e armazenados pelo cliente hello. Os clientes podem armazenar a chave mestra de saudação em um repositório de certificados do Windows, o Cofre de chaves do Azure ou um módulo de segurança de Hardware local. Usando o SQL Server Management Studio, os usuários do SQL escolher qual chave gostariam toouse tooencrypt qual coluna.

|                                  |                |                     | **Modelo de criptografia**             |                              |        |
|----------------------------------|----------------|---------------------|------------------------------|------------------------------|--------|
|                                  |                |                     |                              |                              | **Cliente** |
|                                  | **Gerenciamento de Chaves** | **Chaves de serviço gerenciado** | **Cliente gerenciado no Key Vault** | **Cliente gerenciado no local** |        |
| **Armazenamento e banco de dados**            |                |                     |                              |                              |        |
| Disco (IaaS)                      |                | -                   | Sim                          | Sim*                         | -      |
| SQL Server (IaaS)                |                | Sim                 | Sim                          | Sim                          | Sim    |
| SQL Azure (PaaS)                 |                | Sim                 | Visualização                      | -                            | Sim    |
| Armazenamento do Microsoft Azure (Blobs de páginas e Bloco) |                | Sim                 | Visualização                      | -                            | Sim    |
| Armazenamento do Microsoft Azure (Arquivos)            |                | Sim                 | -                            | -                            | -      |
| Armazenamento do Microsoft Azure (Tabelas, Consultas)   |                | -                   | -                            | -                            | Sim    |
| Cosmos DB (DocumentDB)          |                | Sim                 | -                            | -                            | -      |
| StorSimple                       |                | Sim                 | -                            | -                            | Sim    |
| Backup                           |                | -                   | -                            | -                            | Sim    |
| **Inteligência e Análise**       |                |                     |                              |                              |        |
| Fábrica de dados do Azure               |                | Sim                 | -                            | -                            | -      |
| Azure Machine Learning           |                | -                   | Visualização                      | -                            | -      |
| Stream Analytics do Azure           |                | Sim                 | -                            | -                            | -      |
| HDInsights (Armazenamento de Blobs)  |                | Sim                 | -                            | -                            | -      |
| HDInsights (Armazenamento de Data Lake)   |                | Sim                 | -                            | -                            | -      |
| Repositório Azure Data Lake            |                | Sim                 | Sim                          | -                            | -      |
| Catálogo de Dados do Azure               |                | Sim                 | -                            | -                            | -      |
| Power BI                         |                | Sim                 | -                            | -                            | -      |
| **Serviços de IoT**                     |                |                     |                              |                              |        |
| Hub IoT                          |                | -                   | -                            | -                            | Sim    |
| Barramento de Serviço                      |                | -              | -                            | -                            | Sim    |
| Hubs de Eventos                       |                | -             | -                            | -                            | -      |


## <a name="conclusion"></a>Conclusão

Proteção de dados do cliente armazenados nos serviços do Azure é de suma importância tooMicrosoft. Todos os hospedado do Azure services são confirmada tooproviding criptografia opções Rest. Os serviços fundamentais, como o Armazenamento do Microsoft Azure, SQL Azure e os principais serviços de análise e inteligência, já oferecem opções de criptografia em repouso. Alguns desses serviços oferecem suporte para chaves controladas pelo cliente e criptografia do lado do cliente, assim como criptografia e chaves de serviço gerenciado. Serviços do Microsoft Azure são amplamente melhorando a criptografia na disponibilidade do Rest e novas opções foram planejadas para visualização e disponibilidade geral em meses futuros hello.

