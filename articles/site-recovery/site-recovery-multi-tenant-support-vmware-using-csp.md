---
title: "suporte a aaaMulti locatário tooAzure de replicação de VM do VMware (programa CSP) | Microsoft Docs"
description: "Descreve como toodeploy do Azure Site Recovery em um ambiente multilocatário tooorchestrate replicação, failover e a recuperação de local tooAzure de máquinas virtuais (VMs) do VMware por meio do programa CSP hello usando Olá portal do Azure"
services: site-recovery
documentationcenter: 
author: mayanknayar
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: manayar
ms.openlocfilehash: 9be555c9a438f66e6d3dfcdc9f507a84763846d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="multi-tenant-support-in-azure-site-recovery-for-replicating-vmware-virtual-machines-tooazure-through-csp"></a>Suporte a multilocatário no Azure Site Recovery para replicar tooAzure de máquinas virtuais VMware por meio de CSP

O Azure Site Recovery oferece suporte a ambientes multilocatários para assinaturas de locatários. Ele também dá suporte a multilocação para assinaturas de locatários que são criadas e gerenciadas por meio do programa do provedor de solução de nuvem da Microsoft (CSP) hello. Este artigo detalha as diretrizes de saudação para implementar e gerenciar cenários de VMware para o Azure de vários locatários. Ele também aborda a criação e o gerenciamento de assinaturas de locatários por meio do CSP.

Este guia muito desenhos de documentação existente de saudação para replicar tooAzure de máquinas virtuais VMware. Para obter mais informações, consulte [tooAzure de máquinas virtuais VMware replicar com a recuperação de Site](site-recovery-vmware-to-azure.md).

## <a name="multi-tenant-environments"></a>Ambientes multilocatário
Há três modelos principais de multilocatários:

* **Compartilhado do provedor de serviços de hospedagem (HSP)**: parceiro Olá possui infraestrutura física hello e utiliza recursos compartilhados (vCenter, data centers, armazenamento físico e assim por diante) toohost VMs de vários locatários em Olá mesma infraestrutura. parceiro Olá pode fornecer gerenciamento de recuperação de desastres como um serviço gerenciado ou Locatário Olá pode possuir a recuperação de desastres como uma solução de autoatendimento.

* **Dedicado de provedor de serviços de hospedagem**: parceiro Olá possui infraestrutura física Olá mas usa recursos dedicados (vários vCenters, armazenamentos de dados físicos e assim por diante) toohost VMs de cada locatário em uma infraestrutura separada. parceiro Olá pode fornecer gerenciamento de recuperação de desastres como um serviço gerenciado, ou Locatário Olá pode ter como uma solução de autoatendimento.

* **Gerenciado de provedor de serviços (MSP)**: cliente Olá possui infraestrutura física de saudação que hospeda as VMs de saudação e parceiro Olá fornece gerenciamento e habilitação de recuperação de desastres.

## <a name="shared-hosting-multi-tenant-guidance"></a>Diretriz de multilocatário de hospedagem compartilhada
Esta seção aborda um cenário de hospedagem compartilhada Olá detalhadamente. Olá, outros dois cenários são subconjuntos do cenário de hospedagem compartilhada hello e usarem Olá mesmos princípios. Olá diferenças são descritas no final de saudação de diretrizes de hospedagem compartilhada hello.

Olá, um requisito básico em um cenário de multilocatário é tooisolate Olá vários locatários. Um locatário não deve ser capaz de tooobserve que tenha hosted outro locatário. Em um ambiente gerenciado por parceiros, esse requisito não é tão importante quanto em um ambiente de autoatendimento, no qual ele pode ser crucial. Este guia presume que o isolamento de locatários é necessário.

arquitetura de saudação é apresentada na Olá diagrama a seguir:

![HSP compartilhado com um vCenter](./media/site-recovery-multi-tenant-support-vmware-using-csp/shared-hosting-scenario.png)  
**Cenário de hospedagem compartilhada com um vCenter**

Conforme visto no hello precede o diagrama, cada cliente tem um servidor de gerenciamento separados. Este locatário de limites de configuração acesso específico tootenant VMs e habilita o isolamento de locatário. Um cenário de replicação da máquina virtual VMware usa Olá configuração servidor toomanage contas toodiscover VMs e instalar agentes. Seguimos Olá mesmos princípios para ambientes de multilocatários, com a adição de saudação de restringir a descoberta VM por meio do vCenter controle de acesso.

