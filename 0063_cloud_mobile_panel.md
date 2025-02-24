<head>
<title>The 3D Web Coder</title>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
<link rel="stylesheet" type="text/css" href="3dwc.css"/>
<script src="run_prettify.js" type="text/javascript"></script>
<!--
<script src="https://google-code-prettify.googlecode.com/svn/loader/run_prettify.js" type="text/javascript"></script>
-->
</head>

<!---

#adskdevnetwrk
#expressjs
#RestSharp
#Autodesk #IoT #SeeControl #cloud
#python #markdown #asciidoc
#gcal #caldav #googleapi
#milanojs
#3dwebaccel #prague #webgl #3dweb #a360
#au2015 #autocad #inventor #ah8 #cubeathens #developers
#aws #handlebars
#JsFiddle #Reactjs
#autodesku #rtceur
#Reactjs
#MongoDB
#mongolab
#Heroku
#restapi #nodejs #adsk
#javascript

akn_include

Autodesk Uni Cloud and Mobile Expert Panel #au2015 #3dwebcoder #revitapi #ViewAndDataAPI

Here are the notes I took at the Autodesk University 2015 panel discussion SD9731 &ndash; <i>Autodesk Cloud and Mobile API and Technologies: Meet the Experts</i>, led by Cyrille Fauvel, Senior Manager, ADN M&E, Autodesk Inc.
&ndash; Learning Objectives
&ndash; Description
&ndash; Your AU Expert
&ndash; Overview
&ndash; Panellists
&ndash; Questions and Answers...

-->


### Autodesk Uni Cloud and Mobile Expert Panel

Here are the notes I took at the Autodesk University 2015 panel discussion SD9731 &ndash; *Autodesk Cloud and Mobile API and Technologies: Meet the Experts*, led by Cyrille Fauvel, Senior Manager, ADN M&amp;E, Autodesk Inc.

&ndash; Learning Objectives

- Get to know your fellow cloud and mobile programmers and members of the Cloud and Mobile Engineering Team
- Learn how to integrate Autodesk software’s cloud and mobile technology into your own product (desktop or cloud and mobile)
- Identify new opportunities for your business and develop your own Cloud and Mobile Solutions
- Get the answers to those cloud and mobile programming questions that have been bugging you for so long

#### <a name="3"></a>Description

Address your programming questions to a panel of hard-core cloud and mobile experts from our software development teams. If you’re writing Solutions based on these technologies or you’re just about to start and want to know more, this is the perfect forum to both get to know the people who create the APIs and services you work with and meet fellow programmers using these APIs. Come and ask questions, add your expertise to the discussion, or just listen and learn.

#### <a name="4"></a>Your AU Expert

