---
title: "aaaAzure máquinas virtuais a Central de segurança e do Windows no Azure | Microsoft Docs"
description: "Saiba mais sobre a segurança de sua máquina virtual do Microsoft Azure com a Central de Segurança do Azure."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/01/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 238bf4e266a24a536d35dd647db6056ab39a1f1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-virtual-machine-security-by-using-azure-security-center"></a>Monitorar a segurança da máquina virtual usando a Central de Segurança do Azure

A Central de Segurança do Azure pode ajudá-lo a ganhar visibilidade em suas práticas de segurança de recursos do Azure. A Central de segurança oferece o monitoramento de segurança integrado. Ela pode detectar ameaças que não seriam notadas de outra forma. Neste tutorial, você saberá mais sobre a Central de Segurança do Azure e como:
 
> [!div class="checklist"]
> * Configurar a coleta de dados
> * Definir políticas de segurança
> * Exibir e corrigir problemas de integridade de configuração
> * Examinar ameaças detectadas  

## <a name="security-center-overview"></a>Visão geral da Central de Segurança

A Central de Segurança do Azure identifica possíveis problemas de configuração da VM (máquina virtual) e ameaças de segurança direcionadas. Elas podem incluir VMs que não tenham grupos de segurança de rede, discos não criptografados e ataques de protocolo RDP de força bruta. Olá informações são mostradas no painel de Central de segurança Olá nos gráficos de fácil leitura.

tooaccess Olá painel central de segurança, em Olá portal do Azure, no menu de saudação, selecione **Central de segurança**. No painel de hello, ver Olá integridade da segurança do seu ambiente do Azure, encontrar uma contagem de recomendações atuais e exibir hello o estado atual de alertas de ameaça. Você pode expandir cada gráfico de alto nível toosee mais detalhes.

![Painel da Central de Segurança](./media/tutorial-azure-security/asc-dash.png)

Central de segurança vai além das recomendações de tooprovide de descoberta de dados para problemas detectados. Por exemplo, se uma VM foi implantada sem um grupo de segurança de rede, a Central de segurança exibe uma recomendação com etapas de solução que você pode tomar. Você pode obter retificação automatizada sem sair do contexto de saudação da Central de segurança.  

![Recomendações](./media/tutorial-azure-security/recommendations.png)

## <a name="set-up-data-collection"></a>Configurar a coleta de dados

Antes de poder obter visibilidade em configurações de segurança VM, você precisa tooset a coleta de dados da Central de segurança. Isso envolve ativar a coleta de dados e criar um toohold coletado dados da conta de armazenamento do Azure. 

1. No painel de Central de segurança hello, clique em **política de segurança**e, em seguida, selecione sua assinatura. 
2. Em **Coleta de dados**, selecione **Ativada**.
3. toocreate uma conta de armazenamento, selecione **escolha uma conta de armazenamento**. Depois, selecione **OK**.
4. Em Olá **política de segurança** folha, selecione **salvar**. 

Agente de coleta de dados Olá Central de segurança é instalado em todas as VMs e começa a coleta de dados. 

## <a name="set-up-a-security-policy"></a>Configurar uma política de segurança

Políticas de segurança são itens de saudação toodefine usado para o qual a Central de segurança coleta dados e faz recomendações. Você pode aplicar conjuntos de toodifferent de políticas de segurança diferentes de recursos do Azure. Embora, por padrão, os recursos do Azure são avaliados em relação a todos os itens de política, você pode desativar itens individuais de política para todos os recursos do Azure ou para um grupo de recursos. Para obter informações detalhadas sobre as políticas de segurança da Central de Segurança, consulte [Definir políticas de segurança na Central de Segurança do Azure](../../security-center/security-center-policies.md). 

tooset uma política de segurança para todos os recursos do Azure:

1. No painel de Central de segurança hello, selecione **política de segurança**e, em seguida, selecione sua assinatura.
2. Selecione **Política de prevenção**.
3. Ativar ou desativar recursos do Azure itens de política que você deseja tooapply tooall.
4. Quando terminar de selecionar as configurações, selecione **OK**.
5. Em Olá **política de segurança** folha, selecione **salvar**. 

tooset uma política para um grupo de recursos específicos:

1. No painel de Central de segurança hello, selecione **política de segurança**e, em seguida, selecione um grupo de recursos.
2. Selecione **Política de prevenção**.
3. Ativar ou desativar itens de política que você deseja que o grupo de recursos de toohello tooapply.
4. Em **HERANÇA**, selecione **Exclusivo**.
5. Quando terminar de selecionar as configurações, selecione **OK**.
6. Em Olá **política de segurança** folha, selecione **salvar**.  

Também é possível desativar a coleta de dados para um grupo de recursos específico nesta página.

Saudação de exemplo a seguir, uma política exclusiva foi criada para um grupo de recursos denominado *myResoureGroup*. Nessa política, a criptografia de disco e as recomendações de firewall do aplicativo Web são desabilitadas.

![Política exclusiva](./media/tutorial-azure-security/unique-policy.png)

## <a name="view-vm-configuration-health"></a>Exibir a integridade da configuração da VM

Depois que você tiver ativado a coleta de dados e definir uma política de segurança, a Central de segurança começa tooprovide alertas e recomendações. Como as VMs são implantadas, agente de coleta de dados hello está instalado. Central de segurança é populada com os dados de saudação novas VMs. Para obter informações detalhadas sobre a integridade de configuração de VM, consulte [Proteger suas VMs na Central de segurança](../../security-center/security-center-virtual-machine-recommendations.md). 

Como os dados são coletados, integridade de recursos Olá para cada VM e os recursos do Azure relacionados é agregada. Olá informações são mostradas em um gráfico de fácil leitura. 

integridade de recursos tooview:

1.  No painel de Central de segurança hello, em **integridade da segurança do recurso**, selecione **de computação**. 
2.  Em Olá **de computação** folha, selecione **máquinas virtuais**. Essa exibição fornece um resumo do status de configuração de saudação para todas as suas VMs.

![Computar integridade](./media/tutorial-azure-security/compute-health.png)

toosee todas as recomendações para uma VM, selecione Olá VM. Recomendações e correção são abordados em mais detalhes na próxima seção, Olá deste tutorial.

## <a name="remediate-configuration-issues"></a>Corrigir problemas de configuração

Depois que a Central de segurança começa toopopulate com dados de configuração, as recomendações são feitas com base na política de segurança Olá que você configurar. Por exemplo, se uma máquina virtual foi configurada sem um grupo de segurança de rede associados, uma recomendação é feita toocreate um. 

toosee uma lista de todas as recomendações: 

1. No painel de Central de segurança hello, selecione **recomendações**.
2. Selecione uma recomendação específica. É exibida uma lista de todos os recursos para o qual se aplica a recomendação de saudação.
3. tooapply uma recomendação, selecione um recurso específico. 
4. Siga as instruções de saudação para etapas de correção. 

Em muitos casos, a Central de segurança fornece etapas acionáveis você pode tomar uma recomendação de tooaddress sem sair da Central de segurança. Saudação de exemplo a seguir, a Central de segurança detecta um grupo de segurança de rede que tenha uma regra de entrada irrestrita. Na página de recomendação hello, você pode selecionar Olá **editar regras de entrada** botão. Saudação da interface do usuário é necessária toomodify Olá regra é exibida. 

![Recomendações](./media/tutorial-azure-security/remediation.png)

À medida que as recomendações são corrigidas, elas são marcadas como resolvidas. 

## <a name="view-detected-threats"></a>Exibir as ameaças detectadas

Além disso, recomendações de configuração de tooresource, Central de segurança exibe os alertas de detecção de ameaças. o recurso de alertas de segurança Olá agrega os dados coletados de cada VM, logs de sistema de rede do Azure e parceiro conectado soluções toodetect contra ameaças à segurança com base nos recursos do Azure. Para obter informações detalhadas sobre as funcionalidades de detecção de ameaças da Central de Segurança, consulte [Funcionalidades de detecção da Central de Segurança do Azure](../../security-center/security-center-detection-capabilities.md).

o recurso de alertas de segurança Olá requer a Central de segurança Olá preços toobe camada aumentado de *livre* muito*padrão*. 30 dias **avaliação gratuita** está disponível quando você move toothis maior preço. 

camada de preços toochange hello:  

1. No painel de Central de segurança hello, clique em **política de segurança**e, em seguida, selecione sua assinatura.
2. Selecione **Tipo de preço**.
3. Selecione nova camada de saudação e, em seguida, selecione **selecione**.
4. Em Olá **política de segurança** folha, selecione **salvar**. 

Depois que você alterou Olá preço, o gráfico de alertas de segurança Olá começa toopopulate que ameaças de segurança são detectadas.

![Alertas de segurança](./media/tutorial-azure-security/security-alerts.png)

Selecione um alerta tooview informações. Por exemplo, você pode ver uma descrição de ameaça hello, tempo de detecção de saudação, todas as tentativas de ameaça e Olá correção recomendada. Em Olá exemplo a seguir, um ataque de força bruta do RDP foi detectado, com 294 tentativas RDP. Uma solução recomendada é fornecida.

![Ataque de RDP](./media/tutorial-azure-security/rdp-attack.png)

## <a name="next-steps"></a>Próximas etapas
Nesse tutorial, você configurou a Central de Segurança do Azure e, em seguida, analisou VMs na Central de Segurança. Você aprendeu como:

> [!div class="checklist"]
> * Configurar a coleta de dados
> * Definir políticas de segurança
> * Exibir e corrigir problemas de integridade de configuração
> * Examinar ameaças detectadas

Avançar toolearn tutorial do próximo toohello como toocreate um CI/CD pipeline com o Visual Studio Team Services e uma VM do Windows executando o IIS.

> [!div class="nextstepaction"]
> [Pipeline de CI/CD do Visual Studio Team Services](./tutorial-vsts-iis-cicd.md)
