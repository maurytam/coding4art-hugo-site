---
title: 'ASP .NET 4.0 #3 Ci&ograve; che non &egrave; cambiato'
author: mtammacco
type: post
date: 2009-11-25T03:42:00+00:00
url: /archive/2009/11/25/asp-net-4-0-3-ciograve-che-non-egrave-cambiato.aspx
categories:
  - ASP .NET
  - ASP .NET 4.0

---
ASP .NET 4.0 è ormai alle porte, con la versione beta è possibile scoprire le novità  rispetto alla versione precedente, e non sono certamente poche, ma a livello di controlli lato server ce ne sono alcuni praticamente immutati rispetto alle precedenti versioni. Mi riferisco ad esempio al controllo **Http File Upload**, rimasto identico nelle varie versioni di ASP .NET che si sono succedute. Questo controllo soffre di qualche problema e non è certo il massimo in ottica web 2.0, ovvero su siti dove è richiesto una elevata user experience.

A meno di non utilizzare un controllo di terze parti probabilmente a pagamento, occorre fare i conti con il look del controllo rimasto identico nel tempo, con l&#8217;assenza di funzionalità  oggi richieste quali ad esempio la barra di progressione dell&#8217;upload in corso, e soprattutto con un fastidioso comportamento &#8220;by design&#8221;, ovvero la perdita del contenuto (il nome completo di percorso del file scelto) ad ogni postback della pagina; quest&#8217;ultima caratteristica è resa necessaria da motivi di sicurezza.

Se la pagina dispone di altri controlli che generano un postback, es. una dropdownlist, l&#8217;unico escamotage è quello di rendere il controllo File Upload l&#8217;ultimo controllo che genera postback in ordine di visualizzazione, in modo da invogliare l&#8217;utente ad interagire per ultimo con esso. In caso contrario, un postback della pagina provocherà  la perdita del suo contenuto, cioè del nome del file scelto, ed ovviamente obbligherà  l&#8217;utente a scegliere nuovamente il file da inviare.