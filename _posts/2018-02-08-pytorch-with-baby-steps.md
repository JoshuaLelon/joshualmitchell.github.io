---
layout: post
title: "PyTorch With Baby Steps: From y = x To Training A Convnet"
date: 2018-02-08
---

<html>
<head><meta charset="utf-8" />
<title>Pytorch With Baby Steps: From y = x To Training A Convolutional Neural Network</title><script src="https://cdnjs.cloudflare.com/ajax/libs/require.js/2.1.10/require.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/2.0.3/jquery.min.js"></script>

<style type="text/css">
    /*!
*
* Twitter Bootstrap
*
*/
/*!
 * Bootstrap v3.3.7 (http://getbootstrap.com)
 * Copyright 2011-2016 Twitter, Inc.
 * Licensed under MIT (https://github.com/twbs/bootstrap/blob/master/LICENSE)
 */
/*! normalize.css v3.0.3 | MIT License | github.com/necolas/normalize.css */
#navdontmoveme {
    margin-left: 115px;
}
html {
  font-family: sans-serif;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
}
body {
  margin: 0;
}
article,
aside,
details,
figcaption,
figure,
footer,
header,
hgroup,
main,
menu,
nav,
section,
summary {
  display: block;
}
audio,
canvas,
progress,
video {
  display: inline-block;
  vertical-align: baseline;
}
audio:not([controls]) {
  display: none;
  height: 0;
}
[hidden],
template {
  display: none;
}
a {
  background-color: transparent;
}
a:active,
a:hover {
  outline: 0;
}
abbr[title] {
  border-bottom: 1px dotted;
}
b,
strong {
  font-weight: bold;
}
dfn {
  font-style: italic;
}
h1 {
  font-size: 2em;
  margin: 0.67em 0;
}
mark {
  background: #ff0;
  color: #000;
}
small {
  font-size: 80%;
}
sub,
sup {
  font-size: 75%;
  line-height: 0;
  position: relative;
  vertical-align: baseline;
}
sup {
  top: -0.5em;
}
sub {
  bottom: -0.25em;
}
img {
  border: 0;
}
svg:not(:root) {
  overflow: hidden;
}
figure {
  margin: 1em 40px;
}
hr {
  box-sizing: content-box;
  height: 0;
}
pre {
  overflow: auto;
}
code,
kbd,
pre,
samp {
  font-family: monospace, monospace;
  font-size: 1em;
}
button,
input,
optgroup,
select,
textarea {
  color: inherit;
  font: inherit;
  margin: 0;
}
button {
  overflow: visible;
}
button,
select {
  text-transform: none;
}
button,
html input[type="button"],
input[type="reset"],
input[type="submit"] {
  -webkit-appearance: button;
  cursor: pointer;
}
button[disabled],
html input[disabled] {
  cursor: default;
}
button::-moz-focus-inner,
input::-moz-focus-inner {
  border: 0;
  padding: 0;
}
input {
  line-height: normal;
}
input[type="checkbox"],
input[type="radio"] {
  box-sizing: border-box;
  padding: 0;
}
input[type="number"]::-webkit-inner-spin-button,
input[type="number"]::-webkit-outer-spin-button {
  height: auto;
}
input[type="search"] {
  -webkit-appearance: textfield;
  box-sizing: content-box;
}
input[type="search"]::-webkit-search-cancel-button,
input[type="search"]::-webkit-search-decoration {
  -webkit-appearance: none;
}
fieldset {
  border: 1px solid #c0c0c0;
  margin: 0 2px;
  padding: 0.35em 0.625em 0.75em;
}
legend {
  border: 0;
  padding: 0;
}
textarea {
  overflow: auto;
}
optgroup {
  font-weight: bold;
}
table {
  border-collapse: collapse;
  border-spacing: 0;
}
td,
th {
  padding: 0;
}
/*! Source: https://github.com/h5bp/html5-boilerplate/blob/master/src/css/main.css */
@media print {
  *,
  *:before,
  *:after {
    background: transparent !important;
    color: #000 !important;
    box-shadow: none !important;
    text-shadow: none !important;
  }
  a,
  a:visited {
    text-decoration: underline;
  }
  a[href]:after {
    content: " (" attr(href) ")";
  }
  abbr[title]:after {
    content: " (" attr(title) ")";
  }
  a[href^="#"]:after,
  a[href^="javascript:"]:after {
    content: "";
  }
  pre,
  blockquote {
    border: 1px solid #999;
    page-break-inside: avoid;
  }
  thead {
    display: table-header-group;
  }
  tr,
  img {
    page-break-inside: avoid;
  }
  img {
    max-width: 100% !important;
  }
  p,
  h2,
  h3 {
    orphans: 3;
    widows: 3;
  }
  h2,
  h3 {
    page-break-after: avoid;
  }
  .navbar {
    display: none;
  }
  .btn > .caret,
  .dropup > .btn > .caret {
    border-top-color: #000 !important;
  }
  .label {
    border: 1px solid #000;
  }
  .table {
    border-collapse: collapse !important;
  }
  .table td,
  .table th {
    background-color: #fff !important;
  }
  .table-bordered th,
  .table-bordered td {
    border: 1px solid #ddd !important;
  }
}
@font-face {
  font-family: 'Glyphicons Halflings';
  src: url('../components/bootstrap/fonts/glyphicons-halflings-regular.eot');
  src: url('../components/bootstrap/fonts/glyphicons-halflings-regular.eot?#iefix') format('embedded-opentype'), url('../components/bootstrap/fonts/glyphicons-halflings-regular.woff2') format('woff2'), url('../components/bootstrap/fonts/glyphicons-halflings-regular.woff') format('woff'), url('../components/bootstrap/fonts/glyphicons-halflings-regular.ttf') format('truetype'), url('../components/bootstrap/fonts/glyphicons-halflings-regular.svg#glyphicons_halflingsregular') format('svg');
}
.glyphicon {
  position: relative;
  top: 1px;
  display: inline-block;
  font-family: 'Glyphicons Halflings';
  font-style: normal;
  font-weight: normal;
  line-height: 1;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
.glyphicon-asterisk:before {
  content: "\002a";
}
.glyphicon-plus:before {
  content: "\002b";
}
.glyphicon-euro:before,
.glyphicon-eur:before {
  content: "\20ac";
}
.glyphicon-minus:before {
  content: "\2212";
}
.glyphicon-cloud:before {
  content: "\2601";
}
.glyphicon-envelope:before {
  content: "\2709";
}
.glyphicon-pencil:before {
  content: "\270f";
}
.glyphicon-glass:before {
  content: "\e001";
}
.glyphicon-music:before {
  content: "\e002";
}
.glyphicon-search:before {
  content: "\e003";
}
.glyphicon-heart:before {
  content: "\e005";
}
.glyphicon-star:before {
  content: "\e006";
}
.glyphicon-star-empty:before {
  content: "\e007";
}
.glyphicon-user:before {
  content: "\e008";
}
.glyphicon-film:before {
  content: "\e009";
}
.glyphicon-th-large:before {
  content: "\e010";
}
.glyphicon-th:before {
  content: "\e011";
}
.glyphicon-th-list:before {
  content: "\e012";
}
.glyphicon-ok:before {
  content: "\e013";
}
.glyphicon-remove:before {
  content: "\e014";
}
.glyphicon-zoom-in:before {
  content: "\e015";
}
.glyphicon-zoom-out:before {
  content: "\e016";
}
.glyphicon-off:before {
  content: "\e017";
}
.glyphicon-signal:before {
  content: "\e018";
}
.glyphicon-cog:before {
  content: "\e019";
}
.glyphicon-trash:before {
  content: "\e020";
}
.glyphicon-home:before {
  content: "\e021";
}
.glyphicon-file:before {
  content: "\e022";
}
.glyphicon-time:before {
  content: "\e023";
}
.glyphicon-road:before {
  content: "\e024";
}
.glyphicon-download-alt:before {
  content: "\e025";
}
.glyphicon-download:before {
  content: "\e026";
}
.glyphicon-upload:before {
  content: "\e027";
}
.glyphicon-inbox:before {
  content: "\e028";
}
.glyphicon-play-circle:before {
  content: "\e029";
}
.glyphicon-repeat:before {
  content: "\e030";
}
.glyphicon-refresh:before {
  content: "\e031";
}
.glyphicon-list-alt:before {
  content: "\e032";
}
.glyphicon-lock:before {
  content: "\e033";
}
.glyphicon-flag:before {
  content: "\e034";
}
.glyphicon-headphones:before {
  content: "\e035";
}
.glyphicon-volume-off:before {
  content: "\e036";
}
.glyphicon-volume-down:before {
  content: "\e037";
}
.glyphicon-volume-up:before {
  content: "\e038";
}
.glyphicon-qrcode:before {
  content: "\e039";
}
.glyphicon-barcode:before {
  content: "\e040";
}
.glyphicon-tag:before {
  content: "\e041";
}
.glyphicon-tags:before {
  content: "\e042";
}
.glyphicon-book:before {
  content: "\e043";
}
.glyphicon-bookmark:before {
  content: "\e044";
}
.glyphicon-print:before {
  content: "\e045";
}
.glyphicon-camera:before {
  content: "\e046";
}
.glyphicon-font:before {
  content: "\e047";
}
.glyphicon-bold:before {
  content: "\e048";
}
.glyphicon-italic:before {
  content: "\e049";
}
.glyphicon-text-height:before {
  content: "\e050";
}
.glyphicon-text-width:before {
  content: "\e051";
}
.glyphicon-align-left:before {
  content: "\e052";
}
.glyphicon-align-center:before {
  content: "\e053";
}
.glyphicon-align-right:before {
  content: "\e054";
}
.glyphicon-align-justify:before {
  content: "\e055";
}
.glyphicon-list:before {
  content: "\e056";
}
.glyphicon-indent-left:before {
  content: "\e057";
}
.glyphicon-indent-right:before {
  content: "\e058";
}
.glyphicon-facetime-video:before {
  content: "\e059";
}
.glyphicon-picture:before {
  content: "\e060";
}
.glyphicon-map-marker:before {
  content: "\e062";
}
.glyphicon-adjust:before {
  content: "\e063";
}
.glyphicon-tint:before {
  content: "\e064";
}
.glyphicon-edit:before {
  content: "\e065";
}
.glyphicon-share:before {
  content: "\e066";
}
.glyphicon-check:before {
  content: "\e067";
}
.glyphicon-move:before {
  content: "\e068";
}
.glyphicon-step-backward:before {
  content: "\e069";
}
.glyphicon-fast-backward:before {
  content: "\e070";
}
.glyphicon-backward:before {
  content: "\e071";
}
.glyphicon-play:before {
  content: "\e072";
}
.glyphicon-pause:before {
  content: "\e073";
}
.glyphicon-stop:before {
  content: "\e074";
}
.glyphicon-forward:before {
  content: "\e075";
}
.glyphicon-fast-forward:before {
  content: "\e076";
}
.glyphicon-step-forward:before {
  content: "\e077";
}
.glyphicon-eject:before {
  content: "\e078";
}
.glyphicon-chevron-left:before {
  content: "\e079";
}
.glyphicon-chevron-right:before {
  content: "\e080";
}
.glyphicon-plus-sign:before {
  content: "\e081";
}
.glyphicon-minus-sign:before {
  content: "\e082";
}
.glyphicon-remove-sign:before {
  content: "\e083";
}
.glyphicon-ok-sign:before {
  content: "\e084";
}
.glyphicon-question-sign:before {
  content: "\e085";
}
.glyphicon-info-sign:before {
  content: "\e086";
}
.glyphicon-screenshot:before {
  content: "\e087";
}
.glyphicon-remove-circle:before {
  content: "\e088";
}
.glyphicon-ok-circle:before {
  content: "\e089";
}
.glyphicon-ban-circle:before {
  content: "\e090";
}
.glyphicon-arrow-left:before {
  content: "\e091";
}
.glyphicon-arrow-right:before {
  content: "\e092";
}
.glyphicon-arrow-up:before {
  content: "\e093";
}
.glyphicon-arrow-down:before {
  content: "\e094";
}
.glyphicon-share-alt:before {
  content: "\e095";
}
.glyphicon-resize-full:before {
  content: "\e096";
}
.glyphicon-resize-small:before {
  content: "\e097";
}
.glyphicon-exclamation-sign:before {
  content: "\e101";
}
.glyphicon-gift:before {
  content: "\e102";
}
.glyphicon-leaf:before {
  content: "\e103";
}
.glyphicon-fire:before {
  content: "\e104";
}
.glyphicon-eye-open:before {
  content: "\e105";
}
.glyphicon-eye-close:before {
  content: "\e106";
}
.glyphicon-warning-sign:before {
  content: "\e107";
}
.glyphicon-plane:before {
  content: "\e108";
}
.glyphicon-calendar:before {
  content: "\e109";
}
.glyphicon-random:before {
  content: "\e110";
}
.glyphicon-comment:before {
  content: "\e111";
}
.glyphicon-magnet:before {
  content: "\e112";
}
.glyphicon-chevron-up:before {
  content: "\e113";
}
.glyphicon-chevron-down:before {
  content: "\e114";
}
.glyphicon-retweet:before {
  content: "\e115";
}
.glyphicon-shopping-cart:before {
  content: "\e116";
}
.glyphicon-folder-close:before {
  content: "\e117";
}
.glyphicon-folder-open:before {
  content: "\e118";
}
.glyphicon-resize-vertical:before {
  content: "\e119";
}
.glyphicon-resize-horizontal:before {
  content: "\e120";
}
.glyphicon-hdd:before {
  content: "\e121";
}
.glyphicon-bullhorn:before {
  content: "\e122";
}
.glyphicon-bell:before {
  content: "\e123";
}
.glyphicon-certificate:before {
  content: "\e124";
}
.glyphicon-thumbs-up:before {
  content: "\e125";
}
.glyphicon-thumbs-down:before {
  content: "\e126";
}
.glyphicon-hand-right:before {
  content: "\e127";
}
.glyphicon-hand-left:before {
  content: "\e128";
}
.glyphicon-hand-up:before {
  content: "\e129";
}
.glyphicon-hand-down:before {
  content: "\e130";
}
.glyphicon-circle-arrow-right:before {
  content: "\e131";
}
.glyphicon-circle-arrow-left:before {
  content: "\e132";
}
.glyphicon-circle-arrow-up:before {
  content: "\e133";
}
.glyphicon-circle-arrow-down:before {
  content: "\e134";
}
.glyphicon-globe:before {
  content: "\e135";
}
.glyphicon-wrench:before {
  content: "\e136";
}
.glyphicon-tasks:before {
  content: "\e137";
}
.glyphicon-filter:before {
  content: "\e138";
}
.glyphicon-briefcase:before {
  content: "\e139";
}
.glyphicon-fullscreen:before {
  content: "\e140";
}
.glyphicon-dashboard:before {
  content: "\e141";
}
.glyphicon-paperclip:before {
  content: "\e142";
}
.glyphicon-heart-empty:before {
  content: "\e143";
}
.glyphicon-link:before {
  content: "\e144";
}
.glyphicon-phone:before {
  content: "\e145";
}
.glyphicon-pushpin:before {
  content: "\e146";
}
.glyphicon-usd:before {
  content: "\e148";
}
.glyphicon-gbp:before {
  content: "\e149";
}
.glyphicon-sort:before {
  content: "\e150";
}
.glyphicon-sort-by-alphabet:before {
  content: "\e151";
}
.glyphicon-sort-by-alphabet-alt:before {
  content: "\e152";
}
.glyphicon-sort-by-order:before {
  content: "\e153";
}
.glyphicon-sort-by-order-alt:before {
  content: "\e154";
}
.glyphicon-sort-by-attributes:before {
  content: "\e155";
}
.glyphicon-sort-by-attributes-alt:before {
  content: "\e156";
}
.glyphicon-unchecked:before {
  content: "\e157";
}
.glyphicon-expand:before {
  content: "\e158";
}
.glyphicon-collapse-down:before {
  content: "\e159";
}
.glyphicon-collapse-up:before {
  content: "\e160";
}
.glyphicon-log-in:before {
  content: "\e161";
}
.glyphicon-flash:before {
  content: "\e162";
}
.glyphicon-log-out:before {
  content: "\e163";
}
.glyphicon-new-window:before {
  content: "\e164";
}
.glyphicon-record:before {
  content: "\e165";
}
.glyphicon-save:before {
  content: "\e166";
}
.glyphicon-open:before {
  content: "\e167";
}
.glyphicon-saved:before {
  content: "\e168";
}
.glyphicon-import:before {
  content: "\e169";
}
.glyphicon-export:before {
  content: "\e170";
}
.glyphicon-send:before {
  content: "\e171";
}
.glyphicon-floppy-disk:before {
  content: "\e172";
}
.glyphicon-floppy-saved:before {
  content: "\e173";
}
.glyphicon-floppy-remove:before {
  content: "\e174";
}
.glyphicon-floppy-save:before {
  content: "\e175";
}
.glyphicon-floppy-open:before {
  content: "\e176";
}
.glyphicon-credit-card:before {
  content: "\e177";
}
.glyphicon-transfer:before {
  content: "\e178";
}
.glyphicon-cutlery:before {
  content: "\e179";
}
.glyphicon-header:before {
  content: "\e180";
}
.glyphicon-compressed:before {
  content: "\e181";
}
.glyphicon-earphone:before {
  content: "\e182";
}
.glyphicon-phone-alt:before {
  content: "\e183";
}
.glyphicon-tower:before {
  content: "\e184";
}
.glyphicon-stats:before {
  content: "\e185";
}
.glyphicon-sd-video:before {
  content: "\e186";
}
.glyphicon-hd-video:before {
  content: "\e187";
}
.glyphicon-subtitles:before {
  content: "\e188";
}
.glyphicon-sound-stereo:before {
  content: "\e189";
}
.glyphicon-sound-dolby:before {
  content: "\e190";
}
.glyphicon-sound-5-1:before {
  content: "\e191";
}
.glyphicon-sound-6-1:before {
  content: "\e192";
}
.glyphicon-sound-7-1:before {
  content: "\e193";
}
.glyphicon-copyright-mark:before {
  content: "\e194";
}
.glyphicon-registration-mark:before {
  content: "\e195";
}
.glyphicon-cloud-download:before {
  content: "\e197";
}
.glyphicon-cloud-upload:before {
  content: "\e198";
}
.glyphicon-tree-conifer:before {
  content: "\e199";
}
.glyphicon-tree-deciduous:before {
  content: "\e200";
}
.glyphicon-cd:before {
  content: "\e201";
}
.glyphicon-save-file:before {
  content: "\e202";
}
.glyphicon-open-file:before {
  content: "\e203";
}
.glyphicon-level-up:before {
  content: "\e204";
}
.glyphicon-copy:before {
  content: "\e205";
}
.glyphicon-paste:before {
  content: "\e206";
}
.glyphicon-alert:before {
  content: "\e209";
}
.glyphicon-equalizer:before {
  content: "\e210";
}
.glyphicon-king:before {
  content: "\e211";
}
.glyphicon-queen:before {
  content: "\e212";
}
.glyphicon-pawn:before {
  content: "\e213";
}
.glyphicon-bishop:before {
  content: "\e214";
}
.glyphicon-knight:before {
  content: "\e215";
}
.glyphicon-baby-formula:before {
  content: "\e216";
}
.glyphicon-tent:before {
  content: "\26fa";
}
.glyphicon-blackboard:before {
  content: "\e218";
}
.glyphicon-bed:before {
  content: "\e219";
}
.glyphicon-apple:before {
  content: "\f8ff";
}
.glyphicon-erase:before {
  content: "\e221";
}
.glyphicon-hourglass:before {
  content: "\231b";
}
.glyphicon-lamp:before {
  content: "\e223";
}
.glyphicon-duplicate:before {
  content: "\e224";
}
.glyphicon-piggy-bank:before {
  content: "\e225";
}
.glyphicon-scissors:before {
  content: "\e226";
}
.glyphicon-bitcoin:before {
  content: "\e227";
}
.glyphicon-btc:before {
  content: "\e227";
}
.glyphicon-xbt:before {
  content: "\e227";
}
.glyphicon-yen:before {
  content: "\00a5";
}
.glyphicon-jpy:before {
  content: "\00a5";
}
.glyphicon-ruble:before {
  content: "\20bd";
}
.glyphicon-rub:before {
  content: "\20bd";
}
.glyphicon-scale:before {
  content: "\e230";
}
.glyphicon-ice-lolly:before {
  content: "\e231";
}
.glyphicon-ice-lolly-tasted:before {
  content: "\e232";
}
.glyphicon-education:before {
  content: "\e233";
}
.glyphicon-option-horizontal:before {
  content: "\e234";
}
.glyphicon-option-vertical:before {
  content: "\e235";
}
.glyphicon-menu-hamburger:before {
  content: "\e236";
}
.glyphicon-modal-window:before {
  content: "\e237";
}
.glyphicon-oil:before {
  content: "\e238";
}
.glyphicon-grain:before {
  content: "\e239";
}
.glyphicon-sunglasses:before {
  content: "\e240";
}
.glyphicon-text-size:before {
  content: "\e241";
}
.glyphicon-text-color:before {
  content: "\e242";
}
.glyphicon-text-background:before {
  content: "\e243";
}
.glyphicon-object-align-top:before {
  content: "\e244";
}
.glyphicon-object-align-bottom:before {
  content: "\e245";
}
.glyphicon-object-align-horizontal:before {
  content: "\e246";
}
.glyphicon-object-align-left:before {
  content: "\e247";
}
.glyphicon-object-align-vertical:before {
  content: "\e248";
}
.glyphicon-object-align-right:before {
  content: "\e249";
}
.glyphicon-triangle-right:before {
  content: "\e250";
}
.glyphicon-triangle-left:before {
  content: "\e251";
}
.glyphicon-triangle-bottom:before {
  content: "\e252";
}
.glyphicon-triangle-top:before {
  content: "\e253";
}
.glyphicon-console:before {
  content: "\e254";
}
.glyphicon-superscript:before {
  content: "\e255";
}
.glyphicon-subscript:before {
  content: "\e256";
}
.glyphicon-menu-left:before {
  content: "\e257";
}
.glyphicon-menu-right:before {
  content: "\e258";
}
.glyphicon-menu-down:before {
  content: "\e259";
}
.glyphicon-menu-up:before {
  content: "\e260";
}
* {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
*:before,
*:after {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
/*
html {
  font-size: 10px;
  -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
}
body {
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-size: 13px;
  line-height: 1.42857143;
  color: #000;
  background-color: #fff;
}*/
input,
button,
select,
textarea {
  font-family: inherit;
  font-size: inherit;
  line-height: inherit;
}
a {
  text-decoration: none;
}
a:hover,
a:focus {
  color: #23527c;
  text-decoration: underline;
}
a:focus {
  outline: 5px auto -webkit-focus-ring-color;
  outline-offset: -2px;
}
figure {
  margin: 0;
}
img {
  vertical-align: middle;
}
.img-responsive,
.thumbnail > img,
.thumbnail a > img,
.carousel-inner > .item > img,
.carousel-inner > .item > a > img {
  display: block;
  max-width: 100%;
  height: auto;
}
.img-rounded {
  border-radius: 3px;
}
.img-thumbnail {
  padding: 4px;
  line-height: 1.42857143;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 2px;
  -webkit-transition: all 0.2s ease-in-out;
  -o-transition: all 0.2s ease-in-out;
  transition: all 0.2s ease-in-out;
  display: inline-block;
  max-width: 100%;
  height: auto;
}
.img-circle {
  border-radius: 50%;
}
hr {
  margin-top: 18px;
  margin-bottom: 18px;
  border: 0;
  border-top: 1px solid #eeeeee;
}
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  margin: -1px;
  padding: 0;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  border: 0;
}
.sr-only-focusable:active,
.sr-only-focusable:focus {
  position: static;
  width: auto;
  height: auto;
  margin: 0;
  overflow: visible;
  clip: auto;
}
[role="button"] {
  cursor: pointer;
}
h1,
h2,
h3,
h4,
h5,
h6,
.h1,
.h2,
.h3,
.h4,
.h5,
.h6 {
  line-height: 1.1;
  color: inherit;
}
h1 small,
h2 small,
h3 small,
h4 small,
h5 small,
h6 small,
.h1 small,
.h2 small,
.h3 small,
.h4 small,
.h5 small,
.h6 small,
h1 .small,
h2 .small,
h3 .small,
h4 .small,
h5 .small,
h6 .small,
.h1 .small,
.h2 .small,
.h3 .small,
.h4 .small,
.h5 .small,
.h6 .small {
  font-weight: normal;
  line-height: 1;
  color: #777777;
}
h1,
.h1,
h2,
.h2,
h3,
.h3 {
  margin-top: 18px;
  margin-bottom: 9px;
}
h1 small,
.h1 small,
h2 small,
.h2 small,
h3 small,
.h3 small,
h1 .small,
.h1 .small,
h2 .small,
.h2 .small,
h3 .small,
.h3 .small {
  font-size: 65%;
}
h4,
.h4,
h5,
.h5,
h6,
.h6 {
  margin-top: 9px;
  margin-bottom: 9px;
}
h4 small,
.h4 small,
h5 small,
.h5 small,
h6 small,
.h6 small,
h4 .small,
.h4 .small,
h5 .small,
.h5 .small,
h6 .small,
.h6 .small {
  font-size: 75%;
}
h1,
.h1 {
  font-size: 33px;
}
h2,
.h2 {
  font-size: 27px;
}
h3,
.h3 {
  font-size: 23px;
}
h4,
.h4 {
  font-size: 17px;
}
h5,
.h5 {
  font-size: 13px;
}
h6,
.h6 {
  font-size: 12px;
}
p {
  margin: 0 0 9px;
}
.lead {
  margin-bottom: 18px;
  font-size: 14px;
  font-weight: 300;
  line-height: 1.4;
}
@media (min-width: 768px) {
  .lead {
    font-size: 19.5px;
  }
}
small,
.small {
  font-size: 92%;
}
mark,
.mark {
  background-color: #fcf8e3;
  padding: .2em;
}
.text-left {
  text-align: left;
}
.text-right {
  text-align: right;
}
.text-center {
  text-align: center;
}
.text-justify {
  text-align: justify;
}
.text-nowrap {
  white-space: nowrap;
}
.text-lowercase {
  text-transform: lowercase;
}
.text-uppercase {
  text-transform: uppercase;
}
.text-capitalize {
  text-transform: capitalize;
}
.text-muted {
  color: #777777;
}
.text-primary {
  color: #337ab7;
}
a.text-primary:hover,
a.text-primary:focus {
  color: #286090;
}
.text-success {
  color: #3c763d;
}
a.text-success:hover,
a.text-success:focus {
  color: #2b542c;
}
.text-info {
  color: #31708f;
}
a.text-info:hover,
a.text-info:focus {
  color: #245269;
}
.text-warning {
  color: #8a6d3b;
}
a.text-warning:hover,
a.text-warning:focus {
  color: #66512c;
}
.text-danger {
  color: #a94442;
}
a.text-danger:hover,
a.text-danger:focus {
  color: #843534;
}
.bg-primary {
  color: #fff;
  background-color: #337ab7;
}
a.bg-primary:hover,
a.bg-primary:focus {
  background-color: #286090;
}
.bg-success {
  background-color: #dff0d8;
}
a.bg-success:hover,
a.bg-success:focus {
  background-color: #c1e2b3;
}
.bg-info {
  background-color: #d9edf7;
}
a.bg-info:hover,
a.bg-info:focus {
  background-color: #afd9ee;
}
.bg-warning {
  background-color: #fcf8e3;
}
a.bg-warning:hover,
a.bg-warning:focus {
  background-color: #f7ecb5;
}
.bg-danger {
  background-color: #f2dede;
}
a.bg-danger:hover,
a.bg-danger:focus {
  background-color: #e4b9b9;
}
.page-header {
  padding-bottom: 8px;
  margin: 36px 0 18px;
  border-bottom: 1px solid #eeeeee;
}
ul,
ol {
  margin-top: 0;
  margin-bottom: 9px;
}
ul ul,
ol ul,
ul ol,
ol ol {
  margin-bottom: 0;
}
.list-unstyled {
  padding-left: 0;
  list-style: none;
}
.list-inline {
  padding-left: 0;
  list-style: none;
  margin-left: -5px;
}
.list-inline > li {
  display: inline-block;
  padding-left: 5px;
  padding-right: 5px;
}
dl {
  margin-top: 0;
  margin-bottom: 18px;
}
dt,
dd {
  line-height: 1.42857143;
}
dt {
  font-weight: bold;
}
dd {
  margin-left: 0;
}
@media (min-width: 541px) {
  .dl-horizontal dt {
    float: left;
    width: 160px;
    clear: left;
    text-align: right;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
  }
  .dl-horizontal dd {
    margin-left: 180px;
  }
}
abbr[title],
abbr[data-original-title] {
  cursor: help;
  border-bottom: 1px dotted #777777;
}
.initialism {
  font-size: 90%;
  text-transform: uppercase;
}
blockquote {
  padding: 9px 18px;
  margin: 0 0 18px;
  font-size: inherit;
  border-left: 5px solid #eeeeee;
}
blockquote p:last-child,
blockquote ul:last-child,
blockquote ol:last-child {
  margin-bottom: 0;
}
blockquote footer,
blockquote small,
blockquote .small {
  display: block;
  font-size: 80%;
  line-height: 1.42857143;
  color: #777777;
}
blockquote footer:before,
blockquote small:before,
blockquote .small:before {
  content: '\2014 \00A0';
}
.blockquote-reverse,
blockquote.pull-right {
  padding-right: 15px;
  padding-left: 0;
  border-right: 5px solid #eeeeee;
  border-left: 0;
  text-align: right;
}
.blockquote-reverse footer:before,
blockquote.pull-right footer:before,
.blockquote-reverse small:before,
blockquote.pull-right small:before,
.blockquote-reverse .small:before,
blockquote.pull-right .small:before {
  content: '';
}
.blockquote-reverse footer:after,
blockquote.pull-right footer:after,
.blockquote-reverse small:after,
blockquote.pull-right small:after,
.blockquote-reverse .small:after,
blockquote.pull-right .small:after {
  content: '\00A0 \2014';
}
address {
  margin-bottom: 18px;
  font-style: normal;
  line-height: 1.42857143;
}
code,
kbd,
pre,
samp {
  font-family: monospace;
}
code {
  padding: 2px 4px;
  font-size: 90%;
  color: #c7254e;
  background-color: #f9f2f4;
  border-radius: 2px;
}
kbd {
  padding: 2px 4px;
  font-size: 90%;
  color: #888;
  background-color: transparent;
  border-radius: 1px;
  box-shadow: inset 0 -1px 0 rgba(0, 0, 0, 0.25);
}
kbd kbd {
  padding: 0;
  font-size: 100%;
  font-weight: bold;
  box-shadow: none;
}
pre {
  display: block;
  padding: 8.5px;
  margin: 0 0 9px;
  font-size: 12px;
  line-height: 1.42857143;
  word-break: break-all;
  word-wrap: break-word;
  color: #333333;
  background-color: #f5f5f5;
  border: 1px solid #ccc;
  border-radius: 2px;
}
pre code {
  padding: 0;
  font-size: inherit;
  color: inherit;
  white-space: pre-wrap;
  background-color: transparent;
  border-radius: 0;
}
.pre-scrollable {
  max-height: 340px;
  overflow-y: scroll;
}
.container {
  margin-right: auto;
  margin-left: auto;
  padding-left: 0px;
  padding-right: 0px;
}
@media (min-width: 768px) {
  .container {
    width: 768px;
  }
}
@media (min-width: 992px) {
  .container {
    width: 940px;
  }
}
@media (min-width: 1200px) {
  .container {
    width: 1140px;
  }
}
.container-fluid {
  margin-right: auto;
  margin-left: auto;
  padding-left: 0px;
  padding-right: 0px;
}
.row {
  margin-left: 0px;
  margin-right: 0px;
}
.col-xs-1, .col-sm-1, .col-md-1, .col-lg-1, .col-xs-2, .col-sm-2, .col-md-2, .col-lg-2, .col-xs-3, .col-sm-3, .col-md-3, .col-lg-3, .col-xs-4, .col-sm-4, .col-md-4, .col-lg-4, .col-xs-5, .col-sm-5, .col-md-5, .col-lg-5, .col-xs-6, .col-sm-6, .col-md-6, .col-lg-6, .col-xs-7, .col-sm-7, .col-md-7, .col-lg-7, .col-xs-8, .col-sm-8, .col-md-8, .col-lg-8, .col-xs-9, .col-sm-9, .col-md-9, .col-lg-9, .col-xs-10, .col-sm-10, .col-md-10, .col-lg-10, .col-xs-11, .col-sm-11, .col-md-11, .col-lg-11, .col-xs-12, .col-sm-12, .col-md-12, .col-lg-12 {
  position: relative;
  min-height: 1px;
  padding-left: 0px;
  padding-right: 0px;
}
.col-xs-1, .col-xs-2, .col-xs-3, .col-xs-4, .col-xs-5, .col-xs-6, .col-xs-7, .col-xs-8, .col-xs-9, .col-xs-10, .col-xs-11, .col-xs-12 {
  float: left;
}
.col-xs-12 {
  width: 100%;
}
.col-xs-11 {
  width: 91.66666667%;
}
.col-xs-10 {
  width: 83.33333333%;
}
.col-xs-9 {
  width: 75%;
}
.col-xs-8 {
  width: 66.66666667%;
}
.col-xs-7 {
  width: 58.33333333%;
}
.col-xs-6 {
  width: 50%;
}
.col-xs-5 {
  width: 41.66666667%;
}
.col-xs-4 {
  width: 33.33333333%;
}
.col-xs-3 {
  width: 25%;
}
.col-xs-2 {
  width: 16.66666667%;
}
.col-xs-1 {
  width: 8.33333333%;
}
.col-xs-pull-12 {
  right: 100%;
}
.col-xs-pull-11 {
  right: 91.66666667%;
}
.col-xs-pull-10 {
  right: 83.33333333%;
}
.col-xs-pull-9 {
  right: 75%;
}
.col-xs-pull-8 {
  right: 66.66666667%;
}
.col-xs-pull-7 {
  right: 58.33333333%;
}
.col-xs-pull-6 {
  right: 50%;
}
.col-xs-pull-5 {
  right: 41.66666667%;
}
.col-xs-pull-4 {
  right: 33.33333333%;
}
.col-xs-pull-3 {
  right: 25%;
}
.col-xs-pull-2 {
  right: 16.66666667%;
}
.col-xs-pull-1 {
  right: 8.33333333%;
}
.col-xs-pull-0 {
  right: auto;
}
.col-xs-push-12 {
  left: 100%;
}
.col-xs-push-11 {
  left: 91.66666667%;
}
.col-xs-push-10 {
  left: 83.33333333%;
}
.col-xs-push-9 {
  left: 75%;
}
.col-xs-push-8 {
  left: 66.66666667%;
}
.col-xs-push-7 {
  left: 58.33333333%;
}
.col-xs-push-6 {
  left: 50%;
}
.col-xs-push-5 {
  left: 41.66666667%;
}
.col-xs-push-4 {
  left: 33.33333333%;
}
.col-xs-push-3 {
  left: 25%;
}
.col-xs-push-2 {
  left: 16.66666667%;
}
.col-xs-push-1 {
  left: 8.33333333%;
}
.col-xs-push-0 {
  left: auto;
}
.col-xs-offset-12 {
  margin-left: 100%;
}
.col-xs-offset-11 {
  margin-left: 91.66666667%;
}
.col-xs-offset-10 {
  margin-left: 83.33333333%;
}
.col-xs-offset-9 {
  margin-left: 75%;
}
.col-xs-offset-8 {
  margin-left: 66.66666667%;
}
.col-xs-offset-7 {
  margin-left: 58.33333333%;
}
.col-xs-offset-6 {
  margin-left: 50%;
}
.col-xs-offset-5 {
  margin-left: 41.66666667%;
}
.col-xs-offset-4 {
  margin-left: 33.33333333%;
}
.col-xs-offset-3 {
  margin-left: 25%;
}
.col-xs-offset-2 {
  margin-left: 16.66666667%;
}
.col-xs-offset-1 {
  margin-left: 8.33333333%;
}
.col-xs-offset-0 {
  margin-left: 0%;
}
@media (min-width: 768px) {
  .col-sm-1, .col-sm-2, .col-sm-3, .col-sm-4, .col-sm-5, .col-sm-6, .col-sm-7, .col-sm-8, .col-sm-9, .col-sm-10, .col-sm-11, .col-sm-12 {
    float: left;
  }
  .col-sm-12 {
    width: 100%;
  }
  .col-sm-11 {
    width: 91.66666667%;
  }
  .col-sm-10 {
    width: 83.33333333%;
  }
  .col-sm-9 {
    width: 75%;
  }
  .col-sm-8 {
    width: 66.66666667%;
  }
  .col-sm-7 {
    width: 58.33333333%;
  }
  .col-sm-6 {
    width: 50%;
  }
  .col-sm-5 {
    width: 41.66666667%;
  }
  .col-sm-4 {
    width: 33.33333333%;
  }
  .col-sm-3 {
    width: 25%;
  }
  .col-sm-2 {
    width: 16.66666667%;
  }
  .col-sm-1 {
    width: 8.33333333%;
  }
  .col-sm-pull-12 {
    right: 100%;
  }
  .col-sm-pull-11 {
    right: 91.66666667%;
  }
  .col-sm-pull-10 {
    right: 83.33333333%;
  }
  .col-sm-pull-9 {
    right: 75%;
  }
  .col-sm-pull-8 {
    right: 66.66666667%;
  }
  .col-sm-pull-7 {
    right: 58.33333333%;
  }
  .col-sm-pull-6 {
    right: 50%;
  }
  .col-sm-pull-5 {
    right: 41.66666667%;
  }
  .col-sm-pull-4 {
    right: 33.33333333%;
  }
  .col-sm-pull-3 {
    right: 25%;
  }
  .col-sm-pull-2 {
    right: 16.66666667%;
  }
  .col-sm-pull-1 {
    right: 8.33333333%;
  }
  .col-sm-pull-0 {
    right: auto;
  }
  .col-sm-push-12 {
    left: 100%;
  }
  .col-sm-push-11 {
    left: 91.66666667%;
  }
  .col-sm-push-10 {
    left: 83.33333333%;
  }
  .col-sm-push-9 {
    left: 75%;
  }
  .col-sm-push-8 {
    left: 66.66666667%;
  }
  .col-sm-push-7 {
    left: 58.33333333%;
  }
  .col-sm-push-6 {
    left: 50%;
  }
  .col-sm-push-5 {
    left: 41.66666667%;
  }
  .col-sm-push-4 {
    left: 33.33333333%;
  }
  .col-sm-push-3 {
    left: 25%;
  }
  .col-sm-push-2 {
    left: 16.66666667%;
  }
  .col-sm-push-1 {
    left: 8.33333333%;
  }
  .col-sm-push-0 {
    left: auto;
  }
  .col-sm-offset-12 {
    margin-left: 100%;
  }
  .col-sm-offset-11 {
    margin-left: 91.66666667%;
  }
  .col-sm-offset-10 {
    margin-left: 83.33333333%;
  }
  .col-sm-offset-9 {
    margin-left: 75%;
  }
  .col-sm-offset-8 {
    margin-left: 66.66666667%;
  }
  .col-sm-offset-7 {
    margin-left: 58.33333333%;
  }
  .col-sm-offset-6 {
    margin-left: 50%;
  }
  .col-sm-offset-5 {
    margin-left: 41.66666667%;
  }
  .col-sm-offset-4 {
    margin-left: 33.33333333%;
  }
  .col-sm-offset-3 {
    margin-left: 25%;
  }
  .col-sm-offset-2 {
    margin-left: 16.66666667%;
  }
  .col-sm-offset-1 {
    margin-left: 8.33333333%;
  }
  .col-sm-offset-0 {
    margin-left: 0%;
  }
}
@media (min-width: 992px) {
  .col-md-1, .col-md-2, .col-md-3, .col-md-4, .col-md-5, .col-md-6, .col-md-7, .col-md-8, .col-md-9, .col-md-10, .col-md-11, .col-md-12 {
    float: left;
  }
  .col-md-12 {
    width: 100%;
  }
  .col-md-11 {
    width: 91.66666667%;
  }
  .col-md-10 {
    width: 83.33333333%;
  }
  .col-md-9 {
    width: 75%;
  }
  .col-md-8 {
    width: 66.66666667%;
  }
  .col-md-7 {
    width: 58.33333333%;
  }
  .col-md-6 {
    width: 50%;
  }
  .col-md-5 {
    width: 41.66666667%;
  }
  .col-md-4 {
    width: 33.33333333%;
  }
  .col-md-3 {
    width: 25%;
  }
  .col-md-2 {
    width: 16.66666667%;
  }
  .col-md-1 {
    width: 8.33333333%;
  }
  .col-md-pull-12 {
    right: 100%;
  }
  .col-md-pull-11 {
    right: 91.66666667%;
  }
  .col-md-pull-10 {
    right: 83.33333333%;
  }
  .col-md-pull-9 {
    right: 75%;
  }
  .col-md-pull-8 {
    right: 66.66666667%;
  }
  .col-md-pull-7 {
    right: 58.33333333%;
  }
  .col-md-pull-6 {
    right: 50%;
  }
  .col-md-pull-5 {
    right: 41.66666667%;
  }
  .col-md-pull-4 {
    right: 33.33333333%;
  }
  .col-md-pull-3 {
    right: 25%;
  }
  .col-md-pull-2 {
    right: 16.66666667%;
  }
  .col-md-pull-1 {
    right: 8.33333333%;
  }
  .col-md-pull-0 {
    right: auto;
  }
  .col-md-push-12 {
    left: 100%;
  }
  .col-md-push-11 {
    left: 91.66666667%;
  }
  .col-md-push-10 {
    left: 83.33333333%;
  }
  .col-md-push-9 {
    left: 75%;
  }
  .col-md-push-8 {
    left: 66.66666667%;
  }
  .col-md-push-7 {
    left: 58.33333333%;
  }
  .col-md-push-6 {
    left: 50%;
  }
  .col-md-push-5 {
    left: 41.66666667%;
  }
  .col-md-push-4 {
    left: 33.33333333%;
  }
  .col-md-push-3 {
    left: 25%;
  }
  .col-md-push-2 {
    left: 16.66666667%;
  }
  .col-md-push-1 {
    left: 8.33333333%;
  }
  .col-md-push-0 {
    left: auto;
  }
  .col-md-offset-12 {
    margin-left: 100%;
  }
  .col-md-offset-11 {
    margin-left: 91.66666667%;
  }
  .col-md-offset-10 {
    margin-left: 83.33333333%;
  }
  .col-md-offset-9 {
    margin-left: 75%;
  }
  .col-md-offset-8 {
    margin-left: 66.66666667%;
  }
  .col-md-offset-7 {
    margin-left: 58.33333333%;
  }
  .col-md-offset-6 {
    margin-left: 50%;
  }
  .col-md-offset-5 {
    margin-left: 41.66666667%;
  }
  .col-md-offset-4 {
    margin-left: 33.33333333%;
  }
  .col-md-offset-3 {
    margin-left: 25%;
  }
  .col-md-offset-2 {
    margin-left: 16.66666667%;
  }
  .col-md-offset-1 {
    margin-left: 8.33333333%;
  }
  .col-md-offset-0 {
    margin-left: 0%;
  }
}
@media (min-width: 1200px) {
  .col-lg-1, .col-lg-2, .col-lg-3, .col-lg-4, .col-lg-5, .col-lg-6, .col-lg-7, .col-lg-8, .col-lg-9, .col-lg-10, .col-lg-11, .col-lg-12 {
    float: left;
  }
  .col-lg-12 {
    width: 100%;
  }
  .col-lg-11 {
    width: 91.66666667%;
  }
  .col-lg-10 {
    width: 83.33333333%;
  }
  .col-lg-9 {
    width: 75%;
  }
  .col-lg-8 {
    width: 66.66666667%;
  }
  .col-lg-7 {
    width: 58.33333333%;
  }
  .col-lg-6 {
    width: 50%;
  }
  .col-lg-5 {
    width: 41.66666667%;
  }
  .col-lg-4 {
    width: 33.33333333%;
  }
  .col-lg-3 {
    width: 25%;
  }
  .col-lg-2 {
    width: 16.66666667%;
  }
  .col-lg-1 {
    width: 8.33333333%;
  }
  .col-lg-pull-12 {
    right: 100%;
  }
  .col-lg-pull-11 {
    right: 91.66666667%;
  }
  .col-lg-pull-10 {
    right: 83.33333333%;
  }
  .col-lg-pull-9 {
    right: 75%;
  }
  .col-lg-pull-8 {
    right: 66.66666667%;
  }
  .col-lg-pull-7 {
    right: 58.33333333%;
  }
  .col-lg-pull-6 {
    right: 50%;
  }
  .col-lg-pull-5 {
    right: 41.66666667%;
  }
  .col-lg-pull-4 {
    right: 33.33333333%;
  }
  .col-lg-pull-3 {
    right: 25%;
  }
  .col-lg-pull-2 {
    right: 16.66666667%;
  }
  .col-lg-pull-1 {
    right: 8.33333333%;
  }
  .col-lg-pull-0 {
    right: auto;
  }
  .col-lg-push-12 {
    left: 100%;
  }
  .col-lg-push-11 {
    left: 91.66666667%;
  }
  .col-lg-push-10 {
    left: 83.33333333%;
  }
  .col-lg-push-9 {
    left: 75%;
  }
  .col-lg-push-8 {
    left: 66.66666667%;
  }
  .col-lg-push-7 {
    left: 58.33333333%;
  }
  .col-lg-push-6 {
    left: 50%;
  }
  .col-lg-push-5 {
    left: 41.66666667%;
  }
  .col-lg-push-4 {
    left: 33.33333333%;
  }
  .col-lg-push-3 {
    left: 25%;
  }
  .col-lg-push-2 {
    left: 16.66666667%;
  }
  .col-lg-push-1 {
    left: 8.33333333%;
  }
  .col-lg-push-0 {
    left: auto;
  }
  .col-lg-offset-12 {
    margin-left: 100%;
  }
  .col-lg-offset-11 {
    margin-left: 91.66666667%;
  }
  .col-lg-offset-10 {
    margin-left: 83.33333333%;
  }
  .col-lg-offset-9 {
    margin-left: 75%;
  }
  .col-lg-offset-8 {
    margin-left: 66.66666667%;
  }
  .col-lg-offset-7 {
    margin-left: 58.33333333%;
  }
  .col-lg-offset-6 {
    margin-left: 50%;
  }
  .col-lg-offset-5 {
    margin-left: 41.66666667%;
  }
  .col-lg-offset-4 {
    margin-left: 33.33333333%;
  }
  .col-lg-offset-3 {
    margin-left: 25%;
  }
  .col-lg-offset-2 {
    margin-left: 16.66666667%;
  }
  .col-lg-offset-1 {
    margin-left: 8.33333333%;
  }
  .col-lg-offset-0 {
    margin-left: 0%;
  }
}
table {
  background-color: transparent;
}
caption {
  padding-top: 8px;
  padding-bottom: 8px;
  color: #777777;
  text-align: left;
}
th {
  text-align: left;
}
.table {
  width: 100%;
  max-width: 100%;
  margin-bottom: 18px;
}
.table > thead > tr > th,
.table > tbody > tr > th,
.table > tfoot > tr > th,
.table > thead > tr > td,
.table > tbody > tr > td,
.table > tfoot > tr > td {
  padding: 8px;
  line-height: 1.42857143;
  vertical-align: top;
  border-top: 1px solid #ddd;
}
.table > thead > tr > th {
  vertical-align: bottom;
  border-bottom: 2px solid #ddd;
}
.table > caption + thead > tr:first-child > th,
.table > colgroup + thead > tr:first-child > th,
.table > thead:first-child > tr:first-child > th,
.table > caption + thead > tr:first-child > td,
.table > colgroup + thead > tr:first-child > td,
.table > thead:first-child > tr:first-child > td {
  border-top: 0;
}
.table > tbody + tbody {
  border-top: 2px solid #ddd;
}
.table .table {
  background-color: #fff;
}
.table-condensed > thead > tr > th,
.table-condensed > tbody > tr > th,
.table-condensed > tfoot > tr > th,
.table-condensed > thead > tr > td,
.table-condensed > tbody > tr > td,
.table-condensed > tfoot > tr > td {
  padding: 5px;
}
.table-bordered {
  border: 1px solid #ddd;
}
.table-bordered > thead > tr > th,
.table-bordered > tbody > tr > th,
.table-bordered > tfoot > tr > th,
.table-bordered > thead > tr > td,
.table-bordered > tbody > tr > td,
.table-bordered > tfoot > tr > td {
  border: 1px solid #ddd;
}
.table-bordered > thead > tr > th,
.table-bordered > thead > tr > td {
  border-bottom-width: 2px;
}
.table-striped > tbody > tr:nth-of-type(odd) {
  background-color: #f9f9f9;
}
.table-hover > tbody > tr:hover {
  background-color: #f5f5f5;
}
table col[class*="col-"] {
  position: static;
  float: none;
  display: table-column;
}
table td[class*="col-"],
table th[class*="col-"] {
  position: static;
  float: none;
  display: table-cell;
}
.table > thead > tr > td.active,
.table > tbody > tr > td.active,
.table > tfoot > tr > td.active,
.table > thead > tr > th.active,
.table > tbody > tr > th.active,
.table > tfoot > tr > th.active,
.table > thead > tr.active > td,
.table > tbody > tr.active > td,
.table > tfoot > tr.active > td,
.table > thead > tr.active > th,
.table > tbody > tr.active > th,
.table > tfoot > tr.active > th {
  background-color: #f5f5f5;
}
.table-hover > tbody > tr > td.active:hover,
.table-hover > tbody > tr > th.active:hover,
.table-hover > tbody > tr.active:hover > td,
.table-hover > tbody > tr:hover > .active,
.table-hover > tbody > tr.active:hover > th {
  background-color: #e8e8e8;
}
.table > thead > tr > td.success,
.table > tbody > tr > td.success,
.table > tfoot > tr > td.success,
.table > thead > tr > th.success,
.table > tbody > tr > th.success,
.table > tfoot > tr > th.success,
.table > thead > tr.success > td,
.table > tbody > tr.success > td,
.table > tfoot > tr.success > td,
.table > thead > tr.success > th,
.table > tbody > tr.success > th,
.table > tfoot > tr.success > th {
  background-color: #dff0d8;
}
.table-hover > tbody > tr > td.success:hover,
.table-hover > tbody > tr > th.success:hover,
.table-hover > tbody > tr.success:hover > td,
.table-hover > tbody > tr:hover > .success,
.table-hover > tbody > tr.success:hover > th {
  background-color: #d0e9c6;
}
.table > thead > tr > td.info,
.table > tbody > tr > td.info,
.table > tfoot > tr > td.info,
.table > thead > tr > th.info,
.table > tbody > tr > th.info,
.table > tfoot > tr > th.info,
.table > thead > tr.info > td,
.table > tbody > tr.info > td,
.table > tfoot > tr.info > td,
.table > thead > tr.info > th,
.table > tbody > tr.info > th,
.table > tfoot > tr.info > th {
  background-color: #d9edf7;
}
.table-hover > tbody > tr > td.info:hover,
.table-hover > tbody > tr > th.info:hover,
.table-hover > tbody > tr.info:hover > td,
.table-hover > tbody > tr:hover > .info,
.table-hover > tbody > tr.info:hover > th {
  background-color: #c4e3f3;
}
.table > thead > tr > td.warning,
.table > tbody > tr > td.warning,
.table > tfoot > tr > td.warning,
.table > thead > tr > th.warning,
.table > tbody > tr > th.warning,
.table > tfoot > tr > th.warning,
.table > thead > tr.warning > td,
.table > tbody > tr.warning > td,
.table > tfoot > tr.warning > td,
.table > thead > tr.warning > th,
.table > tbody > tr.warning > th,
.table > tfoot > tr.warning > th {
  background-color: #fcf8e3;
}
.table-hover > tbody > tr > td.warning:hover,
.table-hover > tbody > tr > th.warning:hover,
.table-hover > tbody > tr.warning:hover > td,
.table-hover > tbody > tr:hover > .warning,
.table-hover > tbody > tr.warning:hover > th {
  background-color: #faf2cc;
}
.table > thead > tr > td.danger,
.table > tbody > tr > td.danger,
.table > tfoot > tr > td.danger,
.table > thead > tr > th.danger,
.table > tbody > tr > th.danger,
.table > tfoot > tr > th.danger,
.table > thead > tr.danger > td,
.table > tbody > tr.danger > td,
.table > tfoot > tr.danger > td,
.table > thead > tr.danger > th,
.table > tbody > tr.danger > th,
.table > tfoot > tr.danger > th {
  background-color: #f2dede;
}
.table-hover > tbody > tr > td.danger:hover,
.table-hover > tbody > tr > th.danger:hover,
.table-hover > tbody > tr.danger:hover > td,
.table-hover > tbody > tr:hover > .danger,
.table-hover > tbody > tr.danger:hover > th {
  background-color: #ebcccc;
}
.table-responsive {
  overflow-x: auto;
  min-height: 0.01%;
}
@media screen and (max-width: 767px) {
  .table-responsive {
    width: 100%;
    margin-bottom: 13.5px;
    overflow-y: hidden;
    -ms-overflow-style: -ms-autohiding-scrollbar;
    border: 1px solid #ddd;
  }
  .table-responsive > .table {
    margin-bottom: 0;
  }
  .table-responsive > .table > thead > tr > th,
  .table-responsive > .table > tbody > tr > th,
  .table-responsive > .table > tfoot > tr > th,
  .table-responsive > .table > thead > tr > td,
  .table-responsive > .table > tbody > tr > td,
  .table-responsive > .table > tfoot > tr > td {
    white-space: nowrap;
  }
  .table-responsive > .table-bordered {
    border: 0;
  }
  .table-responsive > .table-bordered > thead > tr > th:first-child,
  .table-responsive > .table-bordered > tbody > tr > th:first-child,
  .table-responsive > .table-bordered > tfoot > tr > th:first-child,
  .table-responsive > .table-bordered > thead > tr > td:first-child,
  .table-responsive > .table-bordered > tbody > tr > td:first-child,
  .table-responsive > .table-bordered > tfoot > tr > td:first-child {
    border-left: 0;
  }
  .table-responsive > .table-bordered > thead > tr > th:last-child,
  .table-responsive > .table-bordered > tbody > tr > th:last-child,
  .table-responsive > .table-bordered > tfoot > tr > th:last-child,
  .table-responsive > .table-bordered > thead > tr > td:last-child,
  .table-responsive > .table-bordered > tbody > tr > td:last-child,
  .table-responsive > .table-bordered > tfoot > tr > td:last-child {
    border-right: 0;
  }
  .table-responsive > .table-bordered > tbody > tr:last-child > th,
  .table-responsive > .table-bordered > tfoot > tr:last-child > th,
  .table-responsive > .table-bordered > tbody > tr:last-child > td,
  .table-responsive > .table-bordered > tfoot > tr:last-child > td {
    border-bottom: 0;
  }
}
fieldset {
  padding: 0;
  margin: 0;
  border: 0;
  min-width: 0;
}
legend {
  display: block;
  width: 100%;
  padding: 0;
  margin-bottom: 18px;
  font-size: 19.5px;
  line-height: inherit;
  color: #333333;
  border: 0;
  border-bottom: 1px solid #e5e5e5;
}
label {
  display: inline-block;
  max-width: 100%;
  margin-bottom: 5px;
  font-weight: bold;
}
input[type="search"] {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
input[type="radio"],
input[type="checkbox"] {
  margin: 4px 0 0;
  margin-top: 1px \9;
  line-height: normal;
}
input[type="file"] {
  display: block;
}
input[type="range"] {
  display: block;
  width: 100%;
}
select[multiple],
select[size] {
  height: auto;
}
input[type="file"]:focus,
input[type="radio"]:focus,
input[type="checkbox"]:focus {
  outline: 5px auto -webkit-focus-ring-color;
  outline-offset: -2px;
}
output {
  display: block;
  padding-top: 7px;
  font-size: 13px;
  line-height: 1.42857143;
  color: #555555;
}
.form-control {
  display: block;
  width: 100%;
  height: 32px;
  padding: 6px 12px;
  font-size: 13px;
  line-height: 1.42857143;
  color: #555555;
  background-color: #fff;
  background-image: none;
  border: 1px solid #ccc;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  -webkit-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  -o-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
}
.form-control:focus {
  border-color: #66afe9;
  outline: 0;
  -webkit-box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
  box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
}
.form-control::-moz-placeholder {
  color: #999;
  opacity: 1;
}
.form-control:-ms-input-placeholder {
  color: #999;
}
.form-control::-webkit-input-placeholder {
  color: #999;
}
.form-control::-ms-expand {
  border: 0;
  background-color: transparent;
}
.form-control[disabled],
.form-control[readonly],
fieldset[disabled] .form-control {
  background-color: #eeeeee;
  opacity: 1;
}
.form-control[disabled],
fieldset[disabled] .form-control {
  cursor: not-allowed;
}
textarea.form-control {
  height: auto;
}
input[type="search"] {
  -webkit-appearance: none;
}
@media screen and (-webkit-min-device-pixel-ratio: 0) {
  input[type="date"].form-control,
  input[type="time"].form-control,
  input[type="datetime-local"].form-control,
  input[type="month"].form-control {
    line-height: 32px;
  }
  input[type="date"].input-sm,
  input[type="time"].input-sm,
  input[type="datetime-local"].input-sm,
  input[type="month"].input-sm,
  .input-group-sm input[type="date"],
  .input-group-sm input[type="time"],
  .input-group-sm input[type="datetime-local"],
  .input-group-sm input[type="month"] {
    line-height: 30px;
  }
  input[type="date"].input-lg,
  input[type="time"].input-lg,
  input[type="datetime-local"].input-lg,
  input[type="month"].input-lg,
  .input-group-lg input[type="date"],
  .input-group-lg input[type="time"],
  .input-group-lg input[type="datetime-local"],
  .input-group-lg input[type="month"] {
    line-height: 45px;
  }
}
.form-group {
  margin-bottom: 15px;
}
.radio,
.checkbox {
  position: relative;
  display: block;
  margin-top: 10px;
  margin-bottom: 10px;
}
.radio label,
.checkbox label {
  min-height: 18px;
  padding-left: 20px;
  margin-bottom: 0;
  font-weight: normal;
  cursor: pointer;
}
.radio input[type="radio"],
.radio-inline input[type="radio"],
.checkbox input[type="checkbox"],
.checkbox-inline input[type="checkbox"] {
  position: absolute;
  margin-left: -20px;
  margin-top: 4px \9;
}
.radio + .radio,
.checkbox + .checkbox {
  margin-top: -5px;
}
.radio-inline,
.checkbox-inline {
  position: relative;
  display: inline-block;
  padding-left: 20px;
  margin-bottom: 0;
  vertical-align: middle;
  font-weight: normal;
  cursor: pointer;
}
.radio-inline + .radio-inline,
.checkbox-inline + .checkbox-inline {
  margin-top: 0;
  margin-left: 10px;
}
input[type="radio"][disabled],
input[type="checkbox"][disabled],
input[type="radio"].disabled,
input[type="checkbox"].disabled,
fieldset[disabled] input[type="radio"],
fieldset[disabled] input[type="checkbox"] {
  cursor: not-allowed;
}
.radio-inline.disabled,
.checkbox-inline.disabled,
fieldset[disabled] .radio-inline,
fieldset[disabled] .checkbox-inline {
  cursor: not-allowed;
}
.radio.disabled label,
.checkbox.disabled label,
fieldset[disabled] .radio label,
fieldset[disabled] .checkbox label {
  cursor: not-allowed;
}
.form-control-static {
  padding-top: 7px;
  padding-bottom: 7px;
  margin-bottom: 0;
  min-height: 31px;
}
.form-control-static.input-lg,
.form-control-static.input-sm {
  padding-left: 0;
  padding-right: 0;
}
.input-sm {
  height: 30px;
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
select.input-sm {
  height: 30px;
  line-height: 30px;
}
textarea.input-sm,
select[multiple].input-sm {
  height: auto;
}
.form-group-sm .form-control {
  height: 30px;
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
.form-group-sm select.form-control {
  height: 30px;
  line-height: 30px;
}
.form-group-sm textarea.form-control,
.form-group-sm select[multiple].form-control {
  height: auto;
}
.form-group-sm .form-control-static {
  height: 30px;
  min-height: 30px;
  padding: 6px 10px;
  font-size: 12px;
  line-height: 1.5;
}
.input-lg {
  height: 45px;
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
  border-radius: 3px;
}
select.input-lg {
  height: 45px;
  line-height: 45px;
}
textarea.input-lg,
select[multiple].input-lg {
  height: auto;
}
.form-group-lg .form-control {
  height: 45px;
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
  border-radius: 3px;
}
.form-group-lg select.form-control {
  height: 45px;
  line-height: 45px;
}
.form-group-lg textarea.form-control,
.form-group-lg select[multiple].form-control {
  height: auto;
}
.form-group-lg .form-control-static {
  height: 45px;
  min-height: 35px;
  padding: 11px 16px;
  font-size: 17px;
  line-height: 1.3333333;
}
.has-feedback {
  position: relative;
}
.has-feedback .form-control {
  padding-right: 40px;
}
.form-control-feedback {
  position: absolute;
  top: 0;
  right: 0;
  z-index: 2;
  display: block;
  width: 32px;
  height: 32px;
  line-height: 32px;
  text-align: center;
  pointer-events: none;
}
.input-lg + .form-control-feedback,
.input-group-lg + .form-control-feedback,
.form-group-lg .form-control + .form-control-feedback {
  width: 45px;
  height: 45px;
  line-height: 45px;
}
.input-sm + .form-control-feedback,
.input-group-sm + .form-control-feedback,
.form-group-sm .form-control + .form-control-feedback {
  width: 30px;
  height: 30px;
  line-height: 30px;
}
.has-success .help-block,
.has-success .control-label,
.has-success .radio,
.has-success .checkbox,
.has-success .radio-inline,
.has-success .checkbox-inline,
.has-success.radio label,
.has-success.checkbox label,
.has-success.radio-inline label,
.has-success.checkbox-inline label {
  color: #3c763d;
}
.has-success .form-control {
  border-color: #3c763d;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
}
.has-success .form-control:focus {
  border-color: #2b542c;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #67b168;
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #67b168;
}
.has-success .input-group-addon {
  color: #3c763d;
  border-color: #3c763d;
  background-color: #dff0d8;
}
.has-success .form-control-feedback {
  color: #3c763d;
}
.has-warning .help-block,
.has-warning .control-label,
.has-warning .radio,
.has-warning .checkbox,
.has-warning .radio-inline,
.has-warning .checkbox-inline,
.has-warning.radio label,
.has-warning.checkbox label,
.has-warning.radio-inline label,
.has-warning.checkbox-inline label {
  color: #8a6d3b;
}
.has-warning .form-control {
  border-color: #8a6d3b;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
}
.has-warning .form-control:focus {
  border-color: #66512c;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #c0a16b;
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #c0a16b;
}
.has-warning .input-group-addon {
  color: #8a6d3b;
  border-color: #8a6d3b;
  background-color: #fcf8e3;
}
.has-warning .form-control-feedback {
  color: #8a6d3b;
}
.has-error .help-block,
.has-error .control-label,
.has-error .radio,
.has-error .checkbox,
.has-error .radio-inline,
.has-error .checkbox-inline,
.has-error.radio label,
.has-error.checkbox label,
.has-error.radio-inline label,
.has-error.checkbox-inline label {
  color: #a94442;
}
.has-error .form-control {
  border-color: #a94442;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
}
.has-error .form-control:focus {
  border-color: #843534;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #ce8483;
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #ce8483;
}
.has-error .input-group-addon {
  color: #a94442;
  border-color: #a94442;
  background-color: #f2dede;
}
.has-error .form-control-feedback {
  color: #a94442;
}
.has-feedback label ~ .form-control-feedback {
  top: 23px;
}
.has-feedback label.sr-only ~ .form-control-feedback {
  top: 0;
}
.help-block {
  display: block;
  margin-top: 5px;
  margin-bottom: 10px;
  color: #404040;
}
@media (min-width: 768px) {
  .form-inline .form-group {
    display: inline-block;
    margin-bottom: 0;
    vertical-align: middle;
  }
  .form-inline .form-control {
    display: inline-block;
    width: auto;
    vertical-align: middle;
  }
  .form-inline .form-control-static {
    display: inline-block;
  }
  .form-inline .input-group {
    display: inline-table;
    vertical-align: middle;
  }
  .form-inline .input-group .input-group-addon,
  .form-inline .input-group .input-group-btn,
  .form-inline .input-group .form-control {
    width: auto;
  }
  .form-inline .input-group > .form-control {
    width: 100%;
  }
  .form-inline .control-label {
    margin-bottom: 0;
    vertical-align: middle;
  }
  .form-inline .radio,
  .form-inline .checkbox {
    display: inline-block;
    margin-top: 0;
    margin-bottom: 0;
    vertical-align: middle;
  }
  .form-inline .radio label,
  .form-inline .checkbox label {
    padding-left: 0;
  }
  .form-inline .radio input[type="radio"],
  .form-inline .checkbox input[type="checkbox"] {
    position: relative;
    margin-left: 0;
  }
  .form-inline .has-feedback .form-control-feedback {
    top: 0;
  }
}
.form-horizontal .radio,
.form-horizontal .checkbox,
.form-horizontal .radio-inline,
.form-horizontal .checkbox-inline {
  margin-top: 0;
  margin-bottom: 0;
  padding-top: 7px;
}
.form-horizontal .radio,
.form-horizontal .checkbox {
  min-height: 25px;
}
.form-horizontal .form-group {
  margin-left: 0px;
  margin-right: 0px;
}
@media (min-width: 768px) {
  .form-horizontal .control-label {
    text-align: right;
    margin-bottom: 0;
    padding-top: 7px;
  }
}
.form-horizontal .has-feedback .form-control-feedback {
  right: 0px;
}
@media (min-width: 768px) {
  .form-horizontal .form-group-lg .control-label {
    padding-top: 11px;
    font-size: 17px;
  }
}
@media (min-width: 768px) {
  .form-horizontal .form-group-sm .control-label {
    padding-top: 6px;
    font-size: 12px;
  }
}
.btn {
  display: inline-block;
  margin-bottom: 0;
  font-weight: normal;
  text-align: center;
  vertical-align: middle;
  touch-action: manipulation;
  cursor: pointer;
  background-image: none;
  border: 1px solid transparent;
  white-space: nowrap;
  padding: 6px 12px;
  font-size: 13px;
  line-height: 1.42857143;
  border-radius: 2px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.btn:focus,
.btn:active:focus,
.btn.active:focus,
.btn.focus,
.btn:active.focus,
.btn.active.focus {
  outline: 5px auto -webkit-focus-ring-color;
  outline-offset: -2px;
}
.btn:hover,
.btn:focus,
.btn.focus {
  color: #333;
  text-decoration: none;
}
.btn:active,
.btn.active {
  outline: 0;
  background-image: none;
  -webkit-box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
  box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
}
.btn.disabled,
.btn[disabled],
fieldset[disabled] .btn {
  cursor: not-allowed;
  opacity: 0.65;
  filter: alpha(opacity=65);
  -webkit-box-shadow: none;
  box-shadow: none;
}
a.btn.disabled,
fieldset[disabled] a.btn {
  pointer-events: none;
}
.btn-default {
  color: #333;
  background-color: #fff;
  border-color: #ccc;
}
.btn-default:focus,
.btn-default.focus {
  color: #333;
  background-color: #e6e6e6;
  border-color: #8c8c8c;
}
.btn-default:hover {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
.btn-default:active,
.btn-default.active,
.open > .dropdown-toggle.btn-default {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
.btn-default:active:hover,
.btn-default.active:hover,
.open > .dropdown-toggle.btn-default:hover,
.btn-default:active:focus,
.btn-default.active:focus,
.open > .dropdown-toggle.btn-default:focus,
.btn-default:active.focus,
.btn-default.active.focus,
.open > .dropdown-toggle.btn-default.focus {
  color: #333;
  background-color: #d4d4d4;
  border-color: #8c8c8c;
}
.btn-default:active,
.btn-default.active,
.open > .dropdown-toggle.btn-default {
  background-image: none;
}
.btn-default.disabled:hover,
.btn-default[disabled]:hover,
fieldset[disabled] .btn-default:hover,
.btn-default.disabled:focus,
.btn-default[disabled]:focus,
fieldset[disabled] .btn-default:focus,
.btn-default.disabled.focus,
.btn-default[disabled].focus,
fieldset[disabled] .btn-default.focus {
  background-color: #fff;
  border-color: #ccc;
}
.btn-default .badge {
  color: #fff;
  background-color: #333;
}
.btn-primary {
  color: #fff;
  background-color: #337ab7;
  border-color: #2e6da4;
}
.btn-primary:focus,
.btn-primary.focus {
  color: #fff;
  background-color: #286090;
  border-color: #122b40;
}
.btn-primary:hover {
  color: #fff;
  background-color: #286090;
  border-color: #204d74;
}
.btn-primary:active,
.btn-primary.active,
.open > .dropdown-toggle.btn-primary {
  color: #fff;
  background-color: #286090;
  border-color: #204d74;
}
.btn-primary:active:hover,
.btn-primary.active:hover,
.open > .dropdown-toggle.btn-primary:hover,
.btn-primary:active:focus,
.btn-primary.active:focus,
.open > .dropdown-toggle.btn-primary:focus,
.btn-primary:active.focus,
.btn-primary.active.focus,
.open > .dropdown-toggle.btn-primary.focus {
  color: #fff;
  background-color: #204d74;
  border-color: #122b40;
}
.btn-primary:active,
.btn-primary.active,
.open > .dropdown-toggle.btn-primary {
  background-image: none;
}
.btn-primary.disabled:hover,
.btn-primary[disabled]:hover,
fieldset[disabled] .btn-primary:hover,
.btn-primary.disabled:focus,
.btn-primary[disabled]:focus,
fieldset[disabled] .btn-primary:focus,
.btn-primary.disabled.focus,
.btn-primary[disabled].focus,
fieldset[disabled] .btn-primary.focus {
  background-color: #337ab7;
  border-color: #2e6da4;
}
.btn-primary .badge {
  color: #337ab7;
  background-color: #fff;
}
.btn-success {
  color: #fff;
  background-color: #5cb85c;
  border-color: #4cae4c;
}
.btn-success:focus,
.btn-success.focus {
  color: #fff;
  background-color: #449d44;
  border-color: #255625;
}
.btn-success:hover {
  color: #fff;
  background-color: #449d44;
  border-color: #398439;
}
.btn-success:active,
.btn-success.active,
.open > .dropdown-toggle.btn-success {
  color: #fff;
  background-color: #449d44;
  border-color: #398439;
}
.btn-success:active:hover,
.btn-success.active:hover,
.open > .dropdown-toggle.btn-success:hover,
.btn-success:active:focus,
.btn-success.active:focus,
.open > .dropdown-toggle.btn-success:focus,
.btn-success:active.focus,
.btn-success.active.focus,
.open > .dropdown-toggle.btn-success.focus {
  color: #fff;
  background-color: #398439;
  border-color: #255625;
}
.btn-success:active,
.btn-success.active,
.open > .dropdown-toggle.btn-success {
  background-image: none;
}
.btn-success.disabled:hover,
.btn-success[disabled]:hover,
fieldset[disabled] .btn-success:hover,
.btn-success.disabled:focus,
.btn-success[disabled]:focus,
fieldset[disabled] .btn-success:focus,
.btn-success.disabled.focus,
.btn-success[disabled].focus,
fieldset[disabled] .btn-success.focus {
  background-color: #5cb85c;
  border-color: #4cae4c;
}
.btn-success .badge {
  color: #5cb85c;
  background-color: #fff;
}
.btn-info {
  color: #fff;
  background-color: #5bc0de;
  border-color: #46b8da;
}
.btn-info:focus,
.btn-info.focus {
  color: #fff;
  background-color: #31b0d5;
  border-color: #1b6d85;
}
.btn-info:hover {
  color: #fff;
  background-color: #31b0d5;
  border-color: #269abc;
}
.btn-info:active,
.btn-info.active,
.open > .dropdown-toggle.btn-info {
  color: #fff;
  background-color: #31b0d5;
  border-color: #269abc;
}
.btn-info:active:hover,
.btn-info.active:hover,
.open > .dropdown-toggle.btn-info:hover,
.btn-info:active:focus,
.btn-info.active:focus,
.open > .dropdown-toggle.btn-info:focus,
.btn-info:active.focus,
.btn-info.active.focus,
.open > .dropdown-toggle.btn-info.focus {
  color: #fff;
  background-color: #269abc;
  border-color: #1b6d85;
}
.btn-info:active,
.btn-info.active,
.open > .dropdown-toggle.btn-info {
  background-image: none;
}
.btn-info.disabled:hover,
.btn-info[disabled]:hover,
fieldset[disabled] .btn-info:hover,
.btn-info.disabled:focus,
.btn-info[disabled]:focus,
fieldset[disabled] .btn-info:focus,
.btn-info.disabled.focus,
.btn-info[disabled].focus,
fieldset[disabled] .btn-info.focus {
  background-color: #5bc0de;
  border-color: #46b8da;
}
.btn-info .badge {
  color: #5bc0de;
  background-color: #fff;
}
.btn-warning {
  color: #fff;
  background-color: #f0ad4e;
  border-color: #eea236;
}
.btn-warning:focus,
.btn-warning.focus {
  color: #fff;
  background-color: #ec971f;
  border-color: #985f0d;
}
.btn-warning:hover {
  color: #fff;
  background-color: #ec971f;
  border-color: #d58512;
}
.btn-warning:active,
.btn-warning.active,
.open > .dropdown-toggle.btn-warning {
  color: #fff;
  background-color: #ec971f;
  border-color: #d58512;
}
.btn-warning:active:hover,
.btn-warning.active:hover,
.open > .dropdown-toggle.btn-warning:hover,
.btn-warning:active:focus,
.btn-warning.active:focus,
.open > .dropdown-toggle.btn-warning:focus,
.btn-warning:active.focus,
.btn-warning.active.focus,
.open > .dropdown-toggle.btn-warning.focus {
  color: #fff;
  background-color: #d58512;
  border-color: #985f0d;
}
.btn-warning:active,
.btn-warning.active,
.open > .dropdown-toggle.btn-warning {
  background-image: none;
}
.btn-warning.disabled:hover,
.btn-warning[disabled]:hover,
fieldset[disabled] .btn-warning:hover,
.btn-warning.disabled:focus,
.btn-warning[disabled]:focus,
fieldset[disabled] .btn-warning:focus,
.btn-warning.disabled.focus,
.btn-warning[disabled].focus,
fieldset[disabled] .btn-warning.focus {
  background-color: #f0ad4e;
  border-color: #eea236;
}
.btn-warning .badge {
  color: #f0ad4e;
  background-color: #fff;
}
.btn-danger {
  color: #fff;
  background-color: #d9534f;
  border-color: #d43f3a;
}
.btn-danger:focus,
.btn-danger.focus {
  color: #fff;
  background-color: #c9302c;
  border-color: #761c19;
}
.btn-danger:hover {
  color: #fff;
  background-color: #c9302c;
  border-color: #ac2925;
}
.btn-danger:active,
.btn-danger.active,
.open > .dropdown-toggle.btn-danger {
  color: #fff;
  background-color: #c9302c;
  border-color: #ac2925;
}
.btn-danger:active:hover,
.btn-danger.active:hover,
.open > .dropdown-toggle.btn-danger:hover,
.btn-danger:active:focus,
.btn-danger.active:focus,
.open > .dropdown-toggle.btn-danger:focus,
.btn-danger:active.focus,
.btn-danger.active.focus,
.open > .dropdown-toggle.btn-danger.focus {
  color: #fff;
  background-color: #ac2925;
  border-color: #761c19;
}
.btn-danger:active,
.btn-danger.active,
.open > .dropdown-toggle.btn-danger {
  background-image: none;
}
.btn-danger.disabled:hover,
.btn-danger[disabled]:hover,
fieldset[disabled] .btn-danger:hover,
.btn-danger.disabled:focus,
.btn-danger[disabled]:focus,
fieldset[disabled] .btn-danger:focus,
.btn-danger.disabled.focus,
.btn-danger[disabled].focus,
fieldset[disabled] .btn-danger.focus {
  background-color: #d9534f;
  border-color: #d43f3a;
}
.btn-danger .badge {
  color: #d9534f;
  background-color: #fff;
}
.btn-link {
  color: #337ab7;
  font-weight: normal;
  border-radius: 0;
}
.btn-link,
.btn-link:active,
.btn-link.active,
.btn-link[disabled],
fieldset[disabled] .btn-link {
  background-color: transparent;
  -webkit-box-shadow: none;
  box-shadow: none;
}
.btn-link,
.btn-link:hover,
.btn-link:focus,
.btn-link:active {
  border-color: transparent;
}
.btn-link:hover,
.btn-link:focus {
  color: #23527c;
  text-decoration: underline;
  background-color: transparent;
}
.btn-link[disabled]:hover,
fieldset[disabled] .btn-link:hover,
.btn-link[disabled]:focus,
fieldset[disabled] .btn-link:focus {
  color: #777777;
  text-decoration: none;
}
.btn-lg,
.btn-group-lg > .btn {
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
  border-radius: 3px;
}
.btn-sm,
.btn-group-sm > .btn {
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
.btn-xs,
.btn-group-xs > .btn {
  padding: 1px 5px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
.btn-block {
  display: block;
  width: 100%;
}
.btn-block + .btn-block {
  margin-top: 5px;
}
input[type="submit"].btn-block,
input[type="reset"].btn-block,
input[type="button"].btn-block {
  width: 100%;
}
.fade {
  opacity: 0;
  -webkit-transition: opacity 0.15s linear;
  -o-transition: opacity 0.15s linear;
  transition: opacity 0.15s linear;
}
.fade.in {
  opacity: 1;
}
.collapse {
  display: none;
}
.collapse.in {
  display: block;
}
tr.collapse.in {
  display: table-row;
}
tbody.collapse.in {
  display: table-row-group;
}
.collapsing {
  position: relative;
  height: 0;
  overflow: hidden;
  -webkit-transition-property: height, visibility;
  transition-property: height, visibility;
  -webkit-transition-duration: 0.35s;
  transition-duration: 0.35s;
  -webkit-transition-timing-function: ease;
  transition-timing-function: ease;
}
.caret {
  display: inline-block;
  width: 0;
  height: 0;
  margin-left: 2px;
  vertical-align: middle;
  border-top: 4px dashed;
  border-top: 4px solid \9;
  border-right: 4px solid transparent;
  border-left: 4px solid transparent;
}
.dropup,
.dropdown {
  position: relative;
}
.dropdown-toggle:focus {
  outline: 0;
}
.dropdown-menu {
  position: absolute;
  top: 100%;
  left: 0;
  z-index: 1000;
  display: none;
  float: left;
  min-width: 160px;
  padding: 5px 0;
  margin: 2px 0 0;
  list-style: none;
  font-size: 13px;
  text-align: left;
  background-color: #fff;
  border: 1px solid #ccc;
  border: 1px solid rgba(0, 0, 0, 0.15);
  border-radius: 2px;
  -webkit-box-shadow: 0 6px 12px rgba(0, 0, 0, 0.175);
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.175);
  background-clip: padding-box;
}
.dropdown-menu.pull-right {
  right: 0;
  left: auto;
}
.dropdown-menu .divider {
  height: 1px;
  margin: 8px 0;
  overflow: hidden;
  background-color: #e5e5e5;
}
.dropdown-menu > li > a {
  display: block;
  padding: 3px 20px;
  clear: both;
  font-weight: normal;
  line-height: 1.42857143;
  color: #333333;
  white-space: nowrap;
}
.dropdown-menu > li > a:hover,
.dropdown-menu > li > a:focus {
  text-decoration: none;
  color: #262626;
  background-color: #f5f5f5;
}
.dropdown-menu > .active > a,
.dropdown-menu > .active > a:hover,
.dropdown-menu > .active > a:focus {
  color: #fff;
  text-decoration: none;
  outline: 0;
  background-color: #337ab7;
}
.dropdown-menu > .disabled > a,
.dropdown-menu > .disabled > a:hover,
.dropdown-menu > .disabled > a:focus {
  color: #777777;
}
.dropdown-menu > .disabled > a:hover,
.dropdown-menu > .disabled > a:focus {
  text-decoration: none;
  background-color: transparent;
  background-image: none;
  filter: progid:DXImageTransform.Microsoft.gradient(enabled = false);
  cursor: not-allowed;
}
.open > .dropdown-menu {
  display: block;
}
.open > a {
  outline: 0;
}
.dropdown-menu-right {
  left: auto;
  right: 0;
}
.dropdown-menu-left {
  left: 0;
  right: auto;
}
.dropdown-header {
  display: block;
  padding: 3px 20px;
  font-size: 12px;
  line-height: 1.42857143;
  color: #777777;
  white-space: nowrap;
}
.dropdown-backdrop {
  position: fixed;
  left: 0;
  right: 0;
  bottom: 0;
  top: 0;
  z-index: 990;
}
.pull-right > .dropdown-menu {
  right: 0;
  left: auto;
}
.dropup .caret,
.navbar-fixed-bottom .dropdown .caret {
  border-top: 0;
  border-bottom: 4px dashed;
  border-bottom: 4px solid \9;
  content: "";
}
.dropup .dropdown-menu,
.navbar-fixed-bottom .dropdown .dropdown-menu {
  top: auto;
  bottom: 100%;
  margin-bottom: 2px;
}
@media (min-width: 541px) {
  .navbar-right .dropdown-menu {
    left: auto;
    right: 0;
  }
  .navbar-right .dropdown-menu-left {
    left: 0;
    right: auto;
  }
}
.btn-group,
.btn-group-vertical {
  position: relative;
  display: inline-block;
  vertical-align: middle;
}
.btn-group > .btn,
.btn-group-vertical > .btn {
  position: relative;
  float: left;
}
.btn-group > .btn:hover,
.btn-group-vertical > .btn:hover,
.btn-group > .btn:focus,
.btn-group-vertical > .btn:focus,
.btn-group > .btn:active,
.btn-group-vertical > .btn:active,
.btn-group > .btn.active,
.btn-group-vertical > .btn.active {
  z-index: 2;
}
.btn-group .btn + .btn,
.btn-group .btn + .btn-group,
.btn-group .btn-group + .btn,
.btn-group .btn-group + .btn-group {
  margin-left: -1px;
}
.btn-toolbar {
  margin-left: -5px;
}
.btn-toolbar .btn,
.btn-toolbar .btn-group,
.btn-toolbar .input-group {
  float: left;
}
.btn-toolbar > .btn,
.btn-toolbar > .btn-group,
.btn-toolbar > .input-group {
  margin-left: 5px;
}
.btn-group > .btn:not(:first-child):not(:last-child):not(.dropdown-toggle) {
  border-radius: 0;
}
.btn-group > .btn:first-child {
  margin-left: 0;
}
.btn-group > .btn:first-child:not(:last-child):not(.dropdown-toggle) {
  border-bottom-right-radius: 0;
  border-top-right-radius: 0;
}
.btn-group > .btn:last-child:not(:first-child),
.btn-group > .dropdown-toggle:not(:first-child) {
  border-bottom-left-radius: 0;
  border-top-left-radius: 0;
}
.btn-group > .btn-group {
  float: left;
}
.btn-group > .btn-group:not(:first-child):not(:last-child) > .btn {
  border-radius: 0;
}
.btn-group > .btn-group:first-child:not(:last-child) > .btn:last-child,
.btn-group > .btn-group:first-child:not(:last-child) > .dropdown-toggle {
  border-bottom-right-radius: 0;
  border-top-right-radius: 0;
}
.btn-group > .btn-group:last-child:not(:first-child) > .btn:first-child {
  border-bottom-left-radius: 0;
  border-top-left-radius: 0;
}
.btn-group .dropdown-toggle:active,
.btn-group.open .dropdown-toggle {
  outline: 0;
}
.btn-group > .btn + .dropdown-toggle {
  padding-left: 8px;
  padding-right: 8px;
}
.btn-group > .btn-lg + .dropdown-toggle {
  padding-left: 12px;
  padding-right: 12px;
}
.btn-group.open .dropdown-toggle {
  -webkit-box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
  box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
}
.btn-group.open .dropdown-toggle.btn-link {
  -webkit-box-shadow: none;
  box-shadow: none;
}
.btn .caret {
  margin-left: 0;
}
.btn-lg .caret {
  border-width: 5px 5px 0;
  border-bottom-width: 0;
}
.dropup .btn-lg .caret {
  border-width: 0 5px 5px;
}
.btn-group-vertical > .btn,
.btn-group-vertical > .btn-group,
.btn-group-vertical > .btn-group > .btn {
  display: block;
  float: none;
  width: 100%;
  max-width: 100%;
}
.btn-group-vertical > .btn-group > .btn {
  float: none;
}
.btn-group-vertical > .btn + .btn,
.btn-group-vertical > .btn + .btn-group,
.btn-group-vertical > .btn-group + .btn,
.btn-group-vertical > .btn-group + .btn-group {
  margin-top: -1px;
  margin-left: 0;
}
.btn-group-vertical > .btn:not(:first-child):not(:last-child) {
  border-radius: 0;
}
.btn-group-vertical > .btn:first-child:not(:last-child) {
  border-top-right-radius: 2px;
  border-top-left-radius: 2px;
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}
.btn-group-vertical > .btn:last-child:not(:first-child) {
  border-top-right-radius: 0;
  border-top-left-radius: 0;
  border-bottom-right-radius: 2px;
  border-bottom-left-radius: 2px;
}
.btn-group-vertical > .btn-group:not(:first-child):not(:last-child) > .btn {
  border-radius: 0;
}
.btn-group-vertical > .btn-group:first-child:not(:last-child) > .btn:last-child,
.btn-group-vertical > .btn-group:first-child:not(:last-child) > .dropdown-toggle {
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}
.btn-group-vertical > .btn-group:last-child:not(:first-child) > .btn:first-child {
  border-top-right-radius: 0;
  border-top-left-radius: 0;
}
.btn-group-justified {
  display: table;
  width: 100%;
  table-layout: fixed;
  border-collapse: separate;
}
.btn-group-justified > .btn,
.btn-group-justified > .btn-group {
  float: none;
  display: table-cell;
  width: 1%;
}
.btn-group-justified > .btn-group .btn {
  width: 100%;
}
.btn-group-justified > .btn-group .dropdown-menu {
  left: auto;
}
[data-toggle="buttons"] > .btn input[type="radio"],
[data-toggle="buttons"] > .btn-group > .btn input[type="radio"],
[data-toggle="buttons"] > .btn input[type="checkbox"],
[data-toggle="buttons"] > .btn-group > .btn input[type="checkbox"] {
  position: absolute;
  clip: rect(0, 0, 0, 0);
  pointer-events: none;
}
.input-group {
  position: relative;
  display: table;
  border-collapse: separate;
}
.input-group[class*="col-"] {
  float: none;
  padding-left: 0;
  padding-right: 0;
}
.input-group .form-control {
  position: relative;
  z-index: 2;
  float: left;
  width: 100%;
  margin-bottom: 0;
}
.input-group .form-control:focus {
  z-index: 3;
}
.input-group-lg > .form-control,
.input-group-lg > .input-group-addon,
.input-group-lg > .input-group-btn > .btn {
  height: 45px;
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
  border-radius: 3px;
}
select.input-group-lg > .form-control,
select.input-group-lg > .input-group-addon,
select.input-group-lg > .input-group-btn > .btn {
  height: 45px;
  line-height: 45px;
}
textarea.input-group-lg > .form-control,
textarea.input-group-lg > .input-group-addon,
textarea.input-group-lg > .input-group-btn > .btn,
select[multiple].input-group-lg > .form-control,
select[multiple].input-group-lg > .input-group-addon,
select[multiple].input-group-lg > .input-group-btn > .btn {
  height: auto;
}
.input-group-sm > .form-control,
.input-group-sm > .input-group-addon,
.input-group-sm > .input-group-btn > .btn {
  height: 30px;
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
select.input-group-sm > .form-control,
select.input-group-sm > .input-group-addon,
select.input-group-sm > .input-group-btn > .btn {
  height: 30px;
  line-height: 30px;
}
textarea.input-group-sm > .form-control,
textarea.input-group-sm > .input-group-addon,
textarea.input-group-sm > .input-group-btn > .btn,
select[multiple].input-group-sm > .form-control,
select[multiple].input-group-sm > .input-group-addon,
select[multiple].input-group-sm > .input-group-btn > .btn {
  height: auto;
}
.input-group-addon,
.input-group-btn,
.input-group .form-control {
  display: table-cell;
}
.input-group-addon:not(:first-child):not(:last-child),
.input-group-btn:not(:first-child):not(:last-child),
.input-group .form-control:not(:first-child):not(:last-child) {
  border-radius: 0;
}
.input-group-addon,
.input-group-btn {
  width: 1%;
  white-space: nowrap;
  vertical-align: middle;
}
.input-group-addon {
  padding: 6px 12px;
  font-size: 13px;
  font-weight: normal;
  line-height: 1;
  color: #555555;
  text-align: center;
  background-color: #eeeeee;
  border: 1px solid #ccc;
  border-radius: 2px;
}
.input-group-addon.input-sm {
  padding: 5px 10px;
  font-size: 12px;
  border-radius: 1px;
}
.input-group-addon.input-lg {
  padding: 10px 16px;
  font-size: 17px;
  border-radius: 3px;
}
.input-group-addon input[type="radio"],
.input-group-addon input[type="checkbox"] {
  margin-top: 0;
}
.input-group .form-control:first-child,
.input-group-addon:first-child,
.input-group-btn:first-child > .btn,
.input-group-btn:first-child > .btn-group > .btn,
.input-group-btn:first-child > .dropdown-toggle,
.input-group-btn:last-child > .btn:not(:last-child):not(.dropdown-toggle),
.input-group-btn:last-child > .btn-group:not(:last-child) > .btn {
  border-bottom-right-radius: 0;
  border-top-right-radius: 0;
}
.input-group-addon:first-child {
  border-right: 0;
}
.input-group .form-control:last-child,
.input-group-addon:last-child,
.input-group-btn:last-child > .btn,
.input-group-btn:last-child > .btn-group > .btn,
.input-group-btn:last-child > .dropdown-toggle,
.input-group-btn:first-child > .btn:not(:first-child),
.input-group-btn:first-child > .btn-group:not(:first-child) > .btn {
  border-bottom-left-radius: 0;
  border-top-left-radius: 0;
}
.input-group-addon:last-child {
  border-left: 0;
}
.input-group-btn {
  position: relative;
  font-size: 0;
  white-space: nowrap;
}
.input-group-btn > .btn {
  position: relative;
}
.input-group-btn > .btn + .btn {
  margin-left: -1px;
}
.input-group-btn > .btn:hover,
.input-group-btn > .btn:focus,
.input-group-btn > .btn:active {
  z-index: 2;
}
.input-group-btn:first-child > .btn,
.input-group-btn:first-child > .btn-group {
  margin-right: -1px;
}
.input-group-btn:last-child > .btn,
.input-group-btn:last-child > .btn-group {
  z-index: 2;
  margin-left: -1px;
}
.nav {
  margin-bottom: 0;
  padding-left: 0;
  list-style: none;
}
.nav > li {
  position: relative;
  display: block;
}
.nav > li > a {
  position: relative;
  display: block;
  padding: 10px 15px;
}
.nav > li > a:hover,
.nav > li > a:focus {
  text-decoration: none;
  background-color: #eeeeee;
}
.nav > li.disabled > a {
  color: #777777;
}
.nav > li.disabled > a:hover,
.nav > li.disabled > a:focus {
  color: #777777;
  text-decoration: none;
  background-color: transparent;
  cursor: not-allowed;
}
.nav .open > a,
.nav .open > a:hover,
.nav .open > a:focus {
  background-color: #eeeeee;
  border-color: #337ab7;
}
.nav .nav-divider {
  height: 1px;
  margin: 8px 0;
  overflow: hidden;
  background-color: #e5e5e5;
}
.nav > li > a > img {
  max-width: none;
}
.nav-tabs {
  border-bottom: 1px solid #ddd;
}
.nav-tabs > li {
  float: left;
  margin-bottom: -1px;
}
.nav-tabs > li > a {
  margin-right: 2px;
  line-height: 1.42857143;
  border: 1px solid transparent;
  border-radius: 2px 2px 0 0;
}
.nav-tabs > li > a:hover {
  border-color: #eeeeee #eeeeee #ddd;
}
.nav-tabs > li.active > a,
.nav-tabs > li.active > a:hover,
.nav-tabs > li.active > a:focus {
  color: #555555;
  background-color: #fff;
  border: 1px solid #ddd;
  border-bottom-color: transparent;
  cursor: default;
}
.nav-tabs.nav-justified {
  width: 100%;
  border-bottom: 0;
}
.nav-tabs.nav-justified > li {
  float: none;
}
.nav-tabs.nav-justified > li > a {
  text-align: center;
  margin-bottom: 5px;
}
.nav-tabs.nav-justified > .dropdown .dropdown-menu {
  top: auto;
  left: auto;
}
@media (min-width: 768px) {
  .nav-tabs.nav-justified > li {
    display: table-cell;
    width: 1%;
  }
  .nav-tabs.nav-justified > li > a {
    margin-bottom: 0;
  }
}
.nav-tabs.nav-justified > li > a {
  margin-right: 0;
  border-radius: 2px;
}
.nav-tabs.nav-justified > .active > a,
.nav-tabs.nav-justified > .active > a:hover,
.nav-tabs.nav-justified > .active > a:focus {
  border: 1px solid #ddd;
}
@media (min-width: 768px) {
  .nav-tabs.nav-justified > li > a {
    border-bottom: 1px solid #ddd;
    border-radius: 2px 2px 0 0;
  }
  .nav-tabs.nav-justified > .active > a,
  .nav-tabs.nav-justified > .active > a:hover,
  .nav-tabs.nav-justified > .active > a:focus {
    border-bottom-color: #fff;
  }
}
.nav-pills > li {
  float: left;
}
.nav-pills > li > a {
  border-radius: 2px;
}
.nav-pills > li + li {
  margin-left: 2px;
}
.nav-pills > li.active > a,
.nav-pills > li.active > a:hover,
.nav-pills > li.active > a:focus {
  color: #fff;
  background-color: #337ab7;
}
.nav-stacked > li {
  float: none;
}
.nav-stacked > li + li {
  margin-top: 2px;
  margin-left: 0;
}
.nav-justified {
  width: 100%;
}
.nav-justified > li {
  float: none;
}
.nav-justified > li > a {
  text-align: center;
  margin-bottom: 5px;
}
.nav-justified > .dropdown .dropdown-menu {
  top: auto;
  left: auto;
}
@media (min-width: 768px) {
  .nav-justified > li {
    display: table-cell;
    width: 1%;
  }
  .nav-justified > li > a {
    margin-bottom: 0;
  }
}
.nav-tabs-justified {
  border-bottom: 0;
}
.nav-tabs-justified > li > a {
  margin-right: 0;
  border-radius: 2px;
}
.nav-tabs-justified > .active > a,
.nav-tabs-justified > .active > a:hover,
.nav-tabs-justified > .active > a:focus {
  border: 1px solid #ddd;
}
@media (min-width: 768px) {
  .nav-tabs-justified > li > a {
    border-bottom: 1px solid #ddd;
    border-radius: 2px 2px 0 0;
  }
  .nav-tabs-justified > .active > a,
  .nav-tabs-justified > .active > a:hover,
  .nav-tabs-justified > .active > a:focus {
    border-bottom-color: #fff;
  }
}
.tab-content > .tab-pane {
  display: none;
}
.tab-content > .active {
  display: block;
}
.nav-tabs .dropdown-menu {
  margin-top: -1px;
  border-top-right-radius: 0;
  border-top-left-radius: 0;
}
.navbar {
  position: relative;
  min-height: 30px;
  margin-bottom: 18px;
  border: 1px solid transparent;
}
@media (min-width: 541px) {
  .navbar {
    border-radius: 2px;
  }
}
@media (min-width: 541px) {
  .navbar-header {
    float: left;
  }
}
.navbar-collapse {
  overflow-x: visible;
  padding-right: 0px;
  padding-left: 0px;
  border-top: 1px solid transparent;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.1);
  -webkit-overflow-scrolling: touch;
}
.navbar-collapse.in {
  overflow-y: auto;
}
@media (min-width: 541px) {
  .navbar-collapse {
    width: auto;
    border-top: 0;
    box-shadow: none;
  }
  .navbar-collapse.collapse {
    display: block !important;
    height: auto !important;
    padding-bottom: 0;
    overflow: visible !important;
  }
  .navbar-collapse.in {
    overflow-y: visible;
  }
  .navbar-fixed-top .navbar-collapse,
  .navbar-static-top .navbar-collapse,
  .navbar-fixed-bottom .navbar-collapse {
    padding-left: 0;
    padding-right: 0;
  }
}
.navbar-fixed-top .navbar-collapse,
.navbar-fixed-bottom .navbar-collapse {
  max-height: 340px;
}
@media (max-device-width: 540px) and (orientation: landscape) {
  .navbar-fixed-top .navbar-collapse,
  .navbar-fixed-bottom .navbar-collapse {
    max-height: 200px;
  }
}
.container > .navbar-header,
.container-fluid > .navbar-header,
.container > .navbar-collapse,
.container-fluid > .navbar-collapse {
  margin-right: 0px;
  margin-left: 0px;
}
@media (min-width: 541px) {
  .container > .navbar-header,
  .container-fluid > .navbar-header,
  .container > .navbar-collapse,
  .container-fluid > .navbar-collapse {
    margin-right: 0;
    margin-left: 0;
  }
}
.navbar-static-top {
  z-index: 1000;
  border-width: 0 0 1px;
}
@media (min-width: 541px) {
  .navbar-static-top {
    border-radius: 0;
  }
}
.navbar-fixed-top,
.navbar-fixed-bottom {
  position: fixed;
  right: 0;
  left: 0;
  z-index: 1030;
}
@media (min-width: 541px) {
  .navbar-fixed-top,
  .navbar-fixed-bottom {
    border-radius: 0;
  }
}
.navbar-fixed-top {
  top: 0;
  border-width: 0 0 1px;
}
.navbar-fixed-bottom {
  bottom: 0;
  margin-bottom: 0;
  border-width: 1px 0 0;
}
.navbar-brand {
  float: left;
  padding: 6px 0px;
  font-size: 17px;
  line-height: 18px;
  height: 30px;
}
.navbar-brand:hover,
.navbar-brand:focus {
  text-decoration: none;
}
.navbar-brand > img {
  display: block;
}
@media (min-width: 541px) {
  .navbar > .container .navbar-brand,
  .navbar > .container-fluid .navbar-brand {
    margin-left: 0px;
  }
}
.navbar-toggle {
  position: relative;
  float: right;
  margin-right: 0px;
  padding: 9px 10px;
  margin-top: -2px;
  margin-bottom: -2px;
  background-color: transparent;
  background-image: none;
  border: 1px solid transparent;
  border-radius: 2px;
}
.navbar-toggle:focus {
  outline: 0;
}
.navbar-toggle .icon-bar {
  display: block;
  width: 22px;
  height: 2px;
  border-radius: 1px;
}
.navbar-toggle .icon-bar + .icon-bar {
  margin-top: 4px;
}
@media (min-width: 541px) {
  .navbar-toggle {
    display: none;
  }
}
.navbar-nav {
  margin: 3px 0px;
}
.navbar-nav > li > a {
  padding-top: 10px;
  padding-bottom: 10px;
  line-height: 18px;
}
@media (max-width: 540px) {
  .navbar-nav .open .dropdown-menu {
    position: static;
    float: none;
    width: auto;
    margin-top: 0;
    background-color: transparent;
    border: 0;
    box-shadow: none;
  }
  .navbar-nav .open .dropdown-menu > li > a,
  .navbar-nav .open .dropdown-menu .dropdown-header {
    padding: 5px 15px 5px 25px;
  }
  .navbar-nav .open .dropdown-menu > li > a {
    line-height: 18px;
  }
  .navbar-nav .open .dropdown-menu > li > a:hover,
  .navbar-nav .open .dropdown-menu > li > a:focus {
    background-image: none;
  }
}
@media (min-width: 541px) {
  .navbar-nav {
    float: left;
    margin: 0;
  }
  .navbar-nav > li {
    float: left;
  }
  .navbar-nav > li > a {
    padding-top: 6px;
    padding-bottom: 6px;
  }
}
.navbar-form {
  margin-left: 0px;
  margin-right: 0px;
  padding: 10px 0px;
  border-top: 1px solid transparent;
  border-bottom: 1px solid transparent;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.1), 0 1px 0 rgba(255, 255, 255, 0.1);
  margin-top: -1px;
  margin-bottom: -1px;
}
@media (min-width: 768px) {
  .navbar-form .form-group {
    display: inline-block;
    margin-bottom: 0;
    vertical-align: middle;
  }
  .navbar-form .form-control {
    display: inline-block;
    width: auto;
    vertical-align: middle;
  }
  .navbar-form .form-control-static {
    display: inline-block;
  }
  .navbar-form .input-group {
    display: inline-table;
    vertical-align: middle;
  }
  .navbar-form .input-group .input-group-addon,
  .navbar-form .input-group .input-group-btn,
  .navbar-form .input-group .form-control {
    width: auto;
  }
  .navbar-form .input-group > .form-control {
    width: 100%;
  }
  .navbar-form .control-label {
    margin-bottom: 0;
    vertical-align: middle;
  }
  .navbar-form .radio,
  .navbar-form .checkbox {
    display: inline-block;
    margin-top: 0;
    margin-bottom: 0;
    vertical-align: middle;
  }
  .navbar-form .radio label,
  .navbar-form .checkbox label {
    padding-left: 0;
  }
  .navbar-form .radio input[type="radio"],
  .navbar-form .checkbox input[type="checkbox"] {
    position: relative;
    margin-left: 0;
  }
  .navbar-form .has-feedback .form-control-feedback {
    top: 0;
  }
}
@media (max-width: 540px) {
  .navbar-form .form-group {
    margin-bottom: 5px;
  }
  .navbar-form .form-group:last-child {
    margin-bottom: 0;
  }
}
@media (min-width: 541px) {
  .navbar-form {
    width: auto;
    border: 0;
    margin-left: 0;
    margin-right: 0;
    padding-top: 0;
    padding-bottom: 0;
    -webkit-box-shadow: none;
    box-shadow: none;
  }
}
.navbar-nav > li > .dropdown-menu {
  margin-top: 0;
  border-top-right-radius: 0;
  border-top-left-radius: 0;
}
.navbar-fixed-bottom .navbar-nav > li > .dropdown-menu {
  margin-bottom: 0;
  border-top-right-radius: 2px;
  border-top-left-radius: 2px;
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}
.navbar-btn {
  margin-top: -1px;
  margin-bottom: -1px;
}
.navbar-btn.btn-sm {
  margin-top: 0px;
  margin-bottom: 0px;
}
.navbar-btn.btn-xs {
  margin-top: 4px;
  margin-bottom: 4px;
}
.navbar-text {
  margin-top: 6px;
  margin-bottom: 6px;
}
@media (min-width: 541px) {
  .navbar-text {
    float: left;
    margin-left: 0px;
    margin-right: 0px;
  }
}
@media (min-width: 541px) {
  .navbar-left {
    float: left !important;
    float: left;
  }
  .navbar-right {
    float: right !important;
    float: right;
    margin-right: 0px;
  }
  .navbar-right ~ .navbar-right {
    margin-right: 0;
  }
}
.navbar-default {
  background-color: #f8f8f8;
  border-color: #e7e7e7;
}
.navbar-default .navbar-brand {
  color: #777;
}
.navbar-default .navbar-brand:hover,
.navbar-default .navbar-brand:focus {
  color: #5e5e5e;
  background-color: transparent;
}
.navbar-default .navbar-text {
  color: #777;
}
.navbar-default .navbar-nav > li > a {
  color: #777;
}
.navbar-default .navbar-nav > li > a:hover,
.navbar-default .navbar-nav > li > a:focus {
  color: #333;
  background-color: transparent;
}
.navbar-default .navbar-nav > .active > a,
.navbar-default .navbar-nav > .active > a:hover,
.navbar-default .navbar-nav > .active > a:focus {
  color: #555;
  background-color: #e7e7e7;
}
.navbar-default .navbar-nav > .disabled > a,
.navbar-default .navbar-nav > .disabled > a:hover,
.navbar-default .navbar-nav > .disabled > a:focus {
  color: #ccc;
  background-color: transparent;
}
.navbar-default .navbar-toggle {
  border-color: #ddd;
}
.navbar-default .navbar-toggle:hover,
.navbar-default .navbar-toggle:focus {
  background-color: #ddd;
}
.navbar-default .navbar-toggle .icon-bar {
  background-color: #888;
}
.navbar-default .navbar-collapse,
.navbar-default .navbar-form {
  border-color: #e7e7e7;
}
.navbar-default .navbar-nav > .open > a,
.navbar-default .navbar-nav > .open > a:hover,
.navbar-default .navbar-nav > .open > a:focus {
  background-color: #e7e7e7;
  color: #555;
}
@media (max-width: 540px) {
  .navbar-default .navbar-nav .open .dropdown-menu > li > a {
    color: #777;
  }
  .navbar-default .navbar-nav .open .dropdown-menu > li > a:hover,
  .navbar-default .navbar-nav .open .dropdown-menu > li > a:focus {
    color: #333;
    background-color: transparent;
  }
  .navbar-default .navbar-nav .open .dropdown-menu > .active > a,
  .navbar-default .navbar-nav .open .dropdown-menu > .active > a:hover,
  .navbar-default .navbar-nav .open .dropdown-menu > .active > a:focus {
    color: #555;
    background-color: #e7e7e7;
  }
  .navbar-default .navbar-nav .open .dropdown-menu > .disabled > a,
  .navbar-default .navbar-nav .open .dropdown-menu > .disabled > a:hover,
  .navbar-default .navbar-nav .open .dropdown-menu > .disabled > a:focus {
    color: #ccc;
    background-color: transparent;
  }
}
.navbar-default .navbar-link {
  color: #777;
}
.navbar-default .navbar-link:hover {
  color: #333;
}
.navbar-default .btn-link {
  color: #777;
}
.navbar-default .btn-link:hover,
.navbar-default .btn-link:focus {
  color: #333;
}
.navbar-default .btn-link[disabled]:hover,
fieldset[disabled] .navbar-default .btn-link:hover,
.navbar-default .btn-link[disabled]:focus,
fieldset[disabled] .navbar-default .btn-link:focus {
  color: #ccc;
}
.navbar-inverse {
  background-color: #222;
  border-color: #080808;
}
.navbar-inverse .navbar-brand {
  color: #9d9d9d;
}
.navbar-inverse .navbar-brand:hover,
.navbar-inverse .navbar-brand:focus {
  color: #fff;
  background-color: transparent;
}
.navbar-inverse .navbar-text {
  color: #9d9d9d;
}
.navbar-inverse .navbar-nav > li > a {
  color: #9d9d9d;
}
.navbar-inverse .navbar-nav > li > a:hover,
.navbar-inverse .navbar-nav > li > a:focus {
  color: #fff;
  background-color: transparent;
}
.navbar-inverse .navbar-nav > .active > a,
.navbar-inverse .navbar-nav > .active > a:hover,
.navbar-inverse .navbar-nav > .active > a:focus {
  color: #fff;
  background-color: #080808;
}
.navbar-inverse .navbar-nav > .disabled > a,
.navbar-inverse .navbar-nav > .disabled > a:hover,
.navbar-inverse .navbar-nav > .disabled > a:focus {
  color: #444;
  background-color: transparent;
}
.navbar-inverse .navbar-toggle {
  border-color: #333;
}
.navbar-inverse .navbar-toggle:hover,
.navbar-inverse .navbar-toggle:focus {
  background-color: #333;
}
.navbar-inverse .navbar-toggle .icon-bar {
  background-color: #fff;
}
.navbar-inverse .navbar-collapse,
.navbar-inverse .navbar-form {
  border-color: #101010;
}
.navbar-inverse .navbar-nav > .open > a,
.navbar-inverse .navbar-nav > .open > a:hover,
.navbar-inverse .navbar-nav > .open > a:focus {
  background-color: #080808;
  color: #fff;
}
@media (max-width: 540px) {
  .navbar-inverse .navbar-nav .open .dropdown-menu > .dropdown-header {
    border-color: #080808;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu .divider {
    background-color: #080808;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu > li > a {
    color: #9d9d9d;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu > li > a:hover,
  .navbar-inverse .navbar-nav .open .dropdown-menu > li > a:focus {
    color: #fff;
    background-color: transparent;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu > .active > a,
  .navbar-inverse .navbar-nav .open .dropdown-menu > .active > a:hover,
  .navbar-inverse .navbar-nav .open .dropdown-menu > .active > a:focus {
    color: #fff;
    background-color: #080808;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu > .disabled > a,
  .navbar-inverse .navbar-nav .open .dropdown-menu > .disabled > a:hover,
  .navbar-inverse .navbar-nav .open .dropdown-menu > .disabled > a:focus {
    color: #444;
    background-color: transparent;
  }
}
.navbar-inverse .navbar-link {
  color: #9d9d9d;
}
.navbar-inverse .navbar-link:hover {
  color: #fff;
}
.navbar-inverse .btn-link {
  color: #9d9d9d;
}
.navbar-inverse .btn-link:hover,
.navbar-inverse .btn-link:focus {
  color: #fff;
}
.navbar-inverse .btn-link[disabled]:hover,
fieldset[disabled] .navbar-inverse .btn-link:hover,
.navbar-inverse .btn-link[disabled]:focus,
fieldset[disabled] .navbar-inverse .btn-link:focus {
  color: #444;
}
.breadcrumb {
  padding: 8px 15px;
  margin-bottom: 18px;
  list-style: none;
  background-color: #f5f5f5;
  border-radius: 2px;
}
.breadcrumb > li {
  display: inline-block;
}
.breadcrumb > li + li:before {
  content: "/\00a0";
  padding: 0 5px;
  color: #5e5e5e;
}
.breadcrumb > .active {
  color: #777777;
}
.pagination {
  display: inline-block;
  padding-left: 0;
  margin: 18px 0;
  border-radius: 2px;
}
.pagination > li {
  display: inline;
}
.pagination > li > a,
.pagination > li > span {
  position: relative;
  float: left;
  padding: 6px 12px;
  line-height: 1.42857143;
  text-decoration: none;
  color: #337ab7;
  background-color: #fff;
  border: 1px solid #ddd;
  margin-left: -1px;
}
.pagination > li:first-child > a,
.pagination > li:first-child > span {
  margin-left: 0;
  border-bottom-left-radius: 2px;
  border-top-left-radius: 2px;
}
.pagination > li:last-child > a,
.pagination > li:last-child > span {
  border-bottom-right-radius: 2px;
  border-top-right-radius: 2px;
}
.pagination > li > a:hover,
.pagination > li > span:hover,
.pagination > li > a:focus,
.pagination > li > span:focus {
  z-index: 2;
  color: #23527c;
  background-color: #eeeeee;
  border-color: #ddd;
}
.pagination > .active > a,
.pagination > .active > span,
.pagination > .active > a:hover,
.pagination > .active > span:hover,
.pagination > .active > a:focus,
.pagination > .active > span:focus {
  z-index: 3;
  color: #fff;
  background-color: #337ab7;
  border-color: #337ab7;
  cursor: default;
}
.pagination > .disabled > span,
.pagination > .disabled > span:hover,
.pagination > .disabled > span:focus,
.pagination > .disabled > a,
.pagination > .disabled > a:hover,
.pagination > .disabled > a:focus {
  color: #777777;
  background-color: #fff;
  border-color: #ddd;
  cursor: not-allowed;
}
.pagination-lg > li > a,
.pagination-lg > li > span {
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
}
.pagination-lg > li:first-child > a,
.pagination-lg > li:first-child > span {
  border-bottom-left-radius: 3px;
  border-top-left-radius: 3px;
}
.pagination-lg > li:last-child > a,
.pagination-lg > li:last-child > span {
  border-bottom-right-radius: 3px;
  border-top-right-radius: 3px;
}
.pagination-sm > li > a,
.pagination-sm > li > span {
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
}
.pagination-sm > li:first-child > a,
.pagination-sm > li:first-child > span {
  border-bottom-left-radius: 1px;
  border-top-left-radius: 1px;
}
.pagination-sm > li:last-child > a,
.pagination-sm > li:last-child > span {
  border-bottom-right-radius: 1px;
  border-top-right-radius: 1px;
}
.pager {
  padding-left: 0;
  margin: 18px 0;
  list-style: none;
  text-align: center;
}
.pager li {
  display: inline;
}
.pager li > a,
.pager li > span {
  display: inline-block;
  padding: 5px 14px;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 15px;
}
.pager li > a:hover,
.pager li > a:focus {
  text-decoration: none;
  background-color: #eeeeee;
}
.pager .next > a,
.pager .next > span {
  float: right;
}
.pager .previous > a,
.pager .previous > span {
  float: left;
}
.pager .disabled > a,
.pager .disabled > a:hover,
.pager .disabled > a:focus,
.pager .disabled > span {
  color: #777777;
  background-color: #fff;
  cursor: not-allowed;
}
.label {
  display: inline;
  padding: .2em .6em .3em;
  font-size: 75%;
  font-weight: bold;
  line-height: 1;
  color: #fff;
  text-align: center;
  white-space: nowrap;
  vertical-align: baseline;
  border-radius: .25em;
}
a.label:hover,
a.label:focus {
  color: #fff;
  text-decoration: none;
  cursor: pointer;
}
.label:empty {
  display: none;
}
.btn .label {
  position: relative;
  top: -1px;
}
.label-default {
  background-color: #777777;
}
.label-default[href]:hover,
.label-default[href]:focus {
  background-color: #5e5e5e;
}
.label-primary {
  background-color: #337ab7;
}
.label-primary[href]:hover,
.label-primary[href]:focus {
  background-color: #286090;
}
.label-success {
  background-color: #5cb85c;
}
.label-success[href]:hover,
.label-success[href]:focus {
  background-color: #449d44;
}
.label-info {
  background-color: #5bc0de;
}
.label-info[href]:hover,
.label-info[href]:focus {
  background-color: #31b0d5;
}
.label-warning {
  background-color: #f0ad4e;
}
.label-warning[href]:hover,
.label-warning[href]:focus {
  background-color: #ec971f;
}
.label-danger {
  background-color: #d9534f;
}
.label-danger[href]:hover,
.label-danger[href]:focus {
  background-color: #c9302c;
}
.badge {
  display: inline-block;
  min-width: 10px;
  padding: 3px 7px;
  font-size: 12px;
  font-weight: bold;
  color: #fff;
  line-height: 1;
  vertical-align: middle;
  white-space: nowrap;
  text-align: center;
  background-color: #777777;
  border-radius: 10px;
}
.badge:empty {
  display: none;
}
.btn .badge {
  position: relative;
  top: -1px;
}
.btn-xs .badge,
.btn-group-xs > .btn .badge {
  top: 0;
  padding: 1px 5px;
}
a.badge:hover,
a.badge:focus {
  color: #fff;
  text-decoration: none;
  cursor: pointer;
}
.list-group-item.active > .badge,
.nav-pills > .active > a > .badge {
  color: #337ab7;
  background-color: #fff;
}
.list-group-item > .badge {
  float: right;
}
.list-group-item > .badge + .badge {
  margin-right: 5px;
}
.nav-pills > li > a > .badge {
  margin-left: 3px;
}
.jumbotron {
  padding-top: 30px;
  padding-bottom: 30px;
  margin-bottom: 30px;
  color: inherit;
  background-color: #eeeeee;
}
.jumbotron h1,
.jumbotron .h1 {
  color: inherit;
}
.jumbotron p {
  margin-bottom: 15px;
  font-size: 20px;
  font-weight: 200;
}
.jumbotron > hr {
  border-top-color: #d5d5d5;
}
.container .jumbotron,
.container-fluid .jumbotron {
  border-radius: 3px;
  padding-left: 0px;
  padding-right: 0px;
}
.jumbotron .container {
  max-width: 100%;
}
@media screen and (min-width: 768px) {
  .jumbotron {
    padding-top: 48px;
    padding-bottom: 48px;
  }
  .container .jumbotron,
  .container-fluid .jumbotron {
    padding-left: 60px;
    padding-right: 60px;
  }
  .jumbotron h1,
  .jumbotron .h1 {
    font-size: 59px;
  }
}
.thumbnail {
  display: block;
  padding: 4px;
  margin-bottom: 18px;
  line-height: 1.42857143;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 2px;
  -webkit-transition: border 0.2s ease-in-out;
  -o-transition: border 0.2s ease-in-out;
  transition: border 0.2s ease-in-out;
}
.thumbnail > img,
.thumbnail a > img {
  margin-left: auto;
  margin-right: auto;
}
a.thumbnail:hover,
a.thumbnail:focus,
a.thumbnail.active {
  border-color: #337ab7;
}
.thumbnail .caption {
  padding: 9px;
  color: #000;
}
.alert {
  padding: 15px;
  margin-bottom: 18px;
  border: 1px solid transparent;
  border-radius: 2px;
}
.alert h4 {
  margin-top: 0;
  color: inherit;
}
.alert .alert-link {
  font-weight: bold;
}
.alert > p,
.alert > ul {
  margin-bottom: 0;
}
.alert > p + p {
  margin-top: 5px;
}
.alert-dismissable,
.alert-dismissible {
  padding-right: 35px;
}
.alert-dismissable .close,
.alert-dismissible .close {
  position: relative;
  top: -2px;
  right: -21px;
  color: inherit;
}
.alert-success {
  background-color: #dff0d8;
  border-color: #d6e9c6;
  color: #3c763d;
}
.alert-success hr {
  border-top-color: #c9e2b3;
}
.alert-success .alert-link {
  color: #2b542c;
}
.alert-info {
  background-color: #d9edf7;
  border-color: #bce8f1;
  color: #31708f;
}
.alert-info hr {
  border-top-color: #a6e1ec;
}
.alert-info .alert-link {
  color: #245269;
}
.alert-warning {
  background-color: #fcf8e3;
  border-color: #faebcc;
  color: #8a6d3b;
}
.alert-warning hr {
  border-top-color: #f7e1b5;
}
.alert-warning .alert-link {
  color: #66512c;
}
.alert-danger {
  background-color: #f2dede;
  border-color: #ebccd1;
  color: #a94442;
}
.alert-danger hr {
  border-top-color: #e4b9c0;
}
.alert-danger .alert-link {
  color: #843534;
}
@-webkit-keyframes progress-bar-stripes {
  from {
    background-position: 40px 0;
  }
  to {
    background-position: 0 0;
  }
}
@keyframes progress-bar-stripes {
  from {
    background-position: 40px 0;
  }
  to {
    background-position: 0 0;
  }
}
.progress {
  overflow: hidden;
  height: 18px;
  margin-bottom: 18px;
  background-color: #f5f5f5;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 1px 2px rgba(0, 0, 0, 0.1);
  box-shadow: inset 0 1px 2px rgba(0, 0, 0, 0.1);
}
.progress-bar {
  float: left;
  width: 0%;
  height: 100%;
  font-size: 12px;
  line-height: 18px;
  color: #fff;
  text-align: center;
  background-color: #337ab7;
  -webkit-box-shadow: inset 0 -1px 0 rgba(0, 0, 0, 0.15);
  box-shadow: inset 0 -1px 0 rgba(0, 0, 0, 0.15);
  -webkit-transition: width 0.6s ease;
  -o-transition: width 0.6s ease;
  transition: width 0.6s ease;
}
.progress-striped .progress-bar,
.progress-bar-striped {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-size: 40px 40px;
}
.progress.active .progress-bar,
.progress-bar.active {
  -webkit-animation: progress-bar-stripes 2s linear infinite;
  -o-animation: progress-bar-stripes 2s linear infinite;
  animation: progress-bar-stripes 2s linear infinite;
}
.progress-bar-success {
  background-color: #5cb85c;
}
.progress-striped .progress-bar-success {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
}
.progress-bar-info {
  background-color: #5bc0de;
}
.progress-striped .progress-bar-info {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
}
.progress-bar-warning {
  background-color: #f0ad4e;
}
.progress-striped .progress-bar-warning {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
}
.progress-bar-danger {
  background-color: #d9534f;
}
.progress-striped .progress-bar-danger {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
}
.media {
  margin-top: 15px;
}
.media:first-child {
  margin-top: 0;
}
.media,
.media-body {
  zoom: 1;
  overflow: hidden;
}
.media-body {
  width: 10000px;
}
.media-object {
  display: block;
}
.media-object.img-thumbnail {
  max-width: none;
}
.media-right,
.media > .pull-right {
  padding-left: 10px;
}
.media-left,
.media > .pull-left {
  padding-right: 10px;
}
.media-left,
.media-right,
.media-body {
  display: table-cell;
  vertical-align: top;
}
.media-middle {
  vertical-align: middle;
}
.media-bottom {
  vertical-align: bottom;
}
.media-heading {
  margin-top: 0;
  margin-bottom: 5px;
}
.media-list {
  padding-left: 0;
  list-style: none;
}
.list-group {
  margin-bottom: 20px;
  padding-left: 0;
}
.list-group-item {
  position: relative;
  display: block;
  padding: 10px 15px;
  margin-bottom: -1px;
  background-color: #fff;
  border: 1px solid #ddd;
}
.list-group-item:first-child {
  border-top-right-radius: 2px;
  border-top-left-radius: 2px;
}
.list-group-item:last-child {
  margin-bottom: 0;
  border-bottom-right-radius: 2px;
  border-bottom-left-radius: 2px;
}
a.list-group-item,
button.list-group-item {
  color: #555;
}
a.list-group-item .list-group-item-heading,
button.list-group-item .list-group-item-heading {
  color: #333;
}
a.list-group-item:hover,
button.list-group-item:hover,
a.list-group-item:focus,
button.list-group-item:focus {
  text-decoration: none;
  color: #555;
  background-color: #f5f5f5;
}
button.list-group-item {
  width: 100%;
  text-align: left;
}
.list-group-item.disabled,
.list-group-item.disabled:hover,
.list-group-item.disabled:focus {
  background-color: #eeeeee;
  color: #777777;
  cursor: not-allowed;
}
.list-group-item.disabled .list-group-item-heading,
.list-group-item.disabled:hover .list-group-item-heading,
.list-group-item.disabled:focus .list-group-item-heading {
  color: inherit;
}
.list-group-item.disabled .list-group-item-text,
.list-group-item.disabled:hover .list-group-item-text,
.list-group-item.disabled:focus .list-group-item-text {
  color: #777777;
}
.list-group-item.active,
.list-group-item.active:hover,
.list-group-item.active:focus {
  z-index: 2;
  color: #fff;
  background-color: #337ab7;
  border-color: #337ab7;
}
.list-group-item.active .list-group-item-heading,
.list-group-item.active:hover .list-group-item-heading,
.list-group-item.active:focus .list-group-item-heading,
.list-group-item.active .list-group-item-heading > small,
.list-group-item.active:hover .list-group-item-heading > small,
.list-group-item.active:focus .list-group-item-heading > small,
.list-group-item.active .list-group-item-heading > .small,
.list-group-item.active:hover .list-group-item-heading > .small,
.list-group-item.active:focus .list-group-item-heading > .small {
  color: inherit;
}
.list-group-item.active .list-group-item-text,
.list-group-item.active:hover .list-group-item-text,
.list-group-item.active:focus .list-group-item-text {
  color: #c7ddef;
}
.list-group-item-success {
  color: #3c763d;
  background-color: #dff0d8;
}
a.list-group-item-success,
button.list-group-item-success {
  color: #3c763d;
}
a.list-group-item-success .list-group-item-heading,
button.list-group-item-success .list-group-item-heading {
  color: inherit;
}
a.list-group-item-success:hover,
button.list-group-item-success:hover,
a.list-group-item-success:focus,
button.list-group-item-success:focus {
  color: #3c763d;
  background-color: #d0e9c6;
}
a.list-group-item-success.active,
button.list-group-item-success.active,
a.list-group-item-success.active:hover,
button.list-group-item-success.active:hover,
a.list-group-item-success.active:focus,
button.list-group-item-success.active:focus {
  color: #fff;
  background-color: #3c763d;
  border-color: #3c763d;
}
.list-group-item-info {
  color: #31708f;
  background-color: #d9edf7;
}
a.list-group-item-info,
button.list-group-item-info {
  color: #31708f;
}
a.list-group-item-info .list-group-item-heading,
button.list-group-item-info .list-group-item-heading {
  color: inherit;
}
a.list-group-item-info:hover,
button.list-group-item-info:hover,
a.list-group-item-info:focus,
button.list-group-item-info:focus {
  color: #31708f;
  background-color: #c4e3f3;
}
a.list-group-item-info.active,
button.list-group-item-info.active,
a.list-group-item-info.active:hover,
button.list-group-item-info.active:hover,
a.list-group-item-info.active:focus,
button.list-group-item-info.active:focus {
  color: #fff;
  background-color: #31708f;
  border-color: #31708f;
}
.list-group-item-warning {
  color: #8a6d3b;
  background-color: #fcf8e3;
}
a.list-group-item-warning,
button.list-group-item-warning {
  color: #8a6d3b;
}
a.list-group-item-warning .list-group-item-heading,
button.list-group-item-warning .list-group-item-heading {
  color: inherit;
}
a.list-group-item-warning:hover,
button.list-group-item-warning:hover,
a.list-group-item-warning:focus,
button.list-group-item-warning:focus {
  color: #8a6d3b;
  background-color: #faf2cc;
}
a.list-group-item-warning.active,
button.list-group-item-warning.active,
a.list-group-item-warning.active:hover,
button.list-group-item-warning.active:hover,
a.list-group-item-warning.active:focus,
button.list-group-item-warning.active:focus {
  color: #fff;
  background-color: #8a6d3b;
  border-color: #8a6d3b;
}
.list-group-item-danger {
  color: #a94442;
  background-color: #f2dede;
}
a.list-group-item-danger,
button.list-group-item-danger {
  color: #a94442;
}
a.list-group-item-danger .list-group-item-heading,
button.list-group-item-danger .list-group-item-heading {
  color: inherit;
}
a.list-group-item-danger:hover,
button.list-group-item-danger:hover,
a.list-group-item-danger:focus,
button.list-group-item-danger:focus {
  color: #a94442;
  background-color: #ebcccc;
}
a.list-group-item-danger.active,
button.list-group-item-danger.active,
a.list-group-item-danger.active:hover,
button.list-group-item-danger.active:hover,
a.list-group-item-danger.active:focus,
button.list-group-item-danger.active:focus {
  color: #fff;
  background-color: #a94442;
  border-color: #a94442;
}
.list-group-item-heading {
  margin-top: 0;
  margin-bottom: 5px;
}
.list-group-item-text {
  margin-bottom: 0;
  line-height: 1.3;
}
.panel {
  margin-bottom: 18px;
  background-color: #fff;
  border: 1px solid transparent;
  border-radius: 2px;
  -webkit-box-shadow: 0 1px 1px rgba(0, 0, 0, 0.05);
  box-shadow: 0 1px 1px rgba(0, 0, 0, 0.05);
}
.panel-body {
  padding: 15px;
}
.panel-heading {
  padding: 10px 15px;
  border-bottom: 1px solid transparent;
  border-top-right-radius: 1px;
  border-top-left-radius: 1px;
}
.panel-heading > .dropdown .dropdown-toggle {
  color: inherit;
}
.panel-title {
  margin-top: 0;
  margin-bottom: 0;
  font-size: 15px;
  color: inherit;
}
.panel-title > a,
.panel-title > small,
.panel-title > .small,
.panel-title > small > a,
.panel-title > .small > a {
  color: inherit;
}
.panel-footer {
  padding: 10px 15px;
  background-color: #f5f5f5;
  border-top: 1px solid #ddd;
  border-bottom-right-radius: 1px;
  border-bottom-left-radius: 1px;
}
.panel > .list-group,
.panel > .panel-collapse > .list-group {
  margin-bottom: 0;
}
.panel > .list-group .list-group-item,
.panel > .panel-collapse > .list-group .list-group-item {
  border-width: 1px 0;
  border-radius: 0;
}
.panel > .list-group:first-child .list-group-item:first-child,
.panel > .panel-collapse > .list-group:first-child .list-group-item:first-child {
  border-top: 0;
  border-top-right-radius: 1px;
  border-top-left-radius: 1px;
}
.panel > .list-group:last-child .list-group-item:last-child,
.panel > .panel-collapse > .list-group:last-child .list-group-item:last-child {
  border-bottom: 0;
  border-bottom-right-radius: 1px;
  border-bottom-left-radius: 1px;
}
.panel > .panel-heading + .panel-collapse > .list-group .list-group-item:first-child {
  border-top-right-radius: 0;
  border-top-left-radius: 0;
}
.panel-heading + .list-group .list-group-item:first-child {
  border-top-width: 0;
}
.list-group + .panel-footer {
  border-top-width: 0;
}
.panel > .table,
.panel > .table-responsive > .table,
.panel > .panel-collapse > .table {
  margin-bottom: 0;
}
.panel > .table caption,
.panel > .table-responsive > .table caption,
.panel > .panel-collapse > .table caption {
  padding-left: 15px;
  padding-right: 15px;
}
.panel > .table:first-child,
.panel > .table-responsive:first-child > .table:first-child {
  border-top-right-radius: 1px;
  border-top-left-radius: 1px;
}
.panel > .table:first-child > thead:first-child > tr:first-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child,
.panel > .table:first-child > tbody:first-child > tr:first-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child {
  border-top-left-radius: 1px;
  border-top-right-radius: 1px;
}
.panel > .table:first-child > thead:first-child > tr:first-child td:first-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child td:first-child,
.panel > .table:first-child > tbody:first-child > tr:first-child td:first-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child td:first-child,
.panel > .table:first-child > thead:first-child > tr:first-child th:first-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child th:first-child,
.panel > .table:first-child > tbody:first-child > tr:first-child th:first-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child th:first-child {
  border-top-left-radius: 1px;
}
.panel > .table:first-child > thead:first-child > tr:first-child td:last-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child td:last-child,
.panel > .table:first-child > tbody:first-child > tr:first-child td:last-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child td:last-child,
.panel > .table:first-child > thead:first-child > tr:first-child th:last-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child th:last-child,
.panel > .table:first-child > tbody:first-child > tr:first-child th:last-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child th:last-child {
  border-top-right-radius: 1px;
}
.panel > .table:last-child,
.panel > .table-responsive:last-child > .table:last-child {
  border-bottom-right-radius: 1px;
  border-bottom-left-radius: 1px;
}
.panel > .table:last-child > tbody:last-child > tr:last-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child {
  border-bottom-left-radius: 1px;
  border-bottom-right-radius: 1px;
}
.panel > .table:last-child > tbody:last-child > tr:last-child td:first-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child td:first-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child td:first-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child td:first-child,
.panel > .table:last-child > tbody:last-child > tr:last-child th:first-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child th:first-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child th:first-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child th:first-child {
  border-bottom-left-radius: 1px;
}
.panel > .table:last-child > tbody:last-child > tr:last-child td:last-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child td:last-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child td:last-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child td:last-child,
.panel > .table:last-child > tbody:last-child > tr:last-child th:last-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child th:last-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child th:last-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child th:last-child {
  border-bottom-right-radius: 1px;
}
.panel > .panel-body + .table,
.panel > .panel-body + .table-responsive,
.panel > .table + .panel-body,
.panel > .table-responsive + .panel-body {
  border-top: 1px solid #ddd;
}
.panel > .table > tbody:first-child > tr:first-child th,
.panel > .table > tbody:first-child > tr:first-child td {
  border-top: 0;
}
.panel > .table-bordered,
.panel > .table-responsive > .table-bordered {
  border: 0;
}
.panel > .table-bordered > thead > tr > th:first-child,
.panel > .table-responsive > .table-bordered > thead > tr > th:first-child,
.panel > .table-bordered > tbody > tr > th:first-child,
.panel > .table-responsive > .table-bordered > tbody > tr > th:first-child,
.panel > .table-bordered > tfoot > tr > th:first-child,
.panel > .table-responsive > .table-bordered > tfoot > tr > th:first-child,
.panel > .table-bordered > thead > tr > td:first-child,
.panel > .table-responsive > .table-bordered > thead > tr > td:first-child,
.panel > .table-bordered > tbody > tr > td:first-child,
.panel > .table-responsive > .table-bordered > tbody > tr > td:first-child,
.panel > .table-bordered > tfoot > tr > td:first-child,
.panel > .table-responsive > .table-bordered > tfoot > tr > td:first-child {
  border-left: 0;
}
.panel > .table-bordered > thead > tr > th:last-child,
.panel > .table-responsive > .table-bordered > thead > tr > th:last-child,
.panel > .table-bordered > tbody > tr > th:last-child,
.panel > .table-responsive > .table-bordered > tbody > tr > th:last-child,
.panel > .table-bordered > tfoot > tr > th:last-child,
.panel > .table-responsive > .table-bordered > tfoot > tr > th:last-child,
.panel > .table-bordered > thead > tr > td:last-child,
.panel > .table-responsive > .table-bordered > thead > tr > td:last-child,
.panel > .table-bordered > tbody > tr > td:last-child,
.panel > .table-responsive > .table-bordered > tbody > tr > td:last-child,
.panel > .table-bordered > tfoot > tr > td:last-child,
.panel > .table-responsive > .table-bordered > tfoot > tr > td:last-child {
  border-right: 0;
}
.panel > .table-bordered > thead > tr:first-child > td,
.panel > .table-responsive > .table-bordered > thead > tr:first-child > td,
.panel > .table-bordered > tbody > tr:first-child > td,
.panel > .table-responsive > .table-bordered > tbody > tr:first-child > td,
.panel > .table-bordered > thead > tr:first-child > th,
.panel > .table-responsive > .table-bordered > thead > tr:first-child > th,
.panel > .table-bordered > tbody > tr:first-child > th,
.panel > .table-responsive > .table-bordered > tbody > tr:first-child > th {
  border-bottom: 0;
}
.panel > .table-bordered > tbody > tr:last-child > td,
.panel > .table-responsive > .table-bordered > tbody > tr:last-child > td,
.panel > .table-bordered > tfoot > tr:last-child > td,
.panel > .table-responsive > .table-bordered > tfoot > tr:last-child > td,
.panel > .table-bordered > tbody > tr:last-child > th,
.panel > .table-responsive > .table-bordered > tbody > tr:last-child > th,
.panel > .table-bordered > tfoot > tr:last-child > th,
.panel > .table-responsive > .table-bordered > tfoot > tr:last-child > th {
  border-bottom: 0;
}
.panel > .table-responsive {
  border: 0;
  margin-bottom: 0;
}
.panel-group {
  margin-bottom: 18px;
}
.panel-group .panel {
  margin-bottom: 0;
  border-radius: 2px;
}
.panel-group .panel + .panel {
  margin-top: 5px;
}
.panel-group .panel-heading {
  border-bottom: 0;
}
.panel-group .panel-heading + .panel-collapse > .panel-body,
.panel-group .panel-heading + .panel-collapse > .list-group {
  border-top: 1px solid #ddd;
}
.panel-group .panel-footer {
  border-top: 0;
}
.panel-group .panel-footer + .panel-collapse .panel-body {
  border-bottom: 1px solid #ddd;
}
.panel-default {
  border-color: #ddd;
}
.panel-default > .panel-heading {
  color: #333333;
  background-color: #f5f5f5;
  border-color: #ddd;
}
.panel-default > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #ddd;
}
.panel-default > .panel-heading .badge {
  color: #f5f5f5;
  background-color: #333333;
}
.panel-default > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #ddd;
}
.panel-primary {
  border-color: #337ab7;
}
.panel-primary > .panel-heading {
  color: #fff;
  background-color: #337ab7;
  border-color: #337ab7;
}
.panel-primary > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #337ab7;
}
.panel-primary > .panel-heading .badge {
  color: #337ab7;
  background-color: #fff;
}
.panel-primary > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #337ab7;
}
.panel-success {
  border-color: #d6e9c6;
}
.panel-success > .panel-heading {
  color: #3c763d;
  background-color: #dff0d8;
  border-color: #d6e9c6;
}
.panel-success > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #d6e9c6;
}
.panel-success > .panel-heading .badge {
  color: #dff0d8;
  background-color: #3c763d;
}
.panel-success > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #d6e9c6;
}
.panel-info {
  border-color: #bce8f1;
}
.panel-info > .panel-heading {
  color: #31708f;
  background-color: #d9edf7;
  border-color: #bce8f1;
}
.panel-info > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #bce8f1;
}
.panel-info > .panel-heading .badge {
  color: #d9edf7;
  background-color: #31708f;
}
.panel-info > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #bce8f1;
}
.panel-warning {
  border-color: #faebcc;
}
.panel-warning > .panel-heading {
  color: #8a6d3b;
  background-color: #fcf8e3;
  border-color: #faebcc;
}
.panel-warning > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #faebcc;
}
.panel-warning > .panel-heading .badge {
  color: #fcf8e3;
  background-color: #8a6d3b;
}
.panel-warning > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #faebcc;
}
.panel-danger {
  border-color: #ebccd1;
}
.panel-danger > .panel-heading {
  color: #a94442;
  background-color: #f2dede;
  border-color: #ebccd1;
}
.panel-danger > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #ebccd1;
}
.panel-danger > .panel-heading .badge {
  color: #f2dede;
  background-color: #a94442;
}
.panel-danger > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #ebccd1;
}
.embed-responsive {
  position: relative;
  display: block;
  height: 0;
  padding: 0;
  overflow: hidden;
}
.embed-responsive .embed-responsive-item,
.embed-responsive iframe,
.embed-responsive embed,
.embed-responsive object,
.embed-responsive video {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  height: 100%;
  width: 100%;
  border: 0;
}
.embed-responsive-16by9 {
  padding-bottom: 56.25%;
}
.embed-responsive-4by3 {
  padding-bottom: 75%;
}
.well {
  min-height: 20px;
  padding: 19px;
  margin-bottom: 20px;
  background-color: #f5f5f5;
  border: 1px solid #e3e3e3;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.05);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.05);
}
.well blockquote {
  border-color: #ddd;
  border-color: rgba(0, 0, 0, 0.15);
}
.well-lg {
  padding: 24px;
  border-radius: 3px;
}
.well-sm {
  padding: 9px;
  border-radius: 1px;
}
.close {
  float: right;
  font-size: 19.5px;
  font-weight: bold;
  line-height: 1;
  color: #000;
  text-shadow: 0 1px 0 #fff;
  opacity: 0.2;
  filter: alpha(opacity=20);
}
.close:hover,
.close:focus {
  color: #000;
  text-decoration: none;
  cursor: pointer;
  opacity: 0.5;
  filter: alpha(opacity=50);
}
button.close {
  padding: 0;
  cursor: pointer;
  background: transparent;
  border: 0;
  -webkit-appearance: none;
}
.modal-open {
  overflow: hidden;
}
.modal {
  display: none;
  overflow: hidden;
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 1050;
  -webkit-overflow-scrolling: touch;
  outline: 0;
}
.modal.fade .modal-dialog {
  -webkit-transform: translate(0, -25%);
  -ms-transform: translate(0, -25%);
  -o-transform: translate(0, -25%);
  transform: translate(0, -25%);
  -webkit-transition: -webkit-transform 0.3s ease-out;
  -moz-transition: -moz-transform 0.3s ease-out;
  -o-transition: -o-transform 0.3s ease-out;
  transition: transform 0.3s ease-out;
}
.modal.in .modal-dialog {
  -webkit-transform: translate(0, 0);
  -ms-transform: translate(0, 0);
  -o-transform: translate(0, 0);
  transform: translate(0, 0);
}
.modal-open .modal {
  overflow-x: hidden;
  overflow-y: auto;
}
.modal-dialog {
  position: relative;
  width: auto;
  margin: 10px;
}
.modal-content {
  position: relative;
  background-color: #fff;
  border: 1px solid #999;
  border: 1px solid rgba(0, 0, 0, 0.2);
  border-radius: 3px;
  -webkit-box-shadow: 0 3px 9px rgba(0, 0, 0, 0.5);
  box-shadow: 0 3px 9px rgba(0, 0, 0, 0.5);
  background-clip: padding-box;
  outline: 0;
}
.modal-backdrop {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 1040;
  background-color: #000;
}
.modal-backdrop.fade {
  opacity: 0;
  filter: alpha(opacity=0);
}
.modal-backdrop.in {
  opacity: 0.5;
  filter: alpha(opacity=50);
}
.modal-header {
  padding: 15px;
  border-bottom: 1px solid #e5e5e5;
}
.modal-header .close {
  margin-top: -2px;
}
.modal-title {
  margin: 0;
  line-height: 1.42857143;
}
.modal-body {
  position: relative;
  padding: 15px;
}
.modal-footer {
  padding: 15px;
  text-align: right;
  border-top: 1px solid #e5e5e5;
}
.modal-footer .btn + .btn {
  margin-left: 5px;
  margin-bottom: 0;
}
.modal-footer .btn-group .btn + .btn {
  margin-left: -1px;
}
.modal-footer .btn-block + .btn-block {
  margin-left: 0;
}
.modal-scrollbar-measure {
  position: absolute;
  top: -9999px;
  width: 50px;
  height: 50px;
  overflow: scroll;
}
@media (min-width: 768px) {
  .modal-dialog {
    width: 600px;
    margin: 30px auto;
  }
  .modal-content {
    -webkit-box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
  }
  .modal-sm {
    width: 300px;
  }
}
@media (min-width: 992px) {
  .modal-lg {
    width: 900px;
  }
}
.tooltip {
  position: absolute;
  z-index: 1070;
  display: block;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-style: normal;
  font-weight: normal;
  letter-spacing: normal;
  line-break: auto;
  line-height: 1.42857143;
  text-align: left;
  text-align: start;
  text-decoration: none;
  text-shadow: none;
  text-transform: none;
  white-space: normal;
  word-break: normal;
  word-spacing: normal;
  word-wrap: normal;
  font-size: 12px;
  opacity: 0;
  filter: alpha(opacity=0);
}
.tooltip.in {
  opacity: 0.9;
  filter: alpha(opacity=90);
}
.tooltip.top {
  margin-top: -3px;
  padding: 5px 0;
}
.tooltip.right {
  margin-left: 3px;
  padding: 0 5px;
}
.tooltip.bottom {
  margin-top: 3px;
  padding: 5px 0;
}
.tooltip.left {
  margin-left: -3px;
  padding: 0 5px;
}
.tooltip-inner {
  max-width: 200px;
  padding: 3px 8px;
  color: #fff;
  text-align: center;
  background-color: #000;
  border-radius: 2px;
}
.tooltip-arrow {
  position: absolute;
  width: 0;
  height: 0;
  border-color: transparent;
  border-style: solid;
}
.tooltip.top .tooltip-arrow {
  bottom: 0;
  left: 50%;
  margin-left: -5px;
  border-width: 5px 5px 0;
  border-top-color: #000;
}
.tooltip.top-left .tooltip-arrow {
  bottom: 0;
  right: 5px;
  margin-bottom: -5px;
  border-width: 5px 5px 0;
  border-top-color: #000;
}
.tooltip.top-right .tooltip-arrow {
  bottom: 0;
  left: 5px;
  margin-bottom: -5px;
  border-width: 5px 5px 0;
  border-top-color: #000;
}
.tooltip.right .tooltip-arrow {
  top: 50%;
  left: 0;
  margin-top: -5px;
  border-width: 5px 5px 5px 0;
  border-right-color: #000;
}
.tooltip.left .tooltip-arrow {
  top: 50%;
  right: 0;
  margin-top: -5px;
  border-width: 5px 0 5px 5px;
  border-left-color: #000;
}
.tooltip.bottom .tooltip-arrow {
  top: 0;
  left: 50%;
  margin-left: -5px;
  border-width: 0 5px 5px;
  border-bottom-color: #000;
}
.tooltip.bottom-left .tooltip-arrow {
  top: 0;
  right: 5px;
  margin-top: -5px;
  border-width: 0 5px 5px;
  border-bottom-color: #000;
}
.tooltip.bottom-right .tooltip-arrow {
  top: 0;
  left: 5px;
  margin-top: -5px;
  border-width: 0 5px 5px;
  border-bottom-color: #000;
}
.popover {
  position: absolute;
  top: 0;
  left: 0;
  z-index: 1060;
  display: none;
  max-width: 276px;
  padding: 1px;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-style: normal;
  font-weight: normal;
  letter-spacing: normal;
  line-break: auto;
  line-height: 1.42857143;
  text-align: left;
  text-align: start;
  text-decoration: none;
  text-shadow: none;
  text-transform: none;
  white-space: normal;
  word-break: normal;
  word-spacing: normal;
  word-wrap: normal;
  font-size: 13px;
  background-color: #fff;
  background-clip: padding-box;
  border: 1px solid #ccc;
  border: 1px solid rgba(0, 0, 0, 0.2);
  border-radius: 3px;
  -webkit-box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
}
.popover.top {
  margin-top: -10px;
}
.popover.right {
  margin-left: 10px;
}
.popover.bottom {
  margin-top: 10px;
}
.popover.left {
  margin-left: -10px;
}
.popover-title {
  margin: 0;
  padding: 8px 14px;
  font-size: 13px;
  background-color: #f7f7f7;
  border-bottom: 1px solid #ebebeb;
  border-radius: 2px 2px 0 0;
}
.popover-content {
  padding: 9px 14px;
}
.popover > .arrow,
.popover > .arrow:after {
  position: absolute;
  display: block;
  width: 0;
  height: 0;
  border-color: transparent;
  border-style: solid;
}
.popover > .arrow {
  border-width: 11px;
}
.popover > .arrow:after {
  border-width: 10px;
  content: "";
}
.popover.top > .arrow {
  left: 50%;
  margin-left: -11px;
  border-bottom-width: 0;
  border-top-color: #999999;
  border-top-color: rgba(0, 0, 0, 0.25);
  bottom: -11px;
}
.popover.top > .arrow:after {
  content: " ";
  bottom: 1px;
  margin-left: -10px;
  border-bottom-width: 0;
  border-top-color: #fff;
}
.popover.right > .arrow {
  top: 50%;
  left: -11px;
  margin-top: -11px;
  border-left-width: 0;
  border-right-color: #999999;
  border-right-color: rgba(0, 0, 0, 0.25);
}
.popover.right > .arrow:after {
  content: " ";
  left: 1px;
  bottom: -10px;
  border-left-width: 0;
  border-right-color: #fff;
}
.popover.bottom > .arrow {
  left: 50%;
  margin-left: -11px;
  border-top-width: 0;
  border-bottom-color: #999999;
  border-bottom-color: rgba(0, 0, 0, 0.25);
  top: -11px;
}
.popover.bottom > .arrow:after {
  content: " ";
  top: 1px;
  margin-left: -10px;
  border-top-width: 0;
  border-bottom-color: #fff;
}
.popover.left > .arrow {
  top: 50%;
  right: -11px;
  margin-top: -11px;
  border-right-width: 0;
  border-left-color: #999999;
  border-left-color: rgba(0, 0, 0, 0.25);
}
.popover.left > .arrow:after {
  content: " ";
  right: 1px;
  border-right-width: 0;
  border-left-color: #fff;
  bottom: -10px;
}
.carousel {
  position: relative;
}
.carousel-inner {
  position: relative;
  overflow: hidden;
  width: 100%;
}
.carousel-inner > .item {
  display: none;
  position: relative;
  -webkit-transition: 0.6s ease-in-out left;
  -o-transition: 0.6s ease-in-out left;
  transition: 0.6s ease-in-out left;
}
.carousel-inner > .item > img,
.carousel-inner > .item > a > img {
  line-height: 1;
}
@media all and (transform-3d), (-webkit-transform-3d) {
  .carousel-inner > .item {
    -webkit-transition: -webkit-transform 0.6s ease-in-out;
    -moz-transition: -moz-transform 0.6s ease-in-out;
    -o-transition: -o-transform 0.6s ease-in-out;
    transition: transform 0.6s ease-in-out;
    -webkit-backface-visibility: hidden;
    -moz-backface-visibility: hidden;
    backface-visibility: hidden;
    -webkit-perspective: 1000px;
    -moz-perspective: 1000px;
    perspective: 1000px;
  }
  .carousel-inner > .item.next,
  .carousel-inner > .item.active.right {
    -webkit-transform: translate3d(100%, 0, 0);
    transform: translate3d(100%, 0, 0);
    left: 0;
  }
  .carousel-inner > .item.prev,
  .carousel-inner > .item.active.left {
    -webkit-transform: translate3d(-100%, 0, 0);
    transform: translate3d(-100%, 0, 0);
    left: 0;
  }
  .carousel-inner > .item.next.left,
  .carousel-inner > .item.prev.right,
  .carousel-inner > .item.active {
    -webkit-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
    left: 0;
  }
}
.carousel-inner > .active,
.carousel-inner > .next,
.carousel-inner > .prev {
  display: block;
}
.carousel-inner > .active {
  left: 0;
}
.carousel-inner > .next,
.carousel-inner > .prev {
  position: absolute;
  top: 0;
  width: 100%;
}
.carousel-inner > .next {
  left: 100%;
}
.carousel-inner > .prev {
  left: -100%;
}
.carousel-inner > .next.left,
.carousel-inner > .prev.right {
  left: 0;
}
.carousel-inner > .active.left {
  left: -100%;
}
.carousel-inner > .active.right {
  left: 100%;
}
.carousel-control {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  width: 15%;
  opacity: 0.5;
  filter: alpha(opacity=50);
  font-size: 20px;
  color: #fff;
  text-align: center;
  text-shadow: 0 1px 2px rgba(0, 0, 0, 0.6);
  background-color: rgba(0, 0, 0, 0);
}
.carousel-control.left {
  background-image: -webkit-linear-gradient(left, rgba(0, 0, 0, 0.5) 0%, rgba(0, 0, 0, 0.0001) 100%);
  background-image: -o-linear-gradient(left, rgba(0, 0, 0, 0.5) 0%, rgba(0, 0, 0, 0.0001) 100%);
  background-image: linear-gradient(to right, rgba(0, 0, 0, 0.5) 0%, rgba(0, 0, 0, 0.0001) 100%);
  background-repeat: repeat-x;
  filter: progid:DXImageTransform.Microsoft.gradient(startColorstr='#80000000', endColorstr='#00000000', GradientType=1);
}
.carousel-control.right {
  left: auto;
  right: 0;
  background-image: -webkit-linear-gradient(left, rgba(0, 0, 0, 0.0001) 0%, rgba(0, 0, 0, 0.5) 100%);
  background-image: -o-linear-gradient(left, rgba(0, 0, 0, 0.0001) 0%, rgba(0, 0, 0, 0.5) 100%);
  background-image: linear-gradient(to right, rgba(0, 0, 0, 0.0001) 0%, rgba(0, 0, 0, 0.5) 100%);
  background-repeat: repeat-x;
  filter: progid:DXImageTransform.Microsoft.gradient(startColorstr='#00000000', endColorstr='#80000000', GradientType=1);
}
.carousel-control:hover,
.carousel-control:focus {
  outline: 0;
  color: #fff;
  text-decoration: none;
  opacity: 0.9;
  filter: alpha(opacity=90);
}
.carousel-control .icon-prev,
.carousel-control .icon-next,
.carousel-control .glyphicon-chevron-left,
.carousel-control .glyphicon-chevron-right {
  position: absolute;
  top: 50%;
  margin-top: -10px;
  z-index: 5;
  display: inline-block;
}
.carousel-control .icon-prev,
.carousel-control .glyphicon-chevron-left {
  left: 50%;
  margin-left: -10px;
}
.carousel-control .icon-next,
.carousel-control .glyphicon-chevron-right {
  right: 50%;
  margin-right: -10px;
}
.carousel-control .icon-prev,
.carousel-control .icon-next {
  width: 20px;
  height: 20px;
  line-height: 1;
  font-family: serif;
}
.carousel-control .icon-prev:before {
  content: '\2039';
}
.carousel-control .icon-next:before {
  content: '\203a';
}
.carousel-indicators {
  position: absolute;
  bottom: 10px;
  left: 50%;
  z-index: 15;
  width: 60%;
  margin-left: -30%;
  padding-left: 0;
  list-style: none;
  text-align: center;
}
.carousel-indicators li {
  display: inline-block;
  width: 10px;
  height: 10px;
  margin: 1px;
  text-indent: -999px;
  border: 1px solid #fff;
  border-radius: 10px;
  cursor: pointer;
  background-color: #000 \9;
  background-color: rgba(0, 0, 0, 0);
}
.carousel-indicators .active {
  margin: 0;
  width: 12px;
  height: 12px;
  background-color: #fff;
}
.carousel-caption {
  position: absolute;
  left: 15%;
  right: 15%;
  bottom: 20px;
  z-index: 10;
  padding-top: 20px;
  padding-bottom: 20px;
  color: #fff;
  text-align: center;
  text-shadow: 0 1px 2px rgba(0, 0, 0, 0.6);
}
.carousel-caption .btn {
  text-shadow: none;
}
@media screen and (min-width: 768px) {
  .carousel-control .glyphicon-chevron-left,
  .carousel-control .glyphicon-chevron-right,
  .carousel-control .icon-prev,
  .carousel-control .icon-next {
    width: 30px;
    height: 30px;
    margin-top: -10px;
    font-size: 30px;
  }
  .carousel-control .glyphicon-chevron-left,
  .carousel-control .icon-prev {
    margin-left: -10px;
  }
  .carousel-control .glyphicon-chevron-right,
  .carousel-control .icon-next {
    margin-right: -10px;
  }
  .carousel-caption {
    left: 20%;
    right: 20%;
    padding-bottom: 30px;
  }
  .carousel-indicators {
    bottom: 20px;
  }
}
.clearfix:before,
.clearfix:after,
.dl-horizontal dd:before,
.dl-horizontal dd:after,
.container:before,
.container:after,
.container-fluid:before,
.container-fluid:after,
.row:before,
.row:after,
.form-horizontal .form-group:before,
.form-horizontal .form-group:after,
.btn-toolbar:before,
.btn-toolbar:after,
.btn-group-vertical > .btn-group:before,
.btn-group-vertical > .btn-group:after,
.nav:before,
.nav:after,
.navbar:before,
.navbar:after,
.navbar-header:before,
.navbar-header:after,
.navbar-collapse:before,
.navbar-collapse:after,
.pager:before,
.pager:after,
.panel-body:before,
.panel-body:after,
.modal-header:before,
.modal-header:after,
.modal-footer:before,
.modal-footer:after,
.item_buttons:before,
.item_buttons:after {
  content: " ";
  display: table;
}
.clearfix:after,
.dl-horizontal dd:after,
.container:after,
.container-fluid:after,
.row:after,
.form-horizontal .form-group:after,
.btn-toolbar:after,
.btn-group-vertical > .btn-group:after,
.nav:after,
.navbar:after,
.navbar-header:after,
.navbar-collapse:after,
.pager:after,
.panel-body:after,
.modal-header:after,
.modal-footer:after,
.item_buttons:after {
  clear: both;
}
.center-block {
  display: block;
  margin-left: auto;
  margin-right: auto;
}
.pull-right {
  float: right !important;
}
.pull-left {
  float: left !important;
}
.hide {
  display: none !important;
}
.show {
  display: block !important;
}
.invisible {
  visibility: hidden;
}
.text-hide {
  font: 0/0 a;
  color: transparent;
  text-shadow: none;
  background-color: transparent;
  border: 0;
}
.hidden {
  display: none !important;
}
.affix {
  position: fixed;
}
@-ms-viewport {
  width: device-width;
}
.visible-xs,
.visible-sm,
.visible-md,
.visible-lg {
  display: none !important;
}
.visible-xs-block,
.visible-xs-inline,
.visible-xs-inline-block,
.visible-sm-block,
.visible-sm-inline,
.visible-sm-inline-block,
.visible-md-block,
.visible-md-inline,
.visible-md-inline-block,
.visible-lg-block,
.visible-lg-inline,
.visible-lg-inline-block {
  display: none !important;
}
@media (max-width: 767px) {
  .visible-xs {
    display: block !important;
  }
  table.visible-xs {
    display: table !important;
  }
  tr.visible-xs {
    display: table-row !important;
  }
  th.visible-xs,
  td.visible-xs {
    display: table-cell !important;
  }
}
@media (max-width: 767px) {
  .visible-xs-block {
    display: block !important;
  }
}
@media (max-width: 767px) {
  .visible-xs-inline {
    display: inline !important;
  }
}
@media (max-width: 767px) {
  .visible-xs-inline-block {
    display: inline-block !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .visible-sm {
    display: block !important;
  }
  table.visible-sm {
    display: table !important;
  }
  tr.visible-sm {
    display: table-row !important;
  }
  th.visible-sm,
  td.visible-sm {
    display: table-cell !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .visible-sm-block {
    display: block !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .visible-sm-inline {
    display: inline !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .visible-sm-inline-block {
    display: inline-block !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .visible-md {
    display: block !important;
  }
  table.visible-md {
    display: table !important;
  }
  tr.visible-md {
    display: table-row !important;
  }
  th.visible-md,
  td.visible-md {
    display: table-cell !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .visible-md-block {
    display: block !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .visible-md-inline {
    display: inline !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .visible-md-inline-block {
    display: inline-block !important;
  }
}
@media (min-width: 1200px) {
  .visible-lg {
    display: block !important;
  }
  table.visible-lg {
    display: table !important;
  }
  tr.visible-lg {
    display: table-row !important;
  }
  th.visible-lg,
  td.visible-lg {
    display: table-cell !important;
  }
}
@media (min-width: 1200px) {
  .visible-lg-block {
    display: block !important;
  }
}
@media (min-width: 1200px) {
  .visible-lg-inline {
    display: inline !important;
  }
}
@media (min-width: 1200px) {
  .visible-lg-inline-block {
    display: inline-block !important;
  }
}
@media (max-width: 767px) {
  .hidden-xs {
    display: none !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .hidden-sm {
    display: none !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .hidden-md {
    display: none !important;
  }
}
@media (min-width: 1200px) {
  .hidden-lg {
    display: none !important;
  }
}
.visible-print {
  display: none !important;
}
@media print {
  .visible-print {
    display: block !important;
  }
  table.visible-print {
    display: table !important;
  }
  tr.visible-print {
    display: table-row !important;
  }
  th.visible-print,
  td.visible-print {
    display: table-cell !important;
  }
}
.visible-print-block {
  display: none !important;
}
@media print {
  .visible-print-block {
    display: block !important;
  }
}
.visible-print-inline {
  display: none !important;
}
@media print {
  .visible-print-inline {
    display: inline !important;
  }
}
.visible-print-inline-block {
  display: none !important;
}
@media print {
  .visible-print-inline-block {
    display: inline-block !important;
  }
}
@media print {
  .hidden-print {
    display: none !important;
  }
}
/*!
*
* Font Awesome
*
*/
/*!
 *  Font Awesome 4.2.0 by @davegandy - http://fontawesome.io - @fontawesome
 *  License - http://fontawesome.io/license (Font: SIL OFL 1.1, CSS: MIT License)
 */
/* FONT PATH
 * -------------------------- */
@font-face {
  font-family: 'FontAwesome';
  src: url('../components/font-awesome/fonts/fontawesome-webfont.eot?v=4.2.0');
  src: url('../components/font-awesome/fonts/fontawesome-webfont.eot?#iefix&v=4.2.0') format('embedded-opentype'), url('../components/font-awesome/fonts/fontawesome-webfont.woff?v=4.2.0') format('woff'), url('../components/font-awesome/fonts/fontawesome-webfont.ttf?v=4.2.0') format('truetype'), url('../components/font-awesome/fonts/fontawesome-webfont.svg?v=4.2.0#fontawesomeregular') format('svg');
  font-weight: normal;
  font-style: normal;
}
.fa {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
/* makes the font 33% larger relative to the icon container */
.fa-lg {
  font-size: 1.33333333em;
  line-height: 0.75em;
  vertical-align: -15%;
}
.fa-2x {
  font-size: 2em;
}
.fa-3x {
  font-size: 3em;
}
.fa-4x {
  font-size: 4em;
}
.fa-5x {
  font-size: 5em;
}
.fa-fw {
  width: 1.28571429em;
  text-align: center;
}
.fa-ul {
  padding-left: 0;
  margin-left: 2.14285714em;
  list-style-type: none;
}
.fa-ul > li {
  position: relative;
}
.fa-li {
  position: absolute;
  left: -2.14285714em;
  width: 2.14285714em;
  top: 0.14285714em;
  text-align: center;
}
.fa-li.fa-lg {
  left: -1.85714286em;
}
.fa-border {
  padding: .2em .25em .15em;
  border: solid 0.08em #eee;
  border-radius: .1em;
}
.pull-right {
  float: right;
}
.pull-left {
  float: left;
}
.fa.pull-left {
  margin-right: .3em;
}
.fa.pull-right {
  margin-left: .3em;
}
.fa-spin {
  -webkit-animation: fa-spin 2s infinite linear;
  animation: fa-spin 2s infinite linear;
}
@-webkit-keyframes fa-spin {
  0% {
    -webkit-transform: rotate(0deg);
    transform: rotate(0deg);
  }
  100% {
    -webkit-transform: rotate(359deg);
    transform: rotate(359deg);
  }
}
@keyframes fa-spin {
  0% {
    -webkit-transform: rotate(0deg);
    transform: rotate(0deg);
  }
  100% {
    -webkit-transform: rotate(359deg);
    transform: rotate(359deg);
  }
}
.fa-rotate-90 {
  filter: progid:DXImageTransform.Microsoft.BasicImage(rotation=1);
  -webkit-transform: rotate(90deg);
  -ms-transform: rotate(90deg);
  transform: rotate(90deg);
}
.fa-rotate-180 {
  filter: progid:DXImageTransform.Microsoft.BasicImage(rotation=2);
  -webkit-transform: rotate(180deg);
  -ms-transform: rotate(180deg);
  transform: rotate(180deg);
}
.fa-rotate-270 {
  filter: progid:DXImageTransform.Microsoft.BasicImage(rotation=3);
  -webkit-transform: rotate(270deg);
  -ms-transform: rotate(270deg);
  transform: rotate(270deg);
}
.fa-flip-horizontal {
  filter: progid:DXImageTransform.Microsoft.BasicImage(rotation=0, mirror=1);
  -webkit-transform: scale(-1, 1);
  -ms-transform: scale(-1, 1);
  transform: scale(-1, 1);
}
.fa-flip-vertical {
  filter: progid:DXImageTransform.Microsoft.BasicImage(rotation=2, mirror=1);
  -webkit-transform: scale(1, -1);
  -ms-transform: scale(1, -1);
  transform: scale(1, -1);
}
:root .fa-rotate-90,
:root .fa-rotate-180,
:root .fa-rotate-270,
:root .fa-flip-horizontal,
:root .fa-flip-vertical {
  filter: none;
}
.fa-stack {
  position: relative;
  display: inline-block;
  width: 2em;
  height: 2em;
  line-height: 2em;
  vertical-align: middle;
}
.fa-stack-1x,
.fa-stack-2x {
  position: absolute;
  left: 0;
  width: 100%;
  text-align: center;
}
.fa-stack-1x {
  line-height: inherit;
}
.fa-stack-2x {
  font-size: 2em;
}
.fa-inverse {
  color: #fff;
}
/* Font Awesome uses the Unicode Private Use Area (PUA) to ensure screen
   readers do not read off random characters that represent icons */
.fa-glass:before {
  content: "\f000";
}
.fa-music:before {
  content: "\f001";
}
.fa-search:before {
  content: "\f002";
}
.fa-envelope-o:before {
  content: "\f003";
}
.fa-heart:before {
  content: "\f004";
}
.fa-star:before {
  content: "\f005";
}
.fa-star-o:before {
  content: "\f006";
}
.fa-user:before {
  content: "\f007";
}
.fa-film:before {
  content: "\f008";
}
.fa-th-large:before {
  content: "\f009";
}
.fa-th:before {
  content: "\f00a";
}
.fa-th-list:before {
  content: "\f00b";
}
.fa-check:before {
  content: "\f00c";
}
.fa-remove:before,
.fa-close:before,
.fa-times:before {
  content: "\f00d";
}
.fa-search-plus:before {
  content: "\f00e";
}
.fa-search-minus:before {
  content: "\f010";
}
.fa-power-off:before {
  content: "\f011";
}
.fa-signal:before {
  content: "\f012";
}
.fa-gear:before,
.fa-cog:before {
  content: "\f013";
}
.fa-trash-o:before {
  content: "\f014";
}
.fa-home:before {
  content: "\f015";
}
.fa-file-o:before {
  content: "\f016";
}
.fa-clock-o:before {
  content: "\f017";
}
.fa-road:before {
  content: "\f018";
}
.fa-download:before {
  content: "\f019";
}
.fa-arrow-circle-o-down:before {
  content: "\f01a";
}
.fa-arrow-circle-o-up:before {
  content: "\f01b";
}
.fa-inbox:before {
  content: "\f01c";
}
.fa-play-circle-o:before {
  content: "\f01d";
}
.fa-rotate-right:before,
.fa-repeat:before {
  content: "\f01e";
}
.fa-refresh:before {
  content: "\f021";
}
.fa-list-alt:before {
  content: "\f022";
}
.fa-lock:before {
  content: "\f023";
}
.fa-flag:before {
  content: "\f024";
}
.fa-headphones:before {
  content: "\f025";
}
.fa-volume-off:before {
  content: "\f026";
}
.fa-volume-down:before {
  content: "\f027";
}
.fa-volume-up:before {
  content: "\f028";
}
.fa-qrcode:before {
  content: "\f029";
}
.fa-barcode:before {
  content: "\f02a";
}
.fa-tag:before {
  content: "\f02b";
}
.fa-tags:before {
  content: "\f02c";
}
.fa-book:before {
  content: "\f02d";
}
.fa-bookmark:before {
  content: "\f02e";
}
.fa-print:before {
  content: "\f02f";
}
.fa-camera:before {
  content: "\f030";
}
.fa-font:before {
  content: "\f031";
}
.fa-bold:before {
  content: "\f032";
}
.fa-italic:before {
  content: "\f033";
}
.fa-text-height:before {
  content: "\f034";
}
.fa-text-width:before {
  content: "\f035";
}
.fa-align-left:before {
  content: "\f036";
}
.fa-align-center:before {
  content: "\f037";
}
.fa-align-right:before {
  content: "\f038";
}
.fa-align-justify:before {
  content: "\f039";
}
.fa-list:before {
  content: "\f03a";
}
.fa-dedent:before,
.fa-outdent:before {
  content: "\f03b";
}
.fa-indent:before {
  content: "\f03c";
}
.fa-video-camera:before {
  content: "\f03d";
}
.fa-photo:before,
.fa-image:before,
.fa-picture-o:before {
  content: "\f03e";
}
.fa-pencil:before {
  content: "\f040";
}
.fa-map-marker:before {
  content: "\f041";
}
.fa-adjust:before {
  content: "\f042";
}
.fa-tint:before {
  content: "\f043";
}
.fa-edit:before,
.fa-pencil-square-o:before {
  content: "\f044";
}
.fa-share-square-o:before {
  content: "\f045";
}
.fa-check-square-o:before {
  content: "\f046";
}
.fa-arrows:before {
  content: "\f047";
}
.fa-step-backward:before {
  content: "\f048";
}
.fa-fast-backward:before {
  content: "\f049";
}
.fa-backward:before {
  content: "\f04a";
}
.fa-play:before {
  content: "\f04b";
}
.fa-pause:before {
  content: "\f04c";
}
.fa-stop:before {
  content: "\f04d";
}
.fa-forward:before {
  content: "\f04e";
}
.fa-fast-forward:before {
  content: "\f050";
}
.fa-step-forward:before {
  content: "\f051";
}
.fa-eject:before {
  content: "\f052";
}
.fa-chevron-left:before {
  content: "\f053";
}
.fa-chevron-right:before {
  content: "\f054";
}
.fa-plus-circle:before {
  content: "\f055";
}
.fa-minus-circle:before {
  content: "\f056";
}
.fa-times-circle:before {
  content: "\f057";
}
.fa-check-circle:before {
  content: "\f058";
}
.fa-question-circle:before {
  content: "\f059";
}
.fa-info-circle:before {
  content: "\f05a";
}
.fa-crosshairs:before {
  content: "\f05b";
}
.fa-times-circle-o:before {
  content: "\f05c";
}
.fa-check-circle-o:before {
  content: "\f05d";
}
.fa-ban:before {
  content: "\f05e";
}
.fa-arrow-left:before {
  content: "\f060";
}
.fa-arrow-right:before {
  content: "\f061";
}
.fa-arrow-up:before {
  content: "\f062";
}
.fa-arrow-down:before {
  content: "\f063";
}
.fa-mail-forward:before,
.fa-share:before {
  content: "\f064";
}
.fa-expand:before {
  content: "\f065";
}
.fa-compress:before {
  content: "\f066";
}
.fa-plus:before {
  content: "\f067";
}
.fa-minus:before {
  content: "\f068";
}
.fa-asterisk:before {
  content: "\f069";
}
.fa-exclamation-circle:before {
  content: "\f06a";
}
.fa-gift:before {
  content: "\f06b";
}
.fa-leaf:before {
  content: "\f06c";
}
.fa-fire:before {
  content: "\f06d";
}
.fa-eye:before {
  content: "\f06e";
}
.fa-eye-slash:before {
  content: "\f070";
}
.fa-warning:before,
.fa-exclamation-triangle:before {
  content: "\f071";
}
.fa-plane:before {
  content: "\f072";
}
.fa-calendar:before {
  content: "\f073";
}
.fa-random:before {
  content: "\f074";
}
.fa-comment:before {
  content: "\f075";
}
.fa-magnet:before {
  content: "\f076";
}
.fa-chevron-up:before {
  content: "\f077";
}
.fa-chevron-down:before {
  content: "\f078";
}
.fa-retweet:before {
  content: "\f079";
}
.fa-shopping-cart:before {
  content: "\f07a";
}
.fa-folder:before {
  content: "\f07b";
}
.fa-folder-open:before {
  content: "\f07c";
}
.fa-arrows-v:before {
  content: "\f07d";
}
.fa-arrows-h:before {
  content: "\f07e";
}
.fa-bar-chart-o:before,
.fa-bar-chart:before {
  content: "\f080";
}
.fa-twitter-square:before {
  content: "\f081";
}
.fa-facebook-square:before {
  content: "\f082";
}
.fa-camera-retro:before {
  content: "\f083";
}
.fa-key:before {
  content: "\f084";
}
.fa-gears:before,
.fa-cogs:before {
  content: "\f085";
}
.fa-comments:before {
  content: "\f086";
}
.fa-thumbs-o-up:before {
  content: "\f087";
}
.fa-thumbs-o-down:before {
  content: "\f088";
}
.fa-star-half:before {
  content: "\f089";
}
.fa-heart-o:before {
  content: "\f08a";
}
.fa-sign-out:before {
  content: "\f08b";
}
.fa-linkedin-square:before {
  content: "\f08c";
}
.fa-thumb-tack:before {
  content: "\f08d";
}
.fa-external-link:before {
  content: "\f08e";
}
.fa-sign-in:before {
  content: "\f090";
}
.fa-trophy:before {
  content: "\f091";
}
.fa-github-square:before {
  content: "\f092";
}
.fa-upload:before {
  content: "\f093";
}
.fa-lemon-o:before {
  content: "\f094";
}
.fa-phone:before {
  content: "\f095";
}
.fa-square-o:before {
  content: "\f096";
}
.fa-bookmark-o:before {
  content: "\f097";
}
.fa-phone-square:before {
  content: "\f098";
}
.fa-twitter:before {
  content: "\f099";
}
.fa-facebook:before {
  content: "\f09a";
}
.fa-github:before {
  content: "\f09b";
}
.fa-unlock:before {
  content: "\f09c";
}
.fa-credit-card:before {
  content: "\f09d";
}
.fa-rss:before {
  content: "\f09e";
}
.fa-hdd-o:before {
  content: "\f0a0";
}
.fa-bullhorn:before {
  content: "\f0a1";
}
.fa-bell:before {
  content: "\f0f3";
}
.fa-certificate:before {
  content: "\f0a3";
}
.fa-hand-o-right:before {
  content: "\f0a4";
}
.fa-hand-o-left:before {
  content: "\f0a5";
}
.fa-hand-o-up:before {
  content: "\f0a6";
}
.fa-hand-o-down:before {
  content: "\f0a7";
}
.fa-arrow-circle-left:before {
  content: "\f0a8";
}
.fa-arrow-circle-right:before {
  content: "\f0a9";
}
.fa-arrow-circle-up:before {
  content: "\f0aa";
}
.fa-arrow-circle-down:before {
  content: "\f0ab";
}
.fa-globe:before {
  content: "\f0ac";
}
.fa-wrench:before {
  content: "\f0ad";
}
.fa-tasks:before {
  content: "\f0ae";
}
.fa-filter:before {
  content: "\f0b0";
}
.fa-briefcase:before {
  content: "\f0b1";
}
.fa-arrows-alt:before {
  content: "\f0b2";
}
.fa-group:before,
.fa-users:before {
  content: "\f0c0";
}
.fa-chain:before,
.fa-link:before {
  content: "\f0c1";
}
.fa-cloud:before {
  content: "\f0c2";
}
.fa-flask:before {
  content: "\f0c3";
}
.fa-cut:before,
.fa-scissors:before {
  content: "\f0c4";
}
.fa-copy:before,
.fa-files-o:before {
  content: "\f0c5";
}
.fa-paperclip:before {
  content: "\f0c6";
}
.fa-save:before,
.fa-floppy-o:before {
  content: "\f0c7";
}
.fa-square:before {
  content: "\f0c8";
}
.fa-navicon:before,
.fa-reorder:before,
.fa-bars:before {
  content: "\f0c9";
}
.fa-list-ul:before {
  content: "\f0ca";
}
.fa-list-ol:before {
  content: "\f0cb";
}
.fa-strikethrough:before {
  content: "\f0cc";
}
.fa-underline:before {
  content: "\f0cd";
}
.fa-table:before {
  content: "\f0ce";
}
.fa-magic:before {
  content: "\f0d0";
}
.fa-truck:before {
  content: "\f0d1";
}
.fa-pinterest:before {
  content: "\f0d2";
}
.fa-pinterest-square:before {
  content: "\f0d3";
}
.fa-google-plus-square:before {
  content: "\f0d4";
}
.fa-google-plus:before {
  content: "\f0d5";
}
.fa-money:before {
  content: "\f0d6";
}
.fa-caret-down:before {
  content: "\f0d7";
}
.fa-caret-up:before {
  content: "\f0d8";
}
.fa-caret-left:before {
  content: "\f0d9";
}
.fa-caret-right:before {
  content: "\f0da";
}
.fa-columns:before {
  content: "\f0db";
}
.fa-unsorted:before,
.fa-sort:before {
  content: "\f0dc";
}
.fa-sort-down:before,
.fa-sort-desc:before {
  content: "\f0dd";
}
.fa-sort-up:before,
.fa-sort-asc:before {
  content: "\f0de";
}
.fa-envelope:before {
  content: "\f0e0";
}
.fa-linkedin:before {
  content: "\f0e1";
}
.fa-rotate-left:before,
.fa-undo:before {
  content: "\f0e2";
}
.fa-legal:before,
.fa-gavel:before {
  content: "\f0e3";
}
.fa-dashboard:before,
.fa-tachometer:before {
  content: "\f0e4";
}
.fa-comment-o:before {
  content: "\f0e5";
}
.fa-comments-o:before {
  content: "\f0e6";
}
.fa-flash:before,
.fa-bolt:before {
  content: "\f0e7";
}
.fa-sitemap:before {
  content: "\f0e8";
}
.fa-umbrella:before {
  content: "\f0e9";
}
.fa-paste:before,
.fa-clipboard:before {
  content: "\f0ea";
}
.fa-lightbulb-o:before {
  content: "\f0eb";
}
.fa-exchange:before {
  content: "\f0ec";
}
.fa-cloud-download:before {
  content: "\f0ed";
}
.fa-cloud-upload:before {
  content: "\f0ee";
}
.fa-user-md:before {
  content: "\f0f0";
}
.fa-stethoscope:before {
  content: "\f0f1";
}
.fa-suitcase:before {
  content: "\f0f2";
}
.fa-bell-o:before {
  content: "\f0a2";
}
.fa-coffee:before {
  content: "\f0f4";
}
.fa-cutlery:before {
  content: "\f0f5";
}
.fa-file-text-o:before {
  content: "\f0f6";
}
.fa-building-o:before {
  content: "\f0f7";
}
.fa-hospital-o:before {
  content: "\f0f8";
}
.fa-ambulance:before {
  content: "\f0f9";
}
.fa-medkit:before {
  content: "\f0fa";
}
.fa-fighter-jet:before {
  content: "\f0fb";
}
.fa-beer:before {
  content: "\f0fc";
}
.fa-h-square:before {
  content: "\f0fd";
}
.fa-plus-square:before {
  content: "\f0fe";
}
.fa-angle-double-left:before {
  content: "\f100";
}
.fa-angle-double-right:before {
  content: "\f101";
}
.fa-angle-double-up:before {
  content: "\f102";
}
.fa-angle-double-down:before {
  content: "\f103";
}
.fa-angle-left:before {
  content: "\f104";
}
.fa-angle-right:before {
  content: "\f105";
}
.fa-angle-up:before {
  content: "\f106";
}
.fa-angle-down:before {
  content: "\f107";
}
.fa-desktop:before {
  content: "\f108";
}
.fa-laptop:before {
  content: "\f109";
}
.fa-tablet:before {
  content: "\f10a";
}
.fa-mobile-phone:before,
.fa-mobile:before {
  content: "\f10b";
}
.fa-circle-o:before {
  content: "\f10c";
}
.fa-quote-left:before {
  content: "\f10d";
}
.fa-quote-right:before {
  content: "\f10e";
}
.fa-spinner:before {
  content: "\f110";
}
.fa-circle:before {
  content: "\f111";
}
.fa-mail-reply:before,
.fa-reply:before {
  content: "\f112";
}
.fa-github-alt:before {
  content: "\f113";
}
.fa-folder-o:before {
  content: "\f114";
}
.fa-folder-open-o:before {
  content: "\f115";
}
.fa-smile-o:before {
  content: "\f118";
}
.fa-frown-o:before {
  content: "\f119";
}
.fa-meh-o:before {
  content: "\f11a";
}
.fa-gamepad:before {
  content: "\f11b";
}
.fa-keyboard-o:before {
  content: "\f11c";
}
.fa-flag-o:before {
  content: "\f11d";
}
.fa-flag-checkered:before {
  content: "\f11e";
}
.fa-terminal:before {
  content: "\f120";
}
.fa-code:before {
  content: "\f121";
}
.fa-mail-reply-all:before,
.fa-reply-all:before {
  content: "\f122";
}
.fa-star-half-empty:before,
.fa-star-half-full:before,
.fa-star-half-o:before {
  content: "\f123";
}
.fa-location-arrow:before {
  content: "\f124";
}
.fa-crop:before {
  content: "\f125";
}
.fa-code-fork:before {
  content: "\f126";
}
.fa-unlink:before,
.fa-chain-broken:before {
  content: "\f127";
}
.fa-question:before {
  content: "\f128";
}
.fa-info:before {
  content: "\f129";
}
.fa-exclamation:before {
  content: "\f12a";
}
.fa-superscript:before {
  content: "\f12b";
}
.fa-subscript:before {
  content: "\f12c";
}
.fa-eraser:before {
  content: "\f12d";
}
.fa-puzzle-piece:before {
  content: "\f12e";
}
.fa-microphone:before {
  content: "\f130";
}
.fa-microphone-slash:before {
  content: "\f131";
}
.fa-shield:before {
  content: "\f132";
}
.fa-calendar-o:before {
  content: "\f133";
}
.fa-fire-extinguisher:before {
  content: "\f134";
}
.fa-rocket:before {
  content: "\f135";
}
.fa-maxcdn:before {
  content: "\f136";
}
.fa-chevron-circle-left:before {
  content: "\f137";
}
.fa-chevron-circle-right:before {
  content: "\f138";
}
.fa-chevron-circle-up:before {
  content: "\f139";
}
.fa-chevron-circle-down:before {
  content: "\f13a";
}
.fa-html5:before {
  content: "\f13b";
}
.fa-css3:before {
  content: "\f13c";
}
.fa-anchor:before {
  content: "\f13d";
}
.fa-unlock-alt:before {
  content: "\f13e";
}
.fa-bullseye:before {
  content: "\f140";
}
.fa-ellipsis-h:before {
  content: "\f141";
}
.fa-ellipsis-v:before {
  content: "\f142";
}
.fa-rss-square:before {
  content: "\f143";
}
.fa-play-circle:before {
  content: "\f144";
}
.fa-ticket:before {
  content: "\f145";
}
.fa-minus-square:before {
  content: "\f146";
}
.fa-minus-square-o:before {
  content: "\f147";
}
.fa-level-up:before {
  content: "\f148";
}
.fa-level-down:before {
  content: "\f149";
}
.fa-check-square:before {
  content: "\f14a";
}
.fa-pencil-square:before {
  content: "\f14b";
}
.fa-external-link-square:before {
  content: "\f14c";
}
.fa-share-square:before {
  content: "\f14d";
}
.fa-compass:before {
  content: "\f14e";
}
.fa-toggle-down:before,
.fa-caret-square-o-down:before {
  content: "\f150";
}
.fa-toggle-up:before,
.fa-caret-square-o-up:before {
  content: "\f151";
}
.fa-toggle-right:before,
.fa-caret-square-o-right:before {
  content: "\f152";
}
.fa-euro:before,
.fa-eur:before {
  content: "\f153";
}
.fa-gbp:before {
  content: "\f154";
}
.fa-dollar:before,
.fa-usd:before {
  content: "\f155";
}
.fa-rupee:before,
.fa-inr:before {
  content: "\f156";
}
.fa-cny:before,
.fa-rmb:before,
.fa-yen:before,
.fa-jpy:before {
  content: "\f157";
}
.fa-ruble:before,
.fa-rouble:before,
.fa-rub:before {
  content: "\f158";
}
.fa-won:before,
.fa-krw:before {
  content: "\f159";
}
.fa-bitcoin:before,
.fa-btc:before {
  content: "\f15a";
}
.fa-file:before {
  content: "\f15b";
}
.fa-file-text:before {
  content: "\f15c";
}
.fa-sort-alpha-asc:before {
  content: "\f15d";
}
.fa-sort-alpha-desc:before {
  content: "\f15e";
}
.fa-sort-amount-asc:before {
  content: "\f160";
}
.fa-sort-amount-desc:before {
  content: "\f161";
}
.fa-sort-numeric-asc:before {
  content: "\f162";
}
.fa-sort-numeric-desc:before {
  content: "\f163";
}
.fa-thumbs-up:before {
  content: "\f164";
}
.fa-thumbs-down:before {
  content: "\f165";
}
.fa-youtube-square:before {
  content: "\f166";
}
.fa-youtube:before {
  content: "\f167";
}
.fa-xing:before {
  content: "\f168";
}
.fa-xing-square:before {
  content: "\f169";
}
.fa-youtube-play:before {
  content: "\f16a";
}
.fa-dropbox:before {
  content: "\f16b";
}
.fa-stack-overflow:before {
  content: "\f16c";
}
.fa-instagram:before {
  content: "\f16d";
}
.fa-flickr:before {
  content: "\f16e";
}
.fa-adn:before {
  content: "\f170";
}
.fa-bitbucket:before {
  content: "\f171";
}
.fa-bitbucket-square:before {
  content: "\f172";
}
.fa-tumblr:before {
  content: "\f173";
}
.fa-tumblr-square:before {
  content: "\f174";
}
.fa-long-arrow-down:before {
  content: "\f175";
}
.fa-long-arrow-up:before {
  content: "\f176";
}
.fa-long-arrow-left:before {
  content: "\f177";
}
.fa-long-arrow-right:before {
  content: "\f178";
}
.fa-apple:before {
  content: "\f179";
}
.fa-windows:before {
  content: "\f17a";
}
.fa-android:before {
  content: "\f17b";
}
.fa-linux:before {
  content: "\f17c";
}
.fa-dribbble:before {
  content: "\f17d";
}
.fa-skype:before {
  content: "\f17e";
}
.fa-foursquare:before {
  content: "\f180";
}
.fa-trello:before {
  content: "\f181";
}
.fa-female:before {
  content: "\f182";
}
.fa-male:before {
  content: "\f183";
}
.fa-gittip:before {
  content: "\f184";
}
.fa-sun-o:before {
  content: "\f185";
}
.fa-moon-o:before {
  content: "\f186";
}
.fa-archive:before {
  content: "\f187";
}
.fa-bug:before {
  content: "\f188";
}
.fa-vk:before {
  content: "\f189";
}
.fa-weibo:before {
  content: "\f18a";
}
.fa-renren:before {
  content: "\f18b";
}
.fa-pagelines:before {
  content: "\f18c";
}
.fa-stack-exchange:before {
  content: "\f18d";
}
.fa-arrow-circle-o-right:before {
  content: "\f18e";
}
.fa-arrow-circle-o-left:before {
  content: "\f190";
}
.fa-toggle-left:before,
.fa-caret-square-o-left:before {
  content: "\f191";
}
.fa-dot-circle-o:before {
  content: "\f192";
}
.fa-wheelchair:before {
  content: "\f193";
}
.fa-vimeo-square:before {
  content: "\f194";
}
.fa-turkish-lira:before,
.fa-try:before {
  content: "\f195";
}
.fa-plus-square-o:before {
  content: "\f196";
}
.fa-space-shuttle:before {
  content: "\f197";
}
.fa-slack:before {
  content: "\f198";
}
.fa-envelope-square:before {
  content: "\f199";
}
.fa-wordpress:before {
  content: "\f19a";
}
.fa-openid:before {
  content: "\f19b";
}
.fa-institution:before,
.fa-bank:before,
.fa-university:before {
  content: "\f19c";
}
.fa-mortar-board:before,
.fa-graduation-cap:before {
  content: "\f19d";
}
.fa-yahoo:before {
  content: "\f19e";
}
.fa-google:before {
  content: "\f1a0";
}
.fa-reddit:before {
  content: "\f1a1";
}
.fa-reddit-square:before {
  content: "\f1a2";
}
.fa-stumbleupon-circle:before {
  content: "\f1a3";
}
.fa-stumbleupon:before {
  content: "\f1a4";
}
.fa-delicious:before {
  content: "\f1a5";
}
.fa-digg:before {
  content: "\f1a6";
}
.fa-pied-piper:before {
  content: "\f1a7";
}
.fa-pied-piper-alt:before {
  content: "\f1a8";
}
.fa-drupal:before {
  content: "\f1a9";
}
.fa-joomla:before {
  content: "\f1aa";
}
.fa-language:before {
  content: "\f1ab";
}
.fa-fax:before {
  content: "\f1ac";
}
.fa-building:before {
  content: "\f1ad";
}
.fa-child:before {
  content: "\f1ae";
}
.fa-paw:before {
  content: "\f1b0";
}
.fa-spoon:before {
  content: "\f1b1";
}
.fa-cube:before {
  content: "\f1b2";
}
.fa-cubes:before {
  content: "\f1b3";
}
.fa-behance:before {
  content: "\f1b4";
}
.fa-behance-square:before {
  content: "\f1b5";
}
.fa-steam:before {
  content: "\f1b6";
}
.fa-steam-square:before {
  content: "\f1b7";
}
.fa-recycle:before {
  content: "\f1b8";
}
.fa-automobile:before,
.fa-car:before {
  content: "\f1b9";
}
.fa-cab:before,
.fa-taxi:before {
  content: "\f1ba";
}
.fa-tree:before {
  content: "\f1bb";
}
.fa-spotify:before {
  content: "\f1bc";
}
.fa-deviantart:before {
  content: "\f1bd";
}
.fa-soundcloud:before {
  content: "\f1be";
}
.fa-database:before {
  content: "\f1c0";
}
.fa-file-pdf-o:before {
  content: "\f1c1";
}
.fa-file-word-o:before {
  content: "\f1c2";
}
.fa-file-excel-o:before {
  content: "\f1c3";
}
.fa-file-powerpoint-o:before {
  content: "\f1c4";
}
.fa-file-photo-o:before,
.fa-file-picture-o:before,
.fa-file-image-o:before {
  content: "\f1c5";
}
.fa-file-zip-o:before,
.fa-file-archive-o:before {
  content: "\f1c6";
}
.fa-file-sound-o:before,
.fa-file-audio-o:before {
  content: "\f1c7";
}
.fa-file-movie-o:before,
.fa-file-video-o:before {
  content: "\f1c8";
}
.fa-file-code-o:before {
  content: "\f1c9";
}
.fa-vine:before {
  content: "\f1ca";
}
.fa-codepen:before {
  content: "\f1cb";
}
.fa-jsfiddle:before {
  content: "\f1cc";
}
.fa-life-bouy:before,
.fa-life-buoy:before,
.fa-life-saver:before,
.fa-support:before,
.fa-life-ring:before {
  content: "\f1cd";
}
.fa-circle-o-notch:before {
  content: "\f1ce";
}
.fa-ra:before,
.fa-rebel:before {
  content: "\f1d0";
}
.fa-ge:before,
.fa-empire:before {
  content: "\f1d1";
}
.fa-git-square:before {
  content: "\f1d2";
}
.fa-git:before {
  content: "\f1d3";
}
.fa-hacker-news:before {
  content: "\f1d4";
}
.fa-tencent-weibo:before {
  content: "\f1d5";
}
.fa-qq:before {
  content: "\f1d6";
}
.fa-wechat:before,
.fa-weixin:before {
  content: "\f1d7";
}
.fa-send:before,
.fa-paper-plane:before {
  content: "\f1d8";
}
.fa-send-o:before,
.fa-paper-plane-o:before {
  content: "\f1d9";
}
.fa-history:before {
  content: "\f1da";
}
.fa-circle-thin:before {
  content: "\f1db";
}
.fa-header:before {
  content: "\f1dc";
}
.fa-paragraph:before {
  content: "\f1dd";
}
.fa-sliders:before {
  content: "\f1de";
}
.fa-share-alt:before {
  content: "\f1e0";
}
.fa-share-alt-square:before {
  content: "\f1e1";
}
.fa-bomb:before {
  content: "\f1e2";
}
.fa-soccer-ball-o:before,
.fa-futbol-o:before {
  content: "\f1e3";
}
.fa-tty:before {
  content: "\f1e4";
}
.fa-binoculars:before {
  content: "\f1e5";
}
.fa-plug:before {
  content: "\f1e6";
}
.fa-slideshare:before {
  content: "\f1e7";
}
.fa-twitch:before {
  content: "\f1e8";
}
.fa-yelp:before {
  content: "\f1e9";
}
.fa-newspaper-o:before {
  content: "\f1ea";
}
.fa-wifi:before {
  content: "\f1eb";
}
.fa-calculator:before {
  content: "\f1ec";
}
.fa-paypal:before {
  content: "\f1ed";
}
.fa-google-wallet:before {
  content: "\f1ee";
}
.fa-cc-visa:before {
  content: "\f1f0";
}
.fa-cc-mastercard:before {
  content: "\f1f1";
}
.fa-cc-discover:before {
  content: "\f1f2";
}
.fa-cc-amex:before {
  content: "\f1f3";
}
.fa-cc-paypal:before {
  content: "\f1f4";
}
.fa-cc-stripe:before {
  content: "\f1f5";
}
.fa-bell-slash:before {
  content: "\f1f6";
}
.fa-bell-slash-o:before {
  content: "\f1f7";
}
.fa-trash:before {
  content: "\f1f8";
}
.fa-copyright:before {
  content: "\f1f9";
}
.fa-at:before {
  content: "\f1fa";
}
.fa-eyedropper:before {
  content: "\f1fb";
}
.fa-paint-brush:before {
  content: "\f1fc";
}
.fa-birthday-cake:before {
  content: "\f1fd";
}
.fa-area-chart:before {
  content: "\f1fe";
}
.fa-pie-chart:before {
  content: "\f200";
}
.fa-line-chart:before {
  content: "\f201";
}
.fa-lastfm:before {
  content: "\f202";
}
.fa-lastfm-square:before {
  content: "\f203";
}
.fa-toggle-off:before {
  content: "\f204";
}
.fa-toggle-on:before {
  content: "\f205";
}
.fa-bicycle:before {
  content: "\f206";
}
.fa-bus:before {
  content: "\f207";
}
.fa-ioxhost:before {
  content: "\f208";
}
.fa-angellist:before {
  content: "\f209";
}
.fa-cc:before {
  content: "\f20a";
}
.fa-shekel:before,
.fa-sheqel:before,
.fa-ils:before {
  content: "\f20b";
}
.fa-meanpath:before {
  content: "\f20c";
}
/*!
*
* IPython base
*
*/
.modal.fade .modal-dialog {
  -webkit-transform: translate(0, 0);
  -ms-transform: translate(0, 0);
  -o-transform: translate(0, 0);
  transform: translate(0, 0);
}
code {
  color: #000;
}
pre {
  font-size: inherit;
  line-height: inherit;
}
label {
  font-weight: normal;
}
/* Make the page background atleast 100% the height of the view port */
/* Make the page itself atleast 70% the height of the view port */
.border-box-sizing {
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
.corner-all {
  border-radius: 2px;
}
.no-padding {
  padding: 0px;
}
/* Flexible box model classes */
/* Taken from Alex Russell http://infrequently.org/2009/08/css-3-progress/ */
/* This file is a compatability layer.  It allows the usage of flexible box 
model layouts accross multiple browsers, including older browsers.  The newest,
universal implementation of the flexible box model is used when available (see
`Modern browsers` comments below).  Browsers that are known to implement this 
new spec completely include:

    Firefox 28.0+
    Chrome 29.0+
    Internet Explorer 11+ 
    Opera 17.0+

Browsers not listed, including Safari, are supported via the styling under the
`Old browsers` comments below.
*/
.hbox {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
.hbox > * {
  /* Old browsers */
  -webkit-box-flex: 0;
  -moz-box-flex: 0;
  box-flex: 0;
  /* Modern browsers */
  flex: none;
}
.vbox {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
}
.vbox > * {
  /* Old browsers */
  -webkit-box-flex: 0;
  -moz-box-flex: 0;
  box-flex: 0;
  /* Modern browsers */
  flex: none;
}
.hbox.reverse,
.vbox.reverse,
.reverse {
  /* Old browsers */
  -webkit-box-direction: reverse;
  -moz-box-direction: reverse;
  box-direction: reverse;
  /* Modern browsers */
  flex-direction: row-reverse;
}
.hbox.box-flex0,
.vbox.box-flex0,
.box-flex0 {
  /* Old browsers */
  -webkit-box-flex: 0;
  -moz-box-flex: 0;
  box-flex: 0;
  /* Modern browsers */
  flex: none;
  width: auto;
}
.hbox.box-flex1,
.vbox.box-flex1,
.box-flex1 {
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
}
.hbox.box-flex,
.vbox.box-flex,
.box-flex {
  /* Old browsers */
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
}
.hbox.box-flex2,
.vbox.box-flex2,
.box-flex2 {
  /* Old browsers */
  -webkit-box-flex: 2;
  -moz-box-flex: 2;
  box-flex: 2;
  /* Modern browsers */
  flex: 2;
}
.box-group1 {
  /*  Deprecated */
  -webkit-box-flex-group: 1;
  -moz-box-flex-group: 1;
  box-flex-group: 1;
}
.box-group2 {
  /* Deprecated */
  -webkit-box-flex-group: 2;
  -moz-box-flex-group: 2;
  box-flex-group: 2;
}
.hbox.start,
.vbox.start,
.start {
  /* Old browsers */
  -webkit-box-pack: start;
  -moz-box-pack: start;
  box-pack: start;
  /* Modern browsers */
  justify-content: flex-start;
}
.hbox.end,
.vbox.end,
.end {
  /* Old browsers */
  -webkit-box-pack: end;
  -moz-box-pack: end;
  box-pack: end;
  /* Modern browsers */
  justify-content: flex-end;
}
.hbox.center,
.vbox.center,
.center {
  /* Old browsers */
  -webkit-box-pack: center;
  -moz-box-pack: center;
  box-pack: center;
  /* Modern browsers */
  justify-content: center;
}
.hbox.baseline,
.vbox.baseline,
.baseline {
  /* Old browsers */
  -webkit-box-pack: baseline;
  -moz-box-pack: baseline;
  box-pack: baseline;
  /* Modern browsers */
  justify-content: baseline;
}
.hbox.stretch,
.vbox.stretch,
.stretch {
  /* Old browsers */
  -webkit-box-pack: stretch;
  -moz-box-pack: stretch;
  box-pack: stretch;
  /* Modern browsers */
  justify-content: stretch;
}
.hbox.align-start,
.vbox.align-start,
.align-start {
  /* Old browsers */
  -webkit-box-align: start;
  -moz-box-align: start;
  box-align: start;
  /* Modern browsers */
  align-items: flex-start;
}
.hbox.align-end,
.vbox.align-end,
.align-end {
  /* Old browsers */
  -webkit-box-align: end;
  -moz-box-align: end;
  box-align: end;
  /* Modern browsers */
  align-items: flex-end;
}
.hbox.align-center,
.vbox.align-center,
.align-center {
  /* Old browsers */
  -webkit-box-align: center;
  -moz-box-align: center;
  box-align: center;
  /* Modern browsers */
  align-items: center;
}
.hbox.align-baseline,
.vbox.align-baseline,
.align-baseline {
  /* Old browsers */
  -webkit-box-align: baseline;
  -moz-box-align: baseline;
  box-align: baseline;
  /* Modern browsers */
  align-items: baseline;
}
.hbox.align-stretch,
.vbox.align-stretch,
.align-stretch {
  /* Old browsers */
  -webkit-box-align: stretch;
  -moz-box-align: stretch;
  box-align: stretch;
  /* Modern browsers */
  align-items: stretch;
}
div.error {
  margin: 2em;
  text-align: center;
}
div.error > h1 {
  font-size: 500%;
  line-height: normal;
}
div.error > p {
  font-size: 200%;
  line-height: normal;
}
div.traceback-wrapper {
  text-align: left;
  max-width: 800px;
  margin: auto;
}
/**
 * Primary styles
 *
 * Author: Jupyter Development Team
 */
body {
  background-color: #fff;
  /* This makes sure that the body covers the entire window and needs to
       be in a different element than the display: box in wrapper below */
  position: absolute;
  left: 0px;
  right: 0px;
  top: 0px;
  bottom: 0px;
  overflow: visible;
}
body > #header {
  /* Initially hidden to prevent FLOUC */
  display: none;
  background-color: #fff;
  /* Display over codemirror */
  position: relative;
  z-index: 100;
}
body > #header #header-container {
  padding-bottom: 5px;
  padding-top: 5px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
body > #header .header-bar {
  width: 100%;
  height: 1px;
  background: #e7e7e7;
  margin-bottom: -1px;
}
@media print {
  body > #header {
    display: none !important;
  }
}
#header-spacer {
  width: 100%;
  visibility: hidden;
}
@media print {
  #header-spacer {
    display: none;
  }
}
#ipython_notebook {
  padding-left: 0px;
  padding-top: 1px;
  padding-bottom: 1px;
}
@media (max-width: 991px) {
  #ipython_notebook {
    margin-left: 10px;
  }
}
[dir="rtl"] #ipython_notebook {
  float: right !important;
}
#noscript {
  width: auto;
  padding-top: 16px;
  padding-bottom: 16px;
  text-align: center;
  font-size: 22px;
  color: red;
  font-weight: bold;
}
#ipython_notebook img {
  height: 28px;
}
#site {
  width: 100%;
  display: none;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  overflow: auto;
}
@media print {
  #site {
    height: auto !important;
  }
}
/* Smaller buttons */
.ui-button .ui-button-text {
  padding: 0.2em 0.8em;
  font-size: 77%;
}
input.ui-button {
  padding: 0.3em 0.9em;
}
span#login_widget {
  float: right;
}
span#login_widget > .button,
#logout {
  color: #333;
  background-color: #fff;
  border-color: #ccc;
}
span#login_widget > .button:focus,
#logout:focus,
span#login_widget > .button.focus,
#logout.focus {
  color: #333;
  background-color: #e6e6e6;
  border-color: #8c8c8c;
}
span#login_widget > .button:hover,
#logout:hover {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
span#login_widget > .button:active,
#logout:active,
span#login_widget > .button.active,
#logout.active,
.open > .dropdown-togglespan#login_widget > .button,
.open > .dropdown-toggle#logout {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
span#login_widget > .button:active:hover,
#logout:active:hover,
span#login_widget > .button.active:hover,
#logout.active:hover,
.open > .dropdown-togglespan#login_widget > .button:hover,
.open > .dropdown-toggle#logout:hover,
span#login_widget > .button:active:focus,
#logout:active:focus,
span#login_widget > .button.active:focus,
#logout.active:focus,
.open > .dropdown-togglespan#login_widget > .button:focus,
.open > .dropdown-toggle#logout:focus,
span#login_widget > .button:active.focus,
#logout:active.focus,
span#login_widget > .button.active.focus,
#logout.active.focus,
.open > .dropdown-togglespan#login_widget > .button.focus,
.open > .dropdown-toggle#logout.focus {
  color: #333;
  background-color: #d4d4d4;
  border-color: #8c8c8c;
}
span#login_widget > .button:active,
#logout:active,
span#login_widget > .button.active,
#logout.active,
.open > .dropdown-togglespan#login_widget > .button,
.open > .dropdown-toggle#logout {
  background-image: none;
}
span#login_widget > .button.disabled:hover,
#logout.disabled:hover,
span#login_widget > .button[disabled]:hover,
#logout[disabled]:hover,
fieldset[disabled] span#login_widget > .button:hover,
fieldset[disabled] #logout:hover,
span#login_widget > .button.disabled:focus,
#logout.disabled:focus,
span#login_widget > .button[disabled]:focus,
#logout[disabled]:focus,
fieldset[disabled] span#login_widget > .button:focus,
fieldset[disabled] #logout:focus,
span#login_widget > .button.disabled.focus,
#logout.disabled.focus,
span#login_widget > .button[disabled].focus,
#logout[disabled].focus,
fieldset[disabled] span#login_widget > .button.focus,
fieldset[disabled] #logout.focus {
  background-color: #fff;
  border-color: #ccc;
}
span#login_widget > .button .badge,
#logout .badge {
  color: #fff;
  background-color: #333;
}
.nav-header {
  text-transform: none;
}
#header > span {
  margin-top: 10px;
}
.modal_stretch .modal-dialog {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
  min-height: 80vh;
}
.modal_stretch .modal-dialog .modal-body {
  max-height: calc(100vh - 200px);
  overflow: auto;
  flex: 1;
}
@media (min-width: 768px) {
  .modal .modal-dialog {
    width: 700px;
  }
}
@media (min-width: 768px) {
  select.form-control {
    margin-left: 12px;
    margin-right: 12px;
  }
}
/*!
*
* IPython auth
*
*/
.center-nav {
  display: inline-block;
  margin-bottom: -4px;
}
/*!
*
* IPython tree view
*
*/
/* We need an invisible input field on top of the sentense*/
/* "Drag file onto the list ..." */
.alternate_upload {
  background-color: none;
  display: inline;
}
.alternate_upload.form {
  padding: 0;
  margin: 0;
}
.alternate_upload input.fileinput {
  text-align: center;
  vertical-align: middle;
  display: inline;
  opacity: 0;
  z-index: 2;
  width: 12ex;
  margin-right: -12ex;
}
.alternate_upload .btn-upload {
  height: 22px;
}
/**
 * Primary styles
 *
 * Author: Jupyter Development Team
 */
[dir="rtl"] #tabs li {
  float: right;
}
ul#tabs {
  margin-bottom: 4px;
}
[dir="rtl"] ul#tabs {
  margin-right: 0px;
}
ul#tabs a {
  padding-top: 6px;
  padding-bottom: 4px;
}
ul.breadcrumb a:focus,
ul.breadcrumb a:hover {
  text-decoration: none;
}
ul.breadcrumb i.icon-home {
  font-size: 16px;
  margin-right: 4px;
}
ul.breadcrumb span {
  color: #5e5e5e;
}
.list_toolbar {
  padding: 4px 0 4px 0;
  vertical-align: middle;
}
.list_toolbar .tree-buttons {
  padding-top: 1px;
}
[dir="rtl"] .list_toolbar .tree-buttons {
  float: left !important;
}
[dir="rtl"] .list_toolbar .pull-right {
  padding-top: 1px;
  float: left !important;
}
[dir="rtl"] .list_toolbar .pull-left {
  float: right !important;
}
.dynamic-buttons {
  padding-top: 3px;
  display: inline-block;
}
.list_toolbar [class*="span"] {
  min-height: 24px;
}
.list_header {
  font-weight: bold;
  background-color: #EEE;
}
.list_placeholder {
  font-weight: bold;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 7px;
  padding-right: 7px;
}
.list_container {
  margin-top: 4px;
  margin-bottom: 20px;
  border: 1px solid #ddd;
  border-radius: 2px;
}
.list_container > div {
  border-bottom: 1px solid #ddd;
}
.list_container > div:hover .list-item {
  background-color: red;
}
.list_container > div:last-child {
  border: none;
}
.list_item:hover .list_item {
  background-color: #ddd;
}
.list_item a {
  text-decoration: none;
}
.list_item:hover {
  background-color: #fafafa;
}
.list_header > div,
.list_item > div {
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 7px;
  padding-right: 7px;
  line-height: 22px;
}
.list_header > div input,
.list_item > div input {
  margin-right: 7px;
  margin-left: 14px;
  vertical-align: baseline;
  line-height: 22px;
  position: relative;
  top: -1px;
}
.list_header > div .item_link,
.list_item > div .item_link {
  margin-left: -1px;
  vertical-align: baseline;
  line-height: 22px;
}
.new-file input[type=checkbox] {
  visibility: hidden;
}
.item_name {
  line-height: 22px;
  height: 24px;
}
.item_icon {
  font-size: 14px;
  color: #5e5e5e;
  margin-right: 7px;
  margin-left: 7px;
  line-height: 22px;
  vertical-align: baseline;
}
.item_buttons {
  line-height: 1em;
  margin-left: -5px;
}
.item_buttons .btn,
.item_buttons .btn-group,
.item_buttons .input-group {
  float: left;
}
.item_buttons > .btn,
.item_buttons > .btn-group,
.item_buttons > .input-group {
  margin-left: 5px;
}
.item_buttons .btn {
  min-width: 13ex;
}
.item_buttons .running-indicator {
  padding-top: 4px;
  color: #5cb85c;
}
.item_buttons .kernel-name {
  padding-top: 4px;
  color: #5bc0de;
  margin-right: 7px;
  float: left;
}
.toolbar_info {
  height: 24px;
  line-height: 24px;
}
.list_item input:not([type=checkbox]) {
  padding-top: 3px;
  padding-bottom: 3px;
  height: 22px;
  line-height: 14px;
  margin: 0px;
}
.highlight_text {
  color: blue;
}
#project_name {
  display: inline-block;
  padding-left: 7px;
  margin-left: -2px;
}
#project_name > .breadcrumb {
  padding: 0px;
  margin-bottom: 0px;
  background-color: transparent;
  font-weight: bold;
}
#tree-selector {
  padding-right: 0px;
}
[dir="rtl"] #tree-selector a {
  float: right;
}
#button-select-all {
  min-width: 50px;
}
#select-all {
  margin-left: 7px;
  margin-right: 2px;
}
.menu_icon {
  margin-right: 2px;
}
.tab-content .row {
  margin-left: 0px;
  margin-right: 0px;
}
.folder_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f114";
}
.folder_icon:before.pull-left {
  margin-right: .3em;
}
.folder_icon:before.pull-right {
  margin-left: .3em;
}
.notebook_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f02d";
  position: relative;
  top: -1px;
}
.notebook_icon:before.pull-left {
  margin-right: .3em;
}
.notebook_icon:before.pull-right {
  margin-left: .3em;
}
.running_notebook_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f02d";
  position: relative;
  top: -1px;
  color: #5cb85c;
}
.running_notebook_icon:before.pull-left {
  margin-right: .3em;
}
.running_notebook_icon:before.pull-right {
  margin-left: .3em;
}
.file_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f016";
  position: relative;
  top: -2px;
}
.file_icon:before.pull-left {
  margin-right: .3em;
}
.file_icon:before.pull-right {
  margin-left: .3em;
}
#notebook_toolbar .pull-right {
  padding-top: 0px;
  margin-right: -1px;
}
ul#new-menu {
  left: auto;
  right: 0;
}
[dir="rtl"] #new-menu {
  text-align: right;
}
.kernel-menu-icon {
  padding-right: 12px;
  width: 24px;
  content: "\f096";
}
.kernel-menu-icon:before {
  content: "\f096";
}
.kernel-menu-icon-current:before {
  content: "\f00c";
}
#tab_content {
  padding-top: 20px;
}
#running .panel-group .panel {
  margin-top: 3px;
  margin-bottom: 1em;
}
#running .panel-group .panel .panel-heading {
  background-color: #EEE;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 7px;
  padding-right: 7px;
  line-height: 22px;
}
#running .panel-group .panel .panel-heading a:focus,
#running .panel-group .panel .panel-heading a:hover {
  text-decoration: none;
}
#running .panel-group .panel .panel-body {
  padding: 0px;
}
#running .panel-group .panel .panel-body .list_container {
  margin-top: 0px;
  margin-bottom: 0px;
  border: 0px;
  border-radius: 0px;
}
#running .panel-group .panel .panel-body .list_container .list_item {
  border-bottom: 1px solid #ddd;
}
#running .panel-group .panel .panel-body .list_container .list_item:last-child {
  border-bottom: 0px;
}
[dir="rtl"] #running .col-sm-8 {
  float: right !important;
}
.delete-button {
  display: none;
}
.duplicate-button {
  display: none;
}
.rename-button {
  display: none;
}
.shutdown-button {
  display: none;
}
.dynamic-instructions {
  display: inline-block;
  padding-top: 4px;
}
/*!
*
* IPython text editor webapp
*
*/
.selected-keymap i.fa {
  padding: 0px 5px;
}
.selected-keymap i.fa:before {
  content: "\f00c";
}
#mode-menu {
  overflow: auto;
  max-height: 20em;
}
.edit_app #header {
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
}
.edit_app #menubar .navbar {
  /* Use a negative 1 bottom margin, so the border overlaps the border of the
    header */
  margin-bottom: -1px;
}
.dirty-indicator {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 20px;
}
.dirty-indicator.pull-left {
  margin-right: .3em;
}
.dirty-indicator.pull-right {
  margin-left: .3em;
}
.dirty-indicator-dirty {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 20px;
}
.dirty-indicator-dirty.pull-left {
  margin-right: .3em;
}
.dirty-indicator-dirty.pull-right {
  margin-left: .3em;
}
.dirty-indicator-clean {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 20px;
}
.dirty-indicator-clean.pull-left {
  margin-right: .3em;
}
.dirty-indicator-clean.pull-right {
  margin-left: .3em;
}
.dirty-indicator-clean:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f00c";
}
.dirty-indicator-clean:before.pull-left {
  margin-right: .3em;
}
.dirty-indicator-clean:before.pull-right {
  margin-left: .3em;
}
#filename {
  font-size: 16pt;
  display: table;
  padding: 0px 5px;
}
#current-mode {
  padding-left: 5px;
  padding-right: 5px;
}
#texteditor-backdrop {
  padding-top: 20px;
  padding-bottom: 20px;
}
@media not print {
  #texteditor-backdrop {
    background-color: #EEE;
  }
}
@media print {
  #texteditor-backdrop #texteditor-container .CodeMirror-gutter,
  #texteditor-backdrop #texteditor-container .CodeMirror-gutters {
    background-color: #fff;
  }
}
@media not print {
  #texteditor-backdrop #texteditor-container .CodeMirror-gutter,
  #texteditor-backdrop #texteditor-container .CodeMirror-gutters {
    background-color: #fff;
  }
}
@media not print {
  #texteditor-backdrop #texteditor-container {
    padding: 0px;
    background-color: #fff;
    -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
    box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  }
}
/*!
*
* IPython notebook
*
*/
/* CSS font colors for translated ANSI colors. */
.ansibold {
  font-weight: bold;
}
/* use dark versions for foreground, to improve visibility */
.ansiblack {
  color: black;
}
.ansired {
  color: darkred;
}
.ansigreen {
  color: darkgreen;
}
.ansiyellow {
  color: #c4a000;
}
.ansiblue {
  color: darkblue;
}
.ansipurple {
  color: darkviolet;
}
.ansicyan {
  color: steelblue;
}
.ansigray {
  color: gray;
}
/* and light for background, for the same reason */
.ansibgblack {
  background-color: black;
}
.ansibgred {
  background-color: red;
}
.ansibggreen {
  background-color: green;
}
.ansibgyellow {
  background-color: yellow;
}
.ansibgblue {
  background-color: blue;
}
.ansibgpurple {
  background-color: magenta;
}
.ansibgcyan {
  background-color: cyan;
}
.ansibggray {
  background-color: gray;
}
div.cell {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
  border-radius: 2px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  border-width: 1px;
  border-style: solid;
  border-color: transparent;
  width: 100%;
  padding: 5px;
  /* This acts as a spacer between cells, that is outside the border */
  margin: 0px;
  outline: none;
  border-left-width: 1px;
  padding-left: 5px;
  background: linear-gradient(to right, transparent -40px, transparent 1px, transparent 1px, transparent 100%);
}
div.cell.jupyter-soft-selected {
  border-left-color: #90CAF9;
  border-left-color: #E3F2FD;
  border-left-width: 1px;
  padding-left: 5px;
  border-right-color: #E3F2FD;
  border-right-width: 1px;
  background: #E3F2FD;
}
@media print {
  div.cell.jupyter-soft-selected {
    border-color: transparent;
  }
}
div.cell.selected {
  border-color: #ababab;
  border-left-width: 0px;
  padding-left: 6px;
  background: linear-gradient(to right, #42A5F5 -40px, #42A5F5 5px, transparent 5px, transparent 100%);
}
@media print {
  div.cell.selected {
    border-color: transparent;
  }
}
div.cell.selected.jupyter-soft-selected {
  border-left-width: 0;
  padding-left: 6px;
  background: linear-gradient(to right, #42A5F5 -40px, #42A5F5 7px, #E3F2FD 7px, #E3F2FD 100%);
}
.edit_mode div.cell.selected {
  border-color: #66BB6A;
  border-left-width: 0px;
  padding-left: 6px;
  background: linear-gradient(to right, #66BB6A -40px, #66BB6A 5px, transparent 5px, transparent 100%);
}
@media print {
  .edit_mode div.cell.selected {
    border-color: transparent;
  }
}
.prompt {
  /* This needs to be wide enough for 3 digit prompt numbers: In[100]: */
  min-width: 14ex;
  /* This padding is tuned to match the padding on the CodeMirror editor. */
  padding: 0.4em;
  margin: 0px;
  font-family: monospace;
  text-align: right;
  /* This has to match that of the the CodeMirror class line-height below */
  line-height: 1.21429em;
  /* Don't highlight prompt number selection */
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  /* Use default cursor */
  cursor: default;
}
@media (max-width: 540px) {
  .prompt {
    text-align: left;
  }
}
div.inner_cell {
  min-width: 0;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
}
/* input_area and input_prompt must match in top border and margin for alignment */
div.input_area {
  border: 1px solid #cfcfcf;
  border-radius: 2px;
  background: #f7f7f7;
  line-height: 1.21429em;
}
/* This is needed so that empty prompt areas can collapse to zero height when there
   is no content in the output_subarea and the prompt. The main purpose of this is
   to make sure that empty JavaScript output_subareas have no height. */
div.prompt:empty {
  padding-top: 0;
  padding-bottom: 0;
}
div.unrecognized_cell {
  padding: 5px 5px 5px 0px;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
div.unrecognized_cell .inner_cell {
  border-radius: 2px;
  padding: 5px;
  font-weight: bold;
  color: red;
  border: 1px solid #cfcfcf;
  background: #eaeaea;
}
div.unrecognized_cell .inner_cell a {
  color: inherit;
  text-decoration: none;
}
div.unrecognized_cell .inner_cell a:hover {
  color: inherit;
  text-decoration: none;
}
@media (max-width: 540px) {
  div.unrecognized_cell > div.prompt {
    display: none;
  }
}
div.code_cell {
  /* avoid page breaking on code cells when printing */
}
@media print {
  div.code_cell {
    page-break-inside: avoid;
  }
}
/* any special styling for code cells that are currently running goes here */
div.input {
  page-break-inside: avoid;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
@media (max-width: 540px) {
  div.input {
    /* Old browsers */
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-box-align: stretch;
    display: -moz-box;
    -moz-box-orient: vertical;
    -moz-box-align: stretch;
    display: box;
    box-orient: vertical;
    box-align: stretch;
    /* Modern browsers */
    display: flex;
    flex-direction: column;
    align-items: stretch;
  }
}
/* input_area and input_prompt must match in top border and margin for alignment */
div.input_prompt {
  color: #303F9F;
  border-top: 1px solid transparent;
}
div.input_area > div.highlight {
  margin: 0.4em;
  border: none;
  padding: 0px;
  background-color: transparent;
}
div.input_area > div.highlight > pre {
  margin: 0px;
  border: none;
  padding: 0px;
  background-color: transparent;
}
/* The following gets added to the <head> if it is detected that the user has a
 * monospace font with inconsistent normal/bold/italic height.  See
 * notebookmain.js.  Such fonts will have keywords vertically offset with
 * respect to the rest of the text.  The user should select a better font.
 * See: https://github.com/ipython/ipython/issues/1503
 *
 * .CodeMirror span {
 *      vertical-align: bottom;
 * }
 */
.CodeMirror {
  line-height: 1.21429em;
  /* Changed from 1em to our global default */
  font-size: 14px;
  height: auto;
  /* Changed to auto to autogrow */
  background: none;
  /* Changed from white to allow our bg to show through */
}
.CodeMirror-scroll {
  /*  The CodeMirror docs are a bit fuzzy on if overflow-y should be hidden or visible.*/
  /*  We have found that if it is visible, vertical scrollbars appear with font size changes.*/
  overflow-y: hidden;
  overflow-x: auto;
}
.CodeMirror-lines {
  /* In CM2, this used to be 0.4em, but in CM3 it went to 4px. We need the em value because */
  /* we have set a different line-height and want this to scale with that. */
  padding: 0.4em;
}
.CodeMirror-linenumber {
  padding: 0 8px 0 4px;
}
.CodeMirror-gutters {
  border-bottom-left-radius: 2px;
  border-top-left-radius: 2px;
}
.CodeMirror pre {
  /* In CM3 this went to 4px from 0 in CM2. We need the 0 value because of how we size */
  /* .CodeMirror-lines */
  padding: 0;
  border: 0;
  border-radius: 0;
}
/*

Original style from softwaremaniacs.org (c) Ivan Sagalaev <Maniac@SoftwareManiacs.Org>
Adapted from GitHub theme

*/
.highlight-base {
  color: #000;
}
.highlight-variable {
  color: #000;
}
.highlight-variable-2 {
  color: #1a1a1a;
}
.highlight-variable-3 {
  color: #333333;
}
.highlight-string {
  color: #BA2121;
}
.highlight-comment {
  color: #408080;
  font-style: italic;
}
.highlight-number {
  color: #080;
}
.highlight-atom {
  color: #88F;
}
.highlight-keyword {
  color: #008000;
  font-weight: bold;
}
.highlight-builtin {
  color: #008000;
}
.highlight-error {
  color: #f00;
}
.highlight-operator {
  color: #AA22FF;
  font-weight: bold;
}
.highlight-meta {
  color: #AA22FF;
}
/* previously not defined, copying from default codemirror */
.highlight-def {
  color: #00f;
}
.highlight-string-2 {
  color: #f50;
}
.highlight-qualifier {
  color: #555;
}
.highlight-bracket {
  color: #997;
}
.highlight-tag {
  color: #170;
}
.highlight-attribute {
  color: #00c;
}
.highlight-header {
  color: blue;
}
.highlight-quote {
  color: #090;
}
.highlight-link {
  color: #00c;
}
/* apply the same style to codemirror */
.cm-s-ipython span.cm-keyword {
  color: #008000;
  font-weight: bold;
}
.cm-s-ipython span.cm-atom {
  color: #88F;
}
.cm-s-ipython span.cm-number {
  color: #080;
}
.cm-s-ipython span.cm-def {
  color: #00f;
}
.cm-s-ipython span.cm-variable {
  color: #000;
}
.cm-s-ipython span.cm-operator {
  color: #AA22FF;
  font-weight: bold;
}
.cm-s-ipython span.cm-variable-2 {
  color: #1a1a1a;
}
.cm-s-ipython span.cm-variable-3 {
  color: #333333;
}
.cm-s-ipython span.cm-comment {
  color: #408080;
  font-style: italic;
}
.cm-s-ipython span.cm-string {
  color: #BA2121;
}
.cm-s-ipython span.cm-string-2 {
  color: #f50;
}
.cm-s-ipython span.cm-meta {
  color: #AA22FF;
}
.cm-s-ipython span.cm-qualifier {
  color: #555;
}
.cm-s-ipython span.cm-builtin {
  color: #008000;
}
.cm-s-ipython span.cm-bracket {
  color: #997;
}
.cm-s-ipython span.cm-tag {
  color: #170;
}
.cm-s-ipython span.cm-attribute {
  color: #00c;
}
.cm-s-ipython span.cm-header {
  color: blue;
}
.cm-s-ipython span.cm-quote {
  color: #090;
}
.cm-s-ipython span.cm-link {
  color: #00c;
}
.cm-s-ipython span.cm-error {
  color: #f00;
}
.cm-s-ipython span.cm-tab {
  background: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADAAAAAMCAYAAAAkuj5RAAAAAXNSR0IArs4c6QAAAGFJREFUSMft1LsRQFAQheHPowAKoACx3IgEKtaEHujDjORSgWTH/ZOdnZOcM/sgk/kFFWY0qV8foQwS4MKBCS3qR6ixBJvElOobYAtivseIE120FaowJPN75GMu8j/LfMwNjh4HUpwg4LUAAAAASUVORK5CYII=);
  background-position: right;
  background-repeat: no-repeat;
}
div.output_wrapper {
  /* this position must be relative to enable descendents to be absolute within it */
  position: relative;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
  z-index: 1;
}
/* class for the output area when it should be height-limited */
div.output_scroll {
  /* ideally, this would be max-height, but FF barfs all over that */
  height: 24em;
  /* FF needs this *and the wrapper* to specify full width, or it will shrinkwrap */
  width: 100%;
  overflow: auto;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 2px 8px rgba(0, 0, 0, 0.8);
  box-shadow: inset 0 2px 8px rgba(0, 0, 0, 0.8);
  display: block;
}
/* output div while it is collapsed */
div.output_collapsed {
  margin: 0px;
  padding: 0px;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
}
div.out_prompt_overlay {
  height: 100%;
  padding: 0px 0.4em;
  position: absolute;
  border-radius: 2px;
}
div.out_prompt_overlay:hover {
  /* use inner shadow to get border that is computed the same on WebKit/FF */
  -webkit-box-shadow: inset 0 0 1px #000;
  box-shadow: inset 0 0 1px #000;
  background: rgba(240, 240, 240, 0.5);
}
div.output_prompt {
  color: #D84315;
}
/* This class is the outer container of all output sections. */
div.output_area {
  padding: 0px;
  page-break-inside: avoid;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
div.output_area .MathJax_Display {
  text-align: left !important;
}
div.output_area .rendered_html table {
  margin-left: 0;
  margin-right: 0;
}
div.output_area .rendered_html img {
  margin-left: 0;
  margin-right: 0;
}
div.output_area img,
div.output_area svg {
  max-width: 100%;
  height: auto;
}
div.output_area img.unconfined,
div.output_area svg.unconfined {
  max-width: none;
}
/* This is needed to protect the pre formating from global settings such
   as that of bootstrap */
.output {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
}
@media (max-width: 540px) {
  div.output_area {
    /* Old browsers */
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-box-align: stretch;
    display: -moz-box;
    -moz-box-orient: vertical;
    -moz-box-align: stretch;
    display: box;
    box-orient: vertical;
    box-align: stretch;
    /* Modern browsers */
    display: flex;
    flex-direction: column;
    align-items: stretch;
  }
}
div.output_area pre {
  margin: 0;
  padding: 0;
  border: 0;
  vertical-align: baseline;
  color: black;
  background-color: transparent;
  border-radius: 0;
}
/* This class is for the output subarea inside the output_area and after
   the prompt div. */
div.output_subarea {
  overflow-x: auto;
  padding: 0.4em;
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
  max-width: calc(100% - 14ex);
}
div.output_scroll div.output_subarea {
  overflow-x: visible;
}
/* The rest of the output_* classes are for special styling of the different
   output types */
/* all text output has this class: */
div.output_text {
  text-align: left;
  color: #000;
  /* This has to match that of the the CodeMirror class line-height below */
  line-height: 1.21429em;
}
/* stdout/stderr are 'text' as well as 'stream', but execute_result/error are *not* streams */
div.output_stderr {
  background: #fdd;
  /* very light red background for stderr */
}
div.output_latex {
  text-align: left;
}
/* Empty output_javascript divs should have no height */
div.output_javascript:empty {
  padding: 0;
}
.js-error {
  color: darkred;
}
/* raw_input styles */
div.raw_input_container {
  line-height: 1.21429em;
  padding-top: 5px;
}
pre.raw_input_prompt {
  /* nothing needed here. */
}
input.raw_input {
  font-family: monospace;
  font-size: inherit;
  color: inherit;
  width: auto;
  /* make sure input baseline aligns with prompt */
  vertical-align: baseline;
  /* padding + margin = 0.5em between prompt and cursor */
  padding: 0em 0.25em;
  margin: 0em 0.25em;
}
input.raw_input:focus {
  box-shadow: none;
}
p.p-space {
  margin-bottom: 10px;
}
div.output_unrecognized {
  padding: 5px;
  font-weight: bold;
  color: red;
}
div.output_unrecognized a {
  color: inherit;
  text-decoration: none;
}
div.output_unrecognized a:hover {
  color: inherit;
  text-decoration: none;
}
.rendered_html {
  color: #000;
  /* any extras will just be numbers: */
}
.rendered_html em {
  font-style: italic;
}
.rendered_html strong {
  font-weight: bold;
}
.rendered_html u {
  text-decoration: underline;
}
.rendered_html :link {
  text-decoration: underline;
}
.rendered_html :visited {
  text-decoration: underline;
}
.rendered_html h1 {
  font-size: 185.7%;
  margin: 1.08em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
}
.rendered_html h2 {
  font-size: 157.1%;
  margin: 1.27em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
}
.rendered_html h3 {
  font-size: 128.6%;
  margin: 1.55em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
}
.rendered_html h4 {
  font-size: 100%;
  margin: 2em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
}
.rendered_html h5 {
  font-size: 100%;
  margin: 2em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
  font-style: italic;
}
.rendered_html h6 {
  font-size: 100%;
  margin: 2em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
  font-style: italic;
}
.rendered_html h1:first-child {
  margin-top: 0.538em;
}
.rendered_html h2:first-child {
  margin-top: 0.636em;
}
.rendered_html h3:first-child {
  margin-top: 0.777em;
}
.rendered_html h4:first-child {
  margin-top: 1em;
}
.rendered_html h5:first-child {
  margin-top: 1em;
}
.rendered_html h6:first-child {
  margin-top: 1em;
}
.rendered_html ul {
  list-style: disc;
  margin: 0em 2em;
  padding-left: 0px;
}
.rendered_html ul ul {
  list-style: square;
  margin: 0em 2em;
}
.rendered_html ul ul ul {
  list-style: circle;
  margin: 0em 2em;
}
.rendered_html ol {
  list-style: decimal;
  margin: 0em 2em;
  padding-left: 0px;
}
.rendered_html ol ol {
  list-style: upper-alpha;
  margin: 0em 2em;
}
.rendered_html ol ol ol {
  list-style: lower-alpha;
  margin: 0em 2em;
}
.rendered_html ol ol ol ol {
  list-style: lower-roman;
  margin: 0em 2em;
}
.rendered_html ol ol ol ol ol {
  list-style: decimal;
  margin: 0em 2em;
}
.rendered_html * + ul {
  margin-top: 1em;
}
.rendered_html * + ol {
  margin-top: 1em;
}
.rendered_html hr {
  color: black;
  background-color: black;
}
.rendered_html pre {
  margin: 1em 2em;
}
.rendered_html pre,
.rendered_html code {
  border: 0;
  background-color: #fff;
  color: #000;
  font-size: 100%;
  padding: 0px;
}
.rendered_html blockquote {
  margin: 1em 2em;
}
.rendered_html table {
  margin-left: auto;
  margin-right: auto;
  border: 1px solid black;
  border-collapse: collapse;
}
.rendered_html tr,
.rendered_html th,
.rendered_html td {
  border: 1px solid black;
  border-collapse: collapse;
  margin: 1em 2em;
}
.rendered_html td,
.rendered_html th {
  text-align: left;
  vertical-align: middle;
  padding: 4px;
}
.rendered_html th {
  font-weight: bold;
}
.rendered_html * + table {
  margin-top: 1em;
}
.rendered_html p {
  text-align: left;
}
.rendered_html * + p {
  margin-top: 1em;
}
.rendered_html img {
  display: block;
  margin-left: auto;
  margin-right: auto;
}
.rendered_html * + img {
  margin-top: 1em;
}
.rendered_html img,
.rendered_html svg {
  max-width: 100%;
  height: auto;
}
.rendered_html img.unconfined,
.rendered_html svg.unconfined {
  max-width: none;
}
div.text_cell {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
@media (max-width: 540px) {
  div.text_cell > div.prompt {
    display: none;
  }
}
div.text_cell_render {
  /*font-family: "Helvetica Neue", Arial, Helvetica, Geneva, sans-serif;*/
  outline: none;
  resize: none;
  width: inherit;
  border-style: none;
  padding: 0.5em 0.5em 0.5em 0.4em;
  color: #000;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
a.anchor-link:link {
  text-decoration: none;
  padding: 0px 20px;
  visibility: hidden;
}
h1:hover .anchor-link,
h2:hover .anchor-link,
h3:hover .anchor-link,
h4:hover .anchor-link,
h5:hover .anchor-link,
h6:hover .anchor-link {
  visibility: visible;
}
.text_cell.rendered .input_area {
  display: none;
}
.text_cell.rendered .rendered_html {
  overflow-x: auto;
  overflow-y: hidden;
}
.text_cell.unrendered .text_cell_render {
  display: none;
}
.cm-header-1,
.cm-header-2,
.cm-header-3,
.cm-header-4,
.cm-header-5,
.cm-header-6 {
  font-weight: bold;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
}
.cm-header-1 {
  font-size: 185.7%;
}
.cm-header-2 {
  font-size: 157.1%;
}
.cm-header-3 {
  font-size: 128.6%;
}
.cm-header-4 {
  font-size: 110%;
}
.cm-header-5 {
  font-size: 100%;
  font-style: italic;
}
.cm-header-6 {
  font-size: 100%;
  font-style: italic;
}
/*!
*
* IPython notebook webapp
*
*/
@media (max-width: 767px) {
  .notebook_app {
    padding-left: 0px;
    padding-right: 0px;
  }
}
#ipython-main-app {
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  height: 100%;
}
div#notebook_panel {
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  height: 100%;
}
div#notebook {
  font-size: 14px;
  line-height: 20px;
  overflow-y: hidden;
  overflow-x: auto;
  width: 100%;
  /* This spaces the page away from the edge of the notebook area */
  padding-top: 20px;
  margin: 0px;
  outline: none;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  min-height: 100%;
}
@media not print {
  #notebook-container {
    padding: 15px;
    background-color: #fff;
    min-height: 0;
  }
}
@media print {
  #notebook-container {
    width: 100%;
  }
}
div.ui-widget-content {
  border: 1px solid #ababab;
  outline: none;
}
pre.dialog {
  background-color: #f7f7f7;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding: 0.4em;
  padding-left: 2em;
}
p.dialog {
  padding: 0.2em;
}
/* Word-wrap output correctly.  This is the CSS3 spelling, though Firefox seems
   to not honor it correctly.  Webkit browsers (Chrome, rekonq, Safari) do.
 */
pre,
code,
kbd,
samp {
  white-space: pre-wrap;
}
#fonttest {
  font-family: monospace;
}
p {
  margin-bottom: 0;
}
.end_space {
  min-height: 100px;
  transition: height .2s ease;
}
.notebook_app > #header {
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
}
@media not print {
  .notebook_app {
    background-color: #EEE;
  }
}
kbd {
  border-style: solid;
  border-width: 1px;
  box-shadow: none;
  margin: 2px;
  padding-left: 2px;
  padding-right: 2px;
  padding-top: 1px;
  padding-bottom: 1px;
}
/* CSS for the cell toolbar */
.celltoolbar {
  border: thin solid #CFCFCF;
  border-bottom: none;
  background: #EEE;
  border-radius: 2px 2px 0px 0px;
  width: 100%;
  height: 29px;
  padding-right: 4px;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
  /* Old browsers */
  -webkit-box-pack: end;
  -moz-box-pack: end;
  box-pack: end;
  /* Modern browsers */
  justify-content: flex-end;
  display: -webkit-flex;
}
@media print {
  .celltoolbar {
    display: none;
  }
}
.ctb_hideshow {
  display: none;
  vertical-align: bottom;
}
/* ctb_show is added to the ctb_hideshow div to show the cell toolbar.
   Cell toolbars are only shown when the ctb_global_show class is also set.
*/
.ctb_global_show .ctb_show.ctb_hideshow {
  display: block;
}
.ctb_global_show .ctb_show + .input_area,
.ctb_global_show .ctb_show + div.text_cell_input,
.ctb_global_show .ctb_show ~ div.text_cell_render {
  border-top-right-radius: 0px;
  border-top-left-radius: 0px;
}
.ctb_global_show .ctb_show ~ div.text_cell_render {
  border: 1px solid #cfcfcf;
}
.celltoolbar {
  font-size: 87%;
  padding-top: 3px;
}
.celltoolbar select {
  display: block;
  width: 100%;
  height: 32px;
  padding: 6px 12px;
  font-size: 13px;
  line-height: 1.42857143;
  color: #555555;
  background-color: #fff;
  background-image: none;
  border: 1px solid #ccc;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  -webkit-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  -o-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  height: 30px;
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
  width: inherit;
  font-size: inherit;
  height: 22px;
  padding: 0px;
  display: inline-block;
}
.celltoolbar select:focus {
  border-color: #66afe9;
  outline: 0;
  -webkit-box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
  box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
}
.celltoolbar select::-moz-placeholder {
  color: #999;
  opacity: 1;
}
.celltoolbar select:-ms-input-placeholder {
  color: #999;
}
.celltoolbar select::-webkit-input-placeholder {
  color: #999;
}
.celltoolbar select::-ms-expand {
  border: 0;
  background-color: transparent;
}
.celltoolbar select[disabled],
.celltoolbar select[readonly],
fieldset[disabled] .celltoolbar select {
  background-color: #eeeeee;
  opacity: 1;
}
.celltoolbar select[disabled],
fieldset[disabled] .celltoolbar select {
  cursor: not-allowed;
}
textarea.celltoolbar select {
  height: auto;
}
select.celltoolbar select {
  height: 30px;
  line-height: 30px;
}
textarea.celltoolbar select,
select[multiple].celltoolbar select {
  height: auto;
}
.celltoolbar label {
  margin-left: 5px;
  margin-right: 5px;
}
.completions {
  position: absolute;
  z-index: 110;
  overflow: hidden;
  border: 1px solid #ababab;
  border-radius: 2px;
  -webkit-box-shadow: 0px 6px 10px -1px #adadad;
  box-shadow: 0px 6px 10px -1px #adadad;
  line-height: 1;
}
.completions select {
  background: white;
  outline: none;
  border: none;
  padding: 0px;
  margin: 0px;
  overflow: auto;
  font-family: monospace;
  font-size: 110%;
  color: #000;
  width: auto;
}
.completions select option.context {
  color: #286090;
}
#kernel_logo_widget {
  float: right !important;
  float: right;
}
#kernel_logo_widget .current_kernel_logo {
  display: none;
  margin-top: -1px;
  margin-bottom: -1px;
  width: 32px;
  height: 32px;
}
#menubar {
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  margin-top: 1px;
}
#menubar .navbar {
  border-top: 1px;
  border-radius: 0px 0px 2px 2px;
  margin-bottom: 0px;
}
#menubar .navbar-toggle {
  float: left;
  padding-top: 7px;
  padding-bottom: 7px;
  border: none;
}
#menubar .navbar-collapse {
  clear: left;
}
.nav-wrapper {
  border-bottom: 1px solid #e7e7e7;
}
i.menu-icon {
  padding-top: 4px;
}
ul#help_menu li a {
  overflow: hidden;
  padding-right: 2.2em;
}
ul#help_menu li a i {
  margin-right: -1.2em;
}
.dropdown-submenu {
  position: relative;
}
.dropdown-submenu > .dropdown-menu {
  top: 0;
  left: 100%;
  margin-top: -6px;
  margin-left: -1px;
}
.dropdown-submenu:hover > .dropdown-menu {
  display: block;
}
.dropdown-submenu > a:after {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: block;
  content: "\f0da";
  float: right;
  color: #333333;
  margin-top: 2px;
  margin-right: -10px;
}
.dropdown-submenu > a:after.pull-left {
  margin-right: .3em;
}
.dropdown-submenu > a:after.pull-right {
  margin-left: .3em;
}
.dropdown-submenu:hover > a:after {
  color: #262626;
}
.dropdown-submenu.pull-left {
  float: none;
}
.dropdown-submenu.pull-left > .dropdown-menu {
  left: -100%;
  margin-left: 10px;
}
#notification_area {
  float: right !important;
  float: right;
  z-index: 10;
}
.indicator_area {
  float: right !important;
  float: right;
  color: #777;
  margin-left: 5px;
  margin-right: 5px;
  width: 11px;
  z-index: 10;
  text-align: center;
  width: auto;
}
#kernel_indicator {
  float: right !important;
  float: right;
  color: #777;
  margin-left: 5px;
  margin-right: 5px;
  width: 11px;
  z-index: 10;
  text-align: center;
  width: auto;
  border-left: 1px solid;
}
#kernel_indicator .kernel_indicator_name {
  padding-left: 5px;
  padding-right: 5px;
}
#modal_indicator {
  float: right !important;
  float: right;
  color: #777;
  margin-left: 5px;
  margin-right: 5px;
  width: 11px;
  z-index: 10;
  text-align: center;
  width: auto;
}
#readonly-indicator {
  float: right !important;
  float: right;
  color: #777;
  margin-left: 5px;
  margin-right: 5px;
  width: 11px;
  z-index: 10;
  text-align: center;
  width: auto;
  margin-top: 2px;
  margin-bottom: 0px;
  margin-left: 0px;
  margin-right: 0px;
  display: none;
}
.modal_indicator:before {
  width: 1.28571429em;
  text-align: center;
}
.edit_mode .modal_indicator:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f040";
}
.edit_mode .modal_indicator:before.pull-left {
  margin-right: .3em;
}
.edit_mode .modal_indicator:before.pull-right {
  margin-left: .3em;
}
.command_mode .modal_indicator:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: ' ';
}
.command_mode .modal_indicator:before.pull-left {
  margin-right: .3em;
}
.command_mode .modal_indicator:before.pull-right {
  margin-left: .3em;
}
.kernel_idle_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f10c";
}
.kernel_idle_icon:before.pull-left {
  margin-right: .3em;
}
.kernel_idle_icon:before.pull-right {
  margin-left: .3em;
}
.kernel_busy_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f111";
}
.kernel_busy_icon:before.pull-left {
  margin-right: .3em;
}
.kernel_busy_icon:before.pull-right {
  margin-left: .3em;
}
.kernel_dead_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f1e2";
}
.kernel_dead_icon:before.pull-left {
  margin-right: .3em;
}
.kernel_dead_icon:before.pull-right {
  margin-left: .3em;
}
.kernel_disconnected_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f127";
}
.kernel_disconnected_icon:before.pull-left {
  margin-right: .3em;
}
.kernel_disconnected_icon:before.pull-right {
  margin-left: .3em;
}
.notification_widget {
  color: #777;
  z-index: 10;
  background: rgba(240, 240, 240, 0.5);
  margin-right: 4px;
  color: #333;
  background-color: #fff;
  border-color: #ccc;
}
.notification_widget:focus,
.notification_widget.focus {
  color: #333;
  background-color: #e6e6e6;
  border-color: #8c8c8c;
}
.notification_widget:hover {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
.notification_widget:active,
.notification_widget.active,
.open > .dropdown-toggle.notification_widget {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
.notification_widget:active:hover,
.notification_widget.active:hover,
.open > .dropdown-toggle.notification_widget:hover,
.notification_widget:active:focus,
.notification_widget.active:focus,
.open > .dropdown-toggle.notification_widget:focus,
.notification_widget:active.focus,
.notification_widget.active.focus,
.open > .dropdown-toggle.notification_widget.focus {
  color: #333;
  background-color: #d4d4d4;
  border-color: #8c8c8c;
}
.notification_widget:active,
.notification_widget.active,
.open > .dropdown-toggle.notification_widget {
  background-image: none;
}
.notification_widget.disabled:hover,
.notification_widget[disabled]:hover,
fieldset[disabled] .notification_widget:hover,
.notification_widget.disabled:focus,
.notification_widget[disabled]:focus,
fieldset[disabled] .notification_widget:focus,
.notification_widget.disabled.focus,
.notification_widget[disabled].focus,
fieldset[disabled] .notification_widget.focus {
  background-color: #fff;
  border-color: #ccc;
}
.notification_widget .badge {
  color: #fff;
  background-color: #333;
}
.notification_widget.warning {
  color: #fff;
  background-color: #f0ad4e;
  border-color: #eea236;
}
.notification_widget.warning:focus,
.notification_widget.warning.focus {
  color: #fff;
  background-color: #ec971f;
  border-color: #985f0d;
}
.notification_widget.warning:hover {
  color: #fff;
  background-color: #ec971f;
  border-color: #d58512;
}
.notification_widget.warning:active,
.notification_widget.warning.active,
.open > .dropdown-toggle.notification_widget.warning {
  color: #fff;
  background-color: #ec971f;
  border-color: #d58512;
}
.notification_widget.warning:active:hover,
.notification_widget.warning.active:hover,
.open > .dropdown-toggle.notification_widget.warning:hover,
.notification_widget.warning:active:focus,
.notification_widget.warning.active:focus,
.open > .dropdown-toggle.notification_widget.warning:focus,
.notification_widget.warning:active.focus,
.notification_widget.warning.active.focus,
.open > .dropdown-toggle.notification_widget.warning.focus {
  color: #fff;
  background-color: #d58512;
  border-color: #985f0d;
}
.notification_widget.warning:active,
.notification_widget.warning.active,
.open > .dropdown-toggle.notification_widget.warning {
  background-image: none;
}
.notification_widget.warning.disabled:hover,
.notification_widget.warning[disabled]:hover,
fieldset[disabled] .notification_widget.warning:hover,
.notification_widget.warning.disabled:focus,
.notification_widget.warning[disabled]:focus,
fieldset[disabled] .notification_widget.warning:focus,
.notification_widget.warning.disabled.focus,
.notification_widget.warning[disabled].focus,
fieldset[disabled] .notification_widget.warning.focus {
  background-color: #f0ad4e;
  border-color: #eea236;
}
.notification_widget.warning .badge {
  color: #f0ad4e;
  background-color: #fff;
}
.notification_widget.success {
  color: #fff;
  background-color: #5cb85c;
  border-color: #4cae4c;
}
.notification_widget.success:focus,
.notification_widget.success.focus {
  color: #fff;
  background-color: #449d44;
  border-color: #255625;
}
.notification_widget.success:hover {
  color: #fff;
  background-color: #449d44;
  border-color: #398439;
}
.notification_widget.success:active,
.notification_widget.success.active,
.open > .dropdown-toggle.notification_widget.success {
  color: #fff;
  background-color: #449d44;
  border-color: #398439;
}
.notification_widget.success:active:hover,
.notification_widget.success.active:hover,
.open > .dropdown-toggle.notification_widget.success:hover,
.notification_widget.success:active:focus,
.notification_widget.success.active:focus,
.open > .dropdown-toggle.notification_widget.success:focus,
.notification_widget.success:active.focus,
.notification_widget.success.active.focus,
.open > .dropdown-toggle.notification_widget.success.focus {
  color: #fff;
  background-color: #398439;
  border-color: #255625;
}
.notification_widget.success:active,
.notification_widget.success.active,
.open > .dropdown-toggle.notification_widget.success {
  background-image: none;
}
.notification_widget.success.disabled:hover,
.notification_widget.success[disabled]:hover,
fieldset[disabled] .notification_widget.success:hover,
.notification_widget.success.disabled:focus,
.notification_widget.success[disabled]:focus,
fieldset[disabled] .notification_widget.success:focus,
.notification_widget.success.disabled.focus,
.notification_widget.success[disabled].focus,
fieldset[disabled] .notification_widget.success.focus {
  background-color: #5cb85c;
  border-color: #4cae4c;
}
.notification_widget.success .badge {
  color: #5cb85c;
  background-color: #fff;
}
.notification_widget.info {
  color: #fff;
  background-color: #5bc0de;
  border-color: #46b8da;
}
.notification_widget.info:focus,
.notification_widget.info.focus {
  color: #fff;
  background-color: #31b0d5;
  border-color: #1b6d85;
}
.notification_widget.info:hover {
  color: #fff;
  background-color: #31b0d5;
  border-color: #269abc;
}
.notification_widget.info:active,
.notification_widget.info.active,
.open > .dropdown-toggle.notification_widget.info {
  color: #fff;
  background-color: #31b0d5;
  border-color: #269abc;
}
.notification_widget.info:active:hover,
.notification_widget.info.active:hover,
.open > .dropdown-toggle.notification_widget.info:hover,
.notification_widget.info:active:focus,
.notification_widget.info.active:focus,
.open > .dropdown-toggle.notification_widget.info:focus,
.notification_widget.info:active.focus,
.notification_widget.info.active.focus,
.open > .dropdown-toggle.notification_widget.info.focus {
  color: #fff;
  background-color: #269abc;
  border-color: #1b6d85;
}
.notification_widget.info:active,
.notification_widget.info.active,
.open > .dropdown-toggle.notification_widget.info {
  background-image: none;
}
.notification_widget.info.disabled:hover,
.notification_widget.info[disabled]:hover,
fieldset[disabled] .notification_widget.info:hover,
.notification_widget.info.disabled:focus,
.notification_widget.info[disabled]:focus,
fieldset[disabled] .notification_widget.info:focus,
.notification_widget.info.disabled.focus,
.notification_widget.info[disabled].focus,
fieldset[disabled] .notification_widget.info.focus {
  background-color: #5bc0de;
  border-color: #46b8da;
}
.notification_widget.info .badge {
  color: #5bc0de;
  background-color: #fff;
}
.notification_widget.danger {
  color: #fff;
  background-color: #d9534f;
  border-color: #d43f3a;
}
.notification_widget.danger:focus,
.notification_widget.danger.focus {
  color: #fff;
  background-color: #c9302c;
  border-color: #761c19;
}
.notification_widget.danger:hover {
  color: #fff;
  background-color: #c9302c;
  border-color: #ac2925;
}
.notification_widget.danger:active,
.notification_widget.danger.active,
.open > .dropdown-toggle.notification_widget.danger {
  color: #fff;
  background-color: #c9302c;
  border-color: #ac2925;
}
.notification_widget.danger:active:hover,
.notification_widget.danger.active:hover,
.open > .dropdown-toggle.notification_widget.danger:hover,
.notification_widget.danger:active:focus,
.notification_widget.danger.active:focus,
.open > .dropdown-toggle.notification_widget.danger:focus,
.notification_widget.danger:active.focus,
.notification_widget.danger.active.focus,
.open > .dropdown-toggle.notification_widget.danger.focus {
  color: #fff;
  background-color: #ac2925;
  border-color: #761c19;
}
.notification_widget.danger:active,
.notification_widget.danger.active,
.open > .dropdown-toggle.notification_widget.danger {
  background-image: none;
}
.notification_widget.danger.disabled:hover,
.notification_widget.danger[disabled]:hover,
fieldset[disabled] .notification_widget.danger:hover,
.notification_widget.danger.disabled:focus,
.notification_widget.danger[disabled]:focus,
fieldset[disabled] .notification_widget.danger:focus,
.notification_widget.danger.disabled.focus,
.notification_widget.danger[disabled].focus,
fieldset[disabled] .notification_widget.danger.focus {
  background-color: #d9534f;
  border-color: #d43f3a;
}
.notification_widget.danger .badge {
  color: #d9534f;
  background-color: #fff;
}
div#pager {
  background-color: #fff;
  font-size: 14px;
  line-height: 20px;
  overflow: hidden;
  display: none;
  position: fixed;
  bottom: 0px;
  width: 100%;
  max-height: 50%;
  padding-top: 8px;
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  /* Display over codemirror */
  z-index: 100;
  /* Hack which prevents jquery ui resizable from changing top. */
  top: auto !important;
}
div#pager pre {
  line-height: 1.21429em;
  color: #000;
  background-color: #f7f7f7;
  padding: 0.4em;
}
div#pager #pager-button-area {
  position: absolute;
  top: 8px;
  right: 20px;
}
div#pager #pager-contents {
  position: relative;
  overflow: auto;
  width: 100%;
  height: 100%;
}
div#pager #pager-contents #pager-container {
  position: relative;
  padding: 15px 0px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
div#pager .ui-resizable-handle {
  top: 0px;
  height: 8px;
  background: #f7f7f7;
  border-top: 1px solid #cfcfcf;
  border-bottom: 1px solid #cfcfcf;
  /* This injects handle bars (a short, wide = symbol) for 
        the resize handle. */
}
div#pager .ui-resizable-handle::after {
  content: '';
  top: 2px;
  left: 50%;
  height: 3px;
  width: 30px;
  margin-left: -15px;
  position: absolute;
  border-top: 1px solid #cfcfcf;
}
.quickhelp {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
  line-height: 1.8em;
}
.shortcut_key {
  display: inline-block;
  width: 21ex;
  text-align: right;
  font-family: monospace;
}
.shortcut_descr {
  display: inline-block;
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
}
span.save_widget {
  margin-top: 6px;
}
span.save_widget span.filename {
  height: 1em;
  line-height: 1em;
  padding: 3px;
  margin-left: 16px;
  border: none;
  font-size: 146.5%;
  border-radius: 2px;
}
span.save_widget span.filename:hover {
  background-color: #e6e6e6;
}
span.checkpoint_status,
span.autosave_status {
  font-size: small;
}
@media (max-width: 767px) {
  span.save_widget {
    font-size: small;
  }
  span.checkpoint_status,
  span.autosave_status {
    display: none;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  span.checkpoint_status {
    display: none;
  }
  span.autosave_status {
    font-size: x-small;
  }
}
.toolbar {
  padding: 0px;
  margin-left: -5px;
  margin-top: 2px;
  margin-bottom: 5px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
.toolbar select,
.toolbar label {
  width: auto;
  vertical-align: middle;
  margin-right: 2px;
  margin-bottom: 0px;
  display: inline;
  font-size: 92%;
  margin-left: 0.3em;
  margin-right: 0.3em;
  padding: 0px;
  padding-top: 3px;
}
.toolbar .btn {
  padding: 2px 8px;
}
.toolbar .btn-group {
  margin-top: 0px;
  margin-left: 5px;
}
#maintoolbar {
  margin-bottom: -3px;
  margin-top: -8px;
  border: 0px;
  min-height: 27px;
  margin-left: 0px;
  padding-top: 11px;
  padding-bottom: 3px;
}
#maintoolbar .navbar-text {
  float: none;
  vertical-align: middle;
  text-align: right;
  margin-left: 5px;
  margin-right: 0px;
  margin-top: 0px;
}
.select-xs {
  height: 24px;
}
.pulse,
.dropdown-menu > li > a.pulse,
li.pulse > a.dropdown-toggle,
li.pulse.open > a.dropdown-toggle {
  background-color: #F37626;
  color: white;
}
/**
 * Primary styles
 *
 * Author: Jupyter Development Team
 */
/** WARNING IF YOU ARE EDITTING THIS FILE, if this is a .css file, It has a lot
 * of chance of beeing generated from the ../less/[samename].less file, you can
 * try to get back the less file by reverting somme commit in history
 **/
/*
 * We'll try to get something pretty, so we
 * have some strange css to have the scroll bar on
 * the left with fix button on the top right of the tooltip
 */
@-moz-keyframes fadeOut {
  from {
    opacity: 1;
  }
  to {
    opacity: 0;
  }
}
@-webkit-keyframes fadeOut {
  from {
    opacity: 1;
  }
  to {
    opacity: 0;
  }
}
@-moz-keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
@-webkit-keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
/*properties of tooltip after "expand"*/
.bigtooltip {
  overflow: auto;
  height: 200px;
  -webkit-transition-property: height;
  -webkit-transition-duration: 500ms;
  -moz-transition-property: height;
  -moz-transition-duration: 500ms;
  transition-property: height;
  transition-duration: 500ms;
}
/*properties of tooltip before "expand"*/
.smalltooltip {
  -webkit-transition-property: height;
  -webkit-transition-duration: 500ms;
  -moz-transition-property: height;
  -moz-transition-duration: 500ms;
  transition-property: height;
  transition-duration: 500ms;
  text-overflow: ellipsis;
  overflow: hidden;
  height: 80px;
}
.tooltipbuttons {
  position: absolute;
  padding-right: 15px;
  top: 0px;
  right: 0px;
}
.tooltiptext {
  /*avoid the button to overlap on some docstring*/
  padding-right: 30px;
}
.ipython_tooltip {
  max-width: 700px;
  /*fade-in animation when inserted*/
  -webkit-animation: fadeOut 400ms;
  -moz-animation: fadeOut 400ms;
  animation: fadeOut 400ms;
  -webkit-animation: fadeIn 400ms;
  -moz-animation: fadeIn 400ms;
  animation: fadeIn 400ms;
  vertical-align: middle;
  background-color: #f7f7f7;
  overflow: visible;
  border: #ababab 1px solid;
  outline: none;
  padding: 3px;
  margin: 0px;
  padding-left: 7px;
  font-family: monospace;
  min-height: 50px;
  -moz-box-shadow: 0px 6px 10px -1px #adadad;
  -webkit-box-shadow: 0px 6px 10px -1px #adadad;
  box-shadow: 0px 6px 10px -1px #adadad;
  border-radius: 2px;
  position: absolute;
  z-index: 1000;
}
.ipython_tooltip a {
  float: right;
}
.ipython_tooltip .tooltiptext pre {
  border: 0;
  border-radius: 0;
  font-size: 100%;
  background-color: #f7f7f7;
}
.pretooltiparrow {
  left: 0px;
  margin: 0px;
  top: -16px;
  width: 40px;
  height: 16px;
  overflow: hidden;
  position: absolute;
}
.pretooltiparrow:before {
  background-color: #f7f7f7;
  border: 1px #ababab solid;
  z-index: 11;
  content: "";
  position: absolute;
  left: 15px;
  top: 10px;
  width: 25px;
  height: 25px;
  -webkit-transform: rotate(45deg);
  -moz-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  -o-transform: rotate(45deg);
}
ul.typeahead-list i {
  margin-left: -10px;
  width: 18px;
}
ul.typeahead-list {
  max-height: 80vh;
  overflow: auto;
}
ul.typeahead-list > li > a {
  /** Firefox bug **/
  /* see https://github.com/jupyter/notebook/issues/559 */
  white-space: normal;
}
.cmd-palette .modal-body {
  padding: 7px;
}
.cmd-palette form {
  background: white;
}
.cmd-palette input {
  outline: none;
}
.no-shortcut {
  display: none;
}
.command-shortcut:before {
  content: "(command)";
  padding-right: 3px;
  color: #777777;
}
.edit-shortcut:before {
  content: "(edit)";
  padding-right: 3px;
  color: #777777;
}
#find-and-replace #replace-preview .match,
#find-and-replace #replace-preview .insert {
  background-color: #BBDEFB;
  border-color: #90CAF9;
  border-style: solid;
  border-width: 1px;
  border-radius: 0px;
}
#find-and-replace #replace-preview .replace .match {
  background-color: #FFCDD2;
  border-color: #EF9A9A;
  border-radius: 0px;
}
#find-and-replace #replace-preview .replace .insert {
  background-color: #C8E6C9;
  border-color: #A5D6A7;
  border-radius: 0px;
}
#find-and-replace #replace-preview {
  max-height: 60vh;
  overflow: auto;
}
#find-and-replace #replace-preview pre {
  padding: 5px 10px;
}
.terminal-app {
  background: #EEE;
}
.terminal-app #header {
  background: #fff;
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
}
.terminal-app .terminal {
  width: 100%;
  float: left;
  font-family: monospace;
  color: white;
  background: black;
  padding: 0.4em;
  border-radius: 2px;
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.4);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.4);
}
.terminal-app .terminal,
.terminal-app .terminal dummy-screen {
  line-height: 1em;
  font-size: 14px;
}
.terminal-app .terminal .xterm-rows {
  padding: 10px;
}
.terminal-app .terminal-cursor {
  color: black;
  background: white;
}
.terminal-app #terminado-container {
  margin-top: 20px;
}
/*# sourceMappingURL=style.min.css.map */
    </style>
<style type="text/css">
    .highlight .hll { background-color: #ffffcc }
.highlight  { background: #f8f8f8; }
.highlight .c { color: #408080; font-style: italic } /* Comment */
.highlight .err { border: 1px solid #FF0000 } /* Error */
.highlight .k { color: #008000; font-weight: bold } /* Keyword */
.highlight .o { color: #666666 } /* Operator */
.highlight .ch { color: #408080; font-style: italic } /* Comment.Hashbang */
.highlight .cm { color: #408080; font-style: italic } /* Comment.Multiline */
.highlight .cp { color: #BC7A00 } /* Comment.Preproc */
.highlight .cpf { color: #408080; font-style: italic } /* Comment.PreprocFile */
.highlight .c1 { color: #408080; font-style: italic } /* Comment.Single */
.highlight .cs { color: #408080; font-style: italic } /* Comment.Special */
.highlight .gd { color: #A00000 } /* Generic.Deleted */
.highlight .ge { font-style: italic } /* Generic.Emph */
.highlight .gr { color: #FF0000 } /* Generic.Error */
.highlight .gh { color: #000080; font-weight: bold } /* Generic.Heading */
.highlight .gi { color: #00A000 } /* Generic.Inserted */
.highlight .go { color: #888888 } /* Generic.Output */
.highlight .gp { color: #000080; font-weight: bold } /* Generic.Prompt */
.highlight .gs { font-weight: bold } /* Generic.Strong */
.highlight .gu { color: #800080; font-weight: bold } /* Generic.Subheading */
.highlight .gt { color: #0044DD } /* Generic.Traceback */
.highlight .kc { color: #008000; font-weight: bold } /* Keyword.Constant */
.highlight .kd { color: #008000; font-weight: bold } /* Keyword.Declaration */
.highlight .kn { color: #008000; font-weight: bold } /* Keyword.Namespace */
.highlight .kp { color: #008000 } /* Keyword.Pseudo */
.highlight .kr { color: #008000; font-weight: bold } /* Keyword.Reserved */
.highlight .kt { color: #B00040 } /* Keyword.Type */
.highlight .m { color: #666666 } /* Literal.Number */
.highlight .s { color: #BA2121 } /* Literal.String */
.highlight .na { color: #7D9029 } /* Name.Attribute */
.highlight .nb { color: #008000 } /* Name.Builtin */
.highlight .nc { color: #0000FF; font-weight: bold } /* Name.Class */
.highlight .no { color: #880000 } /* Name.Constant */
.highlight .nd { color: #AA22FF } /* Name.Decorator */
.highlight .ni { color: #999999; font-weight: bold } /* Name.Entity */
.highlight .ne { color: #D2413A; font-weight: bold } /* Name.Exception */
.highlight .nf { color: #0000FF } /* Name.Function */
.highlight .nl { color: #A0A000 } /* Name.Label */
.highlight .nn { color: #0000FF; font-weight: bold } /* Name.Namespace */
.highlight .nt { color: #008000; font-weight: bold } /* Name.Tag */
.highlight .nv { color: #19177C } /* Name.Variable */
.highlight .ow { color: #AA22FF; font-weight: bold } /* Operator.Word */
.highlight .w { color: #bbbbbb } /* Text.Whitespace */
.highlight .mb { color: #666666 } /* Literal.Number.Bin */
.highlight .mf { color: #666666 } /* Literal.Number.Float */
.highlight .mh { color: #666666 } /* Literal.Number.Hex */
.highlight .mi { color: #666666 } /* Literal.Number.Integer */
.highlight .mo { color: #666666 } /* Literal.Number.Oct */
.highlight .sa { color: #BA2121 } /* Literal.String.Affix */
.highlight .sb { color: #BA2121 } /* Literal.String.Backtick */
.highlight .sc { color: #BA2121 } /* Literal.String.Char */
.highlight .dl { color: #BA2121 } /* Literal.String.Delimiter */
.highlight .sd { color: #BA2121; font-style: italic } /* Literal.String.Doc */
.highlight .s2 { color: #BA2121 } /* Literal.String.Double */
.highlight .se { color: #BB6622; font-weight: bold } /* Literal.String.Escape */
.highlight .sh { color: #BA2121 } /* Literal.String.Heredoc */
.highlight .si { color: #BB6688; font-weight: bold } /* Literal.String.Interpol */
.highlight .sx { color: #008000 } /* Literal.String.Other */
.highlight .sr { color: #BB6688 } /* Literal.String.Regex */
.highlight .s1 { color: #BA2121 } /* Literal.String.Single */
.highlight .ss { color: #19177C } /* Literal.String.Symbol */
.highlight .bp { color: #008000 } /* Name.Builtin.Pseudo */
.highlight .fm { color: #0000FF } /* Name.Function.Magic */
.highlight .vc { color: #19177C } /* Name.Variable.Class */
.highlight .vg { color: #19177C } /* Name.Variable.Global */
.highlight .vi { color: #19177C } /* Name.Variable.Instance */
.highlight .vm { color: #19177C } /* Name.Variable.Magic */
.highlight .il { color: #666666 } /* Literal.Number.Integer.Long */
    </style>
<style type="text/css">
    
/* Temporary definitions which will become obsolete with Notebook release 5.0 */
.ansi-black-fg { color: #3E424D; }
.ansi-black-bg { background-color: #3E424D; }
.ansi-black-intense-fg { color: #282C36; }
.ansi-black-intense-bg { background-color: #282C36; }
.ansi-red-fg { color: #E75C58; }
.ansi-red-bg { background-color: #E75C58; }
.ansi-red-intense-fg { color: #B22B31; }
.ansi-red-intense-bg { background-color: #B22B31; }
.ansi-green-fg { color: #00A250; }
.ansi-green-bg { background-color: #00A250; }
.ansi-green-intense-fg { color: #007427; }
.ansi-green-intense-bg { background-color: #007427; }
.ansi-yellow-fg { color: #DDB62B; }
.ansi-yellow-bg { background-color: #DDB62B; }
.ansi-yellow-intense-fg { color: #B27D12; }
.ansi-yellow-intense-bg { background-color: #B27D12; }
.ansi-blue-fg { color: #208FFB; }
.ansi-blue-bg { background-color: #208FFB; }
.ansi-blue-intense-fg { color: #0065CA; }
.ansi-blue-intense-bg { background-color: #0065CA; }
.ansi-magenta-fg { color: #D160C4; }
.ansi-magenta-bg { background-color: #D160C4; }
.ansi-magenta-intense-fg { color: #A03196; }
.ansi-magenta-intense-bg { background-color: #A03196; }
.ansi-cyan-fg { color: #60C6C8; }
.ansi-cyan-bg { background-color: #60C6C8; }
.ansi-cyan-intense-fg { color: #258F8F; }
.ansi-cyan-intense-bg { background-color: #258F8F; }
.ansi-white-fg { color: #C5C1B4; }
.ansi-white-bg { background-color: #C5C1B4; }
.ansi-white-intense-fg { color: #A1A6B2; }
.ansi-white-intense-bg { background-color: #A1A6B2; }

.ansi-bold { font-weight: bold; }

</style>


<style type="text/css">
/* Overrides of notebook CSS for static HTML export */
body {
  overflow: visible;
  padding: 8px;
}

div#notebook {
  overflow: visible;
  border-top: none;
}

@media print {
  div.cell {
    display: block;
    page-break-inside: avoid;
  } 
  div.output_wrapper { 
    display: block;
    page-break-inside: avoid; 
  }
  div.output { 
    display: block;
    page-break-inside: avoid; 
  }
}
</style>

<!-- Custom stylesheet, it must be in the same directory as the html file -->
<link rel="stylesheet" href="custom.css">

<!-- Loading mathjax macro -->
<!-- Load mathjax -->
    <script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS_HTML"></script>
    <!-- MathJax configuration -->
    <script type="text/x-mathjax-config">
    MathJax.Hub.Config({
        tex2jax: {
            inlineMath: [ ['$','$'], ["\\(","\\)"] ],
            displayMath: [ ['$$','$$'], ["\\[","\\]"] ],
            processEscapes: true,
            processEnvironments: true
        },
        // Center justify equations in code and markdown cells. Elsewhere
        // we use CSS to left justify single line equations in code cells.
        displayAlign: 'center',
        "HTML-CSS": {
            styles: {'.MathJax_Display': {"margin": 0}},
            linebreaks: { automatic: true }
        }
    });
    </script>
    <!-- End of mathjax configuration --></head>
<body>
  <div tabindex="-1" id="notebook" class="border-box-sizing">
    <div class="container" id="notebook-container">

<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><a href="https://github.com/joshualmitchell/Pytorch-Tutorial">Take me to the github!</a></p>
<p><a href="#outline">Take me to the outline / table of contents!</a></p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Motivation:">Motivation:<a class="anchor-link" href="#Motivation:">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>As I was going through the <a href="http://pytorch.org/tutorials/beginner/deep_learning_60min_blitz.html">Deep Learning Blitz</a>  tutorial from pytorch.org, I had a lot of questions. I googled my way through all of them, but I had wished there was a more extensive example set (i.e. starting from a really basic model all the way to a CNN). That way I could see very clearly, through examples, what each component did in isolation.</p>
<p>Since I did that for myself, I figured I might as well put it online for everyone else who's learning PyTorch. This is not designed to be an end-all-be-all tutorial (in fact, I use a lot of pytorch tutorial code myself), so for each section, I'll link to various resources that helped me understand the concepts. Hopefully, in conjunction with the examples, it'll be helpful.</p>
<p>Please feel free to email me if you have any questions or suggestions: jlelonmitchell@gmail.com</p>
<p>Here are other things I might do more tutorials on if reception is good and people request them:</p>
<p>network architecture, batch normalization, vanishing gradients, dropout, initialization techniques, non-convex optimization, biases, choices of loss functions, data augmentation, regularization methods, computational considerations, modifications of backpropagation</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Outline:-">Outline: <a id="outline" /><a class="anchor-link" href="#Outline:-">&#182;</a></h1><p>1) <a href="#one">Bare Minimum Model</a>: create an absolute bare minimum model with Tensors</p>
<p>2) <a href="#two">Basic Linear Regression Model</a>: create a basic linear regression model (i.e. no training or anything yet; just initializing it and doing the calculation)</p>
<p>3) <a href="#three">Calculate Loss</a>: calculate our (linear regression) model's loss using a loss function</p>
<p>4) <a href="#four">Calculating Our Gradient</a>: calculate our gradient based on the previous loss function</p>
<p>5) <a href="#five">Recalculating/Updating Our Weights</a>: calculate the change in our weights based on the gradient and updating them</p>
<p>6) <a href="#six">Updating Our Weights More Than Once</a>: set up a for loop to do steps 3-5 an arbitrary number of times (i.e. epochs)</p>
<p>7) <a href="#seven">Making Our Epochs Only Use A Subset Of The Data</a>: make the for loop only use a portion of the data (i.e. a batch)</p>
<p>8) <a href="#eight">Changing Our Model from Linear Regression to Neural Network</a>: make it fit the data better</p>
<p>9) <a href="#nine">Abstracting Our Neural Network Into Its Pytorch Class</a>: make it more maintainable and less messy</p>
<p>10) <a href="#ten">Changing Our Input From Arbitrary Vectors To Images</a>: make it do something more interesting</p>
<p>11) <a href="#eleven">Adding A Convolutional Layer</a>: make our model do convolutions before it does the other stuff</p>
<p>12) <a href="#twelve">Adding A Pooling Layer</a>: make our model faster by only taking the biggest "most important" values into consideration</p>
<p>13) <a href="#thirteen">Making More Optimizations</a>: change our activation functions to ReLU, add more layers, and other housekeeping</p>
<p>14) <a href="#fourteen">Bask in the glory of our newly minted Convolutional Neural Network</a></p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[1]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">import</span> <span class="nn">torch</span> <span class="c1"># Tensor Package (for use on GPU)</span>
<span class="kn">from</span> <span class="nn">torch.autograd</span> <span class="k">import</span> <span class="n">Variable</span> <span class="c1"># for computational graphs</span>
<span class="kn">import</span> <span class="nn">torch.nn</span> <span class="k">as</span> <span class="nn">nn</span> <span class="c1">## Neural Network package</span>
<span class="kn">import</span> <span class="nn">torch.nn.functional</span> <span class="k">as</span> <span class="nn">F</span> <span class="c1"># Non-linearities package</span>
<span class="kn">import</span> <span class="nn">torch.optim</span> <span class="k">as</span> <span class="nn">optim</span> <span class="c1"># Optimization package</span>
<span class="kn">from</span> <span class="nn">torch.utils.data</span> <span class="k">import</span> <span class="n">Dataset</span><span class="p">,</span> <span class="n">TensorDataset</span><span class="p">,</span> <span class="n">DataLoader</span> <span class="c1"># for dealing with data</span>
<span class="kn">import</span> <span class="nn">torchvision</span> <span class="c1"># for dealing with vision data</span>
<span class="kn">import</span> <span class="nn">torchvision.transforms</span> <span class="k">as</span> <span class="nn">transforms</span> <span class="c1"># for modifying vision data to run it through models</span>

<span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="k">as</span> <span class="nn">plt</span> <span class="c1"># for plotting</span>
<span class="kn">import</span> <span class="nn">numpy</span> <span class="k">as</span> <span class="nn">np</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><a id='one'></a></p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="1)--Bare-Minimum-Model:">1)  Bare Minimum Model:<a class="anchor-link" href="#1)--Bare-Minimum-Model:">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Links:</p>
<ul>
<li><a href="http://pytorch.org/tutorials/beginner/blitz/tensor_tutorial.html">http://pytorch.org/tutorials/beginner/blitz/tensor_tutorial.html</a> - Pytorch's Tensor Tutorial</li>
<li><a href="https://www.google.com/search?q=PyTorch+Tensor+Examples">https://www.google.com/search?q=PyTorch+Tensor+Examples</a> - More Examples</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h4 id="Home--|---Back--|---Next"><a href="#outline">Home</a>  |   <a href="#outline">Back</a>  |   <a href="#two">Next</a><a class="anchor-link" href="#Home--|---Back--|---Next">&#182;</a></h4>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Quick-Tensor-Demonstration:">Quick Tensor Demonstration:<a class="anchor-link" href="#Quick-Tensor-Demonstration:">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[2]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># here&#39;s a one dimensional array the pytorch way (i.e. allowing GPU computations):</span>
<span class="n">x1</span> <span class="o">=</span> <span class="n">torch</span><span class="o">.</span><span class="n">Tensor</span><span class="p">([</span><span class="mi">1</span><span class="p">,</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">3</span><span class="p">,</span> <span class="mi">4</span><span class="p">])</span>

<span class="c1"># here&#39;s a two dimensional array (i.e. of size 2 x 4):</span>
<span class="n">x2</span> <span class="o">=</span> <span class="n">torch</span><span class="o">.</span><span class="n">Tensor</span><span class="p">([[</span><span class="mi">5</span><span class="p">,</span> <span class="mi">6</span><span class="p">,</span> <span class="mi">7</span><span class="p">,</span> <span class="mi">8</span><span class="p">],</span> <span class="p">[</span><span class="mi">9</span><span class="p">,</span> <span class="mi">10</span><span class="p">,</span> <span class="mi">11</span><span class="p">,</span> <span class="mi">12</span><span class="p">]])</span>

<span class="c1"># here&#39;s a three dimensional array (i.e. of size 2 x 2 x 4):</span>
<span class="n">x3</span> <span class="o">=</span> <span class="n">torch</span><span class="o">.</span><span class="n">Tensor</span><span class="p">([[[</span><span class="mi">1</span><span class="p">,</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">3</span><span class="p">,</span> <span class="mi">4</span><span class="p">],</span> <span class="p">[</span><span class="mi">5</span><span class="p">,</span> <span class="mi">6</span><span class="p">,</span> <span class="mi">7</span><span class="p">,</span> <span class="mi">8</span><span class="p">]],</span> <span class="p">[[</span><span class="mi">9</span><span class="p">,</span> <span class="mi">10</span><span class="p">,</span> <span class="mi">11</span><span class="p">,</span> <span class="mi">12</span><span class="p">],</span> <span class="p">[</span><span class="mi">13</span><span class="p">,</span> <span class="mi">14</span><span class="p">,</span> <span class="mi">15</span><span class="p">,</span> <span class="mi">16</span><span class="p">]]])</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[3]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># x1</span>

<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;----------------------------------------&quot;</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">x1</span><span class="p">[</span><span class="mi">0</span><span class="p">])</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;----------------------------------------&quot;</span><span class="p">)</span>
<span class="c1"># prints 1.0</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">
<div class="prompt"></div>

<div class="output_subarea output_stream output_stdout output_text">
<pre>----------------------------------------
1.0
----------------------------------------
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[4]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># x2</span>

<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;----------------------------------------&quot;</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">x2</span><span class="p">[</span><span class="mi">0</span><span class="p">,</span> <span class="mi">0</span><span class="p">])</span> 
<span class="c1"># prints 5.0; the first entry of the first vector</span>

<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;----------------------------------------&quot;</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">x2</span><span class="p">[</span><span class="mi">0</span><span class="p">,</span> <span class="p">:])</span> 
<span class="c1"># prints 5, 6, 7, 8; all the entries of the first vector</span>

<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;----------------------------------------&quot;</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">x2</span><span class="p">[:,</span> <span class="mi">2</span><span class="p">])</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;----------------------------------------&quot;</span><span class="p">)</span>
<span class="c1"># prints 7, 11; all the third entries of each vector vector</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">
<div class="prompt"></div>

<div class="output_subarea output_stream output_stdout output_text">
<pre>----------------------------------------
5.0
----------------------------------------

 5
 6
 7
 8
[torch.FloatTensor of size 4]

----------------------------------------

  7
 11
[torch.FloatTensor of size 2]

----------------------------------------
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[5]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># x3</span>

<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;----------------------------------------&quot;</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">x3</span><span class="p">[</span><span class="mi">0</span><span class="p">,</span> <span class="mi">0</span><span class="p">,</span> <span class="mi">0</span><span class="p">])</span> 
<span class="c1"># prints 1.0; the first entry of the first vector of the first set of vectors</span>

<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;----------------------------------------&quot;</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">x3</span><span class="p">[:,</span> <span class="mi">0</span><span class="p">,</span> <span class="mi">0</span><span class="p">])</span> 
<span class="c1"># prints 1, 9; the first entry of each first vector in each set of vectors</span>

<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;----------------------------------------&quot;</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">x3</span><span class="p">[</span><span class="mi">0</span><span class="p">,</span> <span class="p">:,</span> <span class="mi">0</span><span class="p">])</span> 
<span class="c1"># prints 1, 5; pick the first set of vectors, and from each vector, choose the first entry</span>

<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;----------------------------------------&quot;</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">x3</span><span class="p">[</span><span class="mi">0</span><span class="p">,</span> <span class="mi">0</span><span class="p">,</span> <span class="p">:])</span> 
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;----------------------------------------&quot;</span><span class="p">)</span>
<span class="c1"># prints 1, 2, 3, 4; everything in the first vector of the first set</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">
<div class="prompt"></div>

<div class="output_subarea output_stream output_stdout output_text">
<pre>----------------------------------------
1.0
----------------------------------------

 1
 9
[torch.FloatTensor of size 2]

----------------------------------------

 1
 5
[torch.FloatTensor of size 2]

----------------------------------------

 1
 2
 3
 4
[torch.FloatTensor of size 4]

----------------------------------------
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Bare-Minimum-Model-(y-=-x)">Bare Minimum Model (y = x)<a class="anchor-link" href="#Bare-Minimum-Model-(y-=-x)">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[6]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">x1_node</span> <span class="o">=</span> <span class="n">Variable</span><span class="p">(</span><span class="n">x1</span><span class="p">,</span> <span class="n">requires_grad</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
<span class="c1"># we put our tensor in a Variable so we can use it for training and other stuff later</span>

<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;----------------------------------------&quot;</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">x1_node</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;----------------------------------------&quot;</span><span class="p">)</span>
<span class="c1"># prints Variable containing 1, 2, 3, 4</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">
<div class="prompt"></div>

<div class="output_subarea output_stream output_stdout output_text">
<pre>----------------------------------------
Variable containing:
 1
 2
 3
 4
[torch.FloatTensor of size 4]

----------------------------------------
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[7]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">y_node</span> <span class="o">=</span> <span class="n">x1_node</span>
<span class="c1"># we did some &quot;stuff&quot; to x1_node (except we didn&#39;t do anything) and then assigned the result to a new y variable</span>

<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;----------------------------------------&quot;</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">y_node</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;----------------------------------------&quot;</span><span class="p">)</span>
<span class="c1"># prints Variable containing 1, 2, 3, 4</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">
<div class="prompt"></div>

<div class="output_subarea output_stream output_stdout output_text">
<pre>----------------------------------------
Variable containing:
 1
 2
 3
 4
[torch.FloatTensor of size 4]

----------------------------------------
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><a id='two'></a></p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="2)--Basic-Linear-Regression-Model">2)  Basic Linear Regression Model<a class="anchor-link" href="#2)--Basic-Linear-Regression-Model">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Links:</p>
<ul>
<li><a href="http://pytorch.org/docs/0.3.1/nn.html#linear-layers">http://pytorch.org/docs/0.3.1/nn.html#linear-layers</a> - pytorch linear layer documentation</li>
<li><a href="https://www.khanacademy.org/math/ap-statistics/bivariate-data-ap/least-squares-regression/v/example-estimating-from-regression-line">https://www.khanacademy.org/math/ap-statistics/bivariate-data-ap/least-squares-regression/v/example-estimating-from-regression-line</a> - Khan Academy</li>
<li><a href="https://www.google.com/search?q=Linear+Regression+Examples">https://www.google.com/search?q=Linear+Regression+Examples</a> - More Examples</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h4 id="Home--|---Back--|---Next"><a href="#outline">Home</a>  |   <a href="#one">Back</a>  |   <a href="#three">Next</a><a class="anchor-link" href="#Home--|---Back--|---Next">&#182;</a></h4>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[8]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">x1</span> <span class="o">=</span> <span class="n">torch</span><span class="o">.</span><span class="n">Tensor</span><span class="p">([</span><span class="mi">1</span><span class="p">,</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">3</span><span class="p">,</span> <span class="mi">4</span><span class="p">])</span>
<span class="n">x1_var</span> <span class="o">=</span> <span class="n">Variable</span><span class="p">(</span><span class="n">x1</span><span class="p">,</span> <span class="n">requires_grad</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>

<span class="n">linear_layer1</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Linear</span><span class="p">(</span><span class="mi">4</span><span class="p">,</span> <span class="mi">1</span><span class="p">)</span>
<span class="c1"># create a linear layer (i.e. a linear equation: w1x1 + w2x2 + w3x3 + w4x4 + b, with 4 inputs and 1 output)</span>
<span class="c1"># w and b stand for weight and bias, respectively</span>

<span class="n">predicted_y</span> <span class="o">=</span> <span class="n">linear_layer1</span><span class="p">(</span><span class="n">x1_var</span><span class="p">)</span>
<span class="c1"># run the x1 variable through the linear equation and put the output in predicted_y</span>

<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;----------------------------------------&quot;</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">predicted_y</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;----------------------------------------&quot;</span><span class="p">)</span>
<span class="c1"># prints the predicted y value (the weights and bias are initialized randomly; my output was 1.3712)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">
<div class="prompt"></div>

<div class="output_subarea output_stream output_stdout output_text">
<pre>----------------------------------------
Variable containing:
-0.6885
[torch.FloatTensor of size 1]

----------------------------------------
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><a id='three'></a></p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="3)--Calculating-The-Loss-Function">3)  Calculating The Loss Function<a class="anchor-link" href="#3)--Calculating-The-Loss-Function">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Links:</p>
<ul>
<li><a href="https://stackoverflow.com/questions/42877989/what-is-a-loss-function-in-simple-words">https://stackoverflow.com/questions/42877989/what-is-a-loss-function-in-simple-words</a> - good SO post</li>
<li><a href="http://pytorch.org/docs/0.3.1/nn.html#id38">http://pytorch.org/docs/0.3.1/nn.html#id38</a> - pytorch loss functions documentation</li>
<li><a href="https://en.wikipedia.org/wiki/Loss_function">https://en.wikipedia.org/wiki/Loss_function</a> - wikipedia</li>
<li><a href="https://www.google.com/search?q=Loss+Function+Examples">https://www.google.com/search?q=Loss+Function+Examples</a> - More Examples</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h4 id="Home--|---Back--|---Next"><a href="#outline">Home</a>  |   <a href="#two">Back</a>  |   <a href="#four">Next</a><a class="anchor-link" href="#Home--|---Back--|---Next">&#182;</a></h4>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[9]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">x1</span> <span class="o">=</span> <span class="n">torch</span><span class="o">.</span><span class="n">Tensor</span><span class="p">([</span><span class="mi">1</span><span class="p">,</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">3</span><span class="p">,</span> <span class="mi">4</span><span class="p">])</span>
<span class="n">x1_var</span> <span class="o">=</span> <span class="n">Variable</span><span class="p">(</span><span class="n">x1</span><span class="p">,</span> <span class="n">requires_grad</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>

<span class="n">linear_layer1</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Linear</span><span class="p">(</span><span class="mi">4</span><span class="p">,</span> <span class="mi">1</span><span class="p">)</span>

<span class="n">target_y</span> <span class="o">=</span> <span class="n">Variable</span><span class="p">(</span><span class="n">torch</span><span class="o">.</span><span class="n">Tensor</span><span class="p">([</span><span class="mi">0</span><span class="p">]),</span> <span class="n">requires_grad</span><span class="o">=</span><span class="kc">False</span><span class="p">)</span>
<span class="c1"># ideally, we want our model to predict 0 when we input our x1_var variable below.</span>
<span class="c1"># here we&#39;re just sticking a Tensor with just 0 in it into a variable, and labeling it our target y value</span>
<span class="c1"># I put requires_grad=False because we&#39;re not computing any gradient with respect to our target (more on that later)</span>

<span class="n">predicted_y</span> <span class="o">=</span> <span class="n">linear_layer1</span><span class="p">(</span><span class="n">x1_var</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;----------------------------------------&quot;</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">predicted_y</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;----------------------------------------&quot;</span><span class="p">)</span>
<span class="c1"># prints 3.0995 for me; will probably be different for you.</span>

<span class="n">loss_function</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">MSELoss</span><span class="p">()</span>
<span class="c1"># this creates a function that takes a ground-truth Tensor and your model&#39;s output Tensor as inputs and calculates the &quot;loss&quot;</span>
<span class="c1"># in this case, it calculates the Mean Squared Error (a measurement for how far away your output is from where it should be)</span>

<span class="n">loss</span> <span class="o">=</span> <span class="n">loss_function</span><span class="p">(</span><span class="n">predicted_y</span><span class="p">,</span> <span class="n">target_y</span><span class="p">)</span>
<span class="c1"># here we actually use the function to compare our predicted_y vs our target_y</span>

<span class="nb">print</span><span class="p">(</span><span class="n">loss</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;----------------------------------------&quot;</span><span class="p">)</span>
<span class="c1"># prints 9.6067 for me; will probably be different for you. It&#39;s just (target_y - predicted_y)^2 in this case.</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">
<div class="prompt"></div>

<div class="output_subarea output_stream output_stdout output_text">
<pre>----------------------------------------
Variable containing:
-0.2311
[torch.FloatTensor of size 1]

----------------------------------------
Variable containing:
1.00000e-02 *
  5.3404
[torch.FloatTensor of size 1]

----------------------------------------
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><a id='four'></a></p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="4)--Calculating-Our-Gradient-(based-on-the-loss-function)">4)  Calculating Our Gradient (based on the loss function)<a class="anchor-link" href="#4)--Calculating-Our-Gradient-(based-on-the-loss-function)">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Links:</p>
<ul>
<li><a href="http://pytorch.org/tutorials/beginner/blitz/autograd_tutorial.html">http://pytorch.org/tutorials/beginner/blitz/autograd_tutorial.html</a> - pytorch's automatic gradient package</li>
<li><a href="https://discuss.pytorch.org/t/how-the-backward-works-for-torch-variable/907/3">https://discuss.pytorch.org/t/how-the-backward-works-for-torch-variable/907/3</a> - good discussion on pytorch forums</li>
<li><a href="https://www.khanacademy.org/math/multivariable-calculus/multivariable-derivatives/gradient-and-directional-derivatives/v/gradient">https://www.khanacademy.org/math/multivariable-calculus/multivariable-derivatives/gradient-and-directional-derivatives/v/gradient</a> - Khan Academy</li>
<li><a href="https://www.google.com/search?q=Machine+Learning+Gradient+Examples">https://www.google.com/search?q=Machine+Learning+Gradient+Examples</a> - More Examples</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h4 id="Home--|---Back--|---Next"><a href="#outline">Home</a>  |   <a href="#three">Back</a>  |   <a href="#five">Next</a><a class="anchor-link" href="#Home--|---Back--|---Next">&#182;</a></h4>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[10]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">x1</span> <span class="o">=</span> <span class="n">torch</span><span class="o">.</span><span class="n">Tensor</span><span class="p">([</span><span class="mi">1</span><span class="p">,</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">3</span><span class="p">,</span> <span class="mi">4</span><span class="p">])</span>
<span class="n">x1_var</span> <span class="o">=</span> <span class="n">Variable</span><span class="p">(</span><span class="n">x1</span><span class="p">,</span> <span class="n">requires_grad</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>

<span class="n">linear_layer1</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Linear</span><span class="p">(</span><span class="mi">4</span><span class="p">,</span> <span class="mi">1</span><span class="p">)</span>

<span class="n">target_y</span> <span class="o">=</span> <span class="n">Variable</span><span class="p">(</span><span class="n">torch</span><span class="o">.</span><span class="n">Tensor</span><span class="p">([</span><span class="mi">0</span><span class="p">]),</span> <span class="n">requires_grad</span><span class="o">=</span><span class="kc">False</span><span class="p">)</span>

<span class="n">predicted_y</span> <span class="o">=</span> <span class="n">linear_layer1</span><span class="p">(</span><span class="n">x1_var</span><span class="p">)</span>

<span class="n">loss_function</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">MSELoss</span><span class="p">()</span>

<span class="n">loss</span> <span class="o">=</span> <span class="n">loss_function</span><span class="p">(</span><span class="n">predicted_y</span><span class="p">,</span> <span class="n">target_y</span><span class="p">)</span>

<span class="c1"># at this point, we want the gradient of our loss function with respect to our original input, x</span>
<span class="c1"># the Variable object we put our Tensor in is supposed to store its respective gradients, so let&#39;s look:</span>

<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;----------------------------------------&quot;</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">x1_var</span><span class="o">.</span><span class="n">grad</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;----------------------------------------&quot;</span><span class="p">)</span>

<span class="c1"># this prints None, because we haven&#39;t computed any gradients yet.</span>
<span class="c1"># we have to call the backward() function from our loss results in order to compute gradients with respect to x</span>

<span class="n">loss</span><span class="o">.</span><span class="n">backward</span><span class="p">()</span>
<span class="nb">print</span><span class="p">(</span><span class="n">x1_var</span><span class="o">.</span><span class="n">grad</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;----------------------------------------&quot;</span><span class="p">)</span>
<span class="c1"># This is the gradient Tensor that holds the partial derivatives of our loss function with respect to each entry in x1</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">
<div class="prompt"></div>

<div class="output_subarea output_stream output_stdout output_text">
<pre>----------------------------------------
None
----------------------------------------
Variable containing:
-0.7361
-1.0644
 1.4180
 1.2542
[torch.FloatTensor of size 4]

----------------------------------------
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><a id='five'></a></p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="5)--Recalculating/Updating-Our-Weights-(based-on-the-gradient)">5)  Recalculating/Updating Our Weights (based on the gradient)<a class="anchor-link" href="#5)--Recalculating/Updating-Our-Weights-(based-on-the-gradient)">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Links:</p>
<ul>
<li><a href="http://pytorch.org/docs/master/optim.html">http://pytorch.org/docs/master/optim.html</a> - optimizer package documentation</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h4 id="Home--|---Back--|---Next"><a href="#outline">Home</a>  |   <a href="#four">Back</a>  |   <a href="#six">Next</a><a class="anchor-link" href="#Home--|---Back--|---Next">&#182;</a></h4>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[11]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">x1</span> <span class="o">=</span> <span class="n">torch</span><span class="o">.</span><span class="n">Tensor</span><span class="p">([</span><span class="mi">1</span><span class="p">,</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">3</span><span class="p">,</span> <span class="mi">4</span><span class="p">])</span>
<span class="n">x1_var</span> <span class="o">=</span> <span class="n">Variable</span><span class="p">(</span><span class="n">x1</span><span class="p">,</span> <span class="n">requires_grad</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>

<span class="n">linear_layer1</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Linear</span><span class="p">(</span><span class="mi">4</span><span class="p">,</span> <span class="mi">1</span><span class="p">)</span>

<span class="n">target_y</span> <span class="o">=</span> <span class="n">Variable</span><span class="p">(</span><span class="n">torch</span><span class="o">.</span><span class="n">Tensor</span><span class="p">([</span><span class="mi">0</span><span class="p">]),</span> <span class="n">requires_grad</span><span class="o">=</span><span class="kc">False</span><span class="p">)</span>

<span class="n">predicted_y</span> <span class="o">=</span> <span class="n">linear_layer1</span><span class="p">(</span><span class="n">x1_var</span><span class="p">)</span>

<span class="n">loss_function</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">MSELoss</span><span class="p">()</span>

<span class="n">loss</span> <span class="o">=</span> <span class="n">loss_function</span><span class="p">(</span><span class="n">predicted_y</span><span class="p">,</span> <span class="n">target_y</span><span class="p">)</span>

<span class="n">optimizer</span> <span class="o">=</span> <span class="n">optim</span><span class="o">.</span><span class="n">SGD</span><span class="p">(</span><span class="n">linear_layer1</span><span class="o">.</span><span class="n">parameters</span><span class="p">(),</span> <span class="n">lr</span><span class="o">=</span><span class="mf">1e-1</span><span class="p">)</span>
<span class="c1"># here we&#39;ve created an optimizer object that&#39;s responsible for changing the weights</span>
<span class="c1"># we told it which weights to change (those of our linear_layer1 model) and how much to change them (learning rate / lr)</span>
<span class="c1"># but we haven&#39;t quite told it to change anything yet. First we have to calculate the gradient.</span>

<span class="n">loss</span><span class="o">.</span><span class="n">backward</span><span class="p">()</span>

<span class="c1"># now that we have the gradient, let&#39;s look at our weights before we change them:</span>

<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;----------------------------------------&quot;</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Weights (before update):&quot;</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">linear_layer1</span><span class="o">.</span><span class="n">weight</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">linear_layer1</span><span class="o">.</span><span class="n">bias</span><span class="p">)</span>
<span class="c1"># let&#39;s also look at what our model predicts the output to be:</span>

<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;----------------------------------------&quot;</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Output (before update):&quot;</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">linear_layer1</span><span class="p">(</span><span class="n">x1_var</span><span class="p">))</span>

<span class="n">optimizer</span><span class="o">.</span><span class="n">step</span><span class="p">()</span>
<span class="c1"># we told the optimizer to subtract the learning rate * the gradient from our model weights</span>

<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;----------------------------------------&quot;</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Weights (after update):&quot;</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">linear_layer1</span><span class="o">.</span><span class="n">weight</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">linear_layer1</span><span class="o">.</span><span class="n">bias</span><span class="p">)</span>

<span class="c1"># looks like our weights and biases changed. How do we know they changed for the better?</span>
<span class="c1"># let&#39;s also look at what our model predicts the output to be now:</span>

<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;----------------------------------------&quot;</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Output (after update):&quot;</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">linear_layer1</span><span class="p">(</span><span class="n">x1_var</span><span class="p">))</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;----------------------------------------&quot;</span><span class="p">)</span>

<span class="c1"># wow, that&#39;s a huge change (at least for me, and probably for you). It looks like our learning rate might be too high.</span>
<span class="c1"># perhaps we want to make our model learn slower, compensating with more than one weight update?</span>
<span class="c1"># next section!</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">
<div class="prompt"></div>

<div class="output_subarea output_stream output_stdout output_text">
<pre>----------------------------------------
Weights (before update):
Parameter containing:
 0.1946  0.4250 -0.4268  0.2506
[torch.FloatTensor of size 1x4]

Parameter containing:
-0.1696
[torch.FloatTensor of size 1]

----------------------------------------
Output (before update):
Variable containing:
 0.5969
[torch.FloatTensor of size 1]

----------------------------------------
Weights (after update):
Parameter containing:
 0.0752  0.1862 -0.7849 -0.2269
[torch.FloatTensor of size 1x4]

Parameter containing:
-0.2890
[torch.FloatTensor of size 1]

----------------------------------------
Output (after update):
Variable containing:
-3.1037
[torch.FloatTensor of size 1]

----------------------------------------
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><a id='six'></a></p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="6)--Updating-Our-Weights-More-Than-Once-(i.e.-doing-step-3-6-a-few-times-aka-&quot;epochs&quot;)">6)  Updating Our Weights More Than Once (i.e. doing step 3-6 a few times aka "epochs")<a class="anchor-link" href="#6)--Updating-Our-Weights-More-Than-Once-(i.e.-doing-step-3-6-a-few-times-aka-&quot;epochs&quot;)">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Links:</p>
<ul>
<li><a href="https://wiki.python.org/moin/ForLoop">https://wiki.python.org/moin/ForLoop</a> - for loops in python</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h4 id="Home--|---Back--|---Next"><a href="#outline">Home</a>  |   <a href="#five">Back</a>  |   <a href="#seven">Next</a><a class="anchor-link" href="#Home--|---Back--|---Next">&#182;</a></h4>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[12]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># this block of code is organized a little differently than section 5, but it&#39;s mostly the same code</span>
<span class="c1"># the only three differences are:</span>
<span class="c1"># - The &quot;Hyperparameter&quot; constants</span>
<span class="c1"># - The for loop (for helping the model do &lt;number of epochs&gt; training steps)</span>
<span class="c1"># - The linear_layer1.zero_grad() function call on line 25. </span>
<span class="c1">#   (that&#39;s just to clear the gradients in memory, since we&#39;re starting the training over each iteration/epoch)</span>

<span class="n">x1</span> <span class="o">=</span> <span class="n">torch</span><span class="o">.</span><span class="n">Tensor</span><span class="p">([</span><span class="mi">1</span><span class="p">,</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">3</span><span class="p">,</span> <span class="mi">4</span><span class="p">])</span>
<span class="n">x1_var</span> <span class="o">=</span> <span class="n">Variable</span><span class="p">(</span><span class="n">x1</span><span class="p">,</span> <span class="n">requires_grad</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>

<span class="n">linear_layer1</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Linear</span><span class="p">(</span><span class="mi">4</span><span class="p">,</span> <span class="mi">1</span><span class="p">)</span>

<span class="n">target_y</span> <span class="o">=</span> <span class="n">Variable</span><span class="p">(</span><span class="n">torch</span><span class="o">.</span><span class="n">Tensor</span><span class="p">([</span><span class="mi">0</span><span class="p">]),</span> <span class="n">requires_grad</span><span class="o">=</span><span class="kc">False</span><span class="p">)</span>

<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;----------------------------------------&quot;</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Output (BEFORE UPDATE):&quot;</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">linear_layer1</span><span class="p">(</span><span class="n">x1_var</span><span class="p">))</span>

<span class="n">NUMBER_OF_EPOCHS</span> <span class="o">=</span> <span class="mi">3</span> <span class="c1"># Number of times to update the weights</span>
<span class="n">LEARNING_RATE</span> <span class="o">=</span> <span class="mf">1e-4</span> <span class="c1"># Notice how I made the learning rate 1000 times smaller</span>
<span class="n">loss_function</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">MSELoss</span><span class="p">()</span>
<span class="n">optimizer</span> <span class="o">=</span> <span class="n">optim</span><span class="o">.</span><span class="n">SGD</span><span class="p">(</span><span class="n">linear_layer1</span><span class="o">.</span><span class="n">parameters</span><span class="p">(),</span> <span class="n">lr</span><span class="o">=</span><span class="n">LEARNING_RATE</span><span class="p">)</span>

<span class="k">for</span> <span class="n">epoch</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">NUMBER_OF_EPOCHS</span><span class="p">):</span>
    <span class="n">linear_layer1</span><span class="o">.</span><span class="n">zero_grad</span><span class="p">()</span>
    <span class="n">predicted_y</span> <span class="o">=</span> <span class="n">linear_layer1</span><span class="p">(</span><span class="n">x1_var</span><span class="p">)</span>
    <span class="n">loss</span> <span class="o">=</span> <span class="n">loss_function</span><span class="p">(</span><span class="n">predicted_y</span><span class="p">,</span> <span class="n">target_y</span><span class="p">)</span>
    <span class="n">loss</span><span class="o">.</span><span class="n">backward</span><span class="p">()</span>
    <span class="n">optimizer</span><span class="o">.</span><span class="n">step</span><span class="p">()</span>
    
    <span class="nb">print</span><span class="p">(</span><span class="s2">&quot;----------------------------------------&quot;</span><span class="p">)</span>
    <span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Output (UPDATE &quot;</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">epoch</span> <span class="o">+</span> <span class="mi">1</span><span class="p">)</span> <span class="o">+</span> <span class="s2">&quot;):&quot;</span><span class="p">)</span>
    <span class="nb">print</span><span class="p">(</span><span class="n">linear_layer1</span><span class="p">(</span><span class="n">x1_var</span><span class="p">))</span>
    <span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Should be getting closer to 0...&quot;</span><span class="p">)</span>

<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;----------------------------------------&quot;</span><span class="p">)</span>

<span class="c1"># here is where you might discover that training could take a *long* time</span>
<span class="c1"># we&#39;re barely doing anything, computationally speaking, and it&#39;s already scaling up</span>
<span class="c1"># in the next section, we&#39;re going to add more data (other than one sample with 4 features), </span>
<span class="c1"># and then, with each epoch, we&#39;re only going to use a small portion of it (called a &quot;batch&quot;).</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">
<div class="prompt"></div>

<div class="output_subarea output_stream output_stdout output_text">
<pre>----------------------------------------
Output (BEFORE UPDATE):
Variable containing:
-2.9463
[torch.FloatTensor of size 1]

----------------------------------------
Output (UPDATE 1):
Variable containing:
-2.9281
[torch.FloatTensor of size 1]

Should be getting closer to 0...
----------------------------------------
Output (UPDATE 2):
Variable containing:
-2.9099
[torch.FloatTensor of size 1]

Should be getting closer to 0...
----------------------------------------
Output (UPDATE 3):
Variable containing:
-2.8919
[torch.FloatTensor of size 1]

Should be getting closer to 0...
----------------------------------------
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><a id='seven'></a></p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="7)--Making-Our-Epochs-Only-Use-A-Subset-Of-The-Data-(i.e.-a-&quot;batch&quot;)">7)  Making Our Epochs Only Use A Subset Of The Data (i.e. a "batch")<a class="anchor-link" href="#7)--Making-Our-Epochs-Only-Use-A-Subset-Of-The-Data-(i.e.-a-&quot;batch&quot;)">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Links:</p>
<ul>
<li><a href="https://discuss.pytorch.org/t/zero-grad-optimizer-or-net/1887">https://discuss.pytorch.org/t/zero-grad-optimizer-or-net/1887</a> - good discussion on pytorch forums</li>
<li><a href="https://stats.stackexchange.com/questions/49528/batch-gradient-descent-versus-stochastic-gradient-descent">https://stats.stackexchange.com/questions/49528/batch-gradient-descent-versus-stochastic-gradient-descent</a> - good SE post</li>
<li><a href="http://pytorch.org/docs/master/data.html">http://pytorch.org/docs/master/data.html</a> - data utilities pytorch documentation</li>
<li><a href="http://pytorch.org/tutorials/beginner/data_loading_tutorial.html">http://pytorch.org/tutorials/beginner/data_loading_tutorial.html</a> - pytorch's data loading and processing tutorial</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h4 id="Home--|---Back--|---Next"><a href="#outline">Home</a>  |   <a href="#six">Back</a>  |   <a href="#eight">Next</a><a class="anchor-link" href="#Home--|---Back--|---Next">&#182;</a></h4>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[13]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">x</span> <span class="o">=</span> <span class="n">torch</span><span class="o">.</span><span class="n">Tensor</span><span class="p">([[</span><span class="mi">0</span><span class="p">,</span> <span class="mi">0</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">1</span><span class="p">],</span>
                 <span class="p">[</span><span class="mi">0</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">0</span><span class="p">],</span>
                 <span class="p">[</span><span class="mi">1</span><span class="p">,</span> <span class="mi">0</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">0</span><span class="p">],</span>
                 <span class="p">[</span><span class="mi">1</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">1</span><span class="p">]])</span>
<span class="n">target_y</span> <span class="o">=</span> <span class="n">torch</span><span class="o">.</span><span class="n">Tensor</span><span class="p">([</span><span class="mi">0</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">0</span><span class="p">])</span>
<span class="c1"># now, instead of having 1 data sample, we have 4 (oh yea, now we&#39;re in the big leagues)</span>
<span class="c1"># but, pytorch has a DataLoader class to help us scale up, so let&#39;s use that.</span>

<span class="n">inputs</span> <span class="o">=</span> <span class="n">x</span> <span class="c1"># let&#39;s use the same naming convention as the pytorch documentation here</span>
<span class="n">labels</span> <span class="o">=</span> <span class="n">target_y</span> <span class="c1"># and here</span>

<span class="n">train</span> <span class="o">=</span> <span class="n">TensorDataset</span><span class="p">(</span><span class="n">inputs</span><span class="p">,</span> <span class="n">labels</span><span class="p">)</span> <span class="c1"># here we&#39;re just putting our data samples into a tiny Tensor dataset</span>

<span class="n">trainloader</span> <span class="o">=</span> <span class="n">DataLoader</span><span class="p">(</span><span class="n">train</span><span class="p">,</span> <span class="n">batch_size</span><span class="o">=</span><span class="mi">2</span><span class="p">,</span> <span class="n">shuffle</span><span class="o">=</span><span class="kc">False</span><span class="p">)</span> <span class="c1"># and then putting the dataset above into a data loader</span>
<span class="c1"># the batchsize=2 option just means that, later, when we iterate over it, we want to run our model on 2 samples at a time</span>

<span class="n">linear_layer1</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Linear</span><span class="p">(</span><span class="mi">4</span><span class="p">,</span> <span class="mi">1</span><span class="p">)</span>

<span class="n">NUMBER_OF_EPOCHS</span> <span class="o">=</span> <span class="mi">3</span>
<span class="n">LEARNING_RATE</span> <span class="o">=</span> <span class="mf">1e-4</span>
<span class="n">loss_function</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">MSELoss</span><span class="p">()</span>
<span class="n">optimizer</span> <span class="o">=</span> <span class="n">optim</span><span class="o">.</span><span class="n">SGD</span><span class="p">(</span><span class="n">linear_layer1</span><span class="o">.</span><span class="n">parameters</span><span class="p">(),</span> <span class="n">lr</span><span class="o">=</span><span class="n">LEARNING_RATE</span><span class="p">)</span>

<span class="k">for</span> <span class="n">epoch</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">NUMBER_OF_EPOCHS</span><span class="p">):</span>
    <span class="n">train_loader_iter</span> <span class="o">=</span> <span class="nb">iter</span><span class="p">(</span><span class="n">trainloader</span><span class="p">)</span> <span class="c1"># here&#39;s the iterator we use to iterate over our training set</span>
    <span class="k">for</span> <span class="n">batch_idx</span><span class="p">,</span> <span class="p">(</span><span class="n">inputs</span><span class="p">,</span> <span class="n">labels</span><span class="p">)</span> <span class="ow">in</span> <span class="nb">enumerate</span><span class="p">(</span><span class="n">train_loader_iter</span><span class="p">):</span> <span class="c1"># here we split apart our data so we can run it</span>
        <span class="n">linear_layer1</span><span class="o">.</span><span class="n">zero_grad</span><span class="p">()</span>
        <span class="n">inputs</span><span class="p">,</span> <span class="n">labels</span> <span class="o">=</span> <span class="n">Variable</span><span class="p">(</span><span class="n">inputs</span><span class="o">.</span><span class="n">float</span><span class="p">()),</span> <span class="n">Variable</span><span class="p">(</span><span class="n">labels</span><span class="o">.</span><span class="n">float</span><span class="p">())</span>
        <span class="n">predicted_y</span> <span class="o">=</span> <span class="n">linear_layer1</span><span class="p">(</span><span class="n">inputs</span><span class="p">)</span>
        <span class="n">loss</span> <span class="o">=</span> <span class="n">loss_function</span><span class="p">(</span><span class="n">predicted_y</span><span class="p">,</span> <span class="n">labels</span><span class="p">)</span>
        <span class="n">loss</span><span class="o">.</span><span class="n">backward</span><span class="p">()</span>
        <span class="n">optimizer</span><span class="o">.</span><span class="n">step</span><span class="p">()</span>
        <span class="nb">print</span><span class="p">(</span><span class="s2">&quot;----------------------------------------&quot;</span><span class="p">)</span>
        <span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Output (UPDATE: Epoch #&quot;</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">epoch</span> <span class="o">+</span> <span class="mi">1</span><span class="p">)</span> <span class="o">+</span> <span class="s2">&quot;, Batch #&quot;</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">batch_idx</span> <span class="o">+</span> <span class="mi">1</span><span class="p">)</span> <span class="o">+</span> <span class="s2">&quot;):&quot;</span><span class="p">)</span>
        <span class="nb">print</span><span class="p">(</span><span class="n">linear_layer1</span><span class="p">(</span><span class="n">Variable</span><span class="p">(</span><span class="n">x</span><span class="p">)))</span>
        <span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Should be getting closer to [0, 1, 1, 0]...&quot;</span><span class="p">)</span> <span class="c1"># but some of them aren&#39;t! we need a model that fits better...</span>
                                                             <span class="c1"># next up, we&#39;ll convert this model from regression to a NN</span>

<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;----------------------------------------&quot;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">
<div class="prompt"></div>

<div class="output_subarea output_stream output_stdout output_text">
<pre>----------------------------------------
Output (UPDATE: Epoch #1, Batch #1):
Variable containing:
-0.3699
 0.1028
 0.0181
 0.2637
[torch.FloatTensor of size 4x1]

Should be getting closer to [0, 1, 1, 0]...
----------------------------------------
Output (UPDATE: Epoch #1, Batch #2):
Variable containing:
-0.3698
 0.1030
 0.0184
 0.2639
[torch.FloatTensor of size 4x1]

Should be getting closer to [0, 1, 1, 0]...
----------------------------------------
Output (UPDATE: Epoch #2, Batch #1):
Variable containing:
-0.3695
 0.1033
 0.0186
 0.2643
[torch.FloatTensor of size 4x1]

Should be getting closer to [0, 1, 1, 0]...
----------------------------------------
Output (UPDATE: Epoch #2, Batch #2):
Variable containing:
-0.3694
 0.1034
 0.0188
 0.2644
[torch.FloatTensor of size 4x1]

Should be getting closer to [0, 1, 1, 0]...
----------------------------------------
Output (UPDATE: Epoch #3, Batch #1):
Variable containing:
-0.3691
 0.1038
 0.0191
 0.2648
[torch.FloatTensor of size 4x1]

Should be getting closer to [0, 1, 1, 0]...
----------------------------------------
Output (UPDATE: Epoch #3, Batch #2):
Variable containing:
-0.3690
 0.1039
 0.0193
 0.2650
[torch.FloatTensor of size 4x1]

Should be getting closer to [0, 1, 1, 0]...
----------------------------------------
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><a id='eight'></a></p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="8)--Changing-Our-Model-from-Linear-Regression-to-Neural-Network-(to-make-it-fit-the-data-better)">8)  Changing Our Model from Linear Regression to Neural Network (to make it fit the data better)<a class="anchor-link" href="#8)--Changing-Our-Model-from-Linear-Regression-to-Neural-Network-(to-make-it-fit-the-data-better)">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Links:</p>
<ul>
<li><a href="https://www.youtube.com/watch?v=aircAruvnKk">https://www.youtube.com/watch?v=aircAruvnKk</a> - Good video on what a neural network is (3blue1brown)</li>
<li><a href="http://neuralnetworksanddeeplearning.com">http://neuralnetworksanddeeplearning.com</a> - Good online book on neural networks</li>
<li><a href="https://www.deeplearningbook.org">https://www.deeplearningbook.org</a> - <em>The</em> deep learning book</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h4 id="Home--|---Back--|---Next"><a href="#outline">Home</a>  |   <a href="#seven">Back</a>  |   <a href="#nine">Next</a><a class="anchor-link" href="#Home--|---Back--|---Next">&#182;</a></h4>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[14]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">x</span> <span class="o">=</span> <span class="n">torch</span><span class="o">.</span><span class="n">Tensor</span><span class="p">([[</span><span class="mi">0</span><span class="p">,</span> <span class="mi">0</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">1</span><span class="p">],</span>
                 <span class="p">[</span><span class="mi">0</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">0</span><span class="p">],</span>
                 <span class="p">[</span><span class="mi">1</span><span class="p">,</span> <span class="mi">0</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">0</span><span class="p">],</span>
                 <span class="p">[</span><span class="mi">1</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">1</span><span class="p">]])</span>
<span class="n">target_y</span> <span class="o">=</span> <span class="n">torch</span><span class="o">.</span><span class="n">Tensor</span><span class="p">([</span><span class="mi">0</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">0</span><span class="p">])</span>

<span class="n">inputs</span> <span class="o">=</span> <span class="n">x</span>
<span class="n">labels</span> <span class="o">=</span> <span class="n">target_y</span>

<span class="n">train</span> <span class="o">=</span> <span class="n">TensorDataset</span><span class="p">(</span><span class="n">inputs</span><span class="p">,</span> <span class="n">labels</span><span class="p">)</span>
<span class="n">trainloader</span> <span class="o">=</span> <span class="n">DataLoader</span><span class="p">(</span><span class="n">train</span><span class="p">,</span> <span class="n">batch_size</span><span class="o">=</span><span class="mi">4</span><span class="p">,</span> <span class="n">shuffle</span><span class="o">=</span><span class="kc">False</span><span class="p">)</span>

<span class="n">linear_layer1</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Linear</span><span class="p">(</span><span class="mi">4</span><span class="p">,</span> <span class="mi">2</span><span class="p">)</span>
<span class="n">sigmoid</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Sigmoid</span><span class="p">()</span> <span class="c1"># this is the nonlinearity that we pass the output from layers 1 and 2 into</span>
<span class="n">linear_layer2</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Linear</span><span class="p">(</span><span class="mi">2</span><span class="p">,</span> <span class="mi">1</span><span class="p">)</span> <span class="c1"># this is our second layer (i.e. we&#39;re going to pass the outputs from sigmoid into here)</span>

<span class="n">NUMBER_OF_EPOCHS</span> <span class="o">=</span> <span class="mi">3</span>
<span class="n">LEARNING_RATE</span> <span class="o">=</span> <span class="mf">1e-1</span> <span class="c1"># increased learning rate to make learning more obvious</span>
<span class="n">loss_function</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">MSELoss</span><span class="p">()</span>
<span class="n">optimizer</span> <span class="o">=</span> <span class="n">optim</span><span class="o">.</span><span class="n">SGD</span><span class="p">(</span><span class="n">linear_layer1</span><span class="o">.</span><span class="n">parameters</span><span class="p">(),</span> <span class="n">lr</span><span class="o">=</span><span class="n">LEARNING_RATE</span><span class="p">)</span>

<span class="k">for</span> <span class="n">epoch</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">NUMBER_OF_EPOCHS</span><span class="p">):</span>
    <span class="n">train_loader_iter</span> <span class="o">=</span> <span class="nb">iter</span><span class="p">(</span><span class="n">trainloader</span><span class="p">)</span>
    <span class="k">for</span> <span class="n">batch_idx</span><span class="p">,</span> <span class="p">(</span><span class="n">inputs</span><span class="p">,</span> <span class="n">labels</span><span class="p">)</span> <span class="ow">in</span> <span class="nb">enumerate</span><span class="p">(</span><span class="n">train_loader_iter</span><span class="p">):</span>
        <span class="n">linear_layer1</span><span class="o">.</span><span class="n">zero_grad</span><span class="p">()</span>
        <span class="n">inputs</span><span class="p">,</span> <span class="n">labels</span> <span class="o">=</span> <span class="n">Variable</span><span class="p">(</span><span class="n">inputs</span><span class="o">.</span><span class="n">float</span><span class="p">()),</span> <span class="n">Variable</span><span class="p">(</span><span class="n">labels</span><span class="o">.</span><span class="n">float</span><span class="p">())</span>
        
        <span class="n">linear_layer1_output</span> <span class="o">=</span> <span class="n">linear_layer1</span><span class="p">(</span><span class="n">inputs</span><span class="p">)</span>
        <span class="n">sigmoid_output</span> <span class="o">=</span> <span class="n">sigmoid</span><span class="p">(</span><span class="n">linear_layer1_output</span><span class="p">)</span>
        <span class="n">linear_layer2_output</span> <span class="o">=</span> <span class="n">linear_layer2</span><span class="p">(</span><span class="n">sigmoid_output</span><span class="p">)</span>
        <span class="n">sigmoid_output_2</span> <span class="o">=</span> <span class="n">sigmoid</span><span class="p">(</span><span class="n">linear_layer2_output</span><span class="p">)</span> <span class="c1"># see how the output from one layer just goes into the second?</span>
        
        <span class="n">loss</span> <span class="o">=</span> <span class="n">loss_function</span><span class="p">(</span><span class="n">sigmoid_output_2</span><span class="p">,</span> <span class="n">labels</span><span class="p">)</span>
        <span class="n">loss</span><span class="o">.</span><span class="n">backward</span><span class="p">()</span>
        <span class="n">optimizer</span><span class="o">.</span><span class="n">step</span><span class="p">()</span>
        <span class="nb">print</span><span class="p">(</span><span class="s2">&quot;----------------------------------------&quot;</span><span class="p">)</span>
        <span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Output (UPDATE: Epoch #&quot;</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">epoch</span> <span class="o">+</span> <span class="mi">1</span><span class="p">)</span> <span class="o">+</span> <span class="s2">&quot;, Batch #&quot;</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">batch_idx</span> <span class="o">+</span> <span class="mi">1</span><span class="p">)</span> <span class="o">+</span> <span class="s2">&quot;):&quot;</span><span class="p">)</span>
        <span class="nb">print</span><span class="p">(</span><span class="n">sigmoid</span><span class="p">(</span><span class="n">linear_layer2</span><span class="p">(</span><span class="n">sigmoid</span><span class="p">(</span><span class="n">linear_layer1</span><span class="p">(</span><span class="n">Variable</span><span class="p">(</span><span class="n">x</span><span class="p">))))))</span> <span class="c1"># the nested functions are getting out of hand..</span>
        <span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Should be getting closer to [0, 1, 1, 0]...&quot;</span><span class="p">)</span> <span class="c1"># they are if you increase the epochs amount... but it&#39;s slow!</span>

<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;----------------------------------------&quot;</span><span class="p">)</span>

<span class="c1"># Awesome, so we have a neural network (nn). But the nested functions and all the layers are starting to get bloated.</span>
<span class="c1"># Time to refactor. Luckily, PyTorch provides a class specifically for this: the Net class. We&#39;ll port our code there next.</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">
<div class="prompt"></div>

<div class="output_subarea output_stream output_stdout output_text">
<pre>----------------------------------------
Output (UPDATE: Epoch #1, Batch #1):
Variable containing:
 0.2646
 0.2660
 0.2698
 0.2578
[torch.FloatTensor of size 4x1]

Should be getting closer to [0, 1, 1, 0]...
----------------------------------------
Output (UPDATE: Epoch #2, Batch #1):
Variable containing:
 0.2646
 0.2661
 0.2699
 0.2579
[torch.FloatTensor of size 4x1]

Should be getting closer to [0, 1, 1, 0]...
----------------------------------------
Output (UPDATE: Epoch #3, Batch #1):
Variable containing:
 0.2647
 0.2662
 0.2700
 0.2580
[torch.FloatTensor of size 4x1]

Should be getting closer to [0, 1, 1, 0]...
----------------------------------------
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><a id='nine'></a></p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="9)-Abstracting-our-Neural-Network-into-its-PyTorch-class-(i.e.-making-it-more-maintainable-and-less-messy)">9) Abstracting our Neural Network into its PyTorch class (i.e. making it more maintainable and less messy)<a class="anchor-link" href="#9)-Abstracting-our-Neural-Network-into-its-PyTorch-class-(i.e.-making-it-more-maintainable-and-less-messy)">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Links:</p>
<ul>
<li><a href="http://pytorch.org/tutorials/beginner/blitz/neural_networks_tutorial.html">http://pytorch.org/tutorials/beginner/blitz/neural_networks_tutorial.html</a> - pytorch neural network tutorial</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h4 id="Home--|---Back--|---Next"><a href="#outline">Home</a>  |   <a href="#eight">Back</a>  |   <a href="#ten">Next</a><a class="anchor-link" href="#Home--|---Back--|---Next">&#182;</a></h4>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[15]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">x</span> <span class="o">=</span> <span class="n">torch</span><span class="o">.</span><span class="n">Tensor</span><span class="p">([[</span><span class="mi">0</span><span class="p">,</span> <span class="mi">0</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">1</span><span class="p">],</span>
                 <span class="p">[</span><span class="mi">0</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">0</span><span class="p">],</span>
                 <span class="p">[</span><span class="mi">1</span><span class="p">,</span> <span class="mi">0</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">0</span><span class="p">],</span>
                 <span class="p">[</span><span class="mi">1</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">1</span><span class="p">]])</span>
<span class="n">target_y</span> <span class="o">=</span> <span class="n">torch</span><span class="o">.</span><span class="n">Tensor</span><span class="p">([</span><span class="mi">0</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">0</span><span class="p">])</span>

<span class="n">inputs</span> <span class="o">=</span> <span class="n">x</span>
<span class="n">labels</span> <span class="o">=</span> <span class="n">target_y</span>

<span class="n">train</span> <span class="o">=</span> <span class="n">TensorDataset</span><span class="p">(</span><span class="n">inputs</span><span class="p">,</span> <span class="n">labels</span><span class="p">)</span>
<span class="n">trainloader</span> <span class="o">=</span> <span class="n">DataLoader</span><span class="p">(</span><span class="n">train</span><span class="p">,</span> <span class="n">batch_size</span><span class="o">=</span><span class="mi">4</span><span class="p">,</span> <span class="n">shuffle</span><span class="o">=</span><span class="kc">False</span><span class="p">)</span>

<span class="k">class</span> <span class="nc">Net</span><span class="p">(</span><span class="n">nn</span><span class="o">.</span><span class="n">Module</span><span class="p">):</span>
    <span class="k">def</span> <span class="nf">__init__</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>
        <span class="nb">super</span><span class="p">(</span><span class="n">Net</span><span class="p">,</span> <span class="bp">self</span><span class="p">)</span><span class="o">.</span><span class="fm">__init__</span><span class="p">()</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">fc1</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Linear</span><span class="p">(</span><span class="mi">4</span><span class="p">,</span> <span class="mi">2</span><span class="p">)</span> <span class="c1"># here&#39;s where we define the same layers we had earlier</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">fc2</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Linear</span><span class="p">(</span><span class="mi">2</span><span class="p">,</span> <span class="mi">1</span><span class="p">)</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">sigmoid</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Sigmoid</span><span class="p">()</span>

    <span class="k">def</span> <span class="nf">forward</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">x</span><span class="p">):</span>
        <span class="n">x</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">fc1</span><span class="p">(</span><span class="n">x</span><span class="p">)</span> <span class="c1"># the forward function just sends everything through its respective layers</span>
        <span class="n">x</span> <span class="o">=</span> <span class="n">sigmoid</span><span class="p">(</span><span class="n">x</span><span class="p">)</span> <span class="c1"># including through the sigmoids after each Linear layer</span>
        <span class="n">x</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">fc2</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>
        <span class="n">x</span> <span class="o">=</span> <span class="n">sigmoid</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>
        <span class="k">return</span> <span class="n">x</span>

<span class="n">net</span> <span class="o">=</span> <span class="n">Net</span><span class="p">()</span> <span class="c1"># we made a blueprint above for our neural network, now we initialize one.</span>

<span class="n">NUMBER_OF_EPOCHS</span> <span class="o">=</span> <span class="mi">3</span>
<span class="n">LEARNING_RATE</span> <span class="o">=</span> <span class="mf">1e-1</span>
<span class="n">loss_function</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">MSELoss</span><span class="p">()</span>
<span class="n">optimizer</span> <span class="o">=</span> <span class="n">optim</span><span class="o">.</span><span class="n">SGD</span><span class="p">(</span><span class="n">net</span><span class="o">.</span><span class="n">parameters</span><span class="p">(),</span> <span class="n">lr</span><span class="o">=</span><span class="n">LEARNING_RATE</span><span class="p">)</span> <span class="c1"># slight difference: we optimize w.r.t. the net parameters now</span>

<span class="k">for</span> <span class="n">epoch</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">NUMBER_OF_EPOCHS</span><span class="p">):</span>
    <span class="n">train_loader_iter</span> <span class="o">=</span> <span class="nb">iter</span><span class="p">(</span><span class="n">trainloader</span><span class="p">)</span>
    <span class="k">for</span> <span class="n">batch_idx</span><span class="p">,</span> <span class="p">(</span><span class="n">inputs</span><span class="p">,</span> <span class="n">labels</span><span class="p">)</span> <span class="ow">in</span> <span class="nb">enumerate</span><span class="p">(</span><span class="n">train_loader_iter</span><span class="p">):</span>
        <span class="n">net</span><span class="o">.</span><span class="n">zero_grad</span><span class="p">()</span> <span class="c1"># same here: we have to zero out the gradient for the neural network&#39;s inputs</span>
        <span class="n">inputs</span><span class="p">,</span> <span class="n">labels</span> <span class="o">=</span> <span class="n">Variable</span><span class="p">(</span><span class="n">inputs</span><span class="o">.</span><span class="n">float</span><span class="p">()),</span> <span class="n">Variable</span><span class="p">(</span><span class="n">labels</span><span class="o">.</span><span class="n">float</span><span class="p">())</span>
        <span class="n">output</span> <span class="o">=</span> <span class="n">net</span><span class="p">(</span><span class="n">inputs</span><span class="p">)</span> <span class="c1"># but now, all we have to do is pass our inputs to the neural net </span>
        
        <span class="n">loss</span> <span class="o">=</span> <span class="n">loss_function</span><span class="p">(</span><span class="n">output</span><span class="p">,</span> <span class="n">labels</span><span class="p">)</span>
        <span class="n">loss</span><span class="o">.</span><span class="n">backward</span><span class="p">()</span>
        <span class="n">optimizer</span><span class="o">.</span><span class="n">step</span><span class="p">()</span>
        <span class="nb">print</span><span class="p">(</span><span class="s2">&quot;----------------------------------------&quot;</span><span class="p">)</span>
        <span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Output (UPDATE: Epoch #&quot;</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">epoch</span> <span class="o">+</span> <span class="mi">1</span><span class="p">)</span> <span class="o">+</span> <span class="s2">&quot;, Batch #&quot;</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">batch_idx</span> <span class="o">+</span> <span class="mi">1</span><span class="p">)</span> <span class="o">+</span> <span class="s2">&quot;):&quot;</span><span class="p">)</span>
        <span class="nb">print</span><span class="p">(</span><span class="n">net</span><span class="p">(</span><span class="n">Variable</span><span class="p">(</span><span class="n">x</span><span class="p">)))</span> <span class="c1"># much better!</span>
        <span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Should be getting closer to [0, 1, 1, 0]...&quot;</span><span class="p">)</span>

<span class="nb">print</span><span class="p">(</span><span class="s2">&quot;----------------------------------------&quot;</span><span class="p">)</span>

<span class="c1"># Awesome, so we have a neural network (nn) in the actual PyTorch Net class.</span>
<span class="c1"># As it stands right now, there&#39;s tons of optimization that can be done here.</span>
<span class="c1"># But, at the risk of falling for premature optimization, let&#39;s get to the end and build our full-fledged CNN first.</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">
<div class="prompt"></div>

<div class="output_subarea output_stream output_stdout output_text">
<pre>----------------------------------------
Output (UPDATE: Epoch #1, Batch #1):
Variable containing:
 0.5994
 0.6015
 0.5958
 0.5919
[torch.FloatTensor of size 4x1]

Should be getting closer to [0, 1, 1, 0]...
----------------------------------------
Output (UPDATE: Epoch #2, Batch #1):
Variable containing:
 0.5982
 0.6003
 0.5945
 0.5907
[torch.FloatTensor of size 4x1]

Should be getting closer to [0, 1, 1, 0]...
----------------------------------------
Output (UPDATE: Epoch #3, Batch #1):
Variable containing:
 0.5969
 0.5991
 0.5933
 0.5895
[torch.FloatTensor of size 4x1]

Should be getting closer to [0, 1, 1, 0]...
----------------------------------------
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><a id='ten'></a></p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="10)--Changing-Our-Input-From-Arbitrary-Vectors-To-Images">10)  Changing Our Input From Arbitrary Vectors To Images<a class="anchor-link" href="#10)--Changing-Our-Input-From-Arbitrary-Vectors-To-Images">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Links:</p>
<ul>
<li><a href="http://pytorch.org/docs/master/data.html">http://pytorch.org/docs/master/data.html</a> - data utilities pytorch documentation</li>
<li><a href="http://pytorch.org/tutorials/beginner/data_loading_tutorial.html">http://pytorch.org/tutorials/beginner/data_loading_tutorial.html</a> - pytorch's data loading and processing tutorial</li>
<li><a href="http://pytorch.org/docs/master/torchvision/transforms.html">http://pytorch.org/docs/master/torchvision/transforms.html</a> - transforms documentation</li>
<li><a href="http://pytorch.org/tutorials/beginner/blitz/cifar10_tutorial.html">http://pytorch.org/tutorials/beginner/blitz/cifar10_tutorial.html</a> - pytorch's data classifier tutorial</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h4 id="Home--|---Back--|---Next"><a href="#outline">Home</a>  |   <a href="#nine">Back</a>  |   <a href="#eleven">Next</a><a class="anchor-link" href="#Home--|---Back--|---Next">&#182;</a></h4>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[16]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># In preparation for building our Convolutional Neural Network (CNN), we&#39;re going to stop using random, arbitrary vectors.</span>
<span class="c1"># Instead, we&#39;re going to use an actual standardized dataset: CIFAR-10</span>
<span class="c1"># We also have built in modules to help us load/wrangle the dataset, so we&#39;re going to use those too! (since we&#39;re spoiled)</span>

<span class="n">transform</span> <span class="o">=</span> <span class="n">transforms</span><span class="o">.</span><span class="n">Compose</span><span class="p">(</span> <span class="c1"># we&#39;re going to use this to transform our data to make each sample more uniform</span>
   <span class="p">[</span>
    <span class="n">transforms</span><span class="o">.</span><span class="n">ToTensor</span><span class="p">(),</span> <span class="c1"># converts each sample from a (0-255, 0-255, 0-255) PIL Image format to a (0-1, 0-1, 0-1) FloatTensor format</span>
    <span class="n">transforms</span><span class="o">.</span><span class="n">Normalize</span><span class="p">((</span><span class="mf">0.5</span><span class="p">,</span> <span class="mf">0.5</span><span class="p">,</span> <span class="mf">0.5</span><span class="p">),</span> <span class="p">(</span><span class="mf">0.5</span><span class="p">,</span> <span class="mf">0.5</span><span class="p">,</span> <span class="mf">0.5</span><span class="p">))</span> <span class="c1"># for each of the 3 channels of the image, subtract mean 0.5 and divide by stdev 0.5</span>
   <span class="p">])</span> <span class="c1"># the normalization makes each SGD iteration more stable and overall makes convergence easier</span>

<span class="n">trainset</span> <span class="o">=</span> <span class="n">torchvision</span><span class="o">.</span><span class="n">datasets</span><span class="o">.</span><span class="n">CIFAR10</span><span class="p">(</span><span class="n">root</span><span class="o">=</span><span class="s1">&#39;./data&#39;</span><span class="p">,</span> <span class="n">train</span><span class="o">=</span><span class="kc">True</span><span class="p">,</span>
                                        <span class="n">download</span><span class="o">=</span><span class="kc">True</span><span class="p">,</span> <span class="n">transform</span><span class="o">=</span><span class="n">transform</span><span class="p">)</span> <span class="c1"># this is all we need to get/wrangle the dataset!</span>
<span class="n">trainloader</span> <span class="o">=</span> <span class="n">torch</span><span class="o">.</span><span class="n">utils</span><span class="o">.</span><span class="n">data</span><span class="o">.</span><span class="n">DataLoader</span><span class="p">(</span><span class="n">trainset</span><span class="p">,</span> <span class="n">batch_size</span><span class="o">=</span><span class="mi">4</span><span class="p">,</span>
                                          <span class="n">shuffle</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>

<span class="n">testset</span> <span class="o">=</span> <span class="n">torchvision</span><span class="o">.</span><span class="n">datasets</span><span class="o">.</span><span class="n">CIFAR10</span><span class="p">(</span><span class="n">root</span><span class="o">=</span><span class="s1">&#39;./data&#39;</span><span class="p">,</span> <span class="n">train</span><span class="o">=</span><span class="kc">False</span><span class="p">,</span>
                                       <span class="n">download</span><span class="o">=</span><span class="kc">True</span><span class="p">,</span> <span class="n">transform</span><span class="o">=</span><span class="n">transform</span><span class="p">)</span>
<span class="n">testloader</span> <span class="o">=</span> <span class="n">torch</span><span class="o">.</span><span class="n">utils</span><span class="o">.</span><span class="n">data</span><span class="o">.</span><span class="n">DataLoader</span><span class="p">(</span><span class="n">testset</span><span class="p">,</span> <span class="n">batch_size</span><span class="o">=</span><span class="mi">4</span><span class="p">,</span>
                                         <span class="n">shuffle</span><span class="o">=</span><span class="kc">False</span><span class="p">)</span>

<span class="n">classes</span> <span class="o">=</span> <span class="p">(</span><span class="s1">&#39;plane&#39;</span><span class="p">,</span> <span class="s1">&#39;car&#39;</span><span class="p">,</span> <span class="s1">&#39;bird&#39;</span><span class="p">,</span> <span class="s1">&#39;cat&#39;</span><span class="p">,</span> <span class="s1">&#39;deer&#39;</span><span class="p">,</span> <span class="s1">&#39;dog&#39;</span><span class="p">,</span> <span class="s1">&#39;frog&#39;</span><span class="p">,</span> <span class="s1">&#39;horse&#39;</span><span class="p">,</span> <span class="s1">&#39;ship&#39;</span><span class="p">,</span> <span class="s1">&#39;truck&#39;</span><span class="p">)</span> <span class="c1"># each image can have 1 of 10 labels</span>

<span class="c1"># helper function to show an image</span>
<span class="k">def</span> <span class="nf">imshow</span><span class="p">(</span><span class="n">img</span><span class="p">):</span>
    <span class="n">img</span> <span class="o">=</span> <span class="n">img</span> <span class="o">/</span> <span class="mi">2</span> <span class="o">+</span> <span class="mf">0.5</span>     <span class="c1"># unnormalize</span>
    <span class="n">npimg</span> <span class="o">=</span> <span class="n">img</span><span class="o">.</span><span class="n">numpy</span><span class="p">()</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">imshow</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">transpose</span><span class="p">(</span><span class="n">npimg</span><span class="p">,</span> <span class="p">(</span><span class="mi">1</span><span class="p">,</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">0</span><span class="p">)))</span>

<span class="c1"># get some random training images</span>
<span class="n">dataiter</span> <span class="o">=</span> <span class="nb">iter</span><span class="p">(</span><span class="n">trainloader</span><span class="p">)</span>
<span class="n">images</span><span class="p">,</span> <span class="n">labels</span> <span class="o">=</span> <span class="n">dataiter</span><span class="o">.</span><span class="n">next</span><span class="p">()</span>

<span class="c1"># show images</span>
<span class="n">imshow</span><span class="p">(</span><span class="n">torchvision</span><span class="o">.</span><span class="n">utils</span><span class="o">.</span><span class="n">make_grid</span><span class="p">(</span><span class="n">images</span><span class="p">))</span>
<span class="c1"># print labels</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39; &#39;</span><span class="o">.</span><span class="n">join</span><span class="p">(</span><span class="s1">&#39;</span><span class="si">%5s</span><span class="s1">&#39;</span> <span class="o">%</span> <span class="n">classes</span><span class="p">[</span><span class="n">labels</span><span class="p">[</span><span class="n">j</span><span class="p">]]</span> <span class="k">for</span> <span class="n">j</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">4</span><span class="p">)))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">
<div class="prompt"></div>

<div class="output_subarea output_stream output_stdout output_text">
<pre>Files already downloaded and verified
Files already downloaded and verified
horse  bird  deer truck
</pre>
</div>
</div>

<div class="output_area">
<div class="prompt"></div>



<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAXQAAAB6CAYAAACvHqiXAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAALEgAACxIB0t1+/AAAADl0RVh0U29mdHdhcmUAbWF0cGxvdGxpYiB2ZXJzaW9uIDIuMS4wLCBodHRwOi8vbWF0cGxvdGxpYi5vcmcvpW3flQAAIABJREFUeJztvWmMJdl1Hvjd9+LtS+57rd1d1V3dTfbqJim1aEmULEqWRcOwZEq2RWAI9ACWMfbAwJgaQfAQ8A8bHtjyALYGhKURLQgiZUk2CdmSSTZFUivZG7t6qe6qrD0r98yXb18j7vw458Y5lVnZtTUrK1P3Awr56ka8iLtFvHPOdxZjrYWHh4eHx/5HYq874OHh4eHx/sC/0D08PDwOCPwL3cPDw+OAwL/QPTw8PA4I/Avdw8PD44DAv9A9PDw8Dgj8C93Dw8PjgOCuXujGmI8bY941xswbYz7zfnXKw8PDw+P2Ye40sMgYkwRwFsCPAlgA8BKAn7XWvv3+dc/Dw8PD41YR3MV3nwMwb629AADGmC8A+ASAXV/o+XzeDg8P38UtPTw8PP7qYWlpad1aO3Gz8+7mhT4H4Kr6/wKAD73XF4aHh/HCCy/cxS09PDw8/urhs5/97OVbOe9ubOjmBm077DfGmBeMMS8bY15utVp3cTsPDw8Pj/fC3bzQFwAcVv8/BGBx+0nW2s9Za5+11j6bz+fv4nYeHh4eHu+Fu3mhvwTghDHmuDEmDeCTAL78/nTLw8PDw+N2ccc2dGvtwBjzjwH8TwBJAL9urX3rdq/zM39vDgAQDtpxW9TvUOdU7yKE9DeKAADGyG/RIKS2hJVrZNN0PDKiFWxs0TUqtT5dPyE3qF4mOmDhzJm47annnwEAlI+MxW0G3LcEWZz6/b46RhYnmxRrlLEpuv6KnFfZ7AIAWuEAALDWWouP1VpN6vcgHbclkOMxFeO2XnMaGh8qn40/twc8R9Egbssa+pxKp+K2TsT37PZoTIEcywV0/2xCxpIK6Av9gRpLtU5j6dA1QtWnXqtG/bBR3FYqlQAA1VpVTmRDXZLvnyuU4kPHjhwDACSUMe/yhfN0/XZX+tGi8T3x1BMAgExW7rlwhcyPm2uVuG1ri8x/vYd/DtvxrVe+RscCuWk6RfvJqgEmEtTfVIr2Uasj+6/doHkp5bNxWypF5/d6vbit2Wzytej6yWRS7snzEar5SybpeoNI2gaDLl+D/h+k5BoIaQyZhOyn5mDA35PBJHjPhNwWpNTDx9NgtZE1TY3pdCZu+qEnfwwav/zLv6z6ncT3Et2ezP3WFu2t1bVVAECDnykAePThUwCAofL3xjmjWlmPPy9cuQRA9kcuJ3OV4HdPoSjPNJK0gL/yK796x/e/G1IU1tr/AeB/3M01PDw8PDzeH9zVC/39wMY6SU+hkvoiSxJEUollhTz9ukXMxXaVpNTu0X96HTn/2sUVAMDaZfnFvDJPJv7VVfoFLxbkF/ORAkkwJ4dEoppokuTT3mrEbTbN0g33YxDJPZMpukazJm2vv0qS87nTF+K2UmEIAJArFeicC0vxsUqd7mlCka4DlsaGSrm47YnnfgoaDZYIASDBUlM4UNco0ncvL56P21armwCAXkTbYGL8SHysnB0FAGRHlXaSYknQiGSc4flosaSZS4kkmC8O8THpW6dJklQ2kHl2UkplawsAsLwk85FiKfjwoUMyFh5fryd7ZqtCWs78WfKa/eCTj8fHIt7mJiXaWrNL9xKdRFAaJ+mtl5RNNhiwFqO0upDXPhGw9Km0iMDQPCSycocEz40SlpFK0D2SvMY6LiTIsMg9kLaBpX5YJfAm3O3dc5ORg/02zVGr3YnbIpbaRcYHeqzNDQ+X6RpKom40aM1sJCJ60qkDRl/lemjNwqluVxbEMa7epufKaW0AkOW1LRWU5MpYWqTn9+rVK3Hb/Pw8AODMO+/GbRcu0TtlbZWe/Y4a6U//3CcBAP/rP/j5uG20SPeP1Nwb48bq2nb6gISh7A+3FxauCo149uxFAEBhiK6fDEUzq/FeX6vL+6nec1rrjfxNbg0+9N/Dw8PjgMC/0D08PDwOCPbc5NJqEzkVGUUkBvQ7M1AqdZuJu3qdVPtqXcwgPTbX1Nqipv3FH5MKFl4WFWiKyYnZJBM6HVFD/8bzH6RzCnLPRkikXqcufeunk9wfukauOBUfGymTWeC//89vxW1f+M1vAgBmhkWt/LG/8QjdP0/3OjYzFB87NsumpYGoZ2mej+BG9gGGjUT9Gy6T2qyJx/Oshi6ti4oXMdE3wiaGRltMIwbUj0RVtsjIMLdZaWuyCSWVJDvCUL6gekXzloSo770+mWs0mTZUov72e6T2Ly6vxsdOnz4NAMgpl1dnculHtbgtn6M+OdPL+vqGOp++OzY9GrcVhyjoTgxQgi4znzYp8k4iSZOfSMhYgsT18lDGKgKUTS2RYlFDJsuTytxUztHnXpP2c6TMZBFfvm/kGr0u7RmrzBkB7498ntYglZF+JXmtuh3ZT333XAVynvMxCHh/B8ojIWq4e8rYMxm6Vzqt7Efb0OvIM7q5Qfvuv/7RH8Vt33mHzJGptNwrYLPH9DSR/lbN8eULZGpZWZU9vFkh00W/KcTngOcIbBIJQ5mrr/zJnwMApo4fj9v+zvMfBQAM3cDME8WmMGlz5pi6ege1maBfWZO+dZn87jI5m1Ym5MoWEfRvnTu7o+2BI6d29ONW4SV0Dw8PjwOCPZfQ1+v0K9ZUpE2XXQE7bZEqwjb9UiaZpCjkRDIoFUjCG86KFLc5SZLikaPPxm1Jdm16403yrhwtjcTHjj16EgBQ7S7EbStdkpbWWyIh9VlamZw+AQAYnxLy7cy79Ev8pf/+ilyDCVWjpJtLCyRVPPcR+u7CprjT9S1H0yoJqc7ucFrKekSETQDAk08/EX/udKiPkRGJIMOSc3lKiM8+Sx+jY3QstHL9Dq9HqyVS/labtIyU4mz6fIuAZYOUIkVj11IlZWUGLF0rd8/1jU3uN0k509Oz8bGNDZK0q1WRhtLsetlVbnelMo3BsvS0tr4pY+mzBFuSNZieIs3qvAhUMRotmod+R6RlJ5EGyjHTSWoxfaakOGuSfG+5hiM+E0ryD/gaWXbVTKi5ctJhsiskdNSl9QjV2N3lIt6vPX2MicykcvNNZ1jTyspaDVjDs84FWLneptmF1aZl/gpFmu9sVjSt7Xj1L0VTbbH29cobr8dt81eXaSxbIl2HvO+CUZqP7JBIzYbdPktM3ALALJ+3UpFnyJG+loecVOvS58373178StwWsCT/Mz/68bgty/vYsq9mGKr9ukKk/fKivCu6HRpDryH9KGZYQ+jTfur0ZB2TbC14+pQ8t2ke37uX5Lq3Cy+he3h4eBwQ+Be6h4eHxwHBnptcVtfIxNBvSuKuLJM1Q4o4K42TOaVUpC5ns4pIYUKuqyL1hobp+PghiaicnmPf8TH6u/nWtfjYNfb/bhTElrEVkvoUpEX9HB55GACQHyKTy7kFMRW9c57MA2GoiTP6vKUIlJdeexMAcPj4UQBApSXjXK2T/7wj+QAgFbiIRDGJbEe3K2N3PsQTk5Jts8o+9Rt1IT5f/+53AQA/8NHHAAC1+nJ8rBfR9UJFgHZ5iZKRjh6lvrkwgo2aqM95jpKs1YW8LDNhGyqTS5+JwzSbzEZKolIXi/S5qHyVM1m6bqsrc99s0PhqVbrXVl1MHakMqe1daUIqFmXEvOPg3IV7itB0JHVS+1azSSRI7SQG02yKsJHMX5+/WkpLPEGSI3FdJKomGZ35RccTJDi8N+yI+m5dP9lcYhUJ6PzmA0U89tnMY5UZBmxSCHi9ey3ZaxF33CpbG1uUEGF3P/TLG7IXIjaTLav91+WJLpVlPnJsYjEcd5JWngANNjkOIrlugs1AQwUxt+bZRBS2aH90+mosvFFbTKYCwB/9yZ8AAB7mqGQAePoRclwIo51zunKNTCKVVXl/uPnQUdHOeuZMyC6CFQAGvC46WrfijhshzW8XXkL38PDwOCDYcwl9mnOupAuSWyHNhIzOO8K8FmpNksAqNfkl7Pfo57Gqfv2RJ8JzQ/0CbnCUWn6SCZe+uByudkgaP7MopEaGpYVDh+S8oPAgAODKCjEti0sieX/9m0QCbSiXuWSCfm2NiqhbWqNf4q987S8AAKc+IFLiqaMkkeaUB5XzlJuYkDmqSjAl30ekp3yBJB4biOSzuEFjL5TFrfCxx4kIvnaFou3SGZFkcnxerS2S9ICluLAvc5phKa/LGlajKlLIIydoroySYFM5kqSyykUsy6RfKknbMZ2U8517Y6TCMDvsDjY+JetiE9R2dZGI6cq6rONDJ0mrmhgVErxe5ePiMRqjyH1MKOl6MLg+IhYAIpbGChxlPFwWLaLPUZvFkozTaU46Z06WyVaXOiWh3Hfd54wiHhPjNAbTlbUasAQ6YLe4pHpuArc+LZHoQ85t0tcukixp9zlCua4ij5NM0BtFshteA+1avB22L8/GWoPOb6g8NiHnoKkpQtPlFSpMj1NDRvbC8Cxp2w+w9Mydoj9Kgjb8zA9YWzRNpc3wsTWj3JM7tHdfUoTt3Bjdf3yUNHYdu9mo0x7fqouUH/E8h8oVusja6ICJ8ZUVeS8srBFpX28o105+b3zk+z+KO4WX0D08PDwOCPwL3cPDw+OAYM9NLpks6bz1tpB6m6zKtJT60mf/3waTl92OKEGlAqlHY2PiYz00SapuQ/mFVtZJLcskSM05NDoZH9tg3bufEbU8X6D6Henyw3HbepMTXzGpcZXNFQDwzmkiGfstuWcux+qvUldbLVL3LlwiAnS8KCTqiTkyIyTSMvZam8xM3ebuBFRBkULTc2TCqbVEpe5yetSrKjnX7ATNUYeTL0XKlNJpst91IGaEiM06LmoSkFiBGpN0C8vi2H3qUYp4Kyp/5zVWr48dPRq3Tc5RCuU0X7emfMgdAZpQpN6lq2Q+ajeEbC2OUBKxuaM0BmOkH4Z9iYs5IZv67d3TueaZkEsoeafO+25I7RkXAJthe0mgEnEFCZrvbF7MJR3ezzrKc8D72vL+0BJWmhOT9RWpZ7J0U51iOMUmkZ5xJhcZm7PENRQJGILGklURvM0mJx/jsaRCWTNnckmrhF0ZJsb7g9335PqCREG+u85R1yqVreWEVvWaivp2ZhJO2DaUl3G2HSmq0wmzKW5tfUX6xnOTG6G/aaMcKDiR36xKMVzke9WVP/xXvkHm04eO0TtlbkrWvcKm3TfmVczKIhGkR0vyXnrkaarI6WIu5i9KUrHT5yhx1/SEOGEcOTyHu4WX0D08PDwOCG4qoRtjfh3ATwJYtdY+zm2jAL4I4BiASwB+xlpb2e0a74Uv/Sm58G3WRNpy2UJDlcTfcNjX2AjlS3nmqefjY8899/0AgAePSEW8FJOQ8+ek5sYXv/CbAIBzLFVvTQphdTxPkvGDT30kbossEYPNSEk8LOSFXfo1f/2Vl+NjtklS0NyYTOsTf+0h6r+KvHvpJZJcNtdJMnnjTXF/euAh1jZmRNozIUsQG6LFpLblddG5TlwkYB4iZc3N0q//2Xdei9vWQ8pzs7ZMeV6mZ2bkgiyBDZSvX5ULViiBEbkszZFLETp7TCTvPssLhbyQs2kmvboqaq6ySdL0CBcd0BGXjqTbWhWpfcDEWrMqUufw8GH+S5L6cFFJVJxf4/zZd+K28QlJC7wdnZD6Fil3VUcmp9Ii5YfsLtjmKEGrCPgcayVWpVcOmPSNIk3ok/TWj1xUoZB1+SzNW6SjTZ0LYUYV32DW3HI0ZhjJNdLs3qu6ETsaZlOiPTQ5SrjHUnBWjdORudqlMsvji1SE93YsrMorYWGDiMRI5RxK8ELrvDEDniPDNORIRp7RJkdAtxUxnWEC2OVBAYCsK3wyQf3ebMu75exXyUVRVyrJsBOBy4EEAGPj5PI7NkZ/P/p9H5I+NmksLaXRjk+SJN+tSnpgyymJQ9YihkfEqeHwHD1rZfVsjI3cfdGNW5HQfwPAx7e1fQbAi9baEwBe5P97eHh4eOwhbiqhW2u/ZYw5tq35EwB+kD9/HsA3APzzO+nA/CLnc9C1y7hbI8MiMZ46RZLz0aMUBHPkyEPxsU7ExRuuyi/xq3/+IgDgW9/4etzW5Xwwp18nifgbrbfjYz//C48CAE4MSzBOg+2KWqIK2M0ywRnwdO6GCQ56+omPPRm3FSfY9t+SwKkf+utkW75ymSTuCxdF0lxkt7+Njrj/OeF+ekqkyu0SekFlOWw4bUcVdOi1SBt4+pS4fC1dJe3FjtN1M0pauLpE9sFkShcfGOP+yM0t21BXKyTtT0wIj7FVJ+mtWhMXuENTNL8Z5co4aJPEtcxupTZStmi2S+eyIjHyEmBauQm2neTKmfYKKjAryfk+lIcYbLS77ddl++wMRItw9uO+yunhPAzd374qShI16by60jyd81ugbNEuZ4rhkm59lbfFsgSo58pJ7fpeNbZBp/kZ6keqAAm7VLabIkl32IVRxb/FWTMjdv9LqQ3mcufo5yDLUTM9Ha21DaFywXT5ZQba5u40GqW9pnjdXB6WprKvd3kadDCO40WSKgeO5ZeJy3EzrLJsnnqOns3akmT0bPA6l8bFh3V8mri0Nm+ar339a/GxuTE6r6ps7ocepGc6r0ofOgtDxHtmelL6ceIkvb+KBXluE7w/Ll6TkpS3izu1oU9Za5cAgP9O3uR8Dw8PD4/vMb7npKgx5gVjzMvGmJdbSkr18PDw8Hh/caduiyvGmBlr7ZIxZgbA6m4nWms/B+BzADA7O2u3Hw9ZL0qmVW1Odtc6cUJMF4cPk0mklySSZKMlqm+LSYrf+OLn47a/+CaZXGpK5Y0rfbN6ViiKitVvkcp57ay4Wk3PMsmqwsQGnFL1yAwpJT/0zKPxsbURivQ6eUJUqyqbZBp9ucg4mwCGR4mEefgxOb9UIhVyY12YxwwTVJsbon7OijUFAFDfFDUtz+ROpFL2zp87BwDIBqof48cAAL01MkHVm4pMy1CfanUhYutVIhe3tkStfPZDlAI4maLvXr4srlmPPkJz02iIalqpcSGMkuTYSbB6n+DIRV0UIiZdVXX0DruNtasqmtGxfmymiFJyjaFhWmddtV7nR9kOlxOoE8rYB0lOK6semWyG+p1kd8G+qovr9lig8qW4yMyeuneezVwu0jGpU8Xw9SLdcd4LgTJ1DLZoHoyrKq9TtLTZNKiiJUPew31FULoiJI4ANeqeA5eERo2lzWSoK0pyI9RUrp11fr4GauyGCeGqSh/dZPLUuJS9DZU6eITGN9mTdYkiahuosUS8F1yOm6RyW8yN0jugqJ799QqFXXcGInBeXCRHgQRXGVm8LKHZ6SfI7HvywRNx25uXqKDOT37f03Ie088bHa7dq/ItZdhtcnhIzIZhf/e5vFXcqYT+ZQCf4s+fAvClu+6Jh4eHh8dd4VbcFn8bRICOG2MWAPwLAP8KwO8YYz4N4AqAn77TDpQ48KZYEhImn6Nfz5lpIQG/+yq5B04dpfwjE6PyCzv/DpF7f/an34zbXFL5pCom0O3RL3AmQ1JOMS1i7jf/8A/pPi+9Grd9+oV/BACYU0Ewfc4BsXyBCNUy5Ff90WeJcKz1ReJIZUjCnJkVl6QKEy1hn93djJKe2JVrXBE5cSBKavdfcBPKNRKhK3AhbmlOgrlwWTIqzk0TQdnqkrSwvCGugavrJPUVSzLPE6xZLC+Jm6Vzyzt8mNxJV1eF4L1wiYInjh2VgAkXWJRR2TJdpryByyfSkTnN8P7I52Qv5Ni1rbKkgoeYgCsyeWp0oQie07VNOb/NEiMewA50mjT2XqSy9CVY8ldLYJmQs3ClzuT8Hkf0JJOyBo4jzCj3v5Cl1ATob0oRie6YLgZSY6lzqKGKe9RoLFWWANsqK2KaA+CMkuj7LPX2B0phTm0rVKEOJVia1DRykklZY3Z/hRTzolWNFWivF5Iqeyd3M3/kkPT3QVqQyhbto/WGaJ5ZdklttUQz22KNs6PmyPW96tZRuchmOUCtoAj17oC0+IHKWxTwdUeH6J6PHhcnjIcfoPJ1hYy8s9Y2yEihSW1Xzm/A5OhA+eP2WBq/uigBUc33wSR9K14uP7vLoY/d9d09PDw8PN43+EhRDw8PjwOCPc/lMj5EakuQUoRcwH61RkjA2iapNAkmZurjojJ958/I1KLVHReFNhhoNYp9XPlYR6dC5Wr0XeVXfnWeolinZsUrs8Mq8Ve/TqTrxqvfjo/9rR9/BgCwVBHyI1cmtbNYEpU24nu44hC5sph+6i1SNRMqtC9foPNmj0memZZk4qSxt0Vdq3C0X2ZUSNES96PVkWtUOBdKk1X1vCoskWUyravSnbrk/dVNMavMnyUy6NEnSCU9fEjMK6+9fgYAMDkt8+dMYCvKvNPjNRpiE0Y2p9R/l+MkoX2aqR8dVeTB1cwcGybTVkr51FdYRS8Pi9nLRdbeiM0P2TyRUMUojXXkosovxP7zQcoRitJH57OdCJRvOq9pS7Hsls00KTbb5FXEb+D81lPymPbZXJesyt49yaaNRbbkXFT+4hETkyllgpoco3moa9909xX+q3nYLqcC1sEi7jlMJXfPiZNVEasjnAK4ZaUfVc7d01TksymwX3mGrpuwymTFe2e1KqazSqfB/VFrxeuwuEnmxb4iZ+eGKCJ8vCjPwckHPwAAyGVkLGMJep6m2RTchvRjmSO8N9sylhGOLNXFXFJDZG515LaOfeixiSgYElNizC/37tz04iV0Dw8PjwOC+0BCJ7Eik5PfljhKLZRfu0l2N1q6RkTb8ohEDp4/Q5K0VYyV+wVMJORX17lkxWWl1C9miiM/x4eUJB2SZLe+KURi35AEtc75QTZrEtF5nrMErqniA+MpkiJbA5FC0hkaa5sj9nIqb0aCicyGCmvMBURMthq7p8vRRROanD2xuylifIqjH2cPS1GIZILma2mFokKrqkzekWPkVnjlohCgLlH/k0+eitveOUfkcLtHUnsuPx4f+8iHnwMAXLx0IW5zlc1nZ6QfLhNktU6SyYgiDZ0UuVmVvnU4I19fSYxpJqji3CgqI1/E52UysrbJxO6SpfOaTCvJ2GWidBHCdE/qpyPdshmJ+isWaM1U3QW0eCzNlozFZWUMWPrUmRh7LNHrAheW98y4ioR9dIZzrbDb6WZWiGyXi6evMpemOPK0kFMRuVxyrlOnue2ofjjv10JRtIeIozU7iozfjqoqALHSZtdONSEhR6Buqjw9XSbt8+OsLaplGnCOlp6SuENWKRSXDMvaXJmrxIwVRBpvMNE9X5FMidmAiXSVmyXZpDVK8Tsio3LKnH+bXJsPfUCysD7C5SS7PdGcQiaO4/w82mmbrQRJ1WgHu5eYvFV4Cd3Dw8PjgMC/0D08PDwOCPbc5DLGZGFpSFVCZ/NAAqK+TE0QsbZ2jdSXxctSqKFRI9NCONCkDaldOVVgwPmmO3NMSqngLulWMlB6kSGVqdMU00/YJPVwjrs797DUAx1YOm9oVNSzNheAGNZqs6X7Gybd+n3xqx3lqMaJMUkSVuHouZVlUWGntmXPWauoYg9ZUo27qt6jYdWuUBRzxsQE3WNqllTS06elpqLl6u+PnRL/2/VrRCEOD4tZ5emnKJq3UiN/2q2qmIVe49TCH/qIpB69eIHML3Vl3pnm2qA1JkqDrOjZ7R6p15mC7IWLHPVaVEmrGlw4oZR0ydNkHdvs3xuqxFqp5O5bP5lye0eu3+PoynRW1jZfpE3g6m8GgchHWf5uX0X/9Qd0z1IgpotyiT47f3GowguucEW/K/3u9WlcDRVN22bSMmBiPzEkY0tw8qewJn3rMEEaanOkof6GHAHqokkBIBkwQameL8ea6lTH27FwTUwpbR7zqEpbXOI9vjUv0cUu4NMysRlel26X/bl7Oj6AO6BsLq5L46P0bP7AQxJx3uWji+sS+bnaoH7OV6Qt0aN7TSXJ1DtdlvdTiknl5aqML/EW7ecHxsSxYLLEidSinZG2LtmcVeajEr8PVGXk24aX0D08PDwOCPZcQn+QU8L2FWnYtfSrZQIhI4dzJDEcniXpcEu5HIYuUm8gwykW6VfxYx89Gbc5175r1+iXuKncHF11+aJyIVxZIMkhFSiyi0uyTbJ7VXZWUvwmx7gyfFv6VmfXulxCXOYsu2sl8/R7urEl5GU/yale2yItjHGfUoGQp9uRVm5YfZayousTgwAQCRkAVldIKptgqalUEDLtzdPkcnj86INx2yyPdasiUkXE0uHE+CifIxLK4iJF+XUa4oZ15BDlx1leVkSzI6OYEP7K174bHzv5GEURXlqQCN6NVZqbh46Ii2SKox4DJlSzKkK456ROJaGXuar7deGPDKfFtPqyJxOcXyib1Vod7bfRMRp7X2lEIc9LQj1hBZboI5Ue2BWgSHGq464iIxOcKteoSGJHvDa7ouFc65JMV2KtY6AKf7TTdL52g3WSbk/1N5aMucNhqApXcBrprkp9m+HI0nCwu4jeK8mzZHgqN1UpvAprXy1VfjLkvZBkd8VQzUfA6kCoXJHtgMsiKunXuSVXWFt0uXkA4MgE7ZmEipw9WiZNIVCFbL57lYqhXGGX3tU16XeqTOs3gPTjWS4lN10WDS5iS0C/59Jwa9ds6m9elUUcYq2u3tzmk3wb8BK6h4eHxwGBf6F7eHh4HBDsucklYqJy0BXVqtUllanZkYiwIvsZl9nPOaGq0Q8VSM1Zb4hP+PQ0qf6PPCqmiPERUvd7IfmM1hXZmQhIxbNWyI92i1SgmTkxIywvkHpbqRFBWMqLGpXtc8rUtIxleIrUTl1vsskmiKEJOtZKCAG6skDXa0UqdStXoJk5Iuadgaq+AwBbLUUUsVo7rAioes1FpwrRl05xhOECjUWnTE0ZUgVXF2UNMnG1JjFBuYo8ltOzDgZCio4ME3Pb2BJ19dgDZMJZGizGbRfnieCe5rqMhWHp95tnyOylitxjiFOOTqmo1Ih9vJNsBukov2vDKngxIyYAt2duxEAlXMUilaLZJcoKFJHeZ1OBq5ZjFMnofKWvq/KT5nsqc5AjzJrsg99VfsntnjM/SN8yTHifxy+GAAAgAElEQVQ3MzIhm+zvPJehv1NNtXcsrXegSEMXIV1RprANt394DOWiXH9rk+uBKvtUl59ba3eXCXMTYmasM0E6UPESLmzEpTcGJEp3wORwQtUsdZWIBirOI81zHyW1IzpN2LUViqF4sf0n8aEPPU7R3AllOiunaK8/cuR43LbKZo95jnup9+WBGxslM2CnKW2Dh+k9Y09+IG7bchGiWTqWUe+AFkct91WsQ/yOuOpNLh4eHh5/5bHnEnqVa2imVe3KcMCkVF3IxULAdf/KnLazLeTD1Dj78Cki5+m/Rr+2UVKk9rUakXR5dkFKZuQXs15zkY4iLZ98hBLZf+CJvx63fe1r3wIArLOwp90AIyZnm+qXu8hpfnstkW5cdGk/pPENjctYNrZIWh4piDRZ47wdlU2J2jwp9SEAACat3CLZtW6zKpJau8dui2MiDTlSb2ySxry+Jm5Yk3PH6LpWtsj4MEnmmxsyp+UxWrd2l1OQhirnChdG6CjyLcGk24mHJNo04u+47z7znLhFnpufBwD0lYR0aIYknmxO5siCJD/D5J+O2MvwOEeGRGI0yh1uOyIOTwxSoq2Z0JFvKto0TW1Vp6VYlQaZCbCEkowNRxkHSpocsNRZ5/qrSVU7NZ+lvZVTUq1hcraupL2FGn33VIbueTyhog85MlI1xdGVm0riXuRlXmeNoau0jSBN86DntM35cSYmt21EhVBF8qZYK9G5atoswW4oB4d+l74TcGET7RfpioBEtfaO841yGXWuji6a9dyGaOILa0SoB+r5KpToeTE6xw6v22iJ9mJSubk+98zzAIB33nkzbqtw39Yg76BqjjX7Q3T9TEs01TUmtfstFd3OrpJKGb1teAndw8PD44DgVgpcHAbwnwFMg5y8Pmet/ffGmFEAXwRwDMAlAD9jrd092cgucNn3trbkq11OHlEaEtt1kyXAgDMP5stiZ/3Bj/0IAGBp+Y24bXyS8z6Ect2wT9/dYttoOSe24B5nKByoSu9dzj9R3RKb3QgHOLkAid5A8vWFLExEPZGoNpao3+sVkVLnZsgWnuTiGP2U/HKXJ2g++k1le2Wb9YVrYlvbLqGn0iJRNdgWnoBoDx945iPUX5WLpFykfjbYXpgqinQYJEgKHipKBFNjg1wN68pG2+NglnBA9+8oF7Eyu/MZI/NRYWn21ZckiGl0iDSE6RmyiSezcv7kJN3/7NsyR+9uUR6OuWnJB+O81hLsqhlZWbMk8yNd5eqX6L9HLheev0DzDZy9cRApWzTbnYOAjumxO+0kp7Mncj+yanwug2Wan4N2KBJbwUmpqmxbiucyq0iFbo3WpdukOZocFo2vsk4cSDaQR91lpkyqOUpw8FCbuayOsv2nc+w+mRJpudXbGZy3Ayo3iguSyqg57XNeH80zuPlwmk2QkfOzI/Q+0Jk0wXlbEkmZUzgXTfdHS/m87DofTLPpsmbKNSbG6QE7Mkt7spCTOb1ygXK5bGwKD/TEHD0vCZWDafJhshIEvJ+6Ki+S4QDFrgoaS76H1niruBUJfQDgn1lrTwH4MIBfMMY8CuAzAF601p4A8CL/38PDw8Njj3DTF7q1dsla+yp/rgM4A2AOwCcAuKrMnwfwt79XnfTw8PDwuDluixQ1xhwD8BSAbwOYstYuAfTSN8ZMvsdXd8XICKkqHeWi6IoqdJRaFASkioWm5xrkGpNk/hgekdqEnRbl+0gHYrZp9Ug9XGS3oLZiH6am+D8JRS6yer2lIu+ynIrzyANE6s3Pixmkx+6W1Q0x2+Q5yX1apYRd5NS76RRHkLVEJUxz7oiSqvFY2yAyd9DaXSWrqz4OOCKyVZf5Gxvnwg8qBeo750h1LBZJDy2oqLVqhYjPzRUxWfXa1FYoicqbj+hzrc61K5V5xVV4P/GwRJu+/QZF4B07djhuy3Fq0nqd7rV2SeZ0ZZlU0+NHxaWsxnlgXj+jSOKjZN4ZY8K7MCTmNJcapl2TsdQq7K84I1XaHVwtiOvMNkxWJjRx1qF5LrKLX1HlDUKKyLRsUfqRYXLThrpoCKdRZTfRgjJTWCYNOyqSMl2m81JJOW/2COUsGd+k9a6oSMoW55JR6XHQ4Ur2AzWWKqckbnJkaV65LRbYrLE5kP1R5P4OrJiDtuPCd96KP7s6vhNzsifTvO2zusYq127Ncz+SgRDZEyNkqpycFXfVDJuDrHL3NK5Ih0uTraJNDTsuRMq01WNCc31TzKfX1ti8yHsmrwj4Hke4RooEr6zSeWFGTMHHTtGku31SWZfzO1wE57p+M1k+pNbldnHLpKgxpgjg9wD8U2tt7Wbnq++9YIx52Rjzcut9KILq4eHh4XFj3JKEbkjs+j0Av2Wt/X1uXjHGzLB0PoMbV/OCtfZzAD4HALOzszsSP2xs8C9gUdzpwAUDokh+AEp5+rXrJkjyqUeKMG2SBDtXlvObXfpFXVsTF7siF684NMmuhF35XSrxsXZbuZQxsdXtCPmRypB0MDZ9DABw+o2vyvltLlfVEQksxZnvUsqtKs3ua/U63ev8WZFISwX67gdPiBRSZGJtSn78d2BtWXK/JJMk8aTTIlWcPU8ay9jho3HbyDhJPJcvkiQ1PixzGjChapQUMuBSYcWMSOhTU9TPYSapXc4TAGgPSAq+cPFc3JbO0Hysbki188X6VQDA4UPHAADPPfus9CNFktrCouR+GWUudH1T3CwXVklD6XRpD0Q9WfchLi2WUhkYh1TOjR3gTIZGnd9nl1iTFCncSZ1xsYJAxOAsr1lSBbA4b8WuqlDfadGcplhcLeWlX05611kcwdXojXI57LB74BaXDaxUJVqq2+ExKO2rwxJjrSH9aDOjXxqldeyqew7HZLmsbYpLsqXs7kLa5qKsT8j5mYK2rKNNcLm5hPTNEfMBO0YEyg2236Bno11V9+Tsk5r4TLCInuDIpW5XNJwtft9UNuSZy7LWOjIiD9ghlrQvMeHcqsn5R7lQTlMR3usLdF67K5rT5Ac/SF3cJI3y3CuvxcfqS0TsJ1RpwIBz9zzz8BO4U9xUQjfGGAC/BuCMtfbfqkNfBvAp/vwpAF+64154eHh4eNw1bkVC/34A/xDAG8YYlwbv/wTwrwD8jjHm0wCuAPjp700XPTw8PDxuBTd9oVtr/xTY1Ur/sbvtQItrJPbqQlKsbZJaNDszGre5NJ2WSZNMWro0OsR5FBqSGjbLqn2kokebrghCkfPBlMXM4wjKek3U1WSSVKXlNVGVhsaYCEuRcjM6rvJ3tKhPmZLKg9GgeyZV6ltHtsX1NaclMrLA1oxmU0jOXodzqCR2WKxiHJ4TE40rHtFsqpwXXAyiPDSqvkNkWjHP/uhbQkxX10jFzKgiElMPkrmm35d+nD1LxKqN2M84LSRgH1yXUa3V4cN0zweOiOmnskFjvbZApq3vfPvP4mOGSerJGTk/4BSyRvk0v37mEgDg4QeImx8rinngDS6Icer4kbhtRK39diQNj0UR021nfuuLCcrNTYP9mI2KCnVZZbOKkOuzCUenczVMOEZsJmh0VHS0K4KQkGtUq7QuHZVDpctpfsurNN/JLdnDAy5ckSnJfNTZ9zmRFZNBPss5ZZhQb6u6p6UUmeKiKK3O57qkWSEttyNfENNcnZ/vy9dk/myCPk9NSz+c73rIuYxClRbXuZcrKwXazqSliU9XQIYJ2y1lXmnzWmlye7NC+37x/HzcNjpFfuhFzimzXpX3yAU2mZVHpSMPfoSI/7lJyR1VvETXS7BzxdRTj8XHUk/T59hsB8DyAC9clufwduEjRT08PDwOCPY8l0uGpS1HsgBCPHVVqakc/xJ3O3X+K+RKYYSk0zWV+6XDRSbGJ4Xo61n6ritF126IpOkyCeYCkdxS3I/1zatxW3mIJJf5CyRNLl8TwrRUol/1fFYkk0RIU1xviwZybZkIQZdTpl5XWSJHSYoctEQiqNVJWikp6Xo7MhkVKQe6bqsukmAmTZJAfUuI4DOsjbRrJBEcmxPP003uY1UV6yiOkCTVVtFtHSawr1ymrHSdtpBCuTLN6YTKupcOaKxa+i0XaY1OnCAp55GTcmxphbj2cxcvx23rTDI1GrI/snm6xltniBw+dVwkpbFJku4rNVmDVosJO6kgKH1kUrmnysclWfaJlJuZy9mT4Lwn12VWzLGkqTIDtnmuLOS6aZZ02226lnZRbASuiISc76J01fbAJpO4E0wkDlvRGhd5r59XzgHDnLtkWpXYGzRoX7gMgsbIPd0e7qriFDZD860E4x0I1VyVy6S1NptCaLbZLbnbE6k9YoK3tsUZHlVhjoAzE65ek+fLSbg6Std9Z3aGSywqqfnQNLVZlVnUlSisNUSzqXE/U+yWO1cUwnTAhXES8higwfP80MlH4raTh8npYODcJ9Vc9V3xC7W2DZ57L6F7eHh4ePgXuoeHh8dBwZ6bXDY5tWVTqeol9ofu9EVHGQxIBSpxVGMmKapsk00G9S0hchx5lRCtEu0eHe+y+aNXF9W0xMmOxsZEBzchF4C4Ii72o8PUjwKn+w2MEKC1KvUpaUUfHsrSWMKmjG+OCZfRWTLvFFbEfFTiIgxdFcmWGGeVN9w9UnT+ghA6ZU4NmlC+ysMc6dZWPtCTMzTWixUijd56+9342LHDFMk5GMg8Hz5C5qDNilLfh0mFffQx8p29fEnMU22uddntiprtrBLatNDlz4YjGEsqSnF0jPr9/MxTcdvGBpmBzp9fiNuW1zmFLfuCn78oprAf/D6q+p5SvspJVQ9yO7Z4fH1ldgiy1KdUWifWMtf1d6BS2g44eVVPk6LsF53JyTWS7NPsjAi9pronP55JqHVnE07YkOsmOYWzGaW9NlmW+Tu7Smu7aOVBGOcUxkEk92q6FMBsLhwaFrPXaIm+u1FR5qAefe6a3Yn68QlJnuYI/awya9TZX17X1XSGEMMbxShS1EVSDkJVd5XbdFT57DSZDo+yyePoEYlKPvXYowCASkVMj+fniTTPVSSS2PC89XiNZ6bEbBMwcX2tovz92RR2WRGrC+fpeQrtTl/5kPeKTjEs5pf3SHh2E3gJ3cPDw+OAYM8l9DQnzw+Ue1yzRb+elZrKocKkaJpF7mxRfqVz7N7VUmSdK7XWV5FbaS5Y0Odf/UxOfjHzBS6qocrYpRJF/qvYDOdyyIRVSqkAQ+w+mUoIyZPgH93ukozFVTk3nGDD5fEAgEssWWZT8ls7xqROt747WZItClGU5GjCoopSXF6haNpLyqUtwzk0jnH06OnT4t51/iKVfuv1ldtnm+b3wQcfitsurl0CAEyx1vHEk+KatbpGmk1HlRGrsBRklGQSE2Gcj+biJdEUAh5LVkWnltnt9AMPixvigyc4SrdL0tPyNXFhbYdc3i2U9baOiLtBwGiTXU1DVfstxYU+EklFaPL8OVI0pdbM5QpJKve4BLup6ujAAZNpbheNFsTtM835itp1VeaQZbCUKtBg2UUzyrEGoNI3W9b4GgN51NsVGl8ukHXJsybhnA9KOZU6mPd/TuWDaXC+mOvS1m5DvqBc8niNeyoHU47dGnWeowFrkAFrWjeS/60inzttJi/VdYeHuKAEk6g6hfEWuyh2NuU5nxrj1LcJVZyFic80v1uyKmWvK45xTJVKPDxD2ojLLQNIZLDzswySMoFuDwTBzvmbP3t1R9utwkvoHh4eHgcE/oXu4eHhcUCw5yaXLKsom5sqQpOJluGSqCjONJNi/+UgEnNCgavqWJXYaHOT/JEnk0JmRF1WjbnGJAJR+9tcnajTFLOGizY9cfxY3Oa0soBrDLZUJSLTJ99mqyr/uIRNwyOqHx2679Iap9C00o+VBZqHpPqtDTi97Nzs7vUbdZrWMo8v1ZHlvbZKfuVhWwjK119+CQDwoQ9/GADw/A98ND62WSETTWVLEiy9/cYZuoaq2uNU42/9KdVaPXRIIla7nAQqpRJa9dgsNqKqUT30APmft9s09pVlUTkTTF52Vb+7TDDX1uQ8y77sQ1ytZ2hIzDEdjnps6ziFgXLk3oYcJ6ZKBKpCD5PsybSsbdZVpmfiuKuIObfuCaVSW5dqVvlWV9n/O89NJRVPEHH1rKJS4zFMfetB+tHmpGlJNjNuKr434JS+ZWX6SYZcfamrTIlZNilxRTCjzIwJNh+FiuxvR3TeUHp3Aq+yKgnYAq7IpPOM5bjKlrJ0wOB6U4RVxL6btb4y4fXYZJVJ7TRd9Nk00+kLsV9jMjSrCMoeP3/KNR2TbEL54Ac/AACYnhFniSyTuJrkdJWHMllt+gyuO0+n8bXRTmPSICZFvcnFw8PD46889lxC77IUMogU8cN1BIfLqp4lE4kdSxJ0KpBjLlpsnBPgA8CgSaRHW1Wcj/jX3pEmvZ78Si4skxRX3xIpbqvG0uSouIH1V8kt6bGHyI3uiScej4+tMkG4rmqQ1up0T+0mFWZIIihMMSGsSLIEuzLmVM3IKldb76/LdY9I+hcAwNSQuIj12zSnC6tSACKdIfHjucdPxm3XlkiCipiMXFfRdq7G5MlDQoAeP0SS9He+K7ltZo8SoTpxmOZqoHKMlIZoLBvrQramWLpZXhdX0HyB7nXixAkAQHlEpPezb1Ht0bUtIZqnp44BAEaG5V69NM3z0ARNTHlINKLlVXIL3WCtAwDqHPXYvQHrVuD9l0mpmpic4jUoiWRcYNItYMIvp4h9VvjQ0oUUmnXum2iSQ5xTJj3g/iuXRstuhWmVcyXFmlilpdIa1+hmA041u65qliKiPTNTEEk6xfstsSX9TXAOl16KIxhVvx1pH2TldeEk6EDVst0BJfHGUriSTHvsgpnLy1637HTgom5ziowcuHnOiqSb4jm/zg2W01e3eT9fvnQlPjYzRe+IklpHV5C22xHJ33LbBkdW633tJPScksZdrqRBKO8Pl9snzvFjdqbEMko9seF7hN3eIryE7uHh4XFAsOcSep2zCuqQmT7b5zo95fLF9sEsS2Wu2AIg7kDH5x6I2zaWr/A15Lw621IXuARcPie5UVIB26BVjpFNLst1ZVGCVNodzjHRpl/Tw7OSp8S5xxVGRQIrjrr8J2IDbrBmEETO3quDVUiaTeeVJNPk4InB7r+/zaqMc8DSXpRQy2tIolu6cjFuOjJHduYEl0TbWhHXyoglkq11aeuzHbRYEgl6nQsGPPEEFaVYVIFFBc5TooMnIq5sfmhO+AAnULpK8nFRBgDra3T/d89eitvOniNJe0hpNiG7ipYnSHPLF2RtEyxF9lTBlCDYXbJMcyV7nakz46rb60AazurngmaSSSVt8dwnraxtyLcMUsp9jXmaBOeNSaZlzVLsEmiVu1vE2QhLSsp3xVMC7luoRGMWvJFWUnvaSZuqH87FcADaR+lItMGAg9LKKrFig7dbMrFT6nQoq4yW3U73ur8AEHIgmc7v4rSSHruVthR34gK3Wm2dt4W/p+zT6xubfH/qt16yqwuXAAAjSgvs9+i71apo0Ybt370BZRMdGpbBD7PmWVLPQWmItIycKlXnsqkGfK2kWkcnrRutxtxAgr9deAndw8PD44DAv9A9PDw8DghuanIxxmQBfAuUYCAA8LvW2n9hjDkO4AsARgG8CuAfWqvKpN8iSuxm1mqKKrbFORL6A3HFM0xA1dm3qF0XVeyhGVKxnnn8VNz22it/DgC4uixpVw8fJwLPbpGZYKDymuSyHMnWFVIjwRXs83nlhphjsoRTzyayYk7osOpbKiu1mY1JU8o0k+e0vasbZL5ZXZWxTE6zGaakCBcmoFq13XO5bG6oPBT8M22MiqbNsfuaUhNdBF2T3cC0GSLDRFyo3bs4nXFZ1X/NOHdBJojMpJCzCNkMkhcXwmtL5E565ZIQtrOHyCXsjXfeAABcPCtRnmGdCM1cRvaCIxKLKheJ4ZSxXU672qvJfspzulgzkFw/i5y/JvPIM9iOAo9JecfFLnORIu/7TGJFoUuFKl8I2c0WgVLBneteUslRrGWneH/3Q3mEBmxeQVLIy9DQOAeq1qvzjDTsSttUHTfsBqktIy4yN5NX9U5574Zs5tS1YbtMZCYV6ZvkSMqov3tOnNXVtR1tusq9++jIYmBnJZ1IuS0624l+HqNwp0tgm+u0Li2TaXVqSjwIylxLtqXyDztz7uSsuCY6Qr/AUaHZrNzTRVjrCNcEm0tCRSb3eTAR9y0ZyfPliNLrzDA3cGW8XdyKhN4F8MPW2icAPAng48aYDwP41wD+nbX2BIAKgE/fdW88PDw8PO4Yt1KCzgJwok2K/1kAPwzg57j98wD+LwC/ersdcO5AJiOuSxHn71iuiES1uUG/qEucC6SxpfJhbLl8GCJtOXKi15NfbpfAPseSiVG/pjOT9MvdbisCiklIneSwy8Emm+ucSXBDiJR0gfukcsrU10lKMD257txRCr5JrDFRuaLcpSKXxF9c/SbYHXNhRaTaQ+KhSd9TUREBk3Nt5YaV5iyBumhIkwknRyylFUnW6XChg4SSIJi0jJpCSq1wqboG/zXKvQvskqpZqT4TW52mzNF3Xn4bAPDWGXIJ7dZk3X/0Q5Qdb3hIuXFyVs2JjEi/Gb5HnYOH0mk5ZlgiHp87HrddYtdEcWgThCwpRVB7gbUBq4jpDleTz7NmY9Qa9F1hi1CTr1yNPqm0r4yrcu/GoQhTfg60622PN2OkMkGWmdB0+UEGLdmwjphOKK0gzs+jXA5D7tuAc7T0lUhfZyLTqjKKSdPj83dXysvDsmZOEtVueo4s1JphKnB5cdh1VOUjSnMQk9Nm9OeUCixyeZzc9TNZkaQduZ1O77yuI8P1d5M8p7q84A53RDWu6zIqhtdnVNQ5fBx0242CjW4Xt2RDN8YkuUD0KoCvAjgPYMvGoW9YADC3y3dfMMa8bIx5udVq3egUDw8PD4/3Abf0QrfWhtbaJwEcAvAcgFM3Om2X737OWvustfbZvMp65uHh4eHx/uK2/NCttVvGmG8A+DCAYWNMwFL6IQCL7/nlXfDam0ScLKyJmu1MBYGucu9qc3IRiXxGut4IKerwa3/x9bgtyerv+LikuDRMYqX5uxMT4qtccOlRAyEN17bIBzoViHpbGiZybsDRc82amB9KWYpObPdE5Q0jJh5rYpppJ8h0MjVBxEtSjbPJPuebYnFBtUKkb8fu7jsdRkrN5nwjQ2osq6s0R1UVCTs5TUpVhlVOnT5UctZIW5NzlVxdlhwdjojLsGwQ6hqQbAZpt+SeVTaJnFHE57UKXbfKRU6myhLlOTPJkX05We8Ek4XV1UV1Hvmfl8oFHosyjXDEYKQIx7JKU7sdLSYVI0UqR1wHNAwVbRc69plTvaq0rkUmYq0yBfTY5BcOxISS5AjUqO1yxUi/82wmS6jHdMChrTqtMTjPTJcV5pSS04qcdljX9wRH1WoCNuzR9VzKWatSDW/Wqd+ZkloDdz27u5ngKDshAGLyS6ncNo5U1OYSZxJxhUTS6Z3nuzxKgJhyksHONmdmSmj/bnMDGZaHcN1pO056bx9xx8nqPWD5uXamGW1ScaaZ60wu7zGXt4qbSujGmAljzDB/zgH4EQBnAPwxgL/Lp30KwJfuujceHh4eHneMW5HQZwB83hiTBP0A/I619g+MMW8D+IIx5l8CeA3Ar91JB06fIbe0UElDQ5yt8OEHhfnLZEiasANy/yspCSuV4vJWyo2omCXp16pK5asbJFmWRylKsdsXiXftGkudys0s4KIRywtS6izFpb8qXAat15Rf1YilTx0VOlKgfoyWJuK2rQFJ61VOst9riAawtMhagcqwVyqxO2Rqd6lyRUvNCbpnXuXBGB+jMafSuuq6i8YjCXZsRFwr+3xMCegosrvYUEGiFMPQubSRJBWanVJ+X0nocyxJv/H2ubhtfY2I7tUazUNrXfrYf56k2fywrMvRw6RZnK1KPpjNNs2pKzBQUGXNRkfJbW1DuXYmlSvgdrh+9/qi9bhCG1rCy7Am1HXjU5pW1gR8ujxiBc4vY3XoYo/ztTDpmlKRpQmW9lJKunZRvYGKrU4ZF1nd5WMqUycT/5q8DOAiSpU2xQudiFyZN9EimrwXuka0aCRccZbdJdcHjgsJfUPpmglQ7boXS9csuWqp9b1IRS2Fu6/ELo3XdXHA56vSdu67WkB2TfH9ox0HrydK3d+d1zU3igpN7BxTZO8+l8uteLmcBvDUDdovgOzpHh4eHh73AXykqIeHh8cBwZ4n55o7zCaJcVGBhzlFaDkjarOrr+i0lmZTSKEoJCJlcVmKMeTSdFybB/I5TufKfut1VWG9ZOie15ZEjR+eIkJ1elY8Mnusuo7lSX2uKjK3NEzXV2U7kWAitrIlpp/kCJkFRktk4kjnZRmyOWprqKjGISb6GlWl8m7D6roQhJPTdL7iZ8Au09jYkM6VR8iMMTNHEXLGqpSpccIpldqXddKiSkDU5ixNIRcJmJ49FB8bsArZUZXe21yztaxMIuBkYvUqrdnMISFFy7wXdL3OkM0Yxx8RZ6vFVYpA7bNq3FF+2o0a7YuBCihouWIXYgmT63P0Y6jiCZKW96dSi7ug/rY5XatWqRNJMhtl82Imi3gP6+hbN+dFJkP7Lel3xARopytRoa1unBUrbnMhDhGTtAlVgKTTdP7icl1H3CWvE+foIh0ee18R+1UuKJJSMQzOdzsMd5cJh1VCqxuZS8wNzDVSa3Pnq8nNr7lBQrDrr+VMHTv75Ewo5jrT4O7XM+9Bht6Iw7z+Uva687Tpx1ndbkSU3g28hO7h4eFxQGDej1+FW8Xs7Kx94YUX7tn9PDw8PA4CPvvZz75irX32Zud5Cd3Dw8PjgMC/0D08PDwOCPwL3cPDw+OAwL/QPTw8PA4I7ikpaoxZA9AEsH7Pbvq9wTj29xj2e/+B/T+G/d5/YP+PYT/1/6i19gZOttfjnr7QAcAY8/KtsLX3M/b7GPZ7/4H9P4b93v5vvvcAAATkSURBVH9g/49hv/f/RvAmFw8PD48DAv9C9/Dw8Dgg2IsX+uf24J7vN/b7GPZ7/4H9P4b93n9g/49hv/d/B+65Dd3Dw8PD43sDb3Lx8PDwOCC4py90Y8zHjTHvGmPmjTGfuZf3vhMYYw4bY/7YGHPGGPOWMeafcPuoMearxphz/HfkZtfaS3CR79eMMX/A/z9ujPk29/+Lxpjdqz3cBzDGDBtjftcY8w6vxUf24Rr877yH3jTG/LYxJns/r4Mx5teNMavGmDdV2w3n3BD+H36uTxtjnt67ngt2GcO/4X102hjzX101Nj72izyGd40xP7Y3vb473LMXOlc8+g8AfhzAowB+1hjz6L26/x1iAOCfWWtPgeqo/gL3+TMAXrTWngDwIv//fsY/AZUNdPjXAP4d978C4NN70qtbx78H8EfW2kcAPAEay75ZA2PMHID/DcCz1trHQblqP4n7ex1+A8DHt7XtNuc/DuAE/3sBwK/eoz7eDL+BnWP4KoDHrbUfBHAWwC8CAD/XnwTwGH/nP/I7a1/hXkrozwGYt9ZesNb2AHwBwCfu4f1vG9baJWvtq/y5DnqRzIH6/Xk+7fMA/vbe9PDmMMYcAvA3Afwn/r8B8MMAfpdPud/7XwbwUXCJQ2ttz1q7hX20BowAQM4YEwDIA1jCfbwO1tpvAdjc1rzbnH8CwH+2hL8EFZCfwR7jRmOw1n6FC9sDwF+CCtwDNIYvWGu71tqLAOaxDyuy3csX+hyAq+r/C9y2L2CMOQYqxfdtAFPW2iWAXvoAJveuZzfFrwD4PyBFEccAbKlNfb+vwwMA1gD8f2w2+k/GmAL20RpYa68B+L8BXAG9yKsAXsH+Wgdg9znfr8/2/wLgD/nzfh3DdbiXL/Qblf7YFy42xpgigN8D8E+ttbW97s+twhjzkwBWrbWv6OYbnHo/r0MA4GkAv2qtfQqUOuK+Na/cCGxr/gSA4wBmARRAZortuJ/X4b2w3/YUjDG/BDKp/pZrusFp9/UYboR7+UJfAHBY/f8QgMVdzr1vYIxJgV7mv2Wt/X1uXnEqJf9d3e37e4zvB/BTxphLIBPXD4Mk9mFW/YH7fx0WACxYa7/N//9d0At+v6wBAPwIgIvW2jVrbR/A7wP4PuyvdQB2n/N99WwbYz4F4CcB/H0rftv7agy74V6+0F8CcIKZ/TSIgPjyPbz/bYPtzb8G4Iy19t+qQ18G8Cn+/CkAX7rXfbsVWGt/0Vp7yFp7DDTfX7fW/n0Afwzg7/Jp923/AcBauwzgqjHmYW76GIC3sU/WgHEFwIeNMXneU24M+2YdGLvN+ZcB/Dx7u3wYQNWZZu43GGM+DuCfA/gpa21LHfoygE8aYzLGmOMggvc7e9HHu4K19p79A/ATIGb5PIBfupf3vsP+Pg9Su04D+C7/+wmQHfpFAOf47+he9/UWxvKDAP6APz8A2qzzAP4LgMxe9+8mfX8SwMu8Dv8NwMh+WwMAnwXwDoA3AfwmgMz9vA4Afhtk7++DpNdP7zbnIHPFf+Dn+g2QN8/9OoZ5kK3cPc//rzr/l3gM7wL48b3u/53885GiHh4eHgcEPlLUw8PD44DAv9A9PDw8Dgj8C93Dw8PjgMC/0D08PDwOCPwL3cPDw+OAwL/QPTw8PA4I/Avdw8PD44DAv9A9PDw8Dgj+fwSx6iq4PNHdAAAAAElFTkSuQmCC
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[17]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Now that we&#39;ve got a lot of boilerplate code out of the way, here&#39;s how it fits in to what we did above:</span>

<span class="k">class</span> <span class="nc">Net</span><span class="p">(</span><span class="n">nn</span><span class="o">.</span><span class="n">Module</span><span class="p">):</span>
    <span class="k">def</span> <span class="nf">__init__</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>
        <span class="nb">super</span><span class="p">(</span><span class="n">Net</span><span class="p">,</span> <span class="bp">self</span><span class="p">)</span><span class="o">.</span><span class="fm">__init__</span><span class="p">()</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">fc1</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Linear</span><span class="p">(</span><span class="mi">32</span> <span class="o">*</span> <span class="mi">32</span> <span class="o">*</span> <span class="mi">3</span><span class="p">,</span> <span class="mi">25</span><span class="p">)</span> <span class="c1"># now our first layer accepts inputs the size of the image&#39;s total information</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">fc2</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Linear</span><span class="p">(</span><span class="mi">25</span><span class="p">,</span> <span class="mi">10</span><span class="p">)</span> <span class="c1"># we also have 25 hidden layers</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">sigmoid</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Sigmoid</span><span class="p">()</span>

    <span class="k">def</span> <span class="nf">forward</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">x</span><span class="p">):</span>
        <span class="n">x</span> <span class="o">=</span> <span class="n">x</span><span class="o">.</span><span class="n">view</span><span class="p">(</span><span class="o">-</span><span class="mi">1</span><span class="p">,</span> <span class="mi">32</span> <span class="o">*</span> <span class="mi">32</span> <span class="o">*</span> <span class="mi">3</span><span class="p">)</span> <span class="c1"># this just reshapes our tensor of image data so that we have &lt;batch size&gt;</span>
        <span class="n">x</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">fc1</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>             <span class="c1"># in one dimension, and then the image data in the other</span>
        <span class="n">x</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">sigmoid</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>
        <span class="n">x</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">fc2</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>
        <span class="n">x</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">sigmoid</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>
        <span class="k">return</span> <span class="n">x</span>

<span class="n">net</span> <span class="o">=</span> <span class="n">Net</span><span class="p">()</span>

<span class="n">NUMBER_OF_EPOCHS</span> <span class="o">=</span> <span class="mi">3</span>
<span class="n">LEARNING_RATE</span> <span class="o">=</span> <span class="mf">1e-1</span>
<span class="n">loss_function</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">CrossEntropyLoss</span><span class="p">()</span> <span class="c1"># Changing our loss / cost function to work with our labels</span>
<span class="n">optimizer</span> <span class="o">=</span> <span class="n">optim</span><span class="o">.</span><span class="n">SGD</span><span class="p">(</span><span class="n">net</span><span class="o">.</span><span class="n">parameters</span><span class="p">(),</span> <span class="n">lr</span><span class="o">=</span><span class="n">LEARNING_RATE</span><span class="p">)</span>

<span class="k">for</span> <span class="n">epoch</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">NUMBER_OF_EPOCHS</span><span class="p">):</span>
    <span class="n">train_loader_iter</span> <span class="o">=</span> <span class="nb">iter</span><span class="p">(</span><span class="n">trainloader</span><span class="p">)</span>
    <span class="k">for</span> <span class="n">batch_idx</span><span class="p">,</span> <span class="p">(</span><span class="n">inputs</span><span class="p">,</span> <span class="n">labels</span><span class="p">)</span> <span class="ow">in</span> <span class="nb">enumerate</span><span class="p">(</span><span class="n">train_loader_iter</span><span class="p">):</span>
        <span class="n">net</span><span class="o">.</span><span class="n">zero_grad</span><span class="p">()</span>
        <span class="n">inputs</span><span class="p">,</span> <span class="n">labels</span> <span class="o">=</span> <span class="n">Variable</span><span class="p">(</span><span class="n">inputs</span><span class="o">.</span><span class="n">float</span><span class="p">()),</span> <span class="n">Variable</span><span class="p">(</span><span class="n">labels</span><span class="p">)</span>
        <span class="n">output</span> <span class="o">=</span> <span class="n">net</span><span class="p">(</span><span class="n">inputs</span><span class="p">)</span>
        <span class="n">loss</span> <span class="o">=</span> <span class="n">loss_function</span><span class="p">(</span><span class="n">output</span><span class="p">,</span> <span class="n">labels</span><span class="p">)</span>
        <span class="n">loss</span><span class="o">.</span><span class="n">backward</span><span class="p">()</span>
        <span class="n">optimizer</span><span class="o">.</span><span class="n">step</span><span class="p">()</span>
    <span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Iteration: &quot;</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">epoch</span> <span class="o">+</span> <span class="mi">1</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">
<div class="prompt"></div>

<div class="output_subarea output_stream output_stdout output_text">
<pre>Iteration: 1
Iteration: 2
Iteration: 3
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[18]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Awesome! Now it&#39;s trained. Time to test it:</span>

<span class="n">dataiter</span> <span class="o">=</span> <span class="nb">iter</span><span class="p">(</span><span class="n">testloader</span><span class="p">)</span>
<span class="n">images</span><span class="p">,</span> <span class="n">labels</span> <span class="o">=</span> <span class="n">dataiter</span><span class="o">.</span><span class="n">next</span><span class="p">()</span> <span class="c1"># just grabbing a sample from our test data set</span>

<span class="n">imshow</span><span class="p">(</span><span class="n">torchvision</span><span class="o">.</span><span class="n">utils</span><span class="o">.</span><span class="n">make_grid</span><span class="p">(</span><span class="n">images</span><span class="p">))</span> <span class="c1"># display the images we&#39;re going to predict</span>

<span class="n">outputs</span> <span class="o">=</span> <span class="n">net</span><span class="p">(</span><span class="n">Variable</span><span class="p">(</span><span class="n">images</span><span class="p">))</span> <span class="c1"># get our output from our neural network</span>
<span class="n">_</span><span class="p">,</span> <span class="n">predicted</span> <span class="o">=</span> <span class="n">torch</span><span class="o">.</span><span class="n">max</span><span class="p">(</span><span class="n">outputs</span><span class="o">.</span><span class="n">data</span><span class="p">,</span> <span class="mi">1</span><span class="p">)</span> <span class="c1"># get our predictions from the output</span>

<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Predicted: &#39;</span><span class="p">,</span> <span class="s1">&#39; &#39;</span><span class="o">.</span><span class="n">join</span><span class="p">(</span><span class="s1">&#39;</span><span class="si">%5s</span><span class="s1">&#39;</span> <span class="o">%</span> <span class="n">classes</span><span class="p">[</span><span class="n">predicted</span><span class="p">[</span><span class="n">j</span><span class="p">]]</span>
                              <span class="k">for</span> <span class="n">j</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">4</span><span class="p">)))</span>

<span class="c1"># print images</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;GroundTruth: &#39;</span><span class="p">,</span> <span class="s1">&#39; &#39;</span><span class="o">.</span><span class="n">join</span><span class="p">(</span><span class="s1">&#39;</span><span class="si">%5s</span><span class="s1">&#39;</span> <span class="o">%</span> <span class="n">classes</span><span class="p">[</span><span class="n">labels</span><span class="p">[</span><span class="n">j</span><span class="p">]]</span> <span class="k">for</span> <span class="n">j</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">4</span><span class="p">)))</span>

<span class="c1"># and let&#39;s look at the overall accuracy:</span>

<span class="n">correct</span> <span class="o">=</span> <span class="mi">0</span>
<span class="n">total</span> <span class="o">=</span> <span class="mi">0</span>
<span class="k">for</span> <span class="n">data</span> <span class="ow">in</span> <span class="n">testloader</span><span class="p">:</span>
    <span class="n">images</span><span class="p">,</span> <span class="n">labels</span> <span class="o">=</span> <span class="n">data</span>
    <span class="n">outputs</span> <span class="o">=</span> <span class="n">net</span><span class="p">(</span><span class="n">Variable</span><span class="p">(</span><span class="n">images</span><span class="p">))</span>
    <span class="n">_</span><span class="p">,</span> <span class="n">predicted</span> <span class="o">=</span> <span class="n">torch</span><span class="o">.</span><span class="n">max</span><span class="p">(</span><span class="n">outputs</span><span class="o">.</span><span class="n">data</span><span class="p">,</span> <span class="mi">1</span><span class="p">)</span>
    <span class="n">total</span> <span class="o">+=</span> <span class="n">labels</span><span class="o">.</span><span class="n">size</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span>
    <span class="n">correct</span> <span class="o">+=</span> <span class="p">(</span><span class="n">predicted</span> <span class="o">==</span> <span class="n">labels</span><span class="p">)</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span>

<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Accuracy of the network on the 10000 test images: </span><span class="si">%d</span><span class="s1"> </span><span class="si">%%</span><span class="s1">&#39;</span> <span class="o">%</span> <span class="p">(</span>
    <span class="mi">100</span> <span class="o">*</span> <span class="n">correct</span> <span class="o">/</span> <span class="n">total</span><span class="p">))</span>

<span class="c1"># Hmm, maybe we can do better. Let&#39;s add convolutional layers.</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">
<div class="prompt"></div>

<div class="output_subarea output_stream output_stdout output_text">
<pre>Predicted:    cat   car  ship plane
GroundTruth:    cat  ship  ship plane
Accuracy of the network on the 10000 test images: 39 %
</pre>
</div>
</div>

<div class="output_area">
<div class="prompt"></div>



<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><a id='eleven'></a></p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="11)--Adding-A-Convolutional-Layer">11)  Adding A Convolutional Layer<a class="anchor-link" href="#11)--Adding-A-Convolutional-Layer">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h4 id="Home--|---Back--|---Next"><a href="#outline">Home</a>  |   <a href="#ten">Back</a>  |   <a href="#twelve">Next</a><a class="anchor-link" href="#Home--|---Back--|---Next">&#182;</a></h4>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Links:</p>
<ul>
<li><a href="https://github.com/vdumoulin/conv_arithmetic/blob/master/README.md">https://github.com/vdumoulin/conv_arithmetic/blob/master/README.md</a> - Convolution animation</li>
<li><a href="http://setosa.io/ev/image-kernels/">http://setosa.io/ev/image-kernels/</a> - Image kernels explained visually (really helpful)</li>
<li><a href="http://colah.github.io/posts/2014-07-Understanding-Convolutions/">http://colah.github.io/posts/2014-07-Understanding-Convolutions/</a> - good blog post on convolutions by Chris Olah</li>
<li><a href="http://cs231n.github.io">http://cs231n.github.io</a> - CS231n at stanford on CNNs, really good content</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[19]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># here&#39;s all the boilerplate again:</span>
<span class="n">transform</span> <span class="o">=</span> <span class="n">transforms</span><span class="o">.</span><span class="n">Compose</span><span class="p">(</span>
   <span class="p">[</span>
    <span class="n">transforms</span><span class="o">.</span><span class="n">ToTensor</span><span class="p">(),</span> 
    <span class="n">transforms</span><span class="o">.</span><span class="n">Normalize</span><span class="p">((</span><span class="mf">0.5</span><span class="p">,</span> <span class="mf">0.5</span><span class="p">,</span> <span class="mf">0.5</span><span class="p">),</span> <span class="p">(</span><span class="mf">0.5</span><span class="p">,</span> <span class="mf">0.5</span><span class="p">,</span> <span class="mf">0.5</span><span class="p">))</span> 
   <span class="p">])</span>
<span class="n">trainset</span> <span class="o">=</span> <span class="n">torchvision</span><span class="o">.</span><span class="n">datasets</span><span class="o">.</span><span class="n">CIFAR10</span><span class="p">(</span><span class="n">root</span><span class="o">=</span><span class="s1">&#39;./data&#39;</span><span class="p">,</span> <span class="n">train</span><span class="o">=</span><span class="kc">True</span><span class="p">,</span> <span class="n">download</span><span class="o">=</span><span class="kc">False</span><span class="p">,</span> <span class="n">transform</span><span class="o">=</span><span class="n">transform</span><span class="p">)</span>
<span class="n">trainloader</span> <span class="o">=</span> <span class="n">torch</span><span class="o">.</span><span class="n">utils</span><span class="o">.</span><span class="n">data</span><span class="o">.</span><span class="n">DataLoader</span><span class="p">(</span><span class="n">trainset</span><span class="p">,</span> <span class="n">batch_size</span><span class="o">=</span><span class="mi">4</span><span class="p">,</span> <span class="n">shuffle</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
<span class="n">testset</span> <span class="o">=</span> <span class="n">torchvision</span><span class="o">.</span><span class="n">datasets</span><span class="o">.</span><span class="n">CIFAR10</span><span class="p">(</span><span class="n">root</span><span class="o">=</span><span class="s1">&#39;./data&#39;</span><span class="p">,</span> <span class="n">train</span><span class="o">=</span><span class="kc">False</span><span class="p">,</span> <span class="n">download</span><span class="o">=</span><span class="kc">False</span><span class="p">,</span> <span class="n">transform</span><span class="o">=</span><span class="n">transform</span><span class="p">)</span>
<span class="n">testloader</span> <span class="o">=</span> <span class="n">torch</span><span class="o">.</span><span class="n">utils</span><span class="o">.</span><span class="n">data</span><span class="o">.</span><span class="n">DataLoader</span><span class="p">(</span><span class="n">testset</span><span class="p">,</span> <span class="n">batch_size</span><span class="o">=</span><span class="mi">4</span><span class="p">,</span> <span class="n">shuffle</span><span class="o">=</span><span class="kc">False</span><span class="p">)</span>
<span class="n">classes</span> <span class="o">=</span> <span class="p">(</span><span class="s1">&#39;plane&#39;</span><span class="p">,</span> <span class="s1">&#39;car&#39;</span><span class="p">,</span> <span class="s1">&#39;bird&#39;</span><span class="p">,</span> <span class="s1">&#39;cat&#39;</span><span class="p">,</span> <span class="s1">&#39;deer&#39;</span><span class="p">,</span> <span class="s1">&#39;dog&#39;</span><span class="p">,</span> <span class="s1">&#39;frog&#39;</span><span class="p">,</span> <span class="s1">&#39;horse&#39;</span><span class="p">,</span> <span class="s1">&#39;ship&#39;</span><span class="p">,</span> <span class="s1">&#39;truck&#39;</span><span class="p">)</span>

<span class="k">def</span> <span class="nf">imshow</span><span class="p">(</span><span class="n">img</span><span class="p">):</span>
    <span class="n">img</span> <span class="o">=</span> <span class="n">img</span> <span class="o">/</span> <span class="mi">2</span> <span class="o">+</span> <span class="mf">0.5</span>
    <span class="n">npimg</span> <span class="o">=</span> <span class="n">img</span><span class="o">.</span><span class="n">numpy</span><span class="p">()</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">imshow</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">transpose</span><span class="p">(</span><span class="n">npimg</span><span class="p">,</span> <span class="p">(</span><span class="mi">1</span><span class="p">,</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">0</span><span class="p">)))</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[20]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="k">class</span> <span class="nc">Net</span><span class="p">(</span><span class="n">nn</span><span class="o">.</span><span class="n">Module</span><span class="p">):</span>
    <span class="k">def</span> <span class="nf">__init__</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>
        <span class="nb">super</span><span class="p">(</span><span class="n">Net</span><span class="p">,</span> <span class="bp">self</span><span class="p">)</span><span class="o">.</span><span class="fm">__init__</span><span class="p">()</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">conv1</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Conv2d</span><span class="p">(</span><span class="mi">3</span><span class="p">,</span> <span class="mi">6</span><span class="p">,</span> <span class="mi">5</span><span class="p">)</span> <span class="c1"># convolve each of our 3-channel images with 6 different 5x5 kernels, giving us 6 feature maps</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">fc1</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Linear</span><span class="p">(</span><span class="mi">4704</span><span class="p">,</span> <span class="mi">120</span><span class="p">)</span> <span class="c1"># but that results in a 4x6x28x28 = 18816 dimensional output, 18816/4 = 4704 inputs per image.</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">fc2</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Linear</span><span class="p">(</span><span class="mi">120</span><span class="p">,</span> <span class="mi">10</span><span class="p">)</span> 
        <span class="bp">self</span><span class="o">.</span><span class="n">sigmoid</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Sigmoid</span><span class="p">()</span>

    <span class="k">def</span> <span class="nf">forward</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">x</span><span class="p">):</span>
        <span class="n">x</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">conv1</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>
        <span class="n">x</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">sigmoid</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>
        <span class="n">x</span> <span class="o">=</span> <span class="n">x</span><span class="o">.</span><span class="n">view</span><span class="p">(</span><span class="o">-</span><span class="mi">1</span><span class="p">,</span> <span class="mi">4704</span><span class="p">)</span> <span class="c1"># since our output from conv1 is 4x6x28x28, we need to flatten it into a 4x4704 (samples x features) tensor to feed it into a linear layer</span>
        <span class="n">x</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">fc1</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>             
        <span class="n">x</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">sigmoid</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>
        <span class="n">x</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">fc2</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>
        <span class="n">x</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">sigmoid</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>
        <span class="k">return</span> <span class="n">x</span>

<span class="n">net</span> <span class="o">=</span> <span class="n">Net</span><span class="p">()</span>

<span class="n">NUMBER_OF_EPOCHS</span> <span class="o">=</span> <span class="mi">3</span>
<span class="n">LEARNING_RATE</span> <span class="o">=</span> <span class="mf">1e-1</span>
<span class="n">loss_function</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">CrossEntropyLoss</span><span class="p">()</span>
<span class="n">optimizer</span> <span class="o">=</span> <span class="n">optim</span><span class="o">.</span><span class="n">SGD</span><span class="p">(</span><span class="n">net</span><span class="o">.</span><span class="n">parameters</span><span class="p">(),</span> <span class="n">lr</span><span class="o">=</span><span class="n">LEARNING_RATE</span><span class="p">)</span>

<span class="k">for</span> <span class="n">epoch</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">NUMBER_OF_EPOCHS</span><span class="p">):</span>
    <span class="n">train_loader_iter</span> <span class="o">=</span> <span class="nb">iter</span><span class="p">(</span><span class="n">trainloader</span><span class="p">)</span>
    <span class="k">for</span> <span class="n">batch_idx</span><span class="p">,</span> <span class="p">(</span><span class="n">inputs</span><span class="p">,</span> <span class="n">labels</span><span class="p">)</span> <span class="ow">in</span> <span class="nb">enumerate</span><span class="p">(</span><span class="n">train_loader_iter</span><span class="p">):</span>
        <span class="n">net</span><span class="o">.</span><span class="n">zero_grad</span><span class="p">()</span>
        <span class="n">inputs</span><span class="p">,</span> <span class="n">labels</span> <span class="o">=</span> <span class="n">Variable</span><span class="p">(</span><span class="n">inputs</span><span class="o">.</span><span class="n">float</span><span class="p">()),</span> <span class="n">Variable</span><span class="p">(</span><span class="n">labels</span><span class="p">)</span>
        <span class="n">output</span> <span class="o">=</span> <span class="n">net</span><span class="p">(</span><span class="n">inputs</span><span class="p">)</span>
        <span class="n">loss</span> <span class="o">=</span> <span class="n">loss_function</span><span class="p">(</span><span class="n">output</span><span class="p">,</span> <span class="n">labels</span><span class="p">)</span>
        <span class="n">loss</span><span class="o">.</span><span class="n">backward</span><span class="p">()</span>
        <span class="n">optimizer</span><span class="o">.</span><span class="n">step</span><span class="p">()</span>
    <span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Iteration: &quot;</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">epoch</span> <span class="o">+</span> <span class="mi">1</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">
<div class="prompt"></div>

<div class="output_subarea output_stream output_stdout output_text">
<pre>Iteration: 1
Iteration: 2
Iteration: 3
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[21]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Holy guacamole, that takes a LOT longer. Those convolutions are expensive.</span>
<span class="c1"># In the next section we&#39;ll make that a little quicker.</span>
<span class="c1"># For now, let&#39;s see how much our predictions improved.</span>

<span class="n">dataiter</span> <span class="o">=</span> <span class="nb">iter</span><span class="p">(</span><span class="n">testloader</span><span class="p">)</span>
<span class="n">images</span><span class="p">,</span> <span class="n">labels</span> <span class="o">=</span> <span class="n">dataiter</span><span class="o">.</span><span class="n">next</span><span class="p">()</span>
<span class="n">imshow</span><span class="p">(</span><span class="n">torchvision</span><span class="o">.</span><span class="n">utils</span><span class="o">.</span><span class="n">make_grid</span><span class="p">(</span><span class="n">images</span><span class="p">))</span>
<span class="n">outputs</span> <span class="o">=</span> <span class="n">net</span><span class="p">(</span><span class="n">Variable</span><span class="p">(</span><span class="n">images</span><span class="p">))</span>
<span class="n">_</span><span class="p">,</span> <span class="n">predicted</span> <span class="o">=</span> <span class="n">torch</span><span class="o">.</span><span class="n">max</span><span class="p">(</span><span class="n">outputs</span><span class="o">.</span><span class="n">data</span><span class="p">,</span> <span class="mi">1</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Predicted: &#39;</span><span class="p">,</span> <span class="s1">&#39; &#39;</span><span class="o">.</span><span class="n">join</span><span class="p">(</span><span class="s1">&#39;</span><span class="si">%5s</span><span class="s1">&#39;</span> <span class="o">%</span> <span class="n">classes</span><span class="p">[</span><span class="n">predicted</span><span class="p">[</span><span class="n">j</span><span class="p">]]</span>
                              <span class="k">for</span> <span class="n">j</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">4</span><span class="p">)))</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;GroundTruth: &#39;</span><span class="p">,</span> <span class="s1">&#39; &#39;</span><span class="o">.</span><span class="n">join</span><span class="p">(</span><span class="s1">&#39;</span><span class="si">%5s</span><span class="s1">&#39;</span> <span class="o">%</span> <span class="n">classes</span><span class="p">[</span><span class="n">labels</span><span class="p">[</span><span class="n">j</span><span class="p">]]</span> <span class="k">for</span> <span class="n">j</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">4</span><span class="p">)))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">
<div class="prompt"></div>

<div class="output_subarea output_stream output_stdout output_text">
<pre>Predicted:    cat truck  ship  ship
GroundTruth:    cat  ship  ship plane
</pre>
</div>
</div>

<div class="output_area">
<div class="prompt"></div>



<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAXQAAAB6CAYAAACvHqiXAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAALEgAACxIB0t1+/AAAADl0RVh0U29mdHdhcmUAbWF0cGxvdGxpYiB2ZXJzaW9uIDIuMS4wLCBodHRwOi8vbWF0cGxvdGxpYi5vcmcvpW3flQAAIABJREFUeJztfWmMHdl13ner6u2vX+/d7ObOITm7NDMajSRblmXJTkayLRmJ7Mgx7EGiYIDAQuzAQCzHPxwB+WEjgR0HcBQMLFmyY1hWJNlSZMWRPFq9jDScVZrhcBmuTTa72Xv321/VzY9zbp3TG9lkU2x2+34A0cVb9aruvXWr6pzzncVYa+Hh4eHhsf0RbHUHPDw8PDxuDfwL3cPDw2OHwL/QPTw8PHYI/Avdw8PDY4fAv9A9PDw8dgj8C93Dw8Njh8C/0D08PDx2CDb1QjfGPG6MOWGMOW2M+cit6pSHh4eHx43D3GxgkTEmBHASwE8AGAPwLICft9a+euu65+Hh4eGxUUSb+O1jAE5ba88AgDHm0wDeD2DdF3qxWLQ9PT2buKSHh4fHPz6Mj49PWWsHr3fcZl7ouwFcVP8fA/CWa/2gp6cHTz755CYu6eHh4fGPDx/96EfPb+S4zdjQzRptq+w3xpgnjTHHjDHHarXaJi7n4eHh4XEtbOaFPgZgr/r/HgCXVx5krX3KWvuotfbRYrG4ict5eHh4eFwLm3mhPwvgiDHmoDEmC+CDAL54a7rl4eHh4XGjuGkburW2Y4z5MID/ByAE8Alr7Ss3ep79818AABibpG3ZDHXLBPK9abWaAIBO3KZjstl0X5zQb20iFh8TxACAIFR9bpdoH2hfJttI94Vw15RzxEkHANDuSN+ShC1NJuL+iOWpyfu0LSrhcRkjra0WjSGOo1VjD7hvrUTaqtQN1Fpx2la67wlofPjDH063O53OqmveCtzw+eyKv7op0G3UGrhGbbgzbv4SdbybZznJtby11uq3O/5jH/vYqn37f5TnNu6kbdNXrwAAmg1ZM4fuOgwA6OmuAAAyofQnm6GFl9VtvJ4jo9ZYpw4AKJcyfA7pa8TboVrEs7MzAICurq60LZPJ8HnpOBPIOTpJCwAQrCG6BUYaa1Uyh0YRrcl8Pp/ua7XoHB1+BgGgkC/wtaRvv/+7v7Ps/Hv2DqXb5YGj9LtQnttKVxkAsNiUdV1dmOb+0v1O1GKIeBCFKJe25UN+hannNn0AuSlO5PyuLVFt7hpu7HR9nss11o7h+2cC/V6I1ziOfpvLUX+zgfQblrZNVuavNn0cAPD1Z76/6lwbxWZIUVhrvwzgy5s5h4eHh4fHrcGmXui3Ai2WsqytSyNLpzmU0qYA9CWLIpa8tcTBX12TkcamkyoS+QJGLAGG3BSpc5iEpGZ0RApx0nKiztEyJLnEIX1hW3pfHPC55GttWMrPq75FLBkFEXU8brdVRzo8JDmHk0jDcH0LWRiG6+67VbhZiV/PRypHKSkycSKV5TFY2ec0JgORhuQsm5fQ10K5SPc2sPJ4NKvUlrSE2M9n6bylAh0Xqcu4tZNTi6yQ5fuuxtKM3XG0rrJqnbgpiiK5t07yD5SU7+Ymx1qrXibVWpuvKXDarYWcN+CLZVhKdVI/ALSbTR6fGgtLnbjGmkisSPmdsJfOlZFnOg5JQg8ySkKvL1Hf4ir3Q87XtHRcW0nGDZ5fJbSj1SYtKuBnol6Td4t7TvT4nMYcBPIcWqfZ8GRqi0CnE/Mxck1j3PtJ1kxvL405V+ji88s9S9y6zkk/4qUyNgsf+u/h4eGxQ+Bf6B4eHh47BFtucrFskoAVU4dlMsrEohImbVKBwgKbNZTa6qwNmpjIskrVsaLSJO1w2XFOdQIAY1cQcwAMEzg2FNWxHpNud2Wa1LNqS9SopSVqC62ctyvP5Jgi9SpFIpQKORpnErTSfUFqXpGxuxG0k/XNBNqE8IOqE7uR8y4zb7jjl+mmbpc2EdGcN9s0H5HWs2P6bWjWunayRtvGcK2xRGz2CpTZKxvStTKBtOUCNqe5fYrQbNbJNBOGisCL6L63m0KsBmATW4farJFHMmbTUjZTkOPdPKg15sjhmM2GOt5j+upVAMDwQK8cz+aVMCvXCvlabp6V5QcRH99UJLEjbNttaVuJwMq+mPsbq+cgNjTmfJf0o3//MP12fhYAUK4tpftaDXpHxGV5HpNuijzvysrcu+sGbJdtNeX5cg4U+bzcl3RK1Zpw69j9DZSNt8NjTvTy48tnI1m7hQITx3BmQzHpJM6cq2XqW+DE4CV0Dw8Pjx2CLZfQo5gl81C+jgFLGrlQff0d48RfykAzP/zTjpZgHcmTFelm14G7AQALc1MAgKlpkWQyEUnjAeTL3erQ9NStBEQdP08Sj831AwDaoZA8LZYcluZn0rZLEyxp5JXkNT4HANi3i67Z36WlOOfKKGN3wkdsV7tGOWjJ+Fa4K94SKT/tt9Ie2LWzo8SbNmtKp86cAQAM7xJ3t4TJ7cE+kTDzTCQlm+jjteYoy1J40hHJLmTpKqMIuQy3BTGto2xGSX0hu8Yq7SsT0L1NjNLIEnbHbTA5qtZTg8deLMoaDh1TqsVDnocqu1Q+99zz6a42awq9lTenbbkcOweoKUhdZ1l7DZS7oLHOOUDWpE0cMbi+hN6BuFYGoLWehIoQZi0tVNpaidnNSpHv8fPPpvtaUyStjzxwt/TtKj1zTSPzVuaBLdaJWM2rseRYYw/6hYAMmBTVr5Rmkc4btVlzactkLZbovuTm59O2aO99AIBaT3falrDWFfM9yydCrKYWgVjawnjz8rWX0D08PDx2CPwL3cPDw2OHYMtNLk4vN5Gk1XXqcEdHUDIB1WI1OKvIpjh26p8ySfA5tF/vW378JwAAz/39PwAALrPpBQCqHRf5KarY+bFJAMDZsUtpW653BACwZ/ggXTMnamWL1cVMWbJcdhqkJk5PSpqbYi+Za8aWKPqwodTn4S5SCYsZUUPjNqnNOhhuJR24Fil6OyJFr22aYfIto6J62ce8viQk+Nw8qcYTU2SqKnSJ+tzPEZE6qtGRgDp6dI3OrujFxpFl855V58i4yY+l3yEceU9tGeXX3XbqdiLnCCs0D8aquAP2d05cNHIs63ppgUxz5aKQgAHPt47ajDiyeo7J0JkFMSUW2E+7pSwjrTZdK8rqNUNtMUdid5S5yUVpZ5WPteU1m8TrmwH1zDsTYqDGHnd4rMrWYdgk0jB03zOJrAUzQKa42qL0rX32JPXXiFkq4emqOv929Xxl2xw/clGR8jwf2tGiwebTsMFzJZdEcxf1sX5FTKtdhp550z0g4+PrtgNHNKvYC57vUJHsUbB5M6eX0D08PDx2CLZcQm8G9CWer6kIMpZuessiVlSYZIpYQtGEVep2pAgaR5rWarNp29e+RHljJuZI4phYku/Z+Ut03PnLkuI9zJO0HoeVtK1UoS9xpkj7orxIBjmWIvOBjGWqRVFqI3v2pW0NJmvOnCEJfWZO5ZTZTec9MCiaQoZd94xyGxP5jMervv42uTGZNA3MXENA0FJ5sIaEHrMUlrA0oqNZXQTe1emFtG2hSmOt6/wdNRpNkCPyuVqXe1suskSq+ubk/Y0qIDeqqeSMc7GT+XZk6JouhwlHJiqXw4g1ykgxj6Gh+bCxvns8PnYEiJVr29IizdsFfc3IRVaLNLm3QvPmXBRfevnldN8b7r8fAJBol8qY5jevXXpZU6jXWAOO5Pwd1hDDSJwD2pwvqNlcPyV2rKT3hNew1TIkOzG0tHsjX7d7kedqcDjdVxjaT/2xQkaCXS/twK60qZ7h3CxXKC8MlAtwlZ9XO9yftmUS6lNDafgl1hJbizS+ps6xU+CI3Krcl6iftAeTUW6ZnK+li38aKg2gY2juTaBcdLH5aG8voXt4eHjsEPgXuoeHh8cOwZabXK7WSc2YaQsp+s2/+wYA4L6jYrr4sfuJbOhlf3VNxrgkPIFSX2ImXxSXhrPnyc95pk6qkC32pfvCMpNvfWIeKHD905ZKmdpiIq7SS32rlKWPk1fIhLIwq8gSVgnzBTHNXJglMjZTIXVyclyqS5WvLAIAdlXk+IJL1ZsoMm0FqjWd3IxVTqVqutTCoUr05LZdOlCVEwtBsvpb76JYta1jic0BjhwtKOKswRF148rkMjlL24kizNpsT6ktEoE8OSXzN3ZpHABw35FDadtdB/ZQ/5VffkrOukhfbWVx3dZhCtegSkM2+SVtMScEbOKrz8tYwOYGy0mdwoKMPcv3Kqvm27TJ1BZrMwVHQ5uUiBVzU7VKpoWJCTm+VCnzNVViMp7z1hIdl1f+8FfniFh9/vtihinl6JqHD8mcRmz6adZo/RUilUiqSWsrVmmkY/eoNdR8rISaYpfCNlkWK8L71LOcYXNX7vQpOv1z3073dd7MpiqVhtZyjEh2UZ6NBmgeyhzvEebk+KRE5zdWEfWcHK+rX95BmUtsrlmiNZkZFucHXKR9UUXMoo2rNL9hUdqSo+Sb3uDEXoEi8bMdmpxI2RLtNTj+jcJL6B4eHh47BNeV0I0xnwDwUwAmrbUPcFsfgD8HcADAOQA/Z62dXe8c1+xAN0kJtWn5trSzRDzO1FTy9xa5EVWy7OaliBQnkYahkDaNFkm4VxX/NLVIX+diDxEivYNCVFYTkjQGoKLymEBpZURqalRJgmks0fH7FblSY2l8siXSsmFpaX5GSWUsrdT56x9mpd8TCzSN4/OiFewfYA3kGl/wuboMtFwkrSFQeSVcsY5lgrcja1wQ7rK0tWt869dwh7wyTi6dfX2k7RTyIvk0GzTmYk7adg2SpmWV+Fat0VhLLMm0GirdKQ96qSnj66R5NpQbXeo+6fatGuYyifFa3pZ5V8BAHeQk9JzSCspMPnczmRWw+yUA5Pge57VAylpU0JC1kBY94EIprQVZa10l2tfbJ5rk2THSAs9cvJK2nTz9NABgdook0qWGnKPWppozEZQbIkv+D959NG17308+DgDYzeu5mZdxNqpV/p1cs8IF6E19EeshE8r6c+mvHTkKSArZSMmV5Vm6VmeM3HwrSttYvEzXb+UlGtOC3gvmymTaVhplQrPCmifkWSqwu2x2TvrdYCK6MzWetmV5DjsLNFe5GXGMaNdZmyqIhjN3lpwpsgWR0LtGiMR1qaCsclFsOjJcreFWsnkRfSMS+icBPL6i7SMAnrbWHgHwNP/fw8PDw2MLcV0J3Vr7LWPMgRXN7wfwTt7+FIBvAPj1m+nA3W94DAAw9syJtK3cTV//x972lrStGJKducUSspY+DWeji63k++gaovrVL758Ss7bQ9Lh7v3kymWVLS7DUnjSnE7bWq1k1bVC/qK+8tJLAICKSlBfLJFkUFJ2tMtXJgAszzMTstTRx+5mc7Ni/5udoe2z4+KaNTpMLllRVkU3rEBUEU0hZum6revvsW0y/Quxa7pgFS2R2jV8GJ0Arzwk0wAXl+8DynW0h12/2m11LpbaimWxSToJ3XCwmFEuYrmCc+9SZdWYGFlmc1zVN7lmZvkhvHt9Ef3iuXPcb5nvxQVad3FbNIVLl0g7meU1UF0Se/JQP0nV5ZIEBYVcnKWlMhRGnGso4FxCVSW9N9xgVKGNC5eJfzk7JjxDtUW/zXez61xJJsatxFJWZLfx8xSMc/nyRNr27W//HQDgXuYqBntEIq0vkeTvysMBQPteyqeyNL++Yp7Lytitk9YTpTKzhhMoN9slDgRcevSNAIBK9KZ0X22R7kFb5X0yOZ4bVZ4xU6DrVtk9U7vbtjlfSkY9G3WeG+00WGe7fm2JrlkqyFgafHyuLM95Xxe9e2L1rljitQt2oyy0VcZG7pP2MG7fgvxJN2tDH7bWjgMA/x26zvEeHh4eHj9g/MBJUWPMk8aYY8aYYzpPs4eHh4fHrcXNui1OGGNGrLXjxpgRAJPrHWitfQrAUwAwOjq6SqcodpOpYP8hIWjqbIHYd/Bw2jbAavvc2XMAgLaOLuuQ6eKxd/xM2rbv0KMAgIMPnkvbnnuBzCS9ZTJhXJ6UXC4RuzHldHEF7u1SVciuuRlSO/vKGX0I9YPNKgODksvFFW2YmhUTiuFoyi52eYxCRYywyv36xbG0bbCX1PIje5Tr1Ap84o//l5yf+5FR6l+5i1TGwweFCH7zG8itypW9tMos5EhGq+0rLseOMqs4wi6bo/NrsjObJRNKf69yn3S1YVWNxjRHSIbO0ejI+eeYJJ5TqUoX58kE0Naumkxk9rPr2ZHDQlhlXDShLgwfLDPALMO3//4ZHq4qsOKI7LqshXNXiLhLa38q8ai3m0wWJUUS5/i4jHJljNilLuCaojVFaEZ8DqvyFl2ZISK9rdjtYpdzt+N8R0vK3ZLvR6Mh/a500Xnf+qYH07Yqp3xusIvuhQtiSnn99ddp7MrF7vw0zX29JueNckLuA0CpJA4GHZ6HdqzvGReaUWSgYRNUYZiIz4WqjOXqPI3dKHfcFtdMzWpycY5+43JB5bLyHCzwGs9n1KvPpTVWkaJNjl4G1wyer8uadGl0iiqatmsPmXhDbQZM6+HyvdK1LNybQy3K5Bb4Ld6shP5FAE/w9hMAvrDpnnh4eHh4bAobcVv8MxABOmCMGQPwWwB+G8BnjDEfAnABwM/ebAfCHBELlyeOp20PvYmS8Ze65YsfLhIBFbOUEKnyWWcuEnHx9t6DcuIiBZ90lVSV9oiuVWA3wXxWlQrnr/Pu0ZG06VWWTLKK3FlgYubgXtIojt5zX7pvZoaLWVQkQOEyu1MZRcL09JJUO8/Sp85/UijSb+uL0u9TFzjYQxFbw5K6go6vqeCnOm1nVJDPIgu4RdUW33sPAKBhmTxSEnqOJSUt1bpCFToLYXcfaSMp8aTcHZ0bVqikcRfppWWRhKWVcxz4dWlSFL6ZadKI6nWR7OImS6Iq54vLKbJnLwVr7du7J91XSteKJn3Xl9BfPEX9KBZEI7KsETY7cl+6OWumI/9aSgq+ukT3IFRz1ZUnjawTCwlumAQM2bfNRBKolquSZNlqC9k6M+PIUF0ujf62OEfMYlXmqsXurHsHxfWxv5cWjwtcAoCZWcoD099D/Xj0jfen+8bYNXW+Lmv4tTG6L4Fa1wcl7QoAIFKZTgtd9MwtqZJyEas0scoyGHHwTcBrMlHuloYL3kTqmm6r3VIZJlnLjljy1hqRI0NjpQW60nYdtSozBSYt49VZW13ul0xHaQrsMaAzNuZjl6GTr6WWnAusW+5FvPnsqBvxcvn5dXa9e9NX9/Dw8PC4ZfCRoh4eHh47BFueyyWTJ4Km0dDqM9dvVBGUxZIjmcgUoOuNliNSmT751MfTtp/+Fx+mc6jotizXUnTFMg4e2p3um5whgquxJGrzriHyW9cFA5pc5/HQYSJs7zosZO78C1TLsbooaqUjdToqQq7OJpEerj8YW4la6+4ldbGjKhKEAY1v7LKYIobfgGX4uX/2z6WPTBaWVP4YR8IUlKnKpZZYWOD8Kh0xBWSYpIuU/61l1bWu/LNtQudzVdE1ERvx8ZmMjkBdbbZx/rcNzn9SUjkyejmfTtySvuVDGtfctJgMxi6dAwAcZiI9DJRpybqK9irF8DVcfhfYrGc18cixBYVQ5mPP3ruo/y5N8BVZa1NsKhoeFo/e3ACZgapz4s+dcCRsdy/ZK3I5iaVo8JBrHTG55Pk5iNuyxkImF13Rl0xWFdrI0/Zjj4gJ5ej+UTp/S9b62ddpXK+feBUA8LY3C2G6dy8df+FlyTnUjl1OpfVrimZVP7JcUzexYuYsMAneUWmKFzlSNmbiM98tpqLhEpvAFHno1rU2V4RwNVPpry7MsRYsP5va5BKzr7tLUxyoa2adoUclimryO0XnjorY5BiD88fooiv83Oi6rtr0erPwErqHh4fHDsGWS+iGI8hqSjJusISZ0XkcptmliPO1ZDCX7hvpoS/mqeMSFXp57DRt1KT02/mxcwCAh3dRdOru/cIsjk6ShFQ9LVJIX46kw64eKSv1+utn6ZqjJN3PLYj01OYv/cRVJYE5skS5JtZYQjec20FTISWXvTGRyM+sofloTV3BekjaIkGkEoraX87SeQt5mdM6Z8qrtakf586ck2syKbrv4P607exFmssv/fXTaVubM1zmOV9LUZ3fRdd1VyTqsKebpKyHHxYVY3CApNK79tCcBspd0ElZjrgChOyqD4n0NjpC92p0N5HaOoNfjV3blmks1xBlMkzUDw6Npm15JqSnpsSdtMpRyy7cr6EiQLsHaW3tVq63Xd00zsqASO3TTKTHLLG1VUU35yJZU0Riq+0IT9FYsi6jZ47uccaKBjXEcz/YK/cgzwTfYK+wmBV27Zu+cAEAcP71c+m+XX20/ucnnknbMkyGt8L1XyGRyl0SchbJvMrvMjdJBO/MkuRQuTpO89vbRev/gftEU8iwdt5UhHCbNQRN6Lv174q+BIqod1KyLp0Yp0SsZi2X5wbSmVyRnkOeuYiP12vX/SbjNCf9oPPpA+WCGV/DlXaj8BK6h4eHxw6Bf6F7eHh47BBsucklTX2r1JeRAVK3tPr+tZfJJ7yXk+wf6RMVKJ9jUigSX+yrk+fo9E2JeNt3F/mph3zeYkUIqIFhIqymZ0S9nWcyVBc2HxoidTlic1BDkZcu6VJdmQc6/OOOOkmjyak5O/Q97VcquOFag1kjY8kxaRTb5ZF4Gn/5f76SbiecsD9QPrxlJpi7lPnjwBEa82A/mRj6RySKtI/7lFfJpeaOkznqe8el7mrdumIa9P9IqcMV/u3hfWK2edtjj9C1SuLjXWK13Wm8LTWnHfatrs2Lia3NftyFovStp4fMDROcDG1KFckocMTi8C6Z52JRxSCsQC+b2EJlTmhyIQ+jZKCZaerTwgKnQVYmwpAjDM9fkgRYlQUyl3R3S5yC8z9vslOAUQRhzkUzluS+F6yLLNW5gOmZKBXYHGnFHLOnn+alqAjK6gL1u6NMOa74x0E2ER1/7Uy67+hRSsQFRYBevky+6fleMXsBens5CeiKrSTK/LHIMR1Xr4opcW6Wznvy5e8CAF576R/SfYcPU8zHgcP3pm29A2w2UuYKlyraFTvRhoww9WFXfUsLvUibq5ErhXQU6crHa149jaxeg21PSddlye/4rOp+63fJzcJL6B4eHh47BFsuobsoru6yEFY9XbRtVM6QBUuSxtQsfSkHuqTrJSZ04kAkk3OXzwEAhnslGf5+/sI7d7DvPifRqZfGSZLvKovUnmG3qldOX1A9dpGO9LepvqpLHKHXowoSdFjsHJ9QCfi7qE8Ru0YViyKBufwnaAuxGlepb8ND6+dyefaF76fbhQwRlM2mELZZJvXe8tY3p23nL5GkPc2c1AP3i2tblgnNWlOk/AxrNo88IoRmgyMRsyxNHjkk0br3c4rV0QGRSCtFureJclO9eIWiFCdnubjH1NV0X5XJ8rk5kdBbnMI2o1wwXS4ZF0ncVgRlsYfm7QHI+Lq7159LJ2nXVCRqaFwJP9EKYk7FGnEEcmJFPsrm6PwDAxJ5XOY1nleuoN3c74jvmXbntOwa2FHupN3s0hmo6MqE08RGLrqyKZJ3NyeQsR3RGmPWeloq0rHO96PIa/P8FVl/r75O2l+zKRGo7QbNrw019b4+nFSbz8vY77mbIpUP3yvuw7VFktZfeZ5cgF84JkTst79FGuLxV2WtH733IQDAkbtFau/ppfXmyOJwWR/d/K6Re1mTra5kXmd12UcXPRorEjVJ3SfXx7L01MaVzZQ1rFNs3yy8hO7h4eGxQ+Bf6B4eHh47BFtucnHRe7uGxCfc1RhMFLk4sodU+WNsSpkzkqLWhqSWdw8I8dhdYR/QvKjWB9jkUuaUvX/0iT9J99X4Wgt1IdNq7AesM23u4kjOxgypf9WcviaZhV47If7wExNkPlhQ0aM9PXTCSonU51CRWBmO3gtrl9K2wRLt786LQqeSkAIArl5U/vN9ZDbas0dIwPvecITOn5NzvPIiEU/DrAaXVTWjSa6vWKqIyaq/Qse97/F3pG0BO3R3d9NxA/3iPz/DqYbPnpf5mJ8jM9DCvETHLjL5PMdpimcWJAK0wwRvRqU1znKFoEBF1nVXaFw9HFnaq8xTOTZpZQti2lqqC+m8Ev3sQ659+8tcfSZR6V8zAc3HEPurGxUlm2WfaWcKAoA8R0uGKs+uM7GkVZqUycX54NeqsnZcxGJOLUrL5pfaPM33pXMy3zPs/NxTkOOHOcVwPq9r8LIJJSJzU1QU8vwq1/fcOyLPXBdX81pork/kJSotrkviZQPdRn0LlW96Tz+loX37O2ntHj4sJry//eY3AABnz8qzUX2Bn9sFMck9+AaqdrR3L51Lp6eOO7TGY9W3hE27y6p0pfVz3V/Z5ertaoLcWUu0z7sjSNNrLSNF+R2nzDbahHOz8BK6h4eHxw7BlkvojgSs9IqE3ompW7lI3MCOcmGGY8+R5LWQkQi8xJC0N7xbvvSvHid3px/60X+Vtv0DFy6oVklKbLekwMXkFeeKJ9+4Ja4BGKmovN6AJPjdBTrH/FWRhjohScbDQ0KsxuzqVVcSYaNOEmmVybdOIhJYu0GRckMZkQRHyyRJNTvStlJCv3TylXR7gYmzn/4n/zZte/xxSo75N18T98YhJguHihxFqlzh8hw9N9wtkloXb+eVu2CHpRonieqcNVdOkCR1YVJc91pcqCTKS5rYri4ikYdYYmy3VhNRGVWkwOW80LkvurpoLJVKF+9TdSo5n87EhNzvRmP96llFlk7birgtsAtmT0W0niRN5UyEZkHVSU1JLyUdJpbbtBzliou4v4qs6/D97sTS14VpGoN+cDMsoS/NkzY4flmio4f7aCw9JYl2rrF0nShNocNndETsbi7YAAB3c53Rh+6ToiEnz9Dz8sL3xLFgJXTK6IALUASRaN0ZdgqIVXSlSz8bMEl85KgQ8Am7+Y6Pfy5tm52isZ5qilY3cYnqE991hEjXe++XcwwNE0kdqXdLp83FN1RK3Zhr5Lr7uGZBlGU5ZVbvT1M08zzoU6TFZJTovywa9SbhJXQPDw+PHYKNFLjYC+CPAewC+fo8Za39fWNMH4A/B3AAwDkAP2egHt4UAAAgAElEQVStXb8E+DpwuUt6B0SC6PDXvBFIYYR8mSUNzlB44aIEI7z9zeSO1liSL2axi9wExy9J7o3TJ6naecdVA1feTFW223b1i5vZ/DxJRt1lkUjvPkq5JZ596TUAwPPHz0o/fuy9AJZniTxzmiT4OZWx0bk8Nuokme8fFsmuwEEkfX0iGduIJIdOa323poYqBfbgG6mP73r3u9K2/h6ybf/wW5T9myW7LtYUKmWRmkMu2uCq0gNiq9VFB+ZnyW5bYYknURlkDt39AABgaI9kpJyZJc2mq0dcGV3mPmNXV2R3dlhXGg0AltimbFXJMFc44eI42f6dFgQAbS7+ofO7FEvrBxZVWZvqUgUuXJDRpMrTs8DBTglnZTzsAnAA9HD+kzCjpU/a1lpMi+uZ1Zg7aTSl350WzZVRBTFsk44vKY2lp4c0nEKWbNyRkXXSw9pdd5esyRafo6aySbY4w2nAgS69SjMrcpbSMcXTsHCN++8+krZdVe6mdC7NB7C9XPUty7sT/SCy5OpszC2lre3ZewAAcODAgbTt2Qm63x1VHu/q5Bz3h6T348dfTve5wKm77pJ+Dw+T22RXl/BF4AC/Rott7urZy7BGpoOInNuijiuyRrtG0qjS06cFMQThLShwsREJvQPg16y19wJ4K4BfNsbcB+AjAJ621h4B8DT/38PDw8Nji3DdF7q1dtxa+zxvLwI4DmA3gPcD+BQf9ikAP7P2GTw8PDw8bgduiBQ1xhwA8DCA7wAYttaOA/TSN8YMXeOn6yLhGo3dfVLUoFonNacWi4riCDBXK/LkK8oVrkaqTbkkuUi49gDOnxQ18RKTRW97G6XP1WlJuzgdbt+ouEldmCGzSr2pktuXSL2tDBJp9HCX1K68yur4ufMvylhqZJ6Ym5drDQ2SatxtqT/7y+LqN1ThohBGTCguZWpJqbDi9Ec4dM9D6fYHf+nf0PhiUctPnCZiMjEqBw6Tp21W/2bmVNKaxOWxEfrVFVZPIMTW4gL1JJwg1fiyqgfqCpUkDSGbSkzAnjklprCznLLVuf31Dch8OPPA/LyQXtNTRAxaZUIJ2B3OBC6viYo8ZgI2r1MHL62klQU5dpGcnpKxvD5L13RRlgDQ00vk98gI5RNpqajCdovMNomVPi6wWayuzEExR3CGbM7StSudWSVfkrEU2F2xodZuwkRiqcxusGqdZDlKUhPIjmBuKBLQ8HGOlGyrIiZj02RJrakapI5U3DUi638lQmVySLfVNWF4vpa587nfmFX7XJRpV5eYg1KyclnxEmfCo2stzsp9fIFTUL/y0rNpW18/3cddu4QI3jVygK9JZph+ZYod5IK+RhHv7j53lBmww6Rp6raoXR/Z3GWV+c0mK000N44Nk6LGmDKAzwH4VWvtwvWOV7970hhzzBhzrFZb37PAw8PDw2Nz2JCEbigF4OcA/Km19vPcPGGMGWHpfATA5Fq/tdY+BeApABgdHV3F6i1yIpGCylSXZp5LVLk0JlMG+kh6OxlINrjJGZJ8pkP5wnWX6St6zwNCdJw5R5KgKyKgicojR4gkOXLwrrTt/DhJJK+88r20bXqKg1S4CEKvclUbe4Uk+vEp+d4ZJnZDFeA0spfcv/bzF3tfl0hgeS5l1WzowAeSqLRb1Up84Bf+Zbrdu4ukppe+L1KwI5daSgqImaRzpdY0KeNKe8VaguC2YJkYwLlTOAvm1LS4KDq3OxVLgp5KD/dHJN2ZadZGWEqcmhICtMnaSUe5fcZcBjBUuVyKeZrnnHNp1BXZXfIeiPRUUFkkV2KOid7Ll8T9r8Rk9T2q4ILLSFnk/DSNumhVs7Pk3tpuyzhrnGulqNw+uyu07ks5+ltQZGfEUmesSNFOp8XnVdk7XfmztBiDKprAWm5bPXlRyKReolxpOZvk9FXSRKamxcXTZUWcVfl0nKaV6xJtaiWM1RI6/dVEoWGpVuc4SSVt/usISACoL1E/rlyRghiXL9P2fFGOy/A6ciR/SeWPKUZ0nCbIL3FRjVPn5J1Sr1MRl05M5xoYlGInDz5IAYpHDotEPzhIa6HSLc4duQJpEhZ8ffXsddIkjoqYvh2kqKGckh8HcNxa+7tq1xcBPMHbTwD4wqZ74+Hh4eFx09iIhP7DAH4RwPeMMc44/B8B/DaAzxhjPgTgAoCf/cF00cPDw8NjI7juC91a+7dYPyvkuzfbgTOnSc3Zd0TSX+YDTgPaEuIqYrVJiBEhUctctOGee8QP+G++8mUAQG1e/NWL/URenR4j69DePUKiHrybCi/klBp/aB/tn5sR9/pXuW5pwoTL2KyQRwtM5jZiMR8tzJFZZ0gRLuenqa1vL5kfpnPKJzphElWZV2zEtRQTUd9XelG/8OKxdPvl79F310BMOS5fRqSLMKSpYDN8jKjqEafb1elOXT6VrOpvwH7qoaV9laxEyQZslmqHyjzAkbPKbRhZzrXSrrF/dFVMVi0mDU1bRY+yzaelSPOYo0Gri3R8Ud3HwW7qR6RMHc6ysRY12jdI66RXFR5xBRoiNR+LS0RMLi1Rf3M5MZc4UlGnXx0dJjI8lxfzgCNDLecTqTakRw0mnOdmJb/Q9Az5eteVeedeTlOcYd/+5QUduN6pWk9NroU6lkZHiw95i81Ztaqcf36OTI9ZFfXqxv70176Wtr3jLQ9jGVTxhsT5l3dUhCabZJQ7PExqDqJ9oYqcfen55wAAS7Pi797P/vUXx6Wtwj70WX5uEhVhXSmzP7yKD8hGXBgkp+IwAjbjzpKZ6dxZicSem6V5e/6Yyt3DcRt790o07SgXjBkZpWd/dFjeNyVO020Kqt5psH5sxEbhI0U9PDw8dgi2PJfLi6dJWt73wGNpWwL6OhpNAvIXfoEJmrk5IW36+8hl772P/1ja9tAbKY/DZz7/F2mb4bwM3Vx9ffeouFyVmawLOyKZ9O2i6Rk5KFLWPBcneP5FkoLHl5S7VIYI2O4RIYoGDlPbssII7CZ4got2nL4iEmyW2aO6ioys8jR0EpEq3rPCSfTb3/xqul3jzHPZjCpdVnSkrNzy0HL+DlclPaMldOpHPqcIW3b7y6osfVGJxprP0jhzKh+FSxViVJZIR263VeGMBhOeqVSrI+z4eF3aLg3xVRJxT4m2u0s0pnJBpOBchs6XMXIfjXI/XIk2k3TazTFil8p4GdHnyu/x/CnROM9SeL0q46xzhsm68jl1mlCQcW5ssuZPHH8VAHD+3Lm0zUU5W+UOOTpCDgB9nPGyrrzJ3PbcrBCa00z61pUG7HIOOU+0uQXRkgKe+2Ika8fli7lyRTTglRJ6WxXVcKS86cg5XFSqdtazoDZHoi4tyWS5Yip3HxVt/pGHHgUAPPeyFL145lnKIjrHxVHijtyDoREiN9/+9renbRHf53PnxcX5mWcoF9QD91EUeqVbnCsmeMwTE+IA4NburmFxbzx48ABdnx0Lqovi9ukcDDKRaAWNNXIY3Si8hO7h4eGxQ+Bf6B4eHh47BFtucjk5Tyr9VKxSj2ZIBQ9aSkVJXA0++js6IjaHH/khIjTzGVFDD+6nyM+f/MAH07bP/sVf0bWu0HnH50XZazROAwCyEJV3pk7bp8+LWglWi+wgmXR6h8X8kNYVVNGYCZsnEiMmAJeMap4jOfMZlYSMU9hWjUouxWSkTbRKtlw9Gx6U6LnxOhFEcSxqdoXrnEaqbwtTRPYuLlS5X6KaJk5dXit6TZlVMgW6DzZD13eJ1QAgYJtLUSUrc5Xp4/Zqcxo4CZTJiu0iz+RmQZk/+rpITd2rYgD2jJD/r+M9mw1R1QNL6ylSkX09FVp3Ncm1leLkSUoJe//996VtBTah6OkImH5MODpwQkXJumRvzboya7AJMVZmlUOHDwAABoeo/7rwQobNPD0qUZYjVHWZTOdD/toJShu7pApiuH06hiFhk1J1Ueaoxv2scTRrS5nEXDGNCxNCPLoar/E16mDaZRGg1m2kcFGeKogViSNS+VYVVL3dH3nnu3mX/MAVrzj6kJhsH3gT1c11ZVcDRRO7AiyHDkm8ScRzeuCIpNkd3UdEc4EjjruVycWNyxVwAcSsMjQoacBdsq+QTVWBYn9jdnBoKztdYtafy43CS+geHh4eOwRbLqGfmKNvyhf+VqIxH9pP0squrBAGRZYSRnbRF3BkQKSWuw4xuWlFqhjnvCqf+PRfpW3PvUgkk4tEXRZ4aR0pJeeIc3SNWBN97ArYYYK1EyjS0M2mKiXVaPF51Zc4YoI0ZGnMqlwnHaaIMupr7kqRtdrrR5LZtkj03SWSOBYVsdqOSWq7594H5DejJK1McnTgpIoOXOK8Ljpdg5MsbSznLUUkhdzzRkpLelmVlru6QBpAvSUSY50LS+io1By7UpZYE+lRuUsGuYL7yKhIPod3k1vhUE7E1CV2dZxht74wK/NXLBEJXlYRuf2cv+PyWSHCHNos3TeWRMMJHBmpRExXvCJm18RTp06m+xbnHTEtj5grAhIp8TrhkMGAI22hXDH7WavSZGuNUy7X6zKnFy+OLTtOBR/CsotnrSX3zEnX1SnRgDPcT1fyr6MiKavstthRrpISabm+VFlX2knILpiRVRG8/Lx2VARvh+fBnV+XsXMCf0dpOK4cXEvlUBndx/mYEk5Rm6giEvycn70grqD1lssDpAqmdB9cdv3ZeblmxBJ3qXJABuvyIc3LmC9PzPA5qOM5lQ7cBcCasqyPxuz6ZRE3Ci+he3h4eOwQ+Be6h4eHxw7BlptcllgN+ZvnRV09+TpFj77nTUJK3TVKqv3ZMxSp+Y43i+kgz6r6YkvUuc/8NaXHfP5VSbBUc1FqbPIIVKpSpxYFKrrNmUlipc412RTSZpXQKN/mJkdcajIoilbXvyxyIqEsXAXydBdiJhV1UqwOE4jZLqnyszIX2vRlScQVt0l1qyt1uHaREpP1qQrrg5xWNsNVcgoqi1Y9dBVYtF1qtZpdq5OZ5h1cNer+eyV51YULZM6YnpNI26Yj2xSZFjHRXWAWa0ARoD2lEl9Z7sGVKRrLiSlJ0mSY2KoMkRmpUBHCtMgkqk7LW1Yk10oU+J61lFnDkdXL6mQ6/3M2V1QqEr2cZ5/+cklIvZDHVVTRps7Eceo1Suw2PyOmgHmO6IyVz3kmyxGraj3lWH83PH81FW06ycRdrSnqfMhj6O2W9dRi81yNneQ7KvlXkppXdP5Xng+zvkz4rW99XcbSoapBpUjmI+Z111ZmFUfMu4Rk+llqs2lLP4+OcGw0pS1OK2BxKmpVP7Svh8y55bKumEVj0PyuScfnEp6piE4ec6BMKBEn/QrM6uPcEJaFVxh+fxTl+KDB5kJFeN8ovITu4eHhsUOw5RJ6/wDlt5iZlc/jOEe1/T3X7QSAuL2ft+hLOLhLojxNSF/g7x6TaLG/+hpFejUTkQjAX+ogWP0di1lytOoz7dzRtJTgojwzLBkY/TnlPBSa9HK1KHXumZCvH1qWOKzSFFjK12L7yC6SJrsqSqqsLZfQd430pdtjF8Z4TLqYAG2fPXkibZpnd0J39apyi6yyNJTEy5hjOl4VE2g1SaJ7/m+/AgB4Z0nG+QCPs94t0rIjAXUUcIMJu3mO3tTk7PnXKBpvqi6Ri40MXb8wJGPu3UUSV65CYwpVpGiR3f5yRSHZTbj+0neusXFH7oGLMk46SlvjsTtStKAiKQPWGusqJ0pzhrTFC7o4Bc+DSyHr8uUAQp5n8kor4Eu0WjJ/i7MkkTcaS/xXiGx3p/JqzbfrnIJX1X91BKb7q8lI517YUdqJZak2m1mfqM+rSOV2yPdFpcTOsdNBolxdndtmwNfUJHTC+W60VuAiZhOrooB51NbV7TSKhObbF6i6uFHIKaubEtmaEqQ8PF2ztM0as9a63Zox6tlY+Z5pqahXy+doqNdHLiRtanR0P24WXkL38PDw2CHYcgndSbMZlQWw0yDp6uyESGXNKgV7vOMRqiBf6JGcCfNcDOKb35GMg3W2/bZVtrscu4056WOtCkqhkhbSj62yreVYsjNOVArU8TmSQgqq/JlzcWqrQJpFltpcUEZTSYLdveyyOSKJ8svsD1lXgSArP8X7jkomtwV24auOTakjOOueckeb4etmecwtZS8Xu+1qt7RlBQkYp16m/BkXF0XyGQxoPpZpOCy1LCl7/RVLUuFptqmOqRwgtSJrOPukwMDwQZJg8j3iupreB5aaymXRFIpsTw/UGrPXsP0ucJ6g2qK4LU5epjXZaEjfXPk4l8dD32On6QUqmCnDgW+OVwEkw2XENnftothmO7LOB9Ns0tpZVO5x7raVKuwOqyRD26Z5bi7JWndFMuaVROokc2efNspentjVwWUut41J1i+6kqj7uFQlHqUY6ntAf2O1mF0AVIvdcDsd5crHhTysksYlq6U8hx22ocdOG1T32gVVaeHZWupns6Fz28TLjteau035nFi1uaBCXSRm+TXDlu43587p1YVvaHsUXkL38PDw+EcP/0L38PDw2CG4rsnFGJMH8C1QTYUIwGettb9ljDkI4NMA+gA8D+AXrVWhmhtESjJpYjAk1bGlSJuJJVKLnj9BxNJ7a6ICLVoyRVyaFZNEnlXuTk3O0WAV09WAjFQUn9u3zC3NOLcnOc4Gy1POZnLigrbErl4tlYLXmV+02cGZWKocsVruEfNKL+eCaKmUn6+xS1tGuWu9aYVWVukVgnBwmPKrjCuTS6r+qd802azi6k1q18D4GhGAy/bwidusslenJN9HkOOUxMpl7jJf40WIOn464vkokxpf2itFMgZHKSdPPxedAIAcuwK2VE8smwVyEVe5jzQx7doUaXkN37Ar58iFVldhdyq40RG/nL7XVX/X6naWzTs6j43brwnHDpsYlpa45mtT51xhlzmjXQhpXWRVMYbh3aN8DoroXJgVN9EOF6ywioR25pRaS5thnDnD+dhh1fEZNXZXeKJWU2bAFbh4UZwUTo1TP0qqRmjEtqJ4WUkOmlMXDZoooj7LuX50mzPRxDq1Ec+zIy2NypHiyFZt23L5YPR9ce61SeyiSBXZySbKZTmbXAEPuzqy1f2yrfJExX20LnY/KK7Z3e6WbiKly0Yk9CaAd1lr3wjgIQCPG2PeCuB3APyetfYIgFkAH7r5bnh4eHh4bBYbKUFnATg/qwz/swDeBcCVmv8UgP8E4GM33ANHNujCARz8kqi8Dy6fytlJkgg+8Zkvp/ve9U5Kcn/2skiHVRcsoL5ZGZepjqWEonI7ynLhivqiSNeOuLCKtMwwQekkQE2EOUkwUQRKnV3UdJs7roel6n6VFP/qNAWWzE1Jhse58xRMdfjQQayHQl4kthwHsGRUPpOYyTH98e+kkguPT++8hpSwjCJjaWiJx/eakvq6uTzdaw0pBPAKay/TFZFc+/fSuEYOkjTeo1wwc+wGGah8HG1eK2GkSrmxRBylQTZyfCpda5eya5CiYcKue8p1NHUv1OdlbS2wTmKTczTZBbPTlvXkJG5dcd7BkeeZrC4RyGUDNanMazGfU+5/BfrNzDRdU2dRzLDGGerq8qyNdrQ0uYLUWxZI4wp+KK1niYuo1KqSD2YlAqvKFzppNRap1mkDy4KTQnZbtM41UGlaLBmrOKt07q1yTXQ3woqPYgonhWvX4g5fv62cAhJ+B1lXIlA9D2leJtURg9VjsUx+dziAsaLyEe15kJw7IiP3e+4k57PaI9rojWJDNnRjTMgFoicBfBXA6wDmrIQRjgHYvc5vnzTGHDPGHFvLq8TDw8PD49ZgQy90a21srX0IwB4AjwG4d63D1vntU9baR621jxZVbmMPDw8Pj1uLG/JDt9bOGWO+AeCtAHqMMRFL6XsAXL7mj9dBP1cqb6iCBFWOZMuG4s/t0mo6X+JvfvfldN9Zrm84VxVmZGaJ1GbFLaLE6nuH1a6cql7vVPV8QeWJCJyPsKj2zme2wyYGo/1TWQWLVYX6FvvJFlT+Dpdkv2+ATC0tRQg3uaBDPSfXTDh6UFeEX4m2iuiscj6Orh65ZqNKarYuoBCzephmbFWpW81qq0AKq9IDWyaUquwj/G1VlOR8jdqmVb6KaJgqoI/sGUzbDg7Sdn83zUugok2rLCc0FLEVseqva37mOQo04urr+YIIDzmeex2FeS0ka+QRccqoVaYfy2xyatJR53CRhrE2GfA60uvOrTFH0i6zeiVuPQmpHDP53MrIva1zWltnakk0Acq5XxpKO3bjstoX2x3vzBWqHxGPxbaEyJ6dJjNau7X+muwoP/SYj2sFmhB2eX10URRu4mcpUPfApchNtGmEzWKJSjftCGln/dDHO5OZtvIkzj9cmdicmSk1zWj/cjYLQRO2zmyj3gdtTmPddzcV09h9YG+6r8H1SF9/TWJnCm22bEsQ/A3juhK6MWbQGNPD2wUAPw7gOICvA/gAH/YEgC/cfDc8PDw8PDaLjUjoIwA+ZSghQgDgM9baLxljXgXwaWPMfwbwAoCP30wHGix15tSnpckSUiYUKbXDH0qXsD8oiBR3jsnQQJE2HZaeOorQbHBGuSpHamrix0lNpaxIcQUmSgMlVTjCsVCk6+ucGlc5U16i3JMiJkR6K0Ja7uojrWTXLiL/5qoiySxwZsKleYlS7OFCB1NXdeTnADTaqop9mKWx9w7KNdtlmstOW2W2S9xfJkyVhO6GrCMGU+lNs3+OuONshG2VQ6XZTf2+q0dInt4+iu4sV2TplYt033JMODdUvpQWuzlaJV2Hzt1U94O3M6xpabdFV7xBE2z2Gqxvg139Iu2u6lzhtOsjj90VutDraaXkzR2grupITp575zYYq8jLNs9DqDSzNucDiZV7balJmo2TzHWunWadpfs1SsUla0T8un5Eer653zMTkj+ozRGr+hasgh4653wJsnLNjMt2Gi+ryME/5blSp7MuQ6HSEPOsgfRWhEh3JedcQRY9pyG7mOaUBuzytCyLjuX74iJnFxdUHhZenkkkczTPqRSjAenH/qNEfPZy9Pel106n+6ZOU0bZSPUtf428OBvFRrxcXgbw8BrtZ0D2dA8PDw+POwA+UtTDw8Njh2DLk3M5lTCnkhgVHTHSFlXTuZkm7AWtEwYlrJ51WorEil0KTU1s0XaSpuiU79nsDJk6ZtQ1K1wYoVtFYVbYdz0PMse46t0AELFKGKpal01O5uQKJOjjOjWu1VhTSYzmpnnswubmOSKxcY3oxlCpaz39ZA4ql5QfepNNUMrk0omdb7rzPVaJxvhbHyxLB8pmBJVcKmIVusgmjq4uFcHIRQTKOSG3S+ybns2JutrizSX2m68rgtcRt3ml3mZD57MtanOwwpyh73uLSa9sVpFYmfXn0kX/BsqskXGmPm0u4b65GVpWtD2NHFTJq+LVxLSLlHaFLlotue91NrXEdRXRyaRoSZmlCt2k0nd4nO2GnCNYwyaS+uNrgtyFg7ApqqRiNKpcG3ZhQcyAzmKl18xKhB01x1y3M1ERwhbU3xAqZTBvS1StIjSNXfYXABJOvleLJJGfRHu79Ndqvjmau9GWvrm1bpb5sqed5DOpUFS+via8K5zKefCoxIoE/K468ex36JqTYjIN+f7pQiVrmcBuFF5C9/Dw8NghMPYWfBU2itHRUfvkk0/etut5eHh47AR89KMffc5a++j1jvMSuoeHh8cOgX+he3h4eOwQ+Be6h4eHxw6Bf6F7eHh47BDcVlLUGHMVQBXA1PWOvcMxgO09hu3ef2D7j2G79x/Y/mPYTv3fb60dvN5Bt/WFDgDGmGMbYWvvZGz3MWz3/gPbfwzbvf/A9h/Ddu//WvAmFw8PD48dAv9C9/Dw8Ngh2IoX+lNbcM1bje0+hu3ef2D7j2G79x/Y/mPY7v1fhdtuQ/fw8PDw+MHAm1w8PDw8dghu6wvdGPO4MeaEMea0MeYjt/PaNwNjzF5jzNeNMceNMa8YY36F2/uMMV81xpziv71b3ddrgYt8v2CM+RL//6Ax5jvc/z83xmSvd46thDGmxxjzWWPMa3wv3rYN78G/5zX0fWPMnxlj8nfyfTDGfMIYM2mM+b5qW3PODeG/83P9sjHmka3ruWCdMfwXXkcvG2P+wlVj432/wWM4YYz5p1vT683htr3QueLRHwB4D4D7APy8Mea+23X9m0QHwK9Za+8F1VH9Ze7zRwA8ba09AuBp/v+djF8BlQ10+B0Av8f9nwXwoS3p1cbx+wD+2lp7D4A3gsaybe6BMWY3gH8H4FFr7QOgWj4fxJ19Hz4J4PEVbevN+XsAHOF/TwL42G3q4/XwSawew1cBPGCtfQOAkwB+AwD4uf4ggPv5N//DLMunuz1wOyX0xwCcttaesda2AHwawPtv4/VvGNbacWvt87y9CHqR7Ab1+1N82KcA/MzW9PD6MMbsAfCTAP6Q/28AvAvAZ/mQO73/FQDvAJc4tNa2rLVz2Eb3gBEBKBhjIgBFAOO4g++DtfZbAGZWNK835+8H8MeW8AyogPzI7enp+lhrDNbar1hJUv8MpCTz+wF82lrbtNaeBXAa27Ai2+18oe8GcFH9f4zbtgWMMQdApfi+A2DYWjsO0EsfwNDW9ey6+G8A/gMAl+W/H8CcWtR3+n04BOAqgD9is9EfGmNK2Eb3wFp7CcB/BXAB9CKfB/Acttd9ANaf8+36bP9rAP+Xt7frGJbhdr7Q16qAui1cbIwxZQCfA/Cr1tqF6x1/p8AY81MAJq21z+nmNQ69k+9DBOARAB+z1j4MSh1xx5pX1gLbmt8P4CCAUQAlkJliJe7k+3AtbLc1BWPMb4JMqn/qmtY47I4ew1q4nS/0MQB71f/3ALh8G69/UzDGZEAv8z+11n6emyecSsl/J9f7/RbjhwG8zxhzDmTiehdIYu9h1R+48+/DGIAxa+13+P+fBb3gt8s9AIAfB3DWWnvVWtsG8HkAP4TtdR+A9ed8Wz3bxpgnAPwUgF+w4re9raMrqJEAAAF9SURBVMawHm7nC/1ZAEeY2c+CCIgv3sbr3zDY3vxxAMettb+rdn0RwBO8/QSAL9zuvm0E1trfsNbusdYeAM3316y1vwDg6wA+wIfdsf0HAGvtFQAXjTF3c9O7AbyKbXIPGBcAvNUYU+Q15cawbe4DY705/yKAX2Jvl7cCmHemmTsNxpjHAfw6gPdZa2tq1xcBfNAYkzPGHAQRvN/dij5uCtba2/YPwHtBzPLrAH7zdl77Jvv7dpDa9TKAF/nfe0F26KcBnOK/fVvd1w2M5Z0AvsTbh0CL9TSA/w0gt9X9u07fHwJwjO/DXwLo3W73AMBHAbwG4PsA/gRA7k6+DwD+DGTvb4Ok1w+tN+cgc8Uf8HP9PZA3z506htMgW7l7nv+nOv43eQwnALxnq/t/M/98pKiHh4fHDoGPFPXw8PDYIfAvdA8PD48dAv9C9/Dw8Ngh8C90Dw8Pjx0C/0L38PDw2CHwL3QPDw+PHQL/Qvfw8PDYIfAvdA8PD48dgv8P8QITwTAXGKoAAAAASUVORK5CYII=
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[22]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">correct</span> <span class="o">=</span> <span class="mi">0</span>
<span class="n">total</span> <span class="o">=</span> <span class="mi">0</span>
<span class="k">for</span> <span class="n">data</span> <span class="ow">in</span> <span class="n">testloader</span><span class="p">:</span>
    <span class="n">images</span><span class="p">,</span> <span class="n">labels</span> <span class="o">=</span> <span class="n">data</span>
    <span class="n">outputs</span> <span class="o">=</span> <span class="n">net</span><span class="p">(</span><span class="n">Variable</span><span class="p">(</span><span class="n">images</span><span class="p">))</span>
    <span class="n">_</span><span class="p">,</span> <span class="n">predicted</span> <span class="o">=</span> <span class="n">torch</span><span class="o">.</span><span class="n">max</span><span class="p">(</span><span class="n">outputs</span><span class="o">.</span><span class="n">data</span><span class="p">,</span> <span class="mi">1</span><span class="p">)</span>
    <span class="n">total</span> <span class="o">+=</span> <span class="n">labels</span><span class="o">.</span><span class="n">size</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span>
    <span class="n">correct</span> <span class="o">+=</span> <span class="p">(</span><span class="n">predicted</span> <span class="o">==</span> <span class="n">labels</span><span class="p">)</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Accuracy of the network on the 10000 test images: </span><span class="si">%d</span><span class="s1"> </span><span class="si">%%</span><span class="s1">&#39;</span> <span class="o">%</span> <span class="p">(</span>
    <span class="mi">100</span> <span class="o">*</span> <span class="n">correct</span> <span class="o">/</span> <span class="n">total</span><span class="p">))</span>

<span class="c1"># Okay... pretty good improvement. Again, before we prematurely optimize, let&#39;s add some pooling layers to make it quicker.</span>
<span class="c1"># THEN we&#39;ll go ham on the optimizations.</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">
<div class="prompt"></div>

<div class="output_subarea output_stream output_stdout output_text">
<pre>Accuracy of the network on the 10000 test images: 45 %
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><a id='twelve'></a></p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="12)--Adding-A-Pooling-Layer">12)  Adding A Pooling Layer<a class="anchor-link" href="#12)--Adding-A-Pooling-Layer">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Links:</p>
<ul>
<li><a href="https://www.quora.com/What-is-max-pooling-in-convolutional-neural-networks">https://www.quora.com/What-is-max-pooling-in-convolutional-neural-networks</a> - Quora; what is max pooling?</li>
<li><a href="http://pytorch.org/docs/master/_modules/torch/nn/modules/pooling.html">http://pytorch.org/docs/master/_modules/torch/nn/modules/pooling.html</a> - pytorch documentation on pooling</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h4 id="Home--|---Back--|---Next"><a href="#outline">Home</a>  |   <a href="#eleven">Back</a>  |   <a href="#thirteen">Next</a><a class="anchor-link" href="#Home--|---Back--|---Next">&#182;</a></h4>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[23]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># and again, boilerplate:</span>
<span class="n">transform</span> <span class="o">=</span> <span class="n">transforms</span><span class="o">.</span><span class="n">Compose</span><span class="p">(</span>
   <span class="p">[</span>
    <span class="n">transforms</span><span class="o">.</span><span class="n">ToTensor</span><span class="p">(),</span> 
    <span class="n">transforms</span><span class="o">.</span><span class="n">Normalize</span><span class="p">((</span><span class="mf">0.5</span><span class="p">,</span> <span class="mf">0.5</span><span class="p">,</span> <span class="mf">0.5</span><span class="p">),</span> <span class="p">(</span><span class="mf">0.5</span><span class="p">,</span> <span class="mf">0.5</span><span class="p">,</span> <span class="mf">0.5</span><span class="p">))</span> 
   <span class="p">])</span>
<span class="n">trainset</span> <span class="o">=</span> <span class="n">torchvision</span><span class="o">.</span><span class="n">datasets</span><span class="o">.</span><span class="n">CIFAR10</span><span class="p">(</span><span class="n">root</span><span class="o">=</span><span class="s1">&#39;./data&#39;</span><span class="p">,</span> <span class="n">train</span><span class="o">=</span><span class="kc">True</span><span class="p">,</span> <span class="n">download</span><span class="o">=</span><span class="kc">False</span><span class="p">,</span> <span class="n">transform</span><span class="o">=</span><span class="n">transform</span><span class="p">)</span>
<span class="n">trainloader</span> <span class="o">=</span> <span class="n">torch</span><span class="o">.</span><span class="n">utils</span><span class="o">.</span><span class="n">data</span><span class="o">.</span><span class="n">DataLoader</span><span class="p">(</span><span class="n">trainset</span><span class="p">,</span> <span class="n">batch_size</span><span class="o">=</span><span class="mi">4</span><span class="p">,</span> <span class="n">shuffle</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
<span class="n">testset</span> <span class="o">=</span> <span class="n">torchvision</span><span class="o">.</span><span class="n">datasets</span><span class="o">.</span><span class="n">CIFAR10</span><span class="p">(</span><span class="n">root</span><span class="o">=</span><span class="s1">&#39;./data&#39;</span><span class="p">,</span> <span class="n">train</span><span class="o">=</span><span class="kc">False</span><span class="p">,</span> <span class="n">download</span><span class="o">=</span><span class="kc">False</span><span class="p">,</span> <span class="n">transform</span><span class="o">=</span><span class="n">transform</span><span class="p">)</span>
<span class="n">testloader</span> <span class="o">=</span> <span class="n">torch</span><span class="o">.</span><span class="n">utils</span><span class="o">.</span><span class="n">data</span><span class="o">.</span><span class="n">DataLoader</span><span class="p">(</span><span class="n">testset</span><span class="p">,</span> <span class="n">batch_size</span><span class="o">=</span><span class="mi">4</span><span class="p">,</span> <span class="n">shuffle</span><span class="o">=</span><span class="kc">False</span><span class="p">)</span>
<span class="n">classes</span> <span class="o">=</span> <span class="p">(</span><span class="s1">&#39;plane&#39;</span><span class="p">,</span> <span class="s1">&#39;car&#39;</span><span class="p">,</span> <span class="s1">&#39;bird&#39;</span><span class="p">,</span> <span class="s1">&#39;cat&#39;</span><span class="p">,</span> <span class="s1">&#39;deer&#39;</span><span class="p">,</span> <span class="s1">&#39;dog&#39;</span><span class="p">,</span> <span class="s1">&#39;frog&#39;</span><span class="p">,</span> <span class="s1">&#39;horse&#39;</span><span class="p">,</span> <span class="s1">&#39;ship&#39;</span><span class="p">,</span> <span class="s1">&#39;truck&#39;</span><span class="p">)</span>

<span class="k">def</span> <span class="nf">imshow</span><span class="p">(</span><span class="n">img</span><span class="p">):</span>
    <span class="n">img</span> <span class="o">=</span> <span class="n">img</span> <span class="o">/</span> <span class="mi">2</span> <span class="o">+</span> <span class="mf">0.5</span>
    <span class="n">npimg</span> <span class="o">=</span> <span class="n">img</span><span class="o">.</span><span class="n">numpy</span><span class="p">()</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">imshow</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">transpose</span><span class="p">(</span><span class="n">npimg</span><span class="p">,</span> <span class="p">(</span><span class="mi">1</span><span class="p">,</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">0</span><span class="p">)))</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[24]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="k">class</span> <span class="nc">Net</span><span class="p">(</span><span class="n">nn</span><span class="o">.</span><span class="n">Module</span><span class="p">):</span>
    <span class="k">def</span> <span class="nf">__init__</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>
        <span class="nb">super</span><span class="p">(</span><span class="n">Net</span><span class="p">,</span> <span class="bp">self</span><span class="p">)</span><span class="o">.</span><span class="fm">__init__</span><span class="p">()</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">conv1</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Conv2d</span><span class="p">(</span><span class="mi">3</span><span class="p">,</span> <span class="mi">6</span><span class="p">,</span> <span class="mi">5</span><span class="p">)</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">pool</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">MaxPool2d</span><span class="p">(</span><span class="mi">2</span><span class="p">,</span> <span class="mi">2</span><span class="p">)</span> <span class="c1"># in any 2x2 square on each of our feature maps, take the most important (highest) one</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">fc1</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Linear</span><span class="p">(</span><span class="mi">1176</span><span class="p">,</span> <span class="mi">120</span><span class="p">)</span> <span class="c1"># since we&#39;ve pooled our outputs from the convolution, our input is reduced: 4704 -&gt; 1176</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">fc2</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Linear</span><span class="p">(</span><span class="mi">120</span><span class="p">,</span> <span class="mi">10</span><span class="p">)</span> 
        <span class="bp">self</span><span class="o">.</span><span class="n">sigmoid</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Sigmoid</span><span class="p">()</span>

    <span class="k">def</span> <span class="nf">forward</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">x</span><span class="p">):</span>
        <span class="n">x</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">conv1</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>
        <span class="n">x</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">sigmoid</span><span class="p">(</span><span class="n">x</span><span class="p">)</span> <span class="c1"># returns x of size: torch.Size([4, 6, 28, 28])</span>
        <span class="n">x</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">pool</span><span class="p">(</span><span class="n">x</span><span class="p">)</span> <span class="c1"># returns x of size: torch.Size([4, 6, 14, 14]) (so we have to adjust our linear input again)</span>
        <span class="n">x</span> <span class="o">=</span> <span class="n">x</span><span class="o">.</span><span class="n">view</span><span class="p">(</span><span class="o">-</span><span class="mi">1</span><span class="p">,</span> <span class="mi">1176</span><span class="p">)</span> <span class="c1"># now our input to the linear layer is going to be 4 by 6 * 14 * 14 = 1176</span>
        <span class="n">x</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">fc1</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>             
        <span class="n">x</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">sigmoid</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>
        <span class="n">x</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">fc2</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>
        <span class="n">x</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">sigmoid</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>
        <span class="k">return</span> <span class="n">x</span>

<span class="n">net</span> <span class="o">=</span> <span class="n">Net</span><span class="p">()</span>

<span class="n">NUMBER_OF_EPOCHS</span> <span class="o">=</span> <span class="mi">3</span>
<span class="n">LEARNING_RATE</span> <span class="o">=</span> <span class="mf">1e-1</span>
<span class="n">loss_function</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">CrossEntropyLoss</span><span class="p">()</span>
<span class="n">optimizer</span> <span class="o">=</span> <span class="n">optim</span><span class="o">.</span><span class="n">SGD</span><span class="p">(</span><span class="n">net</span><span class="o">.</span><span class="n">parameters</span><span class="p">(),</span> <span class="n">lr</span><span class="o">=</span><span class="n">LEARNING_RATE</span><span class="p">)</span>

<span class="k">for</span> <span class="n">epoch</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">NUMBER_OF_EPOCHS</span><span class="p">):</span>
    <span class="n">train_loader_iter</span> <span class="o">=</span> <span class="nb">iter</span><span class="p">(</span><span class="n">trainloader</span><span class="p">)</span>
    <span class="k">for</span> <span class="n">batch_idx</span><span class="p">,</span> <span class="p">(</span><span class="n">inputs</span><span class="p">,</span> <span class="n">labels</span><span class="p">)</span> <span class="ow">in</span> <span class="nb">enumerate</span><span class="p">(</span><span class="n">train_loader_iter</span><span class="p">):</span>
        <span class="n">net</span><span class="o">.</span><span class="n">zero_grad</span><span class="p">()</span>
        <span class="n">inputs</span><span class="p">,</span> <span class="n">labels</span> <span class="o">=</span> <span class="n">Variable</span><span class="p">(</span><span class="n">inputs</span><span class="o">.</span><span class="n">float</span><span class="p">()),</span> <span class="n">Variable</span><span class="p">(</span><span class="n">labels</span><span class="p">)</span>
        <span class="n">output</span> <span class="o">=</span> <span class="n">net</span><span class="p">(</span><span class="n">inputs</span><span class="p">)</span>
        <span class="n">loss</span> <span class="o">=</span> <span class="n">loss_function</span><span class="p">(</span><span class="n">output</span><span class="p">,</span> <span class="n">labels</span><span class="p">)</span>
        <span class="n">loss</span><span class="o">.</span><span class="n">backward</span><span class="p">()</span>
        <span class="n">optimizer</span><span class="o">.</span><span class="n">step</span><span class="p">()</span>
    <span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Iteration: &quot;</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">epoch</span> <span class="o">+</span> <span class="mi">1</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">
<div class="prompt"></div>

<div class="output_subarea output_stream output_stdout output_text">
<pre>Iteration: 1
Iteration: 2
Iteration: 3
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[25]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Pretty significant speedup! Let&#39;s see how it affects accuracy:</span>

<span class="n">dataiter</span> <span class="o">=</span> <span class="nb">iter</span><span class="p">(</span><span class="n">testloader</span><span class="p">)</span>
<span class="n">images</span><span class="p">,</span> <span class="n">labels</span> <span class="o">=</span> <span class="n">dataiter</span><span class="o">.</span><span class="n">next</span><span class="p">()</span>
<span class="n">imshow</span><span class="p">(</span><span class="n">torchvision</span><span class="o">.</span><span class="n">utils</span><span class="o">.</span><span class="n">make_grid</span><span class="p">(</span><span class="n">images</span><span class="p">))</span>
<span class="n">outputs</span> <span class="o">=</span> <span class="n">net</span><span class="p">(</span><span class="n">Variable</span><span class="p">(</span><span class="n">images</span><span class="p">))</span>
<span class="n">_</span><span class="p">,</span> <span class="n">predicted</span> <span class="o">=</span> <span class="n">torch</span><span class="o">.</span><span class="n">max</span><span class="p">(</span><span class="n">outputs</span><span class="o">.</span><span class="n">data</span><span class="p">,</span> <span class="mi">1</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Predicted: &#39;</span><span class="p">,</span> <span class="s1">&#39; &#39;</span><span class="o">.</span><span class="n">join</span><span class="p">(</span><span class="s1">&#39;</span><span class="si">%5s</span><span class="s1">&#39;</span> <span class="o">%</span> <span class="n">classes</span><span class="p">[</span><span class="n">predicted</span><span class="p">[</span><span class="n">j</span><span class="p">]]</span>
                              <span class="k">for</span> <span class="n">j</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">4</span><span class="p">)))</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;GroundTruth: &#39;</span><span class="p">,</span> <span class="s1">&#39; &#39;</span><span class="o">.</span><span class="n">join</span><span class="p">(</span><span class="s1">&#39;</span><span class="si">%5s</span><span class="s1">&#39;</span> <span class="o">%</span> <span class="n">classes</span><span class="p">[</span><span class="n">labels</span><span class="p">[</span><span class="n">j</span><span class="p">]]</span> <span class="k">for</span> <span class="n">j</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">4</span><span class="p">)))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">
<div class="prompt"></div>

<div class="output_subarea output_stream output_stdout output_text">
<pre>Predicted:    cat   car  ship  ship
GroundTruth:    cat  ship  ship plane
</pre>
</div>
</div>

<div class="output_area">
<div class="prompt"></div>



<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[26]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">correct</span> <span class="o">=</span> <span class="mi">0</span>
<span class="n">total</span> <span class="o">=</span> <span class="mi">0</span>
<span class="k">for</span> <span class="n">data</span> <span class="ow">in</span> <span class="n">testloader</span><span class="p">:</span>
    <span class="n">images</span><span class="p">,</span> <span class="n">labels</span> <span class="o">=</span> <span class="n">data</span>
    <span class="n">outputs</span> <span class="o">=</span> <span class="n">net</span><span class="p">(</span><span class="n">Variable</span><span class="p">(</span><span class="n">images</span><span class="p">))</span>
    <span class="n">_</span><span class="p">,</span> <span class="n">predicted</span> <span class="o">=</span> <span class="n">torch</span><span class="o">.</span><span class="n">max</span><span class="p">(</span><span class="n">outputs</span><span class="o">.</span><span class="n">data</span><span class="p">,</span> <span class="mi">1</span><span class="p">)</span>
    <span class="n">total</span> <span class="o">+=</span> <span class="n">labels</span><span class="o">.</span><span class="n">size</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span>
    <span class="n">correct</span> <span class="o">+=</span> <span class="p">(</span><span class="n">predicted</span> <span class="o">==</span> <span class="n">labels</span><span class="p">)</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Accuracy of the network on the 10000 test images: </span><span class="si">%d</span><span class="s1"> </span><span class="si">%%</span><span class="s1">&#39;</span> <span class="o">%</span> <span class="p">(</span>
    <span class="mi">100</span> <span class="o">*</span> <span class="n">correct</span> <span class="o">/</span> <span class="n">total</span><span class="p">))</span>

<span class="c1"># Not by much! Awesome!</span>
<span class="c1"># Now, let&#39;s add a few more layers, change our nonlinearities around, and do some other house keeping:</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">
<div class="prompt"></div>

<div class="output_subarea output_stream output_stdout output_text">
<pre>Accuracy of the network on the 10000 test images: 45 %
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><a id='thirteen'></a></p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="13)-Do-Some-Final-Optimizations-(i.e.-making-our-first-sigmoid-a-&quot;ReLU&quot;,--and-adding-more-layers)">13) Do Some Final Optimizations (i.e. making our first sigmoid a "ReLU",  and adding more layers)<a class="anchor-link" href="#13)-Do-Some-Final-Optimizations-(i.e.-making-our-first-sigmoid-a-&quot;ReLU&quot;,--and-adding-more-layers)">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Links:</p>
<ul>
<li><a href="https://github.com/Kulbear/deep-learning-nano-foundation/wiki/ReLU-and-Softmax-Activation-Functions">https://github.com/Kulbear/deep-learning-nano-foundation/wiki/ReLU-and-Softmax-Activation-Functions</a> - different activation functions</li>
<li><a href="https://stats.stackexchange.com/questions/126238/what-are-the-advantages-of-relu-over-sigmoid-function-in-deep-neural-networks">https://stats.stackexchange.com/questions/126238/what-are-the-advantages-of-relu-over-sigmoid-function-in-deep-neural-networks</a> - advantages of ReLU over sigmoid</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h4 id="Home--|---Back--|---Next"><a href="#outline">Home</a>  |   <a href="#twelve">Back</a>  |   <a href="#fourteen">Next</a><a class="anchor-link" href="#Home--|---Back--|---Next">&#182;</a></h4>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[27]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">transform</span> <span class="o">=</span> <span class="n">transforms</span><span class="o">.</span><span class="n">Compose</span><span class="p">(</span>
   <span class="p">[</span>
    <span class="n">transforms</span><span class="o">.</span><span class="n">ToTensor</span><span class="p">(),</span> 
    <span class="n">transforms</span><span class="o">.</span><span class="n">Normalize</span><span class="p">((</span><span class="mf">0.5</span><span class="p">,</span> <span class="mf">0.5</span><span class="p">,</span> <span class="mf">0.5</span><span class="p">),</span> <span class="p">(</span><span class="mf">0.5</span><span class="p">,</span> <span class="mf">0.5</span><span class="p">,</span> <span class="mf">0.5</span><span class="p">))</span> 
   <span class="p">])</span>
<span class="n">trainset</span> <span class="o">=</span> <span class="n">torchvision</span><span class="o">.</span><span class="n">datasets</span><span class="o">.</span><span class="n">CIFAR10</span><span class="p">(</span><span class="n">root</span><span class="o">=</span><span class="s1">&#39;./data&#39;</span><span class="p">,</span> <span class="n">train</span><span class="o">=</span><span class="kc">True</span><span class="p">,</span> <span class="n">download</span><span class="o">=</span><span class="kc">False</span><span class="p">,</span> <span class="n">transform</span><span class="o">=</span><span class="n">transform</span><span class="p">)</span>
<span class="n">trainloader</span> <span class="o">=</span> <span class="n">torch</span><span class="o">.</span><span class="n">utils</span><span class="o">.</span><span class="n">data</span><span class="o">.</span><span class="n">DataLoader</span><span class="p">(</span><span class="n">trainset</span><span class="p">,</span> <span class="n">batch_size</span><span class="o">=</span><span class="mi">4</span><span class="p">,</span> <span class="n">shuffle</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
<span class="n">testset</span> <span class="o">=</span> <span class="n">torchvision</span><span class="o">.</span><span class="n">datasets</span><span class="o">.</span><span class="n">CIFAR10</span><span class="p">(</span><span class="n">root</span><span class="o">=</span><span class="s1">&#39;./data&#39;</span><span class="p">,</span> <span class="n">train</span><span class="o">=</span><span class="kc">False</span><span class="p">,</span> <span class="n">download</span><span class="o">=</span><span class="kc">False</span><span class="p">,</span> <span class="n">transform</span><span class="o">=</span><span class="n">transform</span><span class="p">)</span>
<span class="n">testloader</span> <span class="o">=</span> <span class="n">torch</span><span class="o">.</span><span class="n">utils</span><span class="o">.</span><span class="n">data</span><span class="o">.</span><span class="n">DataLoader</span><span class="p">(</span><span class="n">testset</span><span class="p">,</span> <span class="n">batch_size</span><span class="o">=</span><span class="mi">4</span><span class="p">,</span> <span class="n">shuffle</span><span class="o">=</span><span class="kc">False</span><span class="p">)</span>
<span class="n">classes</span> <span class="o">=</span> <span class="p">(</span><span class="s1">&#39;plane&#39;</span><span class="p">,</span> <span class="s1">&#39;car&#39;</span><span class="p">,</span> <span class="s1">&#39;bird&#39;</span><span class="p">,</span> <span class="s1">&#39;cat&#39;</span><span class="p">,</span> <span class="s1">&#39;deer&#39;</span><span class="p">,</span> <span class="s1">&#39;dog&#39;</span><span class="p">,</span> <span class="s1">&#39;frog&#39;</span><span class="p">,</span> <span class="s1">&#39;horse&#39;</span><span class="p">,</span> <span class="s1">&#39;ship&#39;</span><span class="p">,</span> <span class="s1">&#39;truck&#39;</span><span class="p">)</span>

<span class="k">def</span> <span class="nf">imshow</span><span class="p">(</span><span class="n">img</span><span class="p">):</span>
    <span class="n">img</span> <span class="o">=</span> <span class="n">img</span> <span class="o">/</span> <span class="mi">2</span> <span class="o">+</span> <span class="mf">0.5</span>
    <span class="n">npimg</span> <span class="o">=</span> <span class="n">img</span><span class="o">.</span><span class="n">numpy</span><span class="p">()</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">imshow</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">transpose</span><span class="p">(</span><span class="n">npimg</span><span class="p">,</span> <span class="p">(</span><span class="mi">1</span><span class="p">,</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">0</span><span class="p">)))</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[28]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="k">class</span> <span class="nc">Net</span><span class="p">(</span><span class="n">nn</span><span class="o">.</span><span class="n">Module</span><span class="p">):</span>
    <span class="k">def</span> <span class="nf">__init__</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>
        <span class="nb">super</span><span class="p">(</span><span class="n">Net</span><span class="p">,</span> <span class="bp">self</span><span class="p">)</span><span class="o">.</span><span class="fm">__init__</span><span class="p">()</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">conv1</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Conv2d</span><span class="p">(</span><span class="mi">3</span><span class="p">,</span> <span class="mi">10</span><span class="p">,</span> <span class="mi">5</span><span class="p">)</span> <span class="c1"># Let&#39;s add more feature maps - that might help</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">pool</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">MaxPool2d</span><span class="p">(</span><span class="mi">2</span><span class="p">,</span> <span class="mi">2</span><span class="p">)</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">conv2</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Conv2d</span><span class="p">(</span><span class="mi">10</span><span class="p">,</span> <span class="mi">20</span><span class="p">,</span> <span class="mi">5</span><span class="p">)</span> <span class="c1"># And another conv layer with even more feature maps</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">fc1</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Linear</span><span class="p">(</span><span class="mi">20</span> <span class="o">*</span> <span class="mi">5</span> <span class="o">*</span> <span class="mi">5</span><span class="p">,</span> <span class="mi">120</span><span class="p">)</span> <span class="c1"># and finally, adjusting our first linear layer&#39;s input to our previous output</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">fc2</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Linear</span><span class="p">(</span><span class="mi">120</span><span class="p">,</span> <span class="mi">10</span><span class="p">)</span>

    <span class="k">def</span> <span class="nf">forward</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">x</span><span class="p">):</span>
        <span class="n">x</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">conv1</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>
        <span class="n">x</span> <span class="o">=</span> <span class="n">F</span><span class="o">.</span><span class="n">relu</span><span class="p">(</span><span class="n">x</span><span class="p">)</span> <span class="c1"># we&#39;re changing our nonlinearity / activation function from sigmoid to ReLU for a slight speedup</span>
        <span class="n">x</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">pool</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>
        <span class="n">x</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">conv2</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>
        <span class="n">x</span> <span class="o">=</span> <span class="n">F</span><span class="o">.</span><span class="n">relu</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>
        <span class="n">x</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">pool</span><span class="p">(</span><span class="n">x</span><span class="p">)</span> <span class="c1"># after this pooling layer, we&#39;re down to a torch.Size([4, 20, 5, 5]) tensor.</span>
        <span class="n">x</span> <span class="o">=</span> <span class="n">x</span><span class="o">.</span><span class="n">view</span><span class="p">(</span><span class="o">-</span><span class="mi">1</span><span class="p">,</span> <span class="mi">20</span> <span class="o">*</span> <span class="mi">5</span> <span class="o">*</span> <span class="mi">5</span><span class="p">)</span> <span class="c1"># so let&#39;s adjust our tensor again.</span>
        <span class="n">x</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">fc1</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>             
        <span class="n">x</span> <span class="o">=</span> <span class="n">F</span><span class="o">.</span><span class="n">relu</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>
        <span class="n">x</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">fc2</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>
        <span class="n">x</span> <span class="o">=</span> <span class="n">F</span><span class="o">.</span><span class="n">relu</span><span class="p">(</span><span class="n">x</span><span class="p">)</span>
        <span class="k">return</span> <span class="n">x</span>

<span class="c1"># net = Net()</span>
<span class="n">net</span> <span class="o">=</span> <span class="n">Net</span><span class="p">()</span><span class="o">.</span><span class="n">cuda</span><span class="p">()</span> <span class="c1"># Let&#39;s make our NN run on the GPU (I didn&#39;t splurge on this GTX 1080 for nothing...)</span>

<span class="n">NUMBER_OF_EPOCHS</span> <span class="o">=</span> <span class="mi">25</span> <span class="c1"># Let&#39;s also increase our training cycles</span>
<span class="n">LEARNING_RATE</span> <span class="o">=</span> <span class="mf">1e-2</span> <span class="c1"># And decrease our learning rate a little bit to compensate</span>
<span class="n">loss_function</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">CrossEntropyLoss</span><span class="p">()</span>
<span class="n">optimizer</span> <span class="o">=</span> <span class="n">optim</span><span class="o">.</span><span class="n">SGD</span><span class="p">(</span><span class="n">net</span><span class="o">.</span><span class="n">parameters</span><span class="p">(),</span> <span class="n">lr</span><span class="o">=</span><span class="n">LEARNING_RATE</span><span class="p">)</span>

<span class="k">for</span> <span class="n">epoch</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">NUMBER_OF_EPOCHS</span><span class="p">):</span>
    <span class="n">train_loader_iter</span> <span class="o">=</span> <span class="nb">iter</span><span class="p">(</span><span class="n">trainloader</span><span class="p">)</span>
    <span class="k">for</span> <span class="n">batch_idx</span><span class="p">,</span> <span class="p">(</span><span class="n">inputs</span><span class="p">,</span> <span class="n">labels</span><span class="p">)</span> <span class="ow">in</span> <span class="nb">enumerate</span><span class="p">(</span><span class="n">train_loader_iter</span><span class="p">):</span>
        <span class="n">net</span><span class="o">.</span><span class="n">zero_grad</span><span class="p">()</span>
        <span class="n">inputs</span><span class="p">,</span> <span class="n">labels</span> <span class="o">=</span> <span class="n">Variable</span><span class="p">(</span><span class="n">inputs</span><span class="o">.</span><span class="n">float</span><span class="p">()</span><span class="o">.</span><span class="n">cuda</span><span class="p">()),</span> <span class="n">Variable</span><span class="p">(</span><span class="n">labels</span><span class="o">.</span><span class="n">cuda</span><span class="p">())</span> <span class="c1"># Let&#39;s also make these tensors GPU compatible</span>
        <span class="n">output</span> <span class="o">=</span> <span class="n">net</span><span class="p">(</span><span class="n">inputs</span><span class="p">)</span>
        <span class="n">loss</span> <span class="o">=</span> <span class="n">loss_function</span><span class="p">(</span><span class="n">output</span><span class="p">,</span> <span class="n">labels</span><span class="p">)</span>
        <span class="n">loss</span><span class="o">.</span><span class="n">backward</span><span class="p">()</span>
        <span class="n">optimizer</span><span class="o">.</span><span class="n">step</span><span class="p">()</span>
    <span class="k">if</span> <span class="n">epoch</span> <span class="o">%</span> <span class="mi">5</span> <span class="ow">is</span> <span class="mi">0</span><span class="p">:</span>
        <span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Iteration: &quot;</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">epoch</span> <span class="o">+</span> <span class="mi">1</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">
<div class="prompt"></div>

<div class="output_subarea output_stream output_stdout output_text">
<pre>Iteration: 1
Iteration: 6
Iteration: 11
Iteration: 16
Iteration: 21
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[29]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">dataiter</span> <span class="o">=</span> <span class="nb">iter</span><span class="p">(</span><span class="n">testloader</span><span class="p">)</span>
<span class="n">images</span><span class="p">,</span> <span class="n">labels</span> <span class="o">=</span> <span class="n">dataiter</span><span class="o">.</span><span class="n">next</span><span class="p">()</span>
<span class="n">imshow</span><span class="p">(</span><span class="n">torchvision</span><span class="o">.</span><span class="n">utils</span><span class="o">.</span><span class="n">make_grid</span><span class="p">(</span><span class="n">images</span><span class="p">))</span>
<span class="n">outputs</span> <span class="o">=</span> <span class="n">net</span><span class="p">(</span><span class="n">Variable</span><span class="p">(</span><span class="n">images</span><span class="o">.</span><span class="n">cuda</span><span class="p">()))</span>
<span class="n">_</span><span class="p">,</span> <span class="n">predicted</span> <span class="o">=</span> <span class="n">torch</span><span class="o">.</span><span class="n">max</span><span class="p">(</span><span class="n">outputs</span><span class="o">.</span><span class="n">data</span><span class="p">,</span> <span class="mi">1</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Predicted: &#39;</span><span class="p">,</span> <span class="s1">&#39; &#39;</span><span class="o">.</span><span class="n">join</span><span class="p">(</span><span class="s1">&#39;</span><span class="si">%5s</span><span class="s1">&#39;</span> <span class="o">%</span> <span class="n">classes</span><span class="p">[</span><span class="n">predicted</span><span class="p">[</span><span class="n">j</span><span class="p">]]</span>
                              <span class="k">for</span> <span class="n">j</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">4</span><span class="p">)))</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;GroundTruth: &#39;</span><span class="p">,</span> <span class="s1">&#39; &#39;</span><span class="o">.</span><span class="n">join</span><span class="p">(</span><span class="s1">&#39;</span><span class="si">%5s</span><span class="s1">&#39;</span> <span class="o">%</span> <span class="n">classes</span><span class="p">[</span><span class="n">labels</span><span class="p">[</span><span class="n">j</span><span class="p">]]</span> <span class="k">for</span> <span class="n">j</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">4</span><span class="p">)))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">
<div class="prompt"></div>

<div class="output_subarea output_stream output_stdout output_text">
<pre>Predicted:    cat  ship plane plane
GroundTruth:    cat  ship  ship plane
</pre>
</div>
</div>

<div class="output_area">
<div class="prompt"></div>



<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[30]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">correct</span> <span class="o">=</span> <span class="mi">0</span>
<span class="n">total</span> <span class="o">=</span> <span class="mi">0</span>
<span class="k">for</span> <span class="n">data</span> <span class="ow">in</span> <span class="n">testloader</span><span class="p">:</span>
    <span class="n">images</span><span class="p">,</span> <span class="n">labels</span> <span class="o">=</span> <span class="n">data</span>
    <span class="n">inputs</span> <span class="o">=</span> <span class="n">Variable</span><span class="p">(</span><span class="n">images</span><span class="o">.</span><span class="n">cuda</span><span class="p">())</span>
    <span class="n">labels</span> <span class="o">=</span> <span class="n">labels</span><span class="o">.</span><span class="n">cuda</span><span class="p">()</span>
    <span class="n">outputs</span> <span class="o">=</span> <span class="n">net</span><span class="p">(</span><span class="n">inputs</span><span class="p">)</span>
    <span class="n">_</span><span class="p">,</span> <span class="n">predicted</span> <span class="o">=</span> <span class="n">torch</span><span class="o">.</span><span class="n">max</span><span class="p">(</span><span class="n">outputs</span><span class="o">.</span><span class="n">data</span><span class="p">,</span> <span class="mi">1</span><span class="p">)</span>
    <span class="n">total</span> <span class="o">+=</span> <span class="n">labels</span><span class="o">.</span><span class="n">size</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span>
    <span class="n">correct</span> <span class="o">+=</span> <span class="p">(</span><span class="n">predicted</span> <span class="o">==</span> <span class="n">labels</span><span class="p">)</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Accuracy of the network on the 10000 test images: </span><span class="si">%d</span><span class="s1"> </span><span class="si">%%</span><span class="s1">&#39;</span> <span class="o">%</span> <span class="p">(</span>
    <span class="mi">100</span> <span class="o">*</span> <span class="n">correct</span> <span class="o">/</span> <span class="n">total</span><span class="p">))</span>

<span class="c1"># Awesome! A lot better!</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">
<div class="prompt"></div>

<div class="output_subarea output_stream output_stdout output_text">
<pre>Accuracy of the network on the 10000 test images: 61 %
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p><a id='fourteen'></a></p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="14)--Bask...-in-the-glory-that-is-our-newly-created-Convolutional-Neural-Network-(CNN)!">14)  Bask... in the glory that is our newly created Convolutional Neural Network (CNN)!<a class="anchor-link" href="#14)--Bask...-in-the-glory-that-is-our-newly-created-Convolutional-Neural-Network-(CNN)!">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Links:</p>
<ul>
<li><a href="http://www.yaronhadad.com/deep-learning-most-amazing-applications/">http://www.yaronhadad.com/deep-learning-most-amazing-applications/</a> - stuff you can do now</li>
<li><a href="https://machinelearningmastery.com/inspirational-applications-deep-learning/">https://machinelearningmastery.com/inspirational-applications-deep-learning/</a> - more stuff you can do</li>
</ul>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h4 id="Home--|---Back"><a href="#outline">Home</a>  |   <a href="#thirteen">Back</a><a class="anchor-link" href="#Home--|---Back">&#182;</a></h4>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[31]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="c1"># Awesome - we have a full blown convolutional neural network!</span>
<span class="c1"># Let&#39;s condense some stuff and put it all together without comments:</span>

<span class="n">transform</span> <span class="o">=</span> <span class="n">transforms</span><span class="o">.</span><span class="n">Compose</span><span class="p">(</span>
   <span class="p">[</span>
    <span class="n">transforms</span><span class="o">.</span><span class="n">ToTensor</span><span class="p">(),</span> 
    <span class="n">transforms</span><span class="o">.</span><span class="n">Normalize</span><span class="p">((</span><span class="mf">0.5</span><span class="p">,</span> <span class="mf">0.5</span><span class="p">,</span> <span class="mf">0.5</span><span class="p">),</span> <span class="p">(</span><span class="mf">0.5</span><span class="p">,</span> <span class="mf">0.5</span><span class="p">,</span> <span class="mf">0.5</span><span class="p">))</span> 
   <span class="p">])</span>
<span class="n">trainset</span> <span class="o">=</span> <span class="n">torchvision</span><span class="o">.</span><span class="n">datasets</span><span class="o">.</span><span class="n">CIFAR10</span><span class="p">(</span><span class="n">root</span><span class="o">=</span><span class="s1">&#39;./data&#39;</span><span class="p">,</span> <span class="n">train</span><span class="o">=</span><span class="kc">True</span><span class="p">,</span> <span class="n">download</span><span class="o">=</span><span class="kc">False</span><span class="p">,</span> <span class="n">transform</span><span class="o">=</span><span class="n">transform</span><span class="p">)</span>
<span class="n">trainloader</span> <span class="o">=</span> <span class="n">torch</span><span class="o">.</span><span class="n">utils</span><span class="o">.</span><span class="n">data</span><span class="o">.</span><span class="n">DataLoader</span><span class="p">(</span><span class="n">trainset</span><span class="p">,</span> <span class="n">batch_size</span><span class="o">=</span><span class="mi">4</span><span class="p">,</span> <span class="n">shuffle</span><span class="o">=</span><span class="kc">True</span><span class="p">)</span>
<span class="n">testset</span> <span class="o">=</span> <span class="n">torchvision</span><span class="o">.</span><span class="n">datasets</span><span class="o">.</span><span class="n">CIFAR10</span><span class="p">(</span><span class="n">root</span><span class="o">=</span><span class="s1">&#39;./data&#39;</span><span class="p">,</span> <span class="n">train</span><span class="o">=</span><span class="kc">False</span><span class="p">,</span> <span class="n">download</span><span class="o">=</span><span class="kc">False</span><span class="p">,</span> <span class="n">transform</span><span class="o">=</span><span class="n">transform</span><span class="p">)</span>
<span class="n">testloader</span> <span class="o">=</span> <span class="n">torch</span><span class="o">.</span><span class="n">utils</span><span class="o">.</span><span class="n">data</span><span class="o">.</span><span class="n">DataLoader</span><span class="p">(</span><span class="n">testset</span><span class="p">,</span> <span class="n">batch_size</span><span class="o">=</span><span class="mi">4</span><span class="p">,</span> <span class="n">shuffle</span><span class="o">=</span><span class="kc">False</span><span class="p">)</span>
<span class="n">classes</span> <span class="o">=</span> <span class="p">(</span><span class="s1">&#39;plane&#39;</span><span class="p">,</span> <span class="s1">&#39;car&#39;</span><span class="p">,</span> <span class="s1">&#39;bird&#39;</span><span class="p">,</span> <span class="s1">&#39;cat&#39;</span><span class="p">,</span> <span class="s1">&#39;deer&#39;</span><span class="p">,</span> <span class="s1">&#39;dog&#39;</span><span class="p">,</span> <span class="s1">&#39;frog&#39;</span><span class="p">,</span> <span class="s1">&#39;horse&#39;</span><span class="p">,</span> <span class="s1">&#39;ship&#39;</span><span class="p">,</span> <span class="s1">&#39;truck&#39;</span><span class="p">)</span>

<span class="k">def</span> <span class="nf">imshow</span><span class="p">(</span><span class="n">img</span><span class="p">):</span>
    <span class="n">img</span> <span class="o">=</span> <span class="n">img</span> <span class="o">/</span> <span class="mi">2</span> <span class="o">+</span> <span class="mf">0.5</span>
    <span class="n">npimg</span> <span class="o">=</span> <span class="n">img</span><span class="o">.</span><span class="n">numpy</span><span class="p">()</span>
    <span class="n">plt</span><span class="o">.</span><span class="n">imshow</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">transpose</span><span class="p">(</span><span class="n">npimg</span><span class="p">,</span> <span class="p">(</span><span class="mi">1</span><span class="p">,</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">0</span><span class="p">)))</span>

<span class="k">class</span> <span class="nc">Net</span><span class="p">(</span><span class="n">nn</span><span class="o">.</span><span class="n">Module</span><span class="p">):</span>
    <span class="k">def</span> <span class="nf">__init__</span><span class="p">(</span><span class="bp">self</span><span class="p">):</span>
        <span class="nb">super</span><span class="p">(</span><span class="n">Net</span><span class="p">,</span> <span class="bp">self</span><span class="p">)</span><span class="o">.</span><span class="fm">__init__</span><span class="p">()</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">conv1</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Conv2d</span><span class="p">(</span><span class="mi">3</span><span class="p">,</span> <span class="mi">10</span><span class="p">,</span> <span class="mi">5</span><span class="p">)</span> 
        <span class="bp">self</span><span class="o">.</span><span class="n">pool</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">MaxPool2d</span><span class="p">(</span><span class="mi">2</span><span class="p">,</span> <span class="mi">2</span><span class="p">)</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">conv2</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Conv2d</span><span class="p">(</span><span class="mi">10</span><span class="p">,</span> <span class="mi">20</span><span class="p">,</span> <span class="mi">5</span><span class="p">)</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">fc1</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Linear</span><span class="p">(</span><span class="mi">20</span> <span class="o">*</span> <span class="mi">5</span> <span class="o">*</span> <span class="mi">5</span><span class="p">,</span> <span class="mi">120</span><span class="p">)</span>
        <span class="bp">self</span><span class="o">.</span><span class="n">fc2</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">Linear</span><span class="p">(</span><span class="mi">120</span><span class="p">,</span> <span class="mi">10</span><span class="p">)</span>

    <span class="k">def</span> <span class="nf">forward</span><span class="p">(</span><span class="bp">self</span><span class="p">,</span> <span class="n">x</span><span class="p">):</span>
        <span class="n">x</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">pool</span><span class="p">(</span><span class="n">F</span><span class="o">.</span><span class="n">relu</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">conv1</span><span class="p">(</span><span class="n">x</span><span class="p">)))</span>
        <span class="n">x</span> <span class="o">=</span> <span class="bp">self</span><span class="o">.</span><span class="n">pool</span><span class="p">(</span><span class="n">F</span><span class="o">.</span><span class="n">relu</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">conv2</span><span class="p">(</span><span class="n">x</span><span class="p">)))</span>
        <span class="n">x</span> <span class="o">=</span> <span class="n">x</span><span class="o">.</span><span class="n">view</span><span class="p">(</span><span class="o">-</span><span class="mi">1</span><span class="p">,</span> <span class="mi">20</span> <span class="o">*</span> <span class="mi">5</span> <span class="o">*</span> <span class="mi">5</span><span class="p">)</span>           
        <span class="n">x</span> <span class="o">=</span> <span class="n">F</span><span class="o">.</span><span class="n">relu</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">fc1</span><span class="p">(</span><span class="n">x</span><span class="p">)</span> <span class="p">)</span>
        <span class="n">x</span> <span class="o">=</span> <span class="n">F</span><span class="o">.</span><span class="n">relu</span><span class="p">(</span><span class="bp">self</span><span class="o">.</span><span class="n">fc2</span><span class="p">(</span><span class="n">x</span><span class="p">))</span>
        <span class="k">return</span> <span class="n">x</span>

<span class="n">net</span> <span class="o">=</span> <span class="n">Net</span><span class="p">()</span><span class="o">.</span><span class="n">cuda</span><span class="p">()</span>

<span class="n">NUMBER_OF_EPOCHS</span> <span class="o">=</span> <span class="mi">25</span>
<span class="n">LEARNING_RATE</span> <span class="o">=</span> <span class="mf">1e-2</span>
<span class="n">loss_function</span> <span class="o">=</span> <span class="n">nn</span><span class="o">.</span><span class="n">CrossEntropyLoss</span><span class="p">()</span>
<span class="n">optimizer</span> <span class="o">=</span> <span class="n">optim</span><span class="o">.</span><span class="n">SGD</span><span class="p">(</span><span class="n">net</span><span class="o">.</span><span class="n">parameters</span><span class="p">(),</span> <span class="n">lr</span><span class="o">=</span><span class="n">LEARNING_RATE</span><span class="p">)</span>

<span class="k">for</span> <span class="n">epoch</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">NUMBER_OF_EPOCHS</span><span class="p">):</span>
    <span class="n">train_loader_iter</span> <span class="o">=</span> <span class="nb">iter</span><span class="p">(</span><span class="n">trainloader</span><span class="p">)</span>
    <span class="k">for</span> <span class="n">batch_idx</span><span class="p">,</span> <span class="p">(</span><span class="n">inputs</span><span class="p">,</span> <span class="n">labels</span><span class="p">)</span> <span class="ow">in</span> <span class="nb">enumerate</span><span class="p">(</span><span class="n">train_loader_iter</span><span class="p">):</span>
        <span class="n">net</span><span class="o">.</span><span class="n">zero_grad</span><span class="p">()</span>
        <span class="n">inputs</span><span class="p">,</span> <span class="n">labels</span> <span class="o">=</span> <span class="n">Variable</span><span class="p">(</span><span class="n">inputs</span><span class="o">.</span><span class="n">float</span><span class="p">()</span><span class="o">.</span><span class="n">cuda</span><span class="p">()),</span> <span class="n">Variable</span><span class="p">(</span><span class="n">labels</span><span class="o">.</span><span class="n">cuda</span><span class="p">())</span>
        <span class="n">output</span> <span class="o">=</span> <span class="n">net</span><span class="p">(</span><span class="n">inputs</span><span class="p">)</span>
        <span class="n">loss</span> <span class="o">=</span> <span class="n">loss_function</span><span class="p">(</span><span class="n">output</span><span class="p">,</span> <span class="n">labels</span><span class="p">)</span>
        <span class="n">loss</span><span class="o">.</span><span class="n">backward</span><span class="p">()</span>
        <span class="n">optimizer</span><span class="o">.</span><span class="n">step</span><span class="p">()</span>
    <span class="k">if</span> <span class="n">epoch</span> <span class="o">%</span> <span class="mi">5</span> <span class="ow">is</span> <span class="mi">0</span><span class="p">:</span>
        <span class="nb">print</span><span class="p">(</span><span class="s2">&quot;Iteration: &quot;</span> <span class="o">+</span> <span class="nb">str</span><span class="p">(</span><span class="n">epoch</span> <span class="o">+</span> <span class="mi">1</span><span class="p">))</span>

<span class="n">dataiter</span> <span class="o">=</span> <span class="nb">iter</span><span class="p">(</span><span class="n">testloader</span><span class="p">)</span>
<span class="n">images</span><span class="p">,</span> <span class="n">labels</span> <span class="o">=</span> <span class="n">dataiter</span><span class="o">.</span><span class="n">next</span><span class="p">()</span>
<span class="n">imshow</span><span class="p">(</span><span class="n">torchvision</span><span class="o">.</span><span class="n">utils</span><span class="o">.</span><span class="n">make_grid</span><span class="p">(</span><span class="n">images</span><span class="p">))</span>
<span class="n">outputs</span> <span class="o">=</span> <span class="n">net</span><span class="p">(</span><span class="n">Variable</span><span class="p">(</span><span class="n">images</span><span class="o">.</span><span class="n">cuda</span><span class="p">()))</span>
<span class="n">_</span><span class="p">,</span> <span class="n">predicted</span> <span class="o">=</span> <span class="n">torch</span><span class="o">.</span><span class="n">max</span><span class="p">(</span><span class="n">outputs</span><span class="o">.</span><span class="n">data</span><span class="p">,</span> <span class="mi">1</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Predicted: &#39;</span><span class="p">,</span> <span class="s1">&#39; &#39;</span><span class="o">.</span><span class="n">join</span><span class="p">(</span><span class="s1">&#39;</span><span class="si">%5s</span><span class="s1">&#39;</span> <span class="o">%</span> <span class="n">classes</span><span class="p">[</span><span class="n">predicted</span><span class="p">[</span><span class="n">j</span><span class="p">]]</span>
                              <span class="k">for</span> <span class="n">j</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">4</span><span class="p">)))</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;GroundTruth: &#39;</span><span class="p">,</span> <span class="s1">&#39; &#39;</span><span class="o">.</span><span class="n">join</span><span class="p">(</span><span class="s1">&#39;</span><span class="si">%5s</span><span class="s1">&#39;</span> <span class="o">%</span> <span class="n">classes</span><span class="p">[</span><span class="n">labels</span><span class="p">[</span><span class="n">j</span><span class="p">]]</span> <span class="k">for</span> <span class="n">j</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="mi">4</span><span class="p">)))</span>

<span class="n">correct</span> <span class="o">=</span> <span class="mi">0</span>
<span class="n">total</span> <span class="o">=</span> <span class="mi">0</span>
<span class="k">for</span> <span class="n">data</span> <span class="ow">in</span> <span class="n">testloader</span><span class="p">:</span>
    <span class="n">images</span><span class="p">,</span> <span class="n">labels</span> <span class="o">=</span> <span class="n">data</span>
    <span class="n">labels</span> <span class="o">=</span> <span class="n">labels</span><span class="o">.</span><span class="n">cuda</span><span class="p">()</span>
    <span class="n">outputs</span> <span class="o">=</span> <span class="n">net</span><span class="p">(</span><span class="n">Variable</span><span class="p">(</span><span class="n">images</span><span class="o">.</span><span class="n">cuda</span><span class="p">()))</span>
    <span class="n">_</span><span class="p">,</span> <span class="n">predicted</span> <span class="o">=</span> <span class="n">torch</span><span class="o">.</span><span class="n">max</span><span class="p">(</span><span class="n">outputs</span><span class="o">.</span><span class="n">data</span><span class="p">,</span> <span class="mi">1</span><span class="p">)</span>
    <span class="n">total</span> <span class="o">+=</span> <span class="n">labels</span><span class="o">.</span><span class="n">size</span><span class="p">(</span><span class="mi">0</span><span class="p">)</span>
    <span class="n">correct</span> <span class="o">+=</span> <span class="p">(</span><span class="n">predicted</span> <span class="o">==</span> <span class="n">labels</span><span class="p">)</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span>
<span class="nb">print</span><span class="p">(</span><span class="s1">&#39;Accuracy of the network on the 10000 test images: </span><span class="si">%d</span><span class="s1"> </span><span class="si">%%</span><span class="s1">&#39;</span> <span class="o">%</span> <span class="p">(</span>
    <span class="mi">100</span> <span class="o">*</span> <span class="n">correct</span> <span class="o">/</span> <span class="n">total</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">
<div class="prompt"></div>

<div class="output_subarea output_stream output_stdout output_text">
<pre>Iteration: 1
Iteration: 6
Iteration: 11
Iteration: 16
Iteration: 21
Predicted:  truck   car plane plane
GroundTruth:    cat  ship  ship plane
Accuracy of the network on the 10000 test images: 62 %
</pre>
</div>
</div>

<div class="output_area">
<div class="prompt"></div>



<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>
</div>

</div>
    </div>
  </div>
</body>

 


</html>