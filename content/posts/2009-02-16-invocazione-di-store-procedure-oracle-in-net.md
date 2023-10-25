---
title: Invocazione di store procedure oracle in .NET
author: mtammacco
type: post
date: 2009-02-16T07:50:39+00:00
url: /archive/2009/02/16/invocazione-di-store-procedure-oracle-in-net.aspx
categories:
  - .NET Framework 3.5
  - Tips and tricks

---
Il **Data Access Application Block**, contenuto all&#8217;interno della **Enterprise Library 4.1** consente di richiamare store procedures passando esclusivamente il valore dei singoli parametri richiesti (mediante l&#8217;utilizzo del metodo **GetStorepProcCommand** dell&#8217;oggetto **DatabaseFactory**), nello stesso ordine con cui questi sono espressi nella firma della procedura. Poichè ADO .NET richiede comunque che ogni informazione in merito ai parametri della store sia obbligatoria (quindi tipo di dato, dimensione, precisione, scala, ecc), il metodo effettua internamente una chiamata al metodo **DeriveParameters** di ADO .NET che, attraverso un round-trip al database server, consente di recuperare tutte le informazioni necessarie sui parametri. Poichè come detto, questa chiamata richiede un round-trip verso il server, il data access application block fornisce anche un meccanismo di caching delle informazioni sui parametri recuperate dal server. 

Oracle e SqServer hanno un meccanismo differente circa il ritorno di un resultset da una store procedure. Oracle infatti richiede, a differenza di Sql Server, l&#8217;utilizzo di un cursore come parametro di output per recuperare il resultset derivante da procedure che lo ritornano, fornendo anche un tipo speciale di dato, cursor appunto, nel suo provider nativo per .NET.

Se si usa il Data Access Application Block per invocare store procedure Oracle che ritornano un resultset attraverso l&#8217;uso di un cursore come parametro di output, non è necessario indicare quest&#8217;ultimo tra i parametri (anche perchè, pur provando ad indicarlo esplicitamente, non si troverebbe il tipo di dati **cursor** disponibile tra i tipi di dati in quanto viene usato l&#8217;enum **System.Data.DbType** che rappresenta genericamente i tpi di dati  per qualsiasi .NET Data Provider).

Basta infatti passare un generico parametro di output avente il valore null come primo parametro della store procedure Oracle e l&#8217;oggetto **OracleDatabase** farà il lavoro per noi. Questo oggetto infatti assume che il primo parametro di una store procedure sia un cursore di output per la restituzione del resultset