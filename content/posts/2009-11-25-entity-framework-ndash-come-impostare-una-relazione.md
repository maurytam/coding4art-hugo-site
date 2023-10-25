---
title: 'Entity Framework &ndash; Come impostare una relazione'
author: mtammacco
type: post
date: 2009-11-25T04:45:00+00:00
url: /archive/2009/11/25/entity-framework-ndash-come-impostare-una-relazione.aspx
categories:
  - Entity Framework

---
Con Entity Framework è possibile referenziare tra loro entità  in modo molto semplice.

Supponendo di avere l&#8217;entità  Customer e l&#8217;entità Category, che rappresentano rispettivamente un cliente e la sua categoria di appartenenza, nel data model l&#8217;oggetto Customer conterrà  una proprietà  chiamata Category di tipo Category.

In fase di creazione di un nuovo oggetto Customer Ã¨ necessario associare la Category di appartenenza scelta dall&#8217;utente, molto probabilmente mediante una dropdown list contenente la lista delle categorie (DataTextField), e l&#8217;Id delle stesse (DataValueField).

Istintivamente, verrebbe di fare una cosa di questo tipo:



che però non funziona in quanto solleva una eccezione del tipo &#8220;**An entity object cannot be referenced by multiple instances of IEntityChangeTracker&#8221;**.

Per poter funzionare la reference ha bisogno esclusivamente dell&#8217;Id della Categoria di appartenenza del Cliente, e non dell&#8217;intero oggetto Category, anche perchè per ricrearlo interamente potrebbe essere necessario accedere al database di memorizzazione.

Occorre semplicemente creare un oggetto EntityKey ed associarlo all&#8217;oggetto Customer corrispondente, in questo modo: