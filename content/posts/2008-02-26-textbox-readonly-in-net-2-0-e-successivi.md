---
title: TextBox ReadOnly in .NET 2.0 e successivi
author: mtammacco
type: post
date: 2008-02-26T09:13:00+00:00
url: /archive/2008/02/26/textbox-readonly-in-net-2-0-e-successivi.aspx
categories:
  - .NET Framework 1.0 / 1.1 / 2.0
  - ASP .NET

---
Il controllo TextBox di una web application dispone della proprietà ReadOnly che, ovviamente, impedisce l&#8217;interazione dell&#8217;utente con il controllo quando è impostata a True.

Ma c&#8217;è un particolare importantissimo da considerare: a partire dalla versione 2.0 del .NET Framework il contenuto di un textbox in modalità &#8220;ReadOnly&#8221; è inviato al server durante un postback della pagina, ma il server ignora questo valore; in altre parole il contenuto del textbox viene perso durante un postback. Questo comportamento mira ad impedire attacchi alla sicurezza, che potrebbero modificare un valore che dovrebbe essere mantenuto inalterato.

La perdita del valore del textbox può essere inaccettabile in certi contesti applicativi e potrebbe essere necessario applicare il comportamento in essere prima del Framework 2.0. Per far ciò è necessario impostare la proprietà ReadOnly come attributo del controllo, in questo modo:

<pre class="brush: csharp; title: ; notranslate" title="">TextBox1.Attributes.Add("readonly","readonly")
</pre>

e non impostando a True la relativa proprietà.

Così facendo il valore del textbox (ovvero la sua proprietà Text) viene inviato al server durante il postback ed è altresì disponibile per l&#8217;elaborazione.

UPDATE: questo aggiornamento è, diciamo così, dovuto: il &#8220;copyright&#8221; di questa scoperta che ha portato via parecchio tempo prima di venirne a capo non è mio ma della mia collega di lavoro [Ines][1]{.}. Io ho solo raccolto il troubleshooting per aiutare altri programmatori come un tempo altri programmatori hanno aiutato me

 [1]: http://ines.zingarelli.biz/