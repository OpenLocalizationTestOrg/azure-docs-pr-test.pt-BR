## <span data-ttu-id="4ed60-101"><a name="os-config"></a>Adicionar sistema operacional do IP endereços tooa VM</span><span class="sxs-lookup"><span data-stu-id="4ed60-101"><a name="os-config"></a>Add IP addresses tooa VM operating system</span></span>

<span data-ttu-id="4ed60-102">Conecte-se e logon tooa VM que você criou com vários endereços IP privados.</span><span class="sxs-lookup"><span data-stu-id="4ed60-102">Connect and login tooa VM you created with multiple private IP addresses.</span></span> <span data-ttu-id="4ed60-103">Você deve adicionar manualmente todos os Olá endereços IP privados (incluindo Olá primário) que você adicionou toohello VM.</span><span class="sxs-lookup"><span data-stu-id="4ed60-103">You must manually add all hello private IP addresses (including hello primary) that you added toohello VM.</span></span> <span data-ttu-id="4ed60-104">Olá completo seguindo as etapas para seu sistema operacional VM:</span><span class="sxs-lookup"><span data-stu-id="4ed60-104">Complete hello following steps for your VM operating system:</span></span>

### <a name="windows"></a><span data-ttu-id="4ed60-105">Windows</span><span class="sxs-lookup"><span data-stu-id="4ed60-105">Windows</span></span>