requisito de isolamento de dados Olá exige que todas as informações confidenciais de infraestrutura (como credenciais de acesso) permanecem tootenants não revelado. Por esse motivo, é recomendável que todos os componentes do servidor de gerenciamento de saudação permaneçam sob controle exclusivo de saudação do parceiro de saudação. componentes de servidor de gerenciamento de saudação são:
* CS (Servidor de configuração)
* PS (Servidor de processo)
* MT (Servidor de destino mestre) 

PS uma expansão também está sob controle do parceiro hello.

### <a name="every-cs-in-hello-multi-tenant-scenario-uses-two-accounts"></a>Cada CS no cenário de multilocatário Olá usa duas contas

- **conta de acesso do vCenter**: usar máquinas virtuais do locatário de toodiscover essa conta. Ele tem permissões de acesso do vCenter atribuídas tooit (conforme descrito na próxima seção, Olá). toohelp evitar vazamentos acidentais de acesso, é recomendável que os parceiros Insira essas credenciais se na ferramenta de configuração de saudação.

- **Conta de acesso à máquina virtual**: Use este agente de mobilidade conta tooinstall Olá em máquinas virtuais do locatário Olá por meio de um envio automático. Geralmente é uma conta de domínio que um locatário pode fornecer tooa parceiro ou que, como alternativa, o parceiro de saudação pode gerenciar diretamente. Se um locatário não deseja detalhes de saudação tooshare com parceiro Olá diretamente, ele ou ela pode permitida credenciais de saudação tooenter por tempo limitado acessar toohello CS ou com a assistência do parceiro hello, instalar agentes de mobilidade manualmente.

### <a name="requirements-for-a-vcenter-access-account"></a>Requisitos para uma conta de acesso do vCenter

Como mencionado na saudação anterior seção, configure Olá CS com uma conta que tenha um tooit especial de função atribuída. atribuição de função Hello deve ser aplicada a conta de acesso do vCenter toohello para cada objeto do vCenter e propagadas não toohello os objetos filho. Essa configuração garante o isolamento de locatários, porque a propagação de acesso pode resultar em objetos de tooother acesso acidental.

![Olá opção de objetos tooChild Propagate](./media/site-recovery-multi-tenant-support-vmware-using-csp/assign-permissions-without-propagation.png)

alternativa de saudação é tooassign conta de usuário de saudação e a função no objeto de datacenter hello e propagá-los toohello os objetos filho. Dar conta Olá um *nenhum acesso* função para cada objeto (como VMs de outros locatários) que deve ser locatário específico tooa inacessível. Essa configuração é complicada e expõe controles de acesso acidental, porque cada novo objeto filho recebe automaticamente o acesso que é herdado do hello pai. Portanto, é recomendável que você use a primeira abordagem de saudação.

procedimento de acesso da conta do vCenter Olá é o seguinte:

1. Criar uma nova função por meio da clonagem Olá predefinido *somente leitura* função e, em seguida, atribua a ele um nome conveniente (como Azure_Site_Recovery, conforme mostrado neste exemplo).

2. Atribua Olá função toothis de permissões a seguir:

    * **Repositório de dados**: Alocar espaço, Procurar repositório de dados, Operações de arquivo de baixo nível, Remover arquivo, Atualizar arquivos de máquina virtual

    * **Rede**: Atribuição de rede

    * **Recurso**: pool de tooresource atribuir VM, migrar desligado a máquina virtual, migrar ligado a VM

    * **Tarefas**: Criar tarefa, Atualizar tarefa

    * **Máquina virtual**: 
        * Configuração > todas
        * Interação > Responder perguntas, Conexão do dispositivo, Configurar mídia de CD, Configurar mídia de disquete, Desligar, Ligar, Instalação de ferramentas VMware
        * Inventário > Criar com base em existente, Criar novo, Registrar, Cancelar registro
        * Provisionamento > Permitir download de máquina virtual, Permitir upload de arquivos de máquina virtual
        * Gerenciamento de instantâneo > Remover instantâneos

    ![caixa de diálogo Editar função Hello](./media/site-recovery-multi-tenant-support-vmware-using-csp/edit-role-permissions.png)

3. Atribua níveis toohello vCenter conta de acesso (usada no locatário Olá CS) para vários objetos, da seguinte maneira:

