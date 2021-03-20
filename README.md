# Visualizzazione delle informazioni sulle schede NIC wireless e cablate

### Obiettivi

* **Sezione 1: Identificare e utilizzare le schede NIC del PC**
* **Sezione 2: Identificare e utilizzare le icone di rete nella barra delle applicazioni**

### Introduzione e scenario

L'obiettivo di questo laboratorio è determinare la disponibilità e lo stato delle schede di interfaccia di rete (NIC) sul PC in uso. GNU/Linux offre vari modi per visualizzare e utilizzare le schede NIC.

In questa attività di laboratorio si consulteranno le informazioni sulle schede NIC del PC in uso e si modificherà lo stato di tali schede.

### Risorse necessarie

* 1 PC con sistema operativo GNU/Linux e con ambiente grafico KDE Plasma 5
* una NIC cablata
* una NIC wireless
* una connessione wireless

**Nota:** all'inizio di questa attività di laboratorio, la scheda NIC Ethernet cablata del PC è stata collegata via cavo a una porta dello switch integrato in un router wireless. La scheda NIC wireless e cablata sono disabilitate. Se entrambe le schede NIC (cablata e wireless) sono abilitate, al PC verranno assegnati due indirizzi IP distinti e, nel caso si utilizzi NetworkManager la scheda NIC ethernet avrà la precedenza.

## Sezione 1: Identificare e utilizzare le NIC del PC

Nella Sezione 1 verranno identificati i tipi di scheda NIC presenti sul PC in uso. Verranno quindi sperimentati diversi modi per ottenere informazioni sulle schede NIC, nonché per attivarle o disattivarle.

**Nota:** questa attività di laboratorio è stata eseguita utilizzando un PC con sistema operativo Arch Linux e ambiente grafico KDE Plasma 5.21. L'attività può essere completata utilizzando anche altre distribuzioni o altri ambienti grafici. Tuttavia, le opzioni di menu e le schermate visualizzate possono variare.

### Fase 1: Utilizzare il menu connessioni

* Per aprire il menu connessioni, fare clic sul pulsante **Start** > **Impostazioni** > **Impostazioni di sistema.**
* In seguito, nel riquadro a sinistra, fare clic sulla voce **Connessioni.**
* Verrá visualizzata una scheda dove sará possibile **vedere le connessioni configurate** e separate per il tipo di connesione.

![Menu Connessioni.png](Menu%20Connessioni.png?fileId=537002#mimetype=image%2Fpng&hasPreview=true)

**Nota:** in questa finestra potrebbero essere visualizzate anche le schede della rete privata virtuale (VPN) e altri tipi di connessioni di rete.

### Fase 2: Utilizzare la NIC cablata

* Fare clic con il tasto destro sull'interfaccia **Ethernet** e **attivarla** nel caso sia disattivata.

**Nota:** Nel caso in cui la scheda di rete non é collegata al computer non apparirá il pulsante per attivare la connessione ma sará comunque possibile configurare le sue varie impostazioni.

![Attivazione Ethernet.png](Attivazione%20Ethernet.png?fileId=537161#mimetype=image%2Fpng&hasPreview=true)

* Nella sezione destra é possibile impostare la NIC sulla quale usare la connessione. É anche possibile usare un indirizzo MAC fittizio.

![Ethernet Cablata.png](Ethernet%20Cablata.png?fileId=537251#mimetype=image%2Fpng&hasPreview=true)

* Nella sezione **IPv4** é possibile modificare le impostazioni riguardanti l'indirizzamento IP impostando un indirizzo **manuale** o **automatico** (DHCP). In questa schermata é stato impostato un indirizzo IPv4 in modo manuale, aggiungendo anche gli indirizzi dei server DNS.

![Ethernet IPv4.png](Ethernet%20IPv4.png?fileId=537181#mimetype=image%2Fpng&hasPreview=true)

### Fase 3: Utilizzare la NIC wireless

* Fare clic con il tasto destro su **una delle reti wireless** configurate e **attivarla.**

  **Nota:** Nel caso non sia stata ancora configurata nessuna connessione wireless bisogna crearne una con il pulsante "+" situato piú sotto.

![Attivazione Wifi.png](Attivazione%20Wifi.png?fileId=537295#mimetype=image%2Fpng&hasPreview=true)

* La sezione a destra é molto simile a quella giá vista nella connessione ethernet. Qui si protá impostare il **SSID** della connessione wireless e il tipo di **modalitá** che deve usare. Puó essere per esempio usata anche come access point.

![WiFi.png](WiFi.png?fileId=537277#mimetype=image%2Fpng&hasPreview=true)

* Andando nella sezione **Protezione Wi-Fi** sará possibile impostare la **password** e il **tipo di protezione** necessaria per connettersi all'access point. Inoltre é anche possibile **conservare la password in modo criptato** o non criptato.

**Nota:** se la password é stata criptata deve essere inserita ogni volta che ci si vuole connettere a quella connessione.

![WiFi Protezione.png](WiFi%20Protezione.png?fileId=537278#mimetype=image%2Fpng&hasPreview=true)

* La sezione **IPv4** é assolutamente analoga a quella giá vista nella configurazione della NIC cablata per tanto non é stata messa per evitare ripetizioni

### Fase 4: Utilizzare il terminale per ottenere informazioni sulle NIC presenti nel computer

**Nota:** per usufruire del comando ifconfig é necessario installare il pacchetto net-tools tramite il seguente comando:

```bash
$ sudo pacman -S net-tools
```

* Poiché su KDE Plasma 5.21 non é presente un'interfaccia grafica per **visualizzare** le informazioni relative alla scheda di rete, é necessario usare usare il terminale.
* Aprire il terminale premendo **CTRL+Alt+T** oppure cercando **Konsole** nel menú **Start.**
* Digitare all'interno del terminale il seguente comando:

```bash
$ ifconfig -a
```

![comando ifconfig.png](comando%20ifconfig.png?fileId=536871#mimetype=image%2Fpng&hasPreview=true)

* Notiamo che sono presenti 2 schede di rete, in questo caso, **enp0s31f6** indica la **NIC cablata** e **wlp0s20f0u1** la **NIC wireless**. L'interfaccia **lo** invece viene usata per gli indirizzi di **loopback** per riferirsi a servizi aperti sul computer stesso. L'interfaccia **enp0s31f6** ha come indirizzo ip **192.168.1.2**, come subnet mask **255.255.255.0** e il suo **indirizzo MAC é** **70:8b:cd:a6:f7:20**. L'interfaccia **wlp0s20f0u1** non é collegata ancora a nessuna rete ma é possibile comunque vedere il suo indirizzo MAC.
* Per visualizzare gli ip dei server **DNS** in uso basta eseguire questo comando:

```bash
$ grep "^nameserver" /etc/resolv.conf
```

![DNS.png](DNS.png?fileId=536948#mimetype=image%2Fpng&hasPreview=true)

* Invece per visualizzare l**'indirizzo ip del gateway** di default usare questo comando (Quello evidenziato in bianco é il gateway di default della scheda di rete ethernet):

```bash
$ route -n
```

![Default Gateway.png](Default%20Gateway.png?fileId=537428#mimetype=image%2Fpng&hasPreview=true)

## Sezione 2: Identificare e utilizzare le icone di rete nella barra delle applicazioni

Nella Sezione 2 si utilizzeranno le icone di rete nella barra delle applicazioni per determinare e controllare le schede NIC del PC.

### Fase 1: Utilizzare l'icona di Rete

* Fare clic sull'icona **Rete wireless** nella barra delle applicazioni per aprire la finestra a comparsa in cui vengono elencati tutti i **SSID** compresi nell'intervallo della **NIC wireless** e le reti **ethernet configurate**.

![Rete Wireless.png](Rete%20Wireless.png?fileId=537453#mimetype=image%2Fpng&hasPreview=true)

* Adesso se ci scolleghiamo da una connessione wireless cliccando **disconnetti** accanto alla rete selezionata notiamo che l'icona nella barra delle applicazioni **verrá** **sostituita dall'icona Rete cablata**.

![disattivazione wireless.png](disattivazione%20wireless.png?fileId=537452#mimetype=image%2Fpng&hasPreview=true)

![Rete Cablata.png](Rete%20Cablata.png?fileId=537454#mimetype=image%2Fpng&hasPreview=true)

* Se ci **ricolleghiamo** alla rete wireless l'icona dovrebbe di nuovo cambiare in Rete wireless.

### Fase 2: Individuare l'icona Problema di rete

* Andare nel **menu connessioni** (o cliccando sull'icona di rete nella barra delle applicazioni) e **disattivare** sia la **rete cablata** che la **rete wireless**.
* Nella barra delle applicazioni viene visualizzata l'icona di **rete disabilitata** che indica che la connettivitá di rete é stata disabilitata.

![Problema di rete 1.png](Problema%20di%20rete%201.png?fileId=537515#mimetype=image%2Fpng&hasPreview=true)

* Facendo clic su questa icona sará di nuovo possibile **connettersi** ad una rete che avevamo disattivato in precedenza.
* Nel caso siamo connessi ad una rete e **non é possibile connettersi ad Internet** verrá visualizzato un piccolo **triangolo giallo** in basso a destra dell'icona.

![Problema di rete 2.png](Problema%20di%20rete%202.png?fileId=537516#mimetype=image%2Fpng&hasPreview=true)
