---
title: webNavigation.onReferenceFragmentUpdated
slug: Mozilla/Add-ons/WebExtensions/API/webNavigation/onReferenceFragmentUpdated
tags:
  - API
  - Add-ons
  - Event
  - Extensions
  - Non-standard
  - Reference
  - WebExtensions
  - onReferenceFragmentUpdated
  - webNavigation
browser-compat: webextensions.api.webNavigation.onReferenceFragmentUpdated
---
<div>{{AddonSidebar()}}</div>

<div>Fired if the <a class="external external-icon" href="https://en.wikipedia.org/wiki/Fragment_identifier">fragment identifier</a> for a page is changed. For example, if a page implements a table of contents using fragments, and the user clicks an entry in the table of contents, this event will fire. All future events for this frame will use the updated URL.</div>

<h2 id="Syntax">Syntax</h2>

<pre class="brush: js">browser.webNavigation.onReferenceFragmentUpdated.addListener(
  <var>listener</var>,                   // function
  <var>filter</var>                      // optional object
)
browser.webNavigation.onReferenceFragmentUpdated.removeListener(<var>listener</var>)
browser.webNavigation.onReferenceFragmentUpdated.hasListener(<var>listener</var>)
</pre>

<p>Events have three functions:</p>

<dl>
 <dt><code>addListener(<var>callback</var>)</code></dt>
 <dd>Adds a listener to this event.</dd>
 <dt><code>removeListener(<var>listener</var>)</code></dt>
 <dd>Stop listening to this event. The <code><var>listener</var></code> argument is the listener to remove.</dd>
 <dt><code>hasListener(<var>listener</var>)</code></dt>
 <dd>Check whether <code><var>listener</var></code> is registered for this event. Returns <code>true</code> if it is listening, <code>false</code> otherwise.</dd>
</dl>

<h2 id="addListener_syntax">addListener syntax</h2>

<h3 id="Parameters">Parameters</h3>

<dl>
 <dt><code><var>callback</var></code></dt>
 <dd>
 <p>Function that will be called when this event occurs. The function will be passed the following arguments:</p>

 <dl>
  <dt><code><var>details</var></code></dt>
  <dd><a href="#details"><code>object</code></a>. Details about the navigation event.</dd>
 </dl>
 </dd>
 <dt><code><var>filter</var></code>{{optional_inline}}</dt>
 <dd>
 <p><code>object</code>. An object containing a single property <code>url</code>, which is an <code>Array</code> of {{WebExtAPIRef("events.UrlFilter")}} objects. If you include this parameter, then the event will fire only for transitions to URLs which match at least one <code>UrlFilter</code> in the array. If you omit this parameter, the event will fire for all transitions.</p>
 </dd>
</dl>

<h2 id="Additional_objects">Additional objects</h2>

<h3 id="details">details</h3>

<dl>
 <dt><code>tabId</code></dt>
 <dd><code>integer</code>. The ID of the tab in which the navigation is about to occur.</dd>
 <dt><code>url</code></dt>
 <dd><code>string</code>. The URL to which the given frame will navigate.</dd>
 <dt><code>processId</code></dt>
 <dd><code>integer</code>. The ID of the process in which this tab is being rendered.</dd>
 <dt><code>frameId</code></dt>
 <dd><code>integer</code>. Frame in which the navigation will occur. <code>0</code> indicates that navigation happens in the tab's top-level browsing context, not in a nested {{HTMLElement("iframe")}}. A positive value indicates that navigation happens in a nested iframe. Frame IDs are unique for a given tab and process.</dd>
 <dt><code>timeStamp</code></dt>
 <dd><code>number</code>. The time that the fragment identifier for the page was changed, in <a href="https://en.wikipedia.org/wiki/Unix_time">milliseconds since the epoch</a>.</dd>
 <dt><code>transitionType</code></dt>
 <dd><code>{{WebExtAPIRef("webNavigation.transitionType", "transitionType")}}</code>. The reason for the navigation: for example, <code>"link"</code> if the user clicked a link.</dd>
 <dt><code>transitionQualifiers</code></dt>
 <dd><code>Array</code> of {{WebExtAPIRef("webNavigation.transitionQualifier", "transitionQualifier")}}. Extra information about the navigation: for example, whether there was a server or client redirect.</dd>
</dl>

<h2 id="Browser_compatibility">Browser compatibility</h2>

<p>{{Compat}}</p>

<h2 id="Examples">Examples</h2>

<p>Logs the target URLs and extra transition information for <code>onReferenceFragmentUpdated</code>, if the target URL's hostname contains "example.com" or starts with "developer".</p>

<pre class="brush: js">const filter = {
  url:
  [
    {hostContains: "example.com"},
    {hostPrefix: "developer"}
  ]
}

function logOnReferenceFragmentUpdated(details) {
  console.log(`onReferenceFragmentUpdated: ${details.url}`);
  console.log(`Transition type: ${details.transitionType}`);
  console.log(`Transition qualifiers: ${details.transitionQualifiers}`);
}

browser.webNavigation.onReferenceFragmentUpdated.addListener(logOnReferenceFragmentUpdated, filter);
</pre>

<p>{{WebExtExamples}}</p>


<div class="note"><p><strong>Note:</strong> This API is based on Chromium's <a href="https://developer.chrome.com/extensions/webNavigation#event-onBeforeNavigate"><code>chrome.webNavigation</code></a> API. This documentation is derived from <a href="https://chromium.googlesource.com/chromium/src/+/master/chrome/common/extensions/api/web_navigation.json"><code>web_navigation.json</code></a> in the Chromium code.</p>

<p>Microsoft Edge compatibility data is supplied by Microsoft Corporation and is included here under the Creative Commons Attribution 3.0 United States License.</p>
</div>

<div class="hidden">
<pre>// Copyright 2015 The Chromium Authors. All rights reserved.
//
// Redistribution and use in source and binary forms, with or without
// modification, are permitted provided that the following conditions are
// met:
//
//    * Redistributions of source code must retain the above copyright
// notice, this list of conditions and the following disclaimer.
//    * Redistributions in binary form must reproduce the above
// copyright notice, this list of conditions and the following disclaimer
// in the documentation and/or other materials provided with the
// distribution.
//    * Neither the name of Google Inc. nor the names of its
// contributors may be used to endorse or promote products derived from
// this software without specific prior written permission.
//
// THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
// "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
// LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR
// A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT
// OWNER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
// SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT
// LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE,
// DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY
// THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
// (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
// OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
</pre>
</div>