---
layout: post
title: "The Little PHPer - 10. What Is the Value of All of This?"
---

<style>
.post-title {
    font-size: 34px;
}
</style>

<ul>
<li>
<i>entry</i>: a pair of lists whose first list is a set, and also the two lists must be of equal length.
</li>
<li>
<i>table/environment</i>: a list of entries.
</li>
<li>
<i>application</i>: a list of expression whose <code class="primitive">car</code> position contains an expression whose value is a function.
</li>
</ul>
<table>
    <thead>
        <tr>
            <th>
                Scheme
            </th>
            <th>
                PHP
            </th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
            <code>
            new-entry
            </code>
            </td>
            <td>
            {%- highlight php -%}
use function build as new_entry;
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            lookup-in-entry
            </code>
            </td>
            <td>
            {%- highlight php -%}
function lookup_in_entry
($name, $entry, $entry_f) 
{return 
    lookup_in_entry_help($name,
                         first($entry), 
                         second($entry), 
                         $entry_f);
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            lookup-in-entry-help
            </code>
            </td>
            <td>
            {%- highlight php -%}
function lookup_in_entry_help
($name, $names, $values, $entry_f) 
{return
    is_nulll($names) ? $entry_f($name)
    : (is_eq(car($names), $name) ? car($values)
      : lookup_in_entry_help($name,
                             cdr($names), 
                             cdr($values),
                             $entry_f));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            extend-table
            </code>
            </td>
            <td>
            {%- highlight php -%}
use function cons as extend_table;
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            lookup-in-table
            </code>
            </td>
            <td>
            {%- highlight php -%}
function lookup_in_table
($name, $table, $table_f)
{return
    is_nulll($table) ? $table_f($name)
    : lookup_in_entry($name, car($table), 
                      function ($name) use ($table, $table_f)
                      {return 
                          lookup_in_table($name, 
                                          cdr($table), 
                                          $table_f);
                      });
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            atom-to-function
            </code>
            </td>
            <td>
            {%- highlight php -%}
function atom_to_action
($e)
{return
    is_number($e)
    ||  is_eq($e, '#t')
    ||  is_eq($e, '#f')
    ||  is_eq($e, 'cons')
    ||  is_eq($e, 'car')
    ||  is_eq($e, 'cdr')
    ||  is_eq($e, 'null?')
    ||  is_eq($e, 'eq?')
    ||  is_eq($e, 'atom?')
    ||  is_eq($e, 'zero?')
    ||  is_eq($e, 'add1?')
    ||  is_eq($e, 'sub1?')
    ||  is_eq($e, 'number?') ? 
      '_const'
    : '_identifier';
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            list-to-action
            </code>
            </td>
            <td>
            {%- highlight php -%}
function list_to_aciton 
($e)
{return
    is_atom(car($e)) ? 
        is_eq(car($e), 'quote') ? '_quote'
        : (is_eq(car($e), 'lambda') ? '_lambda' 
          : (is_eq(car($e), 'cond') ? '_cond'
            : '_application'))
    : '_application';
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            expression-to-action
            </code>
            </td>
            <td>
            {%- highlight php -%}
function expression_to_action
($e)
{return
    is_atom($e) ? atom_to_action($e)
    : list_to_aciton($e);
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            value
            </code>
            </td>
            <td>
            {%- highlight php -%}
function value
($e)
{return
    meaning($e, []);
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            meaning
            </code>
            </td>
            <td>
            {%- highlight php -%}
function meaning
($e, $table)
{return
    expression_to_action($e)($e, $table);
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            *const
            </code>
            </td>
            <td>
            {%- highlight php -%}
function _const
($e, $table)
{return
    is_number($e) ? $e
    : (is_eq($e, '#t') ? TRUE
      : (is_eq($e, '#f') ? FALSE
        : build('primitive', $e)));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            *quote
            </code>
            </td>
            <td>
            {%- highlight php -%}
function _quote
($e, $table)
{return
    text_of($e);
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            text-of
            </code>
            </td>
            <td>
            {%- highlight php -%}
use function second as text_of;
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            *identifier
            </code>
            </td>
            <td>
            {%- highlight php -%}
function _identifier
($e, $table) 
{return
    lookup_in_table($e, $table, 'initial_table');
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            initial-table
            </code>
            </td>
            <td>
            {%- highlight php -%}
function initial_table
($name)
{return
    car([]);
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            *lambda
            </code>
            </td>
            <td>
            {%- highlight php -%}
function _lambda
($e, $table)
{return
    build('non-primitive', cons($table, cdr($e)));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            table-of
            </code>
            </td>
            <td>
            {%- highlight php -%}
use function first as table_of;
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            formals-of
            </code>
            </td>
            <td>
            {%- highlight php -%}
use function second as formals_of;
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            body-of
            </code>
            </td>
            <td>
            {%- highlight php -%}
use function third as body_of;
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            evcon
            </code>
            </td>
            <td>
            {%- highlight php -%}
function evcon
($lines, $table)
{return
    is_else(question_of(car($lines))) ? 
      meaning(answer_of(car($lines)), $table)
    : (meaning(question_of(car($lines)), $table) ?
        meaning(answer_of(car($lines)), $table)
      : evcon(cdr($lines), $table));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            else?
            </code>
            </td>
            <td>
            {%- highlight php -%}
function is_else
($x)
{return
    is_atom($x) && is_eq($x, 'else');
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            question-of
            </code>
            </td>
            <td>
            {%- highlight php -%}
use function first as question_of;
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            answer-of
            </code>
            </td>
            <td>
            {%- highlight php -%}
use function second as answer_of;
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            *cond
            </code>
            </td>
            <td>
            {%- highlight php -%}
function _cond
($e, $table)
{return
    evcon(cond_lines_of($e), $table);
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            cond-line-of
            </code>
            </td>
            <td>
            {%- highlight php -%}
use function cdr as cond_lines_of;
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            *application
            </code>
            </td>
            <td>
            {%- highlight php -%}
function _application
($e, $table)
{return
    apply(meaning(function_of($e), $table),
          evlis(arguments_of($e), $table));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            evlis
            </code>
            </td>
            <td>
            {%- highlight php -%}
function evlis
($args, $table)
{return
    is_nulll($args) ? []
    : cons(meaning(car($args), $table),
           evlis(cdr($args), $table));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            function-of
            </code>
            </td>
            <td>
            {%- highlight php -%}
use function car as function_of;
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            arguments-of
            </code>
            </td>
            <td>
            {%- highlight php -%}
use function cdr as arguments_of;
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            primitive?
            </code>
            </td>
            <td>
            {%- highlight php -%}
function is_primitive
($l)
{return
    is_eq(first($l), 'primitive');
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            non-primitive?
            </code>
            </td>
            <td>
            {%- highlight php -%}
function is_non_primitive
($l)
{return
    is_eq(first($l), 'non-primitive');
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            apply
            </code>
            </td>
            <td>
            {%- highlight php -%}
function apply
($fun, $vals)
{return
    is_primitive($fun) ?
      apply_primitive(second($fun), $vals)
    : (is_non_primitive($fun) ?
        apply_closure(second($fun), $vals)
      : $fun);  // no answer
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            apply-primitive
            </code>
            </td>
            <td>
            {%- highlight php -%}
function apply_primitive
($name, $vals)
{return
    is_eq($name, 'car') ? car(first($vals))
    : (is_eq($name, 'cdr') ? cdr(first($vals))
    : (is_eq($name, 'cons') ? cons(first($vals), second($vals))
    : (is_eq($name, 'null?') ? is_nulll(first($vals))
    : (is_eq($name, 'atom?') ? _is_atom(first($vals))
    : (is_eq($name, 'eq?') ? is_eq(first($vals), second($vals))
    : (is_eq($name, 'zero?') ? is_zero(first($vals))
    : (is_eq($name, 'add1') ? add1(first($vals))
    : (is_eq($name, 'sub1') ? sub1(first($vals))
    : (is_eq($name, 'number?') ? is_number(first($vals))
    : $name))))))))); // no answer
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            :atom?
            </code>
            </td>
            <td>
            {%- highlight php -%}
function _is_atom
($s)
{return
    is_atom($s) ? TRUE
    : (is_nulll($s) ? FALSE
      : (is_eq(car($s), 'primitive') ? TRUE
        : (is_eq(car($s), 'non-primitive') ? TRUE
          : FALSE)));
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
            <code>
            apply-closure
            </code>
            </td>
            <td>
            {%- highlight php -%}
function apply_closure
($closure, $vals)
{return
    meaning(body_of($closure),
            extend_table(new_entry(formals_of($closure),
                                   $vals),
                         table_of($closure)));
}
            {%- endhighlight -%}
            </td>
        </tr>
    </tbody>
</table>
