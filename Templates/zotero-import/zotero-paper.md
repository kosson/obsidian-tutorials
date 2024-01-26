---
alias: ''
type: '{%- if itemType %}{{itemType}}{%- endif %}'
ids: 
 - citekey: '{{citekey}}'{%- if DOI %}'
 - doi: {{DOI}} {%- endif %}
 - url: {{url}}{%- if ISBN %}
 - isbn: {{ISBN}} {%- endif %}
 - zotero:
    - {{localLibrary}}
    - {{cloudLibrary}}
event: ''
year: {%- if date %}{{date | format("YYYY")}}{%- endif %}
proceedings: {{proceedingsTitle}}
journal: {%- if itemType == "journalArticle" %}{{publicationTitle}}{%- endif %}{%- if volume %}
vol: {{volume}} {%- endif %}{%- if issue %}
issue: {{issue}} {%- endif %}{%- if itemType == "bookSection" %}
partof: {{publicationTitle}} {%- endif %}{%- if publisher %}
publisher: {{publisher}} {%- endif %}{%- if place %}
place: {{place}} {%- endif %}
tags: [{{allTags}}]
title: '{{title}}'
resources:
 - ''
author: [{{authors}}{{directors}}]
abstract: '{{abstractNote}}'
---
# {{title}}
{{authors}}

{%- if abstractNote -%}
      <h2>Abstract</h2>
	{{abstractNote}}
{%- endif %}

linkuri: {%- for attachment in attachments | filterby("path", "endswith", ".pdf") %}
[ replace(" ", " "|{{attachment.title}}](file://{{attachment.path%20)}})  {%- endfor -%}

<h2>Sublinieri</h2>

{%- macro calloutHeader(type, color) -%}  
{%- if type == "highlight" -%}  
<mark style="background-color: {{color}}">Citat</mark>  
{%- endif -%}
{%- if type == "text" -%}  
Notă:
{%- endif -%}  
{%- endmacro -%}

{% for annotation in annotations -%}
{%- if annotation.annotatedText -%}
<h3>{{calloutHeader(annotation.type, annotation.color)}}</h3>
	{{annotation.annotatedText | escape}}
	[pagina {{annotation.page}}](zotero://open-pdf/library/items/{{annotation.attachment.itemKey}}?page={{annotation.page}}&annotation={{annotation.id}})
{%- endif %}
{%- if annotation.imageRelativePath -%}		
![{{annotation.imageRelativePath}}]({{annotation.imageRelativePath}})
{%- endif %}
{%- if annotation.comment -%}
<em>Comentariu:</em> 
{{annotation.comment}}
{%- endif %}<br>
{% endfor -%}

<h2>Relations</h2>
{% for relation in relations | selectattr("citekey") %} [@{{relation.citekey}}](@{{relation.citekey}}){% if not loop.last %}, {% endif%} {% endfor %}

<h2>Links</h2>
{# Aici se vor realiza linkurile automat în cazul în care vor fi importate și lucrările cu care aceasta este înrudită. #}
{# Trucul este să pui numele fișierului dar să-i faci alias citekey-ul din Zotero pentru că acesta se comportă drept cheie comună între note. #}
{% for relation in relations | selectattr("citekey") %} [{{relation.citekey}}]({{relation.citekey}}){% if not loop.last %}, {% endif%} {% endfor %}
