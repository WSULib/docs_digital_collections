# Varnish for Loris

See [visual model](https://docs.google.com/drawings/d/1qUcbTBEo96QG51YEcVTsbcHFLmE9CO15Dub5Ht2EdNM/edit?usp=sharing)

## Configuration
* Varnish is listening on `6081`
* `lorisProxy` in Ouroboros points to `localhost:6081/loris_local`
* Loris's `TemplateHTTPResolver` is configured to look for Fedora behind Varnish @ `localhost:6081/fedora`
* (Forthcoming) Loris caching is turned off entirely
