---
title: Creare una "full trust" xbap application
author: mtammacco
type: post
date: 2008-08-04T16:22:00+00:00
url: /archive/2008/08/04/creare-una-quot-full-trust-quot-xbap-application.aspx
categories:
  - Workaround
  - WPF
  - XBAP Application

---
Come chi programma in WPF ben sa, una applicazione WPF browser, meglio nota come XBAP application, gira all&#8217;interno del browser in un ambiente partial trust, oppure in una sandbox di sicurezza, come meglio si preferisce, per evitare appunto che il codice di una tale applicazione possa accedere a informazioni confidenziali oppure effettuare azioni non autorizzate. In particolari scenari, tuttavia, ad esempio in applicazioni Intranet, può nascere l&#8217;esigenza di dotare tali applicazioni di un maggior numero di permessi, oppure addirittura farle girare in ambiente full trust.

Bene, visto che per default una XBAP application viene eseguita in modalità partial trust, quali sono i passaggi necessari per farla funzionare invece in un ambiente full trust ?. Questo è il motivo di questo post. Di seguito elenco i passaggi che ho dovuto effettuare per raggiungere tale obiettivo, anche se alcuni sono un pò contorti e mi fanno dubitare di aver intrapreso la strada migliore, ma alla fine comunque il tutto ha funzionato:

  * Occorre far si che il processo che ospita la XBAP application non venga eseguito con un process token povero di privilegi. Per far questo è necessario intervenire sul Registry (non sono però certo che non esistano metodi più comodi).  Occorre posizionarsi sulla chiave:

> HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\.NETFramework\Windows Presentation Foundation\Hosting

> e creare un valore DWORD denominato RunUnrestricted ed assegnargli il valore 1.

  * Nella scheda Security, accessibile dalle proprietà del progetto, occorre scegliere come zona il valore &#8220;Custom&#8221; al posto di &#8220;Internet&#8221;. Lasciare il valore di default &#8220;This is a partial trust application&#8221; e non spuntare &#8220;This is a full trust application&#8221; come invece la logica vorrebbe. Se si sceglie &#8220;full trust&#8221; senza cambiare la zona (lasciando il valore di default) il meccanismo non funzionerà. Dopo aver fatto questa modifica, riaprendo la scheda Security, si noterà come sia spuntato il valore &#8220;full trust&#8221; e la zona sia impostata a &#8220;Custom&#8221; e non modificabile.

  * Nel file app.manifest dell&#8217;applicazione occorre aggiungere l&#8217;attributo Unrestricted=&#8221;true&#8221;

  * Se si vuol lanciare la propria applicazione mediante un url http, occorre firmare il manifest con un certificato digitale X.509. Quando creiamo la nostra applicazione XBAP Visual Studio genera un file con estensione **&#8220;pfx&#8221;.** Questo file rappresenta un certificato digitale temporaneo da usare a scopo di test. Occorrerà solo registrare tale certificato in Internet Exporer, scegliendo da menù Tools l&#8217;opzione &#8220;**Options**&#8220;, la scheda &#8220;**Content**&#8221; ed il pulsante &#8220;**Certificates**&#8220;. A questo punto click sul pulsante &#8220;**Import**&#8221; e partirà il wizard di importazione del certificato, dove attraverso vari passaggi il certificato di test sarà registrato (occorre scegliere come store  &#8220;**Trusted root Certification Authorities**&#8220;). E&#8217; comunque possibile generare un certificato di test direttamente da Visual Studio, scegliendo la scheda &#8220;**Signing**&#8221; dalle proprietà del progetto e successivamente cliccando il pulsante &#8220;**Create Test Certificate**&#8220;. A questo punto partirà un wizard che permetterà la creazione e la esportazione del certificato in un file &#8220;**pfx**&#8220;, onde consentire la successiva importazione in Internet Explorer.

A questo punto eseguendo l&#8217;applicazione via web essa funzionerà con tutti i permessi assegnati (full trust).