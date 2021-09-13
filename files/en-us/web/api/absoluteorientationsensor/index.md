---
title: AbsoluteOrientationSensor
slug: Web/API/AbsoluteOrientationSensor
tags:
  - API
  - AbsoluteOrientationSensor
  - Generic Sensor API
  - Interface
  - Orientation Sensor API
  - OrientationSensor
  - Reference
  - Sensor
  - Sensor APIs
  - Sensors
browser-compat: api.AbsoluteOrientationSensor
---
<div>{{APIRef("Sensor API")}}</div>

<p>The <strong><code>AbsoluteOrientationSensor</code></strong> interface of the <a href="/en-US/docs/Web/API/Sensor_APIs">Sensor APIs</a> describes the device's physical orientation in relation to the Earth's reference coordinate system.</p>

<p>To use this sensor, the user must grant permission to the <code>'accelerometer'</code>, <code>'gyroscope'</code>, and <code>'magnetometer'</code> device sensors through the <a href="/en-US/docs/Web/API/Permissions_API">Permissions API</a>.</p>

<p>If a feature policy blocks use of a feature it is because your code is inconsistent with the policies set on your server. This is not something that would ever be shown to a user. The {{httpheader('Feature-Policy')}} HTTP header article contains implementation instructions.</p>

<h2 id="Constructor">Constructor</h2>

<dl>
 <dt>{{domxref("AbsoluteOrientationSensor.AbsoluteOrientationSensor", "AbsoluteOrientationSensor()")}}</dt>
 <dd>Creates a new <code>AbsoluteOrientationSensor</code> object.</dd>
</dl>

<h2 id="Properties">Properties</h2>

<p><em>No specific properties; inherits methods from its ancestors {{domxref('OrientationSensor')}} and {{domxref('Sensor')}}.</em></p>

<h3 id="Event_handlers">Event handlers</h3>

<p><em>No specific event handlers; inherits methods from its ancestor, {{domxref('Sensor')}}.</em></p>

<h2 id="Methods">Methods</h2>

<p><em>No specific methods; inherits methods from its ancestors {{domxref('OrientationSensor')}} and {{domxref('Sensor')}}.</em></p>

<h2 id="Examples">Examples</h2>

<h3 id="Basic_Example">Basic Example</h3>

<p>The following example, which is loosely based on <a href="https://intel.github.io/generic-sensor-demos/orientation-phone/">Intel's Orientation Phone demo</a>, instantiates an <code>AbsoluteOrientationSensor</code> with a frequency of 60 times a second. On each reading it uses {{domxref('OrientationSensor.quaternion')}} to rotate a visual model of a phone.</p>

<pre class="brush: js">const options = { frequency: 60, referenceFrame: 'device' };
const sensor = new AbsoluteOrientationSensor(options);

sensor.addEventListener('reading', () =&gt; {
  // model is a Three.js object instantiated elsewhere.
  model.quaternion.fromArray(sensor.quaternion).inverse();
});
sensor.addEventListener('error', error =&gt; {
  if (event.error.name == 'NotReadableError') {
    console.log("Sensor is not available.");
  }
});
sensor.start();</pre>

<h3 id="Permissions_Example">Permissions Example</h3>

<p>Using orientation sensors requires requesting permissions for multiple device sensors. Because the {{domxref('Permissions')}} interface uses promises, a good way to request permissions is to use {{jsxref('Promise.all')}}.</p>

<pre class="brush: js">const sensor = new AbsoluteOrientationSensor();
Promise.all([navigator.permissions.query({ name: "accelerometer" }),
             navigator.permissions.query({ name: "magnetometer" }),
             navigator.permissions.query({ name: "gyroscope" })])
       .then(results =&gt; {
         if (results.every(result =&gt; result.state === "granted")) {
           sensor.start();
           ...
         } else {
           console.log("No permissions to use AbsoluteOrientationSensor.");
         }
   });</pre>

<h2 id="Specifications">Specifications</h2>

{{Specifications}}

<h2 id="Browser_compatibility">Browser compatibility</h2>

<p>{{Compat}}</p>