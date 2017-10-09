---
title: "implantação do aaaHigh disponibilidade entre fronteiras geográficas AD FS no Azure com o Azure Traffic Manager | Microsoft Docs"
description: "Este documento, você aprenderá como toodeploy AD FS no Azure para alta disponibilidade."
keywords: "AD fs com o Gerenciador de tráfego do Azure, o adfs com o Azure Traffic Manager, geográfico, várias datacenter, datacenters geográfico, vários centros de dados geográficos, implantar o AD FS no azure, implantar adfs do azure, o adfs do azure, o azure ad fs, implantar o AD FS, implantar o ad fs, o AD FS no azure, implantar o AD FS no azure, implantar o AD FS no azure, azure AD FS, introdução tooAD FS, Azure, o AD FS no Azure iaas, ADFS, move tooazure adfs"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: a14bc870-9fad-45ed-acd5-a90ccd432e54
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/01/2016
ms.author: anandy;billmath
ms.openlocfilehash: c5838d749cdc5c8aabbe62b255d568525da747ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-cross-geographic-ad-fs-deployment-in-azure-with-azure-traffic-manager"></a>Implantação do AD FS de alta disponibilidade entre fronteiras geográficas no Azure com o Gerenciador de Tráfego do Azure
[Implantação do AD FS no Azure](active-directory-aadconnect-azure-adfs.md) fornece orientação passo a passo como toohow, você pode implantar uma infraestrutura do AD FS simple para sua organização no Azure. Este artigo fornece as próximas etapas Olá toocreate um entre fronteiras geográficas de implantação do AD FS no Azure usando [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md). O Azure Traffic Manager ajuda a criar uma visualização geograficamente alta disponibilidade e a infraestrutura do AD FS de alto desempenho para a sua organização, fazendo uso de intervalo de métodos de roteamento disponível toosuit diferente necessidades da infraestrutura de saudação.

Uma infraestrutura altamente disponível do AD FS entre fronteiras geográficas habilita o seguinte:

* **Eliminação de ponto único de falha:** com recursos de failover do Azure Traffic Manager, você pode obter uma infraestrutura do AD FS altamente disponível mesmo quando uma dos data centers de saudação em uma parte do globo Olá cair
* **Desempenho aprimorado:** você pode usar Olá sugerido implantação em tooprovide este artigo uma infraestrutura do AD FS de alto desempenho que pode ajudar os usuários a autenticar o mais rápido. 

## <a name="design-principles"></a>Princípios de design
![Design geral](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/blockdiagram.png)

Princípios básicos de design de saudação será o mesmos conforme listado em princípios de Design no artigo Olá a implantação do AD FS no Azure. diagrama de saudação acima mostra uma extensão simple de região geográfica do tooanother Olá implantação básica. Abaixo estão alguns pontos tooconsider ao estender a sua região geográfica do toonew de implantação

* **Rede virtual:** você deve criar uma nova rede virtual na região geográfica Olá deseja que a infraestrutura toodeploy adicional AD FS. No diagrama de saudação acima você vê Geo1 VNET e VNET Geo2 Olá duas redes virtuais em cada região geográfica.
* **Controladores de domínio e servidores do AD FS na nova rede virtual geográfica:** toodeploy controladores de domínio na região geográfica do novo Olá é recomendável para que os servidores de saudação do AD FS na nova região de saudação não possuem toocontact um controlador de domínio em outro momento rede longe toocomplete uma autenticação e, assim, melhorar o desempenho de saudação.
* **Contas de armazenamento:** as contas de armazenamento estão associadas a uma região. Como você implantará máquinas em uma nova região geográfica, você terá toocreate novas contas de armazenamento toobe usadas na região de saudação.  
* **Grupos de Segurança de Rede:** assim como contas de armazenamento, Grupos de Segurança de Rede criados em uma região não podem ser usados em outra região geográfica. Portanto, você precisará toocreate nova rede segurança grupos semelhantes toothose na região geográfica do primeiro Olá para INT e DMZ sub-rede na região geográfica do novo hello.
* **Rótulos de DNS para os endereços IP públicos:** Azure Traffic Manager pode se referir a tooendpoints apenas por meio de rótulos DNS. Portanto, será necessário toocreate DNS rótulos para os endereços IP públicos dos Olá externo balanceadores de carga.
* **O Azure Traffic Manager:** Microsoft Azure Traffic Manager permite que você toocontrol distribuição de saudação do usuário tráfego tooyour pontos de extremidade em execução em diferentes data centers ao redor Olá, mundo. O Azure Traffic Manager funciona no nível DNS de saudação. Ele usa o DNS respostas toodirect do usuário final tráfego distribuído tooglobally pontos de extremidade. Clientes, em seguida, conecte-se pontos de extremidade toothose diretamente. Com opções diferentes de roteamentos de desempenho, ponderado e prioridade, você pode facilmente optar opção de roteamento hello mais adequada às necessidades da sua organização. 
* **V-net net tooV conectividade entre duas regiões:** não é necessário toohave conectividade entre redes virtuais Olá em si. Como cada rede virtual tem acesso toodomain controladores e tem o servidor do AD FS e WAP propriamente dita, possam funcionar sem qualquer conectividade entre redes virtuais de saudação em regiões diferentes. 