Cyrille Fauvel has been with Autodesk, Inc., since 1993, focused on providing programming support, consulting, training, and evangelism to external developers. Cyrille is currently manager of Autodesk Developer Network (ADN) Sparks (Media & Entertainment), the worldwide team of API gurus providing technical services through the Autodesk Developer Network. The rest of the panel have deep expertise in various areas related to the various Autodesk Cloud & Mobile products and services and developing software to work with them. If these guys can’t answer your question, then it’s probably because you’re in the wrong room. [adndevblog.typepad.com/cloud_and_mobile](http://adndevblog.typepad.com/cloud_and_mobile) &ndash; [cyrille.fauvel@autodesk.com](mailto:cyrille.fauvel@autodesk.com)
￼￼
#### <a name="5"></a>Overview

That’s about it for this handout. It’s very short, but then the value of the class is in the Q&A rather than the prepared remarks. If you’d like to see this class keep coming back, please don’t mark us down on the survey feedback just because we lacked the foresight to answer your question in this document before you’d had the chance to ask it.

#### <a name="6"></a>Panellists

<center>
<img src="img/cloud_mobile_panel.jpg" alt="Cloud and Mobile Expert Panel" width="512">
</center>

- Kean Walmsley &ndash; Autodesk Software Architect, AutoCAD Platform Architect
- Stephen Preston &ndash; Autodesk ADN DevTech Manager
- Cyrille Fauvel &ndash; Autodesk Game Programmer, ADN DevTech
- Yiftach Ringel &ndash; Autodesk Development Manager, A360 mobile apps
- Tom Winter &ndash; Autodesk Software Development Manager, A360 mobile and 360 mobile
- Mikako Harada &ndash; Autodesk AEC Workgroup leader, BIM 360 API expert
- Albert Szilvasy &ndash; Autodesk Software Architect

#### <a name="7"></a>Questions and Answers

[Q] Business side of things: what can we expect in terms of cost of translation? We are hesitating to go further right now because we do not know what will be coming cost-wise.

[A] We have not announced any prices because we really don't know what they cost to use yet. Google does the same thing: first, let the people use it for free, measure usage, and then decide on price. The viewing part will always remain free. You can use the APIs for free for at least the next six months. In other words, right now, the answer is simply: it's free.

[Q] In A360 we want to select everything and archive it. How can I achieve that? We need to archive this to keep track of responsibilities etc. It needs to reside in one location.

[A] We do not have any export functionality. Let's discuss this later one-on-one.

[Q] We are looking at moving our LMV project into the mobile environment. Currently it is just HMTL5. It works responsively. We want to use local data storage etc. so we need to implement an app. Do you have any pointers to good starting points?

[A] We have an app that is using the native viewer. We have a native viewer. You can wrap that. There are lots of tools out there, and you can use any one you like. Going fully native is probably best.

[Q] Where do you think the app will go and where the future is?

[A] Looking out three or five years, do you expect iOS or Android to go away? Survival of the fittest. See how people have already started changing their work habits. Mobile usage is increasing professionally as well. Why should you invest in those? Because that is where your customers are going. Some industries are obviously slower than others. Do you want to be in front of or behind your competitors? Do you want to still have a job five years down the road?

[Q] Viewer and I/O: can I use the API to load an AutoCAD DWG and then modify and save it?

[A] That may be a lot of work. The viewer is just a viewer. If you want to re-implement all that yourself, go ahead. Save the changes in JSON together with the DWG and replay it afterwards. Lots of work. [Q] Revit custom properties?

[A] Yes, they come through. You can also add your own custom data seamlessly if you like.

[Q] Revit rooms?

[A] They are not physical objects, so they are handled differently. We have ideas how to address this, and several developers already have implemented solutions.

[Q] Partnership with data warehouse?

[A] Not aware of them. Good point.

[Q] Accessing multiple LMV documents in a bucket. Can we get two documents from one bucket?

[A] Yes, we have an example in the gallery that does exactly that. You can also import an OBJ file directly. The selection is a bit different, though. We also added new API for merging multiple models into the same scene. They are still under development and should be more mature soon.

[Q] Why do you use an own file format?

[A] This is just the most efficient streaming format. It just streams threejs objects. Look at glTF. That did not exist a year ago. Also, it is geometry only, no metadata. LMV is the current use case for our vision of a bubble.

[Q] A360 collaboration version.

[A] You can go back and see other versions. You can't pick an older version and make it the master version. You can see what was done, but not make that current.

[Q] Proof of concept using design review on the web for markup, classify markup. Which platform should we use? Glue or LMV? Will LMV support markup? Associate metadata with markup? Annotation management?

[A] Visit the Autodesk A360 booth and try it out. LMV does support markup. A whole new workflow is being rolled out. Currently a snapshot, later more interactive. Classification and annotation management is being discussed. Like design in AutoCAD 360. You markup drawings and add comments to them. The LMV viewer is a better way to go than the Glue viewer right now and in future. Glue is very limited, LMV is practically unlimited. Many developers at accelerators came thinking about Glue and switched to LMV.

[Q] Model upload. Compress. Future of DWF.

[A] Several pipelines for LMV translations go via DWF. We are not getting rid of DWF. Look at the bubbles. We do not get rid of things that lots of people are using.

[Q] Fusion, AutoCAD I/O? Can we generate geometry as a web service?

[A] Fusion does not have an API for server side geometry creation, so only AutoCAD I/O can do that right now. Take a look at project Leopard. No plan to make it a service, but it is a zero footprint fusion client. Today it is not a service, but it is creating geometry in the browser and in the backend as well. It might help you understand where things are going.

[Q] Can AutoCAD I/O generate SVG?

[A] It does not export SVG. Today, you would have to write the code yourself. People are asking for a Formit API.

[Q] Can I compare DWF files? Compare models in the LMV viewer? Find the differences?

[A] Yes, I saw such an example. Autodesk consulting did something similar, but only for attribute data. For Revit, the bubble includes a piece that is an entire SQL database. Have you heard of BIM 360 Docs? It includes such a comparison feature. Let's look together after the session. It is supposed to be an API- centric product. For geometry comparison, we sometimes automatically generate bitmaps and compare those to find differences. Also look for BIM compare. You can also grab the threejs mesh objects and compare them.

[Q] A few words on Forge?

[A] The press release was yesterday. This is a rebranding, a banner for a whole platform. All web services will come under this platform. One side is APIs and access, docs, communities. We are planning a developer conference in June in Fort Mason with 1000+ developers, 50+ classes, multiple tracks, design-make-use topics, plus collaborate and visualise. Innovative projects can win part of the $100 million pool.

[Q] We use Civil 3D on laptops in the field. It would be nice to replace that by mobile and tablets. But if we open these files in anything else than full Civil 3D, they get corrupted. Vanilla AutoCAD edit corrupts the file for later Civil 3D use.

[A] This sounds like a bug. Please report this and we'll fix it. We will need a reproducible case. Can you share that? Civil 3D loaded into AutoCAD 360 should work fine for viewing. For editing, you might run into the same issue.

[Q] BIM 360 Docs sounds exciting. Will it have an API?

[A] Yes. It may come a bit later, a couple of weeks or a month or two. This is a cloud-based product and will probably come bit by bit.

[Q] The 2D support in LMV is lagging behind. Entity picking is too hard, for instance, and isolate is missing.

[A] Initially 3D was higher priority, and 2D is coming strong now. Show us what you need, please. It should work in the same way. We have a huge amount of things we want to do.

[Q] How accessible is verbal input for tablets?

[A] Very interesting idea! We have internal hackathons going on. Suggest it to Kean. Cyrille and Kean have already played with speech recognition integrated with LMV using the annyang JavaScript library. Look at Cyrille's sample on GitHub. Stephen tells the story of Jim yelling 'explode' while testing this in an airplane... :-)

We will stop now, but please continue asking questions in the forums and elsewhere.

Many thanks to everybody, participants and panellists, for your enthusiasm and interest!

#### <a name="8"></a>Download

For the sake of completeness, here is the AU session SD9731 &ndash; *Autodesk Cloud and Mobile API and Technologies: Meet the Experts*
[handout](/a/doc/au/2015/doc2/sd9731_cloud_mobile_expert_panel_handout.pdf) and
[slide deck](/a/doc/au/2015/doc2/sd9731_cloud_mobile_expert_panel_slides.pdf).
