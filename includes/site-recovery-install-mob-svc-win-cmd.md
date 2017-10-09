1. <span data-ttu-id="da088-101">Copie a pasta local de tooa instalador da saudação (por exemplo, C:\Temp) no servidor de saudação que você deseja tooprotect.</span><span class="sxs-lookup"><span data-stu-id="da088-101">Copy hello installer tooa local folder (for example, C:\Temp) on hello server that you want tooprotect.</span></span> <span data-ttu-id="da088-102">Execute Olá comandos a seguir como um administrador em um prompt de comando:</span><span class="sxs-lookup"><span data-stu-id="da088-102">Run hello following commands as an administrator at a command prompt:</span></span>

  ```
  cd C:\Temp
  ren Microsoft-ASR_UA*Windows*release.exe MobilityServiceInstaller.exe
  MobilityServiceInstaller.exe /q /x:C:\Temp\Extracted
  cd C:\Temp\Extracted.
  ```
2. <span data-ttu-id="da088-103">tooinstall serviço de mobilidade, executar Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="da088-103">tooinstall Mobility Service, run hello following command:</span></span>

  ```
  UnifiedAgent.exe /Role "MS" /InstallLocation "C:\Program Files (x86)\Microsoft Azure Site Recovery" /Platform "VmWare" /Silent
  ```
3. <span data-ttu-id="da088-104">Agente Olá deve toobe registrado com hello servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="da088-104">Now hello agent needs toobe registered with hello Configuration Server.</span></span>

  ```
  cd C:\Program Files (x86)\Microsoft Azure Site Recovery\agent
  UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
  ```

#### <a name="mobility-service-installer-command-line-arguments"></a><span data-ttu-id="da088-105">Argumentos de linha de comando do instalador do Serviço de Mobilidade</span><span class="sxs-lookup"><span data-stu-id="da088-105">Mobility Service installer command-line arguments</span></span>

```
Usage :
UnifiedAgent.exe /Role <MS|MT> /InstallLocation <Install Location> /Platform “VmWare” /Silent
```

| <span data-ttu-id="da088-106">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="da088-106">Parameter</span></span>|<span data-ttu-id="da088-107">Tipo</span><span class="sxs-lookup"><span data-stu-id="da088-107">Type</span></span>|<span data-ttu-id="da088-108">Descrição</span><span class="sxs-lookup"><span data-stu-id="da088-108">Description</span></span>|<span data-ttu-id="da088-109">Valores possíveis</span><span class="sxs-lookup"><span data-stu-id="da088-109">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="da088-110">/Role</span><span class="sxs-lookup"><span data-stu-id="da088-110">/Role</span></span>|<span data-ttu-id="da088-111">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="da088-111">Mandatory</span></span>|<span data-ttu-id="da088-112">Especifica se o Serviço de Mobilidade (MS) deve ser instalado ou se o MasterTarget (MT) deve ser instalado</span><span class="sxs-lookup"><span data-stu-id="da088-112">Specifies whether Mobility Service (MS) should be installed or MasterTarget(MT) should be installed</span></span>|<span data-ttu-id="da088-113">MS</span><span class="sxs-lookup"><span data-stu-id="da088-113">MS</span></span> </br> <span data-ttu-id="da088-114">MT</span><span class="sxs-lookup"><span data-stu-id="da088-114">MT</span></span>|
|<span data-ttu-id="da088-115">/InstallLocation</span><span class="sxs-lookup"><span data-stu-id="da088-115">/InstallLocation</span></span>|<span data-ttu-id="da088-116">Opcional</span><span class="sxs-lookup"><span data-stu-id="da088-116">Optional</span></span>|<span data-ttu-id="da088-117">Local onde o Serviço de Mobilidade está instalado</span><span class="sxs-lookup"><span data-stu-id="da088-117">Location where Mobility Service is installed</span></span>|<span data-ttu-id="da088-118">Qualquer pasta no computador de saudação</span><span class="sxs-lookup"><span data-stu-id="da088-118">Any folder on hello computer</span></span>|
|<span data-ttu-id="da088-119">/Platform</span><span class="sxs-lookup"><span data-stu-id="da088-119">/Platform</span></span>|<span data-ttu-id="da088-120">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="da088-120">Mandatory</span></span>|<span data-ttu-id="da088-121">Especifica a plataforma de saudação em qual Olá serviço de mobilidade está obtendo instalado</span><span class="sxs-lookup"><span data-stu-id="da088-121">Specifies hello platform on which hello Mobility Service is getting installed</span></span> </br> </br><span data-ttu-id="da088-122">- **VMware** : use esse valor se você estiver instalando o serviço de mobilidade em uma VM em execução no *Hosts do VMware vSphere ESXi*, *Hosts do Hyper-V* e *Servidores Físicos*</span><span class="sxs-lookup"><span data-stu-id="da088-122">- **VMware** : use this value if you are installing mobility service on a VM running on *VMware vSphere ESXi Hosts*, *Hyper-V Hosts* and *Phsyical Servers*</span></span> </br> <span data-ttu-id="da088-123">- **Azure** : use esse valor se você estiver instalando o agente em uma VM IaaS do Azure</span><span class="sxs-lookup"><span data-stu-id="da088-123">- **Azure** : use this value if you are installing agent on a Azure IaaS VM</span></span>| <span data-ttu-id="da088-124">VMware</span><span class="sxs-lookup"><span data-stu-id="da088-124">VMware</span></span> </br> <span data-ttu-id="da088-125">As tabelas</span><span class="sxs-lookup"><span data-stu-id="da088-125">Azure</span></span>|
|<span data-ttu-id="da088-126">/Silent</span><span class="sxs-lookup"><span data-stu-id="da088-126">/Silent</span></span>|<span data-ttu-id="da088-127">Opcional</span><span class="sxs-lookup"><span data-stu-id="da088-127">Optional</span></span>|<span data-ttu-id="da088-128">Especifica o instalador de saudação toorun no modo silencioso</span><span class="sxs-lookup"><span data-stu-id="da088-128">Specifies toorun hello installer in silent mode</span></span>| <span data-ttu-id="da088-129">ND</span><span class="sxs-lookup"><span data-stu-id="da088-129">NA</span></span>|