1. <span data-ttu-id="4ed60-106">Em um prompt de comando, digite *ipconfig /all*.</span><span class="sxs-lookup"><span data-stu-id="4ed60-106">From a command prompt, type *ipconfig /all*.</span></span>  <span data-ttu-id="4ed60-107">Você só verá Olá *primário* endereço IP privado (por meio de DHCP).</span><span class="sxs-lookup"><span data-stu-id="4ed60-107">You only see hello *Primary* private IP address (through DHCP).</span></span>
2. <span data-ttu-id="4ed60-108">Tipo *ncpa.cpl* no prompt de comando de Olá tooopen Olá **conexões de rede** janela.</span><span class="sxs-lookup"><span data-stu-id="4ed60-108">Type *ncpa.cpl* in hello command prompt tooopen hello **Network connections** window.</span></span>
3. <span data-ttu-id="4ed60-109">Abrir as propriedades de saudação do adaptador apropriado Olá: **Conexão de área Local**.</span><span class="sxs-lookup"><span data-stu-id="4ed60-109">Open hello properties for hello appropriate adapter: **Local Area Connection**.</span></span>
4. <span data-ttu-id="4ed60-110">Clique duas vezes em versão do Protocolo de Internet 4 (IPv4).</span><span class="sxs-lookup"><span data-stu-id="4ed60-110">Double-click Internet Protocol version 4 (IPv4).</span></span>
5. <span data-ttu-id="4ed60-111">Selecione **Olá Use seguinte endereço IP** e digite Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ed60-111">Select **Use hello following IP address** and enter hello following values:</span></span>

    * <span data-ttu-id="4ed60-112">**Endereço IP**: insira Olá *primário* endereço IP privado</span><span class="sxs-lookup"><span data-stu-id="4ed60-112">**IP address**: Enter hello *Primary* private IP address</span></span>
    * <span data-ttu-id="4ed60-113">**Máscara de sub-rede**: defina com base na sua sub-rede.</span><span class="sxs-lookup"><span data-stu-id="4ed60-113">**Subnet mask**: Set based on your subnet.</span></span> <span data-ttu-id="4ed60-114">Por exemplo, se hello sub-rede é um /24 subrede e sub-rede Olá máscara é 255.255.255.0.</span><span class="sxs-lookup"><span data-stu-id="4ed60-114">For example, if hello subnet is a /24 subnet then hello subnet mask is 255.255.255.0.</span></span>
    * <span data-ttu-id="4ed60-115">**Gateway padrão**: Olá primeiro endereço IP na sub-rede hello.</span><span class="sxs-lookup"><span data-stu-id="4ed60-115">**Default gateway**: hello first IP address in hello subnet.</span></span> <span data-ttu-id="4ed60-116">Se sua sub-rede for 10.0.0.0/24, o endereço IP do gateway de saudação é 10.0.0.1.</span><span class="sxs-lookup"><span data-stu-id="4ed60-116">If your subnet is 10.0.0.0/24, then hello gateway IP address is 10.0.0.1.</span></span>
    * <span data-ttu-id="4ed60-117">Clique em **Olá usar endereços de servidor DNS a seguir** e digite Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ed60-117">Click **Use hello following DNS server addresses** and enter hello following values:</span></span>
        * <span data-ttu-id="4ed60-118">**Servidor DNS preferencial**: digite 168.63.129.16 se você não estiver usando seu próprio servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="4ed60-118">**Preferred DNS server**: If you are not using your own DNS server, enter 168.63.129.16.</span></span>  <span data-ttu-id="4ed60-119">Se você estiver usando seu próprio servidor DNS, digite o endereço IP de saudação do servidor.</span><span class="sxs-lookup"><span data-stu-id="4ed60-119">If you are using your own DNS server, enter hello IP address for your server.</span></span>
    * <span data-ttu-id="4ed60-120">Clique em Olá **avançado** botão e adicionar mais endereços IP.</span><span class="sxs-lookup"><span data-stu-id="4ed60-120">Click hello **Advanced** button and add additional IP addresses.</span></span> <span data-ttu-id="4ed60-121">Adicione cada Olá secundários endereços IP privados listados na etapa 8 toohello NIC com hello mesma sub-rede especificada para o endereço IP primário de saudação.</span><span class="sxs-lookup"><span data-stu-id="4ed60-121">Add each of hello secondary private IP addresses listed in step 8 toohello NIC with hello same subnet specified for hello primary IP address.</span></span>
        >[!WARNING] 
        ><span data-ttu-id="4ed60-122">Se você não seguir as etapas de saudação acima corretamente, você pode perder conectividade tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="4ed60-122">If you do not follow hello steps above correctly, you may lose connectivity tooyour VM.</span></span> <span data-ttu-id="4ed60-123">Certifique-se de que informações Olá inseridas para a etapa 5 são precisas antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="4ed60-123">Ensure hello information entered for step 5 is accurate before proceeding.</span></span>

    * <span data-ttu-id="4ed60-124">Clique em **Okey** tooclose configurações Olá TCP/IP e, em seguida, **Okey** novamente tooclose Olá as configurações do adaptador.</span><span class="sxs-lookup"><span data-stu-id="4ed60-124">Click **OK** tooclose out hello TCP/IP settings and then **OK** again tooclose hello adapter settings.</span></span> <span data-ttu-id="4ed60-125">A conexão RDP é restabelecida.</span><span class="sxs-lookup"><span data-stu-id="4ed60-125">Your RDP connection is re-established.</span></span>

6. <span data-ttu-id="4ed60-126">Em um prompt de comando, digite *ipconfig /all*.</span><span class="sxs-lookup"><span data-stu-id="4ed60-126">From a command prompt, type *ipconfig /all*.</span></span> <span data-ttu-id="4ed60-127">Todos os endereços IP que você adicionou são mostrados e o DHCP está desativado.</span><span class="sxs-lookup"><span data-stu-id="4ed60-127">All IP addresses you added are shown and DHCP is turned off.</span></span>


### <a name="validation-windows"></a><span data-ttu-id="4ed60-128">Validação (Windows)</span><span class="sxs-lookup"><span data-stu-id="4ed60-128">Validation (Windows)</span></span>

<span data-ttu-id="4ed60-129">tooensure você toohello tooconnect capaz de internet por meio de sua configuração de IP secundária via Olá que IP público associado, depois que ela tiver sido adicionada corretamente usando as etapas acima, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ed60-129">tooensure you are able tooconnect toohello internet from your secondary IP configuration via hello public IP associated it, once you have added it correctly using steps above, use hello following command:</span></span>