## <a name="steps-toointegrate-azure-traffic-manager"></a>Etapas toointegrate Azure Traffic Manager
### <a name="deploy-ad-fs-in-hello-new-geographical-region"></a>Implantar o AD FS na região geográfica do novo Olá
Siga as etapas de saudação e diretrizes [implantação do AD FS no Azure](active-directory-aadconnect-azure-adfs.md) toodeploy Olá mesma topologia na região geográfica do novo hello.

### <a name="dns-labels-for-public-ip-addresses-of-hello-internet-facing-public-load-balancers"></a>Rótulos DNS para os endereços IP públicos de saudação voltados para Internet balanceadores de carga (público)
Conforme mencionado acima, hello Azure Traffic Manager só pode fazer referência tooDNS rótulos como pontos de extremidade e, portanto, é importante toocreate rótulos DNS para os endereços IP públicos dos Olá externo balanceadores de carga. Captura de tela abaixo mostra como você pode configurar seu rótulo DNS para o endereço IP público de saudação. 

![Rótulo de DNS](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/eastfabstsdnslabel.png)

### <a name="deploying-azure-traffic-manager"></a>Implantação do Gerenciador de Tráfego do Azure
Siga as próximas etapas, Olá toocreate um perfil do Gerenciador de tráfego. Para obter mais informações, você também pode consultar muito[gerenciar um perfil do Gerenciador de tráfego do Azure](../traffic-manager/traffic-manager-manage-profiles.md).

1. **Criar um perfil do Gerenciador de Tráfego:** dê um nome exclusivo a seu perfil do gerenciador de tráfego. Esse nome de perfil Olá faz parte do nome DNS hello e atua como um prefixo de rótulo de nome de domínio do Traffic Manager hello. nome da saudação / prefixo é adicionado too.trafficmanager.net toocreate um rótulo DNS para o Gerenciador de tráfego. saudação de captura de tela abaixo mostra o Gerenciador de tráfego Olá prefixo DNS que está sendo definido como mysts e o rótulo DNS resultante será mysts.trafficmanager.net. 
   
    ![Criação de perfil do Gerenciador de Tráfego](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/trafficmanager01.png)
2. **Método de roteamento de tráfego:** há três opções de roteamento disponíveis no gerenciador de tráfego:
   
   * Prioridade 
   * Desempenho
   * Ponderado
     
     **Desempenho** Olá recomenda a infraestrutura opção tooachieve altamente responsivo AD FS. No entanto, você pode escolher qualquer método de roteamento mais adequado para suas necessidades de implantação. funcionalidade do Hello AD FS não é afetada pela opção de roteamento de saudação selecionada. Veja [Métodos de roteamento de tráfego do Gerenciador de Tráfego](../traffic-manager/traffic-manager-routing-methods.md) para obter mais informações. Olá captura de tela de exemplo anteriormente, você pode ver Olá **desempenho** método selecionado.
3. **Configurar pontos de extremidade:** na página do Gerenciador de tráfego hello, clique nos pontos de extremidade e selecione Adicionar. Isso abrirá uma Adicionar ponto de extremidade página semelhante toohello captura de tela abaixo
   
   ![Configurar pontos de extremidade](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/eastfsendpoint.png)
   
   Para entradas de diferentes Olá, siga a diretriz de saudação abaixo:
   
   **Tipo:** Selecionar ponto de extremidade do Azure, como podemos estar apontando tooan endereço IP público do Azure.
   
   **Nome:** criar um nome que você deseja tooassociate com ponto de extremidade de saudação. Isso não é um nome DNS hello e não tem suporte nos registros de DNS.
   
   **Tipo de recurso de destino:** endereço IP público selecione como propriedade toothis hello. 
   
   **Recurso de destino:** isso lhe dará uma opção toochoose de rótulos DNS diferentes Olá você tem disponível em sua assinatura. Escolha Olá que DNS rótulo de ponto de extremidade toohello correspondente que está configurando.
   
   Adicione ponto de extremidade para cada região geográfica que você deseja que o tráfego de tooroute hello Azure Traffic Manager para.
   Para obter mais informações e etapas detalhadas sobre como tooadd / configurar pontos de extremidade no Gerenciador de tráfego, consulte muito[adicionar, desabilitar, habilitar ou excluir pontos de extremidade](../traffic-manager/traffic-manager-endpoints.md)
