---
title: "Gerenciar backups com o Controle de Acesso baseado em função do Azure | Microsoft Docs"
description: "Use operações de gerenciamento do controle de acesso baseado em função toomanage acesso toobackup no cofre de serviços de recuperação."
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 3bd46b97-4b29-47a5-b5ac-ac174dd36760
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/22/2017
ms.author: trinadhk;markgal
ms.openlocfilehash: 26d034d152f9b77fc6d5b2ffd5ef2648b1797f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-role-based-access-control-toomanage-azure-backup-recovery-points"></a>Usar pontos de recuperação do controle de acesso baseado em função toomanage Backup do Azure
O RBAC (controle de acesso baseado em função) do Azure permite o gerenciamento de acesso refinado para o Azure. Usando o RBAC, você pode separar as tarefas dentro de sua equipe e conceder apenas Olá total acesso toousers que precisam tooperform seus trabalhos.

> [!IMPORTANT]
> Funções fornecidas pelo Backup do Azure são limitados tooactions que podem ser executadas no portal do Azure ou cmdlets do PowerShell de Cofre de serviços de recuperação. As ações executadas na interface de usuário do Cliente do Agente de backup do Azure, na interface de usuário do System Center Data Protection Manager ou no Servidor de Backup do Azure estão fora do controle dessas funções.

O Backup do Azure fornece funções internas 3 toocontrol operações de gerenciamento de backup. Saiba mais sobre as [funções internas do RBAC do Azure](../active-directory/role-based-access-built-in-roles.md)

* [Fazer backup de Colaborador](../active-directory/role-based-access-built-in-roles.md#backup-contributor) -essa função tem toocreate de todas as permissões e gerenciar o backup exceto criar Cofre de serviços de recuperação e fornecendo acesso tooothers. Imagine essa função como administrador do gerenciamento de backups, que pode executar todas as operações de gerenciamento de backups.
* [Operador de backup](../active-directory/role-based-access-built-in-roles.md#backup-operator) -essa função tem permissões tooeverything, exceto um colaborador de remoção de backup e gerenciamento de políticas de backup. Essa função é equivalente toocontributor exceto não pode executar operações destrutivas como parar backup com dados de excluir ou remover o registro de recursos locais.
* [Leitor de backup](../active-directory/role-based-access-built-in-roles.md#backup-reader) -essa função tem permissões tooview todas as operações de gerenciamento de backup. Imagine toobe essa função uma pessoa de monitoramento.

Se você estiver procurando toodefine suas próprias funções para controlar ainda mais, consulte como muito[criar funções personalizadas](../active-directory/role-based-access-control-custom-roles.md) em RBAC do Azure.



## <a name="mapping-backup-built-in-roles-toobackup-management-actions"></a>Mapeamento de ações de gerenciamento de toobackup de funções internas de Backup
Olá, a tabela a seguir captura ações de gerenciamento de Backup hello e correspondente função RBAC mínimo necessário tooperform essa operação.

| Operação de gerenciamento | Função RBAC mínima necessária |
| --- | --- |
| Criar cofre de Serviços de Recuperação | Colaborador no Grupo de recursos do cofre |
| Habilitar backup de VMs do Azure | Operador de Backup no cofre, Colaborador de máquina virtual em VMs |
| Backup sob demanda de VM | Operador de backup |
| Restaurar VM | Operador de backup, colaborador de grupo de recursos no qual VM e Vnets serão tooget implantado |
| Restaurar discos, arquivos individuais do backup da VM | Operador de backup |
| Criar política de backup para backup da VM do Azure | Colaborador de backup |
| Modificar a política de backup da VM do Azure | Colaborador de backup |
| Excluir a política de backup da VM do Azure | Colaborador de backup |
| Interromper o backup (com retenção de dados ou exclusão de dados) no backup da VM | Colaborador de backup |
| Registrar-se no Windows Server/cliente/SCDPM local ou no Servidor de Backup do Azure | Operador de backup |
| Excluir o Windows Server/cliente/SCDPM local registrado ou o Servidor de Backup do Azure | Colaborador de backup |

## <a name="next-steps"></a>Próximas etapas
* [Controle de acesso baseado em função](../active-directory/role-based-access-control-configure.md): Introdução ao RBAC em Olá portal do Azure.
* Saiba como toomanage acessar com:
  * [PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)
  * [CLI do Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md)
  * [API REST](../active-directory/role-based-access-control-manage-access-rest.md)
* [Solução de problemas de Controle de Acesso Baseado em Função](../active-directory/role-based-access-control-troubleshooting.md): obtenha sugestões para corrigir problemas comuns.
