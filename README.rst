discover.el
===========

Discover more of emacs using context menus.

For in-depth information, including screenshots, please read my article on "discover.el: discover more of Emacs using context menus" here:

http://www.masteringemacs.org/articles/2013/12/21/discoverel-discover-emacs-context-menus/


Installation
------------

Install it from MELPA. It's called ``discover``.


Third-party module support
--------------------------
If you want to support ``discover.el`` you can use the following snippet as a baseline::

 (defconst myfeature-context-menus
   '((yasnippet
      (actions
       ("Snippet"
        ("C-n" "new snippet" yas-new-snippet)
        ("C-s" "insert snippet" yas-insert-snippet)
        ("C-v" "visit snippet file" yas-visit-snippet-file))))))

 (when (and (featurep 'discover) (featurep 'makey))
   (makey-initialize-key-groups myfeature-context-menus)
   ;; bind a key to the dynamically created command
   ;; `makey-key-mode-popup-yasnippet'
   (add-hook 'discover-mode-hook
             #'(lambda () (define-key discover-map (kbd "C-x &") 'makey-key-mode-popup-yasnippet))))

The example above creates one context menu called ``yasnippet``. Attached to it are three actions in the ``Snippet`` actions category. For more advanced examples you should read the source for ``discover.el``. It's very readable.

When ``makey-initialize-key-groups`` is called with the constant ``myfeature-context-menus`` the context menu is created. This is done dynamically when that function is called. They are named ``makey-key-mode-popup-<menu>`` where ``<menu>`` in the example above would be ``yasnippet``.

Finally, a hook is added to ``discover-mode-hook``. In it ``discover-map`` is updated so it overrides the ``C-x & ...`` keybindings yasnippet normally defines. When ``C-x &`` is pressed and ``discover-mode`` is running the context menu is displayed instead. (Please don't bind a lambda to the hook variable though.)

In the case of yasnippet overriding the global key group makes sense. But you must then decide how you want to present the context menu to the user for your own package. Binding the context menus to ``?`` or ``M-?`` where appropriate is another way. It depends on your package: do you have a dedicated interface like ``dired`` or do you expose your package to users through key bindings or minor modes?

Contribution
------------

Install Cask (https://github.com/cask/cask) if you haven't
already, then::

 $ cd /path/to/prodigy.el
 $ cask install

Use ``cask exec`` to run ``discover.el`` with its dependencies in ``load-path``.
