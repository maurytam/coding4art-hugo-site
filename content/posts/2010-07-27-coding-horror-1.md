---
title: 'Coding Horror #1'
author: mtammacco
type: post
date: 2010-07-27T13:59:54+00:00
url: /archive/2010/07/27/coding-horror-1.aspx
categories:
  - Coding horror

---
Se c’è un aspetto che lo sviluppatore medio non tiene nella giusta considerazione quando scrive il codice è il cast tra tipi. Questo lo deduco solo dalla mia esperienza sul campo, ovvio.

Sto parlando del cast ridondante, cioè quel cast semplicemente inutile e che potrebbe essere tranquillamente evitato, basterebbe solo un pò di attenzione in più, e forse un pò di copia ed incolla in meno 

Spesso un cast ridondante non è immediatamente percepibile.

Se si scrive una cosa del genere:



non è immediatamente visibile (ad occhio, intendo) il cast ridondante della riga 4, poichè un oggetto XmlDocument può essere tranquillamente assegnato ad un oggetto XmlNode in quanto quest’ultimo è la classe da cui deriva, e quindi per i principi basilari del polimorfismo o per il principio di sostituzione di [Liskov][1] (al secolo [Barbara Liskov][2], è quindi una donna ) , fate voi, per cui, se B è una classe derivata da A, allora oggetti di tipo A possono essere sostituiti da oggetti di tipo B senza alterare la correttezza dei risultati.

Quindi il codice precedente può essere riscritto senza la ridondanza del cast, cosi:



Ma quando vedo cose del genere:



non riesco proprio a non rabbrividire, anche con il caldo torrido di questi giorni .

Ma come è possibile effettuare un cast del valore zero verso un tipo **Byte** !?!?!, quando, lo sanno pure i bambini, il tipo primitivo **Byte** rappresenta un valore intero senza segno compreso tra 0 e 255 ?.

Scusate lo sfogo…..

 [1]: http://it.wikipedia.org/wiki/Principio_di_sostituzione_di_Liskov
 [2]: http://it.wikipedia.org/wiki/Barbara_Liskov