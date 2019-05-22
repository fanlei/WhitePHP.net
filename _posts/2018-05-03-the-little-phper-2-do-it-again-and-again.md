---
layout: post
title: "The Little PHPer - 2. Do It, Do It Again, and Again, and Again..."
---

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
            <td><pre lang="scheme">
(define foo
  (lambda (a b c) 
    (body
    )))
            </pre></td>
            <td><pre lang="php">
function foo(a, b, c) {
    return 
    body;
}
            </pre></td>
        </tr>
        <tr>
            <td><pre lang="scheme">
(cond 
  (p1 e1)
  (p2 e2)
  ...
  (else en))
            </pre></td>
            <td><pre lang="php">
p1 ? e1 :
p2 ? e2 :
...
en;
            </pre></td>
        </tr>
        <tr>
            <td>
                #t
            </td>
            <td>
                TRUE
            </td>
        </tr>
        <tr>
            <td>
                #f
            </td>
            <td>
                FALSE
            </td>
        </tr>
        <tr>
            <td><pre lang="scheme">
(or p1 p2 ... pn)
            </pre></td>
            <td><pre lang="php">
p2 or p2 ... or pn
            </pre></td>
        </tr>
        <tr>
            <td>
                lat?
            </td>
            <td><pre lang="php">
function is_lat($l) {
    return 
    is_nulll($l) ? TRUE :
    is_atom(car($l)) ? is_lat(cdr($l)) :
    FALSE;
}
            </pre></td>
        </tr>
        <tr>
            <td>
                member?
            </td>
            <td><pre lang="php">
function is_member($a, $lat) {
    return 
    is_nulll($l) ? FALSE :
    is_eq($a, car($lat)) or is_member($a, cdr($lat));
}
            </pre></td>
        </tr>
    </tbody>
</table>
