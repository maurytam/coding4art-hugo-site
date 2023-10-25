---
title: Metodo String.IsNullOrWhiteSpace, era ora!
author: mtammacco
type: post
date: 2010-08-02T19:18:08+00:00
url: /archive/2010/08/02/metodo-string-isnullorwhitespace-era-ora.aspx
categories:
  - .NET Framework 4.0

---
Metodo **String.IsNullOrWhiteSpace**

non capisco come si sia dovuto attendere la versione 4 della BLC per introdurre un metodo la cui funzionalità è sicuramente utilizzatissima dagli svluppatori, costringendo questi ultimi a scrivere helper class oppure, ma solo a partire dal Framework 3.5, extention methods ad hoc.

Infatti, prima dell’introduzione di questo metodo, a meno ripeto di non scriversi un metodo ad hoc. erano necessari ben 2 passaggi per determinare se una stringa fosse uguale a null oppure vuota,  includendo nel concetto di vuota anche lo spazio poichè esso è a tutti gli effetti un carattere.

Vale a dire che questo codice:



ritorna **False** perchè nel concetto di **Empty** non è incluso lo spazio.

Si potrebbe sottoporre preventivamente a **Trim** la stringa da valutare, ma sfortunatamente nel caso in cui la stringa sia null l’invocazione del metodo **Trim**() solleva una eccezione “**Object not set to an instance of a object**”.

Come detto, erano necessari 2 passaggi per determinare se una stringa non è null e non è neanche vuota, spazi compresi, ovvero qualcosa del genere:



Fortunatamente con il .Net Framework 4 ce la caviamo con una sola riga di codice: