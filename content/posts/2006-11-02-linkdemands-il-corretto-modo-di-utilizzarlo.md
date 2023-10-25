---
title: LinkDemands, il corretto modo di utilizzarlo
author: mtammacco
type: post
date: 2006-11-02T12:37:00+00:00
url: /archive/2006/11/02/linkdemands-il-corretto-modo-di-utilizzarlo.aspx
categories:
  - .NET Framework 1.0 / 1.1 / 2.0

---
Una cosa che non sapevo, e che desidero condividerla con gli (eventuali) lettori di questo blog: un link demand a livello di metodo sovrascrive sempre un link demand a livello di classe anche se trattasi di permessi differenti.

Esempio, data questa classe:

<pre class="brush: csharp; title: ; notranslate" title="">[FileIOPermission(SecurityAction.LinkDemand, Unrestricted=true)]
public class ClassA
{
    [EnvironmentPermission(SecurityAction.LinkDemand, Read="VAR1" )]
    public void Method1)
    {
    }
}
</pre>

Il link demands a livello di metodo effettua l&#8217;override di quello a livello di classe, anche se si tratta di permessi differenti. In questo caso il link demands EnvironmentPermission sostituisce il link demands FileIOPermission, con la conseguenza che quest&#8217;ultimo permesso non viene richiesto per il metodo in questione.

Morale, occorre esplicitamente re-indicare i link demands a livello di classe su un metodo, se quest&#8217;ultimo è decorato già con un link demands.

Esempio corretto:

<pre class="brush: csharp; title: ; notranslate" title="">[FileIOPermission(SecurityAction.LinkDemand, Unrestricted=true)]
public class ClassA
{
   [FileIOPermission(SecurityAction.LinkDemand, Unrestricted=true)]
   [EnvironmentPermission(SecurityAction.LinkDemand, Read="VAR1" )]
   public void Method1)
   {
   }
}
</pre>