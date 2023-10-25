---
title: BizTalk o Workflow Foundation ?
author: mtammacco
type: post
date: 2006-10-13T07:20:00+00:00
url: /archive/2006/10/13/biztalk-o-workflow-foundation.aspx
categories:
  - Thoughts

---
Mi è capitato spesso di assistere a dialoghi tecnici del tipo: &#8216;ma conviene usare Workflow Foundation oppure BizTalk per quel particolare progetto ?&#8217;. A prima vista questi 2 prodotti sembra che si sovrappongano; infatti, semplificando parecchio, ambedue forniscono funzionalità per costruire un processo basato su workflow. Ma è solo una impressione poichè sono profondamente diversi. Un utilissima check-list che aiuta a capire quale strumento si adatta meglio allo specifico progetto è disponibile attraverso questo <a title="" href="http://blogs.msdn.com/irenak/archive/2006/10/11/sysk-216-biztalk-orchestration-or-windows-workflow-foundation.aspx" target="" name="" rel="noopener">post</a> di <a title="" href="http://blogs.msdn.com/irenak/default.aspx" target="" name="" rel="noopener">Irena Kennedy</a>. La checklist inquadra i requisiti che giustificano l&#8217;uso di BizTalk, oppure in loro assenza di Workflow Foundation. 

Molto interessante questo estratto:

&#8230;&#8230;.  <font face="Times New Roman" size="3"><em>Biztalk is product that provides scalable deploying and hosting model, built-in integration with many applications and protocols, a runtime configurable instrumentation framework, central management, monitoring and tracking, message mapping and transformation services, batch processing, publish/subscribe mechanism, engine throttling, scale out support, reliability, fail over, deployment tools, business rules engine, etc.<span style="mso-spacerun: yes">  </span></em></font>

<p class="MsoNormal" style="MARGIN: 0in 0in 0pt">
  <font face="Times New Roman" size="3"><em>WinWF is a set of class libraries, itâ€&#x2122;s a developer framework used to build workflow into custom applications.</em></font>
</p>

<p class="MsoNormal" style="MARGIN: 0in 0in 0pt">
  <?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /?><o:p>
  
  <font face="Times New Roman" size="3"><em> </em></font></o:p>
</p>

<p class="MsoNormal" style="MARGIN: 0in 0in 0pt">
  <font face="Times New Roman" size="3"><em>So, are you creating an intra-application workflow (page flow wizard, control flow, a business logic implementation that has multiple activities, state machine, etc)? <span style="mso-spacerun: yes"> </span>Will your application host the workflows itself?<span style="mso-spacerun: yes">  </span>If yes, WinWF will likely satisfy your needs.</em></font>
</p>

<p class="MsoNormal" style="MARGIN: 0in 0in 0pt">
  <em><font face="Times New Roman" size="3" /></em> 
</p>

<p class="MsoNormal" style="MARGIN: 0in 0in 0pt">
  Mi piacerebbe conoscere il pensiero dell&#8217;amico <a title="" href="http://www.dotnetside.org/blogs/mighell/default.aspx" target="" name="" rel="noopener">Mighell</a> sull&#8217;argomento, che di Workflow Foundation sicuramente ne sa parecchio, visto <a title="" href="http://www.dotnetside.org/blogs/mighell/archive/2006/05/06/EventoWorkflowCommunicationFoundation.aspx" target="" name="" rel="noopener">l&#8217;evento</a> del maggio scorso, l&#8217;ultimo <a title="" href="http://www.dotnetside.org/blogs/mighell/archive/2006/09/28/Webcast-Fatto_2100_.aspx" target="" name="" rel="noopener">webcast</a>, e soprattutto il prossimo workshop <a title="" href="http://www.dotnetside.org/content/netpresentandfuture.aspx" target="" name="" rel="noopener"><strong>&#8220;.NET Present & Future&#8221;</strong></a><strong> </strong>che si terrà a Bari il prossimo 26 Ottobre.
</p>

<font face="Verdana" size="2"></p> 

<p>
  Fonte: <a href="http://blogs.msdn.com/irenak/archive/2006/10/11/sysk-216-biztalk-orchestration-or-windows-workflow-foundation.aspx">http://blogs.msdn.com/irenak/archive/2006/10/11/sysk-216-biztalk-orchestration-or-windows-workflow-foundation.aspx</a>
</p>

<p>
  </font>
</p>