```bash
ping -S 10.0.0.5 hotmail.com
```
>[!NOTE]
><span data-ttu-id="4ed60-130">Para configurações de IP secundárias, você pode apenas executar ping toohello Internet se a configuração de saudação tem um endereço IP público associado a ele.</span><span class="sxs-lookup"><span data-stu-id="4ed60-130">For secondary IP configurations, you can only ping toohello Internet if hello configuration has a public IP address associated with it.</span></span> <span data-ttu-id="4ed60-131">Para configurações de IP primárias, um endereço IP público não é necessário tooping toohello da Internet.</span><span class="sxs-lookup"><span data-stu-id="4ed60-131">For primary IP configurations, a public IP address is not required tooping toohello Internet.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="4ed60-132">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="4ed60-132">Linux (Ubuntu)</span></span>

1. <span data-ttu-id="4ed60-133">Abra uma janela de terminal.</span><span class="sxs-lookup"><span data-stu-id="4ed60-133">Open a terminal window.</span></span>
2. <span data-ttu-id="4ed60-134">Verifique se que você for usuário de raiz de saudação.</span><span class="sxs-lookup"><span data-stu-id="4ed60-134">Make sure you are hello root user.</span></span> <span data-ttu-id="4ed60-135">Se você não estiver, digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ed60-135">If you are not, enter hello following command:</span></span>

    ```bash
    sudo -i
    ```

3. <span data-ttu-id="4ed60-136">Atualize o arquivo de configuração de Olá Olá da interface de rede (assumindo 'eth0').</span><span class="sxs-lookup"><span data-stu-id="4ed60-136">Update hello configuration file of hello network interface (assuming ‘eth0’).</span></span>

    * <span data-ttu-id="4ed60-137">Lembre-Olá item de linha existente do dhcp.</span><span class="sxs-lookup"><span data-stu-id="4ed60-137">Keep hello existing line item for dhcp.</span></span> <span data-ttu-id="4ed60-138">endereço IP primário Olá permanece configurado que era anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4ed60-138">hello primary IP address remains configured as it was previously.</span></span>
    * <span data-ttu-id="4ed60-139">Adicione uma configuração para um endereço IP estático adicional com hello comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ed60-139">Add a configuration for an additional static IP address with hello following commands:</span></span>

        ```bash
        cd /etc/network/interfaces.d/
        ls
        ```

    <span data-ttu-id="4ed60-140">Você deve ver um arquivo. cfg.</span><span class="sxs-lookup"><span data-stu-id="4ed60-140">You should see a .cfg file.</span></span>
4. <span data-ttu-id="4ed60-141">Arquivo hello aberto.</span><span class="sxs-lookup"><span data-stu-id="4ed60-141">Open hello file.</span></span> <span data-ttu-id="4ed60-142">Você deve ver Olá linhas final de saudação do arquivo hello seguintes:</span><span class="sxs-lookup"><span data-stu-id="4ed60-142">You should see hello following lines at hello end of hello file:</span></span>

    ```bash
    auto eth0
    iface eth0 inet dhcp
    ```

5. <span data-ttu-id="4ed60-143">Adicione Olá linhas a seguir depois de linhas de saudação que existem neste arquivo:</span><span class="sxs-lookup"><span data-stu-id="4ed60-143">Add hello following lines after hello lines that exist in this file:</span></span>

    ```bash
    iface eth0 inet static
    address <your private IP address here>
    netmask <your subnet mask>
    ```

6. <span data-ttu-id="4ed60-144">Salve arquivo hello usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ed60-144">Save hello file by using hello following command:</span></span>

    ```bash
    :wq
    ```

7. <span data-ttu-id="4ed60-145">Redefinição de interface de rede Olá com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ed60-145">Reset hello network interface with hello following command:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="4ed60-146">Execute ifdown e ifup em Olá mesmo linha se usando uma conexão remota.</span><span class="sxs-lookup"><span data-stu-id="4ed60-146">Run both ifdown and ifup in hello same line if using a remote connection.</span></span>
    >

