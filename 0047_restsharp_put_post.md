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

#mongolab #heroku #mongoosejs #expressjs
#Autodesk #IoT #SeeControl #cloud #adsk
#3dwebcoder #python #adskdevnetwrk #adsk #markdown #asciidoc
#gcal #caldav #cloud #googleapi #restapi
#milanojs
#3dwebaccel #prague #webgl #3dweb #a360
#au2015 #autocad #inventor #ah8 #cubeathens #developers
#aws #revitapi #jquery #handlebars #heroku
#ViewAndDataAPI
#JsFiddle #Reactjs #3dwebcoder #autodesku #rtceur
akn_include

CompHound, #RestSharp, #Mongoose, PUT and POST #3dwebcoder #revitapi #restapi #javascript #mongodb #nodejs

I spent a few exciting and satisfying hours last night cleaning up my C# REST API client to use RestSharp instead of HttpWebRequest and the node.js mongo web server to enable PUT to create as well as update a record
&ndash; Use percent for CSS font-size font sizing
&ndash; The CompHound component tracker
&ndash; GET, PUT and POST stupidity creating versus updating a record
&ndash; Enabling PUT to create as well as update
&ndash; Using RestSharp instead of HttpWebRequest
&ndash; No need to format data as JSON...

-->


### CompHound, RestSharp, Mongoose, PUT and POST

I spent a few exciting and satisfying hours last night cleaning up my C# REST API client to
[use RestSharp instead of HttpWebRequest](#5) and the node.js mongo web server to
[enable PUT to create as well as update](#4) a record.

Here are all my topics for today:

- [Use percent for CSS font-size font sizing](#1)
- [The CompHound component tracker](#2)
- [GET, PUT and POST stupidity creating versus updating a record](#3)
- [Enabling PUT to create as well as update](#4)
- [Using RestSharp instead of HttpWebRequest](#5)
- [No need to format data as JSON](#6)



#### <a name="1"></a>Use Percent for CSS font-size Font Sizing

Being rather perfectionistic, I do a lot of pure HTML editing and really care about the results.

I was therefore quite interested to discover a quite complete and trustworthy analysis and discussion of the topic by Kyle Schaffer,
[CSS font-size: em vs px vs pt vs %](http://kyleschaeffer.com/development/css-font-size-em-vs-px-vs-pt-vs).

Oops. That site seems to have disappeared. Still, I'll leave the link in, in case it reappears one of these days.

Anyway, the executive summary of that discussion is simply, "use percent".

Back to my work at hand:



#### <a name="2"></a>The CompHound Component Tracker

I started work on the CompHound component tracker project for my upcoming conference presentations at 
[RTC Europe](http://www.rtcevents.com/rtc2015eu) in Budapest end of October and
[Autodesk University](http://au.autodesk.com) in Las Vegas in December.

CompHound is a
[cloud-based universal component and asset usage analysis, visualisation and reporting](http://the3dwebcoder.typepad.com/blog/2015/09/comphound-jsfiddle-and-my-first-react-component.html).

So far, it consists of two modules:

- The main JavaScript node.js web server driving a mongo database, now awaiting a user interface and 3D visualisation components.
- A C# Revit add-in populating the database with components to analyse.

To keep these two projects nicely packaged together, I created the
[CompHound GitHub organisation](https://github.com/CompHound) and added them as subprojects to that:

- [CompHoundWeb](https://github.com/CompHound/CompHoundWeb) &ndash;
Cloud-based universal component and asset usage analysis, report and visualisation, a REST API node and mongo web server (server-side JavaScript).
- [CompHoundRvt](https://github.com/CompHound/CompHoundRvt) &ndash;
Revit add-in to populate the CompHound server (desktop C# REST API client).

I grabbed the code from my existing
[fireratingdb](https://github.com/jeremytammik/firerating) web server and
[FireRatingCloud](https://github.com/jeremytammik/FireRatingCloud) Revit add-in
to quickly achieve the following functionality for CompHound as well:

- Set up the node.js web server
- Implement a REST API for it
- Drive the mongo database from it
- Host the mongo database in the cloud on [mongolab](https://mongolab.com)
- Host the web server in the cloud on [heroku](http://heroku.com)
- Retrieve and format the Revit model data
- Send it to the server via REST API

Note that stepping through all of these tasks for the new CompHound project only took an hour or so in all, from scratch.

It took me several weeks to discover how to achieve all this the first time around, for the FireRating project &nbsp; :-)

While doing so, I was once again irritated by the GET, PUT and POST issue I encountered in the firerating project for creating versus updating existing records.

I fixed them in the two new projects and published
[CompHoundWeb 0.0.1](https://github.com/CompHound/CompHoundWeb/releases/tag/0.0.1) and
[CompHoundRvt 2016.0.0.0](https://github.com/CompHound/CompHoundRvt/releases/tag/2016.0.0.0), respectively.

Then I returned to the original FireRating samples to fix these issues there as well.

I'll discuss those improvements in more detail below.

<!--- [Using PUT instead of POST when the Database id is known](http://the3dwebcoder.typepad.com/blog/2015/07/get-and-put-c-net-rest-api-mongodb-storage.html#4) -->



#### <a name="3"></a>GET, PUT and POST Stupidity Creating versus Updating a Record

The previous code to create a new record in the firerating C# add-in looked like this:

<pre class="code">
&nbsp; jsonResponse = Util.QueryOrUpsert(
&nbsp; &nbsp; <span class="maroon">&quot;doors/&quot;</span> + e.UniqueId, <span class="blue">string</span>.Empty, <span class="maroon">&quot;GET&quot;</span> );
&nbsp;
&nbsp; <span class="blue">if</span>( 0 == jsonResponse.Length )
&nbsp; {
&nbsp; &nbsp; jsonResponse = Util.QueryOrUpsert(
&nbsp; &nbsp; &nbsp; <span class="maroon">&quot;doors&quot;</span>, json, <span class="maroon">&quot;POST&quot;</span> );
&nbsp; }
&nbsp; <span class="blue">else</span>
&nbsp; {
&nbsp; &nbsp; jsonResponse = Util.QueryOrUpsert(
&nbsp; &nbsp; &nbsp; <span class="maroon">&quot;doors/&quot;</span> + e.UniqueId, json, <span class="maroon">&quot;PUT&quot;</span> );
&nbsp; }
</pre>

POST is used to creata a new record, and PUT to update an existing one.

I need to use GET first to determine which one of these to call.

I cannot use PUT right away, because it does not create a new record, just silently fails to do anything at all.

I would rather just use one single PUT call to either create or update a record, regardless of whether it already exists or not.

That would save me from making two separate3 REST API calls, with the result of GET deciding whether to use PUT or POST.

Since PUT is
[idempotent](https://en.wikipedia.org/wiki/Representational_state_transfer#Example),
there is no reason &ndash; at least from the REST point of view &ndash; why this should not work.

Please also refer to the succinct and illuminating StackOverflow thread on
[PUT vs POST in REST](http://stackoverflow.com/questions/630453/put-vs-post-in-rest).

I tracked down the reason for this in the underlying REST API implementation issuing the mongo database calls via mongoose.

PUT was driving the Update function, implemented like this:

<pre class="prettyprint">
exports.update = function(req, res) {
  var id = req.params.id;
  console.log('Updating ' + id);
  Door.update({"_id":id}, req.body,
    function (err, numberAffected) {
      if (err) return console.log(err);
      console.log('Updated %s doors', numberAffected.toString());
      return res.sendStatus(202);
  });
};
</pre>

As said, when creating a new record, the target id is not found, the result in null, nothing is added and no error returned.

Easy to fix, once we tracked down the culprit:



#### <a name="4"></a>Enabling PUT to Create as well as Update

I modified the update functionality by implementing update2 in
[controller/doors_v1.js](https://github.com/jeremytammik/firerating/blob/master/controller/doors_v1.js) as follows:

<pre class="prettyprint">
exports.update2 = function(req, res) {
  var id = req.params.id;
  console.log('Updating ' + id);
  Door.findOne({'_id':id},function(err, result) {
    if(result) {
      Door.update({"_id":id}, req.body,
        function (err, numberAffected) {
          if (err) return console.log(err);
          console.log('Updated %s doors', numberAffected.toString());
          return res.sendStatus(202);
      });
    }
    else {
      Door.create(req.body, function (err, door) {
        if (err) return console.log(err);
        return res.send(door);
      });
    }
  });
};
</pre>

That creates a new record if none is found.

I wonder whether mongoose and mongoDB offer that functionality built-in?

The REST API PUT call is routed to the new method in
[routes.js](https://github.com/jeremytammik/firerating/blob/master/routes.js):

<pre class="prettyprint">
module.exports = function(app) {
  var doors = require('./controller/doors_v1');
  app.get('/api/v1/doors', doors.findAll);
  app.get('/api/v1/doors/:id', doors.findById);
  app.post('/api/v1/doors', doors.add);
  //app.put('/api/v1/doors/:id', doors.update); // this one does not allow me to PUT a new instance only update existing
  app.put('/api/v1/doors/:id', doors.update2); // works more like POST + PUT, cf. http://stackoverflow.com/questions/630453/put-vs-post-in-rest
  app.delete('/api/v1/doors/:id', doors.delete);
  app.get('/api/v1/doors/project/:pid', doors.findAllForProject);
}
</pre>


#### <a name="5"></a>Using RestSharp Instead of HttpWebRequest

With that fixed, I also cleaned up my C# REST client a bit.

I switched from the convoluted use of HttpWebRequest to
[RestSharp](http://restsharp.org), also available through
[NuGet](http://www.nuget.org/packages/RestSharp).

Much cleaner.

The previous rather horrible Upsert method looks like this:

<pre class="code">
<span class="gray">///</span><span class="green"> </span><span class="gray">&lt;summary&gt;</span>
<span class="gray">///</span><span class="green"> GET, PUT or POST JSON document data from or to </span>
<span class="gray">///</span><span class="green"> the specified mongoDB collection.</span>
<span class="gray">///</span><span class="green"> </span><span class="gray">&lt;/summary&gt;</span>
<span class="blue">public</span> <span class="blue">static</span> <span class="blue">string</span> QueryOrUpsert(
&nbsp; <span class="blue">string</span> collection_name_id_query,
&nbsp; <span class="blue">string</span> json,
&nbsp; <span class="blue">string</span> method )
{
&nbsp; <span class="blue">string</span> uri = Util.RestApiUri + <span class="maroon">&quot;/&quot;</span>
&nbsp; &nbsp; + collection_name_id_query;
&nbsp;
&nbsp; HttpWebRequest request = HttpWebRequest.Create(
&nbsp; &nbsp; uri ) <span class="blue">as</span> HttpWebRequest;
&nbsp;
&nbsp; request.ContentType = <span class="maroon">&quot;application/json; charset=utf-8&quot;</span>;
&nbsp; request.Accept = <span class="maroon">&quot;application/json, text/javascript, */*&quot;</span>;
&nbsp; request.Timeout = Util.Timeout;
&nbsp; request.Method = method;
&nbsp;
&nbsp; <span class="blue">if</span>( 0 &lt; json.Length )
&nbsp; {
&nbsp; &nbsp; Debug.Assert( !method.Equals( <span class="maroon">&quot;GET&quot;</span> ),
&nbsp; &nbsp; &nbsp; <span class="maroon">&quot;content is not allowed with GET&quot;</span> );
&nbsp;
&nbsp; &nbsp; <span class="blue">using</span>( <span class="teal">StreamWriter</span> writer = <span class="blue">new</span> <span class="teal">StreamWriter</span>(
&nbsp; &nbsp; &nbsp; request.GetRequestStream() ) )
&nbsp; &nbsp; {
&nbsp; &nbsp; &nbsp; writer.Write( json );
&nbsp; &nbsp; }
&nbsp; }
&nbsp; WebResponse response = request.GetResponse();
&nbsp; <span class="teal">Stream</span> stream = response.GetResponseStream();
&nbsp; <span class="blue">string</span> jsonResponse = <span class="blue">string</span>.Empty;
&nbsp;
&nbsp; <span class="blue">using</span>( <span class="teal">StreamReader</span> reader = <span class="blue">new</span> <span class="teal">StreamReader</span>(
&nbsp; &nbsp; stream ) )
&nbsp; {
&nbsp; &nbsp; <span class="blue">while</span>( !reader.EndOfStream )
&nbsp; &nbsp; {
&nbsp; &nbsp; &nbsp; jsonResponse += reader.ReadLine();
&nbsp; &nbsp; }
&nbsp; }
&nbsp; <span class="blue">return</span> jsonResponse;
}
</pre>

That is now replaced by a much simpler Put method using RestSharp:

<pre class="code">
<span class="gray">///</span><span class="green"> </span><span class="gray">&lt;summary&gt;</span>
<span class="gray">///</span><span class="green"> PUT JSON document data into </span>
<span class="gray">///</span><span class="green"> the specified mongoDB collection.</span>
<span class="gray">///</span><span class="green"> </span><span class="gray">&lt;/summary&gt;</span>
<span class="blue">public</span> <span class="blue">static</span> <span class="blue">string</span> Put(
&nbsp; <span class="blue">string</span> collection_name_and_id,
&nbsp; <span class="blue">object</span> data )
{
&nbsp; <span class="blue">var</span> client = <span class="blue">new</span> <span class="teal">RestClient</span>( RestApiBaseUrl );
&nbsp;
&nbsp; <span class="blue">var</span> request = <span class="blue">new</span> <span class="teal">RestRequest</span>( _api_version + <span class="maroon">&quot;/&quot;</span>
&nbsp; &nbsp; + collection_name_and_id, <span class="teal">Method</span>.PUT );
&nbsp;
&nbsp; request.RequestFormat = <span class="teal">DataFormat</span>.Json;
&nbsp;
&nbsp; request.AddBody( data ); <span class="green">// uses JsonSerializer</span>
&nbsp;
&nbsp; <span class="teal">IRestResponse</span> response = client.Execute( request );
&nbsp;
&nbsp; <span class="blue">var</span> content = response.Content; <span class="green">// raw content as string</span>
&nbsp;
&nbsp; <span class="blue">return</span> content;
}
</pre>

Note that the old method took a string specifying the JSON data to send.

The new one takes a native .NET object instead.

This is also much easier to implement:


#### <a name="6"></a>No Need to Format Data as JSON

The JSON string was laboriously assembled by hand:

<pre class="code">
<span class="gray">///</span><span class="green"> </span><span class="gray">&lt;summary&gt;</span>
<span class="gray">///</span><span class="green"> Retrieve the door instance data to store in </span>
<span class="gray">///</span><span class="green"> the external database and return it as a</span>
<span class="gray">///</span><span class="green"> dictionary in a JSON formatted string.</span>
<span class="gray">///</span><span class="green"> </span><span class="gray">&lt;/summary&gt;</span>
<span class="blue">string</span> GetDoorDataJson(
&nbsp; Element door,
&nbsp; <span class="blue">string</span> project_id,
&nbsp; <span class="teal">Guid</span> paramGuid )
{
&nbsp; Document doc = door.Document;
&nbsp;
&nbsp; <span class="blue">string</span> s = <span class="blue">string</span>.Format(
&nbsp; &nbsp; <span class="maroon">&quot;\&quot;_id\&quot;: \&quot;{0}\&quot;,&quot;</span>
&nbsp; &nbsp; + <span class="maroon">&quot;\&quot;project_id\&quot;: \&quot;{1}\&quot;,&quot;</span>
&nbsp; &nbsp; + <span class="maroon">&quot;\&quot;level\&quot;: \&quot;{2}\&quot;,&quot;</span>
&nbsp; &nbsp; + <span class="maroon">&quot;\&quot;tag\&quot;: \&quot;{3}\&quot;,&quot;</span>
&nbsp; &nbsp; + <span class="maroon">&quot;\&quot;firerating\&quot;: {4}&quot;</span>,
&nbsp; &nbsp; door.UniqueId,
&nbsp; &nbsp; project_id,
&nbsp; &nbsp; doc.GetElement( door.LevelId ).Name,
&nbsp; &nbsp; door.get_Parameter( BuiltInParameter.ALL_MODEL_MARK ).AsString(),
&nbsp; &nbsp; door.get_Parameter( paramGuid ).AsDouble() );
&nbsp;
&nbsp; <span class="blue">return</span> <span class="maroon">&quot;{&quot;</span> + s + <span class="maroon">&quot;}&quot;</span>;
}
</pre>

The .NET object is simpler and more efficient to assemble:

<pre class="code">
<span class="gray">///</span><span class="green"> </span><span class="gray">&lt;summary&gt;</span>
<span class="gray">///</span><span class="green"> Retrieve the door instance data to store in </span>
<span class="gray">///</span><span class="green"> the external database and return it as a</span>
<span class="gray">///</span><span class="green"> dictionary-like object.</span>
<span class="gray">///</span><span class="green"> </span><span class="gray">&lt;/summary&gt;</span>
<span class="blue">object</span> GetDoorData(
&nbsp; <span class="teal">Element</span> door,
&nbsp; <span class="blue">string</span> project_id,
&nbsp; <span class="teal">Guid</span> paramGuid )
{
&nbsp; <span class="teal">Document</span> doc = door.Document;
&nbsp;
&nbsp; <span class="blue">string</span> levelName = doc.GetElement(
&nbsp; &nbsp; door.LevelId ).Name;
&nbsp;
&nbsp; <span class="blue">string</span> tagValue = door.get_Parameter(
&nbsp; &nbsp; <span class="teal">BuiltInParameter</span>.ALL_MODEL_MARK ).AsString();
&nbsp;
&nbsp; <span class="blue">double</span> fireratingValue = door.get_Parameter(
&nbsp; &nbsp; paramGuid ).AsDouble();
&nbsp;
&nbsp; <span class="blue">object</span> data = <span class="blue">new</span> {
&nbsp; &nbsp; _id = door.UniqueId,
&nbsp; &nbsp; project_id = project_id,
&nbsp; &nbsp; level = levelName,
&nbsp; &nbsp; tag = tagValue,
&nbsp; &nbsp; firerating = fireratingValue
&nbsp; };
&nbsp;
&nbsp; <span class="blue">return</span> data;
}
</pre>


#### <a name="7"></a>Download

As said, I updated both the existing FireRating and the new CompHound apps to use the new techniques, in their respective repositories:

- [fireratingdb](https://github.com/jeremytammik/firerating) [release 0.0.12](https://github.com/jeremytammik/firerating/releases/tag/0.0.12)
- [FireRatingCloud](https://github.com/jeremytammik/FireRatingCloud) [release 2016.0.0.8](https://github.com/jeremytammik/FireRatingCloud/releases/tag/2016.0.0.8)
- [CompHoundWeb](https://github.com/CompHound/CompHoundWeb) [release 0.0.1](https://github.com/CompHound/CompHoundWeb/releases/tag/0.0.1)
- [CompHoundRvt](https://github.com/CompHound/CompHoundRvt) [release 2016.0.0.0](https://github.com/CompHound/CompHoundRvt/releases/tag/2016.0.0.0)
