1. <span data-ttu-id="fda9c-101">Copie o instalador para uma pasta local (digamos, /tmp) no servidor que você deseja proteger.</span><span class="sxs-lookup"><span data-stu-id="fda9c-101">Copy the installer to a local folder (for example, /tmp) on the server that you want to protect.</span></span> <span data-ttu-id="fda9c-102">Execute os seguintes comandos em um terminal:</span><span class="sxs-lookup"><span data-stu-id="fda9c-102">In a terminal, run the following commands:</span></span>
  ```
  cd /tmp
  tar -xvzf Microsoft-ASR_UA*release.tar.gz
  ```
2. <span data-ttu-id="fda9c-103">Para instalar o Serviço de Mobilidade, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="fda9c-103">To install Mobility Service, run the following command:</span></span>

  ```
  sudo ./install -d <Install Location> -r MS -v VmWare -q
  ```
3. <span data-ttu-id="fda9c-104">Depois que a instalação for concluída, o Serviço de Mobilidade precisa se registrar no servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="fda9c-104">Once installation is complete, the Mobility Service needs to get registered to the configuration server.</span></span> <span data-ttu-id="fda9c-105">Execute o seguinte comando para registrar o Serviço de Mobilidade com o servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="fda9c-105">Run the following command to register the Mobility Service with Configuration server.</span></span>

  ```
  /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <CSIP> -P /var/passphrase.txt
  ```

#### <a name="mobility-service-installer-command-line"></a><span data-ttu-id="fda9c-106">Linha de comando do instalador do Serviço de Mobilidade</span><span class="sxs-lookup"><span data-stu-id="fda9c-106">Mobility Service installer command-line</span></span>

```
Usage:
./install -d <Install Location> -r <MS|MT> -v VmWare -q
```

|<span data-ttu-id="fda9c-107">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="fda9c-107">Parameter</span></span>|<span data-ttu-id="fda9c-108">Tipo</span><span class="sxs-lookup"><span data-stu-id="fda9c-108">Type</span></span>|<span data-ttu-id="fda9c-109">Descrição</span><span class="sxs-lookup"><span data-stu-id="fda9c-109">Description</span></span>|<span data-ttu-id="fda9c-110">Valores possíveis</span><span class="sxs-lookup"><span data-stu-id="fda9c-110">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="fda9c-111">-r</span><span class="sxs-lookup"><span data-stu-id="fda9c-111">-r</span></span> |<span data-ttu-id="fda9c-112">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="fda9c-112">Mandatory</span></span>|<span data-ttu-id="fda9c-113">Especifica se o Serviço de Mobilidade (MS) deve ser instalado ou se o MasterTarget (MT) deve ser instalado</span><span class="sxs-lookup"><span data-stu-id="fda9c-113">Specifies whether Mobility Service (MS) should be installed or MasterTarget(MT) should be installed</span></span>|<span data-ttu-id="fda9c-114">MS</span><span class="sxs-lookup"><span data-stu-id="fda9c-114">MS</span></span> </br> <span data-ttu-id="fda9c-115">MT</span><span class="sxs-lookup"><span data-stu-id="fda9c-115">MT</span></span>|
|<span data-ttu-id="fda9c-116">-d</span><span class="sxs-lookup"><span data-stu-id="fda9c-116">-d</span></span> |<span data-ttu-id="fda9c-117">Opcional</span><span class="sxs-lookup"><span data-stu-id="fda9c-117">Optional</span></span>|<span data-ttu-id="fda9c-118">Local onde o Serviço de Mobilidade será instalado</span><span class="sxs-lookup"><span data-stu-id="fda9c-118">Location where Mobility Service will be installed</span></span>|<span data-ttu-id="fda9c-119">/usr/local/ASR</span><span class="sxs-lookup"><span data-stu-id="fda9c-119">/usr/local/ASR</span></span>|
|<span data-ttu-id="fda9c-120">-v</span><span class="sxs-lookup"><span data-stu-id="fda9c-120">-v</span></span>|<span data-ttu-id="fda9c-121">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="fda9c-121">Mandatory</span></span>|<span data-ttu-id="fda9c-122">Especifica a plataforma onde o Serviço de Mobilidade está sendo instalado</span><span class="sxs-lookup"><span data-stu-id="fda9c-122">Specifies the platform on which the Mobility Service is getting installed</span></span> </br> </br><span data-ttu-id="fda9c-123">- **VMware** : use esse valor se você estiver instalando o serviço de mobilidade em uma VM em execução no *Hosts do VMware vSphere ESXi*, *Hosts do Hyper-V* e *Servidores Físicos*</span><span class="sxs-lookup"><span data-stu-id="fda9c-123">- **VMware** : use this value if you are installing mobility service on a VM running on *VMware vSphere ESXi Hosts*, *Hyper-V Hosts* and *Phsyical Servers*</span></span> </br> <span data-ttu-id="fda9c-124">- **Azure** : use esse valor se você estiver instalando o agente em uma VM IaaS do Azure</span><span class="sxs-lookup"><span data-stu-id="fda9c-124">- **Azure** : use this value if you are installing agent on a Azure IaaS VM</span></span>| <span data-ttu-id="fda9c-125">VMware</span><span class="sxs-lookup"><span data-stu-id="fda9c-125">VMware</span></span> </br> <span data-ttu-id="fda9c-126">As tabelas</span><span class="sxs-lookup"><span data-stu-id="fda9c-126">Azure</span></span>|
|<span data-ttu-id="fda9c-127">-q</span><span class="sxs-lookup"><span data-stu-id="fda9c-127">-q</span></span>|<span data-ttu-id="fda9c-128">Opcional</span><span class="sxs-lookup"><span data-stu-id="fda9c-128">Optional</span></span>|<span data-ttu-id="fda9c-129">Especifica a execução do instalador no modo silencioso</span><span class="sxs-lookup"><span data-stu-id="fda9c-129">Specifies to run installer in silent mode</span></span>| <span data-ttu-id="fda9c-130">N/D </span><span class="sxs-lookup"><span data-stu-id="fda9c-130">N/A</span></span>|


