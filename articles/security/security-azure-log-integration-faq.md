---
title: "aaaAzure perguntas frequentes sobre a integração de Log | Microsoft Docs"
description: "Este artigo de perguntas frequentes responde às perguntas sobre a Integração de Logs do Azure."
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TerryLanfear
ms.assetid: d06d1ac5-5c3b-49de-800e-4d54b3064c64
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload8: na
ms.date: 08/07/2017
ms.author: TomSh
ms.custom: azlog
ms.openlocfilehash: e886035c9a180d0cd5fcbe9cc02483782df6dbe4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-faq"></a>Perguntas frequentes sobre a Integração de Logs do Azure
Este artigo responde as perguntas frequentes (FAQ) sobre a Integração de Logs do Azure. 

Integração de Log do Azure é um serviço do sistema operacional Windows que você pode usar logs bruto toointegrate de seus recursos do Azure em seus locais segurança informações e eventos (SIEM) sistemas de gerenciamento. Essa integração oferece um painel unificado para todos os seus ativos, local ou na nuvem hello. Você pode então agregar, correlacionar, analisar e alertar sobre eventos de segurança associados a seus aplicativos.

## <a name="is-hello-azure-log-integration-software-free"></a>Software de integração do Azure Log Olá é gratuito?
Sim. Não há nenhuma taxa para Olá software de integração de Log do Azure.

## <a name="where-is-azure-log-integration-available"></a>Onde a Integração de log do Azure está disponível?

Atualmente, ela está disponível atualmente no Azure Comercial e o Azure Governamental e não está disponível na China nem na Alemanha.

## <a name="how-can-i-see-hello-storage-accounts-from-which-azure-log-integration-is-pulling-azure-vm-logs"></a>Como posso ver contas de armazenamento de saudação do qual a integração do Azure Log está recebendo logs da VM do Azure?
Execute o comando Olá **lista de origem azlog**.

## <a name="how-can-i-tell-which-subscription-hello-azure-log-integration-logs-are-from"></a>Como saber quais Olá assinatura são logs de integração do Log do Azure?

No caso de saudação de logs de auditoria que são colocados em Olá **AzureResourcemanagerJson** diretórios, ID de assinatura de saudação é no nome de arquivo de log de saudação. Isso também é verdadeiro para logs no hello **AzureSecurityCenterJson** pasta. Por exemplo:

20170407T070805_2768037.0000000023.**1111e5ee-1111-111b-a11e-1e111e1111dc**.json

Logs de auditoria do Active Directory do Azure incluem hello ID de locatário como parte do nome de saudação.

Logs de diagnóstico que são lidos a partir de um hub de eventos não incluem hello ID da assinatura como parte do nome de saudação. Em vez disso, eles incluem o nome amigável do hello especificado como parte da criação de saudação da origem de hub de eventos de saudação. 

## <a name="how-can-i-update-hello-proxy-configuration"></a>Como faço para atualizar a configuração de proxy Olá?
Se a configuração do proxy não permite acesso de armazenamento do Azure diretamente, abra Olá **AZLOG. EXE. CONFIGURAÇÃO** arquivo **c:\Program Files\Microsoft Azure Log integração**. Atualização Olá arquivo tooinclude Olá **defaultProxy** seção com o endereço de proxy de saudação da sua organização. Após ter feita a atualização Olá, parar e iniciar o serviço de saudação usando comandos Olá **net stop azlog** e **net start-azlog**.

    <?xml version="1.0" encoding="utf-8"?>
    <configuration>
      <system.net>
        <connectionManagement>
          <add address="*" maxconnection="400" />
        </connectionManagement>
        <defaultProxy>
          <proxy usesystemdefault="true"
          proxyaddress=http://127.0.0.1:8888
          bypassonlocal="true" />
        </defaultProxy>
      </system.net>
      <system.diagnostics>
        <performanceCounters filemappingsize="20971520" />
      </system.diagnostics>   

## <a name="how-can-i-see-hello-subscription-information-in-windows-events"></a>Como posso ver informações de assinatura de saudação eventos do Windows?
Acrescente o nome amigável da toohello Olá assinatura ID ao adicionar fonte hello:

    Azlog source add <sourcefriendlyname>.<subscription id> <StorageName> <StorageKey>  
evento de saudação XML tem Olá metadados, incluindo a ID da assinatura Olá a seguir:

![Evento XML][1]

## <a name="error-messages"></a>Mensagens de erro
### <a name="when-i-run-hello-command-azlog-createazureid-why-do-i-get-hello-following-error"></a>Ao executar o comando de saudação **azlog createazureid**, por que recebo Olá erro a seguir?
Erro:

  *Falha toocreate aplicativo AAD - locatário 72f988bf-86f1-41af-91ab-2d7cd011db37 - motivo = 'Proibido' - mensagem = 'privilégios insuficientes toocomplete Olá operação'.*

