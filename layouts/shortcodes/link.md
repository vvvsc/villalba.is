{{/* layouts/shortcodes/link.md */}}
{{ $slug := .Get 0 }}
{{ $targetPage := where .Site.Pages "Params.slug" $slug | first 1 }}
{{ if $targetPage }}
<a href="{{ (index $targetPage 0).RelPermalink }}">
{{ (index $targetPage 0).Title }}
</a>
{{ else }}
<span style="color:red">ERROR: Slug '{{ $slug }}' no encontrado</span>
{{ end }}
