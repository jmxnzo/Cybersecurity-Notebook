- **script-src**: Bestimmt, von welchen Domains externe Scripts geladen werden dürfen und ob Inline-Scripte erlaubt sind. Weiterhin kann hier _eval_ wieder erlaubt werden, was standardmäßig durch die CSP verboten ist.
- **object-src**: Besitmmt, von welchen Domains Flash und andere Plugins (Silverlight…) geladen werden – Gilt für die Tags _<object>_, _<embed>_ und _<applet>_
- **style-src**: Bestimmt, von welchen Domains CSS-Dateien geladen werden dürfen. Wichtig: Hier lässt sich nicht angeben, dass Inline-CSS supported werden soll. Das ist generell bei Verwendung der CSP ausgeschlossen.
- **img-src**: Bestimmt, von welchen Domains Bilder geladen werden dürfen. Gilt nicht nur für den _<img>_-Tag sondern auch für CSS-Background-Images.
- **media-src**: Bestimmt, von welchen Domains _<video>_ und _<audio>_-Elemente geladen werden.
- **frame-src**: Bestimmt, welche Seiten per Frame oder iframe eingebunden werden dürfen. _frame-src https://facebook.com_ würde nur facebook-(i)frames durchgehen lassen.
- **font-src**: Bestimmt, von welchen Domains externe Schriftarten mit der _@font-face_-Direktive geladen werden dürfen.
- **connect-src**: Bestimmt, zu welchen Seiten eine Verbindung per _WebSocket_ und _XHR_ erlaubt wird.

Content-Security-Policy: <CSP-Regeln hier>