Olá **azlog createazureid** comando tenta toocreate uma entidade de serviço em todos os locatários de saudação do AD do Azure para assinaturas de Olá Olá logon do Azure tem acesso ao. Se o logon do Azure é apenas um usuário convidado no locatário do AD do Azure, Olá falhará com "privilégios insuficientes toocomplete Olá a operação." Peça ao locatário Olá administrador tooadd sua conta como um usuário no locatário hello.

### <a name="when-i-run-hello-command-azlog-authorize-why-do-i-get-hello-following-error"></a>Ao executar o comando de saudação **azlog autorizar**, por que recebo Olá erro a seguir?
Erro:

  *Aviso de criação de atribuição de função - AuthorizationFailed: cliente Olá janedo@microsoft.com' com o objeto id 'fe9e03e4-4dad-4328-910f-fd24a9660bd2' não tem autorização tooperform ação 'Microsoft.Authorization/roleAssignments/write' no escopo ' / assinaturas / 70d 95299-d689-4c 97 b971 0d8ff0000000'.*

Olá **azlog autorizar** comando atribui Olá função da entidade de serviço do leitor toohello AD do Azure (criado com **azlog createazureid**) assinaturas toohello fornecido. Se Olá logon do Azure não é um coadministrador ou um proprietário de assinatura hello, ele falhará com uma mensagem de erro "Falha de autorização". Azure Role-Based Access RBAC (controle) de coadministrador ou o proprietário é necessário toocomplete esta ação.

## <a name="where-can-i-find-hello-definition-of-hello-properties-in-hello-audit-log"></a>Onde encontrar definição Olá propriedades Olá no log de auditoria Olá?
Consulte:

* [Operações de auditoria com o Azure Resource Manager](../azure-resource-manager/resource-group-audit.md)
* [Lista de eventos de gerenciamento de saudação em uma assinatura no hello API de REST do Monitor do Azure](https://msdn.microsoft.com/library/azure/dn931934.aspx)

## <a name="where-can-i-find-details-on-azure-security-center-alerts"></a>Onde posso encontrar detalhes sobre alertas da Central de Segurança do Azure?
Consulte [toosecurity está respondendo e gerenciamento de alertas na Central de segurança do Azure](../security-center/security-center-managing-and-responding-alerts.md).

## <a name="how-can-i-modify-what-is-collected-with-vm-diagnostics"></a>Como posso modificar o que é coletado com o diagnóstico da VM?
Para obter detalhes sobre como tooget, modificar e definir a configuração de diagnóstico do Azure hello, consulte [tooenable de usar o PowerShell diagnóstico do Azure em uma máquina virtual que executa o Windows](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

saudação de exemplo a seguir obtém a configuração de diagnóstico do Azure hello:

    -AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient
    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

    $xmlconfig | Out-File -Encoding utf8 -FilePath "d:\WADConfig.xml"

saudação de exemplo a seguir modifica a configuração de diagnóstico do Azure hello. Nessa configuração, somente 4624 ID e do evento ID 4625 são coletados do log de eventos de segurança de saudação. O Antimalware da Microsoft para eventos do Azure são coletados do log de eventos do sistema de saudação. Para obter detalhes sobre o uso de saudação de expressões XPath, consulte [consumindo eventos](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85)).

    <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Security!*[System[(EventID=4624 or EventID=4625)]]" />
        <DataSource name="System!*[System[Provider[@Name='Microsoft Antimalware']]]"/>
    </WindowsEventLog>

Olá, exemplo a seguir define configuração de diagnóstico do Azure hello:

    $diagnosticsconfig_path = "d:\WADConfig.xml"
    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName log3121 -StorageAccountKey <storage key>

Depois de fazer alterações, verifique Olá tooensure de conta de armazenamento que Olá correto de eventos são coletados.

Se você tiver problemas durante a saudação de instalação e configuração, abra um [solicitação de suporte](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request). Selecione **Log integração** como serviço Olá para o qual você está solicitando suporte.

## <a name="can-i-use-azure-log-integration-toointegrate-network-watcher-logs-into-my-siem"></a>Pode usar logs do Azure Log integração toointegrate observador de rede em meu SIEM?

O Observador de Rede do Azure gera grandes quantidades de informações de registro em log. Esses logs não são toobe devem enviado tooa SIEM. destino de saudação só tem suportada para logs do observador de rede é uma conta de armazenamento. Integração de Log do Azure não oferece suporte a ler esses logs e tornando-os disponível tooa SIEM.

<!--Image references-->
[1]: ./media/security-azure-log-integration-faq/event-xml.png
