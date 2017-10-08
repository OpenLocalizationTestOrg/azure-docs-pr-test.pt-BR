---
title: aaaTroubleshoot RBAC do Azure | Microsoft Docs
description: "Obtenha ajuda para problemas ou dúvidas sobre recursos do Controle de Acesso Baseado em Função."
services: azure-portal
documentationcenter: na
author: andredm7
manager: femila
ms.assetid: df42cca2-02d6-4f3c-9d56-260e1eb7dc44
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: 15feced32d8459d90c4c246d335932f90e1fc91f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="role-based-access-control-troubleshooting"></a>Solução de problemas de Controle de Acesso baseado em função

Este artigo de documento respostas a perguntas comuns sobre direitos de acesso específicos de saudação que são concedidas com funções, para que você saiba quais tooexpect quando usando Olá funções hello portal do Azure e pode solucionar problemas de acesso. Estas três funções abrangem todos os tipos de recurso:

* Proprietário  
* Colaborador  
* Leitor  

Os proprietários e os fatores que contribuem com o gerenciamento de toohello acesso completo a experiência, mas um Colaborador não pode conceder acesso tooother usuários ou grupos. As coisas são um pouco mais interessantes com a função de leitor de hello, que é onde vamos gastar algum tempo. Consulte Olá [artigo iniciada por get do controle de acesso baseado em função](role-based-access-control-configure.md) para obter detalhes sobre como acessar toogrant.

## <a name="app-service-workloads"></a>Cargas de trabalho do serviço de aplicativo
### <a name="write-access-capabilities"></a>Recursos do acesso de gravação
Se você conceder a um usuário acesso somente leitura tooa web único aplicativo, alguns recursos são desabilitados se você não esperava. Olá, recursos de gerenciamento a seguir exige **gravar** acessar tooa web app (colaborador ou proprietário) e não estão disponíveis em qualquer cenário de somente leitura.

* Comandos (como iniciar, parar, etc.)
* Alterar configurações como configuração geral, configurações de escala, configurações de backup e configurações de monitoramento.
* Acessar credenciais de publicação e outros segredos como configurações de aplicativos e cadeias de conexão.
* Logs de streaming
* Configuração dos logs de diagnóstico
* Console (prompt de comando)
* Ativo e implantações recentes (para a implantação contínua do git local)
* Gasto estimado
* Testes da Web
* Rede virtual (somente o tooa visível leitor se uma rede virtual tiver sido configurada anteriormente por um usuário com acesso de gravação).

Se você não pode acessar qualquer um desses blocos, será necessário tooask o administrador do aplicativo web do Colaborador acesso toohello.

### <a name="dealing-with-related-resources"></a>Lidando com recursos relacionados
Os aplicativos Web são complicados pela presença de saudação de alguns recursos diferentes que interação. Aqui encontra-se um grupo de recursos típico com alguns sites:

![Grupo de recursos do aplicativo Web](./media/role-based-access-control-troubleshooting/website-resource-model.png)

Como resultado, se você conceder a pessoa acesso toojust Olá web app, grande parte da funcionalidade de saudação na folha de site Olá no hello portal do Azure está desabilitado.

Esses itens requerem **gravar** acessar toohello **plano de serviço de aplicativo** que corresponde a tooyour site:  

* Exibindo Olá web app do preço (gratuito ou padrão)  
* Configuração de escala (número instâncias, tamanho da máquina virtual, configurações de escalonamento automático)  
* Cotas (armazenamento, largura de banda, CPU)  

Esses itens requerem **gravar** toohello de acesso toda **grupo de recursos** que contém seu site:  

* Certificados SSL e associações (certificados SSL podem ser compartilhados entre sites em Olá mesmo grupo de recursos e a localização geográfica)  
* Regras de alerta  
* Configurações de autoescala  
* Componentes do Application insights  
* Testes da Web  

## <a name="virtual-machine-workloads"></a>Cargas de trabalho da máquina virtual
Muito como com aplicativos da web, alguns recursos na folha de máquina virtual Olá exigem acesso de gravação toohello VM ou tooother recursos no grupo de recursos de saudação.

Máquinas virtuais são nomes tooDomain relacionados, redes virtuais, contas de armazenamento e regras de alerta.

Esses itens requerem **gravar** acessar toohello **Máquina Virtual**:

* Pontos de extremidade  
* Endereços IP  
* Discos  
* Extensões  

Essas tarefas exigem **gravar** saudação do acesso tooboth **Máquina Virtual**e hello **grupo de recursos** (junto com o nome de domínio Olá) que ele está em:  

* Conjunto de disponibilidade  
* Conjunto de balanceamento de carga  
* Regras de alerta  

Se você não pode acessar qualquer um desses blocos, peça ao administrador para o grupo de recursos de toohello de acesso de Colaborador.

## <a name="see-more"></a>Veja mais
* [Controle de acesso baseado em função](role-based-access-control-configure.md): Introdução ao RBAC em Olá portal do Azure.
* [Funções internas](role-based-access-built-in-roles.md): obter detalhes sobre as funções hello incluídos por padrão em RBAC.
* [Funções personalizadas no Azure RBAC](role-based-access-control-custom-roles.md): Saiba como toocreate funções personalizadas toofit sua necessidades de acesso.
* [Criar um relatório de histórico de alterações de acesso](role-based-access-control-access-change-history-report.md): mantenha o controle das alterações de atribuições de função no RBAC.