>[!TIP]
> <span data-ttu-id="da088-130">Olá logs de instalação podem ser encontrados em %ProgramData%\ASRSetupLogs\ASRUnifiedAgentInstaller.log</span><span class="sxs-lookup"><span data-stu-id="da088-130">hello setup logs can be found under %ProgramData%\ASRSetupLogs\ASRUnifiedAgentInstaller.log</span></span>

#### <a name="mobility-service-registration-command-line-arguments"></a><span data-ttu-id="da088-131">Argumentos da linha de comando de registro do Serviço de Mobilidade</span><span class="sxs-lookup"><span data-stu-id="da088-131">Mobility Service registration command-line arguments</span></span>

```
Usage :
UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
```

  | <span data-ttu-id="da088-132">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="da088-132">Parameter</span></span>|<span data-ttu-id="da088-133">Tipo</span><span class="sxs-lookup"><span data-stu-id="da088-133">Type</span></span>|<span data-ttu-id="da088-134">Descrição</span><span class="sxs-lookup"><span data-stu-id="da088-134">Description</span></span>|<span data-ttu-id="da088-135">Valores possíveis</span><span class="sxs-lookup"><span data-stu-id="da088-135">Possible values</span></span>|
  |-|-|-|-|
  |<span data-ttu-id="da088-136">/CSEndPoint</span><span class="sxs-lookup"><span data-stu-id="da088-136">/CSEndPoint</span></span> |<span data-ttu-id="da088-137">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="da088-137">Mandatory</span></span>|<span data-ttu-id="da088-138">Endereço IP do servidor de configuração de saudação</span><span class="sxs-lookup"><span data-stu-id="da088-138">IP address of hello configuration server</span></span>| <span data-ttu-id="da088-139">Qualquer endereço IP válido</span><span class="sxs-lookup"><span data-stu-id="da088-139">Any valid IP address</span></span>|
  |<span data-ttu-id="da088-140">/PassphraseFilePath</span><span class="sxs-lookup"><span data-stu-id="da088-140">/PassphraseFilePath</span></span>|<span data-ttu-id="da088-141">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="da088-141">Mandatory</span></span>|<span data-ttu-id="da088-142">Local de senha Olá</span><span class="sxs-lookup"><span data-stu-id="da088-142">Location of hello passphrase</span></span> |<span data-ttu-id="da088-143">Qualquer caminho de arquivo UNC ou local válido</span><span class="sxs-lookup"><span data-stu-id="da088-143">Any valid UNC or local file path</span></span>|


>[!TIP]
> <span data-ttu-id="da088-144">Olá AgentConfiguration logs podem ser encontrados em %ProgramData%\ASRSetupLogs\ASRUnifiedAgentConfigurator.log</span><span class="sxs-lookup"><span data-stu-id="da088-144">hello AgentConfiguration logs can be found under %ProgramData%\ASRSetupLogs\ASRUnifiedAgentConfigurator.log</span></span>
