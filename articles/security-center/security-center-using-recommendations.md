---
title: "aaaUse segurança do Centro de segurança do Azure recomendações tooenhance | Microsoft Docs"
description: " Saiba como toouse as políticas de segurança e as recomendações na Central de segurança do Azure toohelp atenuar uma violação de segurança. "
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/08/2017
ms.author: terrylan
ms.openlocfilehash: bd314350a5abfceea3e171f2e1b55afe4549c1b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-security-center-recommendations-tooenhance-security"></a>Segurança de tooenhance recomendações Central de segurança do uso do Azure
Você pode reduzir as chances de saudação de um evento de segurança significativos Configurando uma política de segurança e, em seguida, Implementando recomendações Olá fornecidas pelo Centro de segurança do Azure. Este artigo mostra como toouse políticas de segurança e as recomendações na Central de segurança toohelp atenuar uma violação de segurança.

> [!NOTE]
> Este artigo é baseado em funções hello e conceitos introduzidos na Central de segurança de saudação [guia de planejamento e operações](security-center-planning-and-operations-guide.md). É um guia de planejamento de saudação do tooreview boa ideia antes de continuar.
>
>

## <a name="managing-security-recommendations"></a>Gerenciando recomendações de segurança
Uma política de segurança define o conjunto de saudação de controles que são recomendados para recursos em Olá especificado assinatura ou grupo de recursos. Na Central de segurança, você deve definir políticas de acordo com os requisitos de segurança da empresa tooyour. mais, consulte toolearn [definir políticas de segurança na Central de segurança](security-center-policies.md).

Políticas de segurança para grupos de recursos são herdadas do nível de assinatura de saudação.

![Herança da política de segurança][1]

Se você precisar de políticas personalizadas em grupos de recursos específico, você pode desativar a herança em grupo de recursos de saudação. toodisable, tooUnique de herança na folha de política de segurança hello e personalização de controles de saudação Central de segurança mostra as recomendações para.

Por exemplo, se você tiver cargas de trabalho que não necessitam de política de criptografia de dados transparente (TDE) do SQL Database hello, desabilitar a política de saudação no nível de assinatura hello e habilitá-lo somente nos grupos de recursos de saudação onde TDE SQL é necessária.

> [!NOTE]
> Se houver um conflito entre a política de nível de assinatura e política de nível de grupo de recursos, a política no nível do grupo Olá recurso tem precedência.
>
>

Central de segurança analisa o estado de segurança Olá seus recursos do Azure. Quando a Central de segurança identifica possíveis vulnerabilidades de segurança, ele cria recomendações com base nos controles Olá definidos na política de segurança de saudação. recomendações de saudação orientará você durante processo de saudação do configurando controles de segurança Olá necessário.

As recomendações de política atuais na Central de Segurança se concentram em atualizações do sistema, configuração de sistema operacional, grupos de segurança de rede em sub-redes e máquinas virtuais (VMs), Auditoria do Banco de Dados SQL, TDE do Banco de Dados SQL e firewalls de aplicativo Web. Para cobertura mais atualizada de Olá das recomendações da Central de segurança, consulte [Gerenciando recomendações de segurança na Central de segurança](security-center-recommendations.md).

