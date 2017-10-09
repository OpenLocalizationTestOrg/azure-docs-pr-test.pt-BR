1. <span data-ttu-id="c3c60-101">Copie Olá instalador tooa pasta local (por exemplo, /tmp) no servidor de saudação que você deseja tooprotect.</span><span class="sxs-lookup"><span data-stu-id="c3c60-101">Copy hello installer tooa local folder (for example, /tmp) on hello server that you want tooprotect.</span></span> <span data-ttu-id="c3c60-102">Em um terminal, execute Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="c3c60-102">In a terminal, run hello following commands:</span></span>
  ```
  cd /tmp
  tar -xvzf Microsoft-ASR_UA*release.tar.gz
  ```
2. <span data-ttu-id="c3c60-103">tooinstall serviço de mobilidade, executar Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="c3c60-103">tooinstall Mobility Service, run hello following command:</span></span>

  ```
  sudo ./install -d <Install Location> -r MS -v VmWare -q
  ```
3. <span data-ttu-id="c3c60-104">Após a conclusão da instalação, Olá serviço de mobilidade precisa de servidor de configuração tooget toohello registrado.</span><span class="sxs-lookup"><span data-stu-id="c3c60-104">Once installation is complete, hello Mobility Service needs tooget registered toohello configuration server.</span></span> <span data-ttu-id="c3c60-105">Execute Olá Olá tooregister de comando, serviço de mobilidade com o servidor de configuração a seguir.</span><span class="sxs-lookup"><span data-stu-id="c3c60-105">Run hello following command tooregister hello Mobility Service with Configuration server.</span></span>

  ```
  /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <CSIP> -P /var/passphrase.txt
  ```

#### <a name="mobility-service-installer-command-line"></a><span data-ttu-id="c3c60-106">Linha de comando do instalador do Serviço de Mobilidade</span><span class="sxs-lookup"><span data-stu-id="c3c60-106">Mobility Service installer command-line</span></span>

```
Usage:
./install -d <Install Location> -r <MS|MT> -v VmWare -q
```

|<span data-ttu-id="c3c60-107">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c3c60-107">Parameter</span></span>|<span data-ttu-id="c3c60-108">Tipo</span><span class="sxs-lookup"><span data-stu-id="c3c60-108">Type</span></span>|<span data-ttu-id="c3c60-109">Descrição</span><span class="sxs-lookup"><span data-stu-id="c3c60-109">Description</span></span>|<span data-ttu-id="c3c60-110">Valores possíveis</span><span class="sxs-lookup"><span data-stu-id="c3c60-110">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="c3c60-111">-r</span><span class="sxs-lookup"><span data-stu-id="c3c60-111">-r</span></span> |<span data-ttu-id="c3c60-112">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="c3c60-112">Mandatory</span></span>|<span data-ttu-id="c3c60-113">Especifica se o Serviço de Mobilidade (MS) deve ser instalado ou se o MasterTarget (MT) deve ser instalado</span><span class="sxs-lookup"><span data-stu-id="c3c60-113">Specifies whether Mobility Service (MS) should be installed or MasterTarget(MT) should be installed</span></span>|<span data-ttu-id="c3c60-114">MS</span><span class="sxs-lookup"><span data-stu-id="c3c60-114">MS</span></span> </br> <span data-ttu-id="c3c60-115">MT</span><span class="sxs-lookup"><span data-stu-id="c3c60-115">MT</span></span>|
|<span data-ttu-id="c3c60-116">-d</span><span class="sxs-lookup"><span data-stu-id="c3c60-116">-d</span></span> |<span data-ttu-id="c3c60-117">Opcional</span><span class="sxs-lookup"><span data-stu-id="c3c60-117">Optional</span></span>|<span data-ttu-id="c3c60-118">Local onde o Serviço de Mobilidade será instalado</span><span class="sxs-lookup"><span data-stu-id="c3c60-118">Location where Mobility Service will be installed</span></span>|<span data-ttu-id="c3c60-119">/usr/local/ASR</span><span class="sxs-lookup"><span data-stu-id="c3c60-119">/usr/local/ASR</span></span>|
|<span data-ttu-id="c3c60-120">-v</span><span class="sxs-lookup"><span data-stu-id="c3c60-120">-v</span></span>|<span data-ttu-id="c3c60-121">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="c3c60-121">Mandatory</span></span>|<span data-ttu-id="c3c60-122">Especifica a plataforma de saudação em qual Olá serviço de mobilidade está obtendo instalado</span><span class="sxs-lookup"><span data-stu-id="c3c60-122">Specifies hello platform on which hello Mobility Service is getting installed</span></span> </br> </br><span data-ttu-id="c3c60-123">- **VMware** : use esse valor se você estiver instalando o serviço de mobilidade em uma VM em execução no *Hosts do VMware vSphere ESXi*, *Hosts do Hyper-V* e *Servidores Físicos*</span><span class="sxs-lookup"><span data-stu-id="c3c60-123">- **VMware** : use this value if you are installing mobility service on a VM running on *VMware vSphere ESXi Hosts*, *Hyper-V Hosts* and *Phsyical Servers*</span></span> </br> <span data-ttu-id="c3c60-124">- **Azure** : use esse valor se você estiver instalando o agente em uma VM IaaS do Azure</span><span class="sxs-lookup"><span data-stu-id="c3c60-124">- **Azure** : use this value if you are installing agent on a Azure IaaS VM</span></span>| <span data-ttu-id="c3c60-125">VMware</span><span class="sxs-lookup"><span data-stu-id="c3c60-125">VMware</span></span> </br> <span data-ttu-id="c3c60-126">As tabelas</span><span class="sxs-lookup"><span data-stu-id="c3c60-126">Azure</span></span>|
|<span data-ttu-id="c3c60-127">-q</span><span class="sxs-lookup"><span data-stu-id="c3c60-127">-q</span></span>|<span data-ttu-id="c3c60-128">Opcional</span><span class="sxs-lookup"><span data-stu-id="c3c60-128">Optional</span></span>|<span data-ttu-id="c3c60-129">Especifica o instalador toorun no modo silencioso</span><span class="sxs-lookup"><span data-stu-id="c3c60-129">Specifies toorun installer in silent mode</span></span>| <span data-ttu-id="c3c60-130">N/D</span><span class="sxs-lookup"><span data-stu-id="c3c60-130">N/A</span></span>|


