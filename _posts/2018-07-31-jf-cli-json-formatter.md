---
layout: post
title: "jf: JSON Formatter in CLI"
---

It's easy to write a CLI tool of JSON Formatter by PHP, since a new <a href="https://www.php.net/manual/en/json.constants.php" target="_whitephp-ref">JSON constant</a> **JSON_PRETTY_PRINT** is available as of PHP 5.4.0. Essential implementation looks like:

{%- highlight php -%}
<?php

echo json_encode(json_decode(file_get_contents($argv[1])), 
                 $argv[2] ?? JSON_PRETTY_PRINT);
{%- endhighlight -%}

Latest source codes could be found in <a href="https://github.com/whitephp/json-formatter" target="_whitephp-ref">GitHub</a>.

Install it globally by using <a href="https://getcomposer.org/" target="_whitephp-ref">Composer</a>:

{%- highlight shell -%}
$ composer global require codegear/json-formatter
{%- endhighlight -%}

Suppose there is JSON data in data.json as below:
{%- highlight json -%}
{"id":"7108-1062","no_file":[{"Identifier":"61316","Name":"DHS800 Dissertation Tasks (Model)","Code":"DHS800-MOD"},{"Identifier":"126922","Name":"MGT301 Principles of Management (Model)","Code":"MGT301-MOD"}],"no_file_count":23}
{%- endhighlight -%}

Format file `data.json` and output to screen:

{%- highlight shell -%}
$ jf data.json
{%- endhighlight -%}

Format file `data.json` and save to another file `data_formatted.json`:

{%- highlight shell -%}
$ jf data.json > data_formatted.json
{%- endhighlight -%}

The JSON data after formatted would be like:
{%- highlight json -%}
{
    "id": "7108-1062",
    "no_file": [
        {
            "Identifier": "61316",
            "Name": "DHS800 Dissertation Tasks (Model)",
            "Code": "DHS800-MOD"
        },
        {
            "Identifier": "126922",
            "Name": "MGT301 Principles of Management (Model)",
            "Code": "MGT301-MOD"
        }
    ],
    "no_file_count": 23
}
{%- endhighlight -%}

It's possible to reverse the behavior, say, remove all the white-spaces by passing `0` as the 2nd parameter like:

{%- highlight shell -%}
$ jf data_formatted.json 0
{%- endhighlight -%}

Or,

{%- highlight shell -%}
$ jf data_formatted.json 0 > data.json
{%- endhighlight -%}

More options depend on the <a href="https://www.php.net/manual/en/json.constants.php" target="_whitephp-ref">JSON constants</a> provided.

### In VIM

Format current file:

{%- highlight viml -%}
:%!jf %
{%- endhighlight -%}

Or add a keymap in `vimrc`:

{%- highlight viml -%}
nnoremap <Leader>jf :%!jf %<CR>
{%- endhighlight -%}