## <a name="scenario"></a>Cenário
Este cenário mostra como o toouse Central de segurança toohelp reduzir as chances de saudação de um incidente de segurança significativo monitorando recomendações da Central de segurança e executar uma ação. cenário Hello usa Olá empresa fictícia, a Contoso, e funções apresentadas na Central de segurança de hello [guia de planejamento e operações](security-center-planning-and-operations-guide.md#security-roles-and-access-controls). funções de saudação representam indivíduos e equipes que podem usar a Central de segurança tooperform diferentes tarefas de segurança. Olá funções são:

![Funções de cenário][2]

A Contoso migrado recentemente alguns dos seu tooAzure de recursos locais. A Contoso deseja tooimplement e manter proteções que reduzem seu ataque de segurança tooa vulnerabilidade de seus recursos na nuvem de saudação.

## <a name="recommended-solution"></a>Solução recomendada
Uma solução é toouse Central de segurança tooprevent e detectar vulnerabilidades de segurança. A Contoso tem acesso tooSecurity Center por meio de sua assinatura do Azure. Olá [grátis](security-center-pricing.md) da Central de segurança é habilitada automaticamente em todas as assinaturas do Azure e coleta de dados é habilitada em todas as máquinas virtuais em sua assinatura.

David, do departamento de Segurança de TI da Contoso, configura uma **política de segurança** usando a Central de Segurança. Central de segurança analisa o estado de segurança de saudação de recursos do Azure da Contoso. Quando a Central de segurança identifica possíveis vulnerabilidades de segurança, ele cria **recomendações** com base nos controles Olá definidos na política de segurança de saudação.

Jefferson, um proprietário da carga de trabalho de nuvem, é responsável pela implementação e manutenção das proteções de acordo com a política de segurança da Contoso. Jeff pode monitorar as recomendações de saudação criadas pelo proteções de tooapply Central de segurança. recomendações de saudação orientá Jeff durante processo de saudação de Configurando controles de segurança Olá necessário.

Em ordem de Jeff tooimplement e manter as proteções e eliminar vulnerabilidades de segurança, precisa:

- Monitorar as recomendações de segurança fornecidas pela Central de Segurança
- Avaliar as recomendações de segurança e decidir quais ele deve aplicar ou ignorar
- Aplicar as recomendações de segurança

Vamos acompanhar toosee de etapas de Jeff como ele usa a Central de segurança recomendações tooguide-lo pelo processo de saudação de vulnerabilidades de segurança de tooeliminate controles de configuração.

## <a name="how-tooimplement-this-solution"></a>Como tooimplement nesta solução
Jeff entra muito[portal do Azure](https://azure.microsoft.com/features/azure-portal/) e abre Olá console central de segurança. Como parte de seu diário de monitoramento de atividades, ele verifica toosee se não houver recomendações de segurança executando Olá etapas a seguir:

1. Jeff selecionará Olá **recomendações** bloco tooopen Olá **recomendações** folha.
   ![Selecione Olá recomendações lado a lado][3]
2. Jeff examina a lista de saudação de recomendações. Ele vê que a Central de segurança forneceu lista Olá das recomendações em ordem de prioridade da prioridade de toolowest de prioridade mais alta. Ele decide tooaddress uma recomendação de alta prioridade na lista de saudação. Ele seleciona **instalar o Endpoint Protection** em Olá **recomendações** folha.
3. Olá **instalar o Endpoint Protection** folha é aberta exibindo uma lista de VMs sem antimalware habilitado. Jeff examina a lista de saudação de VMs, seleciona todas as máquinas virtuais e, em seguida, seleciona **instalar nas máquinas 3 virtuais**.
   ![Instalar o Endpoint Protection][4]
4. Olá **selecione Endpoint Protection** folha abre Jeff fornecendo com duas soluções antimalware. Jeff selecionará Olá **Antimalware da Microsoft** solução.
5. Informações adicionais sobre solução de antimalware Olá são exibidas. Jefferson seleciona **Criar**.
   ![Microsoft antimalware][5]
6. Jeff insere Olá necessárias configurações Olá **instalar** folha e seleciona **Okey**.

[O Antimalware da Microsoft](../security/azure-security-antimalware.md) está ativo no hello selecionado VMs.

Jeff continua toomove por meio de alta prioridade hello e recomendações de prioridade média, tomar decisões sobre a implementação. Jeff referencia Olá [Gerenciando recomendações de segurança](security-center-recommendations.md) artigo recomendações de saudação toounderstand e o que faz cada uma delas se ele se aplica a ele.

Jeff aprende que [Microsoft Security Response Center (MSRC)](../security/azure-security-response-center.md) executa selecione segurança monitoramento de saudação rede do Azure e a infraestrutura e recebe reclamações abuso e de inteligência de ameaça de terceiros. Se Jeff fornece detalhes de contato de segurança para a assinatura do Azure da Contoso, contatos do Microsoft Contoso se Olá MSRC descobre os dados do cliente da Contoso que foi acessado por uma parte ilegal ou não autorizada. Vamos acompanhar Jeff como ele se aplica a saudação **fornecer detalhes de contato de segurança** recomendação (uma recomendação com severidade média na lista de saudação das recomendações acima).

1. Jeff seleciona **fornecer detalhes de contato de segurança** em Olá **recomendações** folha, que abre Olá **fornecer detalhes de contato de segurança** folha.
2. Jeff seleciona as informações de contato do hello assinatura do Azure tooprovide em. Uma segunda folha **Fornecer detalhes de contato de segurança** será aberta.
   ![Detalhes do contato de segurança][6]
3. Em Olá segundo **fornecer detalhes de contato de segurança** folha, Jeff insere:

  - endereços de email de contato de segurança Olá separados por vírgulas (não há um número de toohello limite de endereços de email que ele pode inserir)
  - um número de telefone do contato de segurança

4. Jeff também ativa a opção Olá **enviar-me emails sobre alertas** tooreceive emails sobre alertas de gravidade.
5. Jeff seleciona **Okey** tooapply segurança de saudação entre em contato com assinatura de informações do tooContoso.

Por fim, Jeff revisa a recomendação de baixa prioridade Olá **vulnerabilidades do sistema operacional corrigir** e determina que essa recomendação não é aplicável. Ele quer toodismiss recomendação de saudação. Jeff seleciona pontos Olá três que aparecem toohello direita e, em seguida, seleciona **ignorar**.
   ![Ignorar a recomendação][7]

## <a name="conclusion"></a>Conclusão
Monitorar as recomendações na Central de Segurança pode ajudar a eliminar vulnerabilidades de segurança antes de uma violação ocorrer. Você pode impedir um incidente de segurança implementando e mantendo as proteções com políticas de segurança na Central de Segurança.

<!--Image references-->
[1]: ./media/security-center-using-recommendations/security-center-policy-inheritance.png
[2]: ./media/security-center-using-recommendations/scenario-roles.png
[3]: ./media/security-center-using-recommendations/select-recommendations-tile.png
[4]: ./media/security-center-using-recommendations/install-endpoint-protection.png
[5]:./media/security-center-using-recommendations/microsoft-antimalware.png
[6]: ./media/security-center-using-recommendations/provide-security-contact-details.png
[7]: ./media/security-center-using-recommendations/dismiss-recommendation.png