#### <a name="mobility-service-configuration-command-line"></a><span data-ttu-id="c3c60-131">Linha de comando de configuração do Serviço de Mobilidade</span><span class="sxs-lookup"><span data-stu-id="c3c60-131">Mobility Service configuration command-line</span></span>

```
Usage:
cd /usr/local/ASR/Vx/bin
UnifiedAgentConfigurator.sh -i <CSIP> -P <PassphraseFilePath>
```

|<span data-ttu-id="c3c60-132">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c3c60-132">Parameter</span></span>|<span data-ttu-id="c3c60-133">Tipo</span><span class="sxs-lookup"><span data-stu-id="c3c60-133">Type</span></span>|<span data-ttu-id="c3c60-134">Descrição</span><span class="sxs-lookup"><span data-stu-id="c3c60-134">Description</span></span>|<span data-ttu-id="c3c60-135">Valores possíveis</span><span class="sxs-lookup"><span data-stu-id="c3c60-135">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="c3c60-136">-i</span><span class="sxs-lookup"><span data-stu-id="c3c60-136">-i</span></span> |<span data-ttu-id="c3c60-137">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="c3c60-137">Mandatory</span></span>|<span data-ttu-id="c3c60-138">Olá, servidor de configuração de IP</span><span class="sxs-lookup"><span data-stu-id="c3c60-138">IP of hello Configuration Server</span></span>|<span data-ttu-id="c3c60-139">Qualquer endereço IP válido</span><span class="sxs-lookup"><span data-stu-id="c3c60-139">Any valid IP Address</span></span>|
|<span data-ttu-id="c3c60-140">-P</span><span class="sxs-lookup"><span data-stu-id="c3c60-140">-P</span></span> |<span data-ttu-id="c3c60-141">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="c3c60-141">Mandatory</span></span>|<span data-ttu-id="c3c60-142">Arquivo de Olá do caminho completo do arquivo onde a senha de conexão de saudação é salvo</span><span class="sxs-lookup"><span data-stu-id="c3c60-142">Full file path hello file where hello connection passphrase is saved</span></span>|<span data-ttu-id="c3c60-143">Qualquer pasta válida</span><span class="sxs-lookup"><span data-stu-id="c3c60-143">Any valid folder</span></span>|