#### <a name="mobility-service-configuration-command-line"></a><span data-ttu-id="fda9c-131">Linha de comando de configuração do Serviço de Mobilidade</span><span class="sxs-lookup"><span data-stu-id="fda9c-131">Mobility Service configuration command-line</span></span>

```
Usage:
cd /usr/local/ASR/Vx/bin
UnifiedAgentConfigurator.sh -i <CSIP> -P <PassphraseFilePath>
```

|<span data-ttu-id="fda9c-132">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="fda9c-132">Parameter</span></span>|<span data-ttu-id="fda9c-133">Tipo</span><span class="sxs-lookup"><span data-stu-id="fda9c-133">Type</span></span>|<span data-ttu-id="fda9c-134">Descrição</span><span class="sxs-lookup"><span data-stu-id="fda9c-134">Description</span></span>|<span data-ttu-id="fda9c-135">Valores possíveis</span><span class="sxs-lookup"><span data-stu-id="fda9c-135">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="fda9c-136">-i</span><span class="sxs-lookup"><span data-stu-id="fda9c-136">-i</span></span> |<span data-ttu-id="fda9c-137">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="fda9c-137">Mandatory</span></span>|<span data-ttu-id="fda9c-138">IP do Servidor de Configuração</span><span class="sxs-lookup"><span data-stu-id="fda9c-138">IP of the Configuration Server</span></span>|<span data-ttu-id="fda9c-139">Qualquer endereço IP válido</span><span class="sxs-lookup"><span data-stu-id="fda9c-139">Any valid IP Address</span></span>|
|<span data-ttu-id="fda9c-140">-P</span><span class="sxs-lookup"><span data-stu-id="fda9c-140">-P</span></span> |<span data-ttu-id="fda9c-141">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="fda9c-141">Mandatory</span></span>|<span data-ttu-id="fda9c-142">Caminho completo do arquivo onde a senha de conexão é salva</span><span class="sxs-lookup"><span data-stu-id="fda9c-142">Full file path the file where the connection passphrase is saved</span></span>|<span data-ttu-id="fda9c-143">Qualquer pasta válida</span><span class="sxs-lookup"><span data-stu-id="fda9c-143">Any valid folder</span></span>|
