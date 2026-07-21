# Negotiate

HTTP content negotiation: picks the best media type, charset, encoding, or language from a list your application supports, based on the client's `Accept*` request headers (RFC-style `q` weighting).

## Example

```php
use peels\negotiate\Negotiate;

$negotiate = Negotiate::getInstance($input); // $input implements InputInterface

// client sends: Accept: text/html, application/json;q=0.9
$type = $negotiate->media(['application/json', 'text/html']);
// => "text/html" (highest-quality match the app supports)

$charset = $negotiate->charset(['utf-8', 'iso-8859-1']); // defaults to "utf-8" if no match
$encoding = $negotiate->encoding(['gzip', 'br']);         // "identity" is always considered supported
$language = $negotiate->language(['en', 'fr']);           // matches "fr-FR" against "fr", etc.
```

Pass `strictMatch: true` to `media()`/`charset()` to get back an empty string instead of the first supported value when nothing matches.
