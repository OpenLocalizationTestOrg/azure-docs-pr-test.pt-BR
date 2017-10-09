---
title: problemas do Gateway de gerenciamento de dados de aaaTroubleshoot | Microsoft Docs
description: Fornece dicas tootroubleshoot problemas relacionados tooData Gateway de gerenciamento.
services: data-factory
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: c6756c37-4e5a-4d1e-ab52-365f149b4128
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
published: True
ms.openlocfilehash: 85dacc8a1e8d574d6e7d5b556c995cebdc148fde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-issues-with-using-data-management-gateway"></a>Solucionar problemas usando o Gateway de Gerenciamento de Dados
Este artigo fornece informações sobre como solucionar problemas com o uso do Gateway de Gerenciamento de Dados.

> [!NOTE]
> Consulte Olá [Data Management Gateway](data-factory-data-management-gateway.md) artigo para obter informações detalhadas sobre o gateway de saudação. Consulte Olá [mover dados entre locais e na nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo para obter uma explicação da movimentação de dados de um tooMicrosoft de banco de dados do SQL Server local armazenamento de BLOBs do Azure usando o gateway de saudação.
>
>

## <a name="failed-tooinstall-or-register-gateway"></a>Gateway tooinstall ou register com falha
### <a name="1-problem"></a>1. Problema
Você vir essa mensagem de erro ao instalar e registrar um gateway, especificamente, ao baixar o arquivo de instalação do gateway de saudação.

`Unable tooconnect toohello remote server". Please check your local settings (Error Code: 10003).`

#### <a name="cause"></a>Causa
máquina Olá no qual você está tentando gateway de saudação tooinstall falhou toodownload hello mais recente gateway arquivo de instalação do Centro de download da saudação devido a problema de rede tooa.

#### <a name="resolution"></a>Resolução
Verifique seu toosee de configurações de servidor de proxy de firewall se Olá impedirem que a conexão de rede de saudação do hello computador toohello [Centro de download](https://download.microsoft.com/)e atualizar as configurações de saudação adequadamente.

Como alternativa, você pode baixar o arquivo de instalação de Olá para o gateway mais recente de saudação do hello [Centro de download](https://www.microsoft.com/download/details.aspx?id=39717) em outros computadores que podem acessar o Centro de download da saudação. Você pode então gateway de toohello arquivo do instalador de saudação cópia computador host e executá-lo manualmente tooinstall e atualização de gateway de saudação.

### <a name="2-problem"></a>2. Problema
Você verá esse erro quando você estiver tentando tooinstall um gateway clicando **instalar diretamente no computador** em Olá portal do Azure.

`Error:  Abort installing a new gateway on this computer because this computer has an existing installed gateway and a computer without any installed gateway is required for installing a new gateway.`  

#### <a name="cause"></a>Causa
Um gateway já está instalado na máquina de saudação.

#### <a name="resolution"></a>Resolução
Desinstalar o gateway existente na máquina de saudação do hello e clique em Olá **instalar diretamente no computador** link novamente.

### <a name="3-problem"></a>3. Problema
Esse erro poderá ser exibido ao registrar um novo gateway.

`Error: hello gateway has encountered an error during registration.`

#### <a name="cause"></a>Causa
Você verá esta mensagem para uma saudação motivos a seguir:

* formato de saudação da chave do gateway de saudação é inválido.
* chave do gateway Olá foi invalidado.
* chave do gateway Olá tiver sido regenerada do portal de saudação.  

#### <a name="resolution"></a>Resolução
Verifique se você estiver usando a chave de certo de gateway de saudação do portal de saudação. Se necessário, gerar novamente uma chave e usar Olá tooregister chave Olá gateway.

### <a name="4-problem"></a>4. Problema
Talvez você veja Olá a seguinte mensagem de erro quando você estiver registrando um gateway.

`Error: hello content or format of hello gateway key "{gatewayKey}" is invalid, please go tooazure portal toocreate one new gateway or regenerate hello gateway key.`



![O conteúdo ou o formato da chave é inválido](media/data-factory-troubleshoot-gateway-issues/invalid-format-gateway-key.png)

#### <a name="cause"></a>Causa
Olá conteúdo ou formato de chave de gateway de entrada hello está incorreto. Um dos motivos Olá pode ser copiados apenas uma parte da chave de saudação do portal de saudação ou você estiver usando uma chave inválida.

#### <a name="resolution"></a>Resolução
Gerar uma chave do gateway no portal de saudação e usar Olá cópia botão toocopy Olá chave inteira. Em seguida, cole-o no gateway de saudação do tooregister janela.

### <a name="5-problem"></a>5. Problema
Talvez você veja Olá a seguinte mensagem de erro quando você estiver registrando um gateway.

`Error: hello gateway key is invalid or empty. Specify a valid gateway key from hello portal.`

![A chave do gateway é inválida ou está vazia](media/data-factory-troubleshoot-gateway-issues/gateway-key-is-invalid-or-empty.png)

#### <a name="cause"></a>Causa
chave do gateway Olá tiver sido regenerada ou Olá gateway foi excluído no hello portal do Azure. Ele também pode ocorrer se a instalação do Gateway de gerenciamento de dados de saudação não é mais recente.

#### <a name="resolution"></a>Resolução
Verifique se a instalação do Gateway de gerenciamento de dados de saudação versão mais recente do hello, você pode encontrar a versão mais recente da saudação na Olá Microsoft [Centro de download](https://go.microsoft.com/fwlink/p/?LinkId=271260).

Se a instalação for atual / mais recente e gateway ainda existe no Portal, regenerar chave do gateway Olá no hello portal do Azure e usar Olá Olá cópia botão toocopy toda chave e, em seguida, cole-o neste gateway de saudação do tooregister de janela. Caso contrário, recrie o gateway hello e recomeçar.

### <a name="6-problem"></a>6. Problema
Talvez você veja Olá a seguinte mensagem de erro quando você estiver registrando um gateway.

`Error: Gateway has been online for a while, then shows “Gateway is not registered” with hello status “Gateway key is invalid”`

![A chave do gateway é inválida ou está vazia](media/data-factory-troubleshoot-gateway-issues/gateway-not-registered-key-invalid.png)

#### <a name="cause"></a>Causa
Esse erro pode acontecer porque Olá gateway foi excluído ou chave do gateway associado Olá tiver sido regenerada.

#### <a name="resolution"></a>Resolução
Se Olá gateway foi excluído, crie novamente o gateway de saudação do portal de saudação, clique em **registrar**, copie a chave de saudação do portal hello, cole-o e tente tooregister gateway de saudação.

Se o gateway Olá ainda existe, mas sua chave tiver sido regenerada, use o hello novo tooregister chave Olá gateway. Se você não tiver chave hello, regenerar chave de saudação novamente do portal de saudação.

### <a name="7-problem"></a>7. Problema
Quando você estiver registrando um gateway, você pode precisar tooenter caminho e a senha de um certificado.

![Especificar certificado](media/data-factory-troubleshoot-gateway-issues/specify-certificate.png)

#### <a name="cause"></a>Causa
Olá gateway foi registrado em outros computadores antes. Durante o registro inicial de saudação de um gateway, um certificado de criptografia foi associado ao gateway hello. certificado Olá pode ser gerado automaticamente pelo gateway hello ou fornecido pelo usuário hello.  Esse certificado é usado tooencrypt credenciais saudação do repositório de dados (serviço vinculado).  

![Exportar o certificado](media/data-factory-troubleshoot-gateway-issues/export-certificate.png)

Quando restaurar gateway Olá em uma máquina host diferente, solicita que o Assistente de registro Olá para esse certificado toodecrypt credenciais previamente criptografado com esse certificado.  Sem esse certificado, credenciais Olá não podem ser descriptografadas pelo novo gateway de saudação e execuções de atividade de cópia subsequentes associadas com esse novo gateway falharão.  

#### <a name="resolution"></a>Resolução
Se você exportou o certificado de credencial de saudação de máquina de gateway original Olá usando Olá **exportar** botão Olá **configurações** guia no Data Management Gateway Configuration Manager, use Olá certificado aqui.

Não é possível ignorar este estágio ao recuperar um gateway. Se Olá certificado estiver ausente, você precisa toodelete Olá gateway do portal hello e recriar um novo gateway.  Além disso, atualize todos os serviços vinculados que são relacionadas toohello gateway por precisar reinserir suas credenciais.

### <a name="8-problem"></a>8. Problema
Talvez você veja Olá a seguinte mensagem de erro.

`Error: hello remote server returned an error: (407) Proxy Authentication Required.`

#### <a name="cause"></a>Causa
Esse erro ocorre quando o gateway estiver em um ambiente que requer um proxy HTTP tooaccess recursos da Internet, ou a senha de autenticação do proxy for alterada, mas não é atualizado adequadamente no seu gateway.

#### <a name="resolution"></a>Resolução
Siga as instruções de Olá Olá [considerações sobre o servidor Proxy](#proxy-server-considerations) seção deste artigo e definir configurações de proxy com o Gerenciador de Gateway de gerenciamento de configuração do dados.

## <a name="gateway-is-online-with-limited-functionality"></a>O gateway está online com funcionalidade limitada
### <a name="1-problem"></a>1. Problema
Você ver o status de saudação do gateway Olá online com funcionalidade limitada.

#### <a name="cause"></a>Causa
Consulte status de saudação do gateway Olá online com funcionalidade limitada para uma saudação motivos a seguir:

* Gateway não pode se conectar a toocloud serviço por meio do barramento de serviço do Azure.
* Serviço de nuvem não pode se conectar a toogateway por meio do barramento de serviço.

Quando o gateway Olá estiver online com funcionalidade limitada, talvez não seja pipelines de dados de toocreate toouse capaz de saudação Assistente para cópia de fábrica de dados para copiar dados tooor de armazenamentos de dados local. Como alternativa, você pode usar o Editor de fábrica de dados no portal de hello, Visual Studio ou o Azure PowerShell.

#### <a name="resolution"></a>Resolução
Resolução para esse problema (online com funcionalidade limitada) baseia-se gateway Olá não é possível conectar-se o serviço de nuvem toohello ou Olá outra maneira. Olá seções a seguir fornece essas resoluções.

### <a name="2-problem"></a>2. Problema
Você verá Olá erro a seguir.

`Error: Gateway cannot connect toocloud service through service bus`

![Gateway não pode se conectar a serviços toocloud](media/data-factory-troubleshoot-gateway-issues/gateway-cannot-connect-to-cloud-service.png)

#### <a name="cause"></a>Causa
Gateway não é possível conectar o serviço de nuvem toohello por meio do barramento de serviço.

#### <a name="resolution"></a>Resolução
Execute o gateway de saudação tooget essas etapas novamente online:

1. Permitir que o endereço IP no computador do gateway hello e firewall corporativo Olá regras de saída. Você pode localizar endereços IP de saudação Log de eventos do Windows (ID = = 401): uma tentativa foi feita tooaccess um soquete de uma maneira proibida pelas permissões de acesso XX. XX. XX. XX:9350.
* Defina configurações de proxy no gateway hello. Consulte Olá [considerações sobre o servidor Proxy](#proxy-server-considerations) seção para obter detalhes.
* Habilite portas de saída 5671 e 9350-9354 em ambos os Olá Firewall do Windows no computador do gateway hello e firewall corporativo hello. Consulte Olá [portas e firewall](#ports-and-firewall) seção para obter detalhes. Esta etapa é opcional, mas recomendada devido a considerações sobre desempenho.

### <a name="3-problem"></a>3. Problema
Você verá Olá erro a seguir.

`Error: Cloud service cannot connect toogateway through service bus.`

#### <a name="cause"></a>Causa
Um erro transitório na conectividade de rede.

#### <a name="resolution"></a>Resolução
Execute o gateway de saudação tooget essas etapas novamente online:

1. Aguarde alguns minutos, conectividade hello será recuperada automaticamente quando o erro Olá foi eliminado.
* Se Olá erro persistir, reinicie o serviço de gateway de saudação.

## <a name="failed-tooauthor-linked-service"></a>Serviço vinculado de tooauthor com falha
### <a name="problem"></a>Problema
Você poderá ver esse erro quando você tentar toouse Gerenciador de credenciais em credenciais da saudação tooinput portal para um novo serviço vinculado, ou atualizar as credenciais para um serviço vinculado existente.

`Error: hello data store '<Server>/<Database>' cannot be reached. Check connection settings for hello data source.`

Quando você vir esse erro, a página de configurações de saudação do Data Management Gateway Configuration Manager pode parecer com hello captura de tela a seguir.

![Não é possível acessar o banco de dados](media/data-factory-troubleshoot-gateway-issues/database-cannot-be-reached.png)

#### <a name="cause"></a>Causa
certificado SSL Olá pode ter perdido no computador do gateway hello. computador do gateway Olá não é possível carregar o certificado Olá atualmente que é usado para criptografia SSL. Você também poderá ver uma mensagem de erro no log de eventos de saudação que é semelhante toohello mensagem a seguir.

 `Unable tooget hello gateway settings from cloud service. Check hello gateway key and hello network connection. (Certificate with thumbprint cannot be loaded.)`

#### <a name="resolution"></a>Resolução
Siga o problema de saudação de toosolve essas etapas:

1. Inicie o Gerenciador de Configuração do Gateway de Gerenciamento de Dados.
2. Alternar toohello **configurações** guia.  
3. Clique em Olá **alteração** certificado SSL do botão toochange hello.

   ![botão Alterar certificado](media/data-factory-troubleshoot-gateway-issues/change-button-ssl-certificate.png)
4. Selecione um novo certificado como certificado SSL da saudação. Use qualquer certificado SSL gerado por você mesmo ou por qualquer organização.

   ![Especificar certificado](media/data-factory-troubleshoot-gateway-issues/specify-http-end-point.png)

## <a name="copy-activity-fails"></a>Falha na atividade de cópia
### <a name="problem"></a>Problema
Você pode notar Olá após falha de "UserErrorFailedToConnectToSqlserver" depois de configurar um pipeline no portal de saudação.

`Error: Copy activity encountered a user error: ErrorCode=UserErrorFailedToConnectToSqlServer,'Type=Microsoft.DataTransfer.Common.Shared.HybridDeliveryException,Message=Cannot connect tooSQL Server`

#### <a name="cause"></a>Causa
Isso pode ocorrer por diferentes motivos e a mitigação varia de acordo.

#### <a name="resolution"></a>Resolução
Permitir conexões TCP de saída pela porta TCP/1433 no saudação do lado do cliente de Gateway de gerenciamento de dados antes de se conectar tooan banco de dados SQL.

Se o banco de dados de destino de saudação é um banco de dados do SQL Azure, verificar SQL Server configurações do firewall para o Azure também.

Consulte Olá seção tootest Olá conexão toohello dados o repositório local a seguir.

## <a name="data-store-connection-or-driver-related-errors"></a>Erro de conexão com o armazenamento de dados ou erros relacionados a drivers
Se você ver dados armazenar conexão ou erros relacionados a drivers, conclua Olá etapas a seguir:

1. Inicie o Gerenciador de configuração de Gateway de gerenciamento de dados no computador do gateway hello.
2. Alternar toohello **diagnóstico** guia.
3. Em **Conexão de teste**, adicionar valores de grupo de gateway hello.
4. Clique em **teste** toosee se você puder se conectar toohello local fonte de dados do computador do gateway hello usando Olá informações de conexão e credenciais. Se a conexão de teste Olá ainda falhar depois de instalar um driver, reinicialização Olá gateway para que ele toopick a alteração mais recente hello.

![Testar a conexão na guia Diagnóstico](media/data-factory-troubleshoot-gateway-issues/test-connection-in-diagnostics-tab.png)

## <a name="gateway-logs"></a>Logs do gateway
### <a name="send-gateway-logs-toomicrosoft"></a>Enviar tooMicrosoft de logs do gateway
Entrar em contato com a Ajuda do Microsoft Support tooget com solução de problemas do gateway, você pode ser solicitado tooshare seus logs do gateway. Com versão de saudação do gateway hello, você pode compartilhar logs do gateway necessária com dois cliques de botão no Data Management Gateway Configuration Manager.    

1. Alternar toohello **diagnóstico** guia no Data Management Gateway Configuration Manager.

    ![Gateway de Gerenciamento de Dados - guia Diagnóstico](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-diagnostics-tab.png)
2. Clique em **enviar Logs** Olá toosee caixa de diálogo a seguir.

    ![Envio de logs do Gateway de Gerenciamento de Dados](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-dialog.png)
3. (Opcional) Clique em **exibir logs** tooreview logs no Visualizador de eventos de saudação.
4. (Opcional) Clique em **privacidade** tooreview Microsoft web services declaração de privacidade.
5. Quando estiver satisfeito com o que você está prestes a tooupload, clique em **enviar Logs de** tooactually enviar logs de saudação do hello tooMicrosoft última de sete dias para solução de problemas. Você deve ver o status de Olá da operação de envio de logs Olá conforme Olá captura de tela a seguir.

    ![Gateway de Gerenciamento de Dados – status de Enviar logs](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-status.png)
6. Após a conclusão da operação de hello, verá uma caixa de diálogo conforme Olá captura de tela a seguir.

    ![Gateway de Gerenciamento de Dados – status de Enviar logs](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-result.png)
7. Salvar Olá **relatório ID** e compartilhá-lo com o Microsoft Support. Olá relatório ID é usada toolocate logs do gateway Olá que você carregou para solução de problemas.  ID do relatório Olá também serão salvos no Visualizador de eventos de saudação.  Você pode encontrá-lo, observando a ID do evento hello "25" e verifique Olá data e hora.

    ![Gateway de Gerenciamento de Dados – ID de relatório de Enviar logs](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-report-id.png)    

### <a name="archive-gateway-logs-on-gateway-host-machine"></a>Arquivar logs de gateway no computador host de gateway
Existem alguns cenários em que há problemas de gateway e não é possível compartilhar logs do gateway diretamente:

* Você instala o gateway hello e registrar gateway Olá manualmente.
* Tente o gateway de saudação tooregister com uma chave regenerada na Data Management Gateway Configuration Manager.
* Tente toosend logs e o serviço de host do gateway de saudação não pode ser conectado.

Nesses casos, você pode salvar os logs de gateway como um arquivo zip e compartilhá-los quando contatar o suporte da Microsoft. Por exemplo, se você receber um erro ao registrar o gateway hello como mostrado no hello captura de tela a seguir.   

![Gateway de Gerenciamento de Dados – Erro de registro](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-registration-error.png)

Clique em Olá **arquivar os logs do gateway** link tooarchive salvar os logs e, em seguida, compartilhe o arquivo zip de saudação com o suporte da Microsoft.

![Gateway de Gerenciamento de Dados - Arquivar logs](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-archive-logs.png)

### <a name="locate-gateway-logs"></a>Localizar os logs do gateway
Você pode encontrar informações de log detalhado de gateway nos logs de eventos do Windows hello.

1. Inicie o **Visualizador de eventos** do Windows.
2. Localize os logs no hello **Logs de aplicativos e serviços** > **Data Management Gateway** pasta.

 Quando você estiver solucionando problemas relacionados ao gateway, procure eventos de nível de erro no Visualizador de eventos de saudação.

![Gateway de Gerenciamento de Dados – Logs no visualizador de eventos](media/data-factory-troubleshoot-gateway-issues/gateway-logs-event-viewer.png)