8. <span data-ttu-id="4ed60-147">Verifique se o endereço IP de saudação é adicionado toohello interface de rede com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ed60-147">Verify hello IP address is added toohello network interface with hello following command:</span></span>

    ```bash
    ip addr list eth0
    ```

    <span data-ttu-id="4ed60-148">Você deve ver Olá IP endereço adicionados como parte da lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="4ed60-148">You should see hello IP address you added as part of hello list.</span></span>

### <a name="linux-redhat-centos-and-others"></a><span data-ttu-id="4ed60-149">Linux (Redhat, CentOS e outros)</span><span class="sxs-lookup"><span data-stu-id="4ed60-149">Linux (Redhat, CentOS, and others)</span></span>

1. <span data-ttu-id="4ed60-150">Abra uma janela de terminal.</span><span class="sxs-lookup"><span data-stu-id="4ed60-150">Open a terminal window.</span></span>
2. <span data-ttu-id="4ed60-151">Verifique se que você for usuário de raiz de saudação.</span><span class="sxs-lookup"><span data-stu-id="4ed60-151">Make sure you are hello root user.</span></span> <span data-ttu-id="4ed60-152">Se você não estiver, digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ed60-152">If you are not, enter hello following command:</span></span>

    ```bash
    sudo -i
    ```

3. <span data-ttu-id="4ed60-153">Digite sua senha e siga as instruções conforme solicitado.</span><span class="sxs-lookup"><span data-stu-id="4ed60-153">Enter your password and follow instructions as prompted.</span></span> <span data-ttu-id="4ed60-154">Quando você for usuário de raiz Olá, navegue até toohello pasta de scripts de rede com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ed60-154">Once you are hello root user, navigate toohello network scripts folder with hello following command:</span></span>

    ```bash
    cd /etc/sysconfig/network-scripts
    ```

4. <span data-ttu-id="4ed60-155">Ifcfg arquivos usando o comando a seguir de saudação relacionados a saudação da lista:</span><span class="sxs-lookup"><span data-stu-id="4ed60-155">List hello related ifcfg files using hello following command:</span></span>

    ```bash
    ls ifcfg-*
    ```

    <span data-ttu-id="4ed60-156">Você deve ver *ifcfg eth0* como um dos arquivos de saudação.</span><span class="sxs-lookup"><span data-stu-id="4ed60-156">You should see *ifcfg-eth0* as one of hello files.</span></span>

5. <span data-ttu-id="4ed60-157">tooadd um endereço IP, crie um arquivo de configuração para ele, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="4ed60-157">tooadd an IP address, create a configuration file for it as shown below.</span></span> <span data-ttu-id="4ed60-158">Observe que um arquivo deve ser criado para cada configuração de IP.</span><span class="sxs-lookup"><span data-stu-id="4ed60-158">Note that one file must be created for each IP configuration.</span></span>

    ```bash
    touch ifcfg-eth0:0
    ```

6. <span data-ttu-id="4ed60-159">Olá abrir *ifcfg-eth0:0* arquivo com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ed60-159">Open hello *ifcfg-eth0:0* file with hello following command:</span></span>

    ```bash
    vi ifcfg-eth0:0
    ```

7. <span data-ttu-id="4ed60-160">Adicionar arquivo de conteúdo toohello *eth0:0* nesse caso, com hello comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="4ed60-160">Add content toohello file, *eth0:0* in this case, with hello following command.</span></span> <span data-ttu-id="4ed60-161">Ser tooupdate informações com base no seu endereço IP.</span><span class="sxs-lookup"><span data-stu-id="4ed60-161">Be sure tooupdate information based on your IP address.</span></span>

    ```bash
    DEVICE=eth0:0
    BOOTPROTO=static
    ONBOOT=yes
    IPADDR=192.168.101.101
    NETMASK=255.255.255.0
    ```

8. <span data-ttu-id="4ed60-162">Salve o arquivo de saudação com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ed60-162">Save hello file with hello following command:</span></span>

    ```bash
    :wq
    ```

