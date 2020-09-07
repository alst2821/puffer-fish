=======
 Emacs
=======

The example functions below use the prefix "pf-".

Function to copy file marked in dired to the kill-ring::

  (defun pf-copy-filename-as-kill (args)
      (interactive "P")
     (let ( (string
             (mapconcat
              (function identity) (dired-get-marked-files) " ")))
       (kill-new string)
       (message "%s" string)))
       
This gets the function above mapped to "K" in dired::

  (add-hook 'dired-load-hook
          (lambda ()
            (define-key dired-mode-map "K"
              'pf-copy-filename-as-kill)))

This function emulates vim-exec::

  (defun pf-emulate-vim-exec ()
       "Command to emulate vim's .! command"
       (interactive)
       (let (start end command result)
          (save-excursion
             (beginning-of-line)
             (setq start (point))
             (end-of-line)
             (setq end (point))
             (setq command (buffer-substring start end)) )
          (end-of-line)
          (setq result (shell-command-to-string command))
          (insert "\n")
          (setq start (point))
          (insert result)
          (setq end (point))
          (insert
           (concat
            (format "\n=== %d line(s) inserted\n" (count-lines start end))))
          ))

These functions are similar to vim's `*` command::

  (add-hook 'isearch-mode-hook 'pf-isearch-yank-word-hook)

  (defun pf-isearch-yank-word-hook ()
  (when (equal this-command 'pf-isearch-word-at-point)
    (let ((string (concat "\\<"
                          (buffer-substring-no-properties
                           (progn (skip-syntax-backward "w_") (point))
                           (progn (skip-syntax-forward "w_") (point)))
                          "\\>")))
      (if (and isearch-case-fold-search
               (eq 'not-yanks search-upper-case))
          (setq string (downcase string)))
      (setq isearch-string string
            isearch-message
            (concat isearch-message
                    (mapconcat 'isearch-text-char-description
                               string ""))
            isearch-yank-flag t)
      (isearch-search-and-update))))

  (defun pf-isearch-word-at-point ()
    (interactive)
    (call-interactively 'isearch-forward-regexp))

  (global-set-key (kbd "C-c *") 'pf-isearch-word-at-point)
  
