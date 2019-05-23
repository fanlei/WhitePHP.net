---
layout: post
title: "The Little PHPer - 2. Do It, Do It Again, and Again, and Again..."
---

<style>
.v-align-bottom {
    vertical-align: bottom;
}
</style>

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
                <pre>
(define foo
  (lambda (a b c) 
    (body
    )))
                </pre>
            </td>
            <td>
                <pre>
function foo        |       $foo = function
($a, $b, $c)        |       ($a, $b, $c) use (&$foo)
{return             |       {return
    body;           |           body;
}                   |       }</pre>
            </td>
        </tr>
        <tr class="v-align-bottom">
            <td>
                <pre>
(cond 
  (p1 e1)
  (p2 e2)
  ...
  (else en))</pre>
            </td>
            <td>
                <pre>
p1 ? e1 :
p2 ? e2 :
...
en;</pre>
            </td>
        </tr>
        <tr>
            <td>
                <code>
                    #t
                </code>
            </td>
            <td>
                <code>
                    TRUE
                </code>
            </td>
        </tr>
        <tr>
            <td>
                <code>
                    #f
                </code>
            </td>
            <td>
                <code>
                    FALSE
                </code>
            </td>
        </tr>
        <tr>
            <td>
                <code>
                (or ...)
                </code>
            </td>
            <td>
                <code>
                ... or ...
                </code>
            </td>
        </tr>
        <tr>
            <td>
                <pre>
(define lat?
  (lambda l
    (cond
      ((null? l) #t)
      ((atom? (car l)) (lat? (cdr l)))
      (else #f))))
                </pre>
            </td>
            <td>
            {%- highlight php -%}
function is_lat
($l)
{return 
    is_nulll($l) ? TRUE :
    is_atom(car($l)) ? is_lat(cdr($l)) :
    FALSE;
}
            {%- endhighlight -%}
            </td>
        </tr>
        <tr>
            <td>
                <pre>
(define member?
  (lambda (a lat)
    (cond
      ((null? lat) #f)
      (else (or (eq? (car lat) a)
              (member? a (cdr lat)))))))</pre>
            </td>
            <td>
            {%- highlight php -%}
function is_member
($a, $lat)
{return 
    is_nulll($l) ? FALSE :
    is_eq($a, car($lat)) or is_member($a, cdr($lat));
}
            {%- endhighlight -%}
            </td>
        </tr>
    </tbody>
</table>