>| Objeto | Função | Comentários |
>| --- | --- | --- |
>| vCenter | Somente leitura | Somente vCenter de tooallow de acesso necessário para gerenciar diferentes objetos. Você pode remover essa permissão se Olá conta nunca vai toobe fornecido tooa locatário ou usados para as operações de gerenciamento em Olá vCenter. |
>| Datacenter | Azure_Site_Recovery |  |
>| Host e cluster de host | Azure_Site_Recovery | Novamente garante que o acesso é no nível de objeto hello, para que hosts acessíveis apenas ter locatário VMs antes do failover e depois de failback. |
>| Repositório de dados e cluster de repositório de dados | Azure_Site_Recovery | Mesmo que o anterior. |
>| Rede | Azure_Site_Recovery |  |
>| Servidor de gerenciamento | Azure_Site_Recovery | Inclui acesso tooall componentes (CS PS e MT) se houver fora da máquina Olá CS. |
>| VMs do locatário | Azure_Site_Recovery | Garante que qualquer novo locatário VMs de um locatário específico também pode obter esse acesso, ou eles não poderão ser descobertos por meio de saudação portal do Azure. |

acesso à conta Olá vCenter foi concluído. Operações de failback toocomplete do requisito de permissões mínimas Olá atende a essa etapa. Você também pode usar essas permissões de acesso com as políticas existentes. Basta modificar suas permissões conjunto tooinclude função permissões existentes da etapa 2, detalhado anteriormente.

operações de recuperação de desastres toorestrict até que o estado de failover hello (ou seja, sem os recursos de failback), siga Olá precede o procedimento, com uma exceção: em vez de atribuir Olá *Azure_Site_Recovery* função conta de acesso do vCenter toohello, atribuir apenas um *somente leitura* conta com função toothat. Esse conjunto de permissões permite failover e replicação de VM, mas não permite failback. Tudo no hello precede o processo permanece como está. tooensure isolamento de locatários e restringir a descoberta VM, cada permissão ainda estiver atribuído a objetos de nível toochild somente e não propagadas objeto hello.

## <a name="other-multi-tenant-environments"></a>Outros ambientes multilocatários

Olá anterior seção descrita como tooset um ambiente de multilocatário para uma solução de hospedagem compartilhada. Olá outras duas soluções principais são hospedagem dedicado e serviço gerenciado. arquitetura de saudação para essas soluções é descrita na Olá seções a seguir.

### <a name="dedicated-hosting-solution"></a>Solução de hospedagem dedicada

Conforme mostrado no diagrama a seguir de saudação, a diferença de arquitetura de saudação em uma solução de hospedagem dedicada é que a infra-estrutura de cada locatário estiver configurada para esse locatário somente. Como locatários são isolados por meio de vCenters separado, o provedor de hospedagem de saudação ainda deve executar etapas CSP Olá fornecidas para hospedagem compartilhada, mas não precisa tooworry sobre isolamento de locatários. A configuração do CSP permanece inalterada.

![architecture-shared-hsp](./media/site-recovery-multi-tenant-support-vmware-using-csp/dedicated-hosting-scenario.png)  
**Cenário de hospedagem dedicada com vários vCenters**

### <a name="managed-service-solution"></a>Solução de serviço gerenciado

Como Olá mostrada no diagrama a seguir, diferença de arquitetura de saudação em uma solução de serviço gerenciado é que a infra-estrutura de cada locatário também seja fisicamente separada da infraestrutura de outros locatários. Neste cenário geralmente existe quando o locatário Olá possui infra-estrutura de saudação e quer uma recuperação de desastres de toomanage de provedor de solução. Novamente, como locatários são fisicamente isolados através de infraestruturas diferentes, o parceiro Olá precisa de etapas CSP Olá toofollow fornecidas para hospedagem compartilhada, mas não precisa tooworry sobre isolamento de locatários. O provisionamento de CSP permanece inalterado.

![architecture-shared-hsp](./media/site-recovery-multi-tenant-support-vmware-using-csp/managed-service-scenario.png)  
**Cenário de serviço gerenciado com vários vCenters**

