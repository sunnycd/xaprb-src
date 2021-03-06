---
title: If yoda you were, SQL you would invent
date: "2013-02-01"
url: /blog/2013/02/01/if-yoda-you-were-sql-you-would-invent/
image: "/media/2013/02/34182677.jpg"
description: "Make sense, SQL does not."
categories:
  - Databases
---
SQL is such a bizarre language. It is all backwards. Consider:

	SELECT   item_id, COUNT(*) AS qty, SUM(qty * price) AS total
	FROM     line_item
	WHERE    invoice_id = 18743
	GROUP BY item_id
	HAVING   SUM(discount) > 0
	ORDER BY item_id;

What is the logical flow of this statement? If SQL were written in logical-flow order, it might look something like this:

	FROM     line_item
	WHERE    invoice_id = 18743
	RETRIEVE item_id, qty, price, discount
	GROUP BY item_id
	COMPUTE  item_id, COUNT(*) AS qty, SUM(qty * price) AS total, SUM(discount)
	HAVING   SUM(discount) > 0
	PROJECT  item_id, qty, total
	ORDER BY item_id;

SQL can get really hard to read and understand, really fast. Faster than any other language I can think of, and I've been programming in SQL for years. It's such a weird language. It's almost declarative, but it's not. It feels a little pseudo-functional, like LISP, but it's not. Even XSLT makes more sense than SQL!

I'm not the only one who's noticed this; see also [literate
SQL](https://modern-sql.com/use-case/literate-sql) by Markus Winand.

How many fewer bugs would SQL programmers write if they didn't have to do a mental translation between the Yoda-speak that is SQL and the logical operations the RDBMS executes? I'm not saying they should know the actual implementation, I'm just saying it'd be great if we didn't obfuscate things more than needed.

But George Lucas wouldn't like that, and I guess he was on the SQL committee.

![Yoda](/media/2013/02/34182677.jpg)