9. <span data-ttu-id="4ed60-163">Reinicie os serviços de rede hello e certifique-se de alterações de saudação terão êxito executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ed60-163">Restart hello network services and make sure hello changes are successful by running hello following commands:</span></span>

    ```bash
    /etc/init.d/network restart
    ifconfig
    ```

    <span data-ttu-id="4ed60-164">Você deve ver Olá IP endereço que você adicionou, *eth0:0*, na lista de saudação retornada.</span><span class="sxs-lookup"><span data-stu-id="4ed60-164">You should see hello IP address you added, *eth0:0*, in hello list returned.</span></span>

### <a name="validation-linux"></a><span data-ttu-id="4ed60-165">Validação (Linux)</span><span class="sxs-lookup"><span data-stu-id="4ed60-165">Validation (Linux)</span></span>

<span data-ttu-id="4ed60-166">tooensure são toohello tooconnect capaz de internet por meio de sua configuração de IP secundária por meio de IP público Olá associá-lo, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ed60-166">tooensure you are able tooconnect toohello internet from your secondary IP configuration via hello public IP associated it, use hello following command:</span></span>

```bash
ping -I 10.0.0.5 hotmail.com
```
>[!NOTE]
><span data-ttu-id="4ed60-167">Para configurações de IP secundárias, você pode apenas executar ping toohello Internet se a configuração de saudação tem um endereço IP público associado a ele.</span><span class="sxs-lookup"><span data-stu-id="4ed60-167">For secondary IP configurations, you can only ping toohello Internet if hello configuration has a public IP address associated with it.</span></span> <span data-ttu-id="4ed60-168">Para configurações de IP primárias, um endereço IP público não é necessário tooping toohello da Internet.</span><span class="sxs-lookup"><span data-stu-id="4ed60-168">For primary IP configurations, a public IP address is not required tooping toohello Internet.</span></span>

<span data-ttu-id="4ed60-169">Para VMs do Linux, quando você tentar toovalidate conectividade de saída de uma NIC secundário, talvez seja necessário rotas apropriadas tooadd.</span><span class="sxs-lookup"><span data-stu-id="4ed60-169">For Linux VMs, when trying toovalidate outbound connectivity from a secondary NIC, you may need tooadd appropriate routes.</span></span> <span data-ttu-id="4ed60-170">Há muitos toodo de maneiras isso.</span><span class="sxs-lookup"><span data-stu-id="4ed60-170">There are many ways toodo this.</span></span> <span data-ttu-id="4ed60-171">Veja a documentação apropriada para sua distribuição do Linux.</span><span class="sxs-lookup"><span data-stu-id="4ed60-171">Please see appropriate documentation for your Linux distribution.</span></span> <span data-ttu-id="4ed60-172">a seguir Olá este é um tooaccomplish de método:</span><span class="sxs-lookup"><span data-stu-id="4ed60-172">hello following is one method tooaccomplish this:</span></span>

```bash
echo 150 custom >> /etc/iproute2/rt_tables 

ip rule add from 10.0.0.5 lookup custom
ip route add default via 10.0.0.1 dev eth2 table custom

```
- <span data-ttu-id="4ed60-173">Ser tooreplace-se de que:</span><span class="sxs-lookup"><span data-stu-id="4ed60-173">Be sure tooreplace:</span></span>
    - <span data-ttu-id="4ed60-174">**10.0.0.5** com hello privada endereço que tem um IP público endereço IP associado tooit</span><span class="sxs-lookup"><span data-stu-id="4ed60-174">**10.0.0.5** with hello private IP address that has a public IP address associated tooit</span></span>
    - <span data-ttu-id="4ed60-175">**10.0.0.1** gateway padrão de tooyour</span><span class="sxs-lookup"><span data-stu-id="4ed60-175">**10.0.0.1** tooyour default gateway</span></span>
    - <span data-ttu-id="4ed60-176">**eth2** toohello nome de sua NIC secundário</span><span class="sxs-lookup"><span data-stu-id="4ed60-176">**eth2** toohello name of your secondary NIC</span></span>
