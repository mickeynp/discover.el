discover.el
===========

Discover more of emacs using context menus.

For in-depth information, including screenshots, please read my article on "discover.el: discover more of Emacs using context menus" here:

http://www.masteringemacs.org/articles/2013/12/21/discoverel-discover-emacs-context-menus/


Installation
------------

Install it from MELPA. It's called `discover`.


Third-party module support
--------------------------
If you want to support `discover.el` you can use the following snippet as a baseline::

 (defconst myfeature-context-menus
   '((yasnippet
      (actions
       ("Snippet"
        ("C-n" "new snippet" yas-new-snippet)
        ("C-s" "insert snippet" yas-insert-snippet)
        ("C-v" "visit snippet file" yas-visit-snippet-file))))))

 (when (featurep 'discover)
   (makey-initialize-key-groups myfeature-context-menus)
   ;; bind a key to the dynamically created command
   ;; `makey-key-mode-popup-yasnippet'
   )

The example above creates one context menu called `yasnippet`. Attached to it are three actions in the `Snippet` category. When `makey-initialize-key-groups` are run with `myfeature-context-menus` dynamic lisp commands are created. They are named `makey-key-mode-popup-<menu>` where `<menu>` in the example above would be `yasnippet`. For more example usage see the very readable `discover.el`!