## <a name="csp-program-overview"></a>Visão geral do programa CSP
Olá [programa CSP](https://partner.microsoft.com/en-US/cloud-solution-provider) promove histórias melhor que oferecem parceiros todos os serviços de nuvem da Microsoft, incluindo o Office 365 Enterprise Mobility Suite e Microsoft Azure. Com o CSP, nossos parceiros possuem relação de ponta a ponta Olá com clientes e tornam-se o ponto de contato Olá relação primária. Parceiros podem implantar as assinaturas do Azure para clientes e combinar assinaturas Olá com suas próprias ofertas de valor agregadas e personalizadas.

Com o Azure Site Recovery, parceiros podem gerenciar a solução de recuperação de desastres completa Olá para clientes diretamente por meio de CSP. Ou eles podem usar CSP tooset ambientes de recuperação de Site e que permitem aos clientes gerenciar suas necessidades de recuperação de desastres de uma maneira de autoatendimento. Em ambos os cenários, os parceiros são ligação Olá entre a recuperação de Site e seus clientes. Parceiros de relacionamento com o cliente Olá de serviço e cobrar os clientes pelo uso da recuperação de Site.

## <a name="create-and-manage-tenant-accounts"></a>Criar e gerenciar contas de locatário

### <a name="step-0-prerequisite-check"></a>Etapa 0: Verificação de pré-requisitos

Olá pré-requisitos VM são Olá igual ao descrito em Olá [documentação do Azure Site Recovery](site-recovery-vmware-to-azure.md). Nos pré-requisitos do toothose adição, você deve ter Olá a controles de acesso mencionadas anteriormente em vigor antes de prosseguir com o gerenciamento de locatário por meio do CSP. Para cada locatário, crie um servidor de gerenciamento separados que pode se comunicar com VMs do locatário hello e vCenter do parceiro. Somente o parceiro Olá tem servidor de toothis de direitos de acesso.

### <a name="step-1-create-a-tenant-account"></a>Etapa 1: criar uma conta de locatário

1. Por meio de [Microsoft Partner Center](https://partnercenter.microsoft.com/), entre na conta de CSP tooyour. 
 
2. Em Olá **painel** menu, selecione **clientes**.

    ![link de clientes do Microsoft Partner Center Olá](./media/site-recovery-multi-tenant-support-vmware-using-csp/csp-dashboard-display.png)

3. Na página de saudação que é aberta, clique em Olá **Adicionar cliente** botão.

    ![botão Adicionar cliente de saudação](./media/site-recovery-multi-tenant-support-vmware-using-csp/add-new-customer.png)

4. Em Olá **novo cliente** página, preencha os detalhes de informações da conta para locatário Olá Olá e, em seguida, clique em **próximo: assinaturas**.

    ![página de informações da conta de saudação](./media/site-recovery-multi-tenant-support-vmware-using-csp/customer-add-filled.png)

5. Na página de seleção do hello assinaturas, selecione Olá **Microsoft Azure** caixa de seleção. Você pode adicionar outras assinaturas agora ou a qualquer momento.

    ![caixa de seleção de assinatura do Microsoft Azure Olá](./media/site-recovery-multi-tenant-support-vmware-using-csp/azure-subscription-selection.png)

6. Em Olá **revisão** página, confirme os detalhes do locatário hello e, em seguida, clique em **enviar**.

    ![página de revisão Olá](./media/site-recovery-multi-tenant-support-vmware-using-csp/customer-summary-page.png)  

    Depois que você criou a conta de locatário hello, uma página de confirmação aparece, exibindo os detalhes de saudação do hello conta padrão e Olá senha para essa assinatura. 

7. Salvar informações de saudação e alterar a senha de saudação posteriormente conforme necessário por meio de saudação do Azure portal na página de entrada.  
 
    Você pode compartilhar essas informações com locatário hello como está, ou você pode criar e compartilhar uma conta separada, se necessário.

### <a name="step-2-access-hello-tenant-account"></a>Etapa 2: Acessar a conta de locatário Olá

Você pode acessar Olá assinatura de locatário por meio de saudação painel Microsoft Partner Center, conforme descrito em "etapa 1: criar uma conta de locatário." 

1. Vá toohello **clientes** página e clique em nome de saudação da conta de locatário de saudação.

2. Em Olá **assinaturas** página da conta de locatário hello, você pode monitorar assinaturas de conta existentes hello e adicionar mais assinaturas, conforme necessário. operações de recuperação de desastres do locatário de saudação toomanage, selecione **todos os recursos (portal do Azure)**.

    ![link de todos os recursos de saudação](./media/site-recovery-multi-tenant-support-vmware-using-csp/all-resources-select.png)  
    
    Clicando em **todos os recursos** concede acesso a assinaturas de toohello do locatário do Azure. Você pode verificar o acesso clicar no link do Active Directory do Azure Olá no hello parte superior direita da saudação portal do Azure.

    ![Link do Azure Active Directory](./media/site-recovery-multi-tenant-support-vmware-using-csp/aad-admin-display.png)

Agora você pode executar todas as operações de recuperação de site para o locatário Olá por meio de saudação portal do Azure e gerenciar operações de recuperação de desastres de saudação. tooaccess Olá assinatura de locatário por meio de CSP para recuperação de desastres gerenciado, siga Olá descrito anteriormente processo.

### <a name="step-3-deploy-resources-toohello-tenant-subscription"></a>Etapa 3: Implantar a assinatura de recursos de locatário toohello
1. No hello portal do Azure, crie um grupo de recursos e, em seguida, implante um cofre de serviços de recuperação por processo normal de saudação. 
 
2. Baixe a chave de registro de cofre hello.

3. Registre Olá CS para locatário hello usando a chave de registro de cofre hello.

4. Insira as credenciais de saudação para contas de acesso de saudação dois: conta de acesso de conta de acesso do vCenter e VM.

    ![Contas do servidor de configurações do gerenciador](./media/site-recovery-multi-tenant-support-vmware-using-csp/config-server-account-display.png)

### <a name="step-4-register-site-recovery-infrastructure-toohello-recovery-services-vault"></a>Etapa 4: Infra-estrutura de recuperação de Site de registro de serviços de recuperação de toohello cofre
1. No hello portal do Azure, no cofre Olá que você criou anteriormente, registrar Olá vCenter server toohello CS que você registrou na "etapa 3: implantar a assinatura de recursos de locatário toohello." Use conta de acesso do vCenter Olá para essa finalidade.
2. Concluir o processo de "Infraestrutura de preparação" de Olá para recuperação de Site por processo normal de saudação.
3. Olá VMs agora estão pronto toobe replicada. Verifique se apenas hello VMs do locatário são exibidas em Olá **selecionar máquinas virtuais** folha sob Olá **replicar** opção.

    ![Lista de máquinas virtuais de locatário na folha de máquinas virtuais específicas Olá](./media/site-recovery-multi-tenant-support-vmware-using-csp/tenant-vm-display.png)

### <a name="step-5-assign-tenant-access-toohello-subscription"></a>Etapa 5: Atribuir locatário acesso toohello assinatura

Autoatendimento para recuperação de desastres, forneça toohello locatário Olá detalhes da conta, conforme mencionado na etapa 6 do hello "etapa 1: criar uma conta de locatário" seção. Execute esta ação depois parceiro Olá configura a infraestrutura de recuperação de desastres hello. Se o tipo de recuperação de desastres de saudação é gerenciado ou autoatendimento, parceiros devem acessar as assinaturas do locatário por meio do portal CSP Olá. Eles configurar o Cofre de propriedade de parceiro hello e registre assinaturas de locatários de toohello de infraestrutura.

Parceiros também podem adicionar uma nova assinatura de locatário toohello do usuário por meio do portal CSP Olá Olá seguinte:

1. Acesse a página de assinatura do locatário toohello CSP e selecione Olá **usuários e licenças** opção.

    ![Olá a página de inscrição do CSP do locatário](./media/site-recovery-multi-tenant-support-vmware-using-csp/users-and-licences.png)

    Agora você pode criar um novo usuário inserindo detalhes relevantes hello e selecionar permissões ou Carregando lista de saudação de usuários em um arquivo CSV.

2. Depois de criar um novo usuário, volte toohello Azure portal e, em seguida, em Olá **assinatura** folha, assinatura relevantes Olá select.

3. Na folha de saudação que é aberta, selecione **controle de acesso (IAM)**e, em seguida, clique em **adicionar** tooadd um usuário com nível de acesso relevantes hello.      
    usuários Olá que foram criados por meio do portal CSP hello serão automaticamente exibidos na folha de saudação que é aberta após você clicar em um nível de acesso.

    ![Adicionar um usuário](./media/site-recovery-multi-tenant-support-vmware-using-csp/add-user-subscription.png)

    Para a maioria das operações de gerenciamento, Olá *Colaborador* função é suficiente. Usuários com esse nível de acesso podem fazer tudo em uma assinatura, exceto alterar os níveis de acesso (para tal é necessário o nível de acesso *Proprietário*). Você também pode ajustar os níveis de acesso Olá conforme necessário.
