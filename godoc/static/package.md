{{with .PDoc}}{{if $.IsMain}}{{comment_text .Doc "" "    "}}{{else}}{{/*
---------------------------------------
*/}}## package {{.Name}}

  `import "{{.ImportPath}}"`{{$importPath := .ImportPath}}

## Overview

{{comment_text .Doc "" "    "}}
{{example_text $ "" "    "}}{{/*
---------------------------------------
*/}}## Index
{{if .Consts}}
- [Constants](#pkg-constants){{end}}{{if .Vars}}
- [Variables](#pkg-variables){{end}}{{range .Funcs}}{{$name_html := .Name}}
- [{{node_html $ .Decl false | sanitize}}](#{{$name_html}}){{end}}{{range .Types}}{{$tname_html := .Name}}
- [type {{$tname_html}}](#{{$tname_html}}){{range .Funcs}}{{$name_html := .Name}}
  - [{{node_html $ .Decl false | sanitize}}](#{{$name_html}}){{end}}{{range .Methods}}{{$name_html := .Name}}
  - [{{node_html $ .Decl false | sanitize}}](#{{$tname_html}}.{{$name_html}}){{end}}{{end}}{{if $.Notes}}{{range $marker, $item := $.Notes}}
- [{{noteTitle $marker}}s](#pkg-note-{{$marker}}){{end}}{{end}}{{/*
---------------------------------------
*/}}{{if $.Examples}}

### Examples
{{range $.Examples}}
- [{{example_name .Name}}](#example{{.Name}}){{end}}{{end}}{{/*
---------------------------------------
*/}}{{with .Filenames}}

### Package files
{{range .}} [{{.|filename}}]({{.|srcLink|formatSrcLink}}){{end}}

{{end}}{{/*
---------------------------------------
*/}}{{with .Consts}}<h2 id="pkg-constants">Constants</h2>

{{range .}}<pre>{{node_html $ .Decl true | replace `<a href="/pkg` `<a href="` -1}}</pre>

{{comment_text .Doc "" "    "}}
{{end}}{{end}}{{/*
---------------------------------------
*/}}{{with .Vars}}<h2 id="pkg-variables">Variables</h2>

{{range .}}<pre>{{node_html $ .Decl true | replace `<a href="/pkg` `<a href="` -1}}</pre>

{{comment_text .Doc "" "    "}}
{{end}}{{end}}{{/*
---------------------------------------
*/}}{{range .Funcs}}{{$name_html := html .Name}}{{/*
*/}}<h2 id="{{$name_html}}">func <a href="{{posLink_url $ .Decl | replace "target" $importPath 1 | formatSrcLink}}">{{$name_html}}</a>
    <a href="#{{$name_html}}">¶</a></h2>
<pre>{{node_html $ .Decl true | replace `<a href="/pkg` `<a href="` -1}}</pre>

{{comment_text .Doc "" "    "}}
{{example_text $ .Name "    "}}{{end}}{{/*
---------------------------------------
*/}}{{range .Types}}{{$tname := .Name}}{{$tname_html := html .Name}}{{/*
*/}}<h2 id="{{$tname_html}}">type <a href="{{posLink_url $ .Decl | replace "target" $importPath 1 | formatSrcLink}}">{{$tname_html}}</a>
    <a href="#{{$tname_html}}">¶</a></h2>
<pre>{{node_html $ .Decl true | replace `<a href="/pkg` `<a href="` -1}}</pre>

{{comment_text .Doc "" "    "}}
{{range .Consts}}<pre>{{node_html $ .Decl true | replace `<a href="/pkg` `<a href="` -1}}</pre>

{{comment_text .Doc "" "    "}}
{{end}}{{range .Vars}}<pre>{{node_html $ .Decl true | replace `<a href="/pkg` `<a href="` -1}}</pre>

{{comment_text .Doc "" "    "}}
{{range $name := .Names}}{{example_text $ $name "    "}}{{end}}{{end}}{{example_text $ $tname "    "}}{{/*
---------------------------------------
*/}}{{range .Funcs}}{{$name_html := html .Name}}{{/*
*/}}<h3 id="{{$name_html}}">func <a href="{{posLink_url $ .Decl | replace "target" $importPath 1 | formatSrcLink}}">{{$name_html}}</a>
    <a href="#{{$name_html}}">¶</a></h3>
<pre>{{node_html $ .Decl true | replace `<a href="/pkg` `<a href="` -1}}</pre>

{{comment_text .Doc "" "    "}}
{{example_text $ .Name "    "}}{{end}}{{/*
---------------------------------------
*/}}{{range .Methods}}{{$name_html := html .Name}}{{/*
*/}}<h3 id="{{$tname_html}}.{{$name_html}}">func ({{html .Recv}}) <a href="{{posLink_url $ .Decl | replace "target" $importPath 1 | formatSrcLink}}">{{$name_html}}</a>
    <a href="#{{$tname_html}}.{{$name_html}}">¶</a></h3>
<pre>{{node_html $ .Decl true | replace `<a href="/pkg` `<a href="` -1}}</pre>

{{comment_text .Doc "" "    "}}{{$name := printf "%s_%s" $tname .Name}}
{{example_text $ $name "    "}}{{end}}{{end}}{{end}}{{/*
---------------------------------------
*/}}{{$importPath := $.PDoc.ImportPath}}{{with $.Notes}}{{range $marker, $content := .}}{{/*
*/}}<h2 id="pkg-note-{{$marker}}">{{noteTitle $marker | html}}s</h2>

{{range $content}}- [☞]({{posLink_url $ . | replace "target" $importPath 1 | formatSrcLink}}){{comment_text .Body "  " "    "}}{{end}}
{{end}}{{end}}{{end}}{{/*
---------------------------------------
*/}}{{with .Dirs}}## Subdirectories
- [..](..){{range .List}}
- [{{.Path}}]({{.Path}}/{{modeQueryString $.Mode}}){{end}}{{end}}
