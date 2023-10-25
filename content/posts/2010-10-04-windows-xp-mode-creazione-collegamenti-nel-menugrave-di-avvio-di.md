---
title: 'Windows XP Mode, creazione collegamenti nel men&ugrave; di avvio di Windows 7'
author: mtammacco
type: post
date: 2010-10-04T13:47:36+00:00
url: /archive/2010/10/04/windows-xp-mode-creazione-collegamenti-nel-menugrave-di-avvio-di.aspx
categories:
  - Tips and tricks

---
Com’è noto, la modalità XP Mode di Windows 7 consente di eseguire una applicazione funzionante sotto Windows XP all’interno di una macchina virtuale XP completamente invisibile all’utente, e con il collegamento all’applicazione visibile nel menù di avvio di Windows 7. Quindi, lanciando l’applicazione dal menù di avvio di Windows 7 verrà automaticamente avviata la macchina virtuale con l’autologon impostato, senza che l’utente si accorga di questo, e dopodicchè l’applicazione in questione sarà eseguita come se apparentemente facesse parte di Windows 7.

Se l’applicazione è dotata di un pacchetto di setup durante la sua installazione nella macchina virtuale XP Mode sarà automaticamente impostato un collegamento nel menù di avvio di Windows 7, onde permetterne l’esecuzione.

Cosa succede l’applicazione non è dotata di un pacchetto di installazione ma è semplicemente copiata nella directory di destinazione ?

Succede che il predetto collegamento, necessario al lancio, non viene creato e quindi l’applicazione pur essendo presente non è di fatto lanciabile (da Windows 7), e quindi è perfettamente inutile!.

Aggiungo inoltre, solo perchè mi è già successo, che alcune applicazioni, tipo una banale applicazione scritta in Visual Basic 6, pur avendo un normale setup, quest’ultimo non crea alcun link nel menù di avvio di Windows 7.

Come ovviare allora al problema ?

Semplice, basta creare un collegamento al nostro eseguibile e copiarlo nella directory **C:\Documents and Settings\All Users\Menù Avvio** della macchina virtuale XP Mode, e come per magia, esso apparirà nel menù di avvio di Windows 7 sotto le la voce Windows Virtual PC\Applicazioni Windows XP Mode.