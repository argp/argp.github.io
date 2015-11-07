---
id: 51
title: ελληνικός ορθογράφος για το vim
author: argp
layout: post
guid: http://argp.gr/blog/?p=51
permalink: /2008/03/30/vim-spell-check/
categories:
  - greek
  - hacks
tags:
  - spell check
  - vim
---
Δυστυχώς η τελευταία έκδοση του vim δεν συμπεριλαμβάνει ελληνικό λεξικό για τον ενσωματωμένο ορθογράφο του. Ευτυχώς μπορούμε πολύ εύκολα να δημιουργήσουμε ένα χρησιμοποιώντας το ελληνικό λεξικό που παρέχει το OpenOffice:

<div class="wp_syntax">
  <table>
    <tr>
      <td class="code">
        <pre class="bash" style="font-family:monospace;">$ <span style="color: #7a0874; font-weight: bold;">cd</span> ~<span style="color: #000000; font-weight: bold;">/</span>
$ <span style="color: #c20cb9; font-weight: bold;">wget</span> http:<span style="color: #000000; font-weight: bold;">//</span>ftp.services.openoffice.org<span style="color: #000000; font-weight: bold;">/</span>pub<span style="color: #000000; font-weight: bold;">/</span>OpenOffice.org<span style="color: #000000; font-weight: bold;">/</span>contrib<span style="color: #000000; font-weight: bold;">/</span>dictionaries<span style="color: #000000; font-weight: bold;">/</span>el_GR.zip
$ <span style="color: #c20cb9; font-weight: bold;">unzip</span> el_GR.zip</pre>
      </td>
    </tr>
  </table>
</div>

Στη συνέχεια κάνουμε εκκίνηση του vim, και δίνουμε την παρακάτω εντολή:

<div class="wp_syntax">
  <table>
    <tr>
      <td class="code">
        <pre class="bash" style="font-family:monospace;">:mkspell el ~<span style="color: #000000; font-weight: bold;">/</span>el_GR</pre>
      </td>
    </tr>
  </table>
</div>

Αφού έχουμε κλείσει το vim βλέπουμε ότι έχει δημιουργηθεί το αρχείο `~/el.utf-8.spl`, το οποίο πρέπει να μεταφερθεί στον κατάλληλο κατάλογο:

<div class="wp_syntax">
  <table>
    <tr>
      <td class="code">
        <pre class="bash" style="font-family:monospace;">$ <span style="color: #c20cb9; font-weight: bold;">mkdir</span> <span style="color: #660033;">-p</span> ~<span style="color: #000000; font-weight: bold;">/</span>.vim<span style="color: #000000; font-weight: bold;">/</span>spell
$ <span style="color: #c20cb9; font-weight: bold;">mv</span> ~<span style="color: #000000; font-weight: bold;">/</span>el.utf-<span style="color: #000000;">8</span>.spl ~<span style="color: #000000; font-weight: bold;">/</span>.vim<span style="color: #000000; font-weight: bold;">/</span>spell
$ <span style="color: #c20cb9; font-weight: bold;">rm</span> <span style="color: #660033;">-f</span> el_GR.aff el_GR.dic el_GR.zip README_el_GR.txt</pre>
      </td>
    </tr>
  </table>
</div>

Από εδώ και πέρα τα πράγματα είναι απλά. Ο τρόπος με τον οποίο θα χρησιμοποιηθεί ο ελληνικός ορθογράφος κατά τη χρήση του vim είναι θέμα προσωπικής προτίμησης. Για λόγους πληρότητας παραθέτω παρακάτω τις συναφείς σειρές του `~/.vimrc` αρχείου μου (τα λεξικά `en_us` και `en_gb` συμπεριλαμβάνονται στο vim):

<div class="wp_syntax">
  <table>
    <tr>
      <td class="code">
        <pre class="bash" style="font-family:monospace;">map <span style="color: #000000; font-weight: bold;">&lt;</span>F8<span style="color: #000000; font-weight: bold;">&gt;</span> <span style="color: #000000; font-weight: bold;">&lt;</span>Esc<span style="color: #000000; font-weight: bold;">&gt;</span>:setlocal spell<span style="color: #000000; font-weight: bold;">!</span> <span style="color: #007800;">spelllang</span>=el<span style="color: #000000; font-weight: bold;">&lt;</span>CR<span style="color: #000000; font-weight: bold;">&gt;</span>
map <span style="color: #000000; font-weight: bold;">&lt;</span>F7<span style="color: #000000; font-weight: bold;">&gt;</span> <span style="color: #000000; font-weight: bold;">&lt;</span>Esc<span style="color: #000000; font-weight: bold;">&gt;</span>:setlocal spell<span style="color: #000000; font-weight: bold;">!</span> <span style="color: #007800;">spelllang</span>=en_us<span style="color: #000000; font-weight: bold;">&lt;</span>CR<span style="color: #000000; font-weight: bold;">&gt;</span>
map <span style="color: #000000; font-weight: bold;">&lt;</span>F6<span style="color: #000000; font-weight: bold;">&gt;</span> <span style="color: #000000; font-weight: bold;">&lt;</span>Esc<span style="color: #000000; font-weight: bold;">&gt;</span>:setlocal spell<span style="color: #000000; font-weight: bold;">!</span> <span style="color: #007800;">spelllang</span>=en_gb<span style="color: #000000; font-weight: bold;">&lt;</span>CR<span style="color: #000000; font-weight: bold;">&gt;</span></pre>
      </td>
    </tr>
  </table>
</div>