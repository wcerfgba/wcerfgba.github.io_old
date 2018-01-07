---
title: "Additional information in Org-mode agenda views"
date: 2017-08-19T15:58:36+01:00
tags: ["emacs", "org-mode", "gtd", "lisp"]
---

Having recently started to read "Getting Things Done", I decided to have a look in to Emacs Org-mode. I now have an org file setup to manage all of my tasks, and it looks something like this:

~~~nohighlight
* TODO	Wash up.			:home:kitchen:
   SCHEDULED: <2017-08-17 Thu>
   :PROPERTIES:
   :CREATED:  <2017-08-13 Sun 15:56>
   :END:
   
* BLOCK	Email from Ben.			:email:

* Reading				:project:
** TODO	 Read GTD chapter 3.		:reading:

* Maybe
** Watch Funeral Parade of Roses.	:maybe:film:
   :PROPERTIES:
   :CREATED:  [2017-08-17 Thu 17:48]
   :END:
~~~

The general structure is to have a list of uncategorised items at the top, followed by project-based groupings underneath, and other sections such as my 'Maybe' list.

In addition to the tags you can see to the right of and the status keyword you can see at the beginning of some of the headings, Org-mode allows me to attach properties, such as a creation time and scheduled time, to each heading.

Additionally, Org-mode has 'agenda views', which allow you to create different views over your headings. One view -- `(org-tags-view)` -- allows me to search by tag and status, and display a list of all TODO items with a given tag or status. Another view -- `(org-agenda-month-view)` -- will show any tasks that are scheduled within the next month, and displays a heading for each day. You can also create a custom 'block view' which is constructed from many of these views.

I currently have a block view set up which shows a monthly agenda at the top, followed by all items with status NEXT, followed by all items with status TODO or BLOCK, ordered by CREATED time ascending, such that my TODO list is a queue. I am quite interested in the creation time, and would like to see this underneath each item in my TODO list.

In an agenda view you can call `M-x org-agenda-entry-text-show` and it will show some of the text from underneath that heading, but the properties are filtered out. By monkey-patching `(org-agenda-entry-text-show-here)`, we can write a function that displays whatever entry text we want.

~~~lisp
;; Save the original function, just in case.
(if (not (fboundp 'org-agenda-entry-text-show-here--vendor))
    (defalias 'org-agenda-entry-text-show-here--vendor
      (symbol-function 'org-agenda-entry-text-show-here)))

;; This is the function we are money-patching.
(defun org-agenda-entry-text-show-here ()
  "Add some text from the entry as context to the current line."
  (let (m txt o)
    (setq m (org-get-at-bol 'org-hd-marker))
    (unless (marker-buffer m)
      (error "No marker points to an entry here"))
    (setq txt (concat "\n" (org-agenda-entry-text-properties m)))
    (when (string-match "\\S-" txt)
      (setq o (make-overlay (point-at-bol) (point-at-eol)))
      (overlay-put o 'evaporate t)
      (overlay-put o 'org-overlay-type 'agenda-entry-content)
      (overlay-put o 'after-string txt))))

;; This function gets the entry text we want for the entry at marker POM.
(defun org-agenda-entry-text-properties (pom)
  (let* ((included '("CREATED"))
	 (includedp (lambda (prop) (not (eq nil (member (car prop) included)))))
	 (single-string (lambda (prop) (format (concat org-agenda-entry-text-leaders "%s: %s\n") (car prop) (cdr prop))))
	 (props (org-entry-properties pom))
	 (filtered-props (cl-remove-if-not includedp props))
	 (strings (cons "\n" (mapcar single-string filtered-props))))
    (apply 'concat strings)))
~~~