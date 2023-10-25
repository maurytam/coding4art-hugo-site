---
title: Impostare la scheda LAN con file batch
author: mtammacco
type: post
date: 2008-02-14T12:49:36+00:00
url: /archive/2008/02/14/impostare-la-scheda-lan-con-file-batch.aspx
categories:
  - Tips and tricks

---
Non sono un sistemista, nè lo saro mai, ma anche occupandosi solo di sviluppo è utile avere sottomano tools e/o tips prettamente sistemistici che possono essere sicuramente utili.

Eccone uno:

**1) netsh interface ip set address &#8220;Connessione alla rete locale (LAN)&#8221; static 10.xxx.xxx.xxx 255.255.255.0 10.xxx.xxx.xxx 0  
2) netsh interface ip set dns &#8220;Connessione alla rete locale (LAN) &#8221; static 10.xxx.xxx.xxx primary  
3) netsh interface ip add dns &#8220;Connessione alla rete locale (LAN)&#8221; 10.xxx.xxx.xxx  
4) netsh interface ip show config &#8220;Connessione alla rete locale (LAN) &#8220;**

I comandi sopraelencati, messi opportunamente in un file .bat, permettono di settare al volo la configurazione di una scheda di rete ben precisa, ovvero quella la cui descrizione è &#8220;Connessione alla rete locale (LAN)&#8221;, nell&#8217;esempio.

Ovviamente basta cambiare la descrizione della scheda per puntarne un&#8217;altra.

La prima riga del batch setta rispettivamente l&#8217;indirizzo ip, la subnetmask ed il default gateway. La seconda riga imposta l&#8217;indirizzo ip del server dns primario, mentre la terza quello del dns secondario. La quarta riga visualizza a console le impostazioni della scheda appena settate.

Questo vale quando vogliamo settare indirizzi ip ben specifici. E se invece vogliamo che la scheda sia impostata con indirizzi ip ottenuti da un server DHCP ?

Ecco i comandi:

**1) netsh interface ip set address &#8220;Connessione alla rete locale (LAN)&#8221; dhcp  
2) netsh interface ip set dns name=&#8221;Connessione alla rete locale (LAN)&#8221; source=dhcp  
3) netsh interface ip show config &#8220;Connessione alla rete locale (LAN)&#8221;**

Per la descrizione della scheda vale quanto già detto. La prima riga imposta la modalità DHCP. La seconda imposta la modalità DHCP per i server DNS, mentre la terza mostra a console la nuova configurazione.