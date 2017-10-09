



Dependendo do ambiente e opções, script hello pode criar todos os infraestrutura de cluster hello, incluindo Olá rede virtual do Azure, contas de armazenamento, serviços de nuvem, controlador de domínio, bancos de dados SQL locais ou remotos, nó principal e cluster adicionais nós. Como alternativa, script hello pode usar a infraestrutura do Azure já existente e criar somente Olá nós de cluster HPC.

Para obter informações sobre o planejamento de um cluster de HPC Pack, consulte Olá [avaliação do produto e planejamento](https://technet.microsoft.com/library/jj899596.aspx) e [Introdução](https://technet.microsoft.com/library/jj899590.aspx) conteúdo Olá Biblioteca TechNet do HPC Pack 2012 R2.

## <a name="prerequisites"></a>Pré-requisitos
* **Assinatura do Azure**: você pode usar uma assinatura em qualquer serviço Global Azure ou Azure China hello. Seus limites de assinatura afetam o número de saudação e tipo de nós de cluster, que você pode implantar. Para obter informações, consulte [Limites, cotas e restrições de serviço e assinatura do Azure](../articles/azure-subscription-service-limits.md).
* **Computador cliente com Windows com o Azure PowerShell 0.8.10 ou posterior instalado e configurado**: consulte [começar com o Azure PowerShell](/powershell/azureps-cmdlets-docs) para instalação instruções e etapas tooconnect tooyour assinatura do Azure.
* **Script de implantação IaaS do HPC Pack**: Baixe e descompacte a versão mais recente de saudação do script Olá Olá [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949). Verifique a versão de saudação do script hello executando `New-HPCIaaSCluster.ps1 –Version`. Este artigo se baseia na versão 4.5.2 do script hello.
* **Arquivo de configuração do script**: criar um arquivo XML que o script hello usa cluster HPC tooconfigure hello. Para obter informações e exemplos, consulte as seções mais adiante neste artigo e Olá arquivo Manual.rtf que acompanha o script de implantação de saudação.

## <a name="syntax"></a>Sintaxe
```PowerShell
New-HPCIaaSCluster.ps1 [-ConfigFile] <String> [-AdminUserName]<String> [[-AdminPassword] <String>] [[-HPCImageName] <String>] [[-LogFile] <String>] [-Force] [-NoCleanOnFailure] [-PSSessionSkipCACheck] [<CommonParameters>]
```
> [!NOTE]
> Execute o script hello como um administrador.
> 
> 

### <a name="parameters"></a>parâmetros
* **ConfigFile**: Especifica o caminho do arquivo de saudação do cluster HPC Olá configuração arquivo toodescribe hello. Ver mais informações sobre o arquivo de configuração Olá neste tópico, ou no arquivo hello Manual.rtf na pasta Olá que contém o script hello.
* **AdminUserName**: Especifica o nome de usuário de saudação. Se a floresta de domínio Olá criada pelo script hello, isso torna-se nome de usuário de administrador local Olá para todas as máquinas virtuais e o nome do administrador de domínio hello. Se já existir uma floresta de domínio hello, isso Especifica o usuário de domínio Olá Olá tooinstall de nome de usuário de administrador local HPC Pack.
* **AdminPassword**: Especifica a senha do administrador do hello. Se não for especificado na linha de comando hello, script hello solicita tooinput senha de saudação.
* **HPCImageName** (opcional): especifica nome de imagem de VM do HPC Pack Olá usado cluster HPC toodeploy hello. Ele deve ser uma imagem fornecida pela Microsoft HPC Pack de saudação do Azure Marketplace. Se hello (recomendado normalmente), não especificado script escolhe hello mais recente publicada [HPC Pack 2012 R2 imagem](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/). imagem mais recente Olá baseia-se no Windows Server 2012 R2 Datacenter com HPC Pack 2012 R2 Update 3 instalado.
  
  > [!NOTE]
  > A implantação falhará se você não especificar uma imagem válida do Pacote HPC.
  > 
  > 
* **Arquivo de log** (opcional): Especifica o caminho do arquivo de log de implantação de saudação. Se não for especificado, o script hello cria um arquivo de log no diretório temp de saudação do computador Olá executando o script hello.
* **Forçar** (opcional): suprime todos os prompts de confirmação de saudação.
* **NoCleanOnFailure** (opcional): Especifica que Olá VMs do Azure que não são implantados com êxito não serão removidas. Remover essas VMs manualmente antes de executar novamente a implantação de Olá Olá script toocontinue ou Olá implantação poderá falhar.
* **PSSessionSkipCACheck** (opcional): para cada serviço de nuvem com VMs implantadas por esse script, um certificado autoassinado é gerado automaticamente pelo Azure e Olá todas as VMs no serviço de nuvem Olá usar este certificado Olá padrão do Windows Certificado remoto Management (WinRM). toodeploy recursos do HPC nessas VMs do Azure, Olá script por padrão instala temporariamente esses certificados no hello computador Local\\repositório de autoridades de certificação de raiz confiável do toosuppress de computador cliente Olá Olá segurança "autoridade de certificação não confiável" Erro durante a execução do script. certificados de saudação são removidos quando Olá script for concluído. Se esse parâmetro for especificado, certificados de saudação não estão instalados no computador do cliente de saudação e aviso de segurança de saudação é suprimido.
  
  > [!IMPORTANT]
  > Esse parâmetro não é recomendado para implantações de produção.
  > 
  > 

### <a name="example"></a>Exemplo
Olá, exemplo a seguir cria um cluster de HPC Pack usando o arquivo de configuração *MyConfigFile.xml*e especifica as credenciais de administrador para instalar o cluster de saudação.

```PowerShell
.\New-HPCIaaSCluster.ps1 –ConfigFile MyConfigFile.xml -AdminUserName <username> –AdminPassword <password>
```

### <a name="additional-considerations"></a>Considerações adicionais
* script Hello, opcionalmente, pode habilitar o envio de trabalho por meio do portal de web do HPC Pack hello ou hello HPC Pack REST API.
* script Hello opcionalmente pode executar scripts de pré e pós-configuração personalizados no nó de cabeçalho Olá tooinstall o software adicional ou definir outras configurações.

## <a name="configuration-file"></a>Arquivo de configuração
arquivo de configuração de saudação para script de implantação de saudação é um arquivo XML. arquivo de esquema Olá HPCIaaSClusterConfig.xsd está na pasta de script de implantação de IaaS do HPC Pack hello. **IaaSClusterConfig** é elemento de raiz Olá Olá do arquivo de configuração, que contém elementos filhos de saudação descritos em detalhes no arquivo hello Manual.rtf na pasta de script de implantação de saudação.

