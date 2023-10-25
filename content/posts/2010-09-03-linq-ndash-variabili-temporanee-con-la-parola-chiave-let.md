---
title: 'LINQ &ndash; Variabili temporanee con la parola chiave Let'
author: mtammacco
type: post
date: 2010-09-03T15:58:00+00:00
url: /archive/2010/09/03/linq-ndash-variabili-temporanee-con-la-parola-chiave-let.aspx
categories:
  - .NET Framework 3.5
  - LINQ

---
L’uso di LINQ apre davvero a scenari molto molto interessanti grazie alla sua potenza e flessibilità.

Oggi ho scoperto che in una query LINQ è possibile costruire una variabile temporanea ed utilizzarla successivamente nella esposizione del risultato della query.

Ecco un esempio:



Nella query LINQ precedente, mediante la parola chiave “**let”** è possibile creare una variabile temporanea (**discount** nell’esempio), farci delle manipolazioni, e ritrovarsi la variabile nella query.

Figo