4. **Configurar a investigação:** na página do Gerenciador de tráfego hello, clique na configuração. Na página de configuração hello, você precisa toochange Olá monitor configurações tooprobe na porta 80 de HTTP e o caminho relativo /adfs/probe
   
    ![Configurar investigação](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/mystsconfig.png) 
   
   > [!NOTE]
   > **Verifique se o status de saudação de pontos de extremidade de saudação está ONLINE após a conclusão da configuração de saudação**. Se todos os pontos de extremidade estão em estado 'degradado', o Azure Traffic Manager fará um melhor tentativa tooroute Olá o tráfego supondo que Olá diagnóstico está incorreto e todos os pontos de extremidade estão acessíveis.
   > 
   > 
5. **Modificar registros DNS para o Azure Traffic Manager:** seu serviço de federação deve ser um nome de DNS do Azure Traffic Manager toohello CNAME. Crie um CNAME no hello registros DNS públicos para que, na verdade, quem está tentando o serviço de Federação Olá tooreach atinge hello Azure Traffic Manager.
   
    Por exemplo, o serviço de Federação do toopoint Olá fs.fabidentity.com toohello Traffic Manager, você precisaria tooupdate sua saudação de toobe de registro de recurso DNS a seguir:
   
    <code>fs.fabidentity.com IN CNAME mysts.trafficmanager.net</code>

## <a name="test-hello-routing-and-ad-fs-sign-in"></a>Saudação de roteamento e do AD FS sign-in de teste
### <a name="routing-test"></a>Teste de roteamento
Um teste muito básico para roteamento Olá seria tootry ping Olá federação nome DNS do serviço de um computador em cada região geográfica. Dependendo do método de roteamento de saudação escolhido, ponto de extremidade de saudação realmente executa ping será refletido na exibição de ping hello. Por exemplo, se você selecionou o desempenho de saudação roteamento, em seguida, ponto de extremidade hello mais próximo toohello região do cliente Olá seja atingido. Abaixo está o instantâneo de saudação do dois pings de duas máquinas de clientes de uma região diferente, uma na região EastAsia e outra no Oeste dos EUA. 

![Teste de roteamento](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/pingtest.png)

### <a name="ad-fs-sign-in-test"></a>Teste de entrada no AD FS
tootest de maneira mais fácil de saudação do AD FS é por meio de saudação IdpInitiatedSignon.aspx página. Em toodo capaz de toobe de ordem, é necessário tooenable Olá IdpInitiatedSignOn nas propriedades de saudação do AD FS. Siga as etapas de saudação abaixo tooverify sua instalação do AD FS

1. Executar Olá abaixo cmdlet no servidor do hello AD FS, usando o PowerShell, tooset-tooenabled. 
   Set-AdfsProperties -EnableIdPInitiatedSignonPage $true
2. De qualquer computador externo, acesse https://<yourfederationservicedns>/adfs/ls/IdpInitiatedSignon.aspx
3. Você deve ver a página de saudação do AD FS como abaixo:
   
    ![Teste de ADFS - desafio de autenticação](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/adfstest1.png)
   
    e quando você entrar com êxito, ele lhe fornecerá uma mensagem de êxito, conforme mostrado abaixo:
   
    ![Teste de ADFS - êxito da autenticação](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/adfstest2.png)

## <a name="related-links"></a>Links relacionados
* [Implantação básica do AD FS no Azure](active-directory-aadconnect-azure-adfs.md)
* [Gerenciador de Tráfego do Microsoft Azure](../traffic-manager/traffic-manager-overview.md)
* [Métodos de roteamento de tráfego do Gerenciador de Tráfego](../traffic-manager/traffic-manager-routing-methods.md)

## <a name="next-steps"></a>Próximas etapas
* [Gerenciar um perfil de Gerenciador de tráfego do Azure](../traffic-manager/traffic-manager-manage-profiles.md)
* [Adicionar, desabilitar, habilitar ou excluir pontos de extremidade](../traffic-manager/traffic-manager-endpoints.md